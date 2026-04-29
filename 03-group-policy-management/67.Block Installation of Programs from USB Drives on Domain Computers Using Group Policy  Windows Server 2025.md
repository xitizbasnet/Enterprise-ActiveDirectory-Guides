# 🔒 How To Block Installation of Programs from USB Drives on Domain Computers  
### Using Group Policy (Windows Server 2025)

---

## 📌 Overview
This guide explains how to prevent users from installing applications from USB drives on domain-joined computers using Group Policy in **Windows Server 2025**.

---

## 🧪 Initial Test (Before Applying Policy)

### 🖥️ On the Client Computer

1. Insert a USB pendrive containing an executable file (e.g., `WinRAR`).
2. Double-click the executable file.
3. Attempt to install the application.

✅ **Result:**  
The application will successfully install from the USB drive.

---

## 🚫 Objective

Now we are going to block the installation of applications via USB pendrive.

---

## ⚙️ Configuration Steps (On Active Directory Server)

### 🖥️ Access Group Policy Management

1. Go to the **AD Server**.
2. Open **Server Manager**.
3. Navigate to:  
```

Tools > Group Policy Management

```

---

### 🌐 Create a New GPO

1. Navigate to your domain (e.g., `xitiztechservice.local`).
2. Go to the Organizational Unit (OU) (e.g., `domain_user`).
3. Right-click the OU and select:  
**"Create a GPO in this domain, and link it here..."**
4. Name the GPO:  
```

Deny install program from USB

```
5. Click **OK**.

---

### ✏️ Edit the GPO

1. Select the newly created GPO:  
**Deny install program from USB**
2. Right-click and click **Edit**.
3. Navigate to:

```

Computer Configuration
└── Administrative Templates
└── System
└── Removable Storage Access

````

4. Locate the setting:  
**Removable Disks: Deny Execute Access**
5. Right-click → **Edit**
6. Select: **Enabled**
7. Click **Apply** → **OK**

---

## 🔄 Apply Group Policy Update

### 🖥️ On the Server

1. Open **PowerShell** as Administrator.
2. Run:
```powershell
gpupdate /force
````

---

### 🖥️ On the Client Computer

1. Open **PowerShell** as Administrator.

2. Run:

   ```powershell
   gpupdate /force
   ```

3. Reboot the system.

---

## 🧪 Verification (After Applying Policy)

### 🖥️ On the Client Computer

1. Insert a USB pendrive containing an executable file (e.g., `WinRAR`).
2. Double-click the executable file.
3. Attempt to install the application.

❌ **Expected Result:**
You will see the restriction message:

```
Windows cannot access the specified device, path, or file. 
You may not have the appropriate permissions to access the item.
```

---

## ✅ Summary

* USB-based executable files are blocked from running.
* Prevents unauthorized software installation from removable media.
* Policy is enforced via Active Directory Group Policy.

---

## 🛡️ Notes

* This policy applies to **computer configuration**, so it affects all users on targeted machines.
* Ensure the correct OU is targeted for proper enforcement.
* A system reboot may be required for full policy application.

---


