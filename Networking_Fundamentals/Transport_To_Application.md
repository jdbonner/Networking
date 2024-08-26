# Transport to application layer

```
OUTCOMES
Explain OSI Layer 4 Ports, Protocols and Headers

Explain OSI Layer 5 Protocols and Headers

Explain OSI Layer 6 Functions and Responsibilities

Explain OSI Layer 7 Protocols and Headers

Rationale
Understanding OSI Layer 4, Layer 5, Layer 6, and Layer 7
protocols is vital for cybersecurity professionals as these
layers handle critical aspects of communication and data
manipulation. Layer 4 (Transport Layer) protocols like TCP
(Transmission Control Protocol) and UDP (User Datagram Protocol)
govern data transmission reliability and session establishment,
making them targets for exploitation by attackers aiming to
disrupt communication or perform unauthorized data access.
Layer 5 (Session Layer) and Layer 6 (Presentation Layer) protocols
define session management and data representation, respectively,
influencing how applications interact and process data. Layer 7
(Application Layer) protocols encompass a wide range of applications
and services, each potentially introducing vulnerabilities that
attackers can exploit to gain unauthorized access or compromise
data integrity. Mastery of these layers is essential for implementing
robust security measures to protect against various cyber threats
effectively.

Assessment
You will be assessed via CTFd challenges where you will need to score 193/275 points to achieve a 70%.
```

## Explain OSI Layer 4 ports
https://net.cybbh.io/public/networking/latest/03_transport/fg.html#_3_1_explain_osi_layer_4_ports_protocols_and_headers

### Describe Transport Layer Protocols
Connection-oriented
TCP - Segments
Unicast traffic

Connection-less
UDP - Datagrams
Broadcast, Multicast, or Unicast Traffic

### Port ranges
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/PortRanges.png)

### TCP reliability
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/TCPstates.png)

### TCP reliability
- 1. Connection establishment
  - 1. 3-way handshake
- 2. Data Transfer
  - 1. Established phase
- 3. Connection Termination
  - 1. 4-way Termination
  - 2. Reset connection

### TCP HEADERS
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/TCPHeader.png)

### TCP HEADERS
```
00 1f 29 5e 4d 26 00 50　56 bb 3a a0 08 00 45 00
00 3c 83 1b 40 00 40 06　15 0a c0 a8 14 46 4a 7d
83 1b d5 1d 00 19 6b 7f　c7 2d 00 00 00 00 a0 02
72 10 a2 b5 00 00 02 04　05 b4 04 02 08 0a 0a 99
44 36 00 00 00 00 01 03　03 07
```
### TCP FLAGS
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/TCPFlagsBPF.png)
- TCP Flag Breakout (Binary and Hex)
- Collection of Exceptionally Unskilled Attackers Pester Real Security Folks
- Coach Explained to the University of Alaska to Play Really Snowy Football

### TCP Flags Breakout
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/TCP_Flags_Breakout.png)

### TCP States
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/TCPchart.png)

### TCP Options
- 0 - End of Options
- 1 - No Options (NOP)
- 2 - Maximum Segment Size (MSS)
- 3 - TCP Windows Scaling
- 4 - Selective ACK (SACK) Permitted
- 5 - SACK
- 8 - TCP Timestamps

### UDP HEADERS
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/UDPHeader.png)

### UDP HEADERS
```
00 1f 29 5e 4d 26 00 50　56 bb 3a a0 08 00 45 00
00 3c 83 1b 40 00 40 11　15 0a c0 a8 14 46 4a 7d
83 1b dc de 00 35 00 36　7c 15 03 c4 01 20 00 01
00 00 00 00 00 01 04 6f　63 73 70 08 76 65 72 69
73 69 67 6e 03 6e 65 74　00 00 1c 00 01 00 00 29
10 00 00 00 00 00 00 00
```

## Explain OSI Layer 5 protocols and headers
https://net.cybbh.io/public/networking/latest/03_transport/fg.html#_3_2_explain_osi_layer_5_protocols_and_headers

### Virtual Private Networks (VPN)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/VPN_Connection.png)

### Virtual Private Networks (VPN)
- Types:
  - Remote Access(client-to-site)
  - Site-to-Site


### L2TP (UDP 1701)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/l2tp.png)
- RFC 2661
- Origins from Cisco L2F and Microsoft PPTP
- Tunnel only. No Encryption

### PPTP (TCP 1723)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/pptp.png)
- RFC 2637
- Microsoft
- Provides encryption
- Obsolete with many vulnerabilities

### L2F (UDP 1701)
![]()
- Cisco
- Tunnel only. No Encryption
- Requires L2F Network Server (LNS) and a L2F Access Concentrator (LAC)

### IPSec
- Modes: Transport or Tunnel
- Headers:
  - ESP (protocol 50)
  - AH (protocol 51)
  - IKE (UDP port 500 or 4500)


### IPSec - Transport
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ipsectrans.png)


### IPSec - Tunnel
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ipsectunnel.png)


### OpenVPN
- Open source
- Uses OpenSSL for encryption
- UDP*/TCP port 1194

### Understand proxies
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/basic_proxy.png)


### SOCKS 4/5 (TCP 1080)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/socks.png)
- RFC 1928
- Uses various Client / Server exchange messages
  - Client can provide authentication to server
  - Client can request connections from server

### SOCKS4
- No Authentication
- Only IPv4
- No UDP support
- No Proxy binding. Client’s IP is not relayed to destination.

### SOCKS5
- Various methods of Authentication
- IPv4 and IPv6 support
- UDP support
- Supports Proxy binding. Client’s IP is relayed to destination.

### Network Basic Input Output System (NetBIOS) protocol
- TCP 139 and UDP 137/138
- Name Resolution (15 characters)
- Largely replaced by DNS

### SMB/CIFS (TCP 445)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/smb.png)
> SMB Rides over Netbios
- Netbios Dgram Service - UDP 138
- Netbios Session Service - TCP 139
- SAMBA and CIFS are just flavors of SMB

### RPC (any port)
- Allows a program to execute a request on a local/remote computer
- Hides network complexities
- XML, JSON, SOAP, and gRPC
- User application will:
  - 1. Request for information from external server
  - 2. Receives the information from the external server
  - 3. Display collected data to User

### API
- Framework of rules and protocols for software components to interact.
- Methods, parameters, and data formats for requests and responses.
- REST and SOAP


## Explain OSI Layer 6 functions and responsibilities
https://net.cybbh.io/public/networking/latest/03_transport/fg.html#_3_3_explain_osi_layer_6_functions_and_responsibilities

### Responsibilities
- Translation
- Formating
- Encoding (ASCII, EBCDIC, HEX, BASE64)
- Encryption (Symmetric or Asymmetric)
- Compression


## Explain OSI Layer 7 protocols and headers
https://net.cybbh.io/public/networking/latest/03_transport/fg.html#_3_4_explain_osi_layer_7_protocols_and_headers

### Telnet (TCP 23)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/telnet.png)
- Remote Login
- Authentication
- Clear Text
- Credentials susceptible to interception

### SSH (TCP 22)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ssh.png)
- Messages provide:
- Client/server authentication
- Asymmetric or PKI for key exchange
- Symmetric for session
- User authentication
- Data stream channeling

### Components of SSH Architecture
- Client / Server / Session
- Keys
  - User Key - Asymmetric public key used to identify the user to the server
  - Host Key - Asymmetric public key used to identify the server to the user
  - Session Key - Symmetric key created by the client and server to protect the session’s

### SSH Architecture
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ssh_architecture.png)

### SSH Architecture
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ssh_protocol.png)

### SSH Implementation Concerns
- Using password authentication only
- Key rotation
- Key management
- Implementation specification
  - libssh                      # https://github.com/vulhub/vulhub/tree/master/libssh/CVE-2018-10933
  - sshtrangerthings            # https://www.exploit-db.com/exploits/46193

### SSH Usage
```
$ ssh {user}@{ip}
$ ssh student@172.16.82.106
```
### SSH Usage
```
-p {port} - Alternate port
-l {username} - Specify the username
-X - Enable X11 forwarding
-v(vv) - Add logging and debugging
-i {identity file} - Specify a private key identity
-F {config file} - Specify an alternate user config file
-N - Do not send remote commands
-T - Do not create a pseudo vty
-C - Enable compression
-f - Backgroud process after authentication
-J user@host - Proxy jump
-L [bind_address:]port:host:hostport
-R [bind_address:]port:host:hostport
-D {port}
```
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

### SSH Host key Changed
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
- Copy/Paste the ssh-keygen message to remove the Host key from the known_hosts file
- When you re-connect it will prompt you to save the new Host key

### SSH FILES
- Known-Hosts Database
```~/.ssh/known_hosts```
- Configuration Files
```
/etc/ssh/ssh_config
/etc/ssh/sshd_config
```
### VIEW/CHANGE SSH PORT
- To view the current configured SSH port
```cat /etc/ssh/sshd_config | grep Port```
- Edit file to change the SSH Port
```sudo nano /etc/ssh/sshd_config```
- Restart the SSH Service
```systemctl restart ssh```
### SSH-KEYGEN
```ssh-keygen -t rsa -b 4096 -C "Student"```
- Create your own SSH Public/Private keys
  - -t Encryption (rsa|dsa|ecdsa|ed25519)
  - -b Bit length (1024|2048|4096)
  - -C Adds a comment
- ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub

### SSH-COPY-ID
```ssh-copy-id student@172.16.82.106```
- Copies your SSH Public key to the remote server
- Saves key to ~/.ssh/authorized_keys on remote server
- Allows you to authenticate with server using your key instead of password
- Must secure your private key

### HTTP(s) (TCP 80/443)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/http.png)
- User Request methods
  - GET / HEAD / POST / PUT
- Server response Codes
  - 100, 200, 300, 400, 500

### HTTP(s) Vulnerabilities
- Flooding                    # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/syn_flood.adoc
- Amplification
- Low and slow
- Drive-By Downloads
- BeEF Framework

### DNS (TCP/UDP 53)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/dns.png)

### DNS query/response
- Resolves Names to IP addresses
- Queries and responses use UDP
- DNS response larger than 512 bytes use TCP
  - DNS Zone Transfer
  - DNS Security

### DNS Records
- A - IPv4 record
- AAAA - IPv6 record
- MX - Mail Server record
- TXT - Human-readable text
- NS - Name Server record
- SOA - Start of Authority

### DNS Architecture
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/DNS_Architecture.png)

### FTP (TCP 20/21)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ftp.png)
- RFC 959
- Port 21 open for Control
- Port 20 only open during data transfer

### FTP (TCP 20/21)
- Authentication or Anonymous
- Clear Text
- Modes:
  - Active (default)
  - Passive

### FTP Active
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ftp_active.png)

### FTP Active issues
- NAT and Firewall traversal issues
- Complications with tunneling through SSH
- Passive FTP solves issues related to Active mode and is most often used in modern systems

### FTP Passive
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ftp_passive.png)

### TFTP (UDP 69)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tftp.png)
- Clear-Text
- Reliability provided at Application layer
- Used by routers and switches to transfer IOS and config files

### SMTP (TCP 25)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/smtp.png)
- Used to send email
- No encryption
- SMTP over TLS/SSL (SMTPS)
  - TCP Ports 587 and 465

### POP (TCP 110)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/pop.png)
- Receives email
- No sync with server
- No encryption
- POP3

### IMAP (TCP 143)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/imap.png)
- Receives email
- Sync with server
- No encryption
- IMAP4

### DHCP (UDP 67/68)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/dhcp.png)

### DHCPv4
- DORA
  - Discover (Broadcast)
  - Offer (Unicast)
  - Request (Broadcast)
  - Acknowlege (Unicast)

### DHCPv6
- If Managed flag is set during SLAAC:
  - Solicit (Multicast)
  - Advertise (Unicast)
  - Request or Information Request (Multicast)
  - Reply (Unicast)

### DHCP Vulnerabilities
- Rogue DHCP
- Evil Twin
- DHCP Starvation

### NTP (UDP 123)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ntp.png)

### NTP (UDP 123)
- Stratum 0 - authoritative time source
- Up to Stratum 15
- Vulnerable to crafted packet injection

### AAA Protocols
- Authentication, Authorization, and Accounting
- For third party authentication

### TACACS (TCP 49) Simple/Extended
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tacacs-s.png)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tacacs-e.png)

### RADIUS (UDP 1645/1646 and 1812/1813)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/radius.png)

### Diameter (TCP 3868)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Diameter_Header.png)

### SNMP (UDP 161/162)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/snmp.png)
- Versions:
  - SNMPv1 - RFC 1157
  - SNMPv2c - RFC 1441
  - SNMPv3 - RFC 3410

### SNMP (UDP 161/162)
- 7 Message Types
  - Get Request
  - Set Request
  - Get Next
  - Get Bulk
  - Response
  - Trap
  - Inform

### SNMP Vulnerabilities
- v1 and 2c
  - Weak Community Strings
  - Lack of Encryption
  - Information Disclosure
  - Can be "sniffed"

### RTP (UDP any above 1023)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/rtp.png)

### RDP (TCP 3389)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/rdp.png)
- Developed by Microsoft (Open Standard)
  - No server software needed
- Other Proprietary RDP software
  - Requires to have 3rd pary software installed

### Kerberos (UDP 88)
- Secure network authentication protocol
- Clients obtain tickets to access services
- Mutual authentication
- Used by Active Directory

### LDAP(s) (TCP 389 and 636)
- Client/server model
- Hierarchical
- Directory schema
- Unsecure and secure versions





![]()
