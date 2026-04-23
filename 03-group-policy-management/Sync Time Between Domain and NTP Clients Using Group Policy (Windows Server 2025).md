# 🕒 Time Synchronization Guide

## Sync Time Between Domain and NTP Clients Using Group Policy (Windows Server 2025)

---

## 📌 Overview

This document provides step-by-step instructions to configure time synchronization between a domain controller and client machines using **Group Policy** in **Windows Server 2025**.

It ensures all domain-joined systems synchronize their time with a centralized **NTP (Network Time Protocol) server**.

---

## ⚙️ Prerequisites

* Administrative access to the Domain Controller
* Group Policy Management permissions
* Domain-joined client machines

---

## 🖥️ Step 1: Configure NTP Server on Domain Controller

### 🔹 Open Local Group Policy Editor

1. Open **AD Server**

2. Open **PowerShell** → Run as Administrator

3. Type the following command:

   ```powershell
   gpedit.msc
   ```

4. This will open the **Local Group Policy Editor**

---

### 🔹 Navigate to Time Provider Settings

Go to:

```
Local Computer Policy  
└── Computer Configuration  
    └── Policies  
        └── Administrative Templates  
            └── System  
                └── Windows Time Service  
                    └── Time Providers
```

---

### 🔹 Enable Windows NTP Server

1. Find the setting: **Enable Windows NTP Server**
2. Double-click to edit
3. Select:

   * 🔘 **Enabled**
4. Click:

   * ✅ Apply
   * ✅ OK

---

## 🏢 Step 2: Create and Configure Group Policy Object (GPO)

### 🔹 Open Group Policy Management

1. Go to **Server Manager**
2. Navigate to:

   ```
   Tools → Group Policy Management
   ```

---

### 🔹 Create a New GPO

1. Select your domain (e.g., `xitiztechservices.local`)
2. Navigate to the OU (e.g., `Domain_Users`)
3. Right-click → Select:

   ```
   Create a GPO in this domain, and link it here...
   ```
4. Enter GPO Name:

   ```
   NTP Time Server Sync
   ```
5. Click **OK**

---

### 🔹 Edit the GPO

1. Right-click on:

   ```
   NTP Time Server Sync
   ```
2. Click **Edit**

---

## ⚙️ Step 3: Configure NTP Client Settings

### 🔹 Navigate to Time Provider Settings

Go to:

```
Computer Configuration  
└── Policies  
    └── Administrative Templates  
        └── System  
            └── Windows Time Service  
                └── Time Providers
```

---

### 🔹 Configure Windows NTP Client

1. Find:

   ```
   Configure Windows NTP Client
   ```
2. Double-click to edit
3. Select:

   * 🔘 **Enabled**

---

### 🔹 Configure NTP Server Value

Under **Options**:

* **NtpServer**
  👉 *[Note: Enter the Full Domain Name]*

---

### 🔍 How to Get Full Domain Name

1. Go to:

   ```
   This PC → Right-click → Properties
   ```
2. Click:

   ```
   Advanced system settings → Computer Name
   ```
3. Locate:

   ```
   Full Computer Name
   ```

   Example:

   ```
   adserver.local
   ```

---

### 🔹 Apply NTP Server Configuration

Set:

```
NtpServer: adserver.local
```

Then click:

* ✅ Apply
* ✅ OK

---

### 🔹 Enable Windows NTP Client

1. Find:

   ```
   Enable Windows NTP Client
   ```
2. Double-click
3. Select:

   * 🔘 **Enabled**
4. Click:

   * ✅ Apply
   * ✅ OK

---

## 🔄 Step 4: Update Group Policy

### 🔹 On Domain Controller

1. Open **PowerShell** → Run as Administrator
2. Run:

   ```powershell
   gpupdate /force
   ```

---

## 💻 Step 5: Apply Policy on Client Computer

### 🔹 Update Policy

1. Open **PowerShell** → Run as Administrator
2. Run:

   ```powershell
   gpupdate /force
   ```

---

### 🔹 Restart Client Machine

* Restart the computer to apply changes

---

## ✅ Step 6: Verification

After restart:

* Check system time on the client machine
* The time should be **successfully synced with the NTP server**

---

## 🎉 Completion

Time synchronization between the domain controller and client machines is now successfully configured.

---

## 📎 Notes

* Ensure network connectivity between clients and the domain controller
* Verify firewall settings allow NTP traffic (UDP port 123)
* Confirm correct DNS resolution of the NTP server

---

