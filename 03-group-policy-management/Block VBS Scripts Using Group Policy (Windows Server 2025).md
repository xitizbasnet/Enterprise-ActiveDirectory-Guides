# 🛡️ How to Block VBS Scripts Using Group Policy (Windows Server 2025)

## 📌 Overview
This guide explains how to block VBScript (`.vbs`) files from running on domain-joined client computers using Group Policy in Windows Server 2025. This helps protect domain users from potentially harmful scripts.

---

## 🖥️ Step 1: Test VBScript Execution on Client Computer

1. Go to the client computer.
2. Create a VBScript file on the desktop with the extension `.vbs`.
3. Run the `.vbs` file.

✅ **Expected Result:**  
- The script will run successfully.

---

## 🔧 Step 2: Configure Group Policy on Server

### 📂 Open Group Policy Management

1. Go to **Server Manager**.
2. Navigate to:
```

Tools > Group Policy Management

```
3. Select your domain name  
_Example:_ `xitiztechservices.local`

---

### 📁 Create a New GPO

1. Navigate to the Organizational Unit (OU)  
_Example:_ `Domain_Users`
2. Right-click on the OU.
3. Select:
```

Create a GPO in this domain, and Link it here...

```
4. Enter the GPO name:
```

Block VBS Scripts Running

```
5. Click **OK**.

---

### ✏️ Edit the GPO

1. Right-click on the newly created GPO:
```

Block VBS Scripts Running

```
2. Select **Edit**.

---

## 🔐 Step 3: Configure Software Restriction Policy

### 📍 Navigate to Policy Location

Go to:
```

User Configuration > Policies > Windows Settings > Security Settings > Software Restriction Policies

```

---

### ⚙️ Create New Software Restriction Policies

1. Right-click on:
```

Software Restriction Policies

```
2. Select:
```

New Software Restriction Policies

```

📁 This action will create two folders:
- Security Levels
- Additional Rules

---

### ➕ Create a New Path Rule

1. Click on:
```

Additional Rules

```
2. Right-click and select:
```

New Path Rule

```

---

### 📝 Configure Path Rule

Fill in the following details:

- **Path:**
```

*.VBS

```
- **Security Level:**
```

Disallowed

```

3. Click **Apply**, then **OK**.

✅ You will now see the newly created path rule under **Additional Rules**.

---

### 💾 Apply Changes

Click:

```
Apply > OK
````

---

## 🔄 Step 4: Update Group Policy

### 💻 On the Server

1. Open **PowerShell** as Administrator.
2. Run:

   ```
   gpupdate /force
   ```  
  

### 🖥️ On the Client Computer

1. Open **PowerShell** as Administrator.

2. Run:

   ```
   gpupdate /force
   ```

3. Restart the computer.

---

## 🧪 Step 5: Verify the Policy

1. Go to the client computer.
2. Run the `.vbs` file from the desktop.

❌ **Expected Result:**

A blocked message will appear:

```
Execution of the Windows Script Host failed.
This program is blocked by group policy.
For more information, contact your system administrator.
```

---

## ✅ Conclusion

The Group Policy has been successfully configured to block VBScript execution across domain users, enhancing system security.

---

## 🙌 Thank You
