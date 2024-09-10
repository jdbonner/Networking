# Access Controls Network
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_3_understand_network_based_filtering

```
OUTCOMES
Demonstrate the Use of Firewalls

Discuss Filtering with Routers

Explain Filtering with an Intrusion Detection System (IDS)

Discuss Operation System Filtering
Rationale
Cyber professionals should prioritize learning network-based
filtering, firewall types, ACLs, IDS, IPS, and tools like
Snort to bolster network security effectively. These components
provide crucial capabilities such as traffic control, threat
detection, and rapid response to cyber threats. Mastery of
firewall types and ACLs enables precise access control and
policy enforcement, while IDS and IPS systems monitor and
mitigate potential threats in real-time. Tools like Snort
enhance incident analysis and response, ensuring proactive
defense against evolving cybersecurity challenges and
safeguarding organizational networks from unauthorized access
and data breaches.
```

## Describe firewall type
- Zone-Based Policy Firewall (Zone-Policy Firewall, ZBF or ZFW)
- Host Based Firewalls
- Network Based Firewalls

### Interpret a data flow diagram given a set of firewall rules
![](https://ptgmedia.pearsoncmg.com/images/chap2_9781587144462/elementLinks/02fig15_alt.jpg)

### Determine positioning of filtering devices on a network
- Determine network segments
- Conduct Audit
- Filtering devices we need
- Device placement

### Typical locations for filtering devices
- IPS
- Firewalls
- Routers
- Switches

### Filtering Device Placement example
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/placement4.jpg)


## Interpret Cisco access control list (ACL)
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_4_interpret_cisco_access_control_list_acl



### ACL numbering & naming conventions
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/T4a_ACL_Naming2.jpg)


### Syntax to create Access Lists
```
Demo> enable #enter privileged exec mode
Demo# configure terminal #enter global config mode
Demo(config)# access-list 37 ... (output omitted) ...
Demo(config)# ip access-list standard block_echo_request
Demo(config)# access-list 123  ... (output omitted) ...
Demo(config)# ip access-list extended zone_transfers
```
> What types of ACLs were created?



### Standard Numbered ACL Syntax
```
router(config)# access-list {1-99 | 1300-1999}  {permit|deny}  {source IP add}
                {source wildcard mask}
router(config)#  access-list 10 permit host 10.0.0.1
router(config)#  access-list 10 deny 10.0.0.0 0.255.255.255
router(config)#  access-list 10 permit any
```


### Standard Named ACL Syntax
```
router(config)# ip access-list standard [name]
router(config-std-nacl)# {permit | deny}  {source ip add}  {source wildcard mask}
router(config)#  ip access-list standard CCTC-STD
router(config-std-nacl)#  permit host 10.0.0.1
router(config-std-nacl)#  deny 10.0.0.0 0.255.255.255
router(config-std-nacl)#  permit any
```

### Extended Numbered ACL Syntax
```
router(config)# access-list {100-199 | 2000-2699} {permit | deny} {protocol}
                {source IP add & wildcard} {operand: eq|lt|gt|neq}
                {port# |protocol} {dest IP add & wildcard} {operand: eq|lt|gt|neq}
                {port# |protocol}
router(config)# access-list 144 permit tcp host 10.0.0.1 any eq 22
router(config)# access-list 144 deny tcp 10.0.0.0 0.255.255.255 any eq telnet
router(config)# access-list 144 permit icmp 10.0.0.0 0.255.255.255 192.168.0.0
                0.0.255.255 echo
router(config)# access-list 144 deny icmp 10.0.0.0 0.255.255.255 192.168.0.0
                0.0.255.255 echo-reply
router(config)# access-list 144 permit ip any any
```

### Extended Named ACL Syntax
```
router(config)# ip access-list extended  [name]
router(config-ext-nacl)# [sequence number] {permit | deny} {protocol}
                         {source IP add & wildcard} {operand: eq|lt|gt|neq}
                         {port# |protocol} {dest IP add & wildcard} {operand:
                         eq|lt|gt|neq} {port# |protocol}
router(config)# ip access-list extended CCTC-EXT
router(config-ext-nacl)# permit tcp host 10.0.0.1 any eq 22
router(config-ext-nacl)# deny tcp 10.0.0.0 0.255.255.255 any eq telnet
router(config-ext-nacl)# permit icmp 10.0.0.0 0.255.255.255 192.168.0.0
                         0.0.255.255 echo
router(config-ext-nacl)# deny icmp 10.0.0.0 0.255.255.255 192.168.0.0
                         0.0.255.255 echo-reply
router(config-ext-nacl)# permit ip any any
```

### ACLs can be used for:
- Filtering traffic in/out of a network interface.
- Permit or deny traffic to/from a router VTY line.
- Identify authorized users and traffic to perform NAT.
- Classify traffic for Quality of Service (QoS).
- Trigger dial-on-demand (DDR) calls.
- Control Bandwidth.
- Limit debug command output.
- Restrict the content of routing updates.


### ACLs rules
- One ACL per interface, protocol and direction
- Must contain one permit statement
- Read top down
- Standard ACL generally applied closer to traffic destination
- Extended ACL generally applied closer to traffic source


### ACLs rules
- Inbound processed before routing
- Outbound processed after routing
- Does not apply for SSH or telnet traffic to device
- Does not apply to traffic from the device
- Only standard ACLs on VTY lines


### Apply an ACL to an interface or line
```
router(config)#  interface {type} {mod/slot/port}
router(config)#  ip access-group {ACL# | name} {in | out}
router(config)#  interface s0/0/0
router(config-if)#  ip access-group 10 out
router(config)#  interface g0/1/1
router(config-if)#  ip access-group CCTC-EXT in
router(config)#  line vty 0 15
router(config)#  access-class CCTC-STD in
```

## ACL Placement
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_4_7_acl_placement


### ACL Placement 1
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/aclplacement.png)
> Where would you place a Standard ACL (Router and Interface) to block traffic from host 10.3.0.4 to host 10.5.0.7? Would it be in or outbound?

### ACL Placement 2
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/aclplacement.png)
> Where would you place an Extended ACL to block traffic from host 10.1.0.1 to 10.5.0.17? Would it be in or outbound?


### ACL Placement 3
- Interpret this ACL:
```
ip access-list 101 deny udp host 19.3.0.29 10.5.0.0 0.0.0.255 eq 69
ip access-list 101 deny tcp any 10.3.0.0 0.0.0.255 eq 22
ip access-list 101 deny tcp any 10.1.0.0 0.0.0.255 eq 23
ip access-list 101 deny icmp any 10.5.0.0 0.0.0.255 echo
ip access-list 101 deny icmp any 10.5.0.0 0.0.0.255 echo-reply
```
- What Type of list is this?
- What would it do?
- Where should it be placed (use diagram on previous slide)?
- What direction?


## Understand Intrusion Detection or Prevention Systems
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_5_understand_intrusion_detection_or_prevention_systems


### Contrast Intrusion Detection Systems and Intrusion Prevention Systems
- Placement
  - In line
  - or not

### Common IDS and IPS
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/T13_IDSList.jpg)


### Discuss Signature vs Behavior based detection
- Recognition Methods
  - Signature
  - Heuristic aka Behavioral


### Construct advanced IDS (snort) rules
- Installation Directory
  - /etc/snort
- Configuration File
  - /etc/snort/snort.conf
- Rules Directory
  - /etc/snort/rules

### Construct advanced IDS (snort) rules
- Rule naming
  - [name].rules
- Default Log Directory
  - /var/log/snort


### Construct advanced IDS (snort) rules
- Common line switches
  - -D - to run snort as a daemon
  - -c - to specify a configuration file when running snort
  - -l - specify a log directory
  - -r - to have snort read a pcap file


### Construct advanced IDS (snort) rules
- To run snort as a Daemon
```
sudo snort -D -c /etc/snort/snort.conf -l /var/log/snort
```
- To run snort against a PCAP
```
sudo snort -c /etc/snort/rules/file.rules -r file.pcap
```

### Snort IDS/IPS rule - Header
```
[action] [protocol] [s.ip] [s.port] [direction] [d.ip] [d.port] ( match conditions ;)
* Action - alert, log, pass, drop, or reject
* Protocol - TCP, UDP, ICMP, or IP
* Source IP address - one IP, network, [IP range], or any
* Source Port - one, [multiple], any, or [range of ports]
* Direction - source to destination or both
* Destination IP address - one IP, network, [IP range], or any
* Destination port - one, [multiple], any, or [range of ports]
```

### Snort Rule Options
- Categories
  - General
  - Payload detection
  - Non-Payload detection
  - Post detection
  - Thresholding and suppression


### Snort IDS/IPS General rule options:
```
* msg:"text" - specifies the human-readable alert message
* reference: - links to external source of the rule
* sid: - used to uniquely identify Snort rules (required)
* rev: - uniquely identify revisions of Snort rules
* classtype: - used to describe what a successful attack would do
* priority: - level of concern (1 - really bad, 2 - badish, 3 - informational)
* metadata: - allows a rule writer to embed additional information about the rule
```
### Snort IDS/IPS Payload detection options:
```
* content:"text" - looks for a string of text.
* content:"|binary data|" - to look for a string of binary HEX
* nocase - modified content, makes it case insensitive
* depth: - specify how many bytes into a packet Snort should search for the
           specified pattern
* offset: - skips a certain number of bytes before searching (i.e. offset: 12)
* distance: - how far into a packet Snort should ignore before starting to
              search for the specified pattern relative to the end of the
              previous pattern match
* within: - modifier that makes sure that at most N bytes are between pattern
            matches using the content keyword
```

### Snort IDS/IPS Non-Payload detection options:
```
* flow: - direction (to/from client and server) and state of connection
         (established, stateless, stream/no stream)
* ttl: - The ttl keyword is used to check the IP time-to-live value.
* tos: - The tos keyword is used to check the IP TOS field for a specific value.
* ipopts: - The ipopts keyword is used to check if a specific IP option is present
* fragbits: - Check for R|D|M ip flags.
* dsize: - Test the packet payload size
* seq: - Check for a specific TCP sequence number
* ack: - Check for a specific TCP acknowledge number.
* flags: - Check for E|C|U|A|P|R|S|F|0 TCP flags.
* itype: - The itype keyword is used to check for a specific ICMP type value.
* icode: - The icode keyword is used to check for a specific ICMP code value.
```
### Snort IDS/IPS Post detection options:
```
* logto: - The logto keyword tells Snort to log all packets that trigger this rule to
           a special output log file.
* session: - The session keyword is built to extract user data from TCP Sessions.
* react: - This keyword implements an ability for users to react to traffic that
           matches a Snort rule by closing connection and sending a notice.
* tag: - The tag keyword allow rules to log more than just the single packet that
         triggered the rule.
* detection_filter - defines a rate which must be exceeded by a source or destination
                     host before a rule can generate an event.
```
### Snort IDS/IPS Thresholding and suppression options:
```
threshold: type [limit | threshold | both], track [by_src | by_dst],
count [#], seconds [seconds]

* limit - alerts on the 1st event during defined period then ignores the rest.
* threshold - alerts every [x] times during defined period.
* both - alerts once per time internal after seeing [x] amount of occurrences
         of event. It then ignores all other events during period.
* track - rate is tracked either by source IP address, or destination IP address
* count - number of rule matching in [s] seconds that will cause event_filter
          limit to be exceeded
* seconds - time period over which count is accrued. [s] must be nonzero value
```

### Snort rule example
- Look for anonymous ftp traffic:
```
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous";
sid:2121; )
```
- This will cause the pattern matcher to start looking at byte 6 in the payload)
```
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous";
offset:5; sid:2121; )
```

### Snort rule example
- This will search the first 14 bytes of the packet looking for the word “anonymous”.
```
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous";
depth:14; sid:2121; )
```
- Deactivates the case sensitivity of a text search.
```
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous";
nocase; sid:2121; )
```
### Snort rule example
- ICMP ping sweep
```
alert icmp any any -> 10.10.0.40 any (msg: "NMAP ping sweep Scan";
dsize:0; itype:8; icode:0; sid:10000004; rev: 1; )
```
- Look for a specific set of Hex bits (NoOP sled)
```
alert tcp any any -> any any (msg:"NoOp sled"; content: "|9090 9090 9090|";
sid:9090; rev: 1; )
```

### Snort rule example
- Telnet brute force login attempt
```
alert tcp any 23 -> any any (msg:"TELNET login incorrect";
content:"Login incorrect"; nocase; flow:established, from_server;
threshold: type both, track by_src, count 3, seconds 30;
classtype: bad-unknown; sid:2323; rev:6; )
```

### Snort Demonstration
- Snort DEMO


## Interpret the effects of IDS/IPS rules on network traffic
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_5_5_interpret_the_effects_of_ids_ips_rules_on_network_traffic

### IDS/IPS Performance
- True Positive (TP)
- True Negative (TN)
- False Positive (FP)
- False Negative (FN)


### Failed IDS/IPS
- Fail open
- Fail close

### Insertion Attack
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/insertion.png)


### Evasion Attack
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/evasion.png)


### Technical Attacks on IDS/IPS
- packet sequence manipulation
- fragmenting payload
- overlapping fragments with different reassembly by devices
- Manipulating TCP headers
- Manipulating IP options
- Sending data during the TCP connection setup

### Non-Technical attacks against IDS/IPS
- attacking during periods of low manning
- Example - Ramadan 2012 Saudi Aramco attack
- attacking during a surge in activity
- Example - Target Corp. Point of Sale machines during the Thanksgiving-Christmas 2013 shopping season


### Strengthening Defensive Systems
- Linking IDS/IPS to other tools
- Multiconfig
- Tuning
- HIDS and File Integrity


















