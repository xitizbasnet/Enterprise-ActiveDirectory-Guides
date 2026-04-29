# 🚫 How To Block Remote Desktop Access From IP Address Range Using Windows Firewall (Windows Server 2025)

## 📌 Overview
This guide explains how to block Remote Desktop Protocol (RDP) access from a specific IP address range using Windows Defender Firewall in Windows Server 2025. This is useful for enhancing security by restricting unauthorized access.

---

## 💻 Step 1: Connect to the RDP Server (Client Computer)

1. Open the client computer.
2. Press:
```

Win + R

```
3. Type:
```

mstsc /admin

```
4. This will open the RDP client.

5. Enter:
```

Computer: 192.168.1.201

```
6. Click **Connect**.

---

## 🔐 Step 2: Enter Credentials

- A login prompt will appear:
```

Username: administrator
Password: ********

```

- After entering credentials, the RDP session will open.

---

## ❌ Step 3: Close the RDP Session

- Once verified, close the RDP session.

---

## 🌐 Step 4: Identify Client IP Address

1. Open:
```

Control Panel

```
2. Navigate to:
```

Network and Sharing Center

```
3. Click:
```

Ethernet 0 > Details

```
4. Check the IPv4 Address:
```

Example: 192.168.1.99

```

---

## 🖥️ Step 5: Open AD Server Firewall Settings

1. Open the **AD Server**.
2. Navigate to:
```

Control Panel > All Control Panel Items > Windows Defender Firewall > Advanced Settings

```
3. Click:
```

Inbound Rules

```

---

## ⚙️ Step 6: Create New Firewall Rule

1. Right-click on **Inbound Rules** → Select:
```

New Rule

```
2. Select:
```

Custom

```
3. Click **Next**.

---

## 🔌 Step 7: Configure Program & Protocol

1. Program:
```

All programs

```
Click **Next**

2. Protocol:
```

TCP

```
3. Local Port:
```

Specific Ports: 3389

```
4. Click **Next**

---

## 🌍 Step 8: Define Remote IP Addresses

### 🔹 Add Specific IP
1. Under:
```

Which remote IP addresses does this rule apply to?

```
2. Select:
```

These IP addresses

```
3. Click **Add**
4. Enter:
```

192.168.1.201

```
5. Click **OK**

---

### 🔹 Add IP Address Range

1. Click **Add**
2. Select:
```

This IP address range

```
3. Configure:
```

From: 192.168.1.50
To:   192.168.1.120

```
4. Click **OK**
5. Click **Next**

---

## ⛔ Step 9: Block the Connection

1. Select:
```

Block the connection

```
2. Click **Next**

---

## 🌐 Step 10: Apply Rule to Profiles

- Enable all:
- ✅ Domain
- ✅ Private
- ✅ Public

Click **Next**

---

## 🏷️ Step 11: Name the Rule

1. Enter:
```

Block Remote Desktop

```
2. Click **Finish**

---

## ✅ Step 12: Verify the Rule

- The rule is now created on the AD server.

---

## 🧪 Step 13: Test the Configuration

1. Go back to the client computer.
2. Open RDP again:
```

mstsc

```
3. Try connecting to:
```

192.168.1.201

```

> ❌ The connection will fail, and an error message will appear while connecting to the RDP server.

---

## 📎 Notes

- Port **3389** is the default port for RDP.
- Blocking IP ranges helps prevent unauthorized access attempts.
- Ensure correct IP ranges are configured to avoid blocking legitimate users.

---

## 🙏 Thank You
