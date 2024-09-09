# Commands


# Before you flush you should change the default policy.
# when you change the defualt policy it should be changed to accept.



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

## Configure iptables nat rules
https://net.cybbh.io/public/networking/latest/11_acl/fg.html#_11_2_4_configure_iptables_nat_rules

### NAT & PAT operators & Chains

### Source NAT
```iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.1 -j SNAT --to 1.1.1.1```

### Source NAT
```iptables -t nat -A POSTROUTING -p tcp -o eth0 -s 192.168.0.1 -j SNAT --to 1.1.1.1:9001```
### Source NAT
```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE```
### Destination NAT
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
























