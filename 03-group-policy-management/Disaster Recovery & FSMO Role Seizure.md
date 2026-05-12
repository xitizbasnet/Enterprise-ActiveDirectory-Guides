# Disaster Recovery & FSMO Role Seizure

## 📘 Overview

**Objective:** Develop and execute disaster recovery procedures

**Estimated Time:** 75 minutes

---

# 🧩 Scenario

The **PDC Emulator domain controller** has failed catastrophically. You must:

* Seize FSMO roles to a healthy domain controller
* Restore domain functionality
* Execute a controlled disaster recovery process

---

# 🚨 Disaster Recovery & FSMO Role Seizure Procedures

## 1. Diagnose FSMO Holder Status

Identify current FSMO role holders.

### Command

```bash id="fsmq1a"
netdom query fsmo
```

### Purpose

Displays all Flexible Single Master Operation (FSMO) role holders in the domain.

### FSMO Roles

* Schema Master
* Domain Naming Master
* RID Master
* PDC Emulator
* Infrastructure Master

---

## 2. Verify Failed Domain Controller Status

Confirm the failed domain controller is permanently unavailable.

### Tasks

* Attempt remote connectivity checks
* Verify service availability
* Check network reachability
* Confirm replication status failure
* Validate system logs (if accessible)

### Documentation Requirement

Record:

* Failure symptoms
* Diagnostic attempts
* Time of failure
* Recovery attempts

### Purpose

Ensures FSMO seizure is justified and not premature.

---

## 3. Identify Healthy Domain Controller

Select a stable domain controller to assume FSMO roles.

### Selection Criteria

* Fully synchronized with replication
* Healthy DNS and authentication services
* Stable network connectivity
* No critical event log errors
* Up-to-date SYSVOL and NETLOGON status

### Purpose

Ensures FSMO roles are transferred to a reliable system.

---

# ⚙️ FSMO Role Seizure Process

## 4. Seize PDC Emulator Role

Execute role seizure using `ntdsutil`.

### Steps

```text id="pdcseize1"
ntdsutil
roles
connections
connect to server <Healthy-DC>
quit
seize pdc
```

### Purpose

PDC Emulator handles:

* Password changes
* Time synchronization
* Group Policy updates

---

## 5. Seize RID Master Role

### Command

```text id="ridseize1"
seize rid master
```

### Purpose

Manages allocation of security identifiers (SIDs) within the domain.

---

## 6. Seize Infrastructure Master Role

### Command

```text id="infra1"
seize infrastructure master
```

### Purpose

Maintains object references between domains in multi-domain environments.

---

## 7. Seize Schema Master Role (If Required)

### Command

```text id="schema1"
seize schema master
```

### Important Note

This role is rarely seized and should only be performed during critical recovery scenarios.

### Purpose

Controls Active Directory schema modifications.

---

# 🔍 Post-Seizure Verification

## 8. Verify FSMO Role Transfer

Confirm all roles are now held by the new domain controller.

### Command

```bash id="verifyfsmo1"
netdom query fsmo
```

### Validation Checklist

* All FSMO roles assigned to healthy DC
* No references to failed DC
* No replication errors reported

---

## 9. Check Domain Functionality

Validate Active Directory health across the environment.

### Command

```bash id="dcdiag1"
dcdiag /v
```

### Review Areas

* DNS health
* Replication status
* Authentication services
* SYSVOL and NETLOGON shares
* Kerberos functionality

### Purpose

Ensures domain stability after FSMO role seizure.

---

# 🔄 Recovery & Restoration Planning

## 10. Implement Recovery Strategy

Determine next steps for failed domain controller.

### Options

* Restore from system state backup
* Rebuild as new domain controller
* Decommission permanently

### Considerations

* Backup availability
* Data integrity
* Replication consistency
* Organizational policy

### Purpose

Restores redundancy and strengthens domain resilience.

---

## 11. Document Root Cause Analysis (RCA)

Perform detailed failure analysis.

### RCA Report Should Include

* Cause of failure
* Timeline of events
* Impact assessment
* Recovery actions taken
* Preventive measures

### Purpose

Prevents recurrence and improves future resilience.

---

## 12. Implement Proactive Monitoring

Set up monitoring for FSMO role health.

### Monitoring Focus Areas

* FSMO role availability
* Domain controller health
* Replication status
* Event log alerts
* DNS responsiveness

### Recommended Tools

* PowerShell monitoring scripts
* System Center Operations Manager (SCOM)
* Nagios / Zabbix / PRTG
* Windows Event Forwarding

### Purpose

Enables early detection of critical infrastructure failures.

---

# ⚠️ Critical Warning

## 🚨 FSMO Role Seizure Warning

* FSMO role seizure must ONLY be performed when the original role holder is permanently unavailable.
* Improper seizure can lead to:

  * Active Directory inconsistencies
  * Authentication failures
  * Replication conflicts
  * Domain instability

### Mandatory Requirements

* Document every action taken
* Validate failure before seizure
* Ensure recovery plan is in place
* Avoid unnecessary role seizure operations

---

# ✅ Best Practices

## 🔹 Disaster Recovery & FSMO Management Best Practices

* Maintain up-to-date system state backups.
* Monitor FSMO role holders continuously.
* Ensure multiple healthy domain controllers exist per domain.
* Regularly test disaster recovery procedures.
* Document all FSMO role changes.
* Use least privilege administrative accounts.
* Validate replication health before role operations.
* Automate alerting for domain controller failures.
* Maintain offline recovery procedures.
* Perform periodic DR simulations.

---

# 📌 Summary

This guide covered disaster recovery procedures for Active Directory, including:

* Diagnosing FSMO role ownership
* Verifying domain controller failure
* Seizing FSMO roles using `ntdsutil`
* Validating domain health post-recovery
* Planning domain controller restoration
* Performing root cause analysis
* Implementing proactive monitoring

Proper FSMO role management ensures continued domain operation during critical infrastructure failures and supports long-term Active Directory resilience.
