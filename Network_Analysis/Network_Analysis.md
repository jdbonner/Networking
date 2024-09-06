# Network Analysis
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html


```
OUTCOMES
Discuss Network Traffic Baselining

Discuss How to Analyze Network Statistics

Demonstrate Network Statistics

Identify Types of Malware
OUTCOMES
Discuss Post Compromise Analysis

Demonstrate Anomaly Analysis

Define Decoding

Demonstrate Decoding
Rationale
Learning about sniffing tools, OS and application fingerprinting,
network baselining, the cyber kill chain, Mitre frameworks, the
diamond model, NIST framework, indicators of attack, indicators
of compromise, and malware is essential for cybersecurity profess-
ionals. These topics provide crucial insights into understanding
network vulnerabilities, identifying potential threats, and
orchestrating effective defense strategies. By mastering these
concepts, professionals can proactively detect, analyze, and
mitigate cyber threats, safeguarding organizational assets and
maintaining robust cybersecurity posture.
Assessment
You will be assessed via CTFd challenges where you will need to score 228/325 points to achieve a 70%.
```



## Describe the use of sniffing tools and methods
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_1_describe_the_use_of_sniffing_tools_and_methods


### Tools
- Sensors
  - In-Line
    - Test Access Point (TAP)
    - Man-in-the-Middle (MitM)
  - Out of Band (Passive)
    - Switched Port Analyzer (SPAN)

### In-line Sensor
- Placed between communicating devices to stop attacks
  - Intrusion Prevention System (IPS)
  - Firewall
- Impacts network latency


### Passive Sensor
- Monitors network segments
- Can detect attacks but cannot stop them
- Gets copies of network traffic
  - Intrusion Detection System (IDS)
- Does not impact network latency

### TAP
- Appliance placed between 2 network devices
- Best for packet collection with no data loss
- Must be placed "in line" of network traffic
- Not Scalable
- Will need several installed to capture traffic for other network segments

### MitM
- Attacker can use ARP or some other method/protocol
- Attackers can sniff or manipulate traffic that flows through them
- Typically must be on the same network as the victim
- Traffic capture is dependent on the attacker’s system and bandwidth


### SPAN
- Configured on the network Switch
- Best for packet collection of traffic from several switch ports at once
- Scalable
- Can have a high degree of packet loss
- Places burden on the network Switch


##  Identify default characteristics for system identification
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_2_identify_default_characteristics_for_system_identification

### Fingerprinting and Host Identification
- Variances in the RFC implementation for different OS’s and systems enables the capability for fingerprinting
- Tools used for fingerprinting and host identification can be used passively(sniffing/fingerprinting) or actively(scanning)

### Fingerprinting
- Active OS fingerprinting
  - Easier
  - Send packets to the target and monitor response
  - Tools:
    - Nmap
    - Xprobe2
    - sinfp3


### Fingerprinting
- Passive OS fingerprinting
  - More difficult
  - Rely on sniffing packets
  - Tools:
    - p0f
    - Ettercap
    - PRADS


### Open Ports and Protocols
- Known Windows/Linux ports
- Known Windows/Linux protocols
- Banner grab service ports


### Known Windows and Linux Ports
- Windows
  - 88 - Kerberos / Domain Controller
  - 137/138/139 - NetBIOS
  - 445 - SMB
- Linux
  - 22 - SSH
  - 111 - SUN RPC

### Ephemeral Ports
- IANA 49152–65535
- Linux 32768–60999
- Windows XP 1025–5000
- Win 7/8/10 use IANA
- Win Server 2008 1025–60000
- Sun Solaris 32768–65535


### Protocol specific identifiers
- HTTP: User-agent strings    # https://useragentstring.com/pages/useragentstring.php
- SSH: Initial connection     # https://goteleport.com/blog/ssh-handshake-explained/
- NetBIOS Name Service        # https://learn.cnd.ca.gov/Microsoft/NamingConvention/#naming-standards-for-servers


### P0F (Passive OS Fingerprinting)
- Looks at variations in initial TTL, fragmentation flag, default IP header packet length, window size, and TCP options
- Configuration stored in:
 > /etc/p0f/p0f.fp


## Perform Network Traffic Baselining
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_3_perform_network_traffic_baselining


### What is Baselining?
- Snapshot of what the network looks like during a time frame
- No industry standard
- 7 days to establish the initial snapshot
- Prerequisite Information


### Network Baseline Objective
- Determines the current state of your network
- Ascertain the current utilization of network resources
- Identify normal vs peak network traffic time frames
- Verify port/protocol usage


### Perform Baselining
- Preparation:
  - Network Diagram
  - Known Servers, Hosts, and Networking devices
  - Known IPs, ports, and protocols
  - Known forbidden IPs, ports, and protocols
  - Known traffic "flows"


### Perform Baselining
- Scope and Objectives:
  - What traffic/protocols to capture?
  - Which network segments?
  - Which days?
  - What times?


## Determine traffic flow through protocol communication analysis
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_determine_traffic_flow_through_protocol_communication_analysis


### Using Wireshark
- Common Display Filters   # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_1_common_wireshark_display_filters
- Protocol Hierarchy       # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_2_protocol_hierarchy
- Conversations            # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_3_conversations
- Endpoints                # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_4_endpoints
- I/O Graph                # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_5_io_graph


### Using Wireshark
- IPv4 and IPv6 Statistics    # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_6_ipv4_and_ipv6_statistics
- Expert Information          # N/A
- File Magic Numbers          # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_7_file_magic_numbers
- Follow Protocol Streams     # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_8_additional_wireshark_filters
- Apply as Filter options     # https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_4_1_8_additional_wireshark_filters



# Perform Network Forensics
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_5_perform_network_forensics

## Methodologies
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_5_1_methodologies

### Hacker Methodologies
- Footprinting
- Network scanning
- Network Enumeration
- Vulnerability Assessment


### Cyber Kill Chain
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/KILLCHAIN.png)


### Mitre ATT&CK
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/attack.png)


### Mitre D3FEND
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/D3FEND.png)

### The Diamond Model
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/diamond.png)

### NIST Cyber Security Framework
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/nist.jpeg)


## Indicators
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_5_2_indicators


### Anomaly Detection
- Indicator of Attack (IOA)
  - Proactive
  - A series of actions that are suspicious together
  - Focus on Intent
  - Looks for what must happen
    - Code execution. persistence, lateral movement, etc.


### Anomaly Detection
- Indicator of Compromise (IOC)
  - Reactive
  - Forensic Evidence
  - Provides Information that can change
    - Malware, IP addresses, exploits, signatures


### Some Indicators
- .exe/executable files
- NOP sled
- Repeated Letters
- Well Known Signatures
- Mismatched Protocols
- Unusual traffic
- Large amounts of traffic/ unusual times


### Signs of IOA
- Destination IP/Ports
- Public Servers/DMZs
- Off-Hours
- Network Scans
- Alarm Events
- Malware Reinfection
- Remote logins
- High amounts of some protocols

### Signs of IOC
- Unusual traffic outbound
- Anomalous user login or account use
- Size of responses for HTML
- High number of requests for the same files
- Using non-standard ports/ application-port mismatch
- Writing changes to the registry/system files
- Unexpected/unusual patching or tasks


## Types of Malware
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_5_3_types_of_malware

### Adware/Spyware
- large amounts of traffic/ unusual traffic
- IOA
  - Destinations
- IOC
  - Unusual traffic outbound


### Virus
- phishing/ watering hole
- IOA
  - Alarm Events, Email protocols
- IOC
  - Changes to the registry/ system files


### Worm
- phishing/ watering hole
- IOA
  - Alarm events
- IOC
  - changes to registry/ system files


### Trojan
- beaconing
- IOA
  - Destinations
- IOC
  - Unusual traffic outbound, unusual tasks, changes to registry/ system files


### Rootkit
- IOA
  - Malware reinfection
- IOC
  - Anomalous user login/ account use


### Backdoor
- IOA
  - Remote logins
- IOC
  - Anomalous user login/ account use


### Botnets
- large amounts of IPs
- IOA
  - Destinations, remote logins
- IOC
  - Unusual tasks, anomalous user login/ account use

### Polymorphic/Metamorphic Malware
- Depends on the malware type/class


### Ransomware
- IOA
  - Destinations, Ports, Malware reinfection
- IOC
  - Unusual traffic outbound, non-standard ports, unusual tasks


### Mobile Code
- IOA
  - Depends on the malware type/class


### BIOS/Firmware Malware
- IOA
  - Malware reinfection
- IOC
  - Depends on the malware type/class




## Determine network anomalies through traffic analysis
https://net.cybbh.io/public/networking/latest/10_analysis/fg.html#_10_6_determine_network_anomalies_through_traffic_analysis


### ICMP Tunneling
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/icmp-tunnel.png)


### ICMP Tunneling
- ICMP PING uses Type 8 and Type 0
- Both should be:
  - 1 for 1
  - Same size and payload
- Look out for:
  - Request/Reply imbalances
  - Abnormal/different payloads

### DNS Tunneling
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/dns-tunnel.png)

### DNS Tunneling
- DNS uses Query/Response
  - 1 Query typically gets 1 response
- Look out for:
  - Query/Response imbalances
  - Abnormal/different payloads
  - Continuous Queries

### HTTP(s) Tunneling
- HTTP is "bursty" in nature
- Client issues request and the server responds
- Look out for:
  - Steady connections
  - HTTPs you will need to check session establishment for abnormalities

### Beaconing
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/beacons.png)

### Beaconing
- Call back to the C&C server
- Gets/sends commands from/to C&C
- Look out for:
  - Beacon Timing
    - Commonly at regular intervals
  - Beacon Size
    - Check-Ins may not have any payloads
    - Orders will have payloads

































