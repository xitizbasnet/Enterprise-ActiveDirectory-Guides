# 🔐 Disable Password Saving for Domain Users in Microsoft Edge via Group Policy (Windows Server 2025)

## 📌 Overview
This guide explains how to disable password saving in Microsoft Edge for domain users using Group Policy in Windows Server 2025. It ensures users cannot save passwords in the browser, improving organizational security.

---

## 🖥️ Step 1: Verify Settings on Client Computer

1. Go to the client computer.
2. Open **Microsoft Edge**.
3. Navigate to:  
   **Settings > Passwords and Autofill > Microsoft Password Manager**

### 🔍 Observations:
- You will see the option: **"Ask to save passwords"**  
  - This can be manually **enabled or disabled**.
- Another option: **Saved Passwords**
  - Users can manually **add passwords** here.

---

## 🛠️ Step 2: Configure Group Policy on Server

1. Open **Server Manager**.
2. Navigate to:  
   **Tools > Group Policy Management**
3. Select your domain name  
   _(e.g., `xitiztechservices.local`)_

4. Go to the Organizational Unit (OU)  
   _(e.g., `Domain_Users`)_

5. Right-click the OU and select:  
   **"Create a GPO in this domain, and Link it here..."**

6. Enter the GPO name:  
```

Deny User sav password don edge

```
7. Click **OK**.

---

## ✏️ Step 3: Edit the Group Policy Object (GPO)

1. Right-click the newly created GPO:  
```

Deny User sav password don edge

```
2. Select **Edit**.

3. Navigate to:
```

User Configuration
└── Administrative Templates
└── Microsoft Edge
└── Password Manager and Protection

````

4. Locate the setting:  
**Enable saving passwords to the password manager**

5. Double-click to edit the setting.

6. Select the radio button:  
**Disabled**

7. Click:
- **Apply**
- **OK**

---

## ⚡ Step 4: Apply Group Policy Updates

### On Server:
1. Open **PowerShell** as Administrator.
2. Run:
```powershell
gpupdate /force
````

### On Client Computer:

1. Open **PowerShell** as Administrator.
2. Run:

   ```powershell
   gpupdate /force
   ```
3. Restart the computer.

---

## ✅ Step 5: Verify Policy on Client Computer

1. Go to the client computer.
2. Open **Microsoft Edge**.
3. Navigate to:
   **Settings > Passwords and Autofill > Microsoft Password Manager**

### 🔒 Expected Results:

* **"Ask to save passwords"** → Automatically **Disabled**
* **Saved Passwords** → Option to **add passwords is disabled**

---

## 📝 Notes

* This policy enforces centralized control over password saving behavior.
* Users will no longer be able to store credentials in Microsoft Edge.

---

## 🎉 Conclusion

You have successfully disabled password saving in Microsoft Edge for domain users using Group Policy in Windows Server 2025.

---

**Thank you**

---
