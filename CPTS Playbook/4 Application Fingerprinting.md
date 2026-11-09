# 4. Application Fingerprinting

## Tech stack ID

`whatweb http://<ip>
wappalyzer (browser ext / wappalyzer CLI)
nuclei -u http://<ip> -t technologies/
httpx -u http://<ip> -title -tech-detect -status-code -web-server`

## Manual indicators

- Headers: `Server`, `X-Powered-By`, `X-AspNet-Version`, `Set-Cookie`
- Cookie → framework hints:
    - `JSESSIONID` → Java/Tomcat
    - `PHPSESSID` → PHP
    - `ASP.NET_SessionId` → IIS/.NET
    - `laravel_session` → Laravel
    - `connect.sid` → Node/Express
- Favicon hash pivot:

`curl -s http://<ip>/favicon.ico | md5sum
# Or shodan: http.favicon.hash:<murmur3hash>`

- Error pages/default pages reveal version
- CMS detection:

`cmseek -u http://<ip>
wpscan --url http://<ip> --enumerate
joomscan -u http://<ip>
droopescan scan drupal -u http://<ip>`

## Version-to-exploit pivot

`searchsploit <product> <version>
nuclei -u http://<ip> -t cves/ -severity critical,high`