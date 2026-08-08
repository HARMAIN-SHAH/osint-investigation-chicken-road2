# ⚙️ Technologies & Tracking Detection
### Target: chicken-road2.app | Sources: ScamAdviser + GitHub | Date: 22 July 2026

---

## Identified Technologies

| Technology | Category | Evidence Source | Risk Note |
|---|---|---|---|
| HTML5 | Frontend Framework | GitHub source repos | Standard — no risk |
| Cloudflare CDN | CDN / DDoS Protection | DNS resolution + NS records | Legitimate use |
| Google Trust Services | SSL Certificate Authority | Direct TLS handshake | Legitimate use |
| TLS 1.3 | Encryption Protocol | Direct TLS handshake | Strongest available |
| Google Tag Manager | Analytics / Tracking | ScamAdviser metadata (GTM-W9DD2NF) | ⚠️ GDPR risk |
| Facebook Pixel | Marketing Tracking | ScamAdviser (app_id: 380732709336812) | ⚠️ GDPR risk |
| Provably Fair (blockchain) | Game Integrity Tech | GitHub READMEs | Gambling-specific |
| Static HTML / CSS | Build Type | GitHub repo source structure | Standard |

---

## Google Tag Manager (GTM)

**Tag ID:** `GTM-W9DD2NF`
**Source:** ScamAdviser page metadata

Google Tag Manager is a tag management system that loads third-party scripts
(analytics, advertising pixels, heatmaps) on the page. Once GTM loads, it can
fire any number of additional tracking tags.

**Privacy Implication:**
- Loads on every page visit — even before user interaction
- Sends data to Google servers
- Can be used to load Facebook Pixel, Google Analytics, AdWords, and more
- User behaviour (pages visited, time on page, clicks) is transmitted to Google

---

## Facebook Pixel

**App ID:** `380732709336812`
**Source:** ScamAdviser page metadata (fb:app_id meta tag)

The Facebook Pixel is a tracking script that:
- Tracks page visits and user behaviour
- Sends data to Meta (Facebook) servers
- Enables retargeted advertising on Facebook/Instagram
- Can track users who have never interacted with the site directly

**Privacy Implication:**
- Active even without user account registration
- GDPR Article 7 requires explicit consent before activation for EU users
- Gambling + tracking = heightened regulatory scrutiny

---

## GDPR Risk Assessment

For EU-based visitors, the combination of GTM + Facebook Pixel creates compliance
obligations under **GDPR Article 7 (Consent)**:

| Requirement | Status |
|---|---|
| Cookie consent banner before scripts load | Cannot verify (403 blocks scanner) |
| Explicit opt-in for non-essential cookies | Cannot verify |
| Privacy policy clearly accessible | Cannot verify |
| Data processor agreements with Google/Meta | Cannot verify |

If no consent mechanism is in place before these scripts fire, this constitutes
a potential regulatory violation subject to enforcement by EU data protection authorities.

---

## Language-Specific Paths (from GitHub)

GitHub repository analysis revealed the full deployment structure:

| URL Path | Language | Repository |
|---|---|---|
| `https://www.chicken-road2.app/` | French (default) | chickengamegambling/chicken-road2-fr |
| `https://www.chicken-road2.app/en/` | English | chickengamegambling/chicken-road-2 |
| `https://www.chicken-road2.app/it/` | Italian | chickengamegambling/chicken-road-2-it |
| `https://www.chicken-road2.app/es/` | Spanish | chickengamegambling/chicken-road-2-es |
| `https://www.chicken-road2.app/de/` | German | chickengamegambling/chickenroad-de |
| `https://www.chicken-road2.app/pl/` | Polish | chickengamegambling/chicken-road2-pl |
| `https://www.chicken-road2.app/pt/` | Portuguese | chickengamegambling/chicken-road-2-pt |
| `https://www.chicken-road2.app/sk/` | Slovak | chickengameglambling/chicken-road-2-sk |

---

## Sources

| Data | Tool | Source |
|---|---|---|
| GTM tag ID, Facebook Pixel app_id | ScamAdviser metadata | scamadviser.com/check-website/chicken-road2.app |
| Language paths, tech stack | GitHub repos | github.com/chickengamegambling |
| SSL tech, TLS version | Python ssl module | Direct TLS handshake |

---

> ⚠️ Educational purposes only | Passive OSINT | Cryptonic Area Internship — Harmain Shah CA0200
