# 🖥️ Remotely Remove (Unjoin) a Client Computer from Domain

**Windows Server 2025**

---

## 📌 Overview

This guide provides step-by-step instructions to remotely remove (unjoin/disjoin) a client computer from an Active Directory domain using PowerShell in a Windows Server 2025 environment.

The process involves:

* Identifying the client machine
* Verifying its domain membership
* Executing a remote PowerShell command to remove it from the domain
* Confirming successful disjoin

---

## ⚙️ Prerequisites

Ensure the following requirements are met before proceeding:

* 🔐 Administrative privileges on both the server and client machine
* 🖥️ Remote PowerShell access enabled on the client system
* 🌐 Network connectivity between server and client
* 🧾 Valid domain administrator credentials
* 📂 Client computer exists in Active Directory

---

## 🔍 Step 1: Identify the Client Computer

On the **client machine**:

1. Open **File Explorer**
2. Right-click on **This PC**
3. Select **Properties**
4. Locate the **Full Device Name**, for example:

   ```
   ACCOUNTPC.xitiztechservices.local
   ```

* 🏢 Domain Name: `xitiztechservices.local`
* 💻 Computer Name: `ACCOUNTPC`

---

## 🗂️ Step 2: Verify in Active Directory

On the **Domain Controller / Server**:

1. Open **Server Manager**
2. Navigate to:

   ```
   Tools → Active Directory Users and Computers
   ```
3. Expand your domain:

   ```
   xitiztechservices.local
   ```
4. Navigate to:

   ```
   Organizational Units (OU) → Domain Computers
   ```
5. Locate the client machine:

   ```
   ACCOUNTPC
   ```

---

## 💻 Step 3: Execute Remote PowerShell Command

### 🔑 Open PowerShell as Administrator

1. Right-click **Windows PowerShell**
2. Select **Run as Administrator**

---

### 🧾 Command Syntax

```powershell
$cred = Get-Credential

Invoke-Command -ComputerName <ComputerName> -ScriptBlock {
    Remove-Computer -UnjoinDomainCredential $using:cred `
    -WorkgroupName WORKGROUP `
    -PassThru -Verbose -Restart
}
```

---

### ✏️ Example (Modified for Target Machine)

```powershell
$cred = Get-Credential

Invoke-Command -ComputerName ACCOUNTPC -ScriptBlock {
    Remove-Computer -UnjoinDomainCredential $using:cred `
    -WorkgroupName WORKGROUP `
    -PassThru -Verbose -Restart
}
```

---

## 🔐 Step 4: Provide Credentials

After executing the command:

* A credential prompt will appear
* Enter domain administrator credentials:

```
Username: Administrator
Password: ********
```

* Click **OK**
* Type **Y** and press **Enter** to confirm

---

## 🔄 Step 5: Automatic Restart

* The client computer will automatically restart
* Domain removal will be applied during reboot

---

## ✅ Step 6: Verify Domain Removal

After the client system restarts:

1. Open **File Explorer**
2. Right-click **This PC**
3. Select **Properties**
4. Click:

   ```
   Domain or Workgroup Settings
   ```

### ✔️ Expected Result:

```
Workgroup: WORKGROUP
```

This confirms the system has been successfully removed from the domain.

---

## 🛠️ Troubleshooting

| Issue             | Possible Cause               | Solution                                |
| ----------------- | ---------------------------- | --------------------------------------- |
| Access Denied     | Invalid credentials          | Verify admin credentials                |
| Command fails     | PowerShell remoting disabled | Enable using `Enable-PSRemoting -Force` |
| Machine not found | Incorrect hostname           | Verify computer name                    |
| No restart        | Script interruption          | Manually restart client                 |

---

## 📝 Notes

* Ensure the client machine is powered on during execution
* Firewall settings must allow remote management
* Use FQDN if hostname resolution fails
* Always verify removal in Active Directory after operation

---

## 🎉 Conclusion

You have successfully removed a client computer from the domain remotely using PowerShell in Windows Server 2025. This method is efficient for managing multiple systems without physical access.

---
