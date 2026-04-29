# 🔒 How to Deny Domain Users from Installing Google Chrome Extensions Using Group Policy on Windows Server 2022

## 📌 Overview
This guide explains how to prevent domain users from installing Google Chrome extensions using Group Policy in Windows Server 2022.

By default, users can install extensions from the Chrome Web Store without administrative privileges. This document demonstrates how to restrict that behavior.

---

## 🖥️ Default Behavior (Client-Side Verification)

### Step 1: Verify Current Access
1. Go to the client computer.
2. Open **Google Chrome**.
3. Click on the **three dots (⋮)** on the top-right corner of the user profile.
4. Click on **Extensions** → *Visit Chrome Web Store*.

👉 By default, users can install extensions from the Chrome Web Store without an admin account.

---

### Step 2: Install an Extension (Test)
1. Select any extension.
2. Click **Add to Google Chrome**.
3. Click **Add Extension**.

📥 The extension will download and be added successfully to Google Chrome.

---

## ⚙️ Configure Group Policy (Server-Side)

### Step 3: Open Group Policy Management
1. Go to **Server Manager**.
2. Navigate to **Tools** → **Group Policy Management**.
3. Select your domain (e.g., `xitiztechservices.local`).

---

### Step 4: Create a New GPO
1. Navigate to the OU (e.g., `Domain_Users`).
2. Right-click and select:  
   **"Create a GPO in this domain, and link it here..."**
3. Enter the GPO name:  
   **`Block User Install Extensions From Google Chrome`**
4. Click **OK**.

---

### Step 5: Edit the GPO
1. Right-click the GPO:  
   **"Block User Install Extensions From Google Chrome"**
2. Click **Edit**.

---

### Step 6: Configure Extension Block Policy
Navigate to:

```

User Configuration
└── Administrative Templates
└── Google
└── Google Chrome
└── Extensions

```

1. Locate the setting:  
   **"Configure extension installation blocklist"**
2. Double-click the setting.
3. Select the **Enabled** radio button.

---

### Step 7: Define Blocklist Values
1. Click **Show** under:
   **"Extension IDs the user should be prevented from installing (or * for all)"**
2. In the popup window, enter:

```

Value: *

````

📌 **Note:**  
A blocklist value of `"*"` means:
- All extensions are blocked  
- Unless explicitly allowed via an allowlist

3. Click **OK** → **Apply** → **OK**

---

## 🔄 Apply Group Policy Updates

### Step 8: Update Policy on Server
1. Open **PowerShell** as Administrator.
2. Run:

```powershell
gpupdate /force
````

---

### Step 9: Update Policy on Client

1. Go to the client computer.
2. Open **PowerShell** as Administrator.
3. Run:

```powershell
gpupdate /force
```

4. Restart the computer.

---

## ✅ Verification (Client-Side)

### Step 10: Confirm Restriction

1. Go to the client computer.
2. Open **Google Chrome**.
3. Click the **three dots (⋮)** in the top-right corner.
4. Go to **Extensions** → *Visit Chrome Web Store*.
5. Try to install a new extension.

🚫 You should see a blocked message:

```
"Your admin has blocked this item (ID: gyasdnamsdasdjasdh)"
```

---

## 🎉 Result

Users are now prevented from installing Chrome extensions unless explicitly allowed via Group Policy.

---

## 📝 Notes

* The `"*"` wildcard blocks all extensions globally.
* To allow specific extensions, configure the **Allowlist** policy with approved extension IDs.
* Ensure Chrome Administrative Templates (ADMX files) are installed in Group Policy for these settings to appear.

---

**Thank you**
