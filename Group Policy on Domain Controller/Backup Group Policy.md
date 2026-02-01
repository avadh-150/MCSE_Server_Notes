
---

## 🧠 What does **Backup Group Policy** mean?

**Straight truth** 👇

Backing up a GPO means:

- Saving a **copy of its settings**
    
- So you can **restore** it after:
    
    - Accidental deletion
        
    - Bad configuration
        
    - DC crash
        
    - Junior admin disaster 🫠
        

⚠️ **Backup ≠ Export ≠ Link**  
Backup stores:

- GPO settings
    
- GUID
    
- Version
    
- Permissions (partially)
    

---

## 🛑 Reality Check (Read this carefully)

- ❌ GPO backup does **NOT** include:
    
    - OU links
        
    - WMI filter links
        
- ✅ It **ONLY** backs up the GPO itself
    

If you don’t remember where it was linked, that’s **your fault**, not AD’s 😈

---
## 🛠 METHOD 1: Backup GPO using GUI (Recommended)

---

### ✅ Step 1: Open Group Policy Management

On **Windows Server 2022 DC**:

- `Server Manager`
    
- `Tools`
    
- **Group Policy Management**
    

---

### ✅ Step 2: Navigate to Group Policy Objects

```
Forest
 └── Domains
     └── iforward.in
         └── Group Policy Objects
```

   ![image](https://activedirectorypro.com/wp-content/uploads/2022/06/gpo-backup-select-object.webp)

---

### ✅ Step 3: Backup a Single GPO

- Right-click the **GPO**
    
- Click **Back Up All…**

   ![image](https://activedirectorypro.com/wp-content/uploads/2022/06/gpo-backup-all.webp)

---

### ✅ Step 4: Choose Backup Location

- Select a folder  
    Example:
    
    ```
    D:\GPO_Backup\
    ```
    
- (Best practice: separate disk or network share)
    
	![image](https://activedirectorypro.com/wp-content/uploads/2022/06/gpo-backup-select-folder.webp)

---

### ✅ Step 5: Add Description (DO NOT SKIP)

Example:

```
Backup before USB block changes – 01 Feb 2026
```

👉 This saves you during audits & rollbacks 😤

Click **Back Up** → **OK**

✔️ Done. GPO is backed up.

![image](https://activedirectorypro.com/wp-content/uploads/2022/06/gpo-backup-process.webp)


---

## 🧨 METHOD 2: Backup GPO using **PowerShell** (PRO LEVEL)


![Image](https://user-images.githubusercontent.com/55346298/120389418-adfdc980-c32c-11eb-9dfb-bc43ff5fd311.gif)


---

## 🔁 Restore a GPO from Backup (IMPORTANT)

---
### ✅ Restore OVER Existing GPO

1. Right-click **Group Policy Objects**
    
2. Click **Manage Backups**

	![image](https://activedirectorypro.com/wp-content/uploads/2022/06/select-manage-backups.webp)

3. Select backup

	![image](https://activedirectorypro.com/wp-content/uploads/2022/06/select-gpo-to-restore.webp)

4. Click **Restore**
    
5. Confirm

	![image](https://activedirectorypro.com/wp-content/uploads/2022/06/gpo-restore-success-page.webp)

✔️ GPO comes back with same GUID.

---

## 🧱 Backup vs Restore vs Import (DO NOT CONFUSE)

|Action|Purpose|
|---|---|
|Backup|Save GPO|
|Restore|Revert same GPO|
|Import|Copy settings to another GPO|
|Link|Apply policy|
|Enforce|Force priority|

---

## 🧠 Best Practices (REAL WORLD)

✔️ Backup before **every** change  
✔️ Store backups on **network share**  
✔️ Weekly scheduled PowerShell backup  
✔️ Document linked OUs manually  
✔️ Restrict who can edit GPOs

---
