# Traffic Capture
```
OUTCOMES
Describe Network Traffic Sniffing

Perform real-time network traffic sniffing

Rationale
Learning Wireshark, tcpdump primitives, Berkeley Packet Filters
(BPF), and p0f is essential for cybersecurity professionals due
to their critical role in network analysis and intrusion detection.
Wireshark provides a comprehensive platform for packet analysis,
allowing practitioners to inspect network traffic in real-time and
identify anomalies or suspicious activities. Tcpdump primitives
offer a command-line interface for capturing and analyzing network
packets, providing flexibility and scalability in monitoring network
traffic. Berkeley Packet Filters (BPF) enable efficient packet
filtering and capture capabilities, empowering security analysts
to focus on relevant traffic patterns and mitigate potential threats
effectively. Additionally, p0f leverages passive fingerprinting
techniques to identify remote systems, aiding in network reconnaissance
and threat intelligence gathering. Mastery of these tools equips
cybersecurity professionals with the necessary skills to detect,
analyze, and respond to cyber threats effectively.

Assessment
You will be assessed via CTFd challenges where you will need to score 98/140 points to achieve a 70%.
```
## Describe Network Traffic Sniffing
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_1_describe_network_traffic_sniffing

### Explain the capture Libraries
- Libpcap - https://www.tcpdump.org/
- WinPcap - https://www.winpcap.org/
- NPcap - https://nmap.org/npcap/

### Describe the use of sniffing tools and methods
- Practical Uses:
  - Network troubleshooting
  - Diagnosing improper routing or switching
  - Identifying port/protocol misconfigurations
  - Monitor networking consumption
  - Intercepting usernames and passwords
  - Eavesdrop on network communications

### Describe the use of sniffing tools and methods
- Disadvantages:
  - Requires elevate permissions
  - Can only capture what NIC can see
  - Cannot capture local traffic
  - Can consume massive amounts of system resources
  - Lost packets on busy networks

### Packets can be captured in two ways:
- Hardware Packet Sniffers
- Software Packet Sniffers

### Describe Socket Types
- User Space Sockets
  - Stream socket - TCP
  - Datagram socket - UDP
- Kernel Space Sockets
  - RAW Sockets

### Capture Library (Image)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/capture.png)

### Capture Library
- Requires root for:
  - Promicious Mode (Listen on all NICs)
  - All captured packets are created as RAW Sockets

### Types of sniffing
- Active
- Passive

### Popular Software Packet Capture Programs
- tcpdump          # https://www.tcpdump.org/
- Wireshark        # https://www.wireshark.org/
- tshark           # https://www.wireshark.org/docs/man-pages/tshark.html
- p0f              # https://github.com/p0f/p0f
- NetworkMiner     # https://www.netresec.com/?page=NetworkMiner
- NetMiner         # http://www.netminer.com/product/overview.do
- SolarWinds       # https://www.solarwinds.com/network-performance-monitor
- BetterCap        # https://www.bettercap.org/
- EtterCap         # https://www.ettercap-project.org/

### Other packet Capture Programs
Kismet          # https://www.kismetwireless.net/
L0phtCrack      # https://www.l0phtcrack.com/
McAfee ePO      # https://www.mcafee.com/enterprise/en-us/products/epolicy-orchestrator.html
ngrep           # https://github.com/jpr5/ngrep
Nmap            # https://nmap.org/
Scapy           # https://scapy.net/
Snort           # https://www.snort.org/
Suricata        # https://suricata-ids.org/

### Interface Naming
- Traditional:
  - eth0, eth1
- Consistent:
  - eno1, ens3

## Perform real-time network traffic sniffing
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_perform_real_time_network_traffic_sniffing

### Explain TCPDUMP primitives
- User friendly capture expressions
  - src or dst
  - host or net
  - tcp or udp

### TCPDUMP Primitive Qualifiers
- type - the 'kind of thing' that the id name or number refers to
  - host, net, port, or portrange
- dir - transfer direction to and/or from
  - src or dst
- proto - restricts the match to a particular protocol(s)
  - ether, arp, ip, ip6, icmp, tcp, or udp

### Basic TCPDump options
- -A = print payload in ASCII
- -D = list interfaces
- -i = specify capture interface
- -e = print data-link headers
- -X or XX = print payload in HEX and ASCII

### Basic TCPDump options
- -w = write to pcap
- -r = read from pcap
- -v, vv, or vvv = verbosity
- -n = no inverse lookups

### Logical Operators
- Primitives may be combined using:
  - Concatenation: 'and' ( && )
  - Alteration: 'or' ( || )
  - Negation: 'not' ( ! )

### Relational Operators
- < or < =
- > or >=
- = or == or !=

### TCPDump Primitive Examples
- Simple
- Extended

### Verify TCPDUMP
- -d = Dump the compiled packet-matching code in a human readable form
```
tcpdump "ether[12:2] = 0x800" -d

(000) ldh   [12]
(001) jeq   0x800,  jt 2  jf 3
(002) ret   #262144
(003) ret   #0
```
```
ldh  - loads half-word (16-bit) value in the accumulator from offset 12
      in the ethernet header
jeq - check if the value is "0x800" and if this is true "jump true" to line 2,
      if it is false "jump false" to line 3
ret #262144 - returns the default snapshot length in bytes
ret #0 - returns nothing, it didn’t meet the criteria in the jeq statement.
```

### Define the function of a Berkley packet filter (BPF)
- Similar in function to primitives
- Reduces redudant computations
- More complex expressions

### Compare primitives and BPFs
- Primitives (macros)
  - CMU/Stanford Packet Filter (CSPF) Model commonly called Boolean Expression Tree
  - Simple and easy filter expressions
  - First user-level packet filter model
  - Memory-stack-based filter machine which can create bottlenecks on model CPUs
  - can have redundant computations of the same information

### Compare primitives and BPFs
- Berkley Packet Filters (BPF)
  - Control Flow Graph (CFG) Model
  - Uses a simple (non-shared) buffer model which can make it 1.5 to 20 times faster than CSPF
  - Can be more complex to create expressions but offer far more precision


## Construct A BPF
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_4_construct_a_bpf

### Kernel API
- TCPDUMP requests a RAW Socket creation
- Filters are set using the SO_ATTACH_FILTER
- SO_ATTACH_FILTER allows us to attach a Berkley Packet Filter to the socket to capture incoming packets.

### Berkley Packet Filters
```
tcpdump {A} [B:C] {D} {E} {F} {G}

A = Protocol (ether | arp | ip | ip6 | icmp | tcp | udp)
B = Header Byte offset
C = optional: Byte Length. Can be 1, 2 or 4 (default 1)
D = optional: Bitwise mask ( & )
E = Relational operator ( = | == | > | < | <= | >= | != | () | << | >> )
F = Result of Expression
G = optional: Logical Operator ( && || ) to bridge expressions
```

### BPF examples
```
tcpdump -i eth0 'ether[12:2] = 0x0806'
tcpdump -i eth1 'ip[9] = 0x06'
tcpdump -i eth0 'tcp[0:2] = 53 || tcp[2:2] = 53'
tcpdump 'ether[12:2] = 0x0800 && (tcp[2:2] != 22 && tcp[2:2] != 23)'
```

### Bitwise Masking
- BPFs can read 1 (byte), 2 (half-word) or 4 (word)
- BPFs alone will only filter to the byte level
- Bit-wise masking allow filtering precision to the bit level
- Binary (0) to ignore bit
- Binary (1) to match bit


### Bitwise Masking examples
```
tcpdump 'ether[12:4] & 0xffff0fff = 0x81000abc'
tcpdump 'ip[1] & 252 = 32'
tcpdump 'ip[6] & 224 != 0'
tcpdump 'tcp[13] & 0x11 = 0x11'
tcpdump 'tcp[12] & 0xf0 > 0x50'
```


### Filter Logic - Most exclusive
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/most-bpf.png)
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/most-bpf2.png)
```
tcp[13] = 0x11
--assumes this--
tcp[13] & 0xFF = 0x11
```

### Filter Logic - Less exclusive
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/less-bpf.png)
tcp[13] & 0x11 = 0x11

### Filter Logic - Least exclusive
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/least-bpf.png)
```
tcp[13] & 0x11 > 0
tcp[13] & 0x11 !=0
```

## Use a BPF to filter packets entering a network interface
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_5_use_a_bpf_to_filter_packets_entering_a_network_interface

## BPFs at the Data-Link layer
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_5_1_bpfs_at_the_data_link_layer

### BPFs at the Data-Link layer
- Search for the destination broadcast MAC address.
```
'ether[0:4] = 0xffffffff && ether[4:2] = 0xffff'
'ether[0:2] = 0xffff && ether[2:2]= 0xffff && ether[4:2] = 0xffff'
```
- Search for the source MAC address of fa:16:3e:f0:ca:fc.
```
'ether[6:4] = 0xfa163ef0 && ether[10:2] = 0xcafc'
'ether[6:2] = 0xfa16 && ether[8:2] = 0x3ef0 && ether[10:2] = 0xcafc'
```

### BPFs at the Data-Link layer
- Search for unicast (0x00) or multicast (0x01) MAC address.
```
'ether[0] & 0x01 = 0x00'
'ether[0] & 0x01 = 0x01'
'ether[6] & 0x01 = 0x00'
'ether[6] & 0x01 = 0x01'
```

### BPFs at the Data-Link layer
- Search for IPv4, ARP, VLAN Tag, and IPv6 respectively.
```
ether[12:2] = 0x0800
ether[12:2] = 0x0806
ether[12:2] = 0x8100
ether[12:2] = 0x86dd
```

### BPFs at the Data-Link layer
- Search for 802.1Q VLAN 100.
```
'ether[12:2] = 0x8100 && ether[14:2] & 0x0fff = 0x0064'
'ether[12:4] & 0xffff0fff = 0x81000064'
```
- Search for double VLAN Tag.
```
'ether[12:2] = 0x8100 && ether[16:2] = 0x8100'
```

## BPFs at the Network layer
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_5_2_bpfs_at_the_network_layer

### BPFs at the Network layer
- Search for IHL greater than 5.
```
'ip[0] & 0x0f > 0x05'
'ip[0] & 15 > 5'
```

### BPFs at the Network layer
- Search for ipv4 DSCP value of 16.
```
'ip[1] & 0xfc = 0x40'
'ip[1] & 252 = 64'
'ip[1] >> 2 = 16'
```
- Search for traffic class in ipv6 having a value.
```
'ip6[0:2] & 0x0ff0 != 0'
```

### BPFs at the Network layer
- Search for ONLY the RES flag set. DF and MF must be off.
```
'ip[6] & 0xE0 = 0x80'
'ip[6] & 224 = 128'
```
- Search for RES bit set. The other 2 flags are ignored so they can be on or off.
```
'ip[6] & 0x80 = 0x80'
'ip[6] & 128 = 128'
```

### BPFs at the Network layer
- Search for ONLY the DF flag set. RES and MF must be off.
```
'ip[6] & 0xE0 = 0x40'
'ip[6] & 224 = 64'
```
- Search for DF bit set. The other 2 flags are ignored so they can be on or off.
```
'ip[6] & 0x40 = 0x40'
'ip[6] & 64 = 64'
```

### BPFs at the Network layer
- Search for ONLY the MF flag set. RES and DF must be off.
```
'ip[6] & 0xe0 = 0x20'
'ip[6] & 224 = 32'
```
- Search for MF bit set. The other 2 flags are ignored so they can be on or off.
```
'ip[6] & 0x20 = 0x20'
'ip[6] & 32 = 32'
```

### BPFs at the Network layer
- Search for offset field having any value greater than zero (0).
```
'ip[6:2] & 0x1fff > 0'
'ip[6:2] & 8191 > 0'
```
- Search for MF set or offset field having any value greater than zero (0).
```
'ip[6] & 0x20 = 0x20 || ip[6:2] & 0x1fff > 0'
'ip[6] & 32 = 32 || ip[6:2] & 8191 > 0'
```

### BPFs at the Network layer
- Search for TTL in ipv4(6) packet.
```
'ip[8] = 128'
'ip[8] < 128'
'ip[8] >= 128'
'ip6[7] = 128'
'ip6[7] < 128'
'ip6[7] >= 128'
```

### BPFs at the Network layer
- Search for ICMPv4(6), TCP, or UDP encapsulated within an ipv4(6) packet.
```
'ip[9] = 0x01'
'ip[9] = 0x06'
'ip[9] = 0x11'
'ip6[6] = 0x3A'
'ip6[6] = 0x06'
'ip6[6] = 0x11'
```

### BPFs at the Network layer
- Search for ipv4 source or destination address of 10.1.1.1.
```
'ip[12:4] = 0x0a010101'
'ip[16:4] = 0x0a010101'
```
- Search for ipv6 source or destination address starting with FE80.
```
'ip6[8:2] = 0xfe80'
'ip6[24:2] = 0xfe80'
```


## BPFs at the Transport layer
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_5_3_bpfs_at_the_transport_layer

### BPFs at the Transport layer
- Search for TCP source port 3389.
```
'tcp[0:2] = 3389'
```
- Search for TCP destination port 3389.
```
'tcp[2:2] = 3389'
```
- Search for TCP source or destination port 3389.
```
'tcp[0:2] = 0x0d3d || tcp[2:2] = 0x0d3d'
```

### BPFs at the Transport layer
- Search for TCP with options.
```
'tcp[12] & 0xF0 > 0x50'
'tcp[12] & 240 > 80'
```
- Search for TCP Reserve field with a value.
```
'tcp[12] & 0x0F != 0'
'tcp[12] & 15 > 0'
```

### BPFs at the Transport layer
- Search for TCP Flags set to ACK+SYN. No other flags can be set.
```
'tcp[13] = 0x12'
```
- Search for TCP Flags set to ACK+SYN. The other flags are ignored.
```
'tcp[13] & 0x12 = 0x12'
```

### BPFs at the Transport layer
- Search for TCP Flags ACK and SYN (both or 1 must be on).
```
'tcp[13] & 0x12 != 0'
'tcp[13] & 0x12 > 0'
```

### BPFs at the Transport layer
- Search for TCP Urgent Pointer having a value.
```
'tcp[18:2] != 0'
'tcp[18:2] > 0'
```

## Understand Wireshark’s use of BPFs
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_6_understand_wiresharks_use_of_bpfs

### Wireshark Display Filters vs Capture filters
- Capture filters - used to specify which packets should be saved to disk while capturing.
- Display filters - allow you to change the view of what packets are displayed of those that are captured.

### Wireshark Capture Filters
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/wcapture.png)
- Can use most primitives and/or BPFs

### Wireshark Display Filters
- Protocol Headers
- Addresses/Ports
- Header Fields
- Follow Streams
- Apply as Filter

### Popular Wireshark Menus
- Colorize Traffic
- Protocol Hierarchy
- Firewall Rules
- Exporting Objects
- Decrypt Traffic
- Conversations
- Endpoints

### Popular Wireshark Menus
- I/O Graph
- ipv4 and ipv6 statistics
- Expert Information
- Geo Location

### Colorize traffic
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w12.PNG)
- Menu → View → Coloring Rules…​

### Protocol Hierarchy
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w8.PNG)
- Menu→ Statistics → Protocol Hierarchy

### Firewall rules
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w13.PNG)
- Menu → Tools → Firewall ACL Rules

### Exporting objects
- Menu → File → Export Objects

### Decrypt traffic
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w15.PNG)
- Menu → Edit → Preference → Protocols → SSL

### Conversations
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w9.PNG)
- Menu → Statistics → Conversations

### Endpoints
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w10.PNG)
- Menu → Statistics → Endpoints

### I/O Graph.
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w11.PNG)
- Menu → Statistics → I/O Graph

### ipv4 and ipv6 statistics
- Menu → Statistics → ipv4 Statistics
- Menu → Statistics → ipv6 Statistics

### Expert Information
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w16.PNG)
- Menu → Analyze → Expert Information

### Geo location
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/w14.PNG)
- Menu → Edit → preferences → name resolution → GeoIP database directories "Edit"

## Describe passive OS fingerprinting (p0f)
https://net.cybbh.io/public/networking/latest/06_traffic_cap/fg.html#_6_2_7_describe_passive_os_fingerprinting_p0f
- Similar to tcpdump except it only captures traffic that matches signatures in its database file.

### Operating systems
- Searches for specific signatures in:
  - Most Operating Systems
  - Most Browsers
  - Search Robots
  - Command Line Tools

### P0f Signature Database
```
less /etc/p0f/p0f.fp
```

### p0f help
```
p0f -h
```

### Run p0f on interface
```
p0f -i eth0
```

### Run p0f on a pcap
```
p0f -r capture.pcap
```

### Output to greppable log file
```
p0f -r wget.pcap -o /var/log/p0f.log
cat /var/log/p0f.log | grep {expression}
```










