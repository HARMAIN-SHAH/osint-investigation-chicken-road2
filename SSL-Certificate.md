# 🔒 SSL / TLS Certificate Analysis
### Target: www.chicken-road2.app:443 | Tool: Python ssl module | Date: 22 July 2026

---

## Method

SSL certificate data was retrieved via a **direct Python TLS handshake** — connecting
directly to the target server on port 443 and extracting the X.509 certificate without
relying on any third-party scanner.

```python
import ssl, socket

ctx = ssl.create_default_context()
conn = ctx.wrap_socket(socket.socket(), server_hostname='www.chicken-road2.app')
conn.settimeout(10)
conn.connect(('www.chicken-road2.app', 443))
cert = conn.getpeercert()

print('Subject:', cert.get('subject'))
print('Issuer:', cert.get('issuer'))
print('Valid From:', cert.get('notBefore'))
print('Valid Until:', cert.get('notAfter'))
print('SANs:', cert.get('subjectAltName'))
conn.close()
```

---

## Certificate Details

| SSL Field | Value | Notes |
|---|---|---|
| **Common Name (CN)** | `*.chicken-road2.app` | Wildcard — covers all subdomains |
| **Subject Alt Name** | `DNS: www.chicken-road2.app` | Confirmed scope |
| **Certificate Issuer** | Google Trust Services | Legitimate, globally trusted CA |
| **Certificate Type** | Domain Validated (DV SSL) | Domain ownership confirmed only |
| **Valid From** | 22 July 2026, 05:36:07 UTC | Current certificate start |
| **Valid Until** | 21 August 2026, 05:37:07 UTC | 30-day lifespan |
| **TLS Protocol** | TLS 1.3 | Latest standard — strong encryption |
| **Certificate Version** | X.509 v3 | Standard format |
| **Key Coverage** | All `*.chicken-road2.app` | Entire domain covered |

---

## Certificate Type Explanation

### Domain Validated (DV) SSL
A DV certificate confirms **only** that the applicant had control over the domain
at the time of issuance. It does **NOT** verify:
- The legal name of the organisation
- Company registration number
- Physical address
- Whether the business is legitimate

### Comparison

| Type | What It Verifies | Trust Level |
|---|---|---|
| DV (Domain Validated) | Domain control only | Basic |
| OV (Organisation Validated) | Domain + legal org identity | Medium |
| EV (Extended Validation) | Domain + org + strict vetting | High |

chicken-road2.app uses DV — the minimum tier. This is normal for affiliate/content
sites but provides no org-level identity assurance.

---

## 30-Day Auto-Renewal

The 30-day validity period is standard for certificates managed via:
- Cloudflare's automated TLS management
- Google Certificate Manager
- Let's Encrypt (90-day with auto-renew)

This is not a security concern — it indicates automated certificate lifecycle management.

---

## Intelligence Analysis

The DV wildcard certificate covers the entire `*.chicken-road2.app` domain space,
meaning any subdomain (api.chicken-road2.app, admin.chicken-road2.app, etc.) would
be covered by the same certificate without requiring additional cert issuance.

The use of Google Trust Services as the CA is consistent with Cloudflare's certificate
management infrastructure.

---

## Source

| Data | Tool | Method |
|---|---|---|
| Full certificate details | Python ssl module | `ssl.create_default_context().wrap_socket()` → port 443 |

---

> ⚠️ Educational purposes only | Passive OSINT | Cryptonic Area Internship — Harmain Shah CA0200
