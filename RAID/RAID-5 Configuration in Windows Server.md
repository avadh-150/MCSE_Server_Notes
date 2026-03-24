RAID-5 in **Windows Server 2022** uses **disk striping with parity**. Data is split across disks and parity information is stored so the system can **survive one disk failure**. Minimum **3 disks required**. If one disk dies, the system rebuilds data using parity. 💾🛡️

---

# ⚙️ RAID-5 Configuration in Windows Server 2022

## 🧰 Lab Requirements

Before starting, make sure your lab has:

|Requirement|Value|
|---|---|
|OS|Windows Server 2022|
|Minimum disks|**3 disks**|
|Disk state|**Unallocated**|
|Disk size|Same size recommended|

Example lab:

```
Disk 1 – 10 GB
Disk 2 – 10 GB
Disk 3 – 10 GB
```

Usable RAID-5 space will be:

```
(n-1) × disk size
(3-1) × 10GB = 20GB usable
```

---

# 🪜 Step-by-Step RAID-5 Setup

## 1️⃣ Open Disk Management

Press:

```
Windows + R
```

Type:

```
diskmgmt.msc
```

Press **Enter**

You should see **three disks with unallocated space**.

---

## 2️⃣ Start RAID-5 Creation

Right-click **Unallocated Space on Disk 1**

Select:

```
New RAID-5 Volume
```

This starts the RAID-5 configuration wizard.

---

## 3️⃣ RAID-5 Wizard Welcome

The **New RAID-5 Volume Wizard** opens.

Click:

```
Next
```

---

## 4️⃣ Select the Disks

Now choose disks that will participate in RAID-5.

Left side = **Available disks**  
Right side = **Selected disks**

Steps:

1️⃣ Select **Disk 2**  
2️⃣ Click **Add**

3️⃣ Select **Disk 3**  
4️⃣ Click **Add**

Now you should see:

```
Selected Disks
Disk 1
Disk 2
Disk 3
```

Click **Next**

---

## 5️⃣ Assign Drive Letter

Windows asks how the volume will be accessed.

Select:

```
Assign the following drive letter
```

Example:

```
i
```

So the RAID volume becomes:

```
i:\
```

Click **Next**

---

## 6️⃣ Format the RAID Volume

Choose filesystem settings.

Recommended configuration:

|Setting|Value|
|---|---|
|File System|NTFS|
|Allocation Unit|Default|
|Volume Label|RAID5|
|Quick Format|Enabled|

Click:

```
Next
```

---

## 7️⃣ Confirm Configuration

You will see a summary like:

```
Volume Type: RAID-5
Disks: Disk 1, Disk 2, Disk 3
File System: NTFS
Drive Letter: i
Label: RAID5
```

Click:

```
Finish
```

---

## 8️⃣ Disk Conversion Warning ⚠️

Windows will show this message:

> Disks must be converted to **Dynamic disks**

Why?

Because **Windows software RAID requires Dynamic disks**.

Click:

```
Yes
```

---

## 9️⃣ RAID-5 Creation

Disk Management will now:

1️⃣ Convert disks to **Dynamic**  
2️⃣ Create RAID-5 structure  
3️⃣ Format filesystem

You will see the volume colored **green** labeled:

```
RAID5 (i:)
```

Status may show:

```
Resynching
```

Wait until it becomes **Healthy**.

---

# 📂 Testing the RAID-5 Volume

## 🔎 1️⃣ Open File Explorer

Open:

```
This PC
```

You should see:

```
RAID5 (I:)
```

---

## 📁 2️⃣ Create a Folder

Inside the drive:

```
Right Click → New → Folder
```

Name:

```
data
```

---

## 📄 3️⃣ Create Test File

Inside **data folder**

```
Right Click → New → Text Document
```

Name:

```
test1
```

Now RAID-5 is working.

---

# 🧠 What Actually Happens in RAID-5

Example with **3 disks**:

```
Disk1   Disk2   Disk3
-----   -----   -----
DataA   DataB   Parity
DataC   Parity  DataD
Parity  DataE   DataF
```

Parity rotates across disks.

If **Disk2 fails**, system rebuilds data using parity math.

---

# 💥 Example Disk Failure Scenario

If **Disk 2 crashes**:

Server still runs using:

```
Disk1 + Disk3 + parity calculation
```

Status becomes:

```
Degraded
```

Replace failed disk → system **rebuilds automatically**.

---

# ⚠️ Hard Truth (Many Students Get This Wrong)

RAID-5 is **NOT backup**.

If you:

- delete files ❌
    
- ransomware attack ❌
    
- filesystem corruption ❌
    

RAID mirrors the damage across disks.

Companies still use:

- Backup servers
    
- Snapshots
    
- Offsite backup
    

RAID only protects against **hardware disk failure**.

---

# 📊 Quick RAID Comparison

|RAID|Min Disks|Protection|Speed|Use Case|
|---|---|---|---|---|
|RAID0|2|None|Fast|Temp data|
|RAID1|2|1 disk|Medium|OS drives|
|RAID5|3|1 disk|Good read|File servers|
|RAID10|4|Multiple|Very fast|Databases|

---

✅ Since you're studying **Windows Server labs and cybersecurity**, the **next important lab** you should know is:

**RAID-5 Disk Failure Simulation & Recovery** (what admins actually do in production).

If you want, I’ll show you that **full practical lab step-by-step**. 💀🔧