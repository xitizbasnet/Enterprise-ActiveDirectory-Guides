# Delegation Management & Least Privilege

## 📘 Overview

**Objective:** Implement proper delegation of administrative tasks

**Estimated Time:** 50 minutes

---

# 🧩 Scenario

Implement delegation for the IT support team to:

* Reset user passwords
* Manage user accounts within specific Organizational Units (OUs)

without granting full **Domain Admin** privileges.

---

# 🔐 Delegation Management Procedures

## 1. Create Security Group for IT Support Team

Create a dedicated security group for delegated administrative permissions.

### Example Group Name

```text id="8c3y0r"
IT-Support-Group
```

### Steps

1. Open **Active Directory Users and Computers (ADUC)**.

2. Navigate to the appropriate OU or container.

3. Create a new:

   * **Group Type:** Security
   * **Group Scope:** Global (recommended)

4. Add IT support staff members to the group.

### Purpose

Using groups instead of individual accounts simplifies permission management and auditing.

---

## 2. Open Delegate Control Wizard

Access delegation settings for the target Organizational Unit.

### Steps

1. In **ADUC**, locate the target OU.
2. Right-click the OU.
3. Select:

```text id="0hm8l0"
Delegate Control
```

4. Click **Next**.

### Purpose

The Delegate Control Wizard provides granular administrative delegation without elevated domain-wide access.

---

## 3. Add Delegated Security Group

Assign the IT support security group to the delegation wizard.

### Steps

1. Click **Add**.
2. Select:

```text id="qg7d1s"
IT-Support-Group
```

3. Click **OK**.
4. Click **Next**.

### Purpose

Defines which users or groups will receive delegated permissions.

---

## 4. Delegate Common Administrative Tasks

Grant password reset permissions.

### Steps

1. Select:

```text id="j9r6ya"
Delegate the following common tasks
```

2. Enable:

```text id="7vf6w8"
Reset user passwords and force password change at next logon
```

3. Click **Next**.

### Purpose

Allows IT support staff to assist users with password-related issues.

---

## 5. Add Additional Delegated Tasks

Delegate group membership management permissions.

### Steps

1. Add the following permission:

```text id="p3j9o1"
Modify the membership of a group
```

2. Continue through the wizard.

### Purpose

Allows support staff to manage user group memberships without elevated administrative rights.

---

## 6. Review and Complete Delegation Wizard

Finalize the delegation configuration.

### Steps

1. Review all selected permissions.
2. Click **Finish**.

### Purpose

Applies the delegated permissions to the target OU.

---

# 🔍 Permission Verification

## 7. Verify Delegated Permissions

Review applied permissions on the Organizational Unit.

### Steps

1. Right-click the OU.
2. Select:

```text id="5zv2ny"
Properties
```

3. Open the:

```text id="7i2i1v"
Security
```

tab.

### Verify

* The delegated group appears in the permission list.
* Assigned permissions match organizational requirements.

### Purpose

Confirms proper delegation and security assignment.

---

## 8. Add Additional Permissions (If Needed)

Grant more granular permissions when required.

### Possible Additional Permissions

* Create user objects
* Delete user objects
* Unlock user accounts
* Read/write account properties

### Steps

1. Open **Advanced Security Settings** for the OU.
2. Add custom permissions as needed.

### Purpose

Supports expanded support responsibilities while maintaining controlled access.

---

# 🧪 Delegation Testing & Validation

## 9. Test Delegated Access

Validate delegated administrative capabilities.

### Steps

1. Log in using an IT support account.
2. Attempt to:

   * Reset a user password
   * Modify group membership
   * Unlock user accounts (if delegated)

### Validation Checklist

* Password reset succeeds
* Group modifications succeed
* Access is limited to delegated OU

### Purpose

Confirms delegated permissions function correctly.

---

## 10. Verify Restricted Access

Ensure least privilege boundaries are enforced.

### Confirm IT Support Users CANNOT:

* Modify Group Policy Objects (GPOs)
* Create or manage Domain Controllers
* Modify domain-wide settings
* Access privileged administrative groups
* Change FSMO roles

### Purpose

Ensures delegated users remain within approved administrative scope.

---

# 📝 Documentation & Governance

## 11. Document Delegation Model

Create formal documentation for delegated administration.

### Recommended Documentation Sections

* Delegated Group Name
* OU Scope
* Assigned Permissions
* Business Justification
* Approval Information
* Review Schedule
* Expiration Date (if temporary)

### Purpose

Supports auditing, compliance, and operational governance.

---

# ✅ Best Practices

## 🔹 Delegation & Least Privilege Best Practices

* Always apply the **Principle of Least Privilege**.
* Delegate permissions only as required.
* Use security groups instead of assigning permissions directly to users.
* Implement time-bound delegation for temporary access needs.
* Regularly review delegated permissions and memberships.
* Document all delegations and approval workflows.
* Separate administrative accounts from standard user accounts.
* Monitor delegated activity through auditing and event logs.
* Avoid granting Domain Admin privileges unless absolutely necessary.

---

# 📌 Summary

This guide covered delegation management and least privilege implementation in Active Directory, including:

* Creating delegated security groups
* Using the Delegate Control Wizard
* Assigning password reset and group management permissions
* Verifying OU-level delegated access
* Testing delegated administrative functionality
* Enforcing least privilege restrictions
* Documenting delegation models

Proper delegation improves operational efficiency while reducing security risks associated with excessive administrative privileges.
