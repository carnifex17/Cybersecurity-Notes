---
# Password Attacks
---
## Credential Storage
### Linux Shadow File
- **/etc/shadows structure**

|`guest:`|`$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:`|`18955:`|`0:`|`99999:`|`7:`|`:`|`:`|`:`|
|-|-|-|-|-|-|-|-|-|
|`<username>:`|`<encrypted password>:`|`<day of last change>:`|`<min age>:`|`<max age>:`|`<warning period>:`|`<inactivity period>:`|`<expiration date>:`|`<reserved field>`|

## John The Ripper
**`John the Ripper (JTR or john)` is an essential pentesting tool used to check the strength of passwords and crack encrypted (or hashed) passwords using either brute force or dictionary attacks. It is open-source software initially developed for UNIX-based systems and first released in 1996.**
### Cracking Modes
- **Single Crack Mode** is one of the most common John modes used when attempting to crack passwords using a single password list. It is a brute-force attack which use single password list, meaning all passwords on the list are tried, one by one, until the correct one is found.
```bash
$ john --format=sha256 hashes_to_crack.txt
```
- **Wordlist Mode** is used to crack passwords using multiple lists of words. It is a dictionary attack which means it will try all the words in the lists one by one until it finds the right one. It is almost same with Single Crack Mode, just uses custom wordlists.
```bash
$ john --wordlist=<wordlist_file> --rules <hash_file>
```
- **Incremental Mode** is an advanced John mode used to crack passwords using a character set. It is a hybrid attack, which means it will attempt to match the password by trying all possible combinations of characters from the character set. 
```bash
$ john --incremental <hash_file>
```
- **Cracking Files**
```bash
<tool> <file_to_crack> > file.hash
$ pdf2john server_doc.pdf > server_doc.hash
$ john server_doc.hash
$ john --wordlist=<wordlist.txt> server_doc.hash 
```



