# Network prep

1	Tunnel Prep – What is localhost


2	Tunnel Prep – Alternate port 1
OPS$ ssh cctc@10.50.1.150 -p 1111

3	Tunnel Prep – Alternate port 2
OPS$ ssh cctc@localhost -p 1111


4	Tunnel Prep – Fill in the blank
SSH to PC1 from OPS
ssh cctc@10.50.1.150

5	Tunnel Prep – Dynamic
setup a Dynamic tunnel to PC1
ssh cctc@10.50.1.150 -D 9050 -NT

6	Tunnel Prep – Local to SSH
setup a Local tunnel to PC1 SSH port
ssh -L 1111:localhost:22 cctc@10.50.1.150 -NT

7	Tunnel Prep – Local to HTTP
setup a Local tunnel to PC1 HTTP port
ssh cctc@100.1.1.1 -L 1111:localhost:80 -NT

8	Tunnel Prep – Dynamic thru 1st Local
establish a Dynamic tunnel using the Local tunnel created
ssh -D 9050 cctc@localhost -p 1111 -NT

9	Tunnel Prep – Pull HTTP thru Local
download the webpage of PC1 using the Local tunnel created
wget -r http://localhost:1111


10	Tunnel Prep – Pull HTTP thru Dynamic
download the webpage of PC2 using the Dynamic tunnel created
proxychains wget -r http://100.1.1.2


11	Tunnel Prep – Local to 2nd Pivot SSH
setup a Local tunnel to PC2 SSH port using PC1 as your pivot
ssh cctc@10.50.1.150 -L 1111:100.1.1.2:22 -NT

12	Tunnel Prep – 2nd Local thru 1st Local SSH
setup a 2nd Local tunnel to PC2 SSH port using the tunnel made
ssh -L 2222:100.1.1.2:22 cctc@localhost -p 1111 -NT

13	Tunnel Prep – 2nd Local thru 1st Local HTTP
setup a 2nd Local tunnel to PC2 HTTP port using the tunnel made in Question 6 as your first tunnel
ssh cctc@localhost -p 1111 -L 2222:100.1.1.2:80 -NT

14	Tunnel Prep – Dynamic thru 2nd Local
establish a Dynamic tunnel using the Local tunnel created in Question 12
ssh -D 9050 cctc@localhost -p 2222 -NT

15	Tunnel Prep – What’s Wrong 1
Admin is trying to create a Dynamic tunnel to PC2.
1.) ssh cctc@10.50.1.150 -L 1234:100.1.1.2:22 -NT
2.) ssh -D 9050 cctc@100.1.1.2 -p 1234 -NT
authenticated to wrong IP in line 2

16	Tunnel Prep – What’s Wrong 2
Admin is trying to telnet through the tunnels to PC3
1.) ssh cctc@10.50.1.150 -L 1234:192.168.2.1:22 -NT
2.) ssh -L 4321:192.168.2.2:23 cctc@localhost -p 1234 -NT
3.) telnet localhost 4321
targeted wrong IP in line 1

17	Tunnel Prep – Local to 3rd Pivot TELNET
ssh syntax would properly setup a 3rd Local tunnel to PC3 TELNET port using the tunnels made in Question 6 and Question 12?
ssh -p 2222 cctc@localhost -L 3333:192.168.2.2:23 -NT

18	Tunnel Prep – Telnet to 3rd Pivot
telnet to PC3 using the tunnel make in Question 17
telnet localhost 3333

19	Tunnel Prep – Remote
setup a Remote tunnel from PC3 back to PC2 using PC3 SSH port as the target
ssh -R 4444:localhost:22 cctc@192.168.2.1 -NT


20	Tunnel Prep – Local to Remote
set up a Local tunnel to map to the tunnel made in Question 19 using the tunnel made in Question 6 and Question 12
ssh cctc@localhost -p 2222 -L 5555:localhost:4444 -NT
