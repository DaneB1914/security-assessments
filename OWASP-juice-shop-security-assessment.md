# Web Application Security Assessment — OWASP Juice Shop

**Platform:** TryHackMe  
**Application:** OWASP Juice Shop  
**Assessment Type:** Web Application Penetration Test (Practice / Capstone)  
**Date:** 1/28/2026  
**Author:** Dane Babcock  

---

## 1. Executive Summary

A web application security assessment was conducted against **OWASP Juice Shop**, a modern, intentionally vulnerable application designed to represent real-world web and API architectures. The objective of the assessment was to identify and validate common web application security vulnerabilities and assess their potential impact.

Multiple high- and medium-severity issues were identified, primarily related to **authentication**, **authorization**, **API security**, and **business logic flaws**. These findings demonstrate how weaknesses in access control and logic enforcement can lead to serious security risks even when traditional input validation is present.

---

## 2. Scope & Authorization

**In Scope**
- OWASP Juice Shop web application
- Application functionality and exposed API endpoints

**Out of Scope**
- Denial of service attacks
- Attacks against underlying infrastructure not exposed by the application

⚠️ All testing was performed in a controlled lab environment with explicit authorization.

---

## 3. Methodology

The assessment followed a standard web application penetration testing methodology:

1. Application reconnaissance and mapping  
2. Authentication and session testing  
3. Authorization and access control testing  
4. Input handling and client-side trust evaluation  
5. Business logic analysis  
6. Impact validation  
7. Remediation guidance  

Testing focused on **manual techniques**, supported by tools such as Burp Suite and browser developer tools.

---

## 4. Application Overview

OWASP Juice Shop is a modern single-page application backed by multiple API endpoints. The application includes user authentication, product management, account functionality, and administrative features, making it representative of real-world web applications commonly assessed during penetration tests.

---

## 5. Findings Summary

| ID | Vulnerability | Severity |
|----|---------------|----------|
| JS-01 | Broken Object Level Authorization (IDOR) | High |
| JS-02 | Authentication Logic Weakness | High |
| JS-03 | Cross-Site Scripting (XSS) | Medium |
| JS-04 | API Excessive Data Exposure | Medium |
| JS-05 | Business Logic Flaw | Medium |

---

## 6. Detailed Findings

---

### JS-01 — Broken Object Level Authorization (IDOR)

**Severity:** High  
**Category:** Access Control  

**Description:**  
The application failed to properly enforce ownership checks when accessing certain resources. By modifying object identifiers in requests, it was possible to access or manipulate data belonging to other users.

**Impact:**  
An attacker could access sensitive user data or perform actions on behalf of other users without authorization.

**Remediation:**  
Implement server-side authorization checks to ensure users can only access resources they own. Avoid relying on client-side controls or predictable identifiers.

---

### JS-02 — Authentication Logic Weakness

**Severity:** High  
**Category:** Authentication  

**Description:**  
Authentication-related functionality relied on flawed logic that could be abused to bypass intended restrictions under certain conditions.

**Impact:**  
Attackers could gain unauthorized access to application functionality, potentially escalating privileges or accessing protected resources.

**Remediation:**  
Ensure authentication workflows enforce strict server-side validation and do not rely on client-side assumptions or predictable behavior.

---

### JS-03 — Cross-Site Scripting (XSS)

**Severity:** Medium  
**Category:** Client-Side Injection  

**Description:**  
User-supplied input was reflected or stored without adequate output encoding, allowing execution of arbitrary JavaScript in the victim’s browser.

**Impact:**  
XSS could be used to hijack user sessions, manipulate application behavior, or deliver malicious payloads to users.

**Remediation:**  
Apply proper output encoding based on context and validate user input. Implement a strong Content Security Policy (CSP).

---

### JS-04 — API Excessive Data Exposure

**Severity:** Medium  
**Category:** API Security  

**Description:**  
API responses exposed more data than necessary, including fields not required by the client application.

**Impact:**  
Sensitive information could be harvested by attackers, increasing the risk of account compromise or data leakage.

**Remediation:**  
Limit API responses to only required fields. Implement response filtering and review API schemas for unnecessary data exposure.

---

### JS-05 — Business Logic Flaw

**Severity:** Medium  
**Category:** Business Logic  

**Description:**  
The application failed to enforce certain business rules correctly, allowing actions to be performed in unintended ways.

**Impact:**  
Attackers could abuse application workflows to gain unfair advantages or bypass restrictions.

**Remediation:**  
Define and enforce business rules strictly on the server side. Perform logic validation independent of client behavior.

---

## 7. Overall Risk Assessment

The application demonstrates a **high-risk security posture**, primarily due to weaknesses in access control and logic enforcement. While individual vulnerabilities may appear simple, their combined impact could result in significant data exposure and unauthorized access.

---

## 8. Key Takeaways

- Modern applications often fail due to **logic and authorization flaws**, not just input validation.
- API security is critical and frequently overlooked.
- Manual testing and careful inspection of requests are essential for identifying real-world issues.
- Effective penetration testing requires understanding application behavior, not just exploiting individual vulnerabilities.

---

## 9. Disclaimer

This assessment was conducted against an intentionally vulnerable applica
