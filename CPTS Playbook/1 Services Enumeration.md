# 1. Services Enumeration

## Initial host discovery

`# Ping sweep
fping -asgq 10.10.10.0/24
nmap -sn 10.10.10.0/24 -oA hosts

# If ICMP blocked
nmap -sn -PS22,80,443,445,3389 10.10.10.0/24`

## Port scanning workflow

`# Fast full TCP sweep first
nmap -p- --min-rate 10000 -T4 10.10.10.10 -oA allports

# Pull open ports into a variable
ports=$(grep open allports.nmap | cut -d/ -f1 | tr '\n' ',' | sed 's/,$//')

# Deep scan on open ports
nmap -p$ports -sCV -A -oA deep 10.10.10.10

# UDP top ports (slow, run in background)
sudo nmap -sU --top-ports 100 -oA udp 10.10.10.10`

## Per-service enumeration reference

`# FTP (21)
nmap --script ftp-anon,ftp-syst -p21 <ip>
ftp <ip>            # try anonymous:anonymous

# SSH (22)
nmap --script ssh2-enum-algos,ssh-auth-methods -p22 <ip>
ssh-audit <ip>

# SMTP (25)
nmap --script smtp-commands,smtp-enum-users -p25 <ip>
smtp-user-enum -M VRFY -U users.txt -t <ip>

# DNS (53)
dig axfr @<ip> domain.local           # zone transfer
dnsenum domain.local
nslookup -> server <ip> -> domain

# Kerberos (88) -> AD present, jump to AD section

# POP3/IMAP (110/143)
nmap --script pop3-capabilities,imap-capabilities -p110,143 <ip>

# RPC (135)
rpcdump.py <ip>
rpcclient -U "" -N <ip>

# SMB (139/445)
nmap --script smb-os-discovery,smb-enum-shares,smb-enum-users -p445 <ip>
smbclient -L //<ip> -N
crackmapexec smb <ip> -u '' -p '' --shares
enum4linux-ng -A <ip>
smbmap -H <ip> -u null

# SNMP (161 UDP)
snmpwalk -v2c -c public <ip>
onesixtyone -c community.txt <ip>
snmpbulkwalk -c public -v2c <ip>

# LDAP (389/636)
nmap --script ldap-rootdse -p389 <ip>
ldapsearch -x -H ldap://<ip> -s base namingcontexts
ldapsearch -x -H ldap://<ip> -b "DC=domain,DC=local"

# MSSQL (1433)
nmap --script ms-sql-info,ms-sql-empty-password -p1433 <ip>
mssqlclient.py user:pass@<ip>

# Oracle (1521)
odat all -s <ip>

# NFS (2049)
showmount -e <ip>
mount -t nfs <ip>:/share /mnt/nfs

# MySQL (3306)
mysql -h <ip> -u root -p

# RDP (3389)
nmap --script rdp-ntlm-info,rdp-enum-encryption -p3389 <ip>
xfreerdp /v:<ip> /u:user /p:pass

# WinRM (5985/5986)
crackmapexec winrm <ip> -u user -p pass
evil-winrm -i <ip> -u user -p pass

# Redis (6379)
redis-cli -h <ip>

# VNC (5900)
nmap --script vnc-info -p5900 <ip>`