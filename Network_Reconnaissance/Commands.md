# Commands
https://duckduckgo.com/
VYOS system creds
vyos
password

Entry Float IP: 10.50.37.85
Your Network Number is 2 (Given by Instructor)
Credentials: net2_studentX:passwordX
X is your student number


## Ping
- Ping one IP:
  - ping 172.16.82.106 -c 1
- Ping a range:
  - for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
> the ping sweep command is much faster to identify hosts in a network range. Utilize DuckDuckGo to find out the ip range for your ping sweep.



## NMAP
- Default Scan:
  - User: TCP Full Connect Scan (-sT)
  - Root: TCP SYN Scan (-sS)
- Default Ports scanned: 1000 most commonly used TCP or UDP ports
> default is full scan
> root is stealth scan 

### NMAP Scan Types
```
Broadcast Ping/Ping sweep (-sP, -PE)
SYN scan (-sS)
Full connect scan (-sT)
Null scan (-sN)
FIN scan (-sF)
XMAS tree scan (-sX)
UDP scan (-sU)    # Checking for the absence of an ICMP.
Idle scan (-sI)
Decoy scan (-D)
ACK/Window scan (-sA)
RPC scan (-sR)
FTP scan (-b)
OS fingerprinting scan (-O)
Version scan (-sV)
Discovery probes
-PE - ICMP Ping
-Pn - No Ping
```

### NMAP - Time-Out
- -T0 - Paranoid - 300 Sec
- -T1 - Sneaky - 15 Sec
- -T2 - Polite - 1 Sec
- -T3 - Normal - 1 Sec
- -T4 - Aggresive - 500 ms    # use this one
- -T5 - Insane - 250 ms%3CmxGraphModel%3E%3Croot%3E%3CmxCell%20id%3D%220%22%2F%3E%3CmxCell%20id%3D%221%22%20parent%3D%220%22%2F%3E%3CmxCell%20id%3D%222%22%20value%3D%22%26lt%3Bspan%20style%3D%26quot%3Bfont-family%3A%20-apple-system%2C%20BlinkMacSystemFont%2C%20%26amp%3Bquot%3BSegoe%20UI%26amp%3Bquot%3B%2C%20%26amp%3Bquot%3BNoto%20Sans%26amp%3Bquot%3B%2C%20Helvetica%2C%20Arial%2C%20sans-serif%2C%20%26amp%3Bquot%3BApple%20Color%20Emoji%26amp%3Bquot%3B%2C%20%26amp%3Bquot%3BSegoe%20UI%20Emoji%26amp%3Bquot%3B%3B%20font-size%3A%2016px%3B%20text-align%3A%20start%3B%20text-wrap%3A%20wrap%3B%20background-color%3A%20rgb(255%2C%20255%2C%20255)%3B%26quot%3B%26gt%3B10.50.26.79%26lt%3B%2Fspan%26gt%3B%22%20style%3D%22edgeLabel%3Bhtml%3D1%3Balign%3Dcenter%3BverticalAlign%3Dmiddle%3Bresizable%3D0%3Bpoints%3D%5B%5D%3B%22%20vertex%3D%221%22%20connectable%3D%220%22%20parent%3D%221%22%3E%3CmxGeometry%20x%3D%22241%22%20y%3D%22623.8095238095237%22%20as%3D%22geometry%22%2F%3E%3C%2FmxCell%3E%3C%2Froot%3E%3C%2FmxGraphModel%3E

## Traceroute

### Traceroute - Firewalking
traceroute 172.16.82.106
traceroute 172.16.82.106 -p 123
sudo traceroute 172.16.82.106 -I
sudo traceroute 172.16.82.106 -T
sudo traceroute 172.16.82.106 -T -p 443


## Netcat scanning

### Netcat - Scanning
```
nc [Options] [Target IP] [Target Port(s)]
```
- -z : Port scanning mode i.e. zero I/O mode
- -v : Be verbose [use twice -vv to be more verbose]
- -n : do not resolve ip addresses
- -w1 : Set time out value to 1
- -u : To switch to UDP

### Netcat - Horizontal Scanning
- Range of IPs for specific ports
- TCP
```
for i in {1..254}; do nc -nvzw1 172.16.82.$i 20-23 80 2>&1 & done | grep -E 'succ|open'
```
- UDP
```
for i in {1..254}; do nc -nuvzw1 172.16.82.$i 1000-2000 2>&1 & done | grep -E 'succ|open'
```

### Netcat - Vertical Scanning
- Range of ports on specific IP
- TCP
```
nc -nzvw1 172.16.82.106 21-23 80 2>&1 | grep -E 'succ|open'
```
- UDP
```
nc -nuzvw1 172.16.82.106 1000-2000 2>&1 | grep -E 'succ|open'
```


### Netcat - TCP Scan Script
```
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done
```


### Netcat - UDP Scan Script
```
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nuvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done
```

### Netcat - Banner Grabbing
- Find what is running on a particular port
```
nc [Target IP] [Target Port]
nc 172.16.82.106 22
nc -u 172.16.82.106 53
```
- -u : To switch to UDP

### Curl and Wget
- Both can be used to interact with the HTTP, HTTPS and FTP protocols.
- Curl - Displays ASCII
```
curl http://172.16.82.106
curl ftp://172.16.82.106
```
- Wget - Downloads (-r recursive)
```
wget -r http://172.16.82.106
wget -r ftp://172.16.82.106
```


### IP Configuration
```
Windows: ipconfig /all
Linux: ip address (ifconfig depreciated)
VyOS: show interface
```

### DNS configuration
```
Windows: ipconfig /displaydns
Linux: cat /etc/resolv.conf
```


### ARP Cache
```
Windows: arp -a
Linux: ip neighbor (arp -a depreciated)
```


### Network connections
```
Windows: netstat
Linux: ss (netstat depreciated)

Example options useful for both netstat and ss: -antp
a = Displays all active connections and ports.
n = No determination of protocol names. Shows 22 not SSH.
t = Display only TCP connections.
u = Display only UDP connections.
p = Shows which processes are using which sockets.
```

### Services File
```
Windows: %SystemRoot%\system32\drivers\etc\services
Linux/Unix: /etc/services
```
### OS Information
```
Windows: systeminfo
Linux: uname -a and /etc/os-release
```

### Running Processes
```
Windows: tasklist
Linux: ps or top

Example options useful for ps: -elf
e = Show all running processes
l = Show long format view
f = Show full format listing
```

### Command path
```
which
whereis
```

### Routing Table
```
Windows: route print
Linux: ip route (netstat -r deprecated)
VyOS: show ip route
```

### File search
```
find / -name hint* 2> /dev/null
find / -iname flag* 2> /dev/null
```
### SSH Config
```
Windows: C:\Windows\System32\OpenSSH\sshd_config
Linux: /etc/ssh/sshd_config
```

### ARP Scanning
```
arp-scan --interface=eth0 --localnet
nmap -sP -PR 172.16.82.96/27
```

### Ping Scanning
```
ping -c 1 172.16.82.106
for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
sudo nmap -sP 172.16.82.96/27
```

### DEV TCP Banner Grab
```
exec 3<>/dev/tcp/172.16.82.106/22; echo -e "" >&3; cat <&3
```

### DEV TCP Scanning
```
for p in {1..1023}; do(echo >/dev/tcp/172.16.82.106/$p) >/dev/null 2>&1 && echo "$p open"; done
```





which tcpdump ssh telnet wireshark ping










