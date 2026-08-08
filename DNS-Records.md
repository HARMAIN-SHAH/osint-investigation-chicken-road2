# 🌐 DNS Records & IP Resolution
### Target: chicken-road2.app | Tool: Python socket module | Date: 22 July 2026

---

## Method

DNS enumeration was performed using Python's built-in `socket.getaddrinfo()` function
querying the system DNS resolver directly — no third-party DNS tool required.

```python
import socket

# A / AAAA record resolution
info = socket.getaddrinfo('chicken-road2.app', 443)
for result in info:
    print(result)

# Quick A record
print(socket.gethostbyname('chicken-road2.app'))
# Output: 172.67.137.239
```

---

## Results

### A Records (IPv4)

| IP Address | Organisation | ASN | Type |
|---|---|---|---|
| `172.67.137.239` | Cloudflare, Inc. | AS13335 — CLOUDFLARENET | Primary anycast endpoint |
| `104.21.38.193` | Cloudflare, Inc. | AS13335 — CLOUDFLARENET | Secondary anycast endpoint |

### AAAA Records (IPv6)

| IP Address | Organisation | Type |
|---|---|---|
| `2606:4700:3030::ac43:89ef` | Cloudflare, Inc. | IPv6 primary |
| `2606:4700:3034::6815:26c1` | Cloudflare, Inc. | IPv6 secondary |

### NS Records (Nameservers)

| Nameserver | Provider | Source |
|---|---|---|
| `autumn.ns.cloudflare.com` | Cloudflare, Inc. | ScamAdviser infrastructure data |
| `denver.ns.cloudflare.com` | Cloudflare, Inc. | ScamAdviser infrastructure data |

### SSL Common Name (from DNS perspective)

| Record | Value | Notes |
|---|---|---|
| SSL CN | `*.chicken-road2.app` | Wildcard — covers all subdomains |

---

## Intelligence Analysis

**All four IP addresses belong to Cloudflare's anycast network (ASN 13335 — CLOUDFLARENET).**

This confirms the site is deployed behind Cloudflare CDN as a reverse proxy. The real
origin server — the physical machine hosting the web application — is not exposed to
the public internet and cannot be determined through passive DNS enumeration alone.

**What this means:**
- Direct DDoS attacks against the origin server are prevented
- The real hosting provider and server location are unknown via passive OSINT
- Active techniques (crt.sh certificate transparency, historical DNS, Shodan) would
  be required to discover the origin IP

**Dual-stack support confirmed:** Both IPv4 and IPv6 addresses are present, indicating
a modern, properly configured infrastructure deployment.

---

## Source

| Data | Source |
|---|---|
| A/AAAA records | `python3 -c "import socket; print(socket.getaddrinfo('chicken-road2.app', 443))"` |
| NS records | ScamAdviser — scamadviser.com/check-website/chicken-road2.app |

---

> ⚠️ Educational purposes only | Passive OSINT | Cryptonic Area Internship — Harmain Shah CA0200
