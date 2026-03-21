# 📁 Block Access to Folder Options Using Group Policy (Windows Server 2025)

---

## 📌 Overview

This guide provides step-by-step instructions to prevent domain users from accessing **Folder Options** in File Explorer using **Group Policy** in **Windows Server 2025**.

Blocking access to Folder Options helps enforce system policies, restrict user customization, and maintain a standardized environment across client machines.

---

## 🎯 Objective

* Disable access to **Folder Options** from File Explorer
* Apply the restriction to **domain users** via Group Policy
* Ensure changes are enforced across client systems

---

## ⚙️ Prerequisites

Before proceeding, ensure the following:

* 🖥️ Windows Server 2025 with Active Directory Domain Services (AD DS)
* 👤 Domain user accounts organized within an Organizational Unit (OU)
* 🔐 Administrative privileges to modify Group Policy
* 💻 Domain-joined client machines

---

## 🛠️ Configuration Steps

### 1. 🔍 Verify Folder Options on Client Machine

1. Log in to a domain-joined **client computer**
2. Open **This PC**
3. Click the **three-dot menu (⋯)** in the top navigation bar
4. Select **Options**

📌 The **Folder Options** dialog box should appear (this confirms current access)

---

### 2. 🖥️ Open Group Policy Management

1. Log in to the **Domain Controller**
2. Open **Server Manager**
3. Navigate to:

   ```
   Tools → Group Policy Management
   ```

---

### 3. 📂 Create and Link a New GPO

1. In **Group Policy Management**, expand your domain (e.g., `example.local`)

2. Locate the target OU (e.g., **Domain Users**)

3. Right-click the OU and select:

   ```
   Create a GPO in this domain, and Link it here...
   ```

4. Name the GPO:

   ```
   Deny User Access to Folder Options
   ```

5. Click **OK**

---

### 4. ✏️ Edit the Group Policy Object

1. Right-click the newly created GPO

2. Select **Edit**

3. Navigate to:

   ```
   User Configuration
   → Policies
   → Administrative Templates
   → Windows Components
   → File Explorer
   ```

4. Locate the policy:

   ```
   Do not allow Folder Options to be opened from the Options button on the View tab of the ribbon
   ```

5. Configure the setting:

   * Select **Enabled**
   * Click **Apply**
   * Click **OK**

---

## 🔄 Apply Group Policy Updates

### On Domain Controller

1. Open **PowerShell** as Administrator
2. Run:

   ```powershell
   gpupdate /force
   ```

---

### On Client Machine

1. Open **PowerShell** as Administrator

2. Run:

   ```powershell
   gpupdate /force
   ```

3. Restart the computer:

   ```powershell
   Restart-Computer
   ```

---

## ✅ Verification

1. Log in to the **client machine**
2. Open **This PC**
3. Click the **three-dot menu (⋯)** → **Options**

### 🔒 Expected Result

Users should see the following message:

```
This operation has been cancelled due to restrictions in effect on this computer. Please contact your system administrator.
```

---

## 🛠️ Troubleshooting

| Issue                  | Possible Cause           | Solution                 |
| ---------------------- | ------------------------ | ------------------------ |
| Policy not applied     | GPO not linked correctly | Verify OU linkage        |
| No restriction visible | Group Policy not updated | Run `gpupdate /force`    |
| Applies to wrong users | Incorrect OU targeting   | Move users to correct OU |
| Policy conflicts       | Multiple GPOs applied    | Check GPO precedence     |

---

## 📝 Notes

* This policy applies only to **User Configuration**, so it affects users regardless of which machine they log into.
* Ensure proper OU structure for targeted policy enforcement.
* Use **Group Policy Results (gpresult /r)** to verify applied policies if needed.

---

## 🎉 Conclusion

By implementing this Group Policy, administrators can effectively restrict access to Folder Options, enhancing system security and maintaining configuration consistency across domain environments.

---
