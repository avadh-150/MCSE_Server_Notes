
---
# 📁 Mapped Network Drive & Storage Quota Configuration


- Automatically map a **network drive** for domain users using **Group Policy (GPO)**
    
- Enforce a **storage quota** on a shared folder using **File Server Resource Manager (FSRM)**

---

## 🔹 Part 1: Map a Network Drive Using Group Policy (GPO)

This section maps a shared folder automatically when users log in.

---

### ✅ Step 1: Open Group Policy Management

1. Click **Start**
    
2. Type `gpmc.msc`
    
3. Press **Enter**
    

---

### ✅ Step 2: Create a New GPO

1. Right-click your domain (example: `forward.in`)
    
2. Select **Create a GPO in this domain, and Link it here**
    
3. Name the GPO:  
    **`Mapped Drive`**
    
4. Click **OK**
    
---

### ✅ Step 3: Edit the GPO

1. Right-click **Mapped Drive** → **Edit**
    
2. Navigate to:
    

```
User Configuration
 └── Preferences
     └── Windows Settings
         └── Drive Maps
```

---

### ✅ Step 4: Create the Drive Mapping

1. Right-click → **New → Mapped Drive**
    
2. Configure as follows:
    

| Setting          | Value       |
| ---------------- | ----------- |
| **Action**       | Create      |
| **Location**     | `\\DC\data` |
| **Drive Letter** | D:          |
| **Label As**     | Data        |

3. Click **Apply → OK**
    

---

### ✅ Step 5: Apply Policy on Client Machine

On the client PC:

```cmd
gpupdate /force
```

🔁 Log out and log back in  
📂 Open **This PC** → Drive **Z:** should appear

---

## 🔹 Part 2: Set Storage Quota Using FSRM

This ensures users **cannot exceed a defined storage limit**, even if the disk has free space.

---

### ✅ Step 1: Open File Server Resource Manager

1. Open **Server Manager**
    
2. Go to **Tools → File Server Resource Manager**
    

---

### ✅ Step 2: Create a Quota Template (Recommended)

1. Expand **Quota Management → Quota Templates**
    
2. Right-click → **Create Quota Template**
    
3. Configure:
    

|Setting|Value|
|---|---|
|**Template Name**|100 MB Limit|
|**Space Limit**|100 MB|
|**Quota Type**|Hard Quota|

🚫 Hard Quota = user **cannot** exceed the limit

---

### ✅ Step 3: Apply Quota to Shared Folder

1. Right-click **Quotas → Create Quota**
    
2. Set **Quota Path**:  
    `C:\data`
    
3. Select **Derive properties from quota template**
    
4. Choose **100 MB Limit**
    
5. Click **Create**
    

---

### ✅ Step 4: Verify from Client Side

- Open mapped drive **D:** on client PC
    
- Drive size will show **100 MB total**
    
- User cannot store more than 100 MB ❌
    

✔️ Quota works **regardless of actual disk size**

---

## 📊 Tools & Commands Summary

|Purpose|Tool|Command / Path|
|---|---|---|
|Group Policy Management|GPMC|`gpmc.msc`|
|Force Policy Update|CMD|`gpupdate /force`|
|Storage Quota|FSRM|Server Manager → Tools|

---
