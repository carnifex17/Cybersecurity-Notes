---
# Table of Contents
---

- [Commands and Utilities](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B8-%D1%82%D0%B0-%D1%83%D1%82%D0%B8%D0%BB%D1%96%D1%82%D0%B8)
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
- [Theory](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#%D1%82%D0%B5%D0%BE%D1%80%D1%96%D1%8F)
	- [Logical Operators](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#%D0%BB%D0%BE%D0%B3%D1%96%D1%87%D0%BD%D1%96-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%B8)
	- [SSH Tunneling](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#ssh-%D1%82%D1%83%D0%BD%D0%B5%D0%BB%D1%8E%D0%B2%D0%B0%D0%BD%D0%BD%D1%8F)
	- [Access Rights](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#%D0%BF%D1%80%D0%B0%D0%B2%D0%B0-%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D1%83)
	- [Data Streams, Redirects](https://github.com/carnifex17/Cybersecurity-Notes/blob/main/Linux%20Basics.md#%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8-%D0%B7%D0%B2%D1%8F%D0%B7%D0%BA%D1%83-%D0%BF%D0%B5%D1%80%D0%B5%D0%BD%D0%B0%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%BD%D1%8F)

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
|`less -F` | Слідкувати за змінами в файлі| 
|`less -X` |Лишити те що було в файлі без видалення після вимкнення команди|
|`less -N` | Нумерувати рядки |

---
## TAIL

**Command used to output the contents of a file, usually at the end of that file**

---

| Command | Explanation |
| ------|-------|
|`tail -50` | Скільки рядків треба з кінця взяти|
|`tail +50` | Скільки рядків треба взяти з початку|
|`tail -c` | Кількість байтів яку треба забрати з кінця|
|`tail -F` | Моніторити зміни в файлі|

---

## WGET 

**Download files from sites**

---

|Command|Explanation|
|-|-|
|`wget IP`| Завантажити файл з сайту|
|`wget -O` | Зберегти файл під новим іменем|
|`wget -i` | Завантажувати файл зі списку|

---
## GREP

**Linux command used to search for text strings in files or other commands output**

---

|Command|Explanation|
|-|-|
|`grep "text" file.txt` | Найти текст в файлі|
|`grep -i` | Пошук незалежно від регістра|
|`grep "text" file1.txt file2.txt` | Пошук в двух файлах|
|`grep -r "text" documents/ -e "*.txt"` | Пошук в каталозі documents виключно в файлах .txt|
|`grep -r "text"` | Пошук в локальних директоріях і субдиректоріях|

---


## SCP

**Linux command, which is used to securely copy files and directories from one computer to another over a network**

---

|Command|Explanation|
|-|-|
|`scp username@remote_server:/full/path/to/remote_file /local/path/to/local_directory/`|З віддаленого сервера на локальний|
|`scp /local/path/to/local_file username@remote_server:/remote/path/to/destination/`|З локального сервера на віддалений|

---

## FIND

**Linux command used to search for various information in the file system**

---
|Command|Explanation|
|-|-|
|`.`| Поточний каталог|
|`./kek` | Відносний каталог|
|`/home/carnifex17/kek` | Абсолютний шлях до каталогу|
| `find ./GFG -perm 664` | Шукати в  директорії \.GFG файли з правами 664|
|`-name` | Назва файлу|
|`-type f` | Цей параметр вказує на пошук лише файлів (регулярних файлів).|
|`-type d` | Він вказує на пошук лише каталогів.|
|`find . -type f -mtime -3`| використовується для пошуку файлів за часом їхньої зміни (modification time) Змінений файл менше ніж 3 дня назад|

---
## PS

**Програма для Linux яка створена для пошуку різних системних процесів**

---

|Command|Explanation|
|-|-|
|`ps aux` | Всі процеси |
|`ps -p PID`| Доп інфа по PID|
|`ps -u shrek` | Доп інфа по процесам від користувача **shrek**|

---
## CHOWN

**Command в операційній системі Linux, яка використовується для зміни власника або групи файлу або каталогу**

---

|Command|Explanation|
|-|-|
|`chown owner_name file_name`| Змінити власника|
|`chown :group1 file1.txt`|Змінити групу файлу|
|`chown master:group1 file1.txt`| Змінити і те і те|
|`chown --reference=greek1 greek2`| Змінити право власника з одного файлу на інший|

---
## NSLOOKUP

**Command в операційній системі, яка використовується для виконання DNS-запитів і отримання інформації про доменні імена, IP-адреси та інші DNS-записи.**

---

|Command|Explanation|
|-|-|
|`nslookup -type=any` | Пошук всіх DNS записів |
|`nslookup -type={type of dns recording}` |Пошук конкретного DNS запиту|
|`A`, `MX`, `NS`, `TXT`, `SOA`, `AAAA`, `CNAME` |Типи DNS записів|

---
## DIG

**Command яка схожа по сенсу та функціоналу за nslookup**

---

|Command|Explanation|
|-|-|
|`dig site.com +short` | A запис|
|`dig site.com +nocomments` |Без коментарів|
|`dig site.com ANY` | Всі записи|
|`dig site.com +trace` | Відслідкувати шлях DNS|

---
## UNAME

**Command в операційній системі Unix та подібних системах, яка виводить інформацію про систему та її ядро.**

---

|Command|Explanation|
|-|-|
| `uname -a` |Вся системна інформація|
| `uname -s`|Назва ядра|
| `uname -r`|Дата релізу ядра|

---

## UNIQ

**Command яка видаляє стрічки, які повторюються**

---

|Command|Explanation|
|-|-|
|`uniq -c`| Рахує скільки раз повторюється|
| `uniq -d`| Тільки виводить стрічки які повторювались|
| `uniq -u` | Виводить унікальні стрічки|

---

## SORT

**Command Linux, яка сортує файли**

---

|Command|Explanation|
|-|-|
| `sort -o outputfile.txt inputfile.txt` |Сортування з виводом у вказаний файл|
| `sort -r`|Сортування по порядку навпаки|
| `sort -n`|Сортування по числам|
| `sort -nr`|Сортуванням по числам навпаки|
| `sort -k 2n file.txt`|Сортування за другою колонкою числами|

---
## WHOIS

**Command Linux, which looks for info about domains**

---

|Command|Explanation|
|-|-|
|`whois site.com` | Вивід інформації за доменом|
|`whois 125.8.888.200`| Вивід інформації за ІР адресою|

---
## TAR

**Command Linux, яка використовується для розархівування tar формату**

---

|Command|Explanation|
|-|-|
|`tar -xvf file.tar`| Детальне розархівування|

---
## SYSTEMCTL

**Command Linux, яка використовується для контролю різноманітними сервісами**

---

|Command|Explanation|
|-|-|
|`sudo systemctl restart service`| Перезавантажити сервіс|
|`sudo systemctl status service`|Провірити стан сервісу|
|`sudo systemctl stop service`| Зупинити сервіс|
|`sudo systemctl --type=service --state=running`| Перелік активних сервісів|

---

## NETCAT

**Універсальна утиліта для мережевого з'єднання в операційних системах Unix та подібних системах**

---

|Command|Explanation|
|-|-|
|`nc host port`|Робить з'єднання до хоста на вказаний порт|
|`nc -l -p port`|Запускає nc в режим слухання(listener) на вказаному порті|
|`nc -z host {port-range}`|Базовий сканер портів|
|`nc -v host port`|Дістати баннер|
|`nc -l -p local_port -c 'nc remote_host remote_port'`|Налаштовує базовий проксі, коли він прослуховує певний локальний порт і пересилає його на віддалений сервер|
|`nc -l -p 1234 -e /bin/bash`|Простий бекдор|

---


## IP

**Command Linux для контролю ІР. Старіший аналог ifconfig**

---

|Command|Explanation|
|-|-|
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

<img src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/ssh-image1.jpg">

```
ssh -L local_port:destination_address:destination_port username@remote_server
```
---
2.    **`Remote or Reverse Port Forwarding`**: In this case, the remote server is used to transfer traffic from the remote port to the local computer. 

<img src="https://github.com/carnifex17/Cybersecurity-Notes/blob/main/images/ssh-image2.jpg">

```
ssh -R remote_port:localhost:local_port username@local_machine_ip
```
3.    **`Dynamic Port Forwarding`**: This type of tunneling allows you to create a "proxy" on a remote server through which you can route traffic from your local computer through the remote server to various Internet resources. This is especially useful when you need anonymous access to the Internet or when you need to bypass network restrictions.
```
ssh -D local_socks_port username@remote_server
```
---



## Access Rights

**У Linux є своя схема показу прав доступу за допомогою цифр, щоб було швидко і легко показати які права де. Кожні три цифри відповідають трьом правам доступу (читання, запис, виконання) для трьох різних категорій користувачів (власник, група, інші).
Кожна з цих цифр може мати значення від 0 до 7, де кожне значення представляє собою комбінацію трьох можливих прав доступу:**

>0 - Немає прав доступу (відсутність права).
>1 - Виконання (execute).
>2 - Запис (write).
>4 - Читання (read).

---

### **File Rights**

Для встановлення прав доступу за допомогою цифр, ви просто додаєте значення цифр для кожної категорії разом:
Наприклад, `chmod 755 file.txt` встановлює такі права:
1. Власник має права на читання, запис і виконання (4 + 2 + 1 = 7).
2. Група має права на читання, виконання (4 + 1 = 5).
3. Інші користувачі мають права на читання і виконання (4 + 1 = 5).

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



