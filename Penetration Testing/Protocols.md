---
# Protocols
---

## FTP
**The File Transfer Protocol is a standard communication protocol used for the transfer of computer files from a server to a client on a computer network. FTP is built on a client–server model architecture using separate control and data connections between the client and the server.**
### TFTP
One of the most used FTP servers on Linux-based distributions is vsFTPd. The default configuration of vsFTPd can be found in `/etc/vsftpd.conf`. Users, for which access to FTP server is forbidden could be found at /etc/ftpusers file
### Dangerous Config Settings
- `anonymous_enable=YES` - Allowing anonymous login?
- `anon_upload_enable=YES` - Allowing anonymous to upload files?
- `anon_mkdir_write_enable=YES` - Allowing anonymous to create new directories?
- `no_anon_password=YES` - Do not ask anonymous for password?
- `anon_root=/home/username/ftp` - Directory for anonymous.
- `write_enable=YES` -  Allow the usage of FTP commands
### Tips2Hack
1. Try to use anonymous login, config allows that, you could lurk for some juicy info. For this just use `anonymous` as login name, and left password empty.
2. If config allows, you could lurk even faster through directories with recursive listing `ls -R`
3. To download a file you need to use `get` command and to upload you need `put` and also you could use `status` to get more info about server and FTP state
4. To download **all** files you need to use
```bash
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136
```
5. Check all available nmap ftp scripts:
```bash
find / -type f -name ftp* 2>/dev/null | grep scripts
```
---

## SMB
**Server Message Block (SMB) is a client-server protocol that regulates access to files and entire directories and other network resources such as printers, routers, or interfaces released for the network.** The SMB protocol enables the client to communicate with other participants in the same network to access files or services shared with it on the network. 
### Samba 
**Samba is an alternative variant to the SMB server, called Samba, developed for Unix-based operating system.** Samba implements the Common Internet File System (CIFS) network protocol. CIFS is a "dialect" of SMB. In other words, CIFS is a very specific implementation of the SMB protocol, which in turn was created by Microsoft. Therefore, it usually is referred to as SMB / CIFS. However, CIFS is the extension of the SMB protocol.
- Samba server over TCP ports `137`, `138`, `139`, but CIFS uses TCP port `445` only.
In a network,using Samba, each host participates in the same `workgroup`. A workgroup is a group name that identifies an arbitrary collection of computers and their resources on an SMB network.
- `smbstatus` command to see who, from which host, and which share the client is connected.
### Smbclient
**Connecting to the Share**
```bash
smbclient -N -L //13.13.13.13
```
**OR**
```bash
smbclient -U username \\\\13.13.13.13\\share
```

- `-N` is for **null session**, which is anonymous access without the input user/pass. And `-L` is to list all shares.
- For basic interaction with share, you would need only these commands:
	- `help` to have list of available commands
	- `ls` list
	- `get` download
	- `!command` user prefix ! before command to execute it locally
### RPCclient
**The Remote Procedure Call (RPC) is a concept and, therefore, also a central tool to realize operational and work-sharing structures in networks and client-server architectures. Other words, RPC is a mechanism for interaction between processes that are executed on different nodes in the network.** The communication process via RPC includes passing parameters and the return of a function value. Also RPC have Remote Invocation Descriptor,which is a unique identifier assigned to each remote procedure call. It is used to keep track of and manage the execution of remote procedures.
- Connect to SMB server
```bash
rpcclient -U "" 10.129.14.128
```
With connected RPC clietn we could use many different functions as:

|Function|Description|
|-|-|
|`srvinfo`|Server information|
|`enumdomains`|Enumerate all domains that are deployed in the network|
|`querydominfo`|Provides domain, server, and user information of deployed domains|
|`netshareenumall`|Enumerates all available shares|
|`netsharegetinfo <share>`|Provides information about a specific share|
|`enumdomusers`|Enumerates all domain users|
|`queryuser <RID>`|Provides information about a specific user|
|`querygroup <RID>`|Provides information about a specific group|
### Dangerous Config Settings
- `browseable = yes` - Allow listing available shares in the current share?
- `read only = no` - Forbid the creation and modification of files?
- `writable = yes` - Allow users to create and modify files?
- `guest ok = yes` - Allow connecting to the service without using a password?
- `enable privileges = yes` - Honor privileges assigned to specific SID?
- `create mask = 0777` - What permissions must be assigned to the newly created files?
- `directory mask = 0777` - What permissions must be assigned to the newly created directories?
- `logon script = script.sh` - What script needs to be executed on the user's login?
- `magic script = script.sh` - Which script should be executed when the script gets closed?
- `magic output = script.out` - Where the output of the magic script needs to be stored?
### Tips2Hack
1. Samba config location:
```bash
cat /etc/samba/smb.conf | grep -v "#\|\;"
```
2. To bruteforce RID using rpcclient to do active enum of users and groups you could use this command:
```bash
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```
3. Or for the same cause you could try yo use [samrdump.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py) script
4. You could use `SMBmap tool`
```bash
smbmap -H 13.13.13.13
```
5. You could use `CrackMapExec`
```bash
crackmapexec smb 13.13.13.13 --shares -u '' -p ''
```
6. You could use [enum4linux-ng](https://github.com/cddmp/enum4linux-ng)
```bash
./enum4linux-ng.py 13.13.13.13 -A
```
---

## NFS
**Network File System (NFS) is a network file system developed by Sun Microsystems and has the same purpose as SMB.** Its purpose is to access file systems over a network as if they were local. NFS is used between Linux and Unix systems. This means that NFS clients cannot communicate directly with SMB servers. The `/etc/exports` file contains a table of physical filesystems on an NFS server accessible by the clients.
### Dangerous Settings
- `rw` - Read and write permissions.
- `insecure` - Ports above 1024 will be used.
- `nohide` - If another file system was mounted below an exported directory, this directory is exported by its own exports entry.
- `no_root_squash` - All files created by root are kept with the UID/GID 0.
### Tips2Hack
1. Basic nmap footprinting
```bash  
sudo nmap --script nfs* 13.13.13.13 -sV -p111,2049
```
2. Show available NFS shares
```bash
showmount -e 13.13.13.13
```
3. Mounting & Unmounting NFS shares
```bash
> mkdir target-NFS
> sudo mount -t nfs 13.13.13.13:/ ./target-NFS/ -o nolock
> sudo umount ./target-NFS
```
---

## SSH

**Secure Shell (SSH) enables two computers to establish an encrypted and direct connection within a possibly insecure network on the standard port `TCP 22`.**

OpenSSH has six different authentification methods:
1. Password authentification
2. Public-key authentification
3. Host-based authentification
4. Keyboard authentification
5. Challenge-response authentification
6. GSSAPI authentification

### Public Key Authentification

In a first step, the SSH server and client authenticate themselves to each other. The server sends a certificate to the client to verify that it is the correct server. After server authentication, however, the client must also prove to the server that it has access authorization. However, the SSH server is already in possession of the encrypted hash value of the password set for the desired user. As a result, users have to enter the password every time they log on to another server during the same session. To make all this process easier, there is ability to use `public` and `private key`. The **private key** is created individually for the user's own computer and secured with a passphrase that should be longer than a typical password. The private key is stored exclusively on our own computer and always remains secret. **Public keys** are also stored on the server. The server creates a cryptographic problem with the client's public key and sends it to the client. The client, in turn, decrypts the problem with its own private key, sends back the solution, and thus informs the server that it may establish a legitimate connection. Config file is sshd_config, and located in /etc/ssh/sshd_config, also could be found via command:

```bash
cat /etc/ssh/sshd_config  | grep -v "#" | sed -r '/^\s*$/d'
```

### Dangerous Settings

| Setting | Description |
| ---- | ---- |
| `PasswordAuthentication yes` | Allows password-based authentication. |
| `PermitEmptyPasswords yes` | Allows the use of empty passwords. |
| `PermitRootLogin yes` | Allows to log in as the root user. |
| `Protocol 1` | Uses an outdated version of encryption. |
| `X11Forwarding yes` | Allows X11 forwarding for GUI applications. |
| `AllowTcpForwarding yes` | Allows forwarding of TCP ports. |
| `PermitTunnel` | Allows tunneling. |
| `DebianBanner yes` | Displays a specific banner when logging in. |
### Tips2Hack

1. SSH-Audit
```bash
> git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit
> ./ssh-audit.py 13.13.13.13
```
2. Change Auth Method
```bash
ssh -v carnifex17@13.13.13.13 -o PreferredAuthentications=password
```
3. If you have access to `/.ssh/authorized_keys` file, then put your **public key** inside of this file, and then you could log in without password
4. If you have access to some **private key** you could download it and use, but check if permissions to private key is **chmod 600**
```bash
ssh -i /path/to/private/keyfile user@hostname
```

---

## SMTP
**The Simple Mail Transfer Protocol (SMTP) is a protocol for sending emails in an IP network.** It can be used between an email client and an outgoing mail server or between two SMTP servers. SMTP is often combined with the `IMAP` or `POP3` protocols, which can fetch emails and send emails. In principle, it is a client-server-based protocol, although SMTP can be used between a client and a server and between two SMTP servers.
### SMTP Servers
SMTP servers play a crucial role in preventing spam by supporting `ESMTP` with `SMTP-Auth` for authorized user-based email sending. The Mail User Agent (`MUA`) converts emails into headers and bodies, uploading them to the SMTP server. A Mail Transfer Agent (`MTA`) checks email size and spam, storing it after validation. Occasionally, a Mail Submission Agent (`MSA`) or Relay server validates email origin to prevent `Open Relay` Attacks. The MTA then searches DNS for the recipient mail server's IP address.
```bash
MUA(Client) -> MSA(Submission Agent) -> MTA(Open Relay) -> MDA(Mail Delivery Agent) -> POP3/IMAP(Mailbox)
```
But SMTP has some disadvantages:
1. Sending an email using SMTP doesn't return usable delivery confirmation.
2. Users are not authenticated when a connection is established, and the sender of an email is therefore unreliable. As a result, open SMTP relays are often misused to send spam a lot
For this purpose, an extension for SMTP has been developed called Extended SMTP (`ESMTP`). When people talk about SMTP in general, they usually mean ESMTP
### Tips2Hack
1. You can try to enumerate users via Telnet VRFY
```bash
> telnet 13.13.13.13 25
> VRFY carnifex17
252 2.0.0 carnifex17
```
2. Nmap - Open Relay
```bash
sudo nmap 13.13.13.13 -p25 --script smtp-open-relay -v
```
3. SMTP - Nmap all enum
```bash
sudo nmap 13.13.13.13 -p25 -sV -sC --script smtp* -v
```

---

## Rsync
**`Rsync` is a fast and efficient tool for locally and remotely copying files.** Rsync reduces the amount of data transmitted over the network when a version of the file already exists on the destination host. It does this by sending only the differences between the source files and the older version of the files that reside on the destination server. It is often used for backups and mirroring. You could use [that](https://book.hacktricks.xyz/network-services-pentesting/873-pentesting-rsync) page to view more ways to abuse Rsync. 

### Tips2Hack
1. Scanning for Rsync
```bash
sudo nmap -sV -p 873 127.0.0.1
```
2. Probing for `Accessible Share`
```bash
nc -nv 127.0.0.1 873
```
3. Enumerating an Open Share
```bash
rsync -av --list-only rsync://127.0.0.1/dev
```

---

## IMAP / POP3
**With the help of the Internet Message Access Protocol (IMAP), access to emails from a mail server is possible. Unlike the Post Office Protocol (POP3), IMAP allows online management of emails directly on the server and supports folder structures.** Thus, it is a network protocol for the online management of emails on a remote server. The protocol is client-server-based and allows synchronization of a local email client with the mailbox on the server, providing a kind of network file system for emails, allowing problem-free synchronization across several independent clients. POP3, on the other hand, does not have the same functionality as IMAP, and it only provides listing, retrieving, and deleting emails as functions at the email server. Therefore, protocols such as IMAP must be used for additional functionalities such as hierarchical mailboxes directly at the mail server, access to multiple mailboxes during a session, and preselection of emails. Clients access these structures online and can create local copies. Emails remain on the server until they are deleted. It is also possible for several users to access the email server simultaneously. Without an active connection to the server, managing emails is impossible. However, some clients offer an offline mode with a local copy of the mailbox. The client synchronizes all offline local changes when a connection is reestablished. The client establishes the connection to the server via port 143.
### IMAP Commands

|Command|Description|
|-|-|
|`LOGIN username password`|User's login|
|`LIST "" *`| Lists all directories|
|`CREATE "INBOX"`|Creates a mailbox with a specified name|
|`DELETE "INBOX"`| Deletes a mailbox|
|`RENAME "ToRead" "Important"`|Renames a mailbox|
|`LSUB "" *`|Returns a subset of names from the set of names that the User has declared as being `active` or `subscribed`|
|`SELECT INBOX`|Selects a mailbox so that messages in the mailbox can be accessed|
|`UNSELECT INBOX`| Exits the selected mailbox|
|`FETCH <ID> all`| Retrieves data associated with a message in the mailbox|
|`CLOSE`| Removes all messages with the Deleted flag set|
|`LOGOUT`|Closes the connection with the IMAP server|

---

### POP3 Commands
|Command|Description|
|-|-|
|`USER username`|Identifies the user|
|`PASS password`|Authentication of the user using its password|
|`STAT`|Requests the number of saved emails from the server|
|`LIST`|Requests from the server the number and size of all emails|
|`RETR id`|Requests the server to deliver the requested email by ID|
|`DELE id`|Requests the server to delete the requested email by ID|
|`CAPA`|Requests the server to display the server capabilities|
|`RSET`|Requests the server to reset the transmitted information|
|`QUIT`|Closes the connection with the POP3 server|

### Dangerous Settings

- `auth_debug` -  Enables all authentication debug logging.
- `auth_debug_passwords` - This setting adjusts log verbosity, the submitted passwords, and the scheme gets logged.
- `auth_verbose` - Logs unsuccessful authentication attempts and their reasons.
- `auth_verbose_passwords` - Passwords used for authentication are logged and can also be truncated.
- `auth_anonymous_username` - This specifies the username to be used when logging in with the ANONYMOUS SASL mechanism.

### Tips2Hack
1. By default, ports `110`, `143`, `993`, and `995` are used for IMAP and POP3
2. Nmap basic footprinting
```bash 
sudo nmap 13.13.13.13 -sV -p110,143,993,995 -sC
```
3. IMAP Curl List mailboxes
```bash
curl -k 'imaps://13.13.13.13' --user user:p4ssw0rd
```
4. OpenSSL - TLS Encypted Interaction POP3 
```bash
openssl s_client -connect 13.13.13.13:pop3s
```

---
## DNS
**Domain Name System (DNS) is an integral part of the Internet. For example, through domain names, such as academy.hackthebox.com or www.hackthebox.com, we can reach the web servers that the hosting provider has assigned one or more specific IP addresses.** DNS is a system for resolving computer names into IP addresses, and it does not have a central database. The configuration files are usually : `named.conf.local`, `named.conf.options`, `named.conf.log`

| Server Type | Description |
|-|-|
| `DNS Root Server` | The root servers of the DNS are responsible for the top-level domains (`TLD`). As the last instance, they are only requested if the name server does not respond. Thus, a root server is a central interface between users and content on the Internet, as it links domain and IP address. The Internet Corporation for Assigned Names and Numbers (`ICANN`) coordinates the work of the root name servers. There are 13 such root servers around the globe. |
|` Authoritative Nameserver`| Authoritative name servers hold authority for a particular zone. They only answer queries from their area of responsibility, and their information is binding. If an authoritative name server cannot answer a client's query, the root name server takes over at that point.|
| `Non-authoritative Nameserver` | Non-authoritative name servers are not responsible for a particular DNS zone. Instead, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying.|
| `Caching DNS Server` | Caching DNS servers cache information from other name servers for a specified period. The authoritative name server determines the duration of this storage.|
| `Forwarding Server`| Forwarding servers perform only one function: they forward DNS queries to another DNS server. |
| `Resolver` | Resolvers are not authoritative DNS servers but perform name resolution locally in the computer or router.|
![image info](./images/pentesting-image-3.png)
There are many useful and not DNS records:

- `A`:  Returns an IPv4 address of the requested domain as a result.
- `AAAA`: Returns an IPv6 address of the requested domain.
- `MX`: Returns the responsible mail servers as a result. 
- `NS`: Returns the DNS servers (nameservers) of the domain.
- `TXT`: this type of record often contains verification keys for different third-party providers and other security aspects of DNS
- `CNAME`: This record serves as an alias. 
- `PRT`: The PTR record works the other way around (reverse lookup). It converts IP addresses into valid domain names.
- `SOA`: Provides information about the corresponding DNS zone and email address of the administrative contact.

### Zone Files
**A DNS zone is a portion of the DNS namespace that a specific organization or administrator manages. Since DNS comprises multiple DNS zones, DNS servers utilize DNS zone transfers to copy a portion of their database to another DNS server. Unless a DNS server is configured correctly (limiting which IPs can perform a DNS zone transfer), anyone can ask a DNS server for a copy of its zone information since DNS zone transfers do not require any authentication.** For the IP address to be resolved from the Fully Qualified Domain Name (`FQDN`), the DNS server must have a reverse lookup file. In this file, the computer name (FQDN) is assigned to the last octet of an IP address, which corresponds to the respective host, using a PTR record.

#### Zone Transfer
`Zone transfer` refers to the transfer of zones to another server in DNS, which generally happens over TCP port 53. This procedure is abbreviated **Asynchronous Full Transfer Zone** (`AXFR`). Since a DNS failure usually has severe consequences for a company, the zone file is almost invariably kept identical on several name servers. When changes are made, it must be ensured that all servers have the same data. Synchronization between the servers involved is realized by zone transfer. A DNS server that serves as a direct source for synchronizing a zone file is called a master. A DNS server that obtains zone data from a master is called a slave.

### Tips2Hack

1. DIG - NS Query
```bash
dig ns inlanefreight.kek @13.13.13.13
```
2. DIG - Version Query
```bash
dig CH TXT version.bind 13.13.13.13
```
3. DIG - ANY Query
```bash
dig any inlanefreight.kek @13.13.13.13
```
4. DIG - AXFR Zone Transfer
```bash
dig axfr inlanefreight.kek @13.13.13.13
```
5. DIG - AXFR Zone Transfer - Internal  
```bash
dig axfr internal.inlanefreight.kek @13.13.13.13
```
6. DNSEnum
```bash
dnsenum --dnsserver 13.13.13.13 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.kek
```
---
## SNMP
**SNMP or Simple Network Management Protocol is an application-layer Internet Standard protocol used for managing information about devices on an IP network.**.It can also be used to modify the device information and change device behavior. The protocol lets devices on the same network communicate with each other and is commonly used for collecting information about the health and status of the devices on the network. SNMP also transmits control commands using agents over UDP port 161 and sometimes port 162
- `OID` - **Object Identifier**. An OID represents a node in a hierarchical namespace. A sequence of numbers uniquely identifies each node, allowing the node's position in the tree to be determined.
- `MIB` - **Management Information Base**. MIB is an independent format for storing device information. A MIB is a text file in which all queryable SNMP objects of a device are listed in a standardized tree hierarchy. It contains at least one OID

### SNMPwalk
An SNMPwalk is an application that repeatedly sends out GetNextRequest to collect information about different OIDs. The application bundles together multiple SNMP commands and lets you collect information from multiple devices without having to type out individual commands for all OIDs. It can help you identify devices in the network that are not working. By performing an SNMP walk, you can find out the entire list of devices in your network that supports SNMP and form a library of MIBs.

### Versions
1. `SNMPv1` - No authentification. For SNMPwalk use `-v1` argument to use.
2. `SNMPv2` - No encryption. Community strings can be seen as passwords that are used to determine whether the requested information can be viewed or not. Also could be called as `v2c`, which means**v2 community** In `v2c` can be intercepted.
3. `SNMPv3` - Finally now it has authentification and encryption. That's a won

### Dangerous Settings
**View config file**
```bash
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'
```
- `rwuser noauth` -  Provides access to the full OID tree without authentication.
- `rwcommunity <community string> <IPv4 address>` - Provides access to the full OID tree regardless of where the requests were sent from.
- `rwcommunity6 <community string> <IPv6 address>` - Same access as with rwcommunity with the difference of using IPv6.

### Tips2Hack

1. SNMPwalk
```bash
snmpwalk -v2c -c public 10.129.14.128
```
2. OneSixtyOne (`SNMP scanner`). Can be used to brute-force the names of the community strings since they can be named arbitrarily by the administrator
```bash
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt 13.13.13.13
```
3. Braa. Once we know a community string, we can use it with braa to brute-force the individual `OIDs` and enumerate the information behind them.
```bash
> braa <community string>@13.13.13.13:.1.3.6.*
```

---

## MySQL
**MySQL is an open-source SQL relational database management system developed and supported by Oracle.** A database is simply a structured collection of data organized for easy use and retrieval. The database system can quickly process large amounts of data with high performance. Default MySQL port is 3306. The most important databases fot the MySQL are the `system schema (sys)` and `information schema (information_schema)`. The system schema contaions tables, information, and metadata necessary for management. The **information schema** contains metadata which mainly retrieved from th system **schema database**.
### Dangerous Settings
**View config file**
```bash
cat /etc/mysql/mysql.conf.d/mysqld.cnf | grep -v "#" | sed -r '/^\s*$/d'
```

- `user` - Sets which user the MySQL service will run as
- `password` - Sets the password for the MySQL user
- `admin_address` - The IP address on which to listen for TCP/IP connections on the administrative network interface
- `debug` - This variable indicates the current debugging settings
- `sql_warnings` - This variable controls whether single-row INSERT statements produce an information string if warnings occur
- `secure_file_priv` - This variable is used to limit the effect of data import and export operations
### Basic MySQL Interaction Commands

|Command|Description|
|-|-|
|`mysql -u <user> -p<password> -h <IP address>`|Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password.|
|`show databases;`|Show all databases|
|`use <database>;`|Select one of the existing databases|
|`show tables;`|Show all available tables in the selected database|
|`show columns from <table>;`|Show all columns in the selected database|
|`select * from <table>;`|Show everything in the desired table|
|`select * from <table> where <column> = "<string>";`|Search for needed `string` in the desired table|

### Tips2Hack

1. Nmap Basic Footprinting
```bash
sudo nmap 13.13.13.13 -sV -sC -p3306 --script mysql*
```
---

## MSSQL
**Microsoft SQL (MSSQL) is Microsoft's SQL-based relational database management system.** It is popular among database administrators and developers when building applications that run on Microsoft's .NET framework due to its strong native support for .NET. MSSQL have a lot of different targets. Default port is 1433

### Databases
MSSQL has default system databases that can help us understand the structure of all the databases that may be hosted on a target server. 

|Database|Description|
|-|-|
|`master`|Tracks all system information for an SQL server instance|
|`model`|Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database|
|`msdb`|The SQL Server Agent uses this database to schedule jobs & alerts|
|`tempdb`|Stores temporary objects|
|`resource`|Read-only database containing system objects included with SQL server|
### Tips2Hack

1. Nmap MSSQL Script Scan
```bash
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 13.13.13.13
```
2. Metasploit scan. We can user `mssql_ping` to get more useful info about MSSQL server.
```bash
msf6 auxiliary(scanner/mssql/mssql_ping) > set rhosts 13.13.13.13

rhosts => 13.13.13.13

msf6 auxiliary(scanner/mssql/mssql_ping) > run

[*] 10.129.201.248:       - SQL Server information for 13.13.13.13:
[+] 10.129.201.248:       -    ServerName      = SQL-01
[+] 10.129.201.248:       -    InstanceName    = MSSQLSERVER
[+] 10.129.201.248:       -    IsClustered     = No
[+] 10.129.201.248:       -    Version         = 15.0.2000.5
[+] 10.129.201.248:       -    tcp             = 1433
[+] 10.129.201.248:       -    np              = \\SQL-01\pipe\sql\query
[*] 10.129.201.248:       - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```
3. Connecting with Mssqlclient.py
```bash
python3 mssqlclient.py Administrator@13.13.13.13 -windows-auth
```
---

## Oracle TNS

**The Oracle Transparent Network Substrate (TNS) server is a communication protocol that facilitates communication between Oracle databases and applications over networks.**. Default Oracle TNS port is TCP/1521, but can be easily changed. The configuration files for Oracle TNS are called tnsnames.ora and listener.ora and are typically located in the ORACLE_HOME/network/admin directory. Each database or service has a unique entry in the tnsnames.ora file, containing the necessary information for clients to connect to the service. In Oracle RDBMS, a System Identifier (`SID`) is a unique name that identifies a particular database instance. It can have multiple instances, each with its own System ID. An instance is a set of processes and memory structures that interact to manage the database's data. When a client connects to an Oracle database, it specifies the database's SID along with its connection string. The client uses this SID to identify which database instance it wants to connect to
### PLSQL Exclusion List
Oracle databases can be protected by using so-called PL/SQL Exclusion List (PlsqlExclusionList). It is a user-created text file that needs to be placed in the $ORACLE_HOME/sqldeveloper directory, and it contains the names of PL/SQL packages or types that should be excluded from execution.
### ODAT
Oracle Database Attacking Tool (`ODAT`) is an open-source penetration testing tool written in Python and designed to enumerate and exploit vulnerabilities in Oracle databases. It can be used to identify and exploit various security flaws in Oracle databases, including SQL injection, remote code execution, and privilege escalation.
### Tips2Hack

1. Nmap
```bash
sudo nmap -p1521 -sV 13.13.13.13 --open
```
2. Nmap - SID Bruteforcing
```bash
sudo nmap -p1521 -sV 13.13.13.13 --open --script oracle-sid-brute
```
3. ODAT
```bash
./odat.py all -s 13.13.13.13
```
4. SQLplus - Log In
```bash
sqlplus george/burger@13.13.13.13/XE
```
5. Oracle RDBMS - Interaction
```bash
SQL> select table_name from all_tables;
SQL> select * from user_role_privs;

USERNAME                       GRANTED_ROLE                   ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
GEORGE                          CONNECT                        NO  YES NO
GEORGE                          RESOURCE                       NO  YES NO
```
6. Oracle RDBMS - Database Enumeration
```bash
sqlplus george/burger@13.13.13.13/XE as sysdba
SQL> select * from user_role_privs;
-------------------------------------------------------------------------
USERNAME                       GRANTED_ROLE                   ADM DEF OS
------------------------------ ------------------------------ --- --- ---
SYS                            ADM_PARALLEL_EXECUTE_TASK      YES YES NO
SYS                            APEX_ADMINISTRATOR_ROLE        YES YES NO
SYS                            AQ_ADMINISTRATOR_ROLE          YES YES NO
SYS                            AQ_USER_ROLE                   YES YES NO
SYS                            AUTHENTICATEDUSER              YES YES NO
SYS                            CONNECT                        YES YES NO
SYS                            CTXAPP                         YES YES NO
SYS                            DATAPUMP_EXP_FULL_DATABASE     YES YES NO
SYS                            DATAPUMP_IMP_FULL_DATABASE     YES YES NO
SYS                            DBA                            YES YES NO
SYS                            DBFS_ROLE                      YES YES
-------------------------------------------------------------------------
```
7. Oracle RDBMS - Extract Password Hashes
```bash
SQL> select name, password from sys.user$;
```
8. Oracle RDBMS - File Upload
```bash
./odat.py utlfile -s 13.13.13.13 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
curl -X GET http://13.13.13.13/testing.txt

Hello There Adventurer!
```
---

## PostgreSQL
<!--- Used https://gist.github.com/Kartones cheetsheet for this Postgres section --->
**Connect to database**
```bash
psql -U postgres
```
### Basic Commands:
- `\?`: Show help
- `\q`: Quit
- `\c __database__`: Connect to a database
- `\d __table__`: Show table definition (columns, etc.) including triggers
- `\d+ __table__`: More detailed table definition including description and physical disk size
- `\l`: List databases
- `\dy`: List events
- `\df`: List functions
- `\di`: List indexes
- `\dn`: List schemas
- `\dt *.*`: List tables from all schemas (if `*.*` is omitted will only show SEARCH_PATH ones)
- `\dT+`: List all data types
- `\dv`: List views
- `\dx`: List all extensions installed
- `\df+ __function__` : Show function SQL code. 
- `\x`: Pretty-format query results instead of the not-so-useful ASCII tables
- `\copy (SELECT * FROM __table_name__) TO 'file_path_and_name.csv' WITH CSV`: Export a table as CSV
- `\des+`: List all foreign servers
- `\dE[S+]`: List all foreign tables
- `\! __bash_command__`: execute `__bash_command__` (e.g. `\! ls`)

#### User Related:
- `\du`: List users
- `\du __username__`: List a username if present.
- `create role __test1__`: Create a role with an existing username.
- `create role __test2__ noinherit login password __passsword__;`: Create a role with username and password.
- `set role __test__;`: Change role for current session to `__test__`.
- `grant __test2__ to __test1__;`: Allow `__test1__` to set its role as `__test2__`.
- `\deu+`: List all user mapping on server
---

## IPMI

**Intelligent Platform Management Interface (IPMI) is a set of standardized specifications for hardware-based host management systems used for system management and monitoring.** It acts as an autonomous subsystem and works independently of the host's BIOS, CPU, firmware, and underlying operating system. IPMI provides sysadmins with the ability to manage and monitor systems even if they are powered off or in an unresponsive state. It operates using a direct network connection to the system's hardware and does not require access to the operating system via a login shell. IPMI communicates over port `623 UDP`. Systems that use the IPMI protocol are called Baseboard Management Controllers (`BMCs`). If we can access a BMC during an assessment, we would gain full access to the host motherboard and be able to monitor, reboot, power off, or even reinstall the host operating system. Gaining access to a BMC is nearly equivalent to physical access to a system.

`IPMI` us typically used in three ways:
- Before the OS has booted to modify BIOS settings
- When the host is fully powered down
- Access to a host after a system failure

When not being used for these tasks, IPMI can monitor a range of different things such as system temperature, voltage, fan status, and power supplies. To function, IPMI requires the following components:

1. **Baseboard Management Controller** (`BMC`) - A micro-controller and essential component of an IPMI
2. **Intelligent Chassis Management** Bus (`ICMB`) - An interface that permits communication from one chassis to another
3. **Intelligent Platform Management Bus** (`IPMB`) - extends the BMC
4. **IPMI Memory** - stores things such as the system event log, repository store data, and more
5. **Communications Interfaces** - local system interfaces, serial and LAN interfaces, ICMB and PCI Management Bus

### IPMI 2.0 RAKP flaw

During the authentication process, the server sends a salted SHA1 or MD5 hash of the user's password to the client before authentication takes place. This can be leveraged to obtain the password hash for ANY valid user account on the BMC. These password hashes can then be cracked offline using a dictionary attack using `Hashcat` mode `7300`. In the event of an HP iLO using a factory default password, we can use this Hashcat mask attack command `hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u` which tries all combinations of upper case letters and numbers for an eight-character password. 

### Default Credentials

|Product|Username|Password|
|-|-|-|
|Dell iDRAC|root|calvin|
|HP iLO|Administrator|randomized 8-character string consisting of numbers and uppercase letters|
|Supermicro IPMI|ADMIN|ADMIN|


### Tips2Hack

1. Nmap
```bash
sudo nmap -sU --script ipmi-version -p 623 ilo.kekmaster.local
```

2. Metasploit Version Scan
```bash
msf6 > use  auxiliary/scanner/ipmi/ipmi_version
msf6 > set rhosts 13.13.13.13
msf6 > run
```

3. Metasploit Dumping Hashes
```bash
msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes 
msf6 > set rhosts 13.13.13.13
msf6 > run
```

---

## R-Services
**R-Services are a suite of services hosted to enable remote access or issue commands between Unix hosts over TCP/IP.** Much like telnet, r-services transmit information from client to server(and vice versa.) over the network in an unencrypted format, making it possible for attackers to intercept network traffic (passwords, login information, etc.) by performing man-in-the-middle (`MITM`) attacks. R-Services mostly using ports `512, 513, 514` and only accessible via suite of programs known as `r-commands`. 
The R-commands suite contains:
- rcp (`remote copy`)
- rexec (`remote execution`)
- rlogin (`remote login`)
- rsh (`remote shell`)
- rstat
- ruptime
- rwho (`remote who`)
### Quick Overview

|Command|Service Daemon|Port|Transport Protocol|Description|
|-|-|-|-|-|
|`rcp`|`rshd`|514|TCP|Copy a file from the local system to remote (or vice versa). Works like `cp` but don't provide warning for overwriting files.|
|`rsh`|`rshd`|514|TCP|Opens a shell on remote machine without login. Relies upon trusted entries in the `/etc/hosts/equiv` and `.rhosts` files for validation|
|`rexec`|`rexecd`|512|TCP|Enables to run shell command on remote machine. Requires authentification with `username:password` or with `/etc/hosts/equiv` and `.rhosts` files |
|`rlogin`|`rlogind`|513|TCP|Enables a user log in to a remote host over the network. Unix-only. Use `/etc/hosts/equiv` and `.rhosts` files to authentification|

### Tips2Hack
1. Logging in Using Rlogin
```bash
rlogin 13.13.13.13 -l htb-student
```
2. Listing Authenticated Users Using Rwho
```bash
rwho
```
3. Listing Authenticated Users Using Rusers
```bash
rusers -al 13.13.13.13
```

---

## RDP
**The Remote Desktop Protocol (RDP) is a protocol developed by Microsoft for remote access to a computer running the Windows operating system. This protocol allows display and control commands to be transmitted via the GUI encrypted over IP networks. Works at `Application Layer` of TCP/IP model, typically using `TCP port 3389`. If Network Address Translation (NAT) is used on the route between client and server, as is often the case with Internet connections, the remote computer needs the public IP address to reach the server. It uses `TLS/SSL`**


### TIps2Hack
1. Nmap
```bash
nmap -sV -sC 13.13.13.13 -p3389 --script rdp*
```
2. [RDP Security Check](https://github.com/CiscoCXSecurity/rdp-sec-check)
```bash
./rdp-sec-check.pl 13.13.13.13
```
3. Initiate an RDP Session via xfreerdp(or Reminna with GUI)
```bash
xfreerdp /u:carnifex17 /p:"S3cr3t!" /v:13.13.13.13 /cert:ignore /d:DOMAIN
```

---

## WinRM

**The Windows Remote Management (WinRM) is a simple Windows integrated remote management protocol based on the command line.** WinRM uses the **Simple Object Access Protocol (`SOAP`)** to establish connections to remote hosts and their applications. WinRM relies on TCP ports `5985` and `5986` for communication, with the last port 5986 using HTTPS. Services like remote sessions using PowerShell and event log merging require WinRM.
### Tips2Hack
1. Nmap WinRM
```bash
nmap -sV -sC 13.13.13.13 -p5985,5986 --disable-arp-ping -n
```
2. Evil-WinRM
```bash
evil-winrm -i 13.13.13.13 -u carnifex17 -p S3cr3t!
```
3. CrackMapExec
```bash
crackmapexec winrm 10.129.42.197 -u user.list -p password.list
```

## WMI
**Windows Management Instrumentation (`WMI`) is Microsoft's implementation and also an extension of the Common Information Model (`CIM`), core functionality of the standardized Web-Based Enterprise Management (`WBEM`) for the Windows platform.** WMI allows read and write access to almost all settings on Windows systems. Mostly uses `TCP port 135`
### Tips2Hack
1. WMIexec.py
```bash
/usr/share/doc/python3-impacket/examples/wmiexec.py carnifex17:"S3cr3t!"@13.13.13.13 "hostname"
```

---

## LDAP
**Lightweight directory access protocol (LDAP) is a protocol that helps users find data about organizations, persons, and more.** LDAP has two main goals: to store data in the LDAP directory and authenticate users to access the directory. It also provides the communication language that applications require to send and receive information from directory services. A directory service provides access to *where* information on organizations, individuals, and other data is located within a network.
### Basic LDAP Components
- `DIT` - Directory Information tree
- `DN` - Distinguished name, which contains a path through the DIT for LDAP to navigate (ex. cn=Susan, ou=users, o=Company)
- `dc` - Domain Access Component - uses DNS mapping to locate Internet domain names and translate them into Ip address. Most users don’t know the domain name and/or IP address of the individual they’re searching for. In this case, LDAP uses the Distinguished Name (DN) assigned to the user as a path to quickly navigate through the DIT and find the search result.
- `o` - o subclass is one of the most general subclasses listed in the DN, and it is usually where LDAP starts when it runs a search
- `ou` - Organizational Unit. Subclass of o. Mostly seen as ou=users or/and ou=group, with each containing a list of user accounts or groups. 
- `cn` - Common Name. Used to identify the name of a group or user account.
