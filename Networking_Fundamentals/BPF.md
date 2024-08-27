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
idk fam

Basic Analysis - tcp flags
What is the Berkeley Packet Filter, using tcpdump, to capture packets with only the ACK/RST or ACK/FIN flag set, utilizing the correct Transport Layer Header? There should be 1201 packets.






