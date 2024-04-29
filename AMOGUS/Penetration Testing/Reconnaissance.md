# Reconnaissance
---
### Our goal is not to get at the systems but to find all the ways to get there. 
---
**To do proper reconnnaissance we should use three principles:**
1. There is more than meets the eye. Consider all points of view.
2. Distinguish between what we see and what we do not see.
3. There are always ways to gain more information. Understand the target.
### Methodology
This methodology of footprinting is nested in 6 layers and represents, metaphorically speaking, boundaries that we try to pass with the enumeration process. The whole enumeration process is divided into three different levels:
- Infrastructure-based enumeration
- Host-based enumeration
- OS-based enumeration
![image info](./images/pentesting-image-1.png)
So basically our hacking process should look like this (squares is our gaps in security):
![image info](./images/pentesting-image-2.png)
Let's look more about our goals in each layer of this labyrinth:

- Layer No.1: **Internet Presence**
`The goal of this layer is to identify all possible target systems and interfaces that can be tested. `

- Layer No.2: **Gateway**
`The goal is to understand what we are dealing with and what we have to watch out for.`

- Layer No.3: **Accessible Services**
`This layer aims to understand the reason and functionality of the target system and gain the necessary knowledge to communicate with it and exploit it for our purposes effectively.`

- Layer No.4: **Processes**
`The goal here is to understand these factors and identify the dependencies between them.`

- Layer No.5: **Privileges**
`It is crucial to identify these and understand what is and is not possible with these privileges.`

- Layer No.6: **OS Setup**
`The goal here is to see how the administrators manage the systems and what sensitive internal information we can glean from them.`

## Domain Information
The first point of presence on the Internet may be the SSL certificate from the company's main website that we can examine. Often, such a certificate includes more than just a subdomain, and this means that the certificate is used for several domains, and these are most likely still active. You could look for subdomains and certificates in [crt.sh](https://crt.sh/) website, or try to use command:

```bash
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```

Also we could use shodan, but for this we need to pay some money for subscription or API usage, so we'll miss that part.
The other part we could gather info about is DNS Records by using as example 

```bash
dig any inlanefreight.com
```
## Nmap

<!-- Cheetsheet from HTB Academy  -->

| Option | Description |
| ------ | ----------- |
| 10.10.10.0/24 | Target network range. |
| -sn | Disables port scanning. |
| -Pn | Disables ICMP Echo Requests. |
| -n | Disables DNS Resolution. |
| -PE | Performs the ping scan using ICMP Echo Requests against the target. |
| --packet-trace | Shows all packets sent and received. |
| --reason | Displays the reason for a specific result. |
| --disable-arp-ping | Disables ARP Ping Requests. |
| --top-ports=\<num> | Scans the specified top ports defined as most frequent. |
| -p- | Scan all ports. |
| -p22-110 | Scan all ports between 22 and 110. |
| -p22,25 | Scans only the specified ports 22 and 25. |
| -F | Scans top 100 ports. |
| -sS | Performs a TCP SYN-Scan. |
| -sA | Performs a TCP ACK-Scan. |
| -sU | Performs a UDP Scan. |
| -sV | Scans the discovered services for their versions. |
| -sC | Perform a Script Scan with scripts categorized as "default". |
| --script=\<script> | Performs a Script Scan using the specified scripts. |
| -O | Performs an OS Detection Scan to determine the OS of the target. |
| -A | Performs OS Detection, Service Detection, and traceroute scans. |
| -D RND:5 | Sets the number of random Decoys used to scan the target. |
| -e | Specifies the network interface used for the scan. |
| -S 10.10.10.200 | Specifies the source IP address for the scan. |
| -g | Specifies the source port for the scan. |
| --dns-server \<ns> | DNS resolution is performed using a specified name server. |

### Output Options

| Option | Description |
| ------ | ----------- |
| -oA filename | Stores the results in all available formats starting with the name "filename". |
| -oN filename | Stores the results in normal format with the name "filename". |
| -oG filename | Stores the results in "grepable" format with the name "filename". |
| -oX filename | Stores the results in XML format with the name "filename". |

### Performance Options

| Option | Description |
| ------ | ----------- |
| --max-retries \<num> | Sets the number of retries for scans of specific ports. |
| --stats-every=5s | Displays the scan's status every 5 seconds. |
| -v/-vv | Displays verbose output during the scan. |
| --initial-rtt-timeout 50ms | Sets the specified time value as the initial RTT timeout. |
| --max-rtt-timeout 100ms | Sets the specified time value as the maximum RTT timeout. |
| --min-rate 300 | Sets the number of packets that will be sent simultaneously. |
| -T <0-5> | Specifies the specific timing template. |

## Subdomain and Directory Enum
- **Gobuster DNS**
```bash
gobuster dns -d superkek.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -t 20
```
- **Gobuster VHOST**
```bash
gobuster vhost -u superkek.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
- **Dirsearch**
```bash
dirsearch -u superkek.com
```
- **Ffuf Subdomain**
```bash
ffuf -w wordlist.txt:FUZZ -u https://FUZZ.superkek.com/`
```
- **Ffuf VHost**
```bash
ffuf -w wordlist.txt:FUZZ -u http://superkek.com:PORT/ -H 'Host: FUZZ.superkek.com' -fs xxx
```

## Fuzzing
### Ffuf
| **Command**   | **Description**   |
| --------------|-------------------|
| `ffuf -h` | ffuf help |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ` | Directory Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ` | Extension Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php` | Page Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v` | Recursive Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u https://FUZZ.hackthebox.eu/` | Sub-domain Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb' -fs xxx` | VHost Fuzzing |
| `ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx` | Parameter Fuzzing - GET |
| `ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx` | Parameter Fuzzing - POST |
| `ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx` | Value Fuzzing |  

### Wordlists

| **Command**   | **Description**   |
| --------------|-------------------|
| `/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt` | Directory/Page Wordlist |
| `/opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt` | Extensions Wordlist |
| `/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` | Domain Wordlist |
| `/opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt` | Parameters Wordlist |

### Misc

| **Command**   | **Description**   |
| --------------|-------------------|
| `sudo sh -c 'echo "SERVER_IP  academy.htb" >> /etc/hosts'` | Add DNS entry |
| `for i in $(seq 1 1000); do echo $i >> ids.txt; done` | Create Sequence Wordlist |
| `curl http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded'` | curl w/ POST |

