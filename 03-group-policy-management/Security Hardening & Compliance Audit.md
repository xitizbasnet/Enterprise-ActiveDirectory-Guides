# Security Hardening & Compliance Audit

## 📘 Overview

**Objective:** Audit and harden Active Directory (AD) infrastructure against modern security threats

**Estimated Time:** 120 minutes

---

# 🧩 Scenario

Your organization must comply with modern security standards.
You are required to:

* Audit Active Directory for vulnerabilities
* Implement security hardening controls
* Produce a formal compliance report

---

# 🔐 Security Audit & Hardening Procedures

## 1. Audit User Accounts

Identify risky or unused accounts in Active Directory.

### Tasks

* Identify **inactive user accounts**
* Detect **orphaned accounts**
* Review **privileged accounts**
* Identify stale or unused accounts

### Recommended Commands (PowerShell)

```powershell id="uac1"
Search-ADAccount -AccountInactive -UsersOnly -TimeSpan 90.00:00:00
```

### Purpose

Reduces attack surface by eliminating unused or forgotten accounts.

---

## 2. Review Group Memberships

Analyze group structure and privilege assignments.

### Tasks

* Identify excessive nested groups
* Review high-privilege group membership
* Detect privilege escalation risks
* Validate least privilege enforcement

### Focus Groups

* Domain Admins
* Enterprise Admins
* Schema Admins
* Server Operators
* Backup Operators

### Purpose

Prevents privilege creep and excessive access rights.

---

## 3. Audit Service Accounts

Review all service accounts for security risks.

### Tasks

* Identify all service accounts
* Verify SPN (Service Principal Name) registrations
* Ensure unique and strong passwords
* Confirm password rotation policies

### SPN Review Command

```bash id="spn1"
setspn -L <service_account>
```

### Purpose

Mitigates risks such as Kerberoasting and credential theft.

---

## 4. Implement Account Lockout Policy

Configure account lockout thresholds.

### Recommended Settings

* Lockout threshold: 5–10 attempts
* Lockout duration: 15–30 minutes
* Reset counter: 15–30 minutes

### Path in Group Policy

```text id="lockout1"
Computer Configuration → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
```

### Purpose

Prevents brute-force password attacks while maintaining usability.

---

## 5. Enforce Strong Password Policy

Implement enterprise-grade password complexity.

### Recommended Settings

* Minimum length: 12–16 characters
* Complexity requirements enabled
* Password history enforcement
* Maximum password age policy
* Prevent reuse of previous passwords

### Purpose

Reduces risk of credential compromise.

---

## 6. Audit Group Policy Objects (GPOs)

Review GPO security configuration.

### Tasks

* Validate GPO scoping
* Review WMI filters
* Check security filtering
* Audit delegation permissions

### Tool

```text id="gpoaudit1"
Group Policy Management Console (GPMC)
```

### Purpose

Ensures policies are correctly applied and not exposing security gaps.

---

## 7. Enable Advanced Audit Logging

Track critical Active Directory activities.

### Events to Monitor

* User logon/logoff
* Directory service changes
* Privilege escalation attempts
* Account modifications
* Group membership changes

### Path

```text id="audit1"
Security Settings → Advanced Audit Policy Configuration
```

### Purpose

Provides forensic visibility into AD activity.

---

## 8. Implement Microsoft LAPS

Deploy Local Administrator Password Solution.

### Key Features

* Unique local admin passwords per device
* Automatic password rotation
* Centralized password storage in AD

### Purpose

Prevents lateral movement using shared local administrator passwords.

---

## 9. Review Delegation Model

Audit and clean up delegated permissions.

### Tasks

* Identify unnecessary delegations
* Remove excessive privileges
* Validate OU-level permissions
* Document required delegations

### Purpose

Ensures least privilege access control is enforced.

---

## 10. Check for Kerberoasting Risks

Identify vulnerable service accounts.

### Tasks

* Review SPN-enabled accounts
* Identify accounts with weak passwords
* Detect high-privilege service accounts

### Tool Example

```bash id="kerb1"
setspn -Q */*
```

### Purpose

Reduces exposure to Kerberoasting attacks targeting service accounts.

---

## 11. Implement Attack Surface Reduction

Strengthen endpoint and AD security posture.

### Recommended Controls

* Enable Windows Defender features
* Enable ASR (Attack Surface Reduction) rules
* Enable Credential Guard
* Enable Exploit Protection
* Restrict PowerShell execution policies

### Purpose

Reduces exploitable attack vectors across the environment.

---

## 12. Create Compliance Report

Document all audit findings and remediation actions.

### Report Sections

* Executive Summary
* Identified Risks
* Account Audit Results
* Group Membership Findings
* Service Account Analysis
* GPO Security Review
* Audit Logging Configuration
* Remediation Actions
* Risk Ratings
* Recommendations

### Purpose

Provides formal compliance evidence and security posture overview.

---

## 13. Establish Continuous Monitoring

Implement ongoing security monitoring.

### Monitoring Areas

* Failed login attempts
* Privilege escalation attempts
* Group membership changes
* Service account usage anomalies
* GPO modifications
* Domain controller health events

### Tools

* SIEM solutions (e.g., Microsoft Sentinel)
* Event log forwarding
* PowerShell monitoring scripts
* Security dashboards

### Purpose

Ensures continuous detection of security threats.

---

# ⚠️ Security Considerations

## 🚨 Key Risk Areas

* Privileged account misuse
* Weak service account credentials
* Misconfigured GPOs
* Excessive delegation
* Unmonitored authentication activity

---

# 🛡️ Security Best Practice

## 🔹 Microsoft Security Recommendations

* Use the **Microsoft Security Compliance Toolkit (SCT)**
* Perform regular vulnerability assessments
* Conduct periodic access reviews
* Apply least privilege principles consistently
* Enable centralized logging and monitoring
* Perform security audits at scheduled intervals

---

# 📌 Summary

This guide covered enterprise Active Directory security hardening and compliance auditing, including:

* User and privileged account auditing
* Group membership and delegation review
* Service account and SPN analysis
* Password and lockout policy enforcement
* GPO security validation
* Advanced audit logging configuration
* LAPS deployment
* Kerberoasting risk mitigation
* Attack surface reduction strategies
* Compliance reporting and monitoring

A strong security posture requires continuous auditing, proactive hardening, and ongoing monitoring of Active Directory environments.
