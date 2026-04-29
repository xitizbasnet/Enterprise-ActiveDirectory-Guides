# 📦 Deploy Program EXE via Group Policy (Windows Server 2022)

## 🧾 Overview
This guide explains how to deploy an `.exe` application (e.g., WinRAR) to all domain computers using **Group Policy** in **Windows Server 2022**.

---

## 🖥️ Step 1: Prepare the Application on the AD Server

1. Go to the **AD Server**.

2. Assume the server has:
   - `Local Disk (C:)` → Operating System  
   - `Local Disk (D:)` → Data Storage  

3. In `Local Disk (D:)`, ensure the **WinRAR executable file** is available.

4. To confirm the file type:
   - Right-click on the **WinRAR file**
   - Select **Properties**
   - Verify:
     ```
     Type of file: Application (.exe)
     ```

---

## 📁 Step 2: Create Shared Folder

1. Create a new folder:

 ```
D:\Program

```

2. Move the **WinRAR.exe** file into this folder.

3. Share the folder:
- Right-click `Program` → **Properties**
- Go to **Sharing** tab → **Advanced Sharing**
- ✔️ Check **"Share this folder"**

4. Configure permissions:
- Click **Permissions**
- Select **Everyone**
- ✔️ Enable:
  - Full Control  
  - Change  
  - Read  
- Click **Apply → OK → Apply → OK**

5. 📌 **Note:** Copy the network path:
```

\adserver\program

````

---

## 📝 Step 3: Create PowerShell Deployment Script

1. Open **Notepad**.

2. Paste the following script:

```powershell
$path = 'C:\Program Files (x86)\winrar'
if (-not (Test-Path -Path $path)) {
 $filePath = '\\adserver\program\winrar.exe'
 $report   = '\\adserver\program\report.txt'
 Start-Process -FilePath $filePath -ArgumentList '/S'
 Add-Content -Path $report -Value "$(hostname) `t`t$(Get-Date)"
}
else {}
````

3. Save the file as:

   ```
   Filename: installwinrar.ps1
   Save as type: All Files
   ```

4. Save location:

   ```
   D:\Program
   ```

5. ✅ Verify contents of folder:

   * `winrar.exe`
   * `installwinrar.ps1`

---

## ⚙️ Step 4: Configure Group Policy Object (GPO)

1. Open **Server Manager**.

2. Navigate:

   ```
   Tools → Group Policy Management
   ```

3. Select your domain:

   ```
   Example: xitiztechservices.local
   ```

4. Go to the OU:

   ```
   Example: Domain_Users
   ```

5. Right-click → Select:

   ```
   "Create a GPO in this domain, and Link it here..."
   ```

6. Name the GPO:

   ```
   Deploy WinRAR program
   ```

---

## ✏️ Step 5: Edit GPO and Add Startup Script

1. Right-click the GPO:

   ```
   Deploy WinRAR program → Edit
   ```

2. Navigate:

   ```
   Computer Configuration → Policies → Windows Settings → Scripts (Startup/Shutdown)
   ```

3. Select:

   ```
   Startup → Right-click → Properties
   ```

4. Switch to:

   ```
   PowerShell Scripts tab
   ```

5. Click **Add**.

6. File Explorer will open:

   ```
   \\adserver.local\SysVol\adserver.local\Policies\{bhgsfsdfgsdf121-asdas2151-asdasd1155}\Machine\Scripts\Startup
   ```

7. Paste the file:

   ```
   installwinrar.ps1
   ```

8. Select the script and click **Open**.

9. Confirm details:

   ```
   Script Name: installwinrar.ps1
   ```

10. Click:

```
OK → Apply → OK
```

---

## 🔄 Step 6: Update Group Policy (Server)

1. Open **PowerShell** as Administrator.

2. Run:

   ```powershell
   gpupdate /force
   ```

---

## 💻 Step 7: Apply Policy on Client Computer

1. Go to a **client computer**.

2. Open **PowerShell** as Administrator.

3. Run:

   ```powershell
   gpupdate /force
   ```

4. Restart the computer.

---

## 📦 Step 8: Verify Installation

1. Open:

   ```
   Control Panel → Programs and Features
   ```

2. Wait a moment.

3. ✅ WinRAR should install silently.

---

## 📊 Step 9: Verify Deployment Report

1. Go back to the **AD Server**.

2. Navigate:

   ```
   D:\Program
   ```

3. Locate file:

   ```
   report.txt
   ```

4. This file contains:

   * PC Name
   * Date & Time of installation

---

## ✅ Result

* WinRAR is deployed silently to all domain computers.
* Installation logs are recorded centrally.

---

## 📌 Notes

* Ensure network sharing permissions are correctly configured.
* Confirm client machines can access the shared path.
* Silent installation switch `/S` must be supported by the `.exe`.

---

## 🙏 Thank You

