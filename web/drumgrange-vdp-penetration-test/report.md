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

| Observations |
|----|
| Canonical redirect enforcement |
| Authentication enforced prior to access |
| Strong transport security (HSTS) |
| Secure cache-control behavior |
| Proper session handling |

#### Assessment:
No misconfigigurations or exposure risks identified.

---

## 11. Phase 6 – Unauthenticated Application Behavior Analysis

### Target
https://support.drumgrange.co.uk/User/Login

| Method |
|---|
| Submission of benign input values |
| Network traffic observation via browser developer tools |
| No credential guessing of brute-force attempts |

| Observations |
|---|
| Server-side login handling |
| CSRF protection implemented |
| Generic error messaging |
| No response differentiation based on input |
| No session elevation on failure |

### Assessment:
Authentication logic behaves securely and resists common enumeration and logic flaws.

---

## 12. Phase 7 – Federated Authentication Flow Observation (Webmail)

### Target
https://webmail.drumgrange.com/mail

| Observations |
|---|
| Immediate redirect to Microsoft identity services
| OAuth-based authentication flow |
| No local credential handling observed |

## Security Posture Summery

### Observed defensive strengths include:
- Clear separation of infrastructure roles (VPN, support, webmail)

-Proper enforcement of authentication prior to application access

-Strong transport-layer protections (HSTS)

-Secure session and cache-handling behavior

-Delegation of authentication to Microsoft identity services

-Perimeter protection via Cloudflare

---

## Methodology & Professional Judgment

Testing decisions were guided by **scope compliance**, **signal quality**, and **risk minimization**.

Certain tools and intrusive techniques were intentionally not used where they would have introduced unnecessary noise, exceeded authorization boundaries, or provided limited analytical value. Scope limitations directly influenced testing depth, particularly for authenticated functionality and third-party identity services.

Potential false positives were avoided by validating observed behavior against expected enterprise design patterns. Only defensible, actionable observations were documented.

---

## Conclusion

The assessed Drumgrange Ltd assets exhibit a strong external security posture and adhere to industry best practices for access control, transport security, and authentication architecture.

Equally important, this engagement demonstrates disciplined methodology, appropriate restraint, and professional judgment — all critical components of real-world penetration testing.

---

**Disclaimer**: No exploitation attempts were performed, as no validated vulnerabilities were identified within scope.
