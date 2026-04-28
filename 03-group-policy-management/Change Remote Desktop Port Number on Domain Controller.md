# 🛡️ Windows Server 2025 Security Guide

## 🔧 Change Remote Desktop Port Number on Domain Controller

---

## 📌 Overview

This guide provides step-by-step instructions to change the default Remote Desktop (RDP) port on a Windows Server 2025 Domain Controller. It includes configuration via Registry Editor and Windows Defender Firewall, followed by connection validation from a client machine.

---

## 💻 Step 1: Connect to the Server (Client Computer)

1. Open **Run**:
   `Win + R`

2. Type:

   ```bash
   mstsc /admin
   ```

3. This will open the **Remote Desktop Connection**.

4. Enter:

   ```
   Computer: 192.168.1.201
   ```

5. Click **Connect**.

6. Enter the user credentials:

   ```
   Username: admin
   Password: ******
   ```

7. Click **OK**.

8. If a pop-up option appears, click **Yes** to proceed.

---

## 🖥️ Step 2: Modify RDP Port in Registry

1. Open **Server Manager**.

2. Search for **Registry Editor** and open it.

3. Navigate to the following path:

   ```
   HKEY_LOCAL_MACHINE\system\currentcontrolset\control\terminal server\winStations\rdp-tcp
   ```

4. Locate **Port Number**.

5. Right-click → **Modify**.

6. Update the values:

   ```
   Value Data: 11111
   Base: Decimal
   ```

7. Click **OK**.

✅ The new RDP port number is now set to: **11111**

---

## 🔥 Step 3: Configure Windows Defender Firewall

1. Open:

   ```
   Control Panel > Windows Defender Firewall > Advanced Settings
   ```

2. Select **Inbound Rules**.

3. Right-click → **New Rule**.

4. Configure the rule as follows:

### ⚙️ Rule Configuration

* **Rule Type**: Custom
* **Program**: All programs

### 🌐 Protocol and Ports

* **Protocol Type**: TCP
* **Protocol Number**: 6
* **Local Ports**: 11111
* **Remote Ports**: All ports

Click **Next**.

---

### 📍 Scope

* Select **Any IP address** for:

  * Which local IP addresses does this rule apply to?
  * Which remote IP addresses does this rule apply to?

Click **Next**.

---

### ✅ Action

* Select: **Allow the connection**

Click **Next**.

---

### 🌎 Profile

* Select all:

  * ☑ Domain
  * ☑ Private
  * ☑ Public

Click **Next**.

---

### 🏷️ Name

* Enter:

  ```
  Name: New RDP Port: 11111
  ```

Click **Finish**.

---

## 🔄 Step 4: Restart Server

Restart the **Domain Server** to apply the changes.

---

## 🔌 Step 5: Test Remote Connection

### ❌ Attempt Without Port (Expected to Fail)

1. On the client computer, open **Run**:

   ```
   Win + R
   ```

2. Type:

   ```bash
   mstsc /admin
   ```

3. Enter:

   ```
   Computer: 192.168.1.201
   ```

4. Click **Connect**.

⚠️ This will **not connect** to the server.

---

### ✅ Connect Using New Port

1. Try again using the updated port:

   ```
   Computer: 192.168.1.201:11111
   ```

2. Click **Connect**.

3. Enter credentials:

   ```
   Username: admin
   Password: ******
   ```

4. Click **OK**.

---

## 🎉 Completion

You have successfully changed the Remote Desktop port number and verified connectivity using the new port.

---

**Thank you**
