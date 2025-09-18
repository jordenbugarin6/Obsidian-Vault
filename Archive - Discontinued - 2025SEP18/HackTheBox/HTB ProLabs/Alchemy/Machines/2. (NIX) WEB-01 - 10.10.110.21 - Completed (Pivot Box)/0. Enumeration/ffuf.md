```bash
┌──(kali㉿gobots)-[12Jun2024 16:29:35]-[~/SUT/Alchemy]                                                                                                                                                      
└─$ ffuf -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -u http://10.10.110.21/FUZZ                                                                                              
                                                                                                                                                                                                            
        /'___\  /'___\           /'___\                                                                                                                                                                     
       /\ \__/ /\ \__/  __  __  /\ \__/                                                                                                                                                                     
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\                                                                                                                                                                    
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/                                                                                                                                                                    
         \ \_\   \ \_\  \ \____/  \ \_\                                                                                                                                                                     
          \/_/    \/_/   \/___/    \/_/                                                                                                                                                                     
                                                                                                                                                                                                            
       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.110.21/FUZZ
 :: Wordlist         : FUZZ: /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

contact                 [Status: 200, Size: 10870, Words: 2449, Lines: 195, Duration: 60ms]
# Copyright 2007 James Fisher [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 66ms]
#                       [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 66ms]
# Attribution-Share Alike 3.0 License. To view a copy of this  [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 66ms]
#                       [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 67ms]
# or send a letter to Creative Commons, 171 Second Street,  [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 70ms]
# license, visit http://creativecommons.org/licenses/by-sa/3.0/  [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 72ms]
# on atleast 2 different hosts [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 70ms]
# Priority ordered case insensative list, where entries were found  [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 72ms]
#                       [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 75ms]
login                   [Status: 200, Size: 10390, Words: 2265, Lines: 186, Duration: 98ms]
                        [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 75ms]
#                       [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 75ms]
# Suite 300, San Francisco, California, 94105, USA. [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 76ms]
# This work is licensed under the Creative Commons  [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 86ms]
# directory-list-lowercase-2.3-medium.txt [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 82ms]
events                  [Status: 200, Size: 13335, Words: 3052, Lines: 224, Duration: 533ms]
store                   [Status: 200, Size: 12981, Words: 2643, Lines: 267, Duration: 188ms]
admin                   [Status: 500, Size: 21, Words: 3, Lines: 1, Duration: 64ms]
menu                    [Status: 200, Size: 37276, Words: 16508, Lines: 630, Duration: 195ms]
status                  [Status: 200, Size: 2, Words: 1, Lines: 1, Duration: 55ms]
masterclass             [Status: 200, Size: 18512, Words: 4558, Lines: 295, Duration: 74ms]
                        [Status: 200, Size: 19359, Words: 4244, Lines: 317, Duration: 50ms]
:: Progress: [207643/207643] :: Job [1/1] :: 980 req/sec :: Duration: [0:04:27] :: Errors: 0 ::

```