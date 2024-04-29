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

