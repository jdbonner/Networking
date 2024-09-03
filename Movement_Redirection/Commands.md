# Commands


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









