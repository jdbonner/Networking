# Network Layer

## outcomes
```
Explain Layer 3 Routing Technologies

Describe Security Implications Present in Header Fields

Rationale
Understanding OSI Layer 3, layer 3 protocols and headers, as
well as routing protocols, is crucial for cybersecurity professionals.
OSI Layer 3, also known as the Network Layer, is where routing and
addressing occur, making it a prime target for attackers seeking to
intercept or manipulate network traffic. Layer 3 protocols like IP
(Internet Protocol) and its associated headers define how data is
routed across networks, making them essential for understanding
potential vulnerabilities and attack vectors. Moreover, familiarity
with routing protocols such as OSPF (Open Shortest Path First) and
BGP (Border Gateway Protocol) is necessary for securing network
infrastructure against routing-based attacks, ensuring the integrity
and confidentiality of data traversing the network.
Assessment
You will be assessed via CTFd challenges where you will need to score 193/275 points to achieve a 70%.

Describe IP Networking


Assessment
You will be assessed via CTFd challenges where you will need to score 193/275 points to achieve a 70%.
```


## Describe IP Networking
https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_1_describe_ip_networking

### Network Layer

- Addressing Schemes for Network (Logical Addressing)
- Routing
- Encapsulation
- IP Fragmentation and Reassembly
- Error Handling and Diagnostics

### Internet Protocol Versions

- IPv4 (ARPANET 1982)
  - Classful subnetting
  - Classless subnetting (CIDR)
  - NAT
- IPv6 (Standardized 2017)


## IPV4 Addressing

### Describe Classful IPv4 addressing and subnetting
- Class A (0 to 127)
- Class B (128 to 191)
- Class C (192 to 223)
- Class D (224 to 239) - Multicasting
- Class E (240 to 255) - Not used

### Subnetting
- IP addresses:
  - Network Portion
  - Host Portion
- Practice of "borrowing" host bits and used them as subnet bits.

### Analyze IPv4 packet header
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/IPv4_Header.png)

### Analyze IPv4 packet header
```
00 1f 29 5e 4d 26 00 50　56 bb 3a a0 08 00 45 00
00 3c 83 1b 40 00 40 06　15 0a c0 a8 14 46 4a 7d
83 1b d5 1d 00 19 6b 7f　c7 2d 00 00 00 00 a0 02
72 10 a2 b5 00 00 02 04　05 b4 04 02 08 0a 0a 99
44 36 00 00 00 00 01 03　03 07
```


### Identify IPv4 address types
- Unicast
  - Any Class A thu C
- Multicast
  - Class D
- Broadcast
  - Any IP were the host portion is all on

### IPv4 address scopes
- Public
- Private (RFC 1918)        # https://www.rfc-editor.org/rfc/rfc1918.txt
- Loopback (127.0.0.0/8)
- Link-Local (APIPA)
- Multicast (class D)

### IPv4 Fragmentation
- Breaking up packets from higher MTU to lower MTU network
- Performed by routers
- MF flag is on from 1st until 2nd to last
- Offset is on from 2nd until the last
- Offset = (MTU - (IHL x 4)) ÷ 8

### FRAGMENTATION PROCESS
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Fragmentation.png)

### FRAGMENTATION PROCESS
- IPv4 Fragmentation PCAP    #https://www.cloudshark.org/captures/004070781efd
- Teardrop attack PCAP      #https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/teardrop.cap


### IPv6 Fragmentation
- IPv6 does not support fragmentation within it’s header
- Routers do not fragment IPv6 packets
- Source adjusts MTU to avoid fragmentation
- Source can use IPv6 fragmentation extension header

### Fragmentation Vulnerability
- Can use fragmentation overlaps to avoid firewall detection
- Attack depends on how OS deals with overlap
- Example: Teardrop attack


### OS Fingerprinting with TTL
> Vendors have chosen different values for TTL which can provide insight to which OS family a generated packet is from.
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Default_TTL.png)

### IPv4 Auto Configuration
- APIPA
  - 169.254.0.0/16
  - RFC 3927      # https://www.rfc-editor.org/rfc/rfc3927.txt
- DHCP
  - DORA process
  - RFC 1531      # https://www.rfc-editor.org/rfc/rfc1531.txt

### IPv4 Auto Configuration Vulnerability
- Rogue DHCP
- Evil Twin
- DHCP Starvation

### Analyze ICMPv4 protocol and header structure
> IPv4 Protocol = 1
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ICMPHeader.png)

### ICMPv4 Types and Codes

![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/icmptc.png)

### ICMPv4 OS Fingerprinting
- Linux:
  - Default size: 64 bytes
  - Payload message:
  > !\”#\$%&\‘()*+,-./01234567
- Windows:
  - Default size: 40 bytes
  - Payload message:
  > abcdefghijklmnopqrstuvwabcdefghi

### ICMPv4 Traceroute
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/traceroute.png)
```
- Identifies hops between the source and destination
- Uses incrementing TTLs
- Hops return an ICMP Type 11 Time exceeded message when TTL reaches zero
- Continues until it reaches target or 30 hops*
```

### ICMPv4 Traceroute

- Can use various protocols and ports
  - ICMP (windows default)
  - UDP (linux default)
  - TCP


### ICMPv4 Traceroute (Linux)

- Default:
```
traceroute 172.16.82.106
traceroute -U 172.16.82.106
```
- Requires root:
```
sudo traceroute -I 172.16.82.106
sudo traceroute -T 172.16.82.106
sudo traceroute -T 172.16.82.106 -p 443
```

### ICMPv4 Attacks
```
- Firewalking (traceroute)
- Oversized ICMP messages
- ICMP Redirects
- SMURF Attack
- Map network w/ IP unreachables
- ICMP Covert Channels
```

## IPV6 Addressing
https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_1_2_explain_ipv6_addressing

### Describe IPv6 addressing
- IPv6 Addressing
  - 128 bit address
  - 64-bit Prefix (4 hextets)
  - 64-bit Interface ID (4 hextets)
  - 340 undecillian addresses

### Describe IPv6 subnetting
- Organizations asigned a 48-bit Prefix by IANA
- Last 16-bits of prefix is used for subnetting
- Allows for upto 65,536 subnets to be created

### Analyze IPv6 packet header

![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/IPv6_Header.png)

### Analyze IPv6 packet header
```
38 c9 86 2d 92 61 00 e0　4c 36 1c 43 86 dd 60 04
82 45 00 10 3a 40 20 01　0d b8 00 01 00 00 00 00
00 00 00 00 00 01 20 01　0d b8 00 02 00 00 00 00
00 00 00 00 00 02 80 00　31 e7 21 c1 00 07 5c 98
25 e4 00 02 4e 0f
```

### IPv4/IPv6 Header Comparison
> Comparison Outlook
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/IPv4_IPv6_Comparison.png)

### Explain IPv6 address representation
> 2001:ABCD:1234:DEF0:1111:2222:3333:4444
- 128-bit (64bit Prefix and 64bit Int ID)
- Represented using 32 Hex digits
- Hextet: 4 hex separated by (:)

### Explain IPv6 address representation (shortening)
> 2001:0000:0000:0001:0000:0000:0000:0001
- Can shorten consecutive 0’s with (::)
- Can only use it once
> 2001:0:0:1::1

### Identify IPv6 address types
- Unicast
- Multicast
- Anycast

### IPv6 address scopes
- Global Unicast Addresses (2000::/3)
- Unique Local (fc00::/7)
- Loopback (::1/128)
- Link-Local (fe80::/10)
- Multicast (ff00::/8)

### IPv6 zero configuration (Link-Local)
- Hosts generate link-local prefix (FE80::/8)
- Interface ID can be:
  - Random (Windows default)
  - EUI-64 (nix* and Cisco default)

### IPv6 zero configuration (Global)
- Hosts requests global prefix
  - SLAAC (RFC 4862) (default)          # https://www.rfc-editor.org/rfc/rfc4862.txt
  - DHCPv6 (configured)
- Interface ID can be:
  - EUI-64 (nix* and Cisco default)
  - Random (Windows default)


### IPv6 zero configuration (EUI-64 link-local)
- MAC: fa:16:3e:c3:68:f2
- Append: ff:fe between OUI and Vendor assigned
- Flip 7th bit
- Result: FE80::f816:3eff:fec3:68f2

### IPv6 zero configuration (EUI-64 Global)
- Prefix from RA: 2001:ABCD:1234:DEF0::
- MAC: fa:16:3e:c3:68:f2
- Append: ff:fe between OUI and Vendor assigned
- Flip 7th bit
- Result: 2001:ABCD:1234:DEF0:f816:3eff:fec3:68f2

### IPv6 zero configuration (Random)
- Prefix from RA: 2001:ABCD:1234:DEF0::
- Link-Local: FE80::cdc3:b3ac:1623:f552
- Global: 2001:ABCD:1234:DEF0:182f:dd86:f2be:653b

### IPv6 zero configuration Vulnerability
- SLAAC MitM                      # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/slaac_mitm.adoc
- Can be used to figerprint OS
- Rogue DHCP
- Evil Twin
- DHCP Starvation

### Analyze ICMPv6 protocol and header structure
> IPv6 Next Header = 58
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ICMPHeader.png)

### Explain Neighbor Discovery Protocol (NDP)
- Router Solicitation (Type 133)
- Router Advertisement (Type 134)
- Neighbor Solicitation (Type 135)
- Neighbor Advertisement (Type 136)
- Redirect (Type 137)




## Analyze Internetwork Routing
https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_2_analyze_internetwork_routing

### Discuss Routing
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ip_routing_example.jpg)


### Discuss Routing Tables
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Route_Types.png)

### Discuss Routing Tables
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Routing_table.png)


### ADMINISTRATIVE DISTANCE
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/AD.png)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Table_Entry.jpg)

### LOOKUP PROCESS
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Packet_Routing_Flow.png)

### LOOKUP PROCESS
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Bit_Match.jpg)

### Metrics
- RIP: Hop
- EIGRP: Bandwidth, Delay, Load, Reliability
- OSPF: Cost
- BGP: Policy

## Dynamic Routing Protocols Operation and Vulnerabilities
https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_2_2_dynamic_routing_protocols_operation_and_vulnerabilities

### Classful vs Classless
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Classful_Classless.png)

### Routed vs Routing Protocols
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/routed_routing.png)

### IGP AND EGP
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/IGP_EGP.jpg)

### Autonomous Systems
- Definition:
  - Collection of connected Internet Protocol routing prefixes under the control of one or more network operators on behalf of a single administrative entity or domain, that presents a common and clearly defined routing policy to the Internet.

### Autonomous Systems
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/iana.png)

### Autonomous Systems
- 16 or 32-bit Number
```
AS109   CISCO-EU-109 Cisco Systems Global ASN
AS193   FORD-ASN - Lockheed Martin Western Development Labs
AS721   DoD Network Information Center Network
AS3598  MICROSOFT-CORP-AS - Microsoft Corporation
AS15169 GOOGLE - Google Inc.
```

### Distance Vector Routing Protocols
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/DV.png)

### Link State Routing Protocols
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/LS.jpg)

### Distance Vector vs Link State
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/dynamic_table.png)

### Routing Protocol vulnerabilities
- Distributed Denial of Service (DDOS)
- Packet Mistreating Attacks (PMA)
- Routing Table Poisoning (RTP)
- Hit and Run DDOS (HAR)
- Persistent Attacks (PA)

### BGP
- Road-map of the Internet
- Routes traffic between Autonomous System (AS) Number
- Advertises IP CIDR address blocks
- Establishes Peer relationships
- Complicated configuration
- Complicated and slow path selection

### BGP Operation
- How BGP chooses the best path:
- Advertise a more specific route. 192.168.1.0 /24 is more specific than 192.168.0.0 /16.
- Offer a shorter route to certain blocks of IP addresses.
- A route to ip prefix with 4 AS 'hops" is better than route with 5 AS 'hops'

### BGP Hijacking
- Illegitimate advertising of addresses
- BGP propagates false information
- Purpose:
  - stealing prefixes
  - monitoring traffic
  - intercept (and possibly modify) Internet traffic
  - 'black holing' traffic
  - perform MitM

### BGP Hijacking Defense
- IP prefix filtering
- BGP hijacking detection
  - Tracking the change in TTL of incoming packets
  - Increased Round Trip Time (RTT) which increases latency
  - Monitoring misdirected traffic (change in AS path from tools like Looking Glass)
- BGPSec

### BGP Hijacking Public incidents
Various examples can be found in the student guide      # https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_2_2_9_2_bgp_hijacking_public_incidents


## Compare Static routing vs. dynamic routing
https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_2_3_compare_static_routing_vs_dynamic_routing

### Static Routing
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Static.jpg)

### STATIC ROUTING ADVANTAGES AND DISADVANTAGES
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/staticAD.png)

### Dynamic Routing
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Dynamic_Routing.jpg)

### DYNAMIC ROUTING ADVANTAGES AND DISADVANTAGES
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/dynamicAD.png)


## Understand First Hop Redundancy Protocols and their vulnerabilities
https://net.cybbh.io/public/networking/latest/02_network/fg.html#_2_2_4_understand_first_hop_redundancy_protocols_and_their_vulnerabilities

### First Hop Redundancy Protocol
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/FHRP.jpg)

### FHRP Attack
- Intercept the FHRP message exchange
- Inject manipulated messages
- MitM by becoming active forwarder









![]()














































![]()
