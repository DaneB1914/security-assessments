# Technical Overview – Drumgrange VDP Penetration Test

**Prepared by:** Dane Babcock  
**Assessment Date:** February 2026

## Purpose

This document provides a **technical breakdown** of the tools, techniques, and decision-making process used during the Drumgrange Ltd Vulnerability Disclosure Program (VDP) penetration testing engagement.

It is intended for:
- Security engineers
- Penetration testers
- Technical interviewers

For a complete narrative report, see `report.md`.

---

## Authorization & Scope Handling

- Authorization obtained via Drumgrange Ltd’s HackerOne VDP
- Testing limited to explicitly listed assets
- No authentication credentials provided
- No scope expansion performed

Out-of-scope discoveries were **not tested**, in accordance with VDP requirements.

---

## In-Scope Assets

| Asset | Role |
|-----|-----|
| support.drumgrange.com | Support portal |
| support.drumgrange.co.uk | Canonical support portal |
| webmail.drumgrange.com | Enterprise webmail interface |
| vpnportland.drumgrange.com | VPN infrastructure |
| vpnchertsey.drumgrange.com | VPN infrastructure |

---

## Tooling Summary

| Tool | Usage |
|----|-----|
| subfinder | Passive subdomain enumeration |
| amass (passive) | OSINT-based discovery |
| ffuf | Targeted content discovery |
| curl | HTTP/header analysis |
| Browser DevTools | Network traffic inspection |
| Manual analysis | Behavioral validation |

Automated vulnerability scanners and exploit frameworks were intentionally not used.

---

## Methodology Breakdown

### Passive Reconnaissance
- OSINT-based discovery only
- No direct interaction with services
- Additional subdomains identified but not tested due to scope restrictions

---

### Asset Classification
- VPN endpoints identified as non-web services
- Web enumeration halted immediately on VPN hosts
- Testing focused only on appropriate web assets

---

### Content Discovery (ffuf)
- Common wordlists used
- HTTP 200/301 responses analyzed
- No sensitive configuration or administrative endpoints exposed

---

### HTTP & Header Analysis
- Canonical redirects verified
- HTTPS enforcement confirmed via HSTS
- Cache-control behavior reviewed
- Session cookie attributes validated

---

### Unauthenticated Application Behavior
- Login flows observed without credential guessing
- CSRF protections identified
- Error messaging analyzed for enumeration risk
- No response differentiation observed

---

### Federated Authentication (Webmail)
- OAuth-based redirection to Microsoft identity services
- No local credential handling observed
- Authentication delegated to third-party provider
- Testing halted at identity boundary

---

## Testing Restraint & False Positive Avoidance

Several techniques were intentionally excluded:
- Brute force or credential attacks
- Active vulnerability scanning
- Exploitation attempts
- Third-party identity testing

Observed behaviors were validated against expected enterprise patterns to avoid false positives and over-reporting.

---

## Technical Conclusion

Within the bounds of authorization and scope, no vulnerabilities or misconfigurations were identified. Observed behavior across all assets aligns with modern enterprise security best practices.

The engagement emphasizes **methodology, judgment, and ethical restraint** over raw vulnerability discovery.

---

## References

- `report.md` – Full professional engagement report
- HackerOne Vulnerability Disclosure Program – Drumgrange Ltd

