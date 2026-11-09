# Abducted

sudo nmap -sCV 10.129.10.77
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-05 21:32 EDT
Nmap scan report for 10.129.10.77
Host is up (0.016s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
139/tcp open  netbios-ssn Samba smbd 4
445/tcp open  netbios-ssn Samba smbd 4
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|*nbstat: NetBIOS name: ABDUCTED, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-time:
|   date: 2026-06-06T01:32:30
|*  start_date: N/A
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at [https://nmap.org/submit/](https://nmap.org/submit/) .
Nmap done: 1 IP address (1 host up) scanned in 12.43 seconds
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-coreioznzy]─[~]
└──╼ [★]$ sudo nmap -sU --top-ports 50 10.129.10.77
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-05 21:33 EDT
Nmap scan report for 10.129.10.77
Host is up (0.014s latency).
Not shown: 47 closed udp ports (port-unreach)
PORT    STATE         SERVICE
68/udp  open|filtered dhcpc
137/udp open          netbios-ns
138/udp open|filtered netbios-dgm

cme smb 10.129.10.77 -u '' -p '’

SMB         10.129.10.77    445    ABDUCTED         [*] Unix - Samba (name:ABDUCTED) (domain:ABDUCTED) (signing:False) (SMBv1:None) (Null Auth:True)
SMB         10.129.10.77    445    ABDUCTED         [+] ABDUCTED\:

cme smb 10.129.10.77 -u '' -p '' --shares
SMB         10.129.10.77    445    ABDUCTED         [*] Unix - Samba (name:ABDUCTED) (domain:ABDUCTED) (signing:False) (SMBv1:None) (Null Auth:True)
SMB         10.129.10.77    445    ABDUCTED         [+] ABDUCTED\:
SMB         10.129.10.77    445    ABDUCTED         [*] Enumerated shares
SMB         10.129.10.77    445    ABDUCTED         Share           Permissions     Remark
SMB         10.129.10.77    445    ABDUCTED         -----           -----------     ------
SMB         10.129.10.77    445    ABDUCTED         HP-Reception    WRITE           Reception printer
SMB         10.129.10.77    445    ABDUCTED         projects                        Hartley Group Project Files
SMB         10.129.10.77    445    ABDUCTED         transfer                        Staff file transfer
SMB         10.129.10.77    445    ABDUCTED         IPC$                            IPC Service (Hartley Group Document Services)

nbtscan 10.129.10.77/30 -v
Doing NBT name scan for addresses from 10.129.10.77/30

NetBIOS Name Table for Host 10.129.10.77:

## Incomplete packet, 191 bytes long.
Name Service Type

ABDUCTED         <00>             UNIQUE
ABDUCTED         <03>             UNIQUE
ABDUCTED         <20>             UNIQUE
WORKGROUP        <00>              GROUP
WORKGROUP        <1e>              GROUP

Adapter address: 00:00:00:00:00:00

enum4linux-ng 10.129.10.77
ENUM4LINUX - next generation (v1.3.10)

# ==========================
| Target Information |

[*] Target ........... 10.129.10.77
[*] Username ......... ''
[*] Random Username .. 'xypjkhki'
[*] Password ......... ''
[*] Timeout .......... 10 second(s)

# =====================================
| Listener Scan on 10.129.10.77 |

[*] Checking LDAP
[-] Could not connect to LDAP on 389/tcp: connection refused
[*] Checking LDAPS
[-] Could not connect to LDAPS on 636/tcp: connection refused
[*] Checking SMB
[+] SMB is accessible on 445/tcp
[*] Checking SMB over NetBIOS
[+] SMB over NetBIOS is accessible on 139/tcp

# ===========================================================
| NetBIOS Names and Workgroup/Domain for 10.129.10.77 |

[+] Got domain/workgroup name: WORKGROUP
[+] Full NetBIOS names information:

- ABDUCTED <00> - B <ACTIVE> Workstation Service
- ABDUCTED <03> - B <ACTIVE> Messenger Service
- ABDUCTED <20> - B <ACTIVE> File Server Service
- WORKGROUP <00> - <GROUP> B <ACTIVE> Domain/Workgroup Name
- WORKGROUP <1e> - <GROUP> B <ACTIVE> Browser Service Elections
- MAC Address = 00-00-00-00-00-00

# =========================================
| SMB Dialect Check on 10.129.10.77 |

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
SMB signing required: false

# ===========================================================
| Domain Information via SMB session for 10.129.10.77 |

[*] Enumerating via unauthenticated SMB session on 445/tcp
[+] Found domain information via SMB
NetBIOS computer name: ABDUCTED
NetBIOS domain name: ''
DNS domain: ''
FQDN: abducted
Derived membership: workgroup member
Derived domain: unknown

# =========================================
| RPC Session Check on 10.129.10.77 |

[*] Check for anonymous access (null session)
[+] Server allows authentication via username '' and password ''
[*] Check for guest access
[+] Server allows authentication via username 'xypjkhki' and password ''
[H] Rerunning enumeration with user 'xypjkhki' might give more results

# ===================================================
| Domain Information via RPC for 10.129.10.77 |

[+] Domain: WORKGROUP
[+] Domain SID: NULL SID
[+] Membership: workgroup member

# ===============================================
| OS Information via RPC for 10.129.10.77 |

[*] Enumerating via unauthenticated SMB session on 445/tcp
[+] Found OS information via SMB
[*] Enumerating via 'srvinfo'
[+] Found OS information via 'srvinfo'
[+] After merging OS information we have the following result:
OS: Windows 7, Windows Server 2008 R2
OS version: '6.1'
OS release: ''
OS build: '0'
Native OS: not supported
Native LAN manager: not supported
Platform id: '500'
Server type: '0x809a03'
Server type string: Wk Sv PrQ Unx NT SNT Hartley Group Document Services

# =====================================
| Users via RPC on 10.129.10.77 |

[*] Enumerating users via 'querydispinfo'
[+] Found 1 user(s) via 'querydispinfo'
[*] Enumerating users via 'enumdomusers'
[+] Found 1 user(s) via 'enumdomusers'
[+] After merging user results we have 1 user(s) total:
'1000':
username: scott
name: Scott Mercer
acb: '0x00000010'
description: ''

# ======================================
| Groups via RPC on 10.129.10.77 |

[*] Enumerating local groups
[+] Found 0 group(s) via 'enumalsgroups domain'
[*] Enumerating builtin groups
[+] Found 0 group(s) via 'enumalsgroups builtin'
[*] Enumerating domain groups
[+] Found 0 group(s) via 'enumdomgroups'

# ======================================
| Shares via RPC on 10.129.10.77 |

[*] Enumerating shares
[+] Found 4 share(s):
HP-Reception:
comment: Reception printer
type: Printer
IPC$:
comment: IPC Service (Hartley Group Document Services)
type: IPC
projects:
comment: Hartley Group Project Files
type: Disk
transfer:
comment: Staff file transfer
type: Disk
[*] Testing share HP-Reception
[+] Mapping: OK, Listing: NOT SUPPORTED
[*] Testing share IPC$
[+] Mapping: OK, Listing: NOT SUPPORTED
[*] Testing share projects
[+] Mapping: DENIED, Listing: N/A
[*] Testing share transfer
[+] Mapping: DENIED, Listing: N/A

# =========================================
| Policies via RPC for 10.129.10.77 |

[*] Trying port 445/tcp
[+] Found policy:
Domain password information:
Password history length: None
Minimum password length: 5
Minimum password age: none
Maximum password age: 49710 days (136 years) 6 hours 21 minutes
Password properties:

- DOMAIN_PASSWORD_COMPLEX: false
- DOMAIN_PASSWORD_NO_ANON_CHANGE: false
- DOMAIN_PASSWORD_NO_CLEAR_CHANGE: false
- DOMAIN_PASSWORD_LOCKOUT_ADMINS: false
- DOMAIN_PASSWORD_PASSWORD_STORE_CLEARTEXT: false
- DOMAIN_PASSWORD_REFUSE_PASSWORD_CHANGE: false
Domain lockout information:
Lockout observation window: 30 minutes
Lockout duration: 30 minutes
Lockout threshold: None
Domain logoff information:
Force logoff time: 49710 days (136 years) 6 hours 21 minutes

# =========================================
| Printers via RPC for 10.129.10.77 |

[+] Found 1 printer(s):
\\10.129.10.77\:
description: \\10.129.10.77\,,Reception printer
comment: Reception printer
flags: '0x800000'

found user scott