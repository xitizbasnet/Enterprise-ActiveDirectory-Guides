# 🛠️ How to Remove the Security Tab from Files & Folders for Domain Users via Group Policy (Windows Server 2025)

## 📌 Overview
This guide explains how to remove the **Security tab** from files and folders for domain users using **Group Policy** in Windows Server 2025.

---

## 🖥️ Step 1: Prepare the Client Computer

1. Open the **client computer**  
2. Navigate to the **D Drive**  
3. Create a folder named:

```

Data

```

4. Right-click on the newly created folder **"Data"**  
5. Click **Show more options** → **Properties**  
6. The **Data Properties** popup window will open  
7. Observe that the **Security tab** is currently visible  

---

## 🎯 Objective

We will remove the **Security tab** from the folder properties using Group Policy.

---

## 🖧 Step 2: Configure Group Policy on the AD Server

1. Go to the **AD Server**  
2. Navigate to:

```

Tools → Group Policy Management

````

3. Click on the domain name  
- Example:
  ```
  xitiztechservices.local
  ```

4. Navigate to the OU  
- Example:
  ```
  Domain_Users
  ```

5. Right-click on **Domain_Users**  
6. Select:

 ```
  Create a GPO in this domain, and Link it here...

  ```



---

## 🏷️ Step 3: Create the GPO

- **GPO Name:**
```

Remove Security Tab GPO

```

- Click **OK**

---

## ⚙️ Step 4: Edit the GPO

1. Locate the newly created GPO:
```

Remove Security Tab GPO

```

2. Right-click → **Edit**

3. Navigate to:

```

User Configuration
→ Policies
→ Administrative Templates
→ Windows Components
→ File Explorer
→ Remove Security tab

````

4. Double-click on **Remove Security tab**

5. Configure the setting:
- Select: **Enabled**
- Click: **Apply**
- Click: **OK**

---

## 🔄 Step 5: Apply Group Policy (Server Side)

1. Open **PowerShell**  
2. Run as Administrator  
3. Execute:

```powershell
gpupdate /force
````

---

## 🔄 Step 6: Apply Group Policy (Client Side)

1. Open the **client computer**

2. Open **PowerShell** as Administrator

3. Run:

   ```powershell
   gpupdate /force
   ```

4. Restart the system

---

## ✅ Step 7: Verify the Changes

1. Open the **client computer**

2. Navigate to the **D Drive**

3. Search for the folder:

   ```
   Data
   ```

4. Right-click on the folder **"Data"**

5. Click **Show more options** → **Properties**

6. The **Data Properties** popup window will open

✅ The **Security tab is now removed**

---

## 📎 Notes

* This policy applies to **user configurations**, so it affects domain users linked to the OU.
* Ensure the correct OU is targeted for the policy to take effect.
* A system restart may be required for changes to fully apply.

---

## 🎉 Result

The **Security tab** is successfully hidden from files and folders for domain users using Group Policy in Windows Server 2025.

---
