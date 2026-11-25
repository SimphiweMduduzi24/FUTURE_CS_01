# FUTURE_CS_01 - Vulnerability Assessment Report

**Intern:** Simphiwe Mduduzi Gumede
**Program:** Future Interns - Cyber Security Track
**Task:** Task 1 - Vulnerability Assessment Report for a Live Website
**Target:** https://yalos-express.netlify.app (my own project, tested with my authorization)
**Date:** 25 November 2026

## Overview
A passive security assessment of Yalos Express, a snack-delivery web app I built and deployed on Netlify for UKZN residence students. The goal was to identify common web weaknesses, rate their risk (Low / Medium / High), explain them in plain business language, and give clear fixes.

## Result summary
| Risk | Count |
|---|---|
| High | 0 |
| Medium | 0 |
| Low | 2 |
| Informational | 2 |

**Overall:** well configured, with minor improvements recommended.

| ID | Finding | Risk |
|---|---|---|
| VA-01 | Content Security Policy allows inline styles | Low |
| VA-02 | Public admin entry point; order/chat access control not tested | Low |
| VA-03 | Cache-control settings to re-examine | Informational |
| VA-04 | Comments in page source (false positive) | Informational |

Positive findings: HTTPS only, TLS 1.2/1.3 with all A-grade ciphers, HSTS, nosniff, X-Frame-Options, Referrer-Policy, Permissions-Policy, a strong CSP, and no cookies set.

## Tools and methodology
- **Nmap 7.993** - light service detection (ports 80, 443) and TLS cipher review
- **OWASP ZAP 2.17.0** - Safe Mode, Manual Explore (passive only, no active scan)
- **Browser DevTools** - response headers and cookie check

## Scope and ethics
- Only my own site was tested, passively.
- The admin login and order/chat endpoints were **not** attacked or probed, to protect real customer data.
- ZAP alerts from `edge-consumer-static.azureedge.net` were Microsoft Edge background traffic and were excluded.
- Port 80 results were affected by local network filtering and are not treated as findings.

## Repository contents
```
FUTURE_CS_01/
├── README.md
├── report/
│   └── FUTURE_CS_01_Vulnerability_Assessment_Report.pdf
└── evidence/
    ├── nmap_basic.txt
    ├── nmap_tls.txt
    ├── zap_report.html
    └── devtools_cookies.png
```

## Key learnings
- Reading tool output critically matters: three ZAP alerts belonged to browser background traffic, not the target, and one "suspicious comment" was a false positive.
- A tool's automatic risk rating is a starting point. I rated the CSP issue Low rather than ZAP's Medium because scripts were already restricted.
- Responsible testing means defining scope and leaving sensitive areas untouched.

[Download the full report (PDF)](report/FUTURE_CS_01_Vulnerability_Assessment_Report.pdf)
