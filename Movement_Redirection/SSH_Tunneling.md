# SSH TUNNELING AND COVERT CHANNELS
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html
> 112-CCTC19 - Networking

```
OUTCOMES
Discuss Local and Dynamic SSH Tunneling

Demonstrate Local and Dynamic Port Forward

Discuss Remote Port Forwarding

Demonstrate Remote Port Forwarding

Rationale
Understanding tunneling, covert channels, steganography,
and SSH tunneling is crucial for cybersecurity professionals
to comprehend various methods used for data encapsulation,
concealment, and secure communication. Tunneling involves
encapsulating one protocol within another, enabling secure
transmission of data across untrusted networks. Covert
channels allow clandestine communication by exploiting unused
or less-monitored network protocols or channels, posing a
significant risk for data exfiltration or command and control
activities. Steganography conceals secret information within
seemingly innocuous data, making it imperceptible to casual
observers. SSH tunneling provides a secure encrypted channel
for remote access and data transfer, safeguarding sensitive
information from interception or manipulation. Mastery of
these concepts equips cybersecurity practitioners with the
knowledge and tools necessary to detect, prevent, and mitigate
potential threats to data confidentiality, integrity, and
availability.
Assessment
You will be assessed via CTFd challenges where you will need to score 221/315 points to achieve a 70%.

```

## Overview of Tunneling
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_1_tunneling
- Tunneling - Tunneling encapsulates a protocol inside another protocol.
  - Encapsulation
  - Transmission
  - Decapsulation

### Overview of Tunneling
- Tunneling used in the IPv6 Transition
  - IPv6 over IPv4
  - Dual Stack
  - 6in4
  - 6to4
  - 4in6
  - Teredo
  - ISATAP

### Overview of Tunneling
- Traffic Tunneling
  - Mainly used for the IPv4 to IPv6 migration
- Tunneling Malware and Attacks
  - Bypass IPv4-based security measures

### IPv6 over IPv4
> RFC 3056
- Permits IPv6 to be encapsulated in order to move through a IPv4 network
- Done by the Dual Stack Router
- Payload is not generally encrypted
- IPSEC commonly used to secure the payloads

### Dual Stack
- Configures an IPv4 and IPv6 address on all devices
- Resource intensive
- Allows for IPv4 and IPv6 routing because it has the addresses already set
- Can use both but not interchangeably

### 6 in 4
- Tunnel IPv6 traffic in an IPv4 Generic Routing Encapsulation (GRE) tunnel
- Simple and deterministic
- Must be configured manually
- Commonly used for connecting IPv6 islands over an IPv4 network.
- Uses IP protocol 41

### 6 to 4
- Allows for IPv6 packets to be sent over an IPv4 network
- Enables automatic tunneling of IPv6 packets over an IPv4 network.
- Uses 6to4 gateways that encapsulate IPv6 packets within IPv4 packets.
- Allows communication between IPv6 networks across IPv4 infrastructure.
- Uses IP protocol 41


### 4 to 6
- Reverse of 6 to 4
- Uses Next Header 4


### Teredo Tunneling
- RFC 4380
- Allows IPv4 clients to access IPv6 clients
- Encapsulates IPv6 packets within UDP
- Commonly used for devices behind NAT
- Uses the 2001:0000::/32 prefix


### ISATAP
- Allows IPv6 hosts to communicate over an IPv4 network within a site (local network)
- Can be used over the internet for specific site-to-site communications.
- Generates a Link-Local address using its IPv4 address
- 192.168.199.99 → FE80::0000:5EFE:c0a8:c763


## Covert Channels vs Steganography
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_2_overview_of_covert_channels


### Covert Channels
- Using common and legitimate protocols to transfer data in illegitimate ways.
- Unauthorized/hidden communication between entities.
- Utilizes computer system resources, mechanisms, or protocols.
- Transmits information contrary to design intent.
- Bypasses security, violates policies, leaks sensitive data.


### Type of Covert Channels
- Storage
  - Payload
  - Header
    - IP Header (TOS, IP ID, Flags + Fragmentation, and Options)
    - TCP Header (Reserved, URG Pointer, and Options)

### Type of Covert Channels
- Timing
  - Modifying transmission of legitimate traffic
  - Delaying packets between nodes
  - Watch TTL changes
  - Watch for variances between transmissions

### Common Protocols used with Covert Channels
- ICMP    # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/icmp_tunnel.pcap
- DNS     # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/dnscat_tunnel.pcap
- HTTP


### How to Detect Covert Channels
- Host Analysis
  - Requires knowledge of each applications expected behavior.
- Network Analysis
  - A good understanding of your network and the common network protocols being used is the key
- Baselining of what is normal to detect what is abnormal

### Detecting Covert Channels with ICMP
- ICMP works with one request and one reply answer
  - Type 8 code 0 request
  - Type 0 code 0 answer
- Check for:
  - Payload imbalance
  - Request/responce imbalance
  - Large payloads in response

### ICMP Covert Channel Tools
- 1. ptunnel
- 2. Loki
- 3. 007shell
- 4. ICMP Backdoor
- 5. B0CK
- 6. Hans

### Detecting Covert Channels with DNS
- DNS is a request/response protocol
- 1 request typically gets 1 response
- Payloads generally do no exceed 512 bytes
- Check for:
  - Request/response imbalances
  - Unusual payloads
  - Burstiness or continuous use

### DNS Covert Channel Tools
- 1. OzymanDNS
- 2. NSTX
- 3. dns2tcp
- 4. iodine
- 5. heyoka
- 6. dnscat2

### Detecting Covert Channels with HTTP
- Request/Response protocol to pull web content
- GET request may include .png, .exe, .(anything) files
- Can vary in sizes of payloads
- Typically "bursty" but not steady

### HTTP Covert Channel Tools
- 1. tunnelshell tools
- 2. HTTPTunnel
- 3. SirTunnel
- 4. go HTTP tunnel


### Steganography
- Hiding messages inside legitimate information objects
  - Methods:
    - Injection
    - Substitution
    - Propagation

### Steganography Injection
- Done by inserting message into the unused (whitespace) of the file, usually in a graphic
- Second most common method
- Adds size to the file
- Hard to detect unless you have original file
- tools:
  - StegHide

### Steganography Substitution
- Done by inserting message into the insignificant portion of the file
- Most common method used
- Elements within a digital medium are replaced with hidden information
- Example
  - Change color pallate (+1/-1)

### Steganography Propagation
- Generates a new file entirely
- Needs special software to manipulate file
  - tools:
    - StegSecret
    - HyDEn
    - Spammimic


## Secure Shell (SSH)
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_4_secure_shell_ssh

### SSH
- Various Implementations (v1 and v2)
- Provides authentication, encryption, and integrity.
- Allows remote terminal sessions
- Can enable X11 Forwarding
- Used for tunneling and port forwarding
- Proxy connections


### SSH Architecture
- Client vs Server vs Session
- Keys:
  - User Key - Asymmetric public key used to identify the user to the server
  - Host Key - Asymmetric public key used to identify the server to the user
  - Session Key - Symmetric key created by the client and server to protect the session’s communication.

### Configuration Files
- Client Configuration File (/etc/ssh/ssh_config)
- Server Configuration File (/etc/ssh/sshd_config)
- Known Hosts File (~/.ssh/known_hosts)


### SSH Architecture
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ssh_architecture.png)


### SSH First Connect
```
student@internet-host:~$ ssh student@172.16.82.106
The authenticity of host '172.16.82.106 (172.16.82.106)' can't be established.
ECDSA key fingerprint is SHA256:749QJCG1sf9zJWUm1LWdMWO8UACUU7UVgGJIoTT8ig0.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '172.16.82.106' (ECDSA) to the list of known hosts.
student@172.16.82.106's password:
student@blue-host-1:~$
```
- You will need to approve the Server Host (Public) Key
- Key is saved to /home/student/.ssh/known_hosts

### SSH Re-Connect
```
ssh student@172.16.82.106
student@172.16.82.106's password:
student@blue-host-1:~$
```
- Further SSH connections to server will not prompt to save key as long as key does not change

### SH Host key Changed
```
ssh student@172.16.82.106
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:RO05vd7h1qmMmBum2IPgR8laxrkKmgPxuXPzMpfviNQ.
Please contact your system administrator.
Add correct host key in /home/student/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/student/.ssh/known_hosts:1
remove with:
ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
ECDSA host key for 172.16.82.106 has changed and you have requested strict checking.
Host key verification failed.
```

### SSH Key Change Fix
```ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"```
- Copy/Paste the ssh-geygen message to remove the Host key from the known_hosts file



## SSH Port Forwarding
- Creates channels using SSH-CONN protocol
- Allows for tunneling of other services through SSH
- Provides insecure services encryption


### SSH Options
- -L - Creates a port on the client mapped to a ip:port via the server
- -D - Creates a port on the client and sets up a SOCKS4 proxy tunnel where the target ip:port is specified dynamically
- -R - Creates the port on the server mapped to a ip:port via the client
- -NT - Do not execute a remote command and disable pseudo-tty (will hang window)


## Local Port Forwarding
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_5_1_local_port_forwarding
```
ssh -p <optional alt port> <user>@<server ip> -L <local bind port>:<tgt ip>:<tgt port> -NT
or
ssh -L <local bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server ip> -NT
```

### Local Port Forward to localhost of server
```
Internet_Host:
ssh student@172.16.1.15 -L 1122:localhost:22
or
ssh -L 1122:localhost:22 student@172.16.1.15
```
```
Internet_Host:
ssh student@localhost -p 1122
Blue_DMZ_Host-1~$
```

### Local Port Forward to localhost of server
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/local1.png)


### Local Port Forward to localhost of server
```
Internet_Host:
ssh student@172.16.1.15 -L 1123:localhost:23
or
ssh -L 1123:localhost:23 student@172.16.1.15
```
```
Internet_Host:
telnet localhost 1123
Blue_DMZ_Host-1~$
```

### Local Port Forward to localhost of server
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/local2.png)


### Local Port Forward to localhost of server
```
Internet_Host:
ssh student@172.16.1.15 -L 1180:localhost:80
or
ssh -L 1180:localhost:80 student@172.16.1.15
```
```
Internet_Host:
firefox http://localhost:1180
{Webpage of Blue_DMZ_Host-1}
```

### Local Port Forward to localhost of server
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/local3.png)


### Local Port Forward to remote target via server
```
Internet_Host:
ssh student@172.16.1.15 -L 2222:172.16.40.10:22
or
ssh -L 2222:172.16.40.10:22 student@172.16.1.15
```
```
Internet_Host:
ssh student@localhost -p 2222
Blue_INT_DMZ_Host-1~$
```


### Local Port Forward to remote target via server
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/local4.png)

### Local Port Forward to remote target via server
```
Internet_Host:
ssh student@172.16.1.15 -L 2223:172.16.40.10:23
or
ssh -L 2223:172.16.40.10:23 student@172.16.1.15
```
```
Internet_Host:
telnet localhost 2223
Blue_INT_DMZ_Host-1~$
```

### Local Port Forward to remote target via server
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/local5.png)

### Local Port Forward to remote target via server
```
Internet_Host:
ssh student@172.16.1.15 -L 2280:172.16.40.10:80
or
ssh -L 2280:172.16.40.10:80 student@172.16.1.15
```
```
Internet_Host:
firefox http://localhost:2280
{Webpage of Blue_INT_DMZ_Host-1}
```

### Local Port Forward to remote target via server
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/local6.png)


### Forward through Tunnel
```
Internet_Host:
ssh student@172.16.1.15 -L 2222:172.16.40.10:22
ssh student@localhost -p 2222 -L 3322:172.16.82.106:22
```
```
Internet_Host:
ssh student@localhost -p 3322
Blue_Host-1~$
```

### Forward through Tunnel
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/doublelocal1.png)

### Forward through Tunnel
```
Internet_Host:
ssh student@172.16.1.15 -L 2222:172.16.40.10:22
ssh student@localhost -p 2222 -L 3323:172.16.82.106:23
```
```
Internet_Host:
telnet localhost 3323
Blue_Host-1~$
```

### Forward through Tunnel
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/doublelocal2.png)


### Forward through Tunnel
```
Internet_Host:
ssh student@172.16.1.15 -L 2222:172.16.40.10:22
ssh student@localhost -p 2222 -L 3380:172.16.82.106:80
Internet_Host:
firefox http://localhost:3380
{Webpage of Blue_Host-1}
```
### Forward through Tunnel
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/doublelocal3.png)


## Dynamic Port Forwarding
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_5_2_dynamic_port_forwarding
```
ssh <user>@<server ip> -p <alt port> -D <port> -NT
or
ssh -D <port> -p <alt port> <user>@<server ip> -NT
```
- Proxychains default port is 9050
- Creates a dynamic socks4 proxy that interacts alone, or with a previously established remote or local port forward.
- Allows the use of scripts and other userspace programs through the tunnel.

### SSH Dynamic Port Forwarding 1-Step
```
Internet_Host:
ssh student@172.16.1.15 -D 9050
or
ssh -D 9050 student@172.16.1.15
```

### SSH Dynamic Port Forwarding 1-Step
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/dynamic1.png)

### SSH Dynamic Port Forwarding 1-Step
```
Internet_Host:
proxychains ./scan.sh
proxychains nmap -Pn 172.16.40.0/27 -p 21-23,80
proxychains ssh student@172.16.40.10
proxychains telnet 172.16.40.10
proxychains wget -r http://172.16.40.10
proxychains wget -r ftp://172.16.40.10
```

### SSH Dynamic Port Forwarding 2-Step
```
Internet_Host:
ssh student@172.16.1.15 -L 2222:172.16.40.10:22
or
ssh -L 2222:172.16.40.10:22 student@172.16.1.15
Internet_Host:
ssh student@localhost -p 2222 -D 9050
or
ssh -D 9050 student@localhost -p 2222
```

### SSH Dynamic Port Forwarding 2-Step
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/dynamic2.png)

### SSH Dynamic Port Forwarding 2-Step
```
Internet_Host:
proxychains ./scan.sh
proxychains nmap -Pn 172.16.82.96/27 -p 21-23,80
proxychains ssh student@172.16.82.106
proxychains telnet 172.16.82.106
proxychains wget -r http://172.16.82.106
proxychains wget -r ftp://172.16.82.106
```

## Remote Port Forwarding
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_5_3_remote_port_forwarding
```
ssh -p <optional alt port> <user>@<server ip> -R <remote bind port>:<tgt ip>:<tgt port> -NT

or

ssh -R <remote bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server ip> -NT
```

### Remote Port Forwarding from localhost of client
```
Blue_DMZ_Host-1:
ssh student@10.10.0.40 -R 4422:localhost:22
or
ssh -R 4422:localhost:22 student@10.10.0.40
Internet_Host:
ssh student@localhost -p 4422
Blue_DMZ_Host-1~$
```

### Remote Port Forwarding from localhost of client
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/remote1.png)


### Remote Port Forwarding from localhost of client
```
Blue_DMZ_Host-1:
ssh student@10.10.0.40 -R 4423:localhost:23
or
ssh -R 4423:localhost:23 student@10.10.0.40
Internet_Host:
telnet localhost 4423
Blue_DMZ_Host-1~$
```

### Remote Port Forwarding from localhost of client
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/remote2.png)


### Remote Port Forwarding from localhost of client
```
Blue_DMZ_Host-1:
ssh student@10.10.0.40 -R 4480:localhost:80
or
ssh -R 4480:localhost:80 student@10.10.0.40
Internet_Host:
firefox http://localhost:4480
{Webpage of Blue_DMZ_Host-1}
```

### Remote Port Forwarding from localhost of client
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/remote3.png)

### Remote Port Forwarding to remote target via client
```
Blue_DMZ_Host-1:
ssh student@10.10.0.40 -R 5522:172.16.40.10:22
or
ssh -R 5522:172.16.40.10:22 student@10.10.0.40
Internet_Host:
ssh student@localhost -p 5522
Blue_INT_DMZ_Host-1~$
```

### Remote Port Forwarding to remote target via client
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/remote4.png)

### Remote Port Forwarding to remote target via client
```
Blue_DMZ_Host-1:
ssh student@10.10.0.40 -R 5523:172.16.40.10:23
or
ssh -R 5523:172.16.40.10:23 student@10.10.0.40
Internet_Host:
telnet localhost 5523
Blue_INT_DMZ_Host-1~$
```

### Remote Port Forwarding to remote target via client
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/remote5.png)

### Remote Port Forwarding to remote target via client
```
Blue_DMZ_Host-1:
ssh student@10.10.0.40 -R 5580:172.16.40.10:80
or
ssh -R 5580:172.16.40.10:80 student@10.10.0.40
Internet_Host:
firefox http://localhost:5580
{Webpage of Blue_INT_DMZ_Host-1}
```

### Remote Port Forwarding to remote target via client
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/remote6.png)


## Combining Local and Remote Port Forwarding
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_5_4_combining_local_and_remote_port_forwarding


### Bridging Local and Remote Port Forwarding
```
Internet_Host:
ssh student@172.16.1.15 -L 2223:172.16.40.10:23 -NT
or
ssh -L 2223:172.16.40.10:23 student@172.16.1.15 -NT
Internet_Host:
telnet localhost 2223
Blue_INT_DMZ_Host-1~$
```
### Bridging Local and Remote Port Forwarding
```
Blue_INT_DMZ_Host-1:
ssh student@172.16.1.15 -R 1122:localhost:22
or
ssh -R 1122:localhost:22 student@172.16.1.15
```
### Bridging Local and Remote Port Forwarding
```
Internet_Host:
ssh student@172.16.1.15 -L 2222:localhost:1122
or
ssh -L 2222:localhost:1122 student@172.16.1.15
```
### Bridging Local and Remote Port Forwarding
```
Internet_Host:
ssh student@localhost -p 2222 -D 9050
or
ssh -D 9050 student@localhost -p 2222
```

### Bridging Local and Remote Port Forwarding
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/08_tunneling/assets/images/bridge.png)


### Bridging Local and Remote Port Forwarding
```
Internet_Host:
proxychains ./scan.sh
proxychains nmap -Pn -sT 172.16.82.96/27 -p 21-23,80
proxychains ssh student@172.16.82.106
proxychains telnet 172.16.82.106
proxychains wget -r http://172.16.82.106
proxychains wget -r ftp://172.16.82.106
```

## Perform SSH Practice
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_6_perform_ssh_practice

### Scan first pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp1.png)

### First Pivot External Active Recon
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp2.png)

### Enumerate first pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp3.png)

### Scan second pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp4.png)

### Enumerate second pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp5.png)


### Scan third pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp6.png)

### Enumerate third pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp7.png)

### Scan forth pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp8.png)

### Enumerate forth pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp9.png)

### Scan fifth pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp10.png)

### Enumerate fifth pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp11.png)

### Scan sixth pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp12.png)

### Enumerate sixth pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp13.png)


### Scan seventh pivot
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tp14.png)



## Network Recon Methodology
https://net.cybbh.io/public/networking/latest/08_tunneling/fg.html#_4_7_network_recon_methodology
- Define Objectives
- Perform Passive External Reconnaissance
- Perform Active External Reconnaissance
- Perform Passive Internal Reconnaissance
- Perform Active Internal Reconnaissance























































