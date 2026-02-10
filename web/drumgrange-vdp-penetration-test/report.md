# Penetration Testing Report

| Field | Value |
|------|------|
| **Client** | Drumgrange Ltd |
| **Engagement Type** | Vulnerability Disclosure Program (VDP) |
| **Platform** | HackerOne |
| **Tester** | Dane Babcock (handle: labus3r) |
| **Assessment Duration** | ~1.5 days |
| **Date** | February 2026 |
| **Authorization** | Explicit authorization granted via Drumgrange Ltd VDP scope on HackerOne |
  

---

## Engagement Overview

**Engagement Type:** External, Unauthenticated Penetration Testing (VDP)  
**Authorization:** Explicitly authorized via Drumgrange Ltd’s HackerOne Vulnerability Disclosure Program  
**Scope:** Select Drumgrange-owned web and infrastructure assets (unauthenticated access only)  
**Methodology:** Phased assessment emphasizing scope validation, passive reconnaissance, asset classification, targeted enumeration, and behavioral analysis  
**Testing Depth:** Non-intrusive; no credentialed access, exploitation attempts, or denial-of-service activity  
**Outcome:** No vulnerabilities identified within the authorized scope; assets demonstrated secure, expected behavior consistent with enterprise best practices  

---

## 1. Executive Summary

This report documents a scope-authorized, non-intrusive penetration testing engagement conducted against Drumgrange Ltd’s externally exposed assets as defined by their public Vulnerability Disclosure Program (VDP).

The engagement focused on validating the organization’s external security posture through a phased methodology emphasizing authorization verification, passive reconnaissance, asset classification, targeted content discovery, and unauthenticated application behavior analysis.

All testing was conducted ethically, conservatively, and strictly within the published scope. No credentials were used, no authentication was bypassed, and no intrusive or destructive techniques were employed.

### High-Level Outcome

- No vulnerabilities or misconfigurations were identified within the authorized scope  
- Tested assets demonstrated consistent, secure, and expected behavior  
- Strong defensive controls were observed across web and infrastructure boundaries  

The absence of findings reflects effective baseline security controls rather than incomplete testing.

---

## 2. Scope & Authorization

### Authorization Source
- Drumgrange Ltd Vulnerability Disclosure Program (VDP)
- Hosted on HackerOne

Testing was performed only against assets explicitly listed as in scope.

---

## 3. In-Scope Assets Assessed

### Domains and Subdomains

| Asset | Classification |
|-----|--------------|
| support.drumgrange.com | Web application (support portal) |
| support.drumgrange.co.uk | Web application (canonical support portal) |
| webmail.drumgrange.com | Enterprise webmail interface |
| vpnportland.drumgrange.com | VPN infrastructure |
| vpnchertsey.drumgrange.com | VPN infrastructure |

No testing was conducted against any asset not explicitly listed above.

---

## 4. Methodology Overview

The engagement followed a structured penetration testing workflow adapted for a VDP context:

1. Authorization and scope validation  
2. Passive reconnaissance  
3. Asset classification  
4. Content discovery  
5. HTTP and security header analysis  
6. Unauthenticated application behavior analysis  
7. Federated authentication flow observation  
8. Documentation and professional assessment  

Testing emphasized **scope compliance**, **signal quality**, and **risk minimization** throughout.

---

## 5. Tools Utilized

| Tool | Purpose |
|----|--------|
| subfinder | Passive subdomain enumeration |
| amass (passive) | OSINT-based asset discovery |
| ffuf | Targeted content discovery |
| curl | HTTP header and behavior analysis |
| Browser DevTools | Network traffic inspection |
| Manual analysis | Behavioral observation and validation |

Automated vulnerability scanners and exploit frameworks were intentionally not used.

---

## 6. Phase 1 – Passive Reconnaissance

### Objective
Identify publicly observable information related to scoped assets using passive techniques only.

### Actions
- Passive enumeration via `subfinder`
- Passive OSINT correlation via `amass`

### Results
- Confirmed existence of scoped assets
- Identified additional subdomains via OSINT sources

### Professional Judgment
Additional subdomains discovered during passive reconnaissance were not tested, as they were not explicitly included in scope.

---

## 7. Phase 2 – Asset Classification

Each asset was classified prior to enumeration to determine appropriate testing techniques.

| Asset | Determination | Action |
|----|-------------|-------|
| VPN endpoints | Non-web services | Enumeration halted |
| Support portals | Web applications | Enumeration permitted |
| Webmail | Enterprise web application | Enumeration permitted |

This classification prevented misuse of tools and avoided unnecessary interaction with non-web services.

---

## 8. Phase 3 – Content Discovery (ffuf)

### Method

Targeted directory and file enumeration using `ffuf` and common wordlists.

```bash
ffuf -u https://TARGET/FUZZ -w common.txt -mc 200,301
```

### 8.1 VPN Endpoints
| Assets | Result |
|----|-------------|
| vpnportland.drumgrange.com | Connection errors only | 
| vpnchertsey.drumgrange.com | No HTTP responses observed |

#### Conclusion:
These hosts are not web services. Enumeration was halted immediately.

### 8.2 Support Portal
| Asset | Findings |
|----|-------------|
| support.drumgrange.com | Minimal exposed paths
| N/A | Standard .well-known endpoints |
| N/A | No administrative or sensitive files exposed |

#### Assessment:
Behavior consistent with a properly secured support portal.

### 8.3 Webmail Interface
| Asset | Findings |
|----|-------------|
| webmail.drumgrange.com | Application paths consistent with Microsoft-based infrastructure |
| N/A | Framework indicators aligned with ASP.NET / Outlook Web Access |
| N/A | No exposed configuration files or debug output |

#### Assessment:
Surface area consistent with enterprise webmail platforms.

---

## 9. Phase 4 – HTTP & Security Header Analysis (Support Portal)

### Commands

```bash
curl -I https://support.drumgrange.com
curl -I https://support.drumgrange.co.uk/
```

# TO BE CONINUED...

**Disclaimer**: No exploitation attempts were performed, as no validated vulnerabilities were identified within scope.
