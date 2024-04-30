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

![image info](./images/ssh-image1.jpg)

```
ssh -L local_port:destination_address:destination_port username@remote_server
```
---
2.    **`Remote or Reverse Port Forwarding`**: In this case, the remote server is used to transfer traffic from the remote port to the local computer. 

![image info](./images/ssh-image2.jpg)

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

