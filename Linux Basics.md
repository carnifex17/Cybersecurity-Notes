---
# Table of Contents
---

- [Commands and Utilities](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#commands-and-utilities)
	- [AWK](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#awk)
	- [SUDO](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#sudo)
	- [LESS](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#less)
	- [TAIL](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#tail)
	- [WGET](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#wget)
	- [GREP](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#grep)
	- [SCP](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#scp)
	- [FIND](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#find)
	- [PS](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#ps)
	- [CHOWN](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#chown)
	- [NSLOOKUP](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#nslookup)
	- [DIG](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#dig)
	- [UNAME](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#uname)
	- [UNIQ](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#uniq)
	- [SORT](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#sort)
	- [WHOIS](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#whois)
	- [TAR](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#tar)
	- [SYSTEMCTL](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#systemctl)
	- [NETCAT](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#netcat)
	- [IP](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#ip)
- [Theory](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#theory)
	- [Logical Operators](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#logical-operators)
	- [SSH Tunneling](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#ssh-tunneling)
	- [Access Rights](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#access-rights)
	- [Data Streams, Redirects](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#data-streams-redirects)

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

## SUDO

**Linux utility that provides the ability to execute commands with different levels of access, including root**

---

| Command | Explanation |
| ------|-------|
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


---
# Theory 
---


---
## Logical Operators

**Symbols or keywords in Linux that are used to process and compare logical values.**

---

|`Syntax`|`Explanation`|
|-|-|
|**&&** |(AND)|
|`Command1 && Command2`| Executes Command2 only if Command1 succeeds (returns a zero exit code). If Command1 fails, Command2 is not executed|
|**II** |(OR)|
|`Command1 II Command2`|Executes Command2 only if Command1 fails (returns a non-zero exit code). If Command1 succeeds, Command2 is not executed|
|**;**| (Semicolon)|
|`Command1 ; Command2`|Executes Command2 regardless of the success or failure of Command1. Used for sequential execution of commands|
 |**&** |(Background Execution)|
|`Command &`| Executes the command in the background, allowing you to continue working in the terminal without waiting for the command to complete. You can use the **bg** or **jobs** commands to control background processes|
|**!**| (NOT)|
|`! Command`| Executes the command and returns the reverse exit code. If Command succeeds, ! Command fails, and vice versa|
| **I** | (PIPE)|
|`Command1 I Command2`| Redirects the output of Command1 to the input of Command2. Used to transfer data between commands and filter the output|

---



## SSH Tunneling

* `SSH Tunneling` - is a mechanism that allows you to securely transfer data over an unsecured network by encrypting and securing the connection between two points.  
`SSH (Secure Shell)` -  is a protocol for secure remote computer operation and data transfer, and it is used to create these secure tunnels. Mostly we could do the same things with local and reverse tunneling, but it depends which things we are controlling, remote server or local computer. Also to not be confused, you should always remember that "local" is subjective term.*
Also [this](https://youtu.be/AtuAdk4MwWw?si=85DZ-shYuHFJIqX2) video explains very well this topic
---

The main types of SSH Tunneling include:

1.    **`Local Port Forwarding`**: This type of tunneling allows you to pass traffic between your local computer and a remote server over SSH. So shortly we just communicate to some remote service, but in system level all requests to remote server will come through our our local port. It is pretty useful if we want to communicate to remote database as it is our local database. Useful stuff

<img width="500" height="500" src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/ssh-image1.jpg">

```
ssh -L local_port:destination_address:destination_port username@remote_server
```
---
2.    **`Remote or Reverse Port Forwarding`**: In this case, the remote server is used to transfer traffic from the remote port to the local computer. 

<img width="500" height="500" src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/ssh-image2.jpg">

```
ssh -R remote_port:localhost:local_port username@local_machine_ip
```
3.    **`Dynamic Port Forwarding`**: This type of tunneling allows you to create a "proxy" on a remote server through which you can route traffic from your local computer through the remote server to various Internet resources. This is especially useful when you need anonymous access to the Internet or when you need to bypass network restrictions.
```
ssh -D local_socks_port username@remote_server
```
---



## Access Rights

**Linux has its own scheme for displaying access rights using numbers to make it quick and easy to show which rights are where. Each three digits corresponds to three access rights (read, write, execute) for three different categories of users (owner, group, other).
Each of these digits can have a value from 0 to 7, where each value represents a combination of three possible access rights:**

>0 - (no rights).
>1 - (execute).
>2 - (write).
>4 - (read).

---

### **File Rights**

To set permissions using numbers, you simply add the number values for each category together:
For example, `chmod 755 file.txt' sets the following permissions:
1. The owner has read, write, and execute permissions (4 + 2 + 1 = 7).
2. Group has read and execute permissions (4 + 1 = 5).
3. Other users have read and execute permissions (4 + 1 = 5).

---

### **Directory Rights**.

For example, in the directory, it displays `drwxr-xr-x`.
The first character `d` is the type of object. In this case, `d` indicates that it is a directory. The rest of the `rwxr-xr-x` string consists of **nine** characters that represent access rights for different categories of users (***owner, group, and others***). This part of the string can be considered as three sets of three characters each.

The first set `rwx` represents the access rights for the ***object owner***:

1. `r` ***Owner*** has the right to read the file or view the contents of the directory. 
2. `-` ***Owner*** has the right to write or edit the file or create new files in the directory.
3. `x` ***Owner*** has the right to execute the file (for directories, this means the ability to access it as a directory).

The second set of `r-x` represents the access rights for a ***user group***:

1. `r` ***Group*** has the right to read the file or view the contents of the directory.
2. `-` ***Group*** does not have the right to write the file or create new files in the directory.
3. `x` ***Group*** has the right to execute the file (for directories).

The third set of `r-x` represents access rights for ***other users*** (users who are not owners and do not belong to the group):
1. `r` ***Other users*** have the right to read the file or view the contents of the directory.
2. `-` ***Other users*** do not have the right to write the file or create new files in the directory.
3. `x` ***Other users*** have the right to execute the file (for directories).


## Data Streams, Redirects

**In Linux, there is such a thing as *data streams*, which are used to transmit input/output data in programs. Each of them has its own *descriptor*, a numeric identifier that helps to interact with them more easily**
- `STDIN` - Descriptor 0. Input stream
- `STDOUT` - Descriptor 1. Output stream
- `STDERR` - Descriptor 2. Error stream
- The output in the output streams is separate and in parallel.

---

***REDIRECT( > )* is redirect of the command output to the file `(ls > dirs.txt).` Redirect by default is through the `stdout` stream, but it can be changed. 
`cat unexistedfile.txt 2> error.txt`
*Reverse redirect ( < )* is redirect of the output stream through `stdin` so that the input is not through the keyboard but through the file**

---
### Examples

`2>&1` 
*If we redirect the output from `stderr`, we output to the same place as the output from `stdout`. And with this we can output both simple output and errors in one file, one stream*.

`0>&1`
*By using **0>&1**, you are actually telling the shell to read `stdin` from the same source as `stdout`. This can be useful in cases where you need to merge or copy input and output streams for interactive input, for example in reverse shells*.

---



