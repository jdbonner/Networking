# Access Control Hosts

```
OUTCOMES
Explain Filtering Device and Mechanisms

Discuss Operation System Filtering

Demonstrate the Construction of Internet Protocol (IP) Tables Rules
Rationale
Cyber professionals benefit immensely from mastering host-based
filtering, iptables, and nftables as these tools are crucial for
enhancing network security. They enable precise control over
network traffic, support defense-in-depth strategies, and empower
swift responses to cyber threats. Proficiency in iptables and
nftables allows for customizable firewall configurations tailored
to organizational needs, ensuring robust protection of sensitive
data and maintaining operational integrity against potential
attacks.
```
## Describe differences among traffic filtering methods and technologies
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_1_describe_differences_among_traffic_filtering_methods_and_technologies

### Why filter traffic?
- Block malicious traffic
- Decrease load on network infrastructure
- Ensure data flows in an efficient manner
- Ensure data gets to intended recipients and only intended recipients
- Obfuscate network internals


### Practical applications for filtering
- Network Traffic - allow or block traffic to/from remote locations.
- Email addresses - to block unwanted email to reduce risk or increase productivity
- Computer applications in an organization environment - for security from vulnerable software
- MAC filtering - also for security to allow only specific computers access to a network

## Network Traffic Filtering Concepts
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_1_1_network_traffic_filtering_concepts

### Network Traffic Filtering Concepts
- 1. Protocols Operation
- 2. Header Analysis
- 3. Network Reconnaissance
- 4. Tunnel Analysis
- 5. IOA and IOC
- 6. Malware Analysis

### Defense in Depth
- 1. Perimeter Security
- 2. Network Security
- 3. Endpoint Security
- 4. Application and OS Security
- 5. Data Security

### Default policies
- Explicit - precisely and clearly expressed
- Implicit - implied or understood


### Block-Listing vs Allow-Listing
- Block-Listing (Formerly Black-List)
  - Implicit ACCEPT
  - Explicit DENY
- Allow-Listing (Formerly White-List)
  - Implicit DENY
  - Explicit ACCEPT

### Discuss filtering device types
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/T1_Filtering_Devices_Mechanisms&Layer.jpg)

### Operation Modes
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/r-t_mode.png)

### Firewall Filtering Methods
- Stateless (Packet) Filtering (L3+4)
- Stateful Inspection (L4)
- Circuit-Level (L5)
- Application Layer (L7)
- Next Generation (NGFW) (L7)

### Software vs Hardware vs Cloud Firewalls
- Software - typically host-based
- Hardware - typically network-based
- Cloud - provided as a service

### Traffic Directions
- A to B
  - Traffic originating from the localhost to the remote-host
    - You (the client) are the client sending traffic to the server.
  - Return traffic from that remote-host back to the localhost.
    - The server is responding back to you (the client).

### Traffic Directions
- B to A
  - Traffic originating from the remote-host to the localhost.
    - A client is trying to connect to you (the server)
  - Return traffic from the localhost back to the remote-host.
    - You (the server) are responding back to the client.

### Basic filtering intent
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Filter_intentv4.jpg)

### Basic filtering intent
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Filter_intent_example.jpg)

## Understand Host Based Filtering
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_understand_host_based_filtering


### Windows, Linux, or MAC
- Windows - Norton, Mcafee, ZoneAlarm, Avast, etc.
- Linux - iptables, nftables, UFW, firewalld.
- MAC - Little Snitch, LuLu, Vallum, etc.


### Netfilter framework
- Made to provide:
- packet filtering
- stateless/stateful Firewalls
- network address and port translation (NAT and PAT)
- other packet manipulation


### Netfilter hooks - > Chain
- NF_IP_PRE_ROUTING → PREROUTING
- NF_IP_LOCAL_IN → INPUT
- NF_IP_FORWARD → FORWARD
- NF_IP_LOCAL_OUT → OUTPUT
- NF_IP_POST_ROUTING → POSTROUTING

### Chain flow
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/IPtables.png)

### Netfilter paradigm
- 1. tables - contain chains
- 2. chains - contain rules
- 3. rules - dictate what to match and what actions to perform on packets when packets match a rule

### Separate applications
> Netfilter created several (separate) applications to filter on different layer 2 or layer 3+ protocols.
- iptables - IPv4 packet administration
- ip6tables - IPv6 packet administration
- ebtables - Ethernet Bridge frame table administration
- arptables - arp packet administration


## Configure iptables filtering rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_2_3_tables_of_iptables


### Tables of iptables
- filter - default table. Provides packet filtering.
- nat - used to translate private ←→ public address and ports.
- mangle - provides special packet alteration. Can modify various fields header fields.
- raw - used to configure exemptions from connection tracking.
- security - used for Mandatory Access Control (MAC) networking rules.

### Chains of iptables
- PREROUTING - packets entering NIC before routing
- INPUT - packets to localhost after routing
- FORWARD - packets routed from one NIC to another. (needs to be enabled)
- OUTPUT - packets from localhost to be routed
- POSTROUTING - packets leaving system after routing


### Chains assigned to each Table
- filter - INPUT, FORWARD, and OUTPUT
- nat - PREROUTING, POSTROUTING, INPUT, and OUTPUT
- mangle - All chains
- raw - PREROUTING and OUTPUT
- security - INPUT, FORWARD, and OUTPUT


### Common iptable options
```
-t - Specifies the table. (Default is filter)
-A - Appends a rule to the end of the list or below specified rule
-I - Inserts the rule at the top of the list or above specified rule
-R - Replaces a rule at the specified rule number
-D - Deletes a rule at the specified rule number
-F - Flushes the rules in the selected chain
-L - Lists the rules in the selected chain using standard formatting
-S - Lists the rules in the selected chain without standard formatting
-P - Sets the default policy for the selected chain
-n - Disables inverse lookups when listing rules
--line-numbers - Prints the rule number when listing rules
```

### Common iptable options
```
-p - Specifies the protocol
-i - Specifies the input interface
-o - Specifies the output interface
--sport - Specifies the source port
--dport - Specifies the destination port
-s - Specifies the source IP
-d - Specifies the destination IP
-j - Specifies the jump target action
```
### iptables syntax
```iptables -t [table] -A [chain] [rules] -j [action]```
- Table: filter*, nat, mangle
- Chain: INPUT, OUTPUT, PREROUTING, POSTROUTING, FORWARD

### iptables rules syntax
```
-i [ iface ]
-o [ iface ]
-s [ ip.add | network/CIDR ]
-d [ ip.add | network/CIDR ]
```

### iptables rules syntax
```
-p icmp [ --icmp-type type# { /code# } ]
-p tcp [ --sport | --dport { port1 |  port1:port2 } ]
-p tcp [ --tcp-flags SYN,ACK,PSH,RST,FIN,URG,ALL,NONE ]
-p udp [ --sport | --dport { port1 | port1:port2 } ]
```

### iptables rules syntax
```
-m to enable iptables extensions:
-m state --state NEW,ESTABLISHED,RELATED,UNTRACKED,INVALID
-m mac [ --mac-source | --mac-destination ] [mac]
-p [tcp|udp] -m multiport [ --dports | --sports | --ports { port1 | port1:port15 } ]
-m bpf --bytecode [ 'bytecode' ]
-m iprange [ --src-range | --dst-range { ip1-ip2 } ]
```

### iptables action syntax
- ACCEPT - Allow the packet
- REJECT - Deny the packet (send an ICMP reponse)
- DROP - Deny the packet (send no response)
```-j [ ACCEPT | REJECT | DROP ]```


### Modify iptables
- Flush table
```iptables -t [table] -F```
- Change default policy
```iptables -t [table] -P [chain] [action]```
- Lists rules with rule numbers
```iptables -t [table] -L --line-numbers```
- Lists rules as commands interpreted by the system
```iptables -t [table] -S```

### Modify iptables (continued)
- Inserts rule before Rule number
```iptables -t [table] -I [chain] [rule num] [rules] -j [action]```
- Replaces rule at number
```iptables -t [table] -R [chain] [rule num] [rules] -j [action]```
- Deletes rule at number
```iptables -t [table] -D [chain] [rule num]```


### iptables Demonstration
- iptables DEMO


## Configure NFTables filtering rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_3_configure_nftables_filtering_rules


### NFTable Enhancements
- One table command to replace:
  - iptables
  - ip6tables
  - arptables
  - ebtables
- simpler, cleaner syntax
- less code duplication resulting in faster execution
- simultaneous configuration of IPv4 and IPv6


### NFTables families
- ip - IPv4 packets
- ip6 - IPv6 packets
- inet - IPv4 and IPv6 packets
- arp - layer 2
- bridge - processing traffic/packets traversing bridges.
- netdev - allows for user classification of packets - nftables passes up to the networking stack (no counterpart in iptables)


### NFTables hooks
- ingress - netdev only
- prerouting
- input
- forward
- output
- postrouting


### NFTables Chain-types
> There are three chain types:
- filter - to filter packets - can be used with arp, bridge, ip, ip6, and inet families
- route - to reroute packets - can be used with ip and ipv6 families only
- nat - used for Network Address Translation - used with ip and ip6 table families only



### NFTables syntax
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_3_4_nftables_syntax

### 1. Create the Table
```
nft add table [family] [table]
[family] = ip*, ip6, inet, arp, bridge and netdev.
[table] = user provided name for the table.
```


### 2. Create the Base Chain
```
nft add chain [family] [table] [chain] { type [type] hook [hook]
    priority [priority] \; policy [policy] \;}
* [chain] = User defined name for the chain.
* [type] =  can be filter, route or nat.
* [hook] = prerouting, ingress, input, forward, output or
         postrouting.
* [priority] = user provided integer. Lower number = higher
             priority. default = 0. Use "--" before
             negative numbers.
* ; [policy] ; = set policy for the chain. Can be
              accept (default) or drop.
 Use "\" to escape the ";" in bash
```

### 3. Create a rule in the Chain
```
nft add rule [family] [table] [chain] [matches (matches)] [statement]
* [matches] = typically protocol headers(i.e. ip, ip6, tcp,
            udp, icmp, ether, etc)
* (matches) = these are specific to the [matches] field.
* [statement] = action performed when packet is matched. Some
              examples are: log, accept, drop, reject,
              counter, nat (dnat, snat, masquerade)
```

### Rule Match options
```
ip [ saddr | daddr { ip | ip1-ip2 | ip/CIDR | ip1, ip2, ip3 } ]
tcp flags { syn, ack, psh, rst, fin }
tcp [ sport | dport { port1 | port1-port2 | port1, port2, port3 } ]
udp [ sport| dport { port1 | port1-port2 | port1, port2, port3 } ]
icmp [ type | code { type# | code# } ]
```

### Rule Match options
```
ct state { new, established, related, invalid, untracked }
iif [iface]
oif [iface]
```

### Modify NFTables
```
nft { list | flush } ruleset
nft { delete | list | flush } table [family] [table]
nft { delete | list | flush } chain [family] [table] [chain]
```
### Modify NFTables
- List table with handle numbers
```nft list table [family] [table] [-a]```
- Adds after position
```nft add rule [family] [table] [chain] [position <position>] [matches] [statement]```
- Inserts before position
```nft insert rule [family] [table] [chain] [position <position>] [matches] [statement]```
- Replaces rule at handle
```nft replace rule [family] [table] [chain] [handle <handle>] [matches] [statement]```
- Deletes rule at handle
```nft delete rule [family] [table] [chain] [handle <handle>]```


### Modify NFTables
- To change the current policy
```nft add chain [family] [table] [chain] { \; policy [policy] \;}```

### NFTables Demonstration
- NFTables DEMO


## Configure iptables nat rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_4_configure_iptables_nat_rules

### NAT & PAT operators & Chains
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/T55_NAT&PAT_Chains.png)

### Source NAT
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Source_NAT_image.png)
```iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.1 -j SNAT --to 1.1.1.1```

### Source NAT
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/T16_Source_NAT_Graphic.png)
```iptables -t nat -A POSTROUTING -p tcp -o eth0 -s 192.168.0.1 -j SNAT --to 1.1.1.1:9001```
### Source NAT
```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE```
### Destination NAT
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Dest_NAT_image.png)
```iptables -t nat -A PREROUTING -i eth0 -d 8.8.8.8 -j DNAT --to 10.0.0.1```

### Destination NAT
```
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 22 -j DNAT --to 10.0.0.1:22
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 10.0.0.2:80
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 443 -j DNAT --to 10.0.0.3:443
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
```



## Configure NFTables nat rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_5_configure_nftables_nat_rules


### Creating nat tables and chains
- Create the NAT table
```nft add table ip NAT```
- Create the NAT chains
```
nft add chain ip NAT PREROUTING { type nat hook prerouting priority 0 \; }
nft add chain ip NAT POSTROUTING { type nat hook postrouting priority 0 \; }
```

### Source NAT
```
nft add rule ip NAT POSTROUTING ip saddr 10.10.0.40 oif eth0 snat 144.15.60.11
nft add rule ip NAT POSTROUTING oif eth0 masquerade
```
### Destination NAT
```
nft add rule ip NAT PREROUTING iif eth0 ip daddr 144.15.60.11 dnat 10.10.0.40
nft add rule ip NAT PREROUTING iif eth0 tcp dport { 80, 443 } dnat 10.1.0.3
nft add rule ip NAT PREROUTING iif eth0 tcp dport 80 redirect to 8080
```

## Configure iptables mangle rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_6_configure_iptables_mangle_rules


### Mangle examples with iptables
```
iptables -t mangle -A POSTROUTING -o eth0 -j TTL --ttl-set 128
iptables -t mangle -A POSTROUTING -o eth0 -j DSCP --set-dscp 26
```

## Configure nftables mangle rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_6_2_mangle_examples_with_nftables

### Mangle examples with nftables
```
nft add table ip MANGLE
nft add chain ip MANGLE INPUT {type filter hook input priority 0 \; policy accept \;}
nft add chain ip MANGLE OUTPUT {type filter hook output priority 0 \; policy accept \;}
nft add rule ip MANGLE OUTPUT oif eth0 ip ttl set 128
nft add rule ip MANGLE OUTPUT oif eth0 ip dscp set 26
```

























