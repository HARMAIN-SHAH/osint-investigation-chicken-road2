# 🔍 OSINT Investigation & Intelligence Gathering
### Project 02 — Cryptonic Area Cybersecurity Internship

<p align="center">
  <img src="https://img.shields.io/badge/Project-OSINT%20Investigation-blue?style=for-the-badge&logo=search&logoColor=white"/>
  <img src="https://img.shields.io/badge/Status-Completed-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Intern-Harmain%20Shah-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/ID-CA0200-red?style=for-the-badge"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Target-chicken--road2.app-informational?style=flat-square"/>
  <img src="https://img.shields.io/badge/Tools%20Used-7-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Sources%20Documented-13-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Observations-7-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/Method-Passive%20OSINT-purple?style=flat-square"/>
</p>

> ⚠️ **Educational Disclaimer:** This project was completed for educational purposes only as part of the Cryptonic Area Cybersecurity Internship Program. All investigation was conducted using publicly available tools and sources only — no private, restricted, or unauthorised data was accessed. The target website is a real public domain investigated strictly through passive, legal OSINT methods.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Target Information](#-target-information)
- [Methodology](#-methodology)
- [Tools Used](#-tools--websites-used)
- [Key Findings Summary](#-key-findings-summary)
- [Security Observations](#-security-observations)
- [Repository Structure](#-repository-structure)
- [Report](#-report)
- [Skills Demonstrated](#-skills-demonstrated)

---

## 🔍 Project Overview

This project is part of the **Cryptonic Area Cyber Security & Ethical Hacking Internship Program — Project 02 (OSINT)**. The objective was to investigate a target website using only publicly available resources and produce a professional OSINT Intelligence Report.

> *"Public data, private conclusions — the art of Open Source Intelligence."*

The entire investigation was conducted using **passive OSINT techniques only** — no active scanning, no exploitation, no unauthorised access. Every finding is supported by a specific tool, source URL, and documented evidence.

---

## 🎯 Target Information

| Field | Details |
|---|---|
| **Target URL** | https://www.chicken-road2.app/ |
| **Domain** | chicken-road2.app |
| **TLD** | .app (Google Registry — HSTS preloaded) |
| **Site Type** | Casino Affiliate / SEO Affiliate Website |
| **Game Promoted** | Chicken Road 2 by InOut Games |
| **Investigation Date** | 22 July 2026 |
| **Method** | Passive OSINT — publicly available sources only |

---

## 🛠️ Methodology

The investigation followed a structured passive OSINT methodology:

```
1. DNS ENUMERATION
   └─ Resolve A, AAAA, NS records using Python socket module

2. SSL / TLS INSPECTION
   └─ Direct TLS handshake using Python ssl module
   └─ Extract CN, issuer, validity, TLS version

3. HTTP RESPONSE ANALYSIS
   └─ curl HTTP header scan
   └─ Identify WAF, server headers, response codes

4. WHOIS / RDAP LOOKUP
   └─ ScamAdviser public WHOIS database
   └─ Identify registrant status, nameservers

5. HOSTING & ASN IDENTIFICATION
   └─ IP → ASN lookup via ScamAdviser infrastructure data
   └─ Cloudflare CDN confirmation

6. TECHNOLOGY FINGERPRINTING
   └─ ScamAdviser metadata analysis
   └─ GitHub source code inspection

7. OPEN SOURCE INTELLIGENCE
   └─ GitHub organisation enumeration
   └─ Public repository source code review
   └─ Social media profile discovery
   └─ Trustpilot review analysis
```

---

## 🧰 Tools & Websites Used

| # | Tool / Website | Category | Purpose |
|---|---|---|---|
| 01 | **Python socket module** | DNS Tool | A/AAAA record resolution |
| 02 | **Python ssl module** | SSL Inspector | Direct TLS handshake — certificate extraction |
| 03 | **curl** | HTTP Scanner | Response headers, status codes, WAF detection |
| 04 | **Python urllib.request** | HTTP Tool | robots.txt and sitemap.xml testing |
| 05 | **ScamAdviser** | OSINT Platform | Trust score, hosting, WHOIS, tracking tags |
| 06 | **GitHub** | Code Repository | Org enumeration, repo inspection, attribution |
| 07 | **Trustpilot** | Review Platform | User reviews and reputation analysis |

---

## 📊 Key Findings Summary

| Category | Finding | Risk Level |
|---|---|---|
| Domain Registrar | Privacy service active — registrant identity fully concealed | MEDIUM |
| Hosting / CDN | Cloudflare Inc. (ASN 13335) — real origin IP masked | LOW |
| IP Addresses | 172.67.137.239 and 104.21.38.193 (Cloudflare anycast) | LOW |
| SSL Certificate | DV wildcard SSL from Google Trust Services — TLS 1.3 | LOW |
| Security Headers | Not verifiable — Cloudflare WAF returns 403 to scanners | MEDIUM |
| robots.txt / sitemap | 403 Forbidden — Cloudflare WAF blocking both endpoints | INFO |
| Technologies | HTML5, Cloudflare CDN, Google GTM, Facebook Pixel | LOW |
| Language Paths | 8 paths: /en/ /it/ /es/ /fr/ /de/ /pl/ /pt/ /sk/ | INFO |
| GitHub Presence | 9+ public repos by "chickengamegambling" — full structure exposed | MEDIUM |
| Attribution Lead | GitHub user @reshan3812 linked to the organisation | MEDIUM |
| Business Nature | Online gambling / casino affiliate — regulated activity | HIGH |
| Third-Party Tracking | GTM (GTM-W9DD2NF) + Facebook Pixel — GDPR risk for EU | MEDIUM |
| Trust Score | ScamAdviser: "Very Likely Safe" — gambling category flagged | LOW |

---

## 🚨 Security Observations

| ID | Observation | Severity |
|---|---|---|
| OBS-01 | WHOIS registrant identity fully concealed — no public accountability | MEDIUM |
| OBS-02 | DV SSL only — no organisation identity verification | LOW |
| OBS-03 | Real origin server IP hidden behind Cloudflare CDN | LOW |
| OBS-04 | Security headers not verifiable — Cloudflare WAF active | MEDIUM |
| OBS-05 | 9 public GitHub repos expose full site architecture, bonus codes, casino partners | MEDIUM |
| OBS-06 | Gambling affiliate — regulatory and legal risk in multiple jurisdictions | HIGH |
| OBS-07 | GTM + Facebook Pixel active — GDPR compliance risk for EU visitors | MEDIUM |

Full detailed analysis in [`Security-Observations.md`](./Security-Observations.md)

---

## 📁 Repository Structure

```
osint-investigation-chicken-road2/
│
├── README.md                              ← You are here
├── OSINT_Report_Harmain_Shah_CA0200.pdf  ← Full professional intelligence report
│
├── findings/
│   ├── DNS-Records.md                    ← A, AAAA, NS records with evidence
│   ├── WHOIS-Analysis.md                 ← Registrant data, nameservers, privacy status
│   ├── SSL-Certificate.md                ← Full TLS certificate breakdown
│   ├── Hosting-IP-Analysis.md            ← Cloudflare CDN, ASN, IP geolocation
│   ├── HTTP-Response.md                  ← Headers, WAF detection, robots/sitemap
│   ├── Technologies.md                   ← Tech stack, GTM, Facebook Pixel
│   └── GitHub-OSINT.md                   ← Org enumeration, repos, attribution lead
│
├── Security-Observations.md              ← All 7 observations with severity
├── Recommendations.md                    ← 8 actionable recommendations
├── Sources-References.md                 ← All 13 source URLs documented
└── .gitignore
```

---

## 📄 Report

The full professional OSINT Intelligence Report is available in this repository:

📎 **[`OSINT_Report_Harmain_Shah_CA0200.pdf`](./OSINT_Report_Harmain_Shah_CA0200.pdf)**

### Report Sections:
| Section | Content |
|---|---|
| Executive Summary | All findings with risk classification table |
| Target Overview | Complete site profile — 14 fields |
| Information Gathered | 9 sub-sections with full technical detail |
| List of Tools Used | 7 tools with purpose and source URLs |
| References | 13 numbered, attributed source URLs |
| Security Observations | OBS-01 through OBS-07 with evidence |
| Recommendations | R-01 through R-08 mapped to observations |

---

## 💡 Skills Demonstrated

```
✔  Passive OSINT Methodology     — Structured investigation without active scanning
✔  DNS Enumeration               — A, AAAA, NS record resolution and interpretation
✔  SSL/TLS Certificate Analysis  — Direct TLS handshake inspection
✔  HTTP Header Analysis          — WAF detection, security header assessment
✔  WHOIS / RDAP Research         — Registrant attribution and privacy analysis
✔  GitHub OSINT                  — Org enumeration, repo inspection, identity leads
✔  CDN / Hosting Fingerprinting  — ASN lookup, Cloudflare identification
✔  Technology Stack Detection    — GTM, Facebook Pixel, CDN identification
✔  Source Documentation          — Every finding attributed to a specific tool + URL
✔  Intelligence Report Writing   — Professional PDF investigation report
```

---

<p align="center">
  <b>Harmain Shah</b> | Intern ID: CA0200<br>
  Cryptonic Area Cyber Security & Ethical Hacking Internship Program<br>
  <i>Project 02 — OSINT Investigation & Intelligence Gathering</i><br><br>
  ⚠️ For educational purposes only | All investigation conducted via passive, legal OSINT methods
</p>
