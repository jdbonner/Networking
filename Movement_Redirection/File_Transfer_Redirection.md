# FILE TRANSFER AND REDIRECTION
https://net.cybbh.io/public/networking/latest/09_file_transfer/fg.html


```
OUTCOMES
Describe Data Transfer and Exfiltration

Demonstrate File Transfer
Rationale
Learning standard file transfer protocols such as FTP,
SFTP, and SCP provides cybersecurity professionals with
essential knowledge of secure and reliable methods for
transferring files over networks, ensuring data integrity
and confidentiality. Understanding netcat and netcat relays
offers valuable insights into versatile tools commonly used
for creating network connections and transferring files,
both by defenders and malicious actors. Additionally,
familiarity with hex and base64 encoding techniques is
crucial for analyzing encoded data, which may conceal
sensitive information or malware payloads. Mastery of these
concepts equips cybersecurity practitioners with the skills
necessary to detect, prevent, and respond to file transfer-
related threats effectively, thereby bolstering the overall
security posture of their organizations.
Assessment
You will be assessed via CTFd challenges where you will need to score 28/40 points to achieve a 70%.
```

## Standard file transfer methods
- Describe common file transfer methods
- Understand the use of Active and Passive FTP modes
- Use SCP to transfer files

## Describe common methods for transferring data
- TFTP
- FTP
- Active
- Passive
- FTPS
- SFTP
- SCP



### TFTP
- Trivial File Transfer Protocol
- RFC 1350 Rev2    # https://tools.ietf.org/html/rfc1350
- UDP transport
- Extremely small and very simple communication
- No terminal communication
- Insecure (no authentication or encryption)
- No directory services
- Used often for technologies such as BOOTP and PXE


### FTP
- File Transfer Protocol
- RFC 959    # https://tools.ietf.org/html/rfc959
- Uses 2 separate TCP connections
- Control Connection (21) / Data Connection (20*)
- Authentication in clear-text
- Insecure in default configuration
- Has directory services
- Anonymous login


### FTP Active
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ftp_active.png)


### FTP Active for Anonymous
```
bob@bob-host:~$ ftp 10.0.0.104
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:bob): anonymous
331 Anonymous login ok, send your complete email address as your password
Password: (no password)
230-Welcome, archive user anonymous@10.0.0.101 !
230-
230-The local time is: Fri May 03 15:46:43 2024
230-
230-This is an experimental FTP server.  If you have any unusual problems,
230-please report them via e-mail to <root@james-host.novalocal>.
230-
230 Anonymous access granted, restrictions apply
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful
150 Opening ASCII mode data connection for file list
-rw-r--r--   1 ftp      ftp          8323 Dec 29 17:08 flag.png
-rw-r--r--   1 ftp      ftp            74 Dec 29 17:08 hint.txt
-rw-r--r--   1 ftp      ftp           170 Aug 30  2021 welcome.msg
226 Transfer complete
ftp>
```
### FTP Active for User
```
bob@bob-host:~$ ftp 10.0.0.104
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:bob): james
331 Password required for james
Password: (password)
230 User james logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful
150 Opening ASCII mode data connection for file list
226 Transfer complete
ftp>
```

### FTP Passive
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ftp_passive.png)


### FTP Passive with Wget
```
student@blue-internet-host:~$ proxychains wget -r ftp://10.0.0.104
ProxyChains-3.1 (http://proxychains.sf.net)
--2024-05-03 15:09:01--  ftp://10.0.0.104/
           => ‘10.0.0.104/.listing’
Connecting to 10.0.0.104:21... |S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:21-<><>-OK
connected.
Logging in as anonymous ... Logged in!
==> SYST ... done.    ==> PWD ... done.
==> TYPE I ... done.  ==> CWD not needed.
==> PASV ... |S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:32857-<><>-OK
done.    ==> LIST ... done.

{output omitted}

FINISHED --2024-05-03 15:09:01--
Total wall clock time: 0.03s
Downloaded: 3 files, 8.4K in 0s (23.5 MB/s)
```
### FTP Passive for Anonymous
```
student@blue-internet-host:~$ proxychains ftp 10.0.0.104
ProxyChains-3.1 (http://proxychains.sf.net)
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:21-<><>-OK
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:student): anonymous
331 Anonymous login ok, send your complete email address as your password
Password: (no password)
230-Welcome, archive user anonymous@10.0.0.101 !
230-
230-The local time is: Fri May 03 17:20:09 2024
230-
230-This is an experimental FTP server.  If you have any unusual problems,
230-please report them via e-mail to <root@james-host.novalocal>.
230-
230 Anonymous access granted, restrictions apply
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> passive
Passive mode on.
ftp> ls
227 Entering Passive Mode (10,0,0,104,162,147).
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:41619-<><>-OK
150 Opening ASCII mode data connection for file list
-rw-r--r--   1 ftp      ftp          8323 Dec 29 17:08 flag.png
-rw-r--r--   1 ftp      ftp            74 Dec 29 17:08 hint.txt
-rw-r--r--   1 ftp      ftp           170 Aug 30  2021 welcome.msg
226 Transfer complete
ftp>
```

### FTP Passive for User
```
student@blue-internet-host:~$ proxychains ftp 10.0.0.104
ProxyChains-3.1 (http://proxychains.sf.net)
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:21-<><>-OK
Connected to 10.0.0.104.
220 ProFTPD Server (Debian) [::ffff:10.0.0.104]
Name (10.0.0.104:student): james
331 Password required for james
Password: (password)
230 User james logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
500 Illegal PORT command
ftp: bind: Address already in use
ftp> passive
Passive mode on.
ftp> ls
227 Entering Passive Mode (10,0,0,104,168,167).
|S-chain|-<>-127.0.0.1:9050-<><>-10.0.0.104:43175-<><>-OK
150 Opening ASCII mode data connection for file list
226 Transfer complete
ftp>
```

### FTPS
> File Transfer Protocol Secure
- Adds SSL/TLS encryption to FTP
- Interactive terminal access
- Explicit Mode: ports 20/21*
  - Option for Encryption
- Implicit Mode: ports 989/990*
  - Encrytion assumed

### SFTP
- Secure File Transfer Protocol
- TCP transport (port 22)
- Uses symmetric and asymmetric encryption
- Adds FTP like services to SSH
- Authentication through sign in (username and password) or with SSH key
- Interactive terminal access






