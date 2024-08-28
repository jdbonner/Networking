# CTF

## Task 3
BPF
Basic Analysis - ttl
What is the Berkeley Packet Filter, using tcpdump, to capture all packets with a ttl of 64 and less, utilizing the IPv4 or IPv6 Headers? There should be 8508 packets.
sudo tcpdump -n 'ip and (ip[8] <= 64) or ip6 and (ip6[7] <= 64)' -r BPFCheck.pcap | wc -l

Basic Analysis - dont fragment
What is the Berkeley Packet Filter, using tcpdump, to capture all IPv4 packets with at least the Dont Fragment bit set? There should be 2321 packets.
sudo tcpdump -n 'ip[6] & 0x40 != 0' -r BPFCheck.pcap | wc -l

Basic Analysis - high port
What is the Berkeley Packet Filter, using tcpdump, to capture traffic with a Source Port higher than 1024, utilizing the correct Transport Layer Headers? There should be 7805 packets.
sudo tcpdump -n 'tcp[0:2] > 1024 || udp[0:2] > 1024' -r BPFCheck.pcap | wc -l

Basic Analysis - udp
What is the Berkeley Packet Filter, using tcpdump, to capture all Packets with UDP protocol being set, utilizing the IPv4 or IPv6 Headers? There should be 1277 packets.
sudo tcpdump -n 'ip[9] = 0x11 || ip6[6] = 0x11' -r BPFCheck.pcap | wc -l

Basic Analysis - tcp flags
What is the Berkeley Packet Filter, using tcpdump, to capture packets with only the ACK/RST or ACK/FIN flag set, utilizing the correct Transport Layer Header? There should be 1201 packets.
sudo tcpdump -n 'tcp[13]=0x14||tcp[13]=0x11' -r BPFCheck.pcap | wc -l

Basic Analysis - id
What is the Berkeley Packet Filter, using tcpdump, to capture all packets with an IP ID field of 213? There should be 10 packets.
Enter the Filter syntax with no spaces
TCPDUMP Primitives are not accepted as answers
sudo tcpdump -n 'ip[4:2]=213' -r BPFCheck.pcap | wc -l


Basic Analysis - vlan
What is the Berkeley Packet Filter, using tcpdump, to capture all traffic that contains a VLAN tag? There should be 182 packets.
Enter the Filter syntax with no spaces
TCPDUMP Primitives are not accepted as answers
sudo tcpdump -n 'ether[12:2]=0x8100' -r BPFCheck.pcap | wc -l

ether[12:4]&0xffff0fff=0x81000001&&ether[16:4]&0xffff0fff=0x8100000A
tcp[13]=0&&ip[16:4]=0x0A0A0A0A
tcp[13]&32=0&&tcp[18:2]>0 
(ip[9]=17||ip[9]=1)&&ip[8]=1
ip[1]>>2=37
ip[9]=16
ip[6]&128=128
ether[12:2]=0x0806
tcp[0:2]=80||tcp[2:2]=80
tcp[2:2]<1024||udp[2:2]<1024
tcp[13]=0x04
tcp[13]=0x12
tcp[13]=0x02
udp[2:2]=53||tcp[2:2]=53||udp[0:2]=53||tcp[0:2]=53
ether[12:2]=0x8100
ip[4:2]=213
tcp[13]=0x14||tcp[13]=0x11
ip[9]=17||ip6[6]=17
tcp[0:2]>1024||udp[0:2]>1024
ip[6]&64!=0
ip[8]>=64
ip[8]<=64||ip6[7]<=64








