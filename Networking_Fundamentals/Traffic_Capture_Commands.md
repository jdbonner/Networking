# Taffic Capture Commands

sing a User application such as a Web Browser, FTP, Telnet, SSH, netcat, etc to connect to any listening port.
```
nc 10.0.0.1 22
firefox http://10.0.0.1
wget -r http://10.0.0.1
curl ftp://10.0.0.1
ftp 10.0.0.1
telnet 10.0.0.1
ssh user@10.0.0.1
```
Using tcpdump or wireshark to read a file
```
tcpdump -r capture.pcap
```
Using nmap with no switches (-sS) or -sT
```
nmap 10.0.0.1
nmap -sT 10.0.0.1
```
Opening listening ports above the Well-Known range (1024+)
```
python -m SimpleHTTPServer 7800
nc -lvp 1234
```
Using /dev/tcp or /dev/udp to transmit data
```
cat /etc/passwd > /dev/tcp/10.0.0.1/1234
```

Packets that have to be crafted with various flag combinations and other header field manipulation must be created as RAW Sockets. Tools like HPING and Nmap needs to open raw sockets when attempting to set specific flags for performing certain scans.
```
nmap -sX 10.0.0.1
nmap -sN 10.0.0.1
nmap -sF 10.0.0.1
```
Tcpdump requires raw sockets in order to receive each packet, in its entirety, for total packet analysis. The operating system normally strips all the headers when receiving data so to examine these packets with their headers intact they have to be captured as RAW Sockets.
```
tcpdump -w capture.pcap
```
Using Scapy to craft or modify a packet for transmission

Using Python to craft or modify Raw Sockets for transmission

Opening well ports in the Well-Known range (0-1023) require kernel access.
```
python -m SimpleHTTPServer 80
nc -lvp 123
```

Basic TCPDump options
-A Prints the frame payload in ASCII.
```
tcpdump -A
```
-D Print the list of the network interfaces available on the system and on which TCPDump can capture packets. For each network interface, a number and an interface name, followed by a text description of the interface, is printed. This can be used to identify which interfaces are available for traffic capture.
```
tcpdump -D
```
-i Normally, eth0 will be selected by default if you do not specify an interface. However, if a different interface is needed, it must be specified.
```
tcpdump -i eth0
```
-e Prints Data-Link Headers. Default is to print the encapsulated protocol only.
```
tcpdump -e
```
-X displays packet data in HEX and ASCII.
-XX displays the packet data in HEX and ASCII to include the Ethernet portion.
```
tcpdump -i eth0 -X
tcpdump -i eth0 -XX
```
-w writes the capture to an output file
```
tcpdump -w something.pcap
```
-r reads from the pcap
```
tcpdump -r something.pcap
```
-v gives more verbose output with details on the time to live, IPID, total length, options, and flags. Additionally, it enables integrity checking.
```
tcpdump -vv
```
-n Does not covert protocol and addresses to names
```
tcpdump -n
```
Tcpdump for specific protocol traffic.
```
tcpdump port 80 -vn
```

tcpdump for specific protocol traffic of more than one type.
```
tcpdump port 80 or 22 -vn
```
tcpdump for a range of ports on 2 different hosts with a destination to a specific network
```
tcpdump portrange 20-100 and host 10.1.0.2 or host 10.1.0.3 and dst net 10.2.0.0/24 -vn
```
tcpdump filter for source network 10.1.0.0/24 and destination network 10.3.0.0/24 or dst host 10.2.0.3 and not host 10.1.0.3.
```
tcpdump "(src net 10.1.0.0/24  && (dst net 10.3.0.0/24 || dst host 10.2.0.3) && (! dst host 10.1.0.3))"" -vn
```
```
TCPDump Primitive Examples
Simple: Simple primitives are basic filters that match specific attributes of network packets. They are straightforward and generally used to focus on a particular aspect of the traffic. Examples include:
To print all ethernet traffic:

tcpdump ether

To print all packets related to ARP:

tcpdump arp

To print all packets related to ICMP:

tcpdump icmp

To print all ICMP echo-request packets :

tcpdump 'icmp[icmptype] = icmp-echo'

To print all ICMP echo-reply packets :

tcpdump 'icmp[icmptype] = icmp-reply'

To print all packets arriving at or departing from 192.168.1.1:

tcpdump host 192.168.1.1

To print all packets arriving at 192.168.1.1:

tcpdump dst host 192.168.1.1

To print all packets departing from 192.168.1.1:

tcpdump src host 192.168.1.1

To print all packets arriving at or departing from 192.168.1.0/24 network:

tcpdump net 192.168.1.0/24

To print all packets departing from 192.168.1.0/24 network:

tcpdump src net 192.168.1.0/24

To print all packets arriving at 192.168.1.0/24 network:

tcpdump dst net 192.168.1.0/24

To print all packets related to IPv4:

tcpdump ip

To print all packets related to IPv6:

tcpdump ip6

To print all packets related to TCP:

tcpdump tcp

To print all packets related to UDP:

tcpdump udp

To print all packets arriving at or departing from TCP port 22:

tcpdump tcp port 22

To print all packets arriving at TCP port 22:

tcpdump tcp dst port 22

To print all packets departing from TCP port 22:

tcpdump tcp src port 22

To print all packets arriving at or departing from TCP or UDP port 53:

tcpdump port 53

To print all packets with TCP flag ACK set:

'tcp[tcpflags] = tcp-ack'

Complex: Complex primitives combine multiple simple filters using logical operators or refine them to create more specific capture rules. They allow more granular control over the captured data. Examples include:
To print traffic between 192.168.1.1 and either 10.1.1.1 or 10.1.1.2:

tcpdump host 192.168.1.1 and \( 10.1.1.1 or 10.1.1.2 \)

To print all IP packets between 10.1.1.1 and any host except 10.1.1.2:

tcpdump ip host 10.1.1.1 and not 10.1.1.2

To print all traffic between local hosts and hosts at Berkeley:

tcpdump net ucb-ether

To print all ftp traffic through internet gateway 192.168.1.1: (note that the expression is quoted to prevent the shell from (mis-)interpreting the parentheses):

tcpdump 'gateway 192.168.1.1 and (port ftp or ftp-data)'

To print traffic neither sourced from nor destined for local hosts (if you gateway to one other net, this stuff should never make it onto your local net).

tcpdump ip and not net localnet

To print the start and end packets (the SYN and FIN packets) of each TCP conversation that involves a non-local host.

tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-fin) != 0 and not src and dst net localnet'

To print the TCP packets with flags RST and ACK both set. (i.e. select only the RST and ACK flags in the flags field, and if the result is "RST and ACK both set", match)

tcpdump 'tcp[tcpflags] & (tcp-rst|tcp-ack) == (tcp-rst|tcp-ack)'

To print all IPv4 HTTP packets to and from port 80, i.e. print only packets that contain data, not, for example, SYN and FIN packets and ACK-only packets. (IPv6 is left as an exercise for the reader.)

tcpdump 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)'

To print IP packets longer than 576 bytes sent through gateway 192.168.1.1:

tcpdump 'gateway 192.168.1.1 and ip[2:2] > 576'

To print IP broadcast or multicast packets that were not sent via Ethernet broadcast or multicast:

tcpdump 'ether[0] & 1 = 0 and ip[16] >= 224'

To print all ICMP packets that are not echo requests/replies (i.e., not ping packets):

tcpdump 'icmp[icmptype] != icmp-echo and icmp[icmptype] != icmp-echoreply'
```

Primitive to find "arp":
```
root@linux-opstation-pysn:~# tcpdump -d arp
(000) ldh      [12]
(001) jeq      #0x806           jt 2 jf 3
(002) ret      #262144
(003) ret      #0
```
BPF to find "arp":
```
root@linux-opstation-pysn:~# tcpdump -d ether[12:2]=0x0806
(000) ldh      [12]
(001) jeq      #0x806           jt 2 jf 3
(002) ret      #262144
(003) ret      #0
```

Primitive to find "ip" and "icmp":
```
root@linux-opstation-pysn:~# tcpdump -d ip and icmp
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 5
(002) ldb      [23]
(003) jeq      #0x1              jt 4 jf 5
(004) ret      #262144
(005) ret      #0
```

BPF to find "ip" and "icmp":
```
root@linux-opstation-pysn:~# tcpdump -d 'ether[12:2]=0x0800 && ip[9]=0x01'
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 6
(002) jeq      #0x800           jt 3 jf 6
(003) ldb      [23]
(004) jeq      #0x1             jt 5 jf 6
(005) ret      #262144
(006) ret      #0
```

Primitive to find "ip6" and "icmp6":
```
root@linux-opstation-pysn:~# tcpdump -d ip6 and icmp6
(000) ldh [12]                 = Here is loading a half word starting at byte 12.
(001) jeq      #0x86dd        jt 2 jf 8  = if its equal to 0x86dd then jump to line 2, else jump to line 8.
(002) ldb      [20]             = Load 1 byte at byte 20
(003) jeq      #0x3a          jt 7 jf 4  = Jump to line 7 if its 0x3a (58) which is the code for icmpv6. Goto line 4 if it is not.
(004) jeq      #0x2c          jt 5 jf 8 = jump to line 5 if its 0x2c (44) which is IPv6-Fragmentation extension header. Goto line 8 if not.
(005) ldb      [54]             = Load 1 byte at byte 54
(006) jeq      #0x3a          jt 7 jf 8 = Jump to line 7 if its 0x3a (58) which is the code for icmpv6. Goto line 8 if it is not.
(007) ret      #262144            = Has a number larger than the packet size so capture the packet.
(008) ret      #0               = Has a null value so discard this packet.
```
BPF to find "ip6" and "icmp6":
```
root@linux-opstation-pysn:~# tcpdump -d 'ether[12:2]=0x86dd && (ip6[20]=0x3a || ip6[20]=0x2c)'                 =
(000) ldh      [12]
(001) jeq      #0x86dd          jt 2 jf 7 = like for 'ip' this line is because we are looking for E-type 0x86dd
(002) jeq      #0x86dd          jt 3 jf 7 = this line is also looking for the same because we specified 'ip6' so it will automatically look for E-type 0x86dd
(003) ldb      [34]
(004) jeq      #0x3a            jt 6 jf 5
(005) jeq      #0x2c            jt 6 jf 7
(006) ret      #262144
(007) ret      #0
```

Primitive to find "tcp" and "src port 22":
```
root@linux-opstation-pysn:~# tcpdump -d tcp src port 22
(000) ldh      [12]               = Looks automatically for the E-type field
(001) jeq      #0x86dd          jt 2 jf 6  = Looks for 0x86dd goto 2 if true or 6 if false
(002) ldb      [20]               = Goto byte 20 in the ipv6 header
(003) jeq      #0x6             jt 4 jf 15 = goto 4 if it equals 0x06 (TCP) else goto 15
(004) ldh      [54]                = Load half-word at byte 54 (start of tcp header)
(005) jeq      #0x16            jt 14 jf 15 = Jump to 14 if its 0x16 (22)
(006) jeq      #0x800           jt 7 jf 15  = Secondly looks for 0x0800 if not 0x86dd from line 1. Goto 7 if true else 15.
(007) ldb      [23]                = Goto byte 23 of ipv4 header
(008) jeq      #0x6             jt 9 jf 15  = goto 9 if its 0x06 (TCP) else goto 15
(009) ldh      [20]                = Load half-word at byte 20
(010) jset     #0x1fff          jt 15 jf 11 = jset = jump if set. If the mask of 0x01fff had a value then goto 15. This is focusing on only the offset field. If there is a value here then its a fragment with no higher layer header encapsulated. Else goto 11
(011) ldxb     4*([14]&0xf)           = this loads byte 14 with a mask of 0x0f which focuses on the IHL. Performs the math operation of (4 x (IHL value)). If IHL is 5 then value is 20. If IHL is 7 then value is 28. IHL of 15 is 60.
(012) ldh      [x + 14]             = Load a half-word at X + 14. 14 is added to the value from line 11. 14 is the # of bytes from the Ethernet Header added to the size of the ip header.
(013) jeq      #0x16            jt 14 jf 15 = jump to 14 if it equals 0x16 (22) else 15
(014) ret      #262144              = Has a number larger than the packet size so capture the packet.
(015) ret      #0                 = Has a null value so discard this packet.
```
BPF to find "tcp" and "src port 22". The process is similar as using primitives except that it does not check for ipv6 and always assumes ipv4.:
```
root@linux-opstation-pysn:~# tcpdump -d tcp[0:2]=22
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 10
(002) ldb      [23]
(003) jeq      #0x6             jt 4 jf 10
(004) ldh      [20]
(005) jset     #0x1fff          jt 10 jf 6
(006) ldxb     4*([14]&0xf)
(007) ldh      [x + 14]
(008) jeq      #0x16            jt 9 jf 10
(009) ret      #262144
(010) ret      #0

```
Primitive to find "udp" and "dst port 53":
```
root@linux-opstation-pysn:~# tcpdump -d udp dst port 53
(000) ldh      [12]
(001) jeq      #0x86dd          jt 2 jf 6
(002) ldb      [20]
(003) jeq      #0x11            jt 4 jf 15
(004) ldh      [56]
(005) jeq      #0x35            jt 14 jf 15
(006) jeq      #0x800           jt 7 jf 15
(007) ldb      [23]
(008) jeq      #0x11            jt 9 jf 15
(009) ldh      [20]
(010) jset     #0x1fff          jt 15 jf 11
(011) ldxb     4*([14]&0xf)
(012) ldh      [x + 16]             = Adds 16 to the value of line 11. 14 bytes for Ethernet header and 2 bytes of the source port field.
(013) jeq      #0x35            jt 14 jf 15
(014) ret      #262144
(015) ret      #0
```
BPF to find "udp" and "dst port 53". Identical to using primitives except that it will not check for ipv6.:
```
root@linux-opstation-pysn:~# tcpdump -d udp[2:2]=53
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 10
(002) ldb      [23]
(003) jeq      #0x11            jt 4 jf 10
(004) ldh      [20]
(005) jset     #0x1fff          jt 10 jf 6
(006) ldxb     4*([14]&0xf)
(007) ldh      [x + 16]
(008) jeq      #0x35            jt 9 jf 10
(009) ret      #262144
(010) ret      #0
```

Primitive to find "tcp" and "port 80":
```
root@linux-opstation-pysn:~# tcpdump -d tcp port 80
(000) ldh      [12]
(001) jeq      #0x86dd          jt 2 jf 8
(002) ldb      [20]
(003) jeq      #0x6             jt 4 jf 19
(004) ldh      [54]
(005) jeq      #0x50            jt 18 jf 6
(006) ldh      [56]
(007) jeq      #0x50            jt 18 jf 19
(008) jeq      #0x800           jt 9 jf 19
(009) ldb      [23]
(010) jeq      #0x6             jt 11 jf 19
(011) ldh      [20]
(012) jset     #0x1fff          jt 19 jf 13
(013) ldxb     4*([14]&0xf)
(014) ldh      [x + 14]
(015) jeq      #0x50            jt 18 jf 16
(016) ldh      [x + 16]
(017) jeq      #0x50            jt 18 jf 19
(018) ret      #262144
(019) ret      #0
```
BPF to find "tcp" and "port 80". This would have to be done with 2 separate statements. Can only check for IPv4.:
```
root@linux-opstation-pysn:~# tcpdump -d 'tcp[0:2]=80 || tcp[2:2]=80'
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 12
(002) ldb      [23]
(003) jeq      #0x6             jt 4 jf 12
(004) ldh      [20]
(005) jset     #0x1fff          jt 12 jf 6
(006) ldxb     4*([14]&0xf)
(007) ldh      [x + 14]
(008) jeq      #0x50            jt 11 jf 9
(009) ldh      [x + 16]
(010) jeq      #0x50            jt 11 jf 12
(011) ret      #262144
(012) ret      #0

```
BPF to find DSCP:
```
root@linux-opstation-pysn:~# tcpdump -d 'ip[1]&252=184'
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 6
(002) ldb      [15]                = looks at byte 15 which is the TOS field (or DSCP and ECN).
(003) and      #0xfc               = Applies a mask of 0xfc (252) which only checks the high order 6 bits and ignores the low order 2 bits.
(004) jeq      #0xb8            jt 5 jf 6  = Jump to 5 if it equals 0xb8 (184) else goto 6.
(005) ret      #262144
(006) ret      #0
```

BPF to check the TCP flags for SYN+ACK. This must be an exact match.
```
root@linux-opstation-pysn:~# tcpdump -d tcp[13]=17
(001) jeq      #0x800           jt 2 jf 10
(002) ldb      [23]
(003) jeq      #0x6             jt 4 jf 10
(004) ldh      [20]
(005) jset     #0x1fff          jt 10 jf 6
(006) ldxb     4*([14]&0xf)
(007) ldb      [x + 27]               = Load a byte at 27 + value of line 5. This will take you to the TCP flags field
(008) jeq      #0x11            jt 9 jf 10   = jump to 9 if it equals 0x11 (17) which is both the SYN and ACK flags turned on and rest of flags off.
(009) ret      #262144
(010) ret      #0
```
This BPF will also check for SYN+ACK but other flags may/may not be set.
```
root@linux-opstation-pysn:~# tcpdump -d 'tcp[13]&17=17'
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 11
(002) ldb      [23]
(003) jeq      #0x6             jt 4 jf 11
(004) ldh      [20]
(005) jset     #0x1fff          jt 11 jf 6
(006) ldxb     4*([14]&0xf)
(007) ldb      [x + 27]                = Load a byte at 27 + value of line 5. This will take you to the TCP flags field
(008) and      #0x11                 = Applies a mask to only check the SYN and ACK fields. Other bits are ignored.
(009) jeq      #0x11            jt 10 jf 11   = jump to 10 if it equals 0x11 (17) which is both the SYN and ACK flags turned on and rest of flags are ignored.
(010) ret      #262144
(011) ret      #0
```
BPF will just check the SYN+ACK bits to ensure that the combined value do not equal 0. Other flags are not matched.
```
root@linux-opstation-pysn:~# tcpdump -d 'tcp[13]&17!=0'
(000) ldh      [12]
(001) jeq      #0x800           jt 2 jf 10
(002) ldb      [23]
(003) jeq      #0x6             jt 4 jf 10
(004) ldh      [20]
(005) jset     #0x1fff          jt 10 jf 6
(006) ldxb     4*([14]&0xf)
(007) ldb      [x + 27]
(008) jset     #0x11            jt 9 jf 10   = Checks the SYN+ACK bits to see if they have a value. Other flags are ignored.
(009) ret      #262144
(010) ret      #0
```

BPF that will check for VLAN tag and VLAN 111
```
root@linux-opstation-pysn:~# tcpdump -d 'ether[12:2]=0x8100 && ether[14:2] & 0x0fff = 0x006f'
(000) ldh      [12]                  = load a half word at byte 1
(001) jeq      #0x8100          jt 2 jf 6     =  jump to 2 if it equals 0x8100 else jump to 6
(002) ldh      [14]                  = load a half word at byte 14 which will be the PCP/DEI and VLAN ID field.
(003) and      #0xfff                 = applies a mask of 0x0fff which will ignore the PCP/DEI field and only match on the VLAN ID field
(004) jeq      #0x6f            jt 5 jf 6     = jump to 5 if it equals 0x006f (111). Notice that this is showing the leading zero's that normally are removed to identify that we are looking for the value of the entire 2 bytes. Else goto 6.
(005) ret      #262144
(006) ret      #0
```

Filter Format Example:
- TCPDump uses two different formats for tcpdump filters, macro, and BPF format.
  - Macro:
  ```
  <macro> <value>
  not port 22
  ```
  - BPF:
  ```
  <protocol header> [offset:length] <relation> <value>
  tcp[2:2] !=22
  ```










