# 🚨 Security Observations
### Target: chicken-road2.app | 7 Findings | Date: 22 July 2026

---

## OBS-01 — WHOIS Registrant Identity Fully Concealed
**Severity:** 🟡 MEDIUM

The domain operator behind chicken-road2.app has activated a full WHOIS privacy
service. Every registrant field — name, email address, organisation, country,
creation date, and expiry date — is redacted from the public record.

**Why this matters:**
- No public accountability for the entity operating this site
- Users cannot identify who is legally responsible for the content
- Regulatory authorities face additional steps to identify the operator

**Evidence:** ScamAdviser WHOIS lookup — all fields returned as REDACTED FOR PRIVACY

**Attribution Lead Found:** GitHub account @reshan3812 linked to the
chickengamegambling organisation — the only public thread to the registrant.

**Source:** scamadviser.com/check-website/chicken-road2.app

---

## OBS-02 — DV SSL Certificate — No Organisation Verification
**Severity:** 🟢 LOW

The SSL certificate is Domain Validated (DV) — the lowest tier of SSL verification.
It confirms that the certificate applicant controlled the domain at issuance but
does NOT verify the legal name, company registration, or address of the operator.

**Why this matters:**
- A fraudulent actor could obtain the same certificate type
- The green padlock in a browser does NOT mean the site is trustworthy
- OV or EV certificates would provide stronger identity assurance

**Evidence:** Python ssl module — direct TLS handshake to www.chicken-road2.app:443

**Mitigating Factor:** 30-day auto-renewal is standard for cloud-managed TLS.
Google Trust Services is a legitimate, widely trusted CA.

**Source:** `ssl.create_default_context().wrap_socket()` → port 443

---

## OBS-03 — Real Origin Server IP Concealed by Cloudflare
**Severity:** 🟢 LOW

All DNS queries for chicken-road2.app return Cloudflare anycast IP addresses.
The actual web server hosting the site is not determinable through passive OSINT.

**Why this matters:**
- Intelligence gap — hosting provider and country unknown
- Cannot assess origin server security posture via passive methods
- Active techniques (crt.sh, Shodan) would be required for origin discovery

**Evidence:** Python socket.getaddrinfo() — both IPs resolve to Cloudflare AS13335

**Note:** This is a legitimate and widely adopted security configuration.
It also protects the origin server from direct DDoS attacks.

**Source:** DNS resolution + ScamAdviser ASN data

---

## OBS-04 — Security Headers Not Verifiable — Cloudflare WAF Active
**Severity:** 🟡 MEDIUM

The Cloudflare WAF blocks all automated scanner requests with a 403 Forbidden
response (x-deny-reason: host_not_allowed). This prevents verification of critical
security headers including Content-Security-Policy, X-Frame-Options, and Referrer-Policy.

**Why this matters:**
- Cannot confirm whether XSS, clickjacking, or MIME protections are in place
- A full security audit requires real browser session or proxy tool

**Evidence:** `curl -s --max-time 15 -I https://www.chicken-road2.app/`
→ HTTP/2 403, x-deny-reason: host_not_allowed

**Mitigating Factor:** The `.app` TLD enforces HSTS preloading — protocol
downgrade attacks are blocked by default.

**Source:** curl HTTP scan

---

## OBS-05 — Public GitHub Repositories Expose Full Site Architecture
**Severity:** 🟡 MEDIUM

Nine public GitHub repositories under the "chickengamegambling" organisation
contain the complete source code for every language version of the affiliate site.

**What is publicly exposed:**
- All URL path structures for 8 language deployments
- Affiliate bonus code "CHICKEN" (100% match up to €4,500)
- Partner casino referral links and relationships
- Full SEO keyword strategy
- InOut Games API integration details
- GitHub handle @reshan3812 as a deanonymisation lead

**Why this matters:**
- An attacker could audit git commit history for accidentally committed credentials
- Competitors can replicate the entire affiliate strategy
- WHOIS privacy becomes partially ineffective due to GitHub identity exposure

**Evidence:** github.com/chickengamegambling — 9+ public repos, all publicly indexed

**Source:** github.com/chickengamegambling

---

## OBS-06 — Gambling Affiliate — Regulatory & Legal Risk
**Severity:** 🔴 HIGH

The site operates as an affiliate promoting casino gambling. This is a heavily
regulated or outright prohibited activity in many jurisdictions.

**Key facts:**
- Promoted game operates under Curaçao eGaming License 1668/JAZ
- Curaçao provides limited consumer protections vs MGA or UKGC
- Trustpilot reviews include user complaints about non-payment of winnings
- Affiliate marketing of gambling may require local licensing in EU member states
- Bonus code promotions (up to €4,500) subject to advertising regulations

**Why this matters for users:**
- No guarantee of regulatory protection for players
- Dispute resolution may be limited under Curaçao jurisdiction

**Evidence:** GitHub READMEs (license details) + uk.trustpilot.com/review/chickenroad-2.app

**Source:** github.com/chickengamegambling/chicken-road-2 + Trustpilot

---

## OBS-07 — Third-Party Tracking (GTM & Facebook Pixel) — GDPR Risk
**Severity:** 🟡 MEDIUM

Google Tag Manager (GTM-W9DD2NF) and a Facebook tracking Pixel
(app_id: 380732709336812) were identified in page metadata.

**What these scripts do:**
- Load on every page visit — before user registration or login
- Transmit browsing behaviour to Google and Meta servers
- Enable behavioural retargeting and audience profiling

**GDPR Risk:**
For EU-based visitors, GDPR Article 7 requires explicit consent before
non-essential tracking cookies and scripts activate. If no properly implemented
cookie consent mechanism is shown before GTM/Pixel fires, this constitutes
a potential regulatory violation enforceable by EU data protection authorities.

**Cannot confirm:** Whether a consent banner exists — WAF blocks scanner access.

**Evidence:** ScamAdviser page metadata analysis (GTM tag ID, fb:app_id meta tag)

**Source:** scamadviser.com/check-website/chicken-road2.app

---

> ⚠️ Educational purposes only | Passive OSINT | Cryptonic Area Internship — Harmain Shah CA0200
