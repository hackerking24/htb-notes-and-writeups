# 3. Active Web Recon

## Subdomain bruteforce

`ffuf -w subdomains.txt -u http://domain.com -H "Host: FUZZ.domain.com" -fs <baseline_size>
gobuster vhost -u http://domain.com -w subdomains.txt --append-domain`

## Directory & file discovery

`# Directory brute
feroxbuster -u http://<ip> -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php,html,txt -d 3

ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt 
  -u http://<ip>/FUZZ -e .php,.txt,.bak,.zip -recursion -mc 200,301,302,403

gobuster dir -u http://<ip> -w raft-medium-words.txt -x php,html,bak,old,txt -t 50`

## Parameter & endpoint discovery

`# Hidden parameters
arjun -u http://<ip>/page.php
ffuf -w params.txt -u "http://<ip>/page.php?FUZZ=test" -fs <size>

# Crawl
katana -u http://<ip> -jc -d 3 -o endpoints.txt
hakrawler -url http://<ip> -depth 3

# JS analysis for endpoints/secrets
cat endpoints.txt | grep '\.js' | while read u; do curl -s "$u"; done | grep -oE '"[a-zA-Z0-9_/.-]+"'`

## Virtual hosts & headers

`curl -sI http://<ip>                      # response headers
whatweb -a 3 http://<ip>
# Always check /robots.txt /sitemap.xml /.git/ /.svn/ /backup/ /.env`