# 🧹 Auto Delete Temporary Files Using GPO (Storage Sense) – Windows Server 2025

![Windows Server](https://img.shields.io/badge/Windows%20Server-2025-blue)
![GPO](https://img.shields.io/badge/Group%20Policy-Configured-success)
![Automation](https://img.shields.io/badge/Automation-Enabled-brightgreen)

---

## 📑 Table of Contents

* [Overview](#-overview)
* [Prerequisites](#-prerequisites)
* [Understanding Temporary Files](#-understanding-temporary-files)
* [Step 1: Verify Temp Files on Client Machines](#-step-1-verify-temp-files-on-client-machines)
* [Step 2: Create a Group Policy Object (GPO)](#-step-2-create-a-group-policy-object-gpo)
* [Step 3: Configure Storage Sense via GPO](#-step-3-configure-storage-sense-via-gpo)
* [Step 4: Apply Group Policy Updates](#-step-4-apply-group-policy-updates)
* [Step 5: Verify Policy on Client Machines](#-step-5-verify-policy-on-client-machines)
* [Best Practices](#-best-practices)
* [Conclusion](#-conclusion)

---

## 📌 Overview

This guide explains how to automatically delete temporary files on all domain-joined computers using **Group Policy (GPO)** and **Storage Sense** in **Windows Server 2025**.

By implementing this configuration:

* Temporary system and user files are cleaned automatically
* Disk space usage is optimized across all domain computers
* Manual cleanup tasks are eliminated

---

## ⚙️ Prerequisites

Ensure the following before proceeding:

* ✅ Windows Server 2025 (Active Directory Domain Controller)
* ✅ Domain-joined client computers
* ✅ Administrative privileges
* ✅ Group Policy Management Console (GPMC) installed

---

## 📂 Understanding Temporary Files

Windows stores temporary files in two main locations:

| Type        | Location                                 |
| ----------- | ---------------------------------------- |
| System Temp | `C:\Windows\Temp`                        |
| User Temp   | `C:\Users\<Username>\AppData\Local\Temp` |

These files accumulate over time and can consume significant disk space if not managed.

---

## 🔍 Step 1: Verify Temp Files on Client Machines

Before applying the policy, confirm the existence of temporary files.

### 1. Check System Temp Files

* Open **File Explorer**
* Navigate to:

```bash
C:\Windows\Temp
```

---

### 2. Check User Temp Files

* Press `Win + R` to open **Run**
* Type:

```bash
%temp%
```

* Click **OK**

This opens:

```bash
C:\Users\<Username>\AppData\Local\Temp
```

---

## 🛠️ Step 2: Create a Group Policy Object (GPO)

1. Log in to your **Active Directory Server**
2. Open:

```
Server Manager → Tools → Group Policy Management
```

3. Navigate to your domain:

   ```
   YourDomain.local
   ```

4. Select the target OU (e.g., `Domain Computers`)

5. Right-click the OU → Select:

   ```
   Create a GPO in this domain, and Link it here...
   ```

6. Name the GPO:

```text
Auto Delete Temp Files GPO
```

7. Click **OK**

---

## ⚙️ Step 3: Configure Storage Sense via GPO

1. Right-click the newly created GPO → Click **Edit**

2. Navigate to:

```
Computer Configuration
 └── Policies
     └── Administrative Templates
         └── System
             └── Storage Sense
```

---

### 🔧 Configure Required Policies

#### 1. Enable Storage Sense

* Policy: **Allow Storage Sense**
* Set to: `Enabled`

---

#### 2. Enable Temporary File Cleanup

* Policy: **Allow Storage Sense Temporary Files Cleanup**
* Set to: `Enabled`

---

#### 3. Configure Cleanup Schedule

* Policy: **Configure Storage Sense Cadence**
* Set to: `Enabled`

Inside the policy:

* **Run Storage Sense:** `Every day`

---

## 🔄 Step 4: Apply Group Policy Updates

### On the Domain Controller

Open **PowerShell (Admin)** and run:

```powershell
gpupdate /force
```

---

### On Client Computers

Open **PowerShell (Admin)** and run:

```powershell
gpupdate /force
```

---

## 🔍 Step 5: Verify Policy on Client Machines

1. Restart the client computers
2. After reboot:

   * Storage Sense should run automatically
   * Temporary files will be deleted based on the configured schedule

---

## 💡 Best Practices

* 🕒 Schedule cleanup during off-peak hours to reduce performance impact
* 🧪 Test the GPO on a small OU before deploying domain-wide
* 📊 Monitor disk usage improvements after deployment
* 🔐 Ensure proper permissions are maintained for system directories

---

## ✅ Conclusion

By configuring **Storage Sense via Group Policy**, administrators can automate the cleanup of temporary files across all domain computers. This improves system performance, reduces storage issues, and simplifies IT maintenance.

---

**🎯 Result:** Fully automated temp file cleanup across your domain environment.

---
