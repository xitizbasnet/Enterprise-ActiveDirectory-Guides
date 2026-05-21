# How to Remotely Find the Currently Logged-In User on a Specific Computer from a Domain Controller (Windows Server 2025)

## 📘 Overview

This guide explains how to remotely identify the currently logged-in user on a domain-joined client computer using **Windows Server 2025 Domain Controller** and **Windows PowerShell**.

This method is useful for:

* IT administration
* User session monitoring
* Remote support
* Device management within an Active Directory domain

---

# 🖥️ Environment Details

| Component            | Details                   |
| -------------------- | ------------------------- |
| Domain Controller OS | Windows Server 2025       |
| Domain Name          | `xitiztechservices.local` |
| Client OS            | Windows 11 Pro            |
| Client Computer Name | `accountpc`               |
| Logged-In User       | `xitizbasnet`             |

---

# 🔍 Step 1: Verify the Client Computer Name

## On the Client Computer

Navigate to:

```text
Settings > System > About
```

Look under **Device Specifications**.

Example:

```text
Device Name: accountpc
```

Current logged-in username:

```text
xitizbasnet
```

---

# 🖥️ Step 2: Open Server Manager on Domain Controller

On the **Windows Server 2025 Domain Controller**:

1. Open:

```text
Server Manager
```

2. From the **Dashboard**, select:

```text
Add other servers to manage
```

---

# ➕ Step 3: Add the Client Computer to Server Manager

A new window titled **Add Servers** will appear.

## Perform the Following:

1. Under:

```text
Name (CN)
```

2. Click:

```text
Find Now
```

3. You will see the list of domain-joined computers.

Example:

```text
Name: accountpc
Operating System: Windows 11 Pro
```

4. Select the computer.

5. Move the computer to the right-side panel:

```text
Selected Computers
```

6. Click:

```text
OK
```

---

# 📋 Step 4: Access the Added Computer

Return to:

```text
Server Manager > Dashboard
```

Then navigate to:

```text
All Servers
```

You should now see the client computer details.

Example:

| Field         | Value                                                    |
| ------------- | -------------------------------------------------------- |
| Name          | `accountpc`                                              |
| IPv4 Address  | `192.168.1.11`                                           |
| Manageability | `Online - Cannot manage a client-based operating system` |

---

# ⚡ Step 5: Open Remote PowerShell Session

1. Select the computer:

```text
accountpc
```

2. Right-click the computer.

3. Select:

```text
Windows PowerShell
```

A remote PowerShell session will open.

Example prompt:

```powershell
[accountpc.xitiztechservices.local]: PS C:\Users\Administrator\Documents>
```

---

# 👤 Step 6: Find the Currently Logged-In User

Run the following command:

```powershell
query user
```

---

# ✅ Expected Output

Example result:

```text
 USERNAME              SESSIONNAME        ID  STATE   IDLE TIME  LOGON TIME
 xitizbasnet           console             1  Active      none    8/21/2025 9:15 AM
```

This output displays:

* Current logged-in username
* Session status
* Login date and time

---

# 📝 Summary

Using **Server Manager** and **Remote PowerShell** from **Windows Server 2025**, administrators can remotely determine which user is currently logged into a domain-joined Windows client computer.

---

# 🛠️ Commands Used

## Query Logged-In User

```powershell
query user
```

---

# 📌 Notes

> ⚠️ Remote PowerShell access and proper administrative permissions are required.

> 💡 Ensure the client computer is online and domain-joined before attempting the remote connection.

---

# ✅ Result

Successfully identified the currently logged-in user on:

```text
Computer Name: accountpc
Logged-In User: xitizbasnet
```

---

Thank you.
