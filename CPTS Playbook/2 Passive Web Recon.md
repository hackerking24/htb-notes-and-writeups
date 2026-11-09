# 2. Passive Web Recon

## Goal

Collect intel without touching the target directly (OSINT, certificate data, archived content).

## Workflow

`# WHOIS & DNS
whois domain.com
dig domain.com ANY +noall +answer
host -t mx domain.com

# Subdomain discovery (passive)
subfinder -d domain.com -all -silent
amass enum -passive -d domain.com
assetfinder --subs-only domain.com

# Certificate transparency
curl -s "https://crt.sh/?q=%25.domain.com&output=json" | jq -r '.[].name_value' | sort -u

# Wayback / archived URLs
waybackurls domain.com | tee wayback.txt
gau domain.com | tee gau.txt
cat wayback.txt | grep -E "\.js$|\.php$|api" | sort -u

# Google dorking
site:domain.com filetype:pdf
site:domain.com inurl:admin
intitle:"index of" site:domain.com`

## Key resources

- Shodan / Censys — `shodan host <ip>`
- theHarvester — `theHarvester -d domain.com -b all`
- GitHub / GitLab dorking — leaked creds, API keys, hostnames
- LinkedIn — username/email format harvesting
- [Hunter.io](http://Hunter.io) / [phonebook.cz](http://phonebook.cz) — email enumeration