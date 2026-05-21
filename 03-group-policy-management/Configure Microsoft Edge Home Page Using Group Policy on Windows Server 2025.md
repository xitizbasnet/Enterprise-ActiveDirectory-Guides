# 🌐 Configure Microsoft Edge Home Page Using Group Policy on Windows Server 2025

## 📘 Overview

This guide explains how to configure a default startup page (home page) for **Microsoft Edge** using **Group Policy (GPO)** in **Windows Server 2025** domain environments.

Using this configuration, all client computers connected to the domain will automatically open a predefined website whenever Microsoft Edge starts.

---

# 🖥️ Environment Information

| Component             | Details                   |
| --------------------- | ------------------------- |
| **Domain Controller** | Windows Server 2025       |
| **Domain Name**       | `xitiztechservices.local` |
| **Browser**           | Microsoft Edge            |
| **Policy Type**       | Group Policy Object (GPO) |

---

# 📍 Step 1 — Verify Current Behavior on Client Computer

Go to the **client computer**.

## Open Microsoft Edge

Run the **Microsoft Edge** browser.

Here, we can see that there is currently **no configured startup/home page link**.

> 📌 This confirms that no Group Policy has yet been applied for Microsoft Edge startup pages.

---

# 🛠️ Step 2 — Open Group Policy Management

## On the Domain Controller

Go to the **Domain Controller** server.

### Server Information

* **Operating System:** Windows Server 2025
* **Domain:** `xitiztechservices.local`

---

## Open Server Manager

### Navigation

```text
Server Manager → Tools → Group Policy Management
```

### Detailed Steps

1. Open **Server Manager**
2. Click **Tools**
3. Select **Group Policy Management**

---

# 🏢 Step 3 — Create a New Group Policy Object (GPO)

Inside **Group Policy Management**:

1. Expand the server/domain name
   Example:

```text
xitiztechservices.local
```

2. Select the Organizational Unit (OU)
   Example:

```text
Domain User
```

3. Right-click the OU

4. Select:

```text
Create a GPO in this domain, and Link it here
```

---

# 📝 Step 4 — Configure GPO Name

## GPO Name

Set the GPO name as:

```text
Set Home Page for Microsoft Edge
```

> 💡 Use meaningful naming conventions for easier administration and troubleshooting.

---

# ⚙️ Step 5 — Edit the Group Policy

Right-click the newly created GPO and select:

```text
Edit
```

---

# 📂 Step 6 — Navigate to Microsoft Edge Policies

Go to the following path:

```text
Computer Configuration
 └── Policies
     └── Administrative Templates
         └── Microsoft Edge
             └── Startup, home page and new tab page
```

---

# 🚀 Step 7 — Configure Microsoft Edge Startup Action

## Locate the Policy

Search for the following setting:

```text
Action to take on Microsoft Edge startup
```

---

## Configure the Policy

Double-click the policy to configure it.

### Set the Following:

| Setting        | Value               |
| -------------- | ------------------- |
| Policy State   | ✅ Enabled           |
| Startup Action | Open a list of URLs |

---

## Apply the Configuration

Click:

```text
Apply → OK
```

---

# 🌍 Step 8 — Configure Startup URLs

Under the same settings section, search for:

```text
Sites to open when the browser starts
```

---

## Configure the Policy

### Set the Following:

| Setting      | Value     |
| ------------ | --------- |
| Policy State | ✅ Enabled |

---

## Add Startup URLs

Under:

```text
Options → Sites to open when the browser starts
```

Click:

```text
Show
```

This opens the **Show Contents** popup window.

---

## Enter Website URLs

Inside the **Value** field, enter the URLs you want Microsoft Edge to open automatically.

### Example

```text
www.youtube.com/@XitizBasnet
```

> 📌 You can add multiple URLs if required.

---

## Save the Configuration

Click:

```text
OK
```

to close the **Show Contents** window.

Then click:

```text
Apply → OK
```

to save the Group Policy settings.

---

# 🔄 Step 9 — Update Group Policy on the Domain Controller

Go to Windows Search.

Open:

```text
PowerShell → Run as Administrator
```

Run the following command:

```powershell
gpupdate /force
```

> ✅ This forces the Group Policy to update immediately.

---

# 💻 Step 10 — Update Group Policy on the Client Computer

Now go to the **client computer**.

## Open PowerShell as Administrator

### Navigation

```text
Windows Search → PowerShell → Run as Administrator
```

Run the following command:

```powershell
gpupdate /force
```

---

# 🔁 Step 11 — Restart the Client Computer

Restart the PC to ensure the policy is fully applied.

---

# ✅ Step 12 — Verify the Configuration

After the restart:

1. Open the **client computer**
2. Launch **Microsoft Edge**

Microsoft Edge will automatically open the configured URL:

```text
www.youtube.com/@XitizBasnet
```

---

# 📌 Result

The Microsoft Edge startup page has now been successfully configured through **Group Policy** on **Windows Server 2025**.

All users/computers affected by this GPO will automatically open the specified website when launching Microsoft Edge.

---

# 🧰 Troubleshooting Tips

| Issue                       | Solution                                                            |
| --------------------------- | ------------------------------------------------------------------- |
| Policy not applying         | Run `gpupdate /force` again                                         |
| URL not opening             | Verify the URL format                                               |
| GPO not linked correctly    | Check OU linkage                                                    |
| Client not receiving policy | Verify domain connectivity                                          |
| Edge policy missing         | Ensure Microsoft Edge Administrative Templates (ADMX) are installed |

---

# 📚 Useful Commands

## Force Group Policy Update

```powershell
gpupdate /force
```

## Verify Applied Policies

```powershell
gpresult /r
```

---

# 🔐 Best Practices

* ✅ Use descriptive GPO names
* ✅ Test policies on a small OU before production deployment
* ✅ Document all configured URLs
* ✅ Keep ADMX templates updated
* ✅ Restart client machines after major policy changes

---

# 📖 Notes

> ℹ️ This configuration applies to computers/users within the targeted Organizational Unit (OU).

> ⚠️ Ensure that Microsoft Edge Administrative Templates are installed in the Group Policy Central Store for full policy availability.

---

# 🎯 Conclusion

You have successfully configured a startup homepage for Microsoft Edge using Group Policy in a Windows Server 2025 Active Directory environment.

This method provides centralized browser configuration management across domain-joined systems.

---

# 🙌 Thank You
