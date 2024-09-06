# command sheet

### tunnel to device to send to a alternate port
- ssh <USER>@<IP-TO-AUTH> -p <PORT-TO-AUTH> -L <PORT-TO-OPEN>:<IP-TO-TARGET>:<PORT-TO-TARGET> -NT
  - <USER> # This is the username your going to authenticate to the system as.
  - <IP-TO-AUTH> # This is the ip your going to ssh to. It can be a Float, Loopback, or Internal IP.
  - <PORT-TO-AUTH> # This is the port SSH is enabled as on the box/system you are authenticating to.
  - <PORT-TO-OPEN> # This is the port you want to open on your local box/system.
  - <IP-TO-TARGET> # This is the IP or direction you want the tunnel to take you. 
  - <PORT-TO-TARGET> # This is the Port you want the tunnel to take you to on the target IP box/system.
  ### Example
- ssh net2_student4@10.50.38.13 -p 1234 -L 20421:172.17.17.28:23 -NT
  - ssh net2_student4@10.50.38.13 -p 1234 # I want to SSH as net2_student4 to the 10.50.38.13 box/system at port 1234.
  - -L 20421:172.17.17.28:23 -NT # The L for local means I want to open port 20421 on my box/system. The 20421 port on my box/system will take me to the 172.17.17.28 box/system at port 23. Which means I can only send telnet through 20421.

### tunnel to device and open remote port
- ssh <USER>@<IP-TO-AUTH> -p <PORT-TO-AUTH> -R <PORT-TO-OPEN>:<IP-TO-TARGET>:<PORT-TO-TARGET> -NT
  - <USER>
  - <IP-TO-AUTH>
  - <PORT-TO-AUTH>
  - <PORT-TO-OPEN>
  - <IP-TO-TARGET>
  - <PORT-TO-TARGET>### Example
ssh net2_student4@172.17.17.17 -p1234 -R 20489:127.0.0.1:4321 -NT


### tunnel to bridge a remote port to your system
- ssh <USER>@<IP-TO-AUTH> -p <PORT-TO-AUTH> -R <PORT-TO-OPEN>:<IP-TO-TARGET>:<PORT-TO-TARGET> -NT
  - <USER>
  - <IP-TO-AUTH>
  - <PORT-TO-AUTH>
  - <PORT-TO-OPEN>
  - <IP-TO-TARGET>
  - <PORT-TO-TARGET>
### example
ssh net2_student4@10.50.38.13 -p 1234 -L 20422:127.0.0.1:20489 -NT


### tunnel to step through tunnel to reach to next system
- ssh <USER>@<IP-TO-AUTH> -p <PORT-TO-AUTH> -R <PORT-TO-OPEN>:<IP-TO-TARGET>:<PORT-TO-TARGET> -NT
  - <USER>
  - <IP-TO-AUTH>
  - <PORT-TO-AUTH>
  - <PORT-TO-OPEN>
  - <IP-TO-TARGET>
  - <PORT-TO-TARGET>

### Example
ssh net2_student4@127.0.0.1 -p 20422 -L 20423:192.168.30.150:1212 -NT






























