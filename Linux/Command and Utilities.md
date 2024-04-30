---
---
# Commands and Utilities
---
---

## AWK

**Specified Programming Language, which we could use for easy scripts**

---

|Command | Explanation | 
|----------|-------------|
| `$1`  | First column, 
| `$0` | All columns | 
| `$NF`  | Last colums |
| `awk '{print $1}'`  | Output of the first column |
| `OFS="/"` | Change separator to / |
| `BEGIN {print "Kek"}` | Before the main command, display Kek |
| `-F:` | We show that the string uses a separator: : |
| `$3 >= 1000` | The value of the third column is less than more than 1000 |
| `/UUID/`  | Look for UUID pattern |
| `/^UUID/` | Look for pattern which begins with UUID |

---

## TEE

**Command for Redirecting Output in Linux**

| Command | Explanation |
|-|-|
|`command` | tee file` | Redirect output of command to file and display on the terminal |
|`command` | tee -a file | Append output of command to file and display on the terminal |
|`tee file1 file2` | Redirect output to multiple files simultaneously |
|`tee -a file1 file2` | Append output to multiple files simultaneously |
|`echo "Text" \| tee file ` | Display and save "Text" to file |
|`command1 \| tee > (command2)` | Pipe output of command1 to command2 and display on the terminal |
|`command \| tee /dev/tty` | Display output on the terminal, but not redirect to a file |



## SUDO

**Linux utility that provides the ability to execute commands with different levels of access, including root**

---

| Command | Explanation |
|-|-|
|`sudo -l` | Check privileges|
|`sudo -u` | Do smth on behalf of the user |
|`sudo su` | Change to root user |
|`sudo` | Do smth on behalf of root user|

---

## LESS

**If the file is very large, this utility does not allow you to clog up the entire term of the terminal, that is, it shortens the output and allows you to scroll up and down**

---

| Command | Explanation |
| ------|-------|
|`less -F` | Monitor changes in the file| 
|`less -X` |Leave what was in the file without deleting it after disabling the command|
|`less -N` | Number lines |

---
## TAIL

**Command used to output the contents of a file, usually at the end of that file**

---

| Command | Explanation |
| ------|-------|
|`tail -50` | Lines, need to be taken from the end|
|`tail +50` | Lines, need to be taken from the beginning|
|`tail -c` | Number of bytes to be removed from the end|
|`tail -F` | Look for changes in a file|

---

## WGET 

**Download files from sites**

---

|Command|Explanation|
|-|-|
|`wget IP`| Download the file from the site|
|`wget -O` | Download the file under a new name|
|`wget -i` | Download a file from the list|

---
## GREP

**Linux command used to search for text strings in files or other commands output**

---

|Command|Explanation|
|-|-|
|`grep "text" file.txt` | Find text in a file|
|`grep -i` | Search regardless of case|
|`grep "text" file1.txt file2.txt` | Search in two files
|`grep -r "text" documents/ -e "*.txt"` |Search in the documents directory only in .txt files|
|`grep -r "text"` | Search in local directories and subdirectories|

---


## SCP

**Linux command, which is used to securely copy files and directories from one computer to another over a network**

---

|Command|Explanation|
|-|-|
|`scp username@remote_server:/full/path/to/remote_file /local/path/to/local_directory/`|From remote to local|
|`scp /local/path/to/local_file username@remote_server:/remote/path/to/destination/`|From local to remote|

---

## FIND

**Linux command used to search for various information in the file system**

---
|Command|Explanation|
|-|-|
|`.`| Current directory|
|`./kek` | Relative directory|
|`/home/carnifex17/kek` | Absolute path to the directory|
| `find ./GFG -perm 664` | Search for files with permissions 664 in the \.GFG directory|
|`-name` | File name|
|`-type f` | This option specifies that only files are searched.|
|`-type d` | Only directories are being searched.|
|`find . -type f -mtime -3`| Гsed to search for files by their modification time The file was modified less than 3 days ago|

---
## PS

**A program for Linux that is designed to search for various system processes**

---

|Command|Explanation|
|-|-|
|`ps aux` | All processes|
|`ps -p PID`| Additional info about PID|
|`ps -u shrek` | Additional info from **shrek** user|

---
## CHOWN

**A command in the Linux operating system that is used to change the owner or group of a file or directory**

---

|Command|Explanation|
|-|-|
|`chown owner_name file_name`| Change owner|
|`chown :group1 file1.txt`|Change group of file|
|`chown master:group1 file1.txt`| Change both|
|`chown --reference=greek1 greek2`| Use greek1 rights as reference|

---
## NSLOOKUP

**An operating system command used to perform DNS queries and obtain information about domain names, IP addresses, and other DNS records.**

---

|Command|Explanation|
|-|-|
|`nslookup -type=any` | List all available DNS records |
|`nslookup -type={type of dns recording}` |Search for certain DNS record|
|`A`, `MX`, `NS`, `TXT`, `SOA`, `AAAA`, `CNAME` |Types of DNS records|

---
## DIG

**Younger sibling of nslookup**

---

|Command|Explanation|
|-|-|
|`dig site.com +short` | A record|
|`dig site.com +nocomments` |No comments|
|`dig site.com ANY` | All records|
|`dig site.com +trace` | Trace DNS path|

---
## UNAME

**A command in the Unix operating system and similar systems that displays information about the system and its kernel.**

---

|Command|Explanation|
|-|-|
| `uname -a` |All system info|
| `uname -s`|Kernel name|
| `uname -r`|Kernel release date|

---

## UNIQ

**Linux command which looks for repeatings strings and helps to manage them**

---

|Command|Explanation|
|-|-|
|`uniq -c`| Counts how many times it is repeated|
| `uniq -d`| Only displays repeated feeds|
| `uniq -u` | Displays unique feeds|

---

## SORT

**You will never guess what it does**

---

|Command|Explanation|
|-|-|
| `sort -o outputfile.txt inputfile.txt` |Sorting with output to a specified file|
| `sort -r`|Sorting in reverse order|
| `sort -n`|Sorting by numbers|
| `sort -nr`|Sorting by numbers in reverse order|
| `sort -k 2n file.txt`|Sort by second column by numbers|

---
## WHOIS

**Command Linux, which looks for info about domains**

---

|Command|Explanation|
|-|-|
|`whois site.com` | Displaying information by domain name|
|`whois 125.8.888.200`| Displaying information by IP address|

---
## TAR

**Linux command used to unzip tar format**

---

|Command|Explanation|
|-|-|
|`tar -xvf file.tar`| Detailed unzipping|

---
## SYSTEMCTL

**Linux command to manage different services**

---

|Command|Explanation|
|-|-|
|`sudo systemctl restart service`| Restart service|
|`sudo systemctl status service`|Check service status|
|`sudo systemctl stop service`|Stop service|
|`sudo systemctl --type=service --state=running`|List active service|

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

