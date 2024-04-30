---

# Useful Commands

---

**Generate public and private key pair (id_rsa and id_rsa.pub). If you want to add your ssh key to some shell, just copy-paste id_rsa.pub contents into ~/.ssh/authorized_keys file**

```
ssh-keygen -o
```
---

**[CeWL](https://www.geeksforgeeks.org/cewl-tool-creating-custom-wordlists-tool-in-kali-linux/) (pronounced "cool") is a custom word list generator tool that spiders websites to create word lists based on the site's content**
```
cewl -d 0 -m 5 -w usernames.txt http://MACHINE_IP/team.php --lowercase
```
---
**The `cut` command allows you to extract specific sections (columns) of lines from a file or input stream by "cutting" the line into columns based on a delimiter and selecting which columns to display**

```
--> cut -d ' ' -f1,3,6 access.log
[2023/10/25:15:42:02] sway.com:443 200
[2023/10/25:15:42:02] sway.com:443 301
```

---
**The [top](https://www.geeksforgeeks.org/top-command-in-linux-with-examples/) command shows you a list of processes in real time with their usage. It's a dynamic list, meaning it changes with the resource usage of each process.**

---

**Look for an installed software**

```magic
dpkg -l
```

**Base64 encode/decode**
```bash
base64 [encode]
base64 -d [decode]
```

**Grab banner**
```bash
nc -nv 10.129.2.28 25
sudo tcpdump -i eth0 host 10.10.14.2 and 10.129.2.28
```

**Make wordlist from website crawling**
```bash
cewl
```

**Use pspy64 script to monitor Linux processes**
```bash
./pspy64
```
---

