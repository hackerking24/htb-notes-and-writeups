# 20. Reporting & Documentation

## Throughout the engagement

- Screenshot each key step (shells, privesc, flags) with IP + timestamp visible
- Log commands (`script engagement.log`, terminal logging, tmux logging)
- Track per host: IP/hostname/OS/ports/creds/exploit/access/flags
- Maintain a creds table: user/hash/plaintext/source/where it works

## CPTS report structure (HTB)

1. Executive summary
2. Scope (assets, dates, RoE)
3. Attack path narrative (chronological chain)
4. Findings (per vuln: repro + impact + remediation)
5. Appendices (logs, evidence, methodology)

## Severity rating (CVSS 3.1)

| **Severity** | **CVSS** |
| --- | --- |
| Critical | 9.0–10.0 |
| High | 7.0–8.9 |
| Medium | 4.0–6.9 |
| Low | 0.1–3.9 |
| Info | 0.0 |

## Tools

- SysReptor (HTB-recommended)
- Ghostwriter / PwnDoc