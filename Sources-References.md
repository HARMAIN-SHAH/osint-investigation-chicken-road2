# 📚 Sources & References
### All 13 Documented Sources | chicken-road2.app OSINT Investigation

> Every finding in this investigation is attributed to a specific, verifiable
> public source. An intelligence report without source attribution is opinion — not evidence.

---

## Complete Source Table

| # | Data / Finding | Tool Used | Source URL |
|---|---|---|---|
| 01 | A record: 172.67.137.239 and AAAA records | Python socket module | `socket.getaddrinfo("chicken-road2.app", 443)` — system DNS |
| 02 | SSL certificate — CN, issuer, TLS version, validity dates | Python ssl module | `ssl.create_default_context().wrap_socket()` → www.chicken-road2.app:443 |
| 03 | HTTP response code 403, x-deny-reason header, HTTP/2 | curl | https://www.chicken-road2.app/ |
| 04 | robots.txt — 403 Forbidden status | Python urllib.request | https://www.chicken-road2.app/robots.txt |
| 05 | sitemap.xml — 403 Forbidden status | Python urllib.request | https://www.chicken-road2.app/sitemap.xml |
| 06 | Hosting ISP, NS records, SSL type, IP, Tranco rank, trust score | ScamAdviser | https://scamadviser.com/check-website/chicken-road2.app |
| 07 | WHOIS privacy status — all registrant fields redacted | ScamAdviser | https://scamadviser.com/check-website/chicken-road2.app |
| 08 | GTM tag ID (GTM-W9DD2NF) and Facebook Pixel app_id (380732709336812) | ScamAdviser metadata | https://scamadviser.com/check-website/chicken-road2.app |
| 09 | GitHub org "chickengamegambling", 9+ repos, @reshan3812 identity link | GitHub | https://github.com/chickengamegambling |
| 10 | Bonus code CHICKEN, partner casinos, URL path schema, RTP 95.5% | GitHub README | https://github.com/chickengamegambling/chicken-road-2 |
| 11 | Game developer InOut Games, Curaçao License No. 1668/JAZ | GitHub README | https://github.com/chickengamegambling/chicken-road-2 |
| 12 | Facebook page, LinkedIn company, Twitter handle | GitHub org profile | https://github.com/chickengamegambling |
| 13 | User reviews, non-payment complaints | Trustpilot | https://uk.trustpilot.com/review/chickenroad-2.app |

---

## Tools Reference

| Tool | Type | Cost | URL |
|---|---|---|---|
| Python socket module | DNS resolver | Free (built-in) | docs.python.org/3/library/socket.html |
| Python ssl module | TLS inspector | Free (built-in) | docs.python.org/3/library/ssl.html |
| Python urllib.request | HTTP client | Free (built-in) | docs.python.org/3/library/urllib.request.html |
| curl | HTTP scanner | Free (CLI tool) | curl.se |
| ScamAdviser | OSINT platform | Free (basic) | scamadviser.com |
| GitHub | Code repository | Free | github.com |
| Trustpilot | Review platform | Free | trustpilot.com |

---

## Additional OSINT Tools Recommended for Extended Investigation

These tools were not used in this investigation but are recommended for follow-up:

| Tool | Purpose | URL |
|---|---|---|
| VirusTotal | Domain / URL / file reputation | virustotal.com |
| urlscan.io | Live URL sandbox and screenshot | urlscan.io |
| MXToolbox | SPF/DKIM/DMARC and blacklist check | mxtoolbox.com |
| crt.sh | Certificate transparency log search | crt.sh |
| AbuseIPDB | IP reputation and abuse reports | abuseipdb.com |
| Shodan | Internet-connected device search | shodan.io |
| Censys | Certificate and host search engine | search.censys.io |
| Wayback Machine | Historical website snapshots | web.archive.org |
| who.is | WHOIS lookup | who.is |

---

## Investigation Methodology Note

This investigation used **passive OSINT techniques only**. Passive OSINT means:

✅ **Allowed:**
- DNS queries (public record)
- SSL/TLS certificate inspection (publicly exposed)
- HTTP header requests (publicly accessible)
- Reading public GitHub repositories
- Reading public review sites and trust databases
- Any information publicly indexed by search engines

❌ **Not used:**
- Active port scanning
- Vulnerability scanning
- Exploitation of any kind
- Accessing any non-public or restricted data
- Sending more requests than a normal browser would

---

*Investigation by: Harmain Shah | Intern ID: CA0200 | Cryptonic Area Internship Program*
*Date: 22 July 2026 | Method: Passive OSINT only | Educational purposes*
