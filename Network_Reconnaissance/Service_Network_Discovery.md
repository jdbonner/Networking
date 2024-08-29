# SERVICE AND NETWORK DISCOVERY
https://net.cybbh.io/public/networking/latest/07_discovery/fg.html


## Reconnaissance Stages
- Passive External
- Active External
- Passive Internal
- Active Internal


### Reconnaissance
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/recon.png)

### Reconnaissance Steps
- Network Footprinting
- Network Scanning
- Network Enumeration
- Vulnerability Assessment

### Network Footprinting
- Collect information relating to target
  - Network
  - Systems
  - Organization

### Network Scanning
- Port Scanning
- Network Scanning
- Vulnerability Scanning


### Network Enumeration
- Network Resource and shares
- Users and Groups
- Routing tables
- Auditing and Service settings
- Machine names
- Applications and banners
- SNMP and DNS details
- Other common services and ports


### Vulnerability Assessment
- Injection
- Broken Authentication
- Sensitive Data Exposure
- XML External Entities
- Broken Access Control
- Security Misconfiguration
- Software/Components with Known Vulnerabilities


## Describe Methods Used for Passive External Discovery
https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_1_describe_methods_used_for_passive_external_discovery
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/recon1.png)


### Useful Sites
- OSINT Framework      # https://osintframework.com/
- Pentest-Standard     # http://www.pentest-standard.org/index.php/Intelligence_Gathering
- SecuritySift         # https://www.securitysift.com/passive-reconnaissance/

### Passive Recon Activities
- Open-Source Intelligence (OSINT)
- Publicly Available Information (PAI)

### Passive Recon Activities
- IP Addresses and Sub-domains
- Identifying External/3rd Party sites
- Identifying People
- Identifying Technologies
- Identifying Content of Interest
- Identifying Vulnerabilities

### IP Addresses and Sub-domains
- IP Registries:
  - IANA IPv4    # https://www.iana.org/assignments/ipv4-address-space/ipv4-address-space.xhtml
  - IANA IPv6    # https://www.iana.org/assignments/ipv6-unicast-address-assignments/ipv6-unicast-address-assignments.xhtml

### IP Addresses and Sub-domains
- DNS Lookups:
  - arin.net                  # https://search.arin.net/rdap/
  - whois.domaintools.com     # http://whois.domaintools.com/
  - viewdns.info              # http://viewdns.info/
  - dnsdumpster.com           # https://dnsdumpster.com/
  - centralops.net            # https://centralops.net/co/


### IP Addresses and Sub-domains
- URL Scan:
  - sitereport.netcraft.com      # https://sitereport.netcraft.com/
  - web-check.xyz                # https://web-check.xyz/
  - web-check.as93.net           # https://web-check.as93.net/
  - urlscan.io                   # https://urlscan.io/


### IP Addresses and Sub-domains
- IP GeoLocation lookup:
  - maxmind.com            # https://www.maxmind.com/en/locate-my-ip-address/
  - iplocation.io          # https://iplocation.io/
  - iplocation.net         # https://www.iplocation.net/ip-lookup/
  - infosniper.net         # https://infosniper.net/

### IP Addresses and Sub-domains
- BGP prefixes:
  - bgpview.io          # https://bgpview.io/
  - hackertarget.com    # https://hackertarget.com/as-ip-lookup/
  - bgp.he.net          # https://bgp.he.net/
  - bgp4.as             # https://www.bgp4.as/tools/

### Identifying External/3rd Party sites
- Parent/Subordinate organizations
- Clients/Customers
- Service organizations
- Partners

### Identifying People
- Target website
- Crawler tools like Maltego or Creepy
  - Maltego                                # https://www.maltego.com/
  - Creepy                                 # https://www.geocreepy.com/
- Search engines                           # https://en.wikipedia.org/wiki/List_of_search_engines
- Social Media                             # https://en.wikipedia.org/wiki/List_of_social_networking_services
- Job Portals                              # https://en.wikipedia.org/wiki/List_of_employment_websites
- Tracking active emails
- Family Tree

### Identifying Technologies
- File extensions      # https://en.wikipedia.org/wiki/List_of_filename_extensions
- Server responses     # https://websiteguidelines.com/guides/different-types-of-web-servers/
- Job listing          # 
- Website content      # https://dorik.com/blog/how-to-tell-what-website-builder-was-used
- Google Hacking       # https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06
- Shodan.io            # https://www.shodan.io/
- MAC OUI Lookup       # https://macaddress.io/

### Identifying Content of Interest
- /etc/passwd and /etc/shadow or SAM database
- Configuration files
- Log files
- Backup files
- Test pages
- Client-side code

### Identifying Vulnerabilities
- Known Technologies
- Error messages responses
- Identify running services
- Identify running OS
- Monitor running Applications

### Dig vs Whois
- Whois - queries DNS registrar over TCP port 43
  - Information about the owner who registered the domain
- Dig - queries DNS server over UDP port 53
  - Name to IP records

### Whois
```
whois zonetransfer.me
```

### Dig
```
dig zonetransfer.me A
dig zonetransfer.me AAAA
dig zonetransfer.me MX
dig zonetransfer.me TXT
dig zonetransfer.me NS
dig zonetransfer.me SOA
```

### Zone Transfer
- Between Primary and Secondary DNS over TCP port 53
- https://digi.ninja/projects/zonetransferme.php
```
dir axfr {@soa.server} {target-site}
dig axfr @nsztm1.digi.ninja zonetransfer.me
```

### Netcraft
- Similar to whois but web-based
- https://sitereport.netcraft.com/


### Historical Content
- Wayback Machine
- http://archive.org/web/

### Google Searches
- Advanced searches.   # 
- List of filters      # https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06
- Dork Search          # https://dorksearch.com/
```
site:*.ccboe.net
site:*.ccboe.net "administrator"
```

### Shodan
- Shodan: A search engine for Internet-connected devices
- https://www.shodan.io         
- Be aware of attribution

### Passive OS Fingerprinter (p0f)
- p0f: Passive scanning of network traffic and packet captures.
```
more /etc/p0f/p0f.fp
sudo p0f -i eth0
sudo p0f -r test.pcap
```

### Passive OS Fingerprinter (p0f)
- Examine packets sent to/from target
- Can guess Operating Systems and version
- Can guess client/server application and version

### Social Tactics
- Social Engineering (Hack a person)
- Technical based (Email/SMS/Bluetooth)
- Other Types (Dumpster Diving/Shoulder Surf)

## Describe Methods Used for Active External Discovery
https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_describe_methods_used_for_active_external_discovery
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/recon2.png)


### Scanning Nature
- Active
- Passive

### Scanning Strategy
- Remote to Local
- Local to Remote
- Local to Local
- Remote to Remote

### Scanning Approach
- Aim
  - Wide range target scan
  - Target specific scan
- Method
  - Single source scan
    - 1-to-1 or 1-to-many
  - Distributed scan
    - many-to-one or many-to-many

### Vertical Scan
- Scan some (or all ports) on a single target
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/07_discovery/assets/images/verticalscan.png)


### Horizontal Scan
- Scan a single (or set) port(s) on a range of targets.
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/07_discovery/assets/images/horizontalscan1.png)


### Strobe Scan
- Scan a predefined subset of ports on a range of targets.
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/07_discovery/assets/images/horizontalscan2.png)

### Block Scan
- Scan all (or a range) ports on a range of targets.
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/07_discovery/assets/images/horizontalscan3.png)


### Distributed Scan - Block
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/07_discovery/assets/images/distributedscan1.png)


### Distributed Scan - Strobe
![](https://git.cybbh.space/net/public/-/raw/master/networking/modules/07_discovery/assets/images/distributedscan2.png)


### Ping
- Ping one IP:
  - ping 172.16.82.106 -c 1
- Ping a range:
  - for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done


### NMAP Defaults
- Default Scan:
  - User: TCP Full Connect Scan (-sT)
  - Root: TCP SYN Scan (-sS)
- Default Ports scanned: 1000 most commonly used TCP or UDP ports

### NMAP Port States
- open
- closed
- filtered
- unfiltered
- open|filtered
- closed|filtered


### NMAP Options List
- NMAP Options List      # https://nmap.org/book/man-briefoptions.html
> https://nmap.org/book/man-port-scanning-techniques.html

### NMAP Scan Types
- Broadcast Ping/Ping sweep (-sP, -PE)
- SYN scan (-sS)             # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_1_syn_scan
- Full connect scan (-sT)    # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_2_full_connect_scan
- Null scan (-sN)            # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_3_null_scan
- FIN scan (-sF)             # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_4_fin_scan
- XMAS tree scan (-sX)       # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_5_xmas_tree_scan
- UDP scan (-sU)             # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_6_udp_scan
- Idle scan (-sI)            # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_7_idle_scan


### NMAP Scan Types
- Decoy scan (-D)                # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_8_decoy_scan
- ACK/Window scan (-sA)          # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_9_window_scan
- RPC scan (-sR)                 # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_10_rpc_scan
- FTP scan (-b)                  # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_11_ftp_bounce_scan
- OS fingerprinting scan (-O)    # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_12_os_fingerprinting_scan
- Version scan (-sV)             # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_13_version_scan
- Discovery probes               # https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_2_3_3_15_icmp_echo_discovery_probe


### NMAP - Other options
- -PE - ICMP Ping
- -Pn - No Ping


### NMAP - Time-Out
- -T0 - Paranoid - 300 Sec
- -T1 - Sneaky - 15 Sec
- -T2 - Polite - 1 Sec
- -T3 - Normal - 1 Sec
- -T4 - Aggresive - 500 ms
- -T5 - Insane - 250 ms


### NMAP - Delay
- --scan-delay <time> - Minimum delay between probes
- --max-scan-delay <time> - Max delay between probes


### NMAP - Rate Limit
- --min-rate <number> - Minimum packets per second
- --max-rate <number> - Max packets per second


### Traceroute - Firewalking
```
traceroute 172.16.82.106
traceroute 172.16.82.106 -p 123
sudo traceroute 172.16.82.106 -I
sudo traceroute 172.16.82.106 -T
sudo traceroute 172.16.82.106 -T -p 443
```


### Netcat - Scanning
```
nc [Options] [Target IP] [Target Port(s)]
```
- -z : Port scanning mode i.e. zero I/O mode
- -v : Be verbose [use twice -vv to be more verbose]
- -n : do not resolve ip addresses
- -w1 : Set time out value to 1
- -u : To switch to UDP


### Netcat - Horizontal Scanning
- Range of IPs for specific ports
- TCP
```
for i in {1..254}; do nc -nvzw1 172.16.82.$i 20-23 80 2>&1 & done | grep -E 'succ|open'
```
- UDP
```
for i in {1..254}; do nc -nuvzw1 172.16.82.$i 1000-2000 2>&1 & done | grep -E 'succ|open'
```

### Netcat - Vertical Scanning
- Range of ports on specific IP
- TCP
```
nc -nzvw1 172.16.82.106 21-23 80 2>&1 | grep -E 'succ|open'
```
- UDP
```
nc -nuzvw1 172.16.82.106 1000-2000 2>&1 | grep -E 'succ|open'
```


### Netcat - TCP Scan Script
```
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done
```


### Netcat - UDP Scan Script
```
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nuvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done
```

### Netcat - Banner Grabbing
- Find what is running on a particular port
```
nc [Target IP] [Target Port]
nc 172.16.82.106 22
nc -u 172.16.82.106 53
```
- -u : To switch to UDP


### Curl and Wget
- Both can be used to interact with the HTTP, HTTPS and FTP protocols.
- Curl - Displays ASCII
```
curl http://172.16.82.106
curl ftp://172.16.82.106
```
- Wget - Downloads (-r recursive)
```
wget -r http://172.16.82.106
wget -r ftp://172.16.82.106
```

## Describe Methods Used for Passive Internal Discovery
https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_3_describe_methods_used_for_passive_internal_network_reconnaissance
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/recon3.png)

### Packet Sniffers
- Wireshark
- Tcpdump
- p0f
> Limited to traffic in same local area of the network

### IP Configuration
```
Windows: ipconfig /all
Linux: ip address (ifconfig depreciated)
VyOS: show interface
```

### DNS configuration
```
Windows: ipconfig /displaydns
Linux: cat /etc/resolv.conf
```


### ARP Cache
```
Windows: arp -a
Linux: ip neighbor (arp -a depreciated)
```


### Network connections
```
Windows: netstat
Linux: ss (netstat depreciated)

Example options useful for both netstat and ss: -antp
a = Displays all active connections and ports.
n = No determination of protocol names. Shows 22 not SSH.
t = Display only TCP connections.
u = Display only UDP connections.
p = Shows which processes are using which sockets.
```

### Services File
```
Windows: %SystemRoot%\system32\drivers\etc\services
Linux/Unix: /etc/services
```
### OS Information
```
Windows: systeminfo
Linux: uname -a and /etc/os-release
```

### Running Processes
```
Windows: tasklist
Linux: ps or top

Example options useful for ps: -elf
e = Show all running processes
l = Show long format view
f = Show full format listing
```

### Command path
```
which
whereis
```

### Routing Table
```
Windows: route print
Linux: ip route (netstat -r deprecated)
VyOS: show ip route
```

### File search
```
find / -name hint* 2> /dev/null
find / -iname flag* 2> /dev/null
```
### SSH Config
```
Windows: C:\Windows\System32\OpenSSH\sshd_config
Linux: /etc/ssh/sshd_config
```


## Describe Methods Used for Active Internal Discovery
https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_4_describe_methods_used_for_active_internal_network_reconnaissance
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/recon4.png)

### Active Internal Network Reconnaissance
- Will use similar tools as Active External Network Reconnaissance
- Scope and addresses may differ

### ARP Scanning
```
arp-scan --interface=eth0 --localnet
nmap -sP -PR 172.16.82.96/27
```

### Ping Scanning
```
ping -c 1 172.16.82.106
for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
sudo nmap -sP 172.16.82.96/27
```

### DEV TCP Banner Grab
```
exec 3<>/dev/tcp/172.16.82.106/22; echo -e "" >&3; cat <&3
```

### DEV TCP Scanning
```
for p in {1..1023}; do(echo >/dev/tcp/172.16.82.106/$p) >/dev/null 2>&1 && echo "$p open"; done
```


## Perform Network Forensics
https://net.cybbh.io/public/networking/latest/07_discovery/fg.html#_7_5_perform_network_forensics


### Network Forensics - Mapping
- Diagram devices
- Line Types
- Written Information
- Coloring
- Groupings

### Network Forensics - Mapping
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/offensivefinishednetwork.png)



### Network Forensics - Mapping
- Device type (Router/host)
- System Host-names
- Interface names (eth0, eth1, etc)
- IP address and CIDRs for all interfaces
- TCP and UDP ports
- MAC Address
- OS type/version
- Known credentials


### Network Mapping Tools
- Draw.io Local (Template)           # https://1drv.ms/u/s!Arz6vf8sVG8vgpMsQ1RRtb0rcP7x4w?e=R9tlao
- Draw.io Web                        # https://app.diagrams.net/
- Witeboard.com                      # https://witeboard.com/
- Draw.Chat                          # https://draw.chat/
- SmartDraw                          # https://cloud.smartdraw.com/
- Ziteboard                          # https://app.ziteboard.com/
- Tutorialspoint Whiteboard          # https://www.tutorialspoint.com/whiteboard.htm
- Explain Everything Whiteboard      # https://whiteboard.explaineverything.com/































