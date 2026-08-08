# 🏠 Hosting Provider & IP Geolocation
### Target: chicken-road2.app | Sources: DNS Resolution + ScamAdviser | Date: 22 July 2026

---

## Resolved IP Addresses

Both IP addresses returned by DNS were cross-referenced against ASN databases
via ScamAdviser infrastructure data.

### IP 1 — 172.67.137.239

| Field | Value |
|---|---|
| IP Address | 172.67.137.239 |
| Organisation | Cloudflare, Inc. |
| ASN Number | AS13335 |
| ASN Name | CLOUDFLARENET |
| Country | United States |
| City | San Francisco, CA |
| Node Type | Anycast CDN Edge Node |
| Role | Primary endpoint |
| Origin Server | Concealed behind CDN |

### IP 2 — 104.21.38.193

| Field | Value |
|---|---|
| IP Address | 104.21.38.193 |
| Organisation | Cloudflare, Inc. |
| ASN Number | AS13335 |
| ASN Name | CLOUDFLARENET |
| Country | United States |
| City | San Francisco, CA |
| Node Type | Anycast CDN Edge Node |
| Role | Secondary / failover endpoint |
| Origin Server | Concealed behind CDN |

---

## What is Anycast?

Anycast is a network routing method where **multiple servers worldwide share the
same IP address**. When a user connects to 172.67.137.239, they are actually routed
to the nearest Cloudflare data centre geographically — not necessarily one in the US.

**This means:**
- The IP address tells us the CDN operator (Cloudflare) but NOT the hosting location
- The origin server could be hosted anywhere in the world
- Passive OSINT cannot determine the true hosting provider or country

---

## Cloudflare as Reverse Proxy

```
User Browser
     │
     ▼
Cloudflare Edge Node (172.67.137.239 or 104.21.38.193)
     │  ← SSL termination here
     │  ← WAF filtering here
     │  ← DDoS protection here
     ▼
[ORIGIN SERVER — IP UNKNOWN]
     │
     ▼
Web Application (chicken-road2.app content)
```

Cloudflare acts as a **reverse proxy** — it sits between the user and the origin server,
handling SSL, caching, WAF filtering, and DDoS protection. The origin server's IP is
never exposed to the public.

---

## Origin IP Discovery (Active Techniques — Out of Scope)

To find the origin server IP, the following active techniques could be used
(outside the scope of this passive OSINT investigation):

| Technique | Tool | Method |
|---|---|---|
| Certificate Transparency | crt.sh | Find pre-Cloudflare SSL certs with origin hostname |
| Historical DNS | SecurityTrails, VirusTotal | Check DNS records before Cloudflare was added |
| Shodan | shodan.io | Search for TLS cert matching *.chicken-road2.app |
| Mail Server IP | MX record lookup | Mail servers sometimes bypass CDN |

---

## Sources

| Data | Tool | Source |
|---|---|---|
| IP addresses | Python socket.getaddrinfo() | Direct DNS resolution |
| ASN, organisation, hosting | ScamAdviser | scamadviser.com/check-website/chicken-road2.app |

---

> ⚠️ Educational purposes only | Passive OSINT | Cryptonic Area Internship — Harmain Shah CA0200
