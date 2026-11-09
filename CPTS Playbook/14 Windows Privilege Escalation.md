# 14. Windows Privilege Escalation

## Automated enumeration

`winPEAS.exe
PowerUp.ps1; Invoke-AllChecks
Seatbelt.exe -group=all
PrivescCheck.ps1`

## Quick manual wins

`whoami /priv
whoami /groups
systeminfo`

## Common vectors

- SeImpersonate/SeAssignPrimaryToken → Potato family (PrintSpoofer/GodPotato)cmd
- Unquoted service paths
- Weak service permissions
- AlwaysInstallElevated
- Saved creds (`cmdkey /list`)
- GPP passwords in SYSVOL
- Writable scheduled tasks / DLL hijacks

## Kernel exploit triage

`wesng -i systeminfo.txt`