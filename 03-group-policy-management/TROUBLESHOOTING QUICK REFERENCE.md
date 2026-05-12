# TROUBLESHOOTING QUICK REFERENCE

## 📘 Overview

This section provides fast diagnostic steps for common Active Directory, authentication, Group Policy, and replication issues. Use it as a first-line troubleshooting guide during incidents.

---

# 🔐 Issue: Users Cannot Log On to Domain

## 🧪 Diagnostic Steps

### 1. Verify Network Connectivity

```text id="tr1"
ping <Domain Controller IP>
```

**Purpose:** Confirms basic network reachability to the domain controller.

---

### 2. Check DNS Resolution

```bash id="tr2"
nslookup yourdomain.com
```

**Purpose:** Ensures correct DNS configuration and domain resolution.

---

### 3. Verify Domain Controller Discovery

```bash id="tr3"
nltest /dsgetdc:yourdomain.com
```

**Purpose:** Confirms that a valid domain controller can be located.

---

### 4. Verify Kerberos Tickets

```bash id="tr4"
klist
```

**Purpose:** Checks active Kerberos authentication tickets.

---

### 5. Check Time Synchronization

```bash id="tr5"
w32tm /query /status
```

**Purpose:** Ensures system time is synchronized (critical for Kerberos authentication).

---

### 6. Review Event Viewer Logs

* Open **Event Viewer** on Domain Controller
* Check for:

  * Authentication failures
  * Kerberos errors
  * LDAP bind issues

**Purpose:** Identifies authentication-related system errors.

---

# 📦 Issue: GPO Not Applying to Users/Computers

## 🧪 Diagnostic Steps

### 1. Generate Group Policy Report

```bash id="tr6"
gpresult /h report.html
```

**Purpose:** Displays applied and denied Group Policy Objects.

---

### 2. Verify OU Placement

* Confirm user/computer is in the correct Organizational Unit (OU)

**Purpose:** Ensures correct scope for GPO application.

---

### 3. Check Inheritance Settings

* Ensure **Block Inheritance** is not enabled

**Purpose:** Prevents unintended GPO blocking.

---

### 4. Verify Permissions

* Confirm user/group has:

  * **Read**
  * **Apply Group Policy**

**Purpose:** Ensures GPO security filtering is correctly configured.

---

### 5. Force Group Policy Update

```bash id="tr7"
gpupdate /force /logoff
```

**Purpose:** Forces immediate policy refresh.

---

### 6. Check GPO Conflicts

* Review higher priority GPOs
* Check linked OU hierarchy

**Purpose:** Identifies conflicting or overriding policies.

---

# 🔄 Issue: Replication Failures Between Domain Controllers

## 🧪 Diagnostic Steps

### 1. Check Replication Status

```bash id="tr8"
repadmin /showrepl
```

**Purpose:** Identifies replication errors and failed partners.

---

### 2. Verify Network Connectivity

* Test connectivity between domain controllers

**Purpose:** Ensures DC-to-DC communication is functional.

---

### 3. Check DNS Resolution

* Validate forward and reverse DNS lookups between DCs

**Purpose:** Ensures proper name resolution for replication.

---

### 4. Test RPC Connectivity

```powershell id="tr9"
Test-NetConnection -ComputerName DC2 -Port 135
```

**Purpose:** Verifies RPC communication required for replication.

---

### 5. Review Event Logs

* Check **Directory Service Logs**
* Check **System Logs**

**Purpose:** Identifies replication-related errors.

---

### 6. Force Replication

```bash id="tr10"
repadmin /replicate
```

**Purpose:** Attempts immediate replication between domain controllers.

---

# 🐢 Issue: Slow Domain Logons

## 🧪 Diagnostic Steps

### 1. Check Domain Controller Health

```bash id="tr11"
dcdiag /v
```

**Purpose:** Evaluates overall domain controller performance and health.

---

### 2. Analyze Logon Events

* Open Event Viewer
* Navigate to:

```text id="tr12"
Windows Logs → Security → Logon Events
```

**Purpose:** Measures authentication and logon timing.

---

### 3. Check Network Latency

```bash id="tr13"
ping -w 100 <Domain Controller>
```

**Purpose:** Detects network delays affecting logon speed.

---

### 4. Review Group Policy Processing Time

* Check Event Viewer for Group Policy processing logs

**Purpose:** Identifies slow or failing GPO application.

---

### 5. Evaluate GPO Load

* Excessive GPOs (>50) may degrade performance

**Purpose:** Reduces logon delay caused by policy processing overhead.

---

### 6. Check Group Membership Size

* Ensure users belong to fewer than ~100 groups

**Purpose:** Large group memberships slow authentication and token creation.

---

# 📌 Summary

This quick reference guide covers common troubleshooting scenarios, including:

* Domain login failures
* Group Policy application issues
* Replication failures between domain controllers
* Slow domain logon performance

Each section provides rapid diagnostic commands and validation steps to quickly isolate and resolve Active Directory issues in production environments.
