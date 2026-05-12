# REFERENCE & TOOLS

## 📘 Overview

This section provides essential Active Directory administration commands, diagnostic tools, and key network services used for managing and troubleshooting Windows domain environments.

---

# 🧰 Essential PowerShell Commands

## 👤 User Management

### 📌 List All Users

```powershell id="ps1"
Get-ADUser -Filter * | Select SamAccountName
```

**Purpose:** Lists all Active Directory user accounts.

---

### 📌 Create User

```powershell id="ps2"
New-ADUser -Name 'John Doe' -Path 'OU=Users,DC=yourdomain,DC=com'
```

**Purpose:** Creates a new user account in a specified Organizational Unit (OU).

---

### 📌 Reset User Password

```powershell id="ps3"
Set-ADUser -Identity username -AccountPassword (ConvertTo-SecureString 'P@ssw0rd!')
```

**Purpose:** Resets the password for a specified user account.

---

## 👥 Group Management

### 📌 List Group Members

```powershell id="ps4"
Get-ADGroupMember -Identity 'GroupName'
```

**Purpose:** Displays all members of a specified Active Directory group.

---

### 📌 Add Members to Group

```powershell id="ps5"
Add-ADGroupMember -Identity 'GroupName' -Members user1, user2
```

**Purpose:** Adds users to a security or distribution group.

---

## 🔄 Replication & Directory Health

### 📌 Check Replication Metadata

```powershell id="ps6"
Get-ADReplicationPartnerMetadata -Target DC1
```

**Purpose:** Displays replication status and metadata for a domain controller.

---

## 🔁 Group Policy Management

### 📌 Force GPO Update

```powershell id="ps7"
Invoke-GPUpdate -Computer ComputerName -Force
```

**Purpose:** Forces immediate Group Policy refresh on a target computer.

---

## 🏢 Organizational Units (OU)

### 📌 List All OUs

```powershell id="ps8"
Get-ADOrganizationalUnit -Filter * | Select Name, Path
```

**Purpose:** Displays all Organizational Units in Active Directory.

---

# 🧪 Diagnostic Tools & Commands

## 🖥️ Domain Controller Diagnostics

* `dcdiag /v`
  → Comprehensive domain controller diagnostics

* `repadmin /replicate`
  → Force replication between domain controllers

* `repadmin /showrepl`
  → Display replication status

---

## 🔐 Authentication & Domain Tools

* `netdom query fsmo`
  → Display FSMO role holders

* `gpresult /h report.html`
  → Generate Group Policy Results report

* `gpupdate /force`
  → Force immediate Group Policy update

* `nltest /dsgetdc:yourdomain.com`
  → Test domain controller discovery and connectivity

* `klist`
  → Display Kerberos authentication tickets

---

## 🛠️ Active Directory Administration

* `adsiedit.msc`
  → Direct Active Directory schema and object editing tool

---

# 🌐 Useful Ports & Services

## 📡 Active Directory Network Ports

| Port      | Service        | Purpose                          |
| --------- | -------------- | -------------------------------- |
| 53        | DNS            | Domain Name System resolution    |
| 88        | Kerberos       | Authentication service           |
| 135       | RPC Mapper     | Remote Procedure Call mapping    |
| 389       | LDAP           | Directory access protocol        |
| 636       | LDAPS          | Secure LDAP (SSL/TLS)            |
| 3268–3269 | Global Catalog | Forest-wide directory searches   |
| 445       | SMB/CIFS       | File sharing and domain services |

---

# 📌 Summary

This reference guide includes:

* Essential PowerShell commands for Active Directory management
* Diagnostic tools for replication, authentication, and GPO troubleshooting
* Key administrative utilities for domain controllers
* Critical network ports required for Active Directory services

These tools and commands are essential for maintaining, troubleshooting, and securing enterprise Active Directory environments.
