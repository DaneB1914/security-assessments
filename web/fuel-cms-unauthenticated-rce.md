# Web Application Security Assessment — Fuel CMS (Unauthenticated RCE)

**Platform:** TryHackMe  
**Assessment Type:** Vulnerability Capstone (Web Application)  
**Date:** 1/20/2026  
**Author:** Dane Babcock  

---

## 1. Executive Summary

A security assessment was performed against a publicly accessible blog application deployed by *Ackme Support Incorporated* prior to public release. The objective was to identify and validate any security weaknesses that could be abused by an unauthenticated attacker.

During the assessment, the application was identified as running a vulnerable version of **Fuel CMS**, which is affected by a publicly disclosed vulnerability allowing **unauthenticated remote code execution (RCE)**. Successful exploitation resulted in command execution on the underlying system, confirming a critical security risk.

---

## 2. Scope & Authorization

**In Scope**
- Web application and underlying host provided by the training platform

**Out of Scope**
- Denial of service attacks
- Attacks against external systems

⚠️ All testing was performed in a controlled lab environment with explicit authorization.

---

## 3. Methodology

The assessment followed a standard penetration testing workflow:

1. Application reconnaissance and fingerprinting  
2. Version identification  
3. Vulnerability research and validation  
4. Manual exploitation  
5. Post-exploitation verification  
6. Impact assessment and remediation guidance  

This methodology mirrors real-world web application penetration testing engagements.

---

## 4. Reconnaissance & Application Identification

Initial reconnaissance involved manually interacting with the web application to understand its purpose and underlying technology.

Key activities included:
- Reviewing application functionality and structure
- Inspecting HTTP responses and page content
- Identifying application metadata revealing the CMS name and version

The application was confirmed to be running **Fuel CMS**, with a version known to be affected by a publicly documented vulnerability.

---

## 5. Vulnerability Research

After identifying the CMS and version, public vulnerability databases were consulted to determine whether known security issues applied.

Research confirmed the presence of a **publicly disclosed CVE** affecting the identified Fuel CMS version, which allows **unauthenticated remote code execution** when exploited under certain conditions.

An appropriate exploit was identified through public sources and reviewed to ensure applicability to the target environment.

---

## 6. Exploitation (High-Level)

Manual exploitation was performed to validate whether the vulnerability was exploitable in practice.

Important characteristics of the exploitation phase:
- Exploit logic was reviewed prior to execution
- No automated exploitation frameworks were used
- Exploitation was limited strictly to validating impact

Successful exploitation resulted in the ability to execute arbitrary commands on the target system, confirming **unauthenticated remote code execution**.

---

## 7. Post-Exploitation Verification

To confirm the extent of access obtained:
- A reverse shell was established in a controlled manner
- The system context was validated
- Proof of compromise was obtained by accessing a predefined file on the system

⚠️ Specific commands, payloads, and proof values are intentionally omitted.

---

## 8. Impact Assessment

**Vulnerability Type:**  
Unauthenticated Remote Code Execution (RCE)

**Severity:**  
**Critical**

**Impact:**  
If exploited in a real-world environment, this vulnerability would allow an unauthenticated attacker to:
- Execute arbitrary system commands
- Fully compromise the application
- Access or modify sensitive data
- Establish persistence or pivot to internal systems

This represents a complete loss of confidentiality, integrity, and availability.

---

## 9. Root Cause Analysis

The vulnerability existed due to:
- Deployment of an outdated CMS version with a known critical vulnerability
- Lack of patch management for third-party software
- Public exposure of the application without compensating controls

---

## 10. Remediation Recommendations

To mitigate this issue, the following actions are recommended:

- Immediately upgrade Fuel CMS to a patched and supported version
- Implement a formal patch management process for third-party software
- Restrict public access to administrative or sensitive application components
- Monitor vulnerability disclosures relevant to deployed technologies
- Conduct periodic security testing prior to production deployment

---

## 11. Key Takeaways

This assessment demonstrates how critical vulnerabilities can arise from outdated third-party components and highlights the importance of:
- Accurate application fingerprinting
- Correlating versions with known vulnerabilities
- Validating exploitability rather than assuming risk
- Clear documentation of findings and impact

Manual exploitation and careful validation remain essential skills in real-world penetration testing.

---

## 12. Disclaimer

This write-up is provided for educational and portfolio purposes only.  
All testing was conducted against intentionally vulnerable systems in a controlled environment with authorization.  
No sensitive exploit details or real-world targets are disclosed.


