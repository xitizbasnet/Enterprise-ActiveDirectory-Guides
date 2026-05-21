# 🖥️ How to Backup and Restore Hardware Drivers Before Formatting Windows 11 (Without Any Software)

## 📘 Overview

This guide explains how to **backup and restore hardware drivers** in **Windows 11** without using any third-party software.
The process uses the built-in **PowerShell** and **DISM (Deployment Image Servicing and Management)** command-line utility.

This method is useful before:

* Formatting or reinstalling Windows
* Migrating to a new drive
* Troubleshooting driver-related issues
* Creating a local driver backup repository

---

# 🔹 Part 1 — Backup Hardware Drivers

## 📍 Step 1: Open Device Manager

1. Go to the client computer.
2. Open **Device Manager**.

### ✅ Purpose

Here, we can see all the Windows Device Manager drivers currently installed on the system.

---

## 📍 Step 2: Create a Driver Backup Folder

1. Open **This PC**.

2. Here, we can see the two drives such as:

   * `Local Disk (C:)`
   * `New Volume (D:)`

3. In the `New Volume (D:)` drive:

   * Create a new folder named:

```text
DriversBackup
```

---

## 📍 Step 3: Open PowerShell as Administrator

1. Open **PowerShell**.
2. Right-click and select:

```text
Run as Administrator
```

---

## 📍 Step 4: Export Installed Drivers

Paste the following command into PowerShell:

```powershell
dism /online /export-driver /destination:D:\DriversBackup
```

Press:

```text
Enter
```

---

## 📍 Step 5: Verify Successful Driver Backup

After the command executes successfully, the following message will appear:

```text
The operation completed successfully.
```

---

## 📍 Step 6: Verify Exported Driver Files

1. Open **This PC**.
2. Open the folder:

```text
D:\DriversBackup
```

### ✅ Result

Here, we can see a list of folders containing the exported hardware drivers that were backed up using the PowerShell command.

---

# 🔹 Part 2 — Restore / Install Drivers from Backup

## 📍 Step 1: Open Device Manager

1. Open **Device Manager**.
2. Click on:

```text
Action > Add Drivers
```

---

## 📍 Step 2: Browse to the Driver Backup Folder

Under:

```text
Search for drivers in this location
```

Click:

```text
Browse
```

Navigate to:

```text
D:\DriversBackup
```

Click:

```text
OK
```

---

## 📍 Step 3: Include Subfolders

Tick the checkbox:

```text
Include subfolders
```

Then click:

```text
Next
```

---

## 📍 Step 4: Driver Installation Completion

After a moment, a successful notification message will appear:

```text
Drivers successfully installed.
```

Click:

```text
Close
```

---

# ✅ Summary

Using the built-in Windows tools, you can:

* Backup all installed hardware drivers
* Restore drivers after formatting Windows
* Avoid downloading third-party driver software
* Save time during Windows reinstallation

---

# 🛠️ Command Reference

| Command                                                     | Description                                           |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| `dism /online /export-driver /destination:D:\DriversBackup` | Exports all installed drivers to the specified folder |

---

# 📌 Notes

> ⚠️ Ensure the backup folder is stored on a separate partition or external drive before formatting Windows.

> 💡 Administrator privileges are required to run the DISM export command.

> 📁 The exported driver folders should not be modified or renamed.

---

# 🧾 Applicable Systems

* Windows 11
* Windows 10
* Systems with administrative access

---

# 👨‍💻 Author Notes

This procedure uses native Windows tools only and does not require any third-party applications. It is suitable for IT support engineers, system administrators, and desktop support technicians.
