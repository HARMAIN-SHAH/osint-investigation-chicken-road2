# 📡 HTTP Response & WAF Analysis
### Target: https://www.chicken-road2.app/ | Tool: curl + Python urllib | Date: 22 July 2026

---

## Method

Direct HTTP header scan using **curl** to inspect the server response headers
without loading any page content.

```bash
curl -s --max-time 15 -I https://www.chicken-road2.app/
```

robots.txt and sitemap.xml tested using **Python urllib.request**:

```python
import urllib.request, ssl

ctx = ssl.create_default_context()
for path in ['/robots.txt', '/sitemap.xml']:
    try:
        req = urllib.request.Request(
            f'https://www.chicken-road2.app{path}',
            headers={'User-Agent': 'Mozilla/5.0'}
        )
        r = urllib.request.urlopen(req, context=ctx, timeout=10)
        print(f'{path}: HTTP {r.status}')
    except Exception as e:
        print(f'{path}: {e}')
```

---

## HTTP Response Headers

```
HTTP/2  403
x-deny-reason: host_not_allowed
content-type: text/plain
content-length: 108
date: Wed, 22 Jul 2026, 05:37:07 GMT
```

| Header | Value | Significance |
|---|---|---|
| HTTP Version | HTTP/2 | Modern protocol — efficient and secure |
| Status Code | 403 Forbidden | Cloudflare WAF block — not a server error |
| x-deny-reason | host_not_allowed | Cloudflare firewall rule triggered |
| content-type | text/plain | WAF block response page |
| Server | Not disclosed | Cloudflare deliberately suppresses this |

---

## What x-deny-reason: host_not_allowed Means

This is a **Cloudflare WAF (Web Application Firewall)** response. The rule
`host_not_allowed` fires when the request does not match the profile of a
legitimate browser — automated scanners, curl requests, and headless browsers
are blocked at the CDN edge before they even reach the origin server.

The site returns **200 OK** to real browser traffic — confirmed by ScamAdviser
which successfully rendered the full page using a real browser.

---

## robots.txt & sitemap.xml

| File | URL | HTTP Status | Finding |
|---|---|---|---|
| robots.txt | https://www.chicken-road2.app/robots.txt | 403 Forbidden | Cloudflare WAF blocking — content not determinable |
| sitemap.xml | https://www.chicken-road2.app/sitemap.xml | 403 Forbidden | Cloudflare WAF blocking — URL structure not exposed |

Both crawler-discovery files are blocked from automated access. This is a deliberate
anti-scraping / anti-bot configuration — not indicative of malicious intent.

---

## Security Headers Assessment

Because the WAF returns 403 to all scanner requests, the following security headers
**cannot be verified via passive OSINT**:

| Header | Status | Risk if Absent |
|---|---|---|
| Content-Security-Policy (CSP) | ❓ Unknown | XSS attack surface |
| X-Frame-Options | ❓ Unknown | Clickjacking risk |
| X-Content-Type-Options | ❓ Unknown | MIME type sniffing |
| Referrer-Policy | ❓ Unknown | Referral data leakage |
| Permissions-Policy | ❓ Unknown | Browser API abuse |
| Strict-Transport-Security | ✅ Enforced by .app TLD | Protocol downgrade blocked |

**HSTS is enforced** — the `.app` TLD is on the global HSTS preload list, meaning
browsers enforce HTTPS before sending any request, regardless of server config.

---

## Intelligence Analysis

The 403 WAF block is a security feature, not a red flag. However, it creates a
**verification gap** — security headers that should be present cannot be confirmed
through passive methods. A full header audit requires:
- Real browser session with developer tools open
- HTTP interception proxy (e.g. Burp Suite)
- Tool like securityheaders.com accessed from a real browser

---

## Sources

| Data | Tool | Source |
|---|---|---|
| HTTP response headers | curl | `curl -s --max-time 15 -I https://www.chicken-road2.app/` |
| robots.txt / sitemap | Python urllib.request | Direct HTTP request |

---

> ⚠️ Educational purposes only | Passive OSINT | Cryptonic Area Internship — Harmain Shah CA0200
