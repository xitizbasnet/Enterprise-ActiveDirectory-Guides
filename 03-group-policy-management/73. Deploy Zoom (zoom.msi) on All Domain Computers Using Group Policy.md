# 📦 Deploy Zoom (zoom.msi) on All Domain Computers Using Group Policy  
**Windows Server 2025 Deployment Guide**

---

## 🧾 Overview
This guide explains how to deploy the Zoom Workplace desktop application (`.msi`) to all domain computers using Group Policy in a Windows Server 2025 environment.

---

## ⬇️ Step 1: Download Zoom MSI Installer

Download the Zoom application `.msi` file from the following link:

🔗 https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0060407.

### 📌 File Selection
Download the file named:

> **Zoom Workplace desktop app for meeting (64-bit) - MSI installer**

---

## 🔍 Step 2: Verify the Installer File

After downloading, locate the file in the **Downloads** folder:

- File name: `ZoomInstallerFull`

### ✅ Verification Steps:
1. Right-click on `ZoomInstallerFull`
2. Click **Properties**
3. Check the file type:

> ✔️ **Type of file:** Windows Installer Package (`.msi`)

---

## 📁 Step 3: Prepare Shared Deployment Folder

### 🖥️ Environment Assumption:
- `Local Disk (C:)` → Operating System  
- `Local Disk (D:)` → Data Storage  

### 📂 Create Deployment Directory:
1. Open **D: drive**
2. Create a new folder:
```

DeployZoom

```
3. Copy the file `ZoomInstallerFull` into this folder

---

## 🌐 Step 4: Configure Folder Sharing

1. Right-click on `DeployZoom` → **Properties**
2. Navigate to **Sharing** tab
3. Click **Advanced Sharing**

### ⚙️ Sharing Configuration:
- ✔️ Tick: **Share this folder**
- Click **Permissions**
- Select: **Everyone**
- ✔️ Allow: **Read**

4. Click:
```

Apply → OK → Apply → OK

```

### 📌 Copy Network Path:
Example:
```

\adserver2025\DeployZoom

```

Click **Close**

---

## 🛠️ Step 5: Create Group Policy Object (GPO)

1. Open **Server Manager**
2. Go to:
```

Tools → Group Policy Management

```
3. Select your domain  
Example:
```

xitiztechservices.local

```

4. Navigate to the OU  
Example:
```

Domain_Users

```

### ➕ Create GPO:
1. Right-click the OU
2. Select:
```

Create a GPO in this domain, and link it here...

```
3. Name the GPO:
```

Deploy Zoom MSI File

```
4. Click **OK**

---

## ✏️ Step 6: Configure Software Installation Policy

1. Right-click on:
```

Deploy Zoom MSI File

```
2. Select **Edit**

### 📍 Navigate to:
```

Computer Configuration
└── Policies
└── Software Settings
└── Software Installation

```

### 📦 Add Package:
1. Right-click **Software Installation**
2. Select:
```

New → Package

```
3. Browse using the network path:
```

\adserver2025\DeployZoom

```
4. Select the `.msi` file → Click **Open**

### ⚙️ Deployment Option:
- Select:
```

Assigned

````
- Click **OK**

> ⏳ **Note:** It may take some time for the package to appear.

---

## 📊 Step 7: Verify Package Details

Once added, verify the following:

- **Name:** Zoom  
- **Version:** 6.7  
- **Deployment Status:** Assigned  
- **Source:** `\\adserver2025\DeployZoom`  

---

## 🔄 Step 8: Update Group Policy

### 🖥️ On Server:
1. Open **PowerShell** as Administrator
2. Run:
 ```powershell
 gpupdate /force
````

---

## 💻 Step 9: Apply Policy on Client Computer

1. Open **PowerShell** as Administrator

2. Run:

   ```powershell
   gpupdate /force
   ```

3. When prompted:

   ```
   Click Y to restart
   ```

> ⏱️ The computer will restart within approximately 1 minute.

---

## ✅ Step 10: Verify Installation

After restart:

* Zoom Workplace should be installed automatically
* Desktop shortcut should be visible

---

## 🎉 Result

✔️ Zoom Workplace is successfully deployed on the client computer using Group Policy.

---

## 📌 Notes

* Ensure network path permissions are correctly configured
* Clients must be connected to the domain
* Group Policy replication may take some time in large environments

---

## 🙌 Thank You

Your deployment is now complete.

---
