
---

# 🪞 RAID-1 (Mirrored Volume) Configuration in Windows Server

## 📌 Part 1 — Creating the Mirrored Volume

### 1️⃣ Open Disk Management

🖥️ Open **Disk Management** in Windows Server.

You should see:

- **Disk 1** → 9.98 GB **Unallocated**
    
- **Disk 2** → 9.98 GB **Unallocated**
    
	![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/RAID/2.png?raw=true)

These disks will become the mirror pair.

---

### 2️⃣ Start Creating the Mirrored Volume

➡️ Right-click on **Disk 1 – Unallocated Space**

Select:

**New Mirrored Volume**

⚠️ Important:  
You always start with **one disk**, then add the mirror disk in the wizard.

---

### 3️⃣ New Mirrored Volume Wizard

The wizard will appear.

Click:

**Next**

Simple step — just starting the configuration.

---

### 4️⃣ Select the Mirror Disk

Now Windows asks which disks will participate in the mirror.

You will see:

|Column|Meaning|
|---|---|
|Available|Disks not yet used|
|Selected|Disks that will form the RAID|

Steps:

1️⃣ Select **Disk 2** from **Available**  
2️⃣ Click **Add >**  
3️⃣ Disk 2 moves to **Selected**

Now the mirror pair is:

- Disk 1
    
- Disk 2
    

Click **Next**

---

### 5️⃣ Assign a Drive Letter

Windows now asks how users will access the volume.

Select:

**Assign the following drive letter**

Choose:

**G**

So the RAID volume becomes:

*_G:*_

Click **Next**

---

### 6️⃣ Format the Volume

Now configure the filesystem.

Recommended settings:

|Setting|Value|
|---|---|
|File System|NTFS|
|Allocation Unit|Default|
|Volume Label|RAID 1|
|Quick Format|Enabled|

Why NTFS?

Because NTFS supports:

- permissions
    
- encryption
    
- large files
    
- journaling
    

Click **Next**

---

### 7️⃣ Finish the Wizard

You will see a **summary screen** showing:

- Mirrored Volume
    
- Disk 1 + Disk 2
    
- Drive Letter G
    
- NTFS
    
- Label RAID 1
    

Click:

**Finish**

---

### 8️⃣ Disk Conversion Warning ⚠️

Windows shows a warning:

> The disks will be converted from **Basic → Dynamic**

Why?

Because **Windows Software RAID requires Dynamic disks.**

Click:

**Yes**

---

### 9️⃣ Volume Creation & Syncing

Windows now:

1️⃣ Creates the mirror  
2️⃣ Formats the filesystem  
3️⃣ Starts synchronization

In Disk Management you will see:

🔴 **Red colored volume**

Label:

**RAID 1 (G:)**

on both disks.

Meaning:

Disk 1 ↔ Disk 2  
are now mirrors.

---

# 📂 Part 2 — Verifying the RAID Volume

Creating RAID is useless unless you **test it**. Always verify.

---

### 🔎 1️⃣ Open File Explorer

Open:

**This PC**

---

### 💽 2️⃣ Locate the New Drive

You should see:

**RAID 1 (G:)**

under **Devices and drives**

---

### 📁 3️⃣ Open the RAID Volume

Double click:

*_G:*_

It should be empty.

---

### 📁 4️⃣ Create a Test Folder

Right Click → **New → Folder**

Name:

**record**

This tests write capability.

---

### 📂 5️⃣ Open the Folder

Double click:

**record**

---

### 📄 6️⃣ Create a Test File

Right Click → **New → Text Document**

Name:

**F1**

Now the disk contains:

```
G:\
 └── record
      └── F1.txt
```

This data now exists on:

- Disk 1
    
- Disk 2
    

simultaneously.

---

# ⚙️ Part 3 — Checking Mirror Management Options

Back in **Disk Management**

Right-click the volume.

You will see options like:

|Option|Meaning|
|---|---|
|Break Mirror|Splits the mirror but keeps both disks|
|Remove Mirror|Removes one disk from the mirror|
|Add Mirror|Adds another mirror disk|
|Delete Volume|Removes the RAID volume|

These are used for **disk failure or maintenance**.

---

# 🧠 What Actually Happened Behind the Scenes

When RAID-1 was created:

```
Write request → Windows RAID driver
                 ↓
            Disk 1 write
            Disk 2 write
```

Every block written to **Disk 1** is copied to **Disk 2**.

Advantages:

✔ Disk failure protection  
✔ Simple recovery  
✔ Fast read speed (sometimes)

Disadvantages:

❌ Storage efficiency = **50%**

Example:

```
Disk 1 = 10GB
Disk 2 = 10GB

Usable RAID = 10GB
```

Half capacity lost for redundancy.

---

# 🚨 Reality Check (Important)

RAID-1 **IS NOT BACKUP**.

Many beginners misunderstand this.

If you:

- delete a file ❌
    
- get ransomware ❌
    
- corrupt filesystem ❌
    

The same thing is instantly mirrored.

Both disks lose data.

So real environments still use:

- Backup servers
    
- Snapshots
    
- Offsite backup
    
