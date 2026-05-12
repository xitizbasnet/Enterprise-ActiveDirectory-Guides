# 🛠️ IT Infrastructure Documentation  
## Fixing Google Chrome ADMX & ADML Template Error in Group Policy  
📅 Date: 06/26/2025  
🏢 Department: IT Team  
🔐 Domain: INFRA & SECURITY  
📌 Category: Group Policy / ADMX Template Management  

---

# 🚨 Issue Summary

An error occurs when accessing the Group Policy Editor due to a missing or improperly configured Google Chrome administrative template file.

---

## ❌ Error Message

> **An appropriate resource file could not be found for file**  
`C:\Windows\PolicyDefinitions\chrome.admx (error = 2): The system cannot find the file specified.`

---

## ⚠️ Root Cause

This issue indicates one or more of the following:

- The `chrome.admx` file is missing from the local `PolicyDefinitions` directory  
- The corresponding language resource file `chrome.adml` is missing  
- The `.adml` file is not placed in the correct language folder (e.g., `en-US`)  
- ADMX/ADML version mismatch between files  

---

# 🧩 Resolution Procedure

---

## ✅ Step 1: Download Latest Google Chrome ADMX Templates

1. Visit the official Google Chrome Enterprise Policy site:  
   https://chromeenterprise.google/policies/

2. Download the latest **Google Chrome Enterprise Bundle (.zip file)**

3. Extract the downloaded archive

---

### 📁 File Locations After Extraction

- **ADMX File Location:**  
  `C:\Users\xitiz.basnet\Downloads\GoogleChromeEnterpriseBundle64\Configuration\admx`

- **ADML File Location:**  
  `C:\Users\xitiz.basnet\Downloads\GoogleChromeEnterpriseBundle64\Configuration\admx\en-US`

---

## 📦 Step 2: Deploy ADMX and ADML Files

### 📌 Copy ADMX File

Copy:
- `chrome.admx`

To either:

```

C:\Windows\PolicyDefinitions\

```

OR (Recommended for domain environments):

```

\xitiztechservices.local\SYSVOL\xitiztechservices.local\Policies\PolicyDefinitions

```

---

### 📌 Copy ADML File

Copy:
- `chrome.adml`

To either:

```

C:\Windows\PolicyDefinitions\en-US\

```

OR:

```

\xitiztechservices.local\SYSVOL\xitiztechservices.local\Policies\PolicyDefinitions\en-US

```

---

### 🌍 Language Note

> Replace `en-US` with your system’s actual language folder if different (e.g., `en-GB`, `fr-FR`, etc.)

---

## 🔄 Step 3: Verify Group Policy Functionality

1. Open:
   - `gpedit.msc` (Local Group Policy Editor)  
   - OR Group Policy Management Console (GPMC)

2. Confirm the error no longer appears

3. Navigate to:

```

Administrative Templates > Google > Google Chrome

````

4. Verify Chrome policy templates are successfully loaded

---

# 📌 Additional Notes

### ⚠️ Error Code Explanation

- **Error Code 2 = File Not Found**
  - Missing `.admx` file in PolicyDefinitions
  - Missing `.adml` file in language folder
  - Mismatched template versions

---

### 🔗 Important Requirement

Both files are required:

- `.admx` → Policy definition file  
- `.adml` → Language resource file  

> ❗ If either file is missing, Group Policy will fail to load Chrome templates correctly.

---

# 🧪 Optional: Check System Language Folder

To confirm correct language directory:

### ▶️ PowerShell Command:
```powershell
Get-WinSystemLocale
````

### 📌 Example Output:

```
en-US
```

### 📁 Resulting Path:

```
C:\Windows\PolicyDefinitions\en-US\
```

---

# 🏁 End of Document
