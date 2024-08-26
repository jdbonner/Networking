# Hand Notes

## outcomes
Discuss Network Fundamentals
Describe Security Implications Present in Header Fields
Explain Layer 1 Data Communications and Technologies
Explain Layer 2 Switching and Technologies

## why
Understanding the OSI model, IETF, IANA, IEEE, OSI Layer 1, and
OSI Layer 2 is vital for cybersecurity professionals.
The OSI model provides a structured approach to understanding network
protocols, aiding in the identification and mitigation of
vulnerabilities across different layers. 
Familiarity with organizations like IETF, IANA, and IEEE ensures awareness
of evolving standards and protocols, essential for securing
network infrastructure. 
OSI Layer 1 and Layer 2 knowledge is crucial for detecting and preventing physical and data link
layer attacks, forming the foundation for effective cybersecurity
strategies aimed at safeguarding against a wide range of threats.

Assessment
You will be assessed via CTFd challenges where you will need to score 193/275 points to achieve a 70%.


## OSI MODEL
Session-Application = Data
Transport = Segment/Datagram
Network = Packet
Data Link = Frame
Physical = Bit

## ISO
IETF - RFC's
https://www.rfc-editor.org/rfc-index.html
IANA - Internet Numbers
https://www.iana.org/numbers
IEEE - LAN/WAN electrical standards
https://en.wikipedia.org/wiki/IEEE_Standards_Association

# OSI MODEL in depth
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_2_explain_osi_layer_1_data_communications_and_technologies
# OSI Layer 1 DATA
## Binary
  Base2 - Two symbols ( 0 and 1 )
  Place Values - 27=128, 26=64, 25=32, 24=16, 23=8, 22=4, 21=2, 20=1
  Format - 01000010 01100001 01110011 01100101
  Groupings: bit, nibble, byte, half-word, word
  ![image](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Bits_Nibbles_Bytes.png)

## Decimal
  Base10 - Ten symbols ( 0 to 9 )
  Place Values - 103=1000, 102=100, 101=10, 100=1
  Format - 7, 66, 115, 1012

## Hexadecimal
  Base16 - Sixteen symbols ( 0 to 9 and A to F )
  Place Values - 23=8, 22=4, 21=2, 20=1
  Format - 0x42 0xE3 0x73 0xA5

### Hexadecimal Representation
![image](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Binary_Decimal_Hex.png)

### Decimal to Hexadecimal Conversion 1
![image2](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/HEX_DEC_Conversion_Chart.png)

### Decimal to Hexadecimal Conversion 2
![image3](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/hex1.png)

### Decimal to Hexadecimal Conversion 3
![image4](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/hex2.png)

### Decimal to Hexadecimal Conversion 4
![image5](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/hex3.jpg)

## Base64
  Base64 - 64 symbols ( A-Z, a-z, 0-9, +, / )
  Place Values - 25=32, 24=16, 23=8, 22=4, 21=2, 20=1
  Uses ( = ) to represent a null value (max of 2)
  Format - MTI=, MTIzNA==, MTIzNDU2Nzg=, QmFzZSA2NA==

### Base64 Representation
![ya](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/base64table.png)


# LAN topologies
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_2_2_describe_lan_topologies_and_devices

## Topologies
### Bus
![a](https://www.nakivo.com/blog/wp-content/uploads/2021/04/A-bus-network-topology.webp)
### Star
![a](https://www.nakivo.com/blog/wp-content/uploads/2021/04/The-star-network-topology.webp)
### Ring
![a](https://www.nakivo.com/blog/wp-content/uploads/2021/04/The-ring-network-topology.webp)
### Mesh
![a](https://www.nakivo.com/blog/wp-content/uploads/2021/04/The-mesh-network-topology-the-full-mesh-and-partial-mesh.webp)
### Wireless
![a](https://www.conceptdraw.com/How-To-Guide/picture/Roaming-wireless-LAN-diagram.png)
### Hierarchial
![a](https://ptgmedia.pearsoncmg.com/images/chap1_9781587133329/elementLinks/01fig06_alt.jpg)

## Devices
### Hubs
devices that allow multiple nodes to connect on the same wire (Collision Domain).
![a](https://thecybersecurityman.com/wp-content/uploads/2018/01/hub4.png)
### Repeaters
devices that allow a connection to be extended beyond the normal operational cable or wireless limits.
![a](https://media.startech.com/cms/products/gallery_large/poeext1g60w.main.jpg)
### Switches
devices that allow multiple nodes to connect on the network, but on their own collision domain. The layer 2 originating MAC address of the frame are learned from the incoming frames and are stored in the mac address table memory, also called a Content Addressable Memory (CAM) table.
![a](https://images.spiceworks.com/wp-content/uploads/2022/07/26120446/Ciscos-Industry-Standard-Network-Switch.png)
### Routers
Devices that connect networks
![a](https://www.cisco.com/content/dam/cisco-cdc/site/us/en/images/networking/Routing_Listing_Rendering_758x484_v2.png)

## Ethernet Timing
Bit Time - is the period of time is required for a bit to be placed and sensed on the media. Network speeds are measured by how many bits can be placed or sensed on the media in 1 second. Each increase in speed requires more bits to be sent during the same 1 second internal. To accomplish this the bit-times are reduced.

```
Speed      Bit-time
10 Mbps    100ns
100 Mbps   10ns
1 Gbps     1ns
10 Gbps    .1ns
100 Gbps   .01ns
```

# OSI Layer 2
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_explain_osi_layer_2_protocols_headers_and_technologies

## Technologies
```
Technology  	Standard
Ethernet      802.3(x)
Wireless      802.11(x)
Token Ring    802.5
```

## Data Link Sub-Layers
```
MAC (Medium Access Control)      # https://en.wikipedia.org/wiki/Medium_access_control
LLC (Logical Link Control)       # https://en.wikipedia.org/wiki/Logical_link_control
```

# How Frames work
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_2_explain_why_and_how_frames_are_interpreted_by_different_devices

## Message Formatting method
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Message_Format.png)
  ```
  Header - Layer 2 to Layer 7
    The header contains information related to control and communication processes between different protocol elements for different devices. 
  Data - Payload
    This is the actual data being transmitted which contains the payload. This payload may include another higher level message that consists of the same elements.
  Footer - FCS/CRC
    Commonly referred to as the trailer. The contents vary between communication methods or protocols. 
```

## Encapsulation and Decapsulation
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/PDU_SDU.png)
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/encap.png)


# Identify how switches affect network traffic
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_3_identify_how_switches_affect_network_traffic_and_the_visibility_of_network_traffic_by_other_hosts

## switch operation
> A switch allows multiple users to access the network and can provide segmentation to isolate traffic flow and reduce collisions, relieving network congestion in most cases. 

```
  -Building MAC-Address (CAM) Table             #Switches contain a special type of computer memory called Content-addressable memory (CAM) which allows very fast searching and table lookups.
    -Learns by reading Source MAC addresses     #Switches will dynamically build the MAC address table by examining the source MAC address of the frames received on a port.
  -Forwarding Frames                            #When a switch receives a frame, it will identify and check the destination MAC address information on the frame against the switch’s MAC address table.
    -Decision based on Destination MAC address  #If the MAC address is found in the table, it will then send it out to the appropriate interface only.
```
## Switch Operation
```
  -Switching Modes
    -Cut-Through        #(sometimes called fast forward) only examines the destination address before forwarding it to its destination segment. This is the fastest switching mode but requires the interfaces to be the same speed.
    -Fragment-Free      #read at least 64 bytes of the Ethernet frame before switching it to avoid forwarding Ethernet runt frames (Ethernet frames smaller than 64 bytes). A frame should have a minimum of 46 bytes of payload plus its 18-byte frame header.
    -Store-and-Forward  #accepts and analyzes the entire frame before forwarding it to its destination. It takes more time to examine the entire frame, but it allows the switch to catch certain frame errors and collisions and keep them from propagating bad frames through the network.
```
```
  -CAM Table Overflow Attack      #A CAM (Content Addressable Memory) table overflow attack, also known as a MAC (Media Access Control) flooding attack, is a type of security exploit that targets network switches. This attack aims to overwhelm a switch’s CAM table, which is used to store MAC address-to-port mappings, leading to a denial of service (DoS) condition or facilitating a man-in-the-middle attack.
    -Send frames with bogus source MAC address to switch
    -Cause switch to fill table with bogus addresses
    -Switch will not be able to learn new (valid) MAC addresses
```
```
switch(config)# interface fa0/10
switch(config-if)# switchport port security
switch(config-if)# switchport port security maximum 1
switch(config-if)# switchport port security violation shutdown
```

## MAC Addressing
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_4_describe_mac_addressing
```
Length: 48-bit | 6 byte | 12 Hex
Format:
  Windows: 01-23-45-12-34-56
  Unix/Linux: 01:23:45:12:34:56
  Cisco: 1234.5612.3456
Parts:
  OUI - First 24-bits assigned by IANA
  Vendor Assigned - Last 24-bits assigned by vendor
```

### Describe MAC addressing
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/MAC_Address.png)


### MAC Address Types
```
Unicast: One to one
  8th bit is off
Multicast: One to many
  8th bit is on
Broadcast: One to all
  All bits on
```
### MAC Spoofing
```
Could not be changed at first
Used to be called:
  hardware
  firmware
  burned-in
Now it can be changed w/ software
```
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
## Analyze Data-Link frame headers
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_5_analyze_802_3_frame_headers



### Ethernet Header and frame
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/EthernetFramePreamble.png)
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Ethernet_II_Frame.png)
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/CommonEthertypes.png)

### What is VLAN
```
What is a VLAN?
What are networks like without VLANs?
What are networks like with VLANs?
What is a Trunk Link?
```
### VLAN types
```
Default - VLAN 1
Data - User traffic
Voice - VOIP traffic
Management - Switch and router management
Native - Untagged switch and router traffic
```
### 802.1Q Header
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/802.1QFrame.png)
### 802.1ad Header
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/802.1adframe.png)

### VLAN HOPPING attack
```
Switch Spoofing (DTP)
Single Tagging
Double Tagging (using native VLAN)
SCAPY Example Code                  # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/vlan_hopping.adoc
```

## Describe ARP
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_8_describe_the_address_resolution_protocol_arp

### ARP Header
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/ARP_Header.png)

### ARP types
Types
```
ARP (OP 1 and 2)
A request and response in order to resolve the destination L2 (MAC) address when only the destination L3 (IPv4) address is known.
ARP Request Operation code = 1
ARP Reply Operation code = 2
ARP Request:
When a device needs to communicate with another device on the same network segment but only knows the destination’s IP address, it broadcasts an ARP request message to the entire network.
The ARP request contains the sender’s IP address and MAC address and the IP address of the target device.
ARP Reply:
The device with the IP address specified in the ARP request responds with an ARP reply.
The ARP reply contains the target device’s MAC address.
Once the sender receives the ARP reply, it can use the MAC address to address frames destined for the target device.
```
```
RARP (OP 3 and 4)
A request and response in order to resolve the destination L3 (IPv4) address when only the destination L2 (MAC) is known. (This protocol has been deprecated since the widespread use of protocols like BOOTP and DHCP.)
RARP Request Operation code = 3
RARP Reply Operation code = 4
When a device boots up and has no configured IP address, it broadcasts a RARP request onto the local network.
The RARP request contains the device’s MAC address.
RARP servers on the network receive the broadcast request and check their tables for a corresponding IP address entry associated with the MAC address.
```
```
Proxy ARP (OP 2)
Proxy ARP - A device (router) answers the ARP queries for IP address that is on a different network.
The ARP proxy sees the ARP request and determines that the target Network address is not on the local network segment and is aware of how to reach the destination network.
The proxy will offer its own MAC address in response to the request.
Typically this device is the network gateway and is responsible to forward traffic for other networks.
Maliciously the ARP requests can be intercepted and a Proxy ARP sent as a response to poision the victim’s ARP Cache.
```
```
Gratuitous ARP (OP 2)
Gratuitous ARP - An ARP reply that was not requested.
ARP Reply Operation code = 2
A gratuitous ARP messages is an ARP messages sent by a device to announce its own IP-to-MAC address mapping to other devices on the network.
Gratuitous ARP messages are commonly used during network initialization or to update ARP caches in other devices.
These are commonly used for:
Help in detecting IP conflicts
Assist in updating other system’s ARP cache
To inform switches of the MAC address of the client connected to its port
Helps pre-load other systems ARP cache when the local systems IP interface comes up
Maliciously used to:
Poision a victim’s ARP cache
```
### ARP Cache
```
ARP Cache
All resolved MAC to IP resolutions
If MAC is not in cache then ARP is used
Dynamic entries last from 2-20 minutes
Default gateway is present at minimum
Can be easily duped by attackers
```
ARP Cache - is a collection of Layer 2 to Layer 3 address mappings discovered utilizing the ARP request/response process. When a host needs to send a packet both the L2 and L3 addresses are needed. The host will look in this table to determine if it already knows both the L2 and L3 addresses. If the target is not in the table then a ARP request is initiated. The ARP cache can be populated statically but mostly its done dynamically. This cache can be exploited by attackers with the aim to poison the cache with incorrect information to either perform a DoS or MitM.
```
arp -a
ip neighbor
```
### Man in the middle with arp
```
Poison ARP Cache with:
  Gratuitous ARP
  Proxy ARP
```

## VTP vulnerabilities
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_10_explain_vtp_with_its_vulnerabilities

### VLAN Trunking Protocol (VTP)
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/VTP.png)
> Dynamically add/remove/modify VLANs

### VTP
```
Cisco proprietary
Modes:
  Server
  Client
  Transparent
```
### VTP Vulnerability
Can cause switches to dump all VLAN information
Cause a DoS as switch will not support configured VLANS


## DTP Vulnerabilities
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_11_explain_dtp_with_its_vulnerabilities

### Dynamic Trunking Protocol(DTP)
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/DTP_Chart.png)
> Used to dynamically create trunk links
```
Cisco proprietary
Modes:
  Dynamic-Auto
  Dynamic-Desirable
```
### DTP Vulnerability
```
On by default
Can send crafted messages to form a VLAN trunk link
Recommend to:
  Disable DTP negotiations
  Manually assign as Access or Trunk
```

## Explaining CDP
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_12_explain_cdp_fdp_and_lldp_and_the_security_vulnerabilities

### CDP FDP and LLDP
  Cisco Discovery Protocol (CDP)
  Foundry Discovery Protocol (FDP)
  Link Layer Discovery Protocol (LLDP)

### CDP FDP and LLDP Vulnerability
  Leaks valuable information
```
Clear Text
Enabled by default
Disable it:
  Globally
  Per interface
May require it for VOIP
```

## STP Vulnerabilities
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_13_explain_stp_with_its_vulnerabilities
### Spanning Tree Protocol (STP)
![a](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Spanning-Tree-Protocol-Overview.png)

```
Root decision process

1.Elect root Bridge
2.Identify the Root ports on non-root bridge
3.Identify the Designated port for each segment
4.Set alternate ports to blocking state
```

### Types
```
802.1D STP
Per VLAN Spanning Tree + (PVST+)
802.1w – Rapid Spanning Tree Protocol (RSTP)
Rapid Per VLAN Spanning Tree + (RPVST+)
802.1s (Multiple Spanning Tree)
```


### Spanning tree attack
```
Crafted Bridge Protocol Data units (BPDU)
Used to perform a DoS or MitM
```


## Port Security and Vulnerabilities
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_14_explain_port_security_with_its_vulnerabilities

### Port Security Modes
```
MAC Address Limit:
Port security allows administrators to specify the maximum number of MAC addresses allowed on a switch port.
When enabled, the switch monitors the MAC addresses of devices connected to the port and takes action if the number of MAC addresses exceeds the configured limit.

MAC Address Learning:
When a device sends traffic through a switch port, the switch learns the device’s MAC address and associates it with the port.
The switch maintains a table, known as the MAC address table or CAM table, which maps MAC addresses to switch ports.

Violation Actions:
  Administrators can define violation actions to be taken when port security violations occur.
  Common violation actions include shutting down the port, sending an SNMP trap, or logging a message.
  These actions help alert administrators to potential security breaches and mitigate unauthorized access attempts.
  The following are the possible modes:
    protect - Drops any frames with an unknown source addresses.
    restrict - Same as protect except it additionally creates a violation counter report.
    shutdown(default) - Places the interface into an "error-disabled" state immediately and sends an SNMP trap notification. This is typically the default mode.
```


### Port Security Can help to:
-Restrict unauthorized access        # Restrict the possible allowed MAC addresses to a port to (1).
-Limit MAC address learned on port   #
-Prevent CAM Table Overflow attacks  # Protect against CAM Table Overflow attack. This is were an attacker can flood a switch with hundreds of bogus MAC addresses in effort to fill its CAM tables. Once full, the switch will operate much like a Layer 1 Hub.


### Port Security Vulnerabilities
Dependant on MAC address

MAC spoofing


## Layer 2 Attack mitigation techniques
https://net.cybbh.io/public/networking/latest/01_data/fg.html#_1_3_15_layer_2_attack_mitigation_techniques

### Layer 2 Attack mitigation techniques

Shutdown unused ports
Enable Port Security
IP Source Guard
Manually assign STP Root
BPDU Guard
DHCP Snooping

### Layer 2 Attack mitigation techniques

802.1x
Dynamic ARP inspection (DAI)
Static CAM entries
Static ARP entries
Disable DTP negotiations
Manually assign Access/Trunk ports


















![a]()

![a]()

![a]()


![a]()


