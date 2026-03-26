# 🚀 How To Increase Internet Speed on All Domain Computers Using Group Policy (Windows Server 2025)

## 📄 Overview
This guide provides step-by-step instructions to configure a Group Policy Object (GPO) in **Windows Server 2025** to optimize internet speed across all domain computers by modifying the **QoS Packet Scheduler** settings.

---

## 🛠️ Prerequisites
- Active Directory Domain Environment
- Administrative access to the Domain Controller
- Windows Server 2025
- Group Policy Management installed

---

## 📌 Step-by-Step Instructions

### 🔐 Step 1: Access the AD Server
- Go to the **AD Server**

---

### 🧭 Step 2: Open Server Manager
- Open **Server Manager**

---

### ⚙️ Step 3: Open Group Policy Management
- Navigate to:
```

Tools > Group Policy Management

```

---

### 🌐 Step 4: Locate Your Domain
- Go to your domain name  
**Example:**
```

xitiztechservice.local

```

---

### 👥 Step 5: Navigate to Organizational Unit (OU)
- Go to the OU  
**Example:**
```

domain_user

```

---

### ➕ Step 6: Create a New GPO
- Right-click on the OU
- Select:
```

Create a GPO in this domain, and link it here...

```
- Name the GPO:
```

Increase Internet Speed

```
- Click **OK**

---

### ✏️ Step 7: Edit the GPO
- Click on the GPO:
```

Increase Internet Speed

```
- Click **Edit**

---

### 🌍 Step 8: Navigate to QoS Packet Scheduler Settings
Go to:
```

Computer Configuration > Administrative Templates > Network > QoS Packet Scheduler

```

- Search for the setting:
```

Limit reservable bandwidth

```

---

### 🔧 Step 9: Configure Bandwidth Settings
- Right-click:
```

Limit reservable bandwidth

```
- Select **Edit**

#### Apply the following settings:
- Set to:
```

Enabled

```
- Modify:
```

Bandwidth limit (%): 0

```
- Click:
```

Apply > OK

````

---

### 💻 Step 10: Update Group Policy via PowerShell
- Open **PowerShell** as Administrator

- Run the following command:
```powershell
gpupdate /force
````

---

## ✅ Summary

By enabling and configuring the **Limit reservable bandwidth** setting to `0%`, this policy ensures that Windows does not reserve bandwidth unnecessarily, potentially improving internet performance across all domain-joined computers.

---

## ⚠️ Notes

* Ensure this policy is applied to the correct OU for target users/computers.
* Changes may require a system restart or policy refresh to take full effect.
* Test in a controlled environment before deploying organization-wide.

---
