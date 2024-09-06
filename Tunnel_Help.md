# SOS tunnel Hellp

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
  - <USER> # The user you want to tunnel back to and open a port on. You usually will need to come back to get ssh through a firewall.
  - <IP-TO-AUTH> # The IP on the other side of the firewall that you are authenticating as.
  - <PORT-TO-AUTH> # The Port on the internal box/system that you are trying to open a port on.
  - <PORT-TO-OPEN> # The port you want to open on the internal box/system that will let you bridge over the firewall.
  - <IP-TO-TARGET> # The target you want to connect to the port you opened on the IP you authenticated as. This is often loopback because you want to connect the port you opened to SSH on the box/system past the firewall.
  - <PORT-TO-TARGET> # The target port you want to connect your port you opened to. This is usually the port that is set to SSH on the internal box/system that you are connecting to beyond the firewall.
  ### Example
- ssh net2_student4@172.17.17.17 -p 1234 -R 20489:127.0.0.1:4321 -NT
  - ssh net2_student4@172.17.17.17 -p 1234 # The internal ip that you are authenticating to with the SSH port of that box/system
  - -R 20489 # The port that you want to open on 
  
### tunnel to bridge a remote port to your system
> When you build a tunnel back to yourself, you need to line the pipes up to complete the SSH bridge past the firewall.
- ssh <USER>@<IP-TO-AUTH> -p <PORT-TO-AUTH> -L <PORT-TO-OPEN>:<IP-TO-TARGET>:<PORT-TO-TARGET> -NT
  - <USER> # user credentials for the box that is just before the firewall you sent your -R (remote/reverse) tunnel back through.
  - <IP-TO-AUTH> # The IP of the box/system that you opened the port on with the remote tunnel. This might also be loopback if you have a tunnel already there.
  - <PORT-TO-AUTH> # Whatever port will get you to the internal box you are trying to get to.
  - <PORT-TO-OPEN> # This is going to be the port you want to open on your box that will connect you past the firewall. This will connect the pipes between your newly opened port and the box beyond the firewall.
  - <IP-TO-TARGET> # This is the IP of the 
  - <PORT-TO-TARGET> # 
### example
- ssh net2_student4@10.50.38.13 -p 1234 -L 20422:127.0.0.1:20489 -NT
- 
- 


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






























