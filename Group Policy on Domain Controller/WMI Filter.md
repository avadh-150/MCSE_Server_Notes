
---

## 🧠 What is a **WMI Filter**? (No sugarcoating)

A **WMI Filter (Windows Management Instrumentation Filter)** is a **condition** that decides **whether a GPO should apply or not**, based on **system properties** of the target computer.

👉 In plain English:

> “Apply this GPO **ONLY IF** the computer matches these conditions.”

If condition = **TRUE** ✅ → GPO applies  
If condition = **FALSE** ❌ → GPO is ignored

WMI Filter works **ONLY on COMPUTER side** 🖥️

---

## 🧩 What can a WMI Filter check?

Common **REAL-WORLD** uses 👇

- Windows version (Windows 10 / 11 / Server)
    
- OS architecture (32-bit / 64-bit)
    
- Laptop vs Desktop
    
- RAM size
    
- Disk size
    
- Manufacturer (Dell / HP / VMware)
    
- VM vs Physical machine
    

---
## 🛠 STEP-BY-STEP: Create & Configure a WMI Filter


![Image](https://std.rocks/images/windows_gpo/create-new-wmi-filter-gpmc.png)

---

### ✅ Step 1: Open Group Policy Management

On **Domain Controller**:

- `Server Manager`
    
- `Tools`
    
- **Group Policy Management**
    

---

### ✅ Step 2: Locate WMI Filters

Navigate to:

```
Forest
 └── Domains
     └── iforward.in
         └── WMI Filters
```

---

### ✅ Step 3: Create New WMI Filter

- Right-click **WMI Filters**
    
- Click **New**

![Image](https://std.rocks/images/windows_gpo/create-new-wmi-filter-gpmc.png)

- Name: `Windows 10 Only`
    
- Description: `Apply GPO only to Windows 10 systems`

Click **Add**

---

### ✅ Step 4: Add WMI Query (THIS IS THE CORE)

#### Example 1️⃣: Apply GPO ONLY to Windows 10

```sql

SELECT * FROM Win32_OperatingSystem WHERE Version LIKE "10.%" AND ProductType="1"
```

✔️ ProductType = 1 → Client OS  
✔️ Version 10.* → Windows 10

Click **OK** → **Save**

![image](https://www.rebeladmin.com/wp-content/uploads/2018/02/wmi2.png)

---

## 🔗 STEP-BY-STEP: Link WMI Filter to a GPO

![Image](https://media.licdn.com/dms/image/v2/C5612AQHpbKxbtowQwg/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1617225159025?e=1770249600&t=mSHn8grWeDuJhUft7zG4ioU8ZGPTVJLJfECEMYpvr0Q&v=beta)

---

### ✅ Step 5: Select the GPO

- Go to **Group Policy Objects**
    
- Click your GPO (example: `USB Block Policy`)
    

---

### ✅ Step 6: Attach WMI Filter

- In right pane
    
- Bottom section: **WMI Filtering**
    
- Select `Windows 10 Only`
    
- Click **Yes** (warning popup)
    

🎯 Done. Now the GPO applies **ONLY** if WMI condition = TRUE.

---

## ❌ How to REMOVE / UNAPPLY a WMI Filter

### ✅ Steps:

1. Select the **GPO**
    
2. Under **WMI Filtering**
    
3. Choose **None**
    
4. Confirm
    

⚠️ This does **not delete** the filter.

---

## 🧨 Example WMI Filters (REAL USE CASES)

### 🔹 Windows 11 Only

```sql
SELECT * FROM Win32_OperatingSystem WHERE Version LIKE "10.%" AND BuildNumber >= "22000"
```

---

### 🔹 64-bit OS only

```sql
SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture="64-bit"
```

---

### 🔹 Laptop Only

```sql
SELECT * FROM Win32_Battery
```

✔️ If battery exists → laptop  
❌ No battery → desktop

---

### 🔹 Minimum 8GB RAM

```sql
SELECT * FROM Win32_ComputerSystem WHERE TotalPhysicalMemory >= 8589934592
```

---

## 🧱 WMI Filter vs Security Filtering (DON’T MIX THESE UP)

|Feature|WMI Filter|Security Filtering|
|---|---|---|
|Based on|System properties|Permissions|
|Affects|Computers only|Users & Computers|
|Uses|WMI Query|ACL|
|Performance|Slower|Faster|
|Best use|OS / Hardware check|Who gets policy|

👉 Interview line:

> “Security Filtering controls **WHO**, WMI Filtering controls **WHEN**.”

---

## 🧪 How to TEST if WMI Filter works

On client machine:

```cmd
gpupdate /force
gpresult /r
```

Look for:

```
Applied Group Policy Objects
Filtered out (WMI Filter)
```

---

