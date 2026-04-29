# 📘 How to Deploy Notepad++ to All Domain Computers Using Group Policy (Windows Server 2025)

## 🧾 Overview
This guide explains how to deploy **Notepad++** to all domain computers using **Group Policy** in **Windows Server 2025**. The process uses an `.msi` installer and a shared network location.

---

## 📥 Step 1: Download Notepad++ MSI Installer

Download the **Notepad++.msi** file from the official website:

🔗 https://notepad-plus-plus.org/downloads/

- Select the file named: **Notepad++ - MSI installer**
- After downloading, locate the file in the **Downloads** folder:
  - Example: `NotePad++ 64x`

### 🔍 Verify File Type

- Right-click on `NotePad++ 64x` → **Properties**
- Confirm:
  - **Type of file:** `Windows Installer Package (.msi)`

---

## 📁 Step 2: Prepare Shared Folder on Server

### 🖥️ Open AD Server

Assumption:
- `Local Disk (C:)` → Operating System  
- `Local Disk (D:)` → Data Storage  

### 📂 Create Folder Structure

1. Open **D: drive**
2. Create a new folder:
```

NotePadInstaller

```
3. Copy the downloaded file (`NotePad++ 64x`) into this folder

---

### 🔗 Share the Folder

1. Right-click on `NotePadInstaller` → **Properties**
2. Go to **Sharing** tab → **Advanced Sharing**
3. Configure:
- ✅ Check: **Share this folder**
- Click **Permissions**
  - Select: `Everyone`
  - ✅ Allow: **Read**
4. Click:
```

Apply → OK → Apply → OK

```

### 📌 Copy Network Path

- Example network path:
```

\adserver2025\NotePadInstaller

```
- Click **Close**

---

## ⚙️ Step 3: Configure Group Policy

### 🛠️ Open Group Policy Management

1. Open **Server Manager**
2. Go to:
```

Tools → Group Policy Management

```
3. Select your domain:
- Example: `xitiztechservices.local`

---

### 📁 Create a New GPO

1. Navigate to the OU:
- Example: `Domain_Users`
2. Right-click → Select:
```

Create a GPO in this domain, and link it here...

```
3. Name the GPO:
```

Deploy NotePad++ MSI File

```
4. Click **OK**

---

### ✏️ Edit the GPO

1. Right-click the GPO:
```

Deploy NotePad++ MSI File → Edit

```

2. Navigate to:
```

Computer Configuration
→ Policies
→ Software Settings
→ Software Installation

```

---

### 📦 Add MSI Package

1. Right-click **Software Installation** → **New → Package**
2. Browse to the network path:
```

\adserver2025\NotePadInstaller

````
3. Select the `.msi` file → Click **Open**
4. Choose:
- 🔘 **Assigned**
5. Click **OK**

---

### ⏳ Deployment Processing

> ⚠️ Note: Wait until the package appears. This may take some time.

Once visible, details should include:
- **Name:** NotePad++
- **Version:** 8.8
- **Deployment Status:** Assigned
- **Source:** `\\adserver2025\NotePadInstaller`

---

## 🔄 Step 4: Update Group Policy

### 🖥️ On Server

1. Open **PowerShell** as Administrator
2. Run:
```powershell
gpupdate /force
````

---

### 💻 On Client Computer

1. Open **PowerShell** as Administrator

2. Run:

   ```powershell
   gpupdate /force
   ```

3. When prompted:

   * Type: `Y` to restart

---

## 🔁 Step 5: Client System Restart

* The computer will restart in approximately **1 minute**

---

## ✅ Step 6: Verify Installation

After restart:

* **Notepad++** should be installed automatically
* Desktop shortcut should be visible

---

## 🎉 Completion

You have successfully deployed **Notepad++** to all domain computers using Group Policy.

**Thank you**

---
