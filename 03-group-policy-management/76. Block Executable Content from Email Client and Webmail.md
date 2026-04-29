# 🛡️ How to Block Executable Content from Email Client and Webmail  
### Using Group Policy (Attack Surface Reduction) | Windows Server 2025

---

## 📘 Overview
This guide explains how to configure **Attack Surface Reduction (ASR)** rules via **Group Policy** to block executable content originating from email clients and webmail.

---

## ⚙️ Prerequisites
- Windows Server 2025
- Domain environment configured
- Administrative privileges
- Microsoft Defender Antivirus enabled

---

## 🧭 Step 1: Open Group Policy Management

1. Go to **Server Manager**
2. Navigate to:  
   **Tools > Group Policy Management**
3. Select your domain name  
   _Example:_ `xitiztechservices.local`

---

## 📁 Step 2: Create a New GPO

1. Navigate to the Organizational Unit (OU)  
   _Example:_ `Domain_Users`
2. Right-click the OU and select:
   
   **"Create a GPO in this domain, and link it here..."**
4. Enter the GPO name:  
```

Block Executable Content From Email Client and Webmail

```
4. Click **OK**

---

## ✏️ Step 3: Edit the GPO

1. Right-click the newly created GPO:  
**"Block Executable Content From Email Client and Webmail"**
2. Select **Edit**

---

## 🛠️ Step 4: Navigate to ASR Settings

Go to the following path:

```

Computer Configuration

> Administrative Templates
> Windows Components
> Microsoft Defender Antivirus
> Microsoft Defender Exploit Guard
> Attack Surface Reduction

````

---

## 🔍 Step 5: Configure Attack Surface Reduction Rules

1. Locate the setting:  
   **Configure attack surface reduction rules**
2. Right-click and select **Edit**
3. Select the radio button: **Enabled**

> ⚠️ **Note:**  
> The following status IDs are permitted under the value column:  
> - `1` = Block

---

## 🧾 Step 6: Define ASR Rule

1. Under **Options**, find:  
   **Set the state for each ASR rule**
2. Click **Show**

### 🪟 Show Contents Dashboard

Enter the following:

| Value Name (GUID) | Value |
|------------------|------|
| `3B576869-A4EC-4529-8536-B80A7769E899` | `1` |

> 📝 **Note:**  
> GUID used in this tutorial:  
> `3B576869-A4EC-4529-8536-B80A7769E899`  
> This corresponds to:  
> **Block executable content from email client and webmail**

3. Click **OK**
4. Click **Apply > OK**

---

## 💻 Step 7: Apply Policy on Server

1. Open **PowerShell** as Administrator
2. Run the command:

```powershell
gpupdate /force
````

---

## 🖥️ Step 8: Apply Policy on Client Computer

1. Go to the client computer
2. Open **PowerShell** as Administrator
3. Run:

```powershell
gpupdate /force
```

4. Restart the computer

---

## 🧪 Step 9: Verification

1. Go to the client computer
2. Attempt to open an `.exe` file

### 🚫 Expected Result:

A blocked message will appear:

```
This app can't run on your PC
To find a version for your PC, check with the software publisher.
```

---

## ✅ Conclusion

You have successfully configured a Group Policy to block executable content from email clients and webmail using **Attack Surface Reduction (ASR)** rules.

---

## 🙏 Thank You
