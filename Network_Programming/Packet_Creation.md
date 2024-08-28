# Packet Creation and Socket Programming
https://net.cybbh.io/public/networking/latest/12_programming/fg.html
```
OUTCOMES
Identify Socket Types for Network Functions

Discuss Network Programming with Python3

Demonstrate Stream Socket Programming

Demonstrate Datagram Socket Programming
OUTCOMES
Demonstrate RAW Socket with Python3

Demonstrate RAW TCP Socket with Python3
Rationale
Understanding TCP Stream, UDP Datagram, and RAW sockets is
vital for cyber security professionals due to their foundational
role in network communication protocols. TCP Stream enables
reliable, connection-oriented data transmission, UDP Datagram
facilitates lightweight, connectionless communication, and RAW
sockets provide low-level access to network interfaces. Mastery
of these concepts allows professionals to analyze network traffic
effectively, detect anomalies, and develop robust security measures
to safeguard against a wide range of cyber threats, enhancing the
overall resilience of organizational networks.

Assessment
You will be assessed via CTFd challenges where you will need to score 56/80 points to achieve a 70%.
```

## Socket Types
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_1_understanding_socket_types_for_network_functions
- Stream Sockets - Connection oriented and sequenced; methods for connection establishment and tear-down. Used with TCP, SCTP, and Bluetooth.
- Datagram Sockets - Connectionless; designed for quickly sending and receiving data. Used with UDP.
- RAW Sockets - Direct sending and receiving of IP packets without automatic protocol-specific formatting.

## User Space vs. Kernel Space Sockets
- User Space Sockets
  - Stream Sockets
  - Datagram Sockets
- Kernel Space Sockets
  - RAW Sockets


## Socket Creation and Privilege Level
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_2_differentiate_user_spacekernel_space_sockets
- User Space Sockets - The most common sockets that do not require elevated privileges to perform actions on behalf of user applications.
- Kernel Space Sockets - Attempts to access hardware directly on behalf of a user application to either prevent encapsulation/decapsulation or to create packets from scratch, which requires elevated privileges.

### User Space Applications/Sockets
- Using tcpdump or wireshark to read a file
- Using nmap with no switches
- Using netcat to connect to a listener
- Using netcat to create a listener above the well known port range (1024+)
- Using /dev/tcp or /dev/udp to transmit data

### Kernel Space Applications/Sockets
- Using tcpdump or wireshark to capture packets on the wire
- Using nmap for OS identification or to set specific flags when scanning
- Using netcat to create a listener in the well known port range (0 - 1023)

### Kernel Space Applications/Sockets
- Using Scapy to craft or modify a packet for transmission
- Using Python to craft or modify RAW Sockets for transmission
- Network devices using routing protocols such as OSPF
- Any Traffic without Transport Header (ICMP)

## Understanding Python Terminology
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_4_implement_network_programming_with_python3
- Libraries (Standard Python Library)      # https://docs.python.org/3/
  - Modules (_import module)                 # https://docs.python.org/3/py-modindex.html
    - Functions (module.function)
    - Exceptions (try:)
    - Constants (AF_INET)
    - Objects ()
    - List [] vs Tuple ()

### String vs Integer
- String
  - my_string = "Hello World"
- Number
  - int = 1234
  - float = 3.14
  - hex = 0x45

### Built-In Functions
- int()
- len()
- str()
- sum()
- print()

### Built-In Methods
- my_string.upper()
- my_string.lower()
- my_string.split()
- my_list.append()
- my_list.insert()

### How Imports Work
- import {module}
- import {module} as {name}
- from {module} import *
- from {module} import {function}
- from {module} import {function} as {name}


## Network Programming with Python3
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_4_4_understanding_socket_api_functions
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/tcp-socket.png)

### Network Programming with Python3
- Network sockets primarily use the Python3 Socket library and socket.socket function.
```
import socket
  s = socket.socket(socket.FAMILY, socket.TYPE, socket.PROTOCOL)
```

### The socket.socket Function
- Inside the socket.socket. function, you have these arguments, in order:
```
socket.socket( *family*, *type*, *proto* )
```
- family: AF_INET*, AF_INET6, AF_UNIX
- type: SOCK_STREAM*, SOCK_DGRAM, SOCK_RAW
- proto: 0*, IPPROTO_TCP, IPPROTO_UDP, IPPROTO_IP, IPPROTO_ICMP, IPPROTO_RAW

## Python3 Libraries and References
- Socket        # https://docs.python.org/3/library/socket.html
- Errors        # https://docs.python.org/3/tutorial/errors.html
- Struct        # https://docs.python.org/3/library/struct.html
- Exceptions    # https://docs.python.org/3/library/exceptions.html
- Sys           # https://docs.python.org/3/library/sys.html
  

## Stream and Dgram Socket Demos
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_5_demonstration_of_creating_stream_and_dgram_sockets

### Stream Socket Sender Demo
```
#!/usr/bin/python3
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
ip_addr = '127.0.0.1'
port = 1111
s.connect((ip_addr, port))
message = b"Message"
s.send(message)
data, conn = s.recvfrom(1024)
print(data.decode('utf-8'))
s.close()
```

### Stream Socket Receiver Demo
```
#!/usr/bin/python3
import socket
import os
port = 1111
message = b"Connected to TCP Server on port %i\n" % port
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind(('', port))
s.listen(1)
os.system("clear")
print ("Waiting for TCP connections\n")
while 1:
    conn, addr = s.accept()
    connect = conn.recv(1024)
    address, port = addr
    print ("Message Received - '%s'" % connect.decode())
    print ("Sent by -", address, "port -", port, "\n")
    conn.sendall(message)
    conn.close()
```

### Datagram Socket Sender Demo
```
#!/usr/bin/python3
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM, 0)
ip_addr = '127.0.0.1'
port = 2222
message = b"Message"
s.sendto(message, (ip_addr, port))
data, addr = s.recvfrom(1024)
print(data.decode())
```

### Datagram Socket Receiver Demo
```
#!/usr/bin/python3
import socket
import os
port = 2222
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM,0)
s.bind(('', port))
os.system("clear")
print ("Awaiting UDP Messages")
while True:
    data, addr = s.recvfrom(1024)
    address, port = addr
    print ("\nMessage Received: '%s'" % data.decode())
    print ("Sent by -", address, "port", port)
    s.sendto(b"Message received by the UDP Message Server!", addr)
```

## Raw IPV4 Sockets
- RAW Socket scripts must include the IP header and the next headers.
- Requires guidance from the "Request for Comments" (RFC) to follow header structure properly.
  - RFCs contain technical and organizational documents about the Internet, including specifications and policy documents.
- See RFC 791, Section 3 - Specification for details on how to construct an IPv4 header.

### Raw Socket Use Case
- Testing specific defense mechanisms - such as triggering and IDS for an effect, or filtering
- Avoiding defense mechanisms
- Obfuscating data during transfer
- Manually crafting a packet with the chosen data in header fields


## Encoding and Decoding
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_6_encoding_and_decoding
- Encoding
  - The process of taking bits and converting them using a specified cipher.
- Decoding
  - Reverse of the conversion process used by the specified cipher for encoding.
- Common encoding schemes
  - UTF-8, Base64, Hex

### Encoding vs Encryption
Encoding - converts data into a different format

Encryption - scrambles data to make it unreadable without a secret key


### Encoding and Decoding
![](https://git.cybbh.space/net/public/raw/master/modules/networking/slides-v4/images/Encoding.jpg)


### Hex Encoding and Decoding
- Encode text to Hex:
```
echo "Message" | xxd
```
- Encode file to Hex:
```
xxd file.txt file-encoded.txt
```
- Decode file from Hex:
```
xxd -r file-encoded.txt file-decoded.txt
```

### Python Hex Encoding
```
import binascii
```
```
message = b'Message'
hidden_msg = binascii.hexlify(message)
```

### Base64 Encoding and Decoding
- Encode text to base64:
```
echo "Message" | base64
```
- Endode file to Base64:
```
base64 file.txt > file-encoded.txt
```
- Decode file from Base64:
```
base64 -d file-encoded.txt > file-decoded.txt
```

### Python Base64 Encoding
```
import base64
```
```
message = b'Message'
hidden_msg = base64.b64encode(message)
```


## Raw IPV4 and TCP Socket Demos
https://net.cybbh.io/public/networking/latest/12_programming/fg.html#_12_7_demonstration_of_creating_raw_sockets
> Follow along with the instructor on the Internet Host
- ipraw.py shell    # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/ipraw.adoc
- tcpraw.py shell    # https://git.cybbh.space/net/public/-/raw/master/modules/networking/activities/resources/tcpraw.adoc








