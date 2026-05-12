# Advanced GPO Troubleshooting & Scope

## 📘 Overview

**Objective:** Diagnose GPO application failures and implement Security Group Filtering

**Estimated Time:** 45 minutes

---

# 🧩 Scenario

A Group Policy Object (GPO) for **Windows Firewall** is not applying to certain computers.
Investigate the root cause and implement a solution using **Security Group Filtering**.

---

# 🛠️ Troubleshooting & Resolution Procedures

## 1. Collect Affected Computer Names

Identify all systems experiencing the Group Policy issue.

### Tasks

* Collect affected computer names.
* Verify each computer is:

  * Joined to the correct domain
  * Online and reachable
  * Communicating with the domain controller

### Verification Commands

```bash id="7p7tlk"
hostname
```

```bash id="shj3ql"
systeminfo | findstr /B /C:"Domain"
```

### Purpose

Confirms the systems are properly domain-joined and eligible for Group Policy processing.

---

## 2. Generate Group Policy Results Report

Run Group Policy reporting on affected systems.

### Command

```bash id="l8q8t3"
gpresult /h report.html
```

### Steps

1. Open **Command Prompt** as Administrator.
2. Execute the command above.
3. Open the generated `report.html` file in a web browser.

### Purpose

Provides a detailed report of:

* Applied GPOs
* Denied GPOs
* Security filtering results
* WMI filtering status
* User and computer policy processing

---

## 3. Analyze Applied Group Policy Objects

Review the generated report.

### Check For

* The firewall GPO appearing under:

```text id="e4t3uq"
Applied Group Policy Objects
```

* Any entries under:

```text id="ef6m1m"
Denied GPOs
```

### Common Denial Reasons

* Security filtering restrictions
* WMI filter mismatch
* Block inheritance
* Missing permissions
* Replication delays

### Purpose

Determines whether the GPO is reaching the target system.

---

## 4. Force Group Policy Update

If the GPO is missing, refresh Group Policy manually.

### Command

```bash id="nn8m1m"
gpupdate /force
```

### Steps

1. Run the command on the affected computer.
2. Restart the computer if prompted.

### Purpose

Forces immediate Group Policy retrieval and application.

---

## 5. Use Resultant Set of Policy (RSoP)

Visualize applied policies using RSoP.

### Command

```bash id="v6j4ow"
rsop.msc
```

### Purpose

Displays:

* Applied policies
* Effective policy settings
* Winning GPOs
* Policy inheritance structure

### Validation Checklist

* Firewall settings appear correctly
* Expected GPOs are listed
* No policy conflicts exist

---

# 🏢 Organizational Unit (OU) Verification

## 6. Check OU Structure

Verify affected computers reside in the correct Organizational Unit (OU).

### Steps

1. Open **Active Directory Users and Computers (ADUC)**.
2. Locate the affected computers.
3. Confirm they are placed in the intended OU.

### Purpose

GPOs only apply to linked OUs unless inheritance or filtering changes behavior.

### Validation Checklist

* Correct OU placement
* GPO linked to the OU
* No inheritance blocks

---

# 🔐 Security Group Filtering Configuration

## 7. Review GPO Scope Settings

Review Security Group Filtering in the Group Policy Management Console (GPMC).

### Steps

1. Open **Group Policy Management Console (GPMC)**.
2. Select the target GPO.
3. Open the:

```text id="t2k5qv"
Scope
```

tab.

4. Review:

   * Security Filtering
   * Delegation permissions
   * WMI filters

### Purpose

Determines which users or computers are permitted to apply the GPO.

---

## 8. Create a Security Group

Create a security group for targeted computers.

### Example Group Name

```text id="0e7d9g"
Firewall-Policy-Users
```

### Steps

1. Open **Active Directory Users and Computers**.
2. Create a new **Security Group**.
3. Add targeted computer accounts to the group.

### Purpose

Allows granular targeting of Group Policy application.

---

## 9. Configure GPO Permissions

Assign Group Policy permissions to the new security group.

### Steps

1. Open **GPMC**.
2. Select the GPO.
3. Under **Security Filtering**:

   * Add the new security group.
4. Ensure the group has:

   * **Read**
   * **Apply Group Policy**

permissions.

### Purpose

Restricts GPO application to intended systems only.

---

## 10. Remove Authenticated Users (If Required)

Adjust default permissions if stricter targeting is needed.

### Steps

1. In the GPO permissions section:

   * Remove:

```text id="t4x0el"
Authenticated Users
```

from **Apply Group Policy** permissions if necessary.

### Important Note

Removing `Authenticated Users` may prevent unintended systems from receiving the policy.

### Purpose

Enhances policy scoping and security targeting.

---

# ✅ Verification & Validation

## 11. Verify GPO Application Again

Re-run Group Policy reporting.

### Command

```bash id="b6j0t9"
gpresult /h report.html
```

### Validation Checklist

* Firewall GPO appears under Applied GPOs
* No access denied messages
* Security filtering resolves correctly

### Purpose

Confirms the issue has been resolved.

---

## 12. Test Firewall Rule Enforcement

Validate firewall settings are now applied correctly.

### Verification Methods

* Open Windows Firewall settings
* Check configured inbound/outbound rules
* Review applied policies via:

  * Group Policy Results Wizard
  * RSoP
  * `gpresult`

### Purpose

Ensures Group Policy enforcement is functioning as intended.

---

# 🧪 Troubleshooting Tips

## 🔹 Advanced GPO Troubleshooting Tips

* Use **Event Viewer** on the domain controller to monitor Group Policy processing.
* Review logs under:

```text id="9jq6m5"
Applications and Services Logs → Microsoft → Windows → GroupPolicy
```

* Enable verbose logging for detailed diagnostics.
* Verify SYSVOL and NETLOGON shares are accessible.
* Ensure DNS resolution is functioning properly.
* Confirm replication between domain controllers is healthy.
* Use `dcdiag` and `repadmin` for additional diagnostics.
* Review WMI filter conditions if used.

---

# 📌 Summary

This guide covered advanced Group Policy troubleshooting procedures, including:

* Diagnosing GPO application failures
* Using `gpresult` and RSoP tools
* Verifying OU structure and inheritance
* Implementing Security Group Filtering
* Configuring GPO permissions
* Validating firewall policy enforcement
* Monitoring Group Policy processing logs

Proper Group Policy troubleshooting and scoping help ensure secure, reliable, and targeted policy deployment across enterprise environments.
