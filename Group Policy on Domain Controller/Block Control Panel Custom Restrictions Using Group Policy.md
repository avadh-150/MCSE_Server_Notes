
---
# 🔐 Control Panel Restrictions Using Group Policy (GPO)

---

## 🎯 Objective

- Allow **only specific Control Panel items** for users  
    
    **OR**
    
- Hide **specific Control Panel items** while allowing everything else
    

Policy scope: **User Configuration**

---

## 🛠 Step 1: Open Group Policy Management

1. Press `Win + R`
    
2. Type `gpmc.msc` → Press **Enter**
    
3. Right-click the [iforward.in] → **Create a GPO in this domain, and Link it here...**
    
4. Name the GPO clearly, for example:
    

```
Control Panel Restrictions
```

Bad names cause confusion later. Be explicit. 🧠

---

## ✏️ Step 2: Edit the GPO

1. Right-click the newly created GPO like `Control Panel Restrictions`
    
2. Click **Edit**
    
3. Navigate to:
    

```
User Configuration
 └─ Policies
    └─ Administrative Templates
       └─ Control Panel
```

   ![image](https://cdn.mos.cms.futurecdn.net/P4uN9uwr7V23uSDaBxmuyE-1200-80.jpg.webp)

⚠️ This is **User Configuration**, not Computer Configuration.  

---

## Step 3: Hide Specific Control Panel Items

Use this when you want **maximum restriction**.

1. Open **Hide specified Control Panel items**
    
2. Set it to **Enabled**

![image](https://cdn.mos.cms.futurecdn.net/JsD428uLea3sQPjicvHri5-1200-80.jpg.webp)


3. Click **Show…**
    
4. Add the canonical names you want users to see
    

### ✅ Example Canonical Names

```
Microsoft.AdministrativeTools
Microsoft.DefaultPrograms
Microsoft.AutoPlay
Microsoft.UserAccount
Microsoft.DeviceManager
```

## 🚫 Control Panel Items – Restriction Reference Table

|Control Panel Item|Canonical Name|Reason to Restrict|
|---|---|---|
|Administrative Tools|`Microsoft.AdministrativeTools`|Prevents access to powerful utilities like **Services**, **Event Viewer**, and other admin-level tools. 🧨|
|Network & Sharing Center|`Microsoft.NetworkAndSharingCenter`|Stops users from modifying **IP settings, DNS, adapters, or firewall configurations**. 🌐|
|Programs and Features|`Microsoft.ProgramsAndFeatures`|Prevents **unauthorized software installation or removal**, reducing malware risk. 🧪|
|System|`Microsoft.System`|Blocks access to **hardware info, system protection, and advanced system settings**. ⚙️|
|User Accounts|`Microsoft.UserAccounts`|Prevents users from **changing account types or managing other users**. 👤|
|Windows Update|`Microsoft.WindowsUpdate`|Ensures users **cannot delay, pause, or disable critical security updates**. 🔐|
|Device Manager|`Microsoft.DeviceManager`|Prevents **disabling hardware devices or modifying drivers**, which can break the system. 🖥️|
|Power Options|`Microsoft.PowerOptions`|Stops users from altering **sleep, hibernation, or power button behavior**. 🔋|
|Recovery|`Microsoft.Recovery`|Blocks users from **resetting or recovering the PC**, which could bypass security controls. ♻️|
|Security & Maintenance|`Microsoft.ActionCenter`|Prevents users from **ignoring, disabling, or tampering with security alerts**. 🚨|

---

## 🔄 Step 4: Apply the Policy

On the **client machine** (logged in as a domain user):

```cmd
gpupdate /force
```

Then:

- Log out
    
- Log back in
    

---
  
  

**What is a WMI Filter?**

**WMI (Windows Management Instrumentation) Filter** is used to **apply a GPO only when a specific condition is true** on a computer.

**Step 1: Create a WMI Filter**

1. In **Group Policy Management**
    
2. Right-click **WMI Filters**
    
3. Click **New**
    
4. Enter:
    
    - **Name**: (Example: Windows 11 Only) `Excluded DC and ADC`
        
    - **Description**: Optional
          

**Step 2: Add WMI Query**

1. Click **Add**
    
2. Namespace:
    
3. root\CIMv2 9
    
4. WMI Query (Example – Windows 11):
    
5. SELECT * FROM Win32_OperatingSystem
    
	(**Select * from Win32_ComputerSystem where DomainRole < 4)**

6. WHERE Version LIKE "10.0%" AND ProductType="1"
    
7. Click **OK**
    
8. Click **Save**