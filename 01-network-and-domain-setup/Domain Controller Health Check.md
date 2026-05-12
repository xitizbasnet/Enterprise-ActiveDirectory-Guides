# Domain Controller Health Check

## 📘 Overview

**Objective:** Monitor and verify domain controller health
**Estimated Time:** 20 minutes

---

# 🖥️ Domain Controller Health Check Procedures

## 1. Open Active Directory Sites and Services

Access the Active Directory replication topology and site configuration console.

### Steps

1. Open **Server Manager**
2. Navigate to:

```text
Tools → Active Directory Sites and Services
```

### Purpose

This console is used to monitor site replication, domain controller placement, and Active Directory connectivity.

---

## 2. Check Replication Status

Verify Active Directory replication between domain controllers.

### Steps

1. Expand the domain structure.
2. Navigate to the appropriate site and server objects.
3. Right-click the connection objects.
4. Select the replication check option.

### Purpose

Ensures replication is functioning correctly between domain controllers.

### Validation Checklist

* Replication completes successfully
* No replication failures or delays
* Connection objects are present and healthy

---

## 3. Run Replication Diagnostic

Run replication commands from an elevated Command Prompt.

### Steps

1. Open **Command Prompt** as Administrator.
2. Run the following command:

```bash
repadmin /replicate
```

### Purpose

Forces or verifies Active Directory replication between domain controllers.

### Expected Result

Replication should complete without errors.

---

## 4. Check SYSVOL Replication

Verify SYSVOL replication consistency across domain controllers.

### Command

```bash
repadmin /showvector DC=yourdomain,DC=com
```

### Purpose

Confirms replication vectors and SYSVOL synchronization status.

### Validation Checklist

* SYSVOL replication is current
* No lingering replication backlog
* Domain controllers are synchronized

---

# 📊 Monitoring & Diagnostics

## 5. Monitor Event Viewer

Review system and directory service logs for errors or warnings.

### Steps

1. Open **Event Viewer**
2. Navigate to:

```text
Windows Logs → System
```

3. Also review:

```text
Applications and Services Logs → Directory Service
```

### Look For

* Replication failures
* DNS errors
* Authentication issues
* SYSVOL or DFSR warnings
* Kerberos-related errors

### Purpose

Provides insight into operational health and troubleshooting information.

---

## 6. Check FSMO Roles

Verify Flexible Single Master Operation (FSMO) role ownership.

### Command

```bash
netdom query fsmo
```

### Purpose

Displays the domain controllers currently holding FSMO roles.

### FSMO Roles

* Schema Master
* Domain Naming Master
* RID Master
* PDC Emulator
* Infrastructure Master

### Validation Checklist

* All FSMO roles are assigned
* Expected domain controllers hold the roles
* No role transfer issues exist

---

## 7. Verify DNS SRV Records

Ensure Active Directory-related DNS SRV records exist and are healthy.

### Steps

1. Open **DNS Manager**
2. Navigate to the domain DNS zone.
3. Verify SRV records under:

```text
_msdcs
_tcp
_udp
_sites
```

### Purpose

SRV records are critical for domain controller discovery and authentication services.

### Validation Checklist

* Domain controllers are properly registered
* Required SRV records exist
* No duplicate or stale records

---

## 8. Test Connectivity

Run a comprehensive domain controller diagnostic.

### Command

```bash
dcdiag /v
```

### Purpose

Performs extensive health checks on:

* DNS
* Replication
* SYSVOL
* Services
* Connectivity
* Advertising status

### Expected Result

All tests should pass without critical failures.

---

## 9. Review DCPROMO Logs

Inspect domain controller promotion logs for historical or unresolved issues.

### Log File Location

```text
C:\Windows\System32\debug\dcpromo.log
```

### Purpose

Provides detailed information about domain controller installation and promotion processes.

### Review For

* Promotion failures
* Replication setup errors
* DNS registration issues
* Service initialization problems

---

## 10. Document Findings

Create a formal health check report.

### Recommended Report Sections

* Domain Controller Name
* Replication Status
* FSMO Role Assignment
* DNS Health
* SYSVOL Status
* Event Log Summary
* DCDIAG Results
* Outstanding Issues
* Recommendations

### Purpose

Maintains operational records and supports proactive maintenance planning.

---

# ✅ Best Practices

## 🔹 Domain Controller Health Check Best Practices

* Perform health checks weekly.
* Create baseline metrics for:

  * Replication latency
  * Logon response time
  * Event log health
* Review Event Viewer regularly.
* Monitor DFSR and SYSVOL replication consistency.
* Verify DNS registration after changes or updates.
* Maintain documentation of all findings and corrective actions.
* Investigate warnings before they escalate into failures.

---

# 📌 Summary

This guide covered essential domain controller health verification procedures, including:

* Checking Active Directory replication
* Verifying SYSVOL synchronization
* Reviewing FSMO role assignments
* Monitoring Event Viewer logs
* Validating DNS SRV records
* Running `dcdiag` diagnostics
* Reviewing DCPROMO logs
* Documenting health check findings

Regular domain controller health checks help maintain Active Directory stability, authentication reliability, and replication integrity across the enterprise environment.
