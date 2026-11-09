# 15. Linux Privilege Escalation

## Automated enumeration

`./linpeas.sh
./lse.sh -l 2
pspy64`

## Common vectors

`sudo -l
find / -perm -4000 -type f 2>/dev/null
getcap -r / 2>/dev/null`

- SUID/SGID → GTFOBins
- Sudo misconfigs → GTFOBins
- Capabilities (`cap_setuid+ep`)
- Cron/path hijacks
- Writable configs / creds in app dirs
- Docker group → root

## Kernel triage

`uname -a`