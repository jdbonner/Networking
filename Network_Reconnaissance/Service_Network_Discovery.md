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











