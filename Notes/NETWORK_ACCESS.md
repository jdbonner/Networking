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
###Bus
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
![a](https://www.cisco.com/content/dam/cisco-cdc/site/us/en/images/networking/Routing_Listing_Rendering_758x484_v2.png)

## Ethernet Timing
Speed      Bit-time
10 Mbps    100ns
100 Mbps   10ns
1 Gbps     1ns
10 Gbps    .1ns
100 Gbps   .01ns

















![a]()


