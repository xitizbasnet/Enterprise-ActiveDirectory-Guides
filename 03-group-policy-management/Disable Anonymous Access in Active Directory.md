# 🔐 Disable Anonymous Access in Active Directory

## 📌 Overview
Anonymous access allows users to view resources or gain the same access as the *Everyone* group in Active Directory without signing in. While this might have been useful for older systems, it is rarely needed today and can introduce security vulnerabilities if left enabled.

Disabling anonymous access ensures that only authenticated users can access Active Directory data and shared resources, thereby reducing potential security risks.

---

## 🎯 Objective
- Restrict unauthorized (anonymous) access to Active Directory resources  
- Improve overall domain security posture  
- Ensure access is limited to authenticated users only  

---

## ⚙️ Procedure

Follow the steps below to disable anonymous access using Group Policy:

### 1. Open Group Policy Management Console (GPMC)
- Launch the **Group Policy Management Console (GPMC)** on your domain controller or management workstation.

### 2. Edit the Domain Group Policy Object (GPO)
- Select your **Domain GPO**
- Click **Edit**

### 3. Navigate to Security Settings
Go to the following path:

```

Group Policy Management Editor
└── Computer Configuration
└── Policies
└── Windows Settings
└── Security Settings
└── Local Policies
└── Security Options

```

### 4. Configure the Policy Setting
- Locate the policy:
```

Network access: Let Everyone permissions apply to anonymous users

```
- Set the value to:
```

Disabled

```
- Click **OK** to apply the change

---

## 🛡️ Security Impact
- ✅ Prevents anonymous users from inheriting *Everyone* group permissions  
- ✅ Reduces exposure of sensitive Active Directory data  
- ✅ Strengthens authentication enforcement across the domain  

---

## ⚠️ Notes
- This setting is recommended for modern environments and aligns with security best practices  
- Ensure no legacy applications depend on anonymous access before applying this change  

---

## 📎 Summary
Disabling anonymous access is a simple yet effective security measure that ensures only authenticated users can interact with Active Directory resources, helping protect your environment from unauthorized access.

