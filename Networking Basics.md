<p align="center">
  <img src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/cyberspace.gif">
</p>

---

# Table of Contents

---
- [Commands and Utilities](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#commands-and-utilities)
  - [NETCAT](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#netcat)
  - [IP](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#ip)
  - [NETSTAT](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#netstat)
  - [TRACEROUTE](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#traceroute)  
- [Theory](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#theory)
  - [IP and Subnetting](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#ip-and-subnetting)
  - [Network Sockets](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#network-sockets)
  - [DMZ](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#dmz)
  - [SSL](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#ssl)
  - [OpenSSL](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#openssl)
  - [ARP](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#arp)
    - [ARP Spoofing & ARP DOS](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#arp-spoofing--arp-dos)
  - [OSI Model](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#osi)
---
# Commands and Utilities
---

## NETCAT

**Universal utility for network connection in Unix and similar operating systems**

---

|Command|Explanation|
|-|-|
|`nc host port`|Connects to the host on the specified port|
|`nc -l -p port`|Starts nc in listener mode on the specified port|
|`nc -z host {port-range}`|Basic port scanner|
|`nc -v host port`|Get banner|
|`nc -l -p local_port -c 'nc remote_host remote_port'`|Configures a basic proxy where it listens for a specific local port and forwards it to a remote server|
|`nc -l -p 1234 -e /bin/bash`|Simple backdoor|

---


## IP

**Linux command to manage ІР. Older brother of ifconfig**

---

|Command|Explanation|
|-|-|
|`ip addr`|Shows all addresses|
|`ip -4 addr`|Shows IPv4 address|
|`ip -6 addr`|Shows IPv6 address|

---

## NETSTAT

**The netstat command lets you discover which sockets are connected and which sockets are listening. Meaning, it tells you which ports are in use and which processes are using them. It can show you routing tables and statistics about your network interfaces and multicast connections.This command is liable to produce a long listing, so we pipe it into less.**

---

|Syntax|Explanation|
|-|-|
|`netstat -at \| less` | Looks for all tcp sockets|
|`netstat -au \| less`| Looks for all udp sockets|
|`netstat -l \| less `| Looks for all listening sockets. We could combine with -t to make netstat -lt or -lu to search for listening tcp or udp sockets |
|`netstat -p -at `| Shows all TCP sockets with PID|
|`sudo netstat -anp \| grep ":22" `| Finds 22 port target string|
|`sudo netstat -i `|Show network interfaces |
|`sudo netstat -r`|Display kernel routing table|

---
## TRACEROUTE

**For understanding traceroute you should know what is TCP/IP suite of protocols, especially what is UDP or User Datagram Protocol. There are a lot of headers but we need TTL (Time to Live). It is a count how much routers, gateways could possibly pass this packet, each router decrements 1. When TTL reaches 0, router sends ICMP "Time Exceeded" message back to the origin of the packet. So traceroute first sends packet with ttl 1, then 2, then 3 etc. until destination is reached or maximum number of hops (30 by default) is tested.**

|Syntax|Explanation|
|-|-|
|`traceroute -l IP`|Use ICMP Echo requests instead of UDP packets|
|`traceroute -n IP`|Do not resolve hostnames|
|`traceroute -q IP`|Set the number of queries per hop|
|`traceroute -m IP`|Set the maximum hop count|



---
# Theory 
---

## IP and Subnetting

**IP or Internet Protocol is Network OSI layers protocol, which is used for identifying devices in the Internet. For this it uses IP addresses. But there are billions of devices, so to communicate fast and easy with each of it, IP connects firstly not to devices itself, but to subnet, in which this device is located. This is called `Scaling`. Also IP address is 32 bit number, where every 8 bit is called `octet`**

---

**`Subnet` - is the set of computers, which older part of IP address is same:**
- 312.245.10.1 
- 312.245.10.2 
- 312.245.10.3 
Routers works with subnets, not just with certain computers.
---
### Subnet Mask
**`Subnet mask` is 32-bit number, which shows us, where in IP address number of network, and where is host. Previously, `Subnet Classes` were used to classify subnets, but this scheme is outdated, so they started using `CIDR`, which means `Classless Inter-Domain Routing`**

Mask structure:
- **1** in position, specifying net number
- **0** in position, specifying host number

|Explanation|Number|
|-|-|
|`IP(Decimal):`| 213.180.193.3|
|`IP:`| 11010101.10110100.11000001.00000011|
|`Mask:`| 11111111.11111111.11111111.00000000|
|`Subnet:`| 11010101.10110100.11000001.00000000|

---

Subnet mask could be shown with 2 types: decimal and prefix
- **Decimal**: 255.255.255.0
- **Prefix**: /24. Prefix 24 means 24 bits of subnet address in IP address.

**The subnet mask does not have to end on an octet boundary**

|Explanation|Number|
|-|-|
|`IP(Decimal):`| 213.180.193.3 /20|
|`IP:`| 11010101.10110100.11000001.00000011|
|`Mask:`| 11111111.11111111.11110000.00000000|
|`Subnet:`| 11010101.10110100.11000000.00000000|
|`Subnet(Decimal):`| 213.180.192.0|
|`Host(Decimal):`| 0.0.1.3|

So algoritm is that you should replace all `one's` in IP with `zero's` in mask at the same position.

---

## Network Sockets

**A `socket` - is one endpoint of a two way communication link between two programs running on the network. Sockets have two main states: They are either connected and facilitating an ongoing network communication, or they are waiting for an incoming connection to connect to them. The listening socket is called the server, and the socket that requests a connection with the listening socket is called a client. You could use [netstat](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Networking%20Basics.md#netstat) command to manage and discover your own sockets, for what and where are they used. The "Active Internet" section lists the network connections that are (or will be) established to external devices. The "UNIX domain" section lists  the connections that have been established within your computer between different applications, processes, and elements of the operating system.**

---
**TCP Socket States**
|Socket State|Explanation|
|-|-|
|`LISTEN`|Servers-side. Socket waiting for a connection request |
|`SYN-SENT`|Client-side. Socket has made a connection request and wait. |
|`SYN-RECEIVED`|Server-side. Socket is waiting for a connection ack after accepting request |
|`ESTABLISHED`| Server and Client. A working connection has been established between the server and the client, allowing for data transfer|
|`FIN-WAIT-1`|Server and Client. Socket is waiting for a termination request or for ack of previous termination request |
|`FIN-WAIT-2`|Server and Client. Socket is waiting for a termination request |
|`CLOSE-WAIT`|Socket is waiting for a termination request ack from local user |
|`CLOSING`|Server and Client. Socket is waiting for a termination request ack from remote socket|
|`LAST-ACK`|Server and Client. Socket is waiting ack of termination from remote socket|
|`TIME-WAIT`| Server and Client. Server and Client. Checking if termination ack was received |
|`CLOSED`|No connection, socket is terminated |

---

## DMZ

**`DMZ`, or Demilitarized Zone, in the context of computer networks, is a segregated area that acts as a buffer between a trusted internal network and an untrusted external network, such as the internet. It typically contains servers that need to be accessible from the internet. like web servers or email servers. The `DMZ` helps enhance security by isolation these servers from the internal network, by reducing the risk of unauthorized access to sensitive information.**



## SSL

**`SSL`, or Secure Sockets Layer, is an encryption-based Internet security protocol. It was first developed by Netscape in 1995 for the purpose of ensuring privacy, authentication, and data integrity in Internet communications. SSL is the predecessor to the modern TLS encryption used today.**

---

### What is an `SSL` certificate?

`SSL` can only be implemented by websites that have an SSL certificate (technically a "TLS certificate"). An `SSL` certificate is like an ID card or a badge that proves someone is who they say they are. `SSL` certificates are stored and displayed on the Web by a website's or application's server.

One of the most important pieces of information in an `SSL` certificate is the website's public key. The public key makes encryption and authentication possible. A user's device views the public key and uses it to establish secure encryption keys with the web server. Meanwhile the web server also has a private key that is kept secret; the private key decrypts data encrypted with the public key.

---
 
### What are the types of SSL certificates?

There are several different types of SSL certificates. One certificate can apply to a single website or several websites, depending on the type:

---

  - 'Single-domain': A single-domain `SSL` certificate applies to only one domain (a "domain" is the name of a website, like www.cloudflare.com).

--- 

  - 'Wildcard': Like a single-domain certificate, a wildcard SSL certificate applies to only one domain. However, it also includes that domain's subdomains. For example, a wildcard certificate could cover www.cloudflare.com, blog.cloudflare.com, and developers.cloudflare.com, while a single-domain certificate could only cover the first.

---

  - 'Multi-domain': As the name indicates, multi-domain SSL certificates can apply to multiple unrelated domains.

---

## SMB

**`SMB` or `Server Message Block` is a network protocol used for file and printer sharing in a local area network (LAN). It allows computers to share files, printers, and other resources. SMB is often used in Windows-based environments, and it enables users to access files and resources on other computers within the same network.**

---

### Smb Enumeration

**There are a good topic about this in [GeeksForGeeks](https://www.geeksforgeeks.org/smb-enumeration/) and in [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb#smb)** 

---

List SMB shares:

```smbclient -L <target IP>```

---

## OpenSSL

**`OpenSSL` is a widely-used open-source toolkit for implementing the `SSL (Secure Sockets Layer)` and `TLS (Transport Layer Security)` protocols. It provides a set of cryptographic functions and utilities that enable secure communication over a computer network. `OpenSSL` is commonly used for creating and managing `SSL/TLS` certificates, generating cryptographic keys, and performing various cryptographic operations.**

---

**Here are some basic and common OpenSSL commands on Linux:**

1. Check OpenSSL Version:
```
openssl version
```
   

2. Generate a Private Key:
```
openssl genprsa -out private-key.pem 2048
```
   

3. Generate a Public Key from a Private Key:
```
openssl rsa -in private-key.pem -pubout -out public-key.pem
```
   

4. Generate a Self-Signed Certificate:
  ```
openssl req -x509 -newkey rsa:2048 -keyout private_key.pem -out certificate.pem -days 365
```

5. View Certificate Information:
  ```
openssl x509 -in certificate.pem -text -noout
```
   

6. Encrypt/Decrypt a File using RSA:
   - Encrypt:
     ```
     openssl rsautl -encrypt -inkey public_key.pem -pubin -in plaintext.txt -out encrypted_data.bin
     ```
   - Decrypt:
     ```
     openssl rsautl -decrypt -inkey private_key.pem -in encrypted_data.bin -out decrypted_data.txt
     ```
   
7. Hashing:
   - Generate MD5 hash:
      ```
     openssl md5 file.txt
      ```
   - Generate SHA-256 hash:
      ```
     openssl sha256 file.txt
      ```


---

## ARP

**The acronym `ARP` stands for `Address Resolution Protocol` which is one of the most important protocols of the Data link layer in the `OSI` model. It is responsible to find the hardware address of a host from a known `IP` address. So as I get we use ARP when we need to send some info on 2 level of `OSI`, which requires `MAC` address. Every machine has it's own `ARP` cache, where is table like IP-MAC data. So when we need to send some data on `Data Link` level, we broadcast request to entire network like "Hey, who is 10.10.10.10, I want to find his MAC". And if we found it address, it will tell us back with "Hi, you looking for 10.10.10.10? It's me, here's my MAC".**

### ARP Spoofing & ARP DOS

#### Bettercap
**Bettercap is a powerful, modular, and flexible open-source tool designed for network penetration testing. It is primarily used for network discovery, man-in-the-middle attacks, and other security assessments. Bettercap is written in Go and comes with a variety of features that make it a valuable tool for security professionals and ethical hackers. Here are some key aspects that make Bettercap useful:**

---


**Example**


*Ban the address 192.168.1.6 from the network:*

```linux
> set arp.spoof.targets 192.168.1.6; arp.ban on
```

*Spoof 192.168.1.2, 192.168.1.3 and 192.168.1.4:*

```linux
> set arp.spoof.targets 192.168.1.2-4; arp.spoof on
```
**After spoofing or poisoning we could look or change traffic with wireshark**

---

## OSI model

**The `OSI` (Open Systems Interconnection) model is a conceptual framework that standardizes the functions of a telecommunications or networking system into seven distinct layers:**

---
1. `Physical Layer`: This layer deals with the physical medium and hardware aspects of data transmission, such as cables, switches, and electrical signals.

2. `Data Link Layer`: Responsible for the reliable transmission of data over a physical medium, it handles tasks like addressing, error detection, and framing.

3. `Network Layer`: Focuses on routing and forwarding data packets between different networks, often using logical addressing (like IP addresses).

4. `Transport Layer`: Ensures end-to-end data transfer reliability and provides services like flow control, error detection and correction, and data segmentation.

5. `Session Layer`: Manages the establishment, maintenance, and termination of communication sessions between devices, allowing for synchronization and organization of data exchange.

6. `Presentation Layer`: Responsible for data translation, encryption, and compression, making sure data is in a format that can be understood by both sender and receiver.

7. `Application Layer`: This is the topmost layer that interacts with end-user applications and provides network services like email, web browsing, and file transfer.
---
*But I think in this topic pictures are better explainers:*
<p align="center">
  <img width="788" height="584" src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/OSI1.png">
</p>

<p align="center">
  <img width="788" height="504" src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/OSI2.png">
</p>

---
