
---

# ⚡ RAID-0 (Striped Volume) Configuration in Windows Server

RAID-0 spreads data across multiple disks to **increase performance**, but **it has zero fault tolerance**. If **one disk fails → all data is lost**. ⚠️

![](https://networkencyclopedia.com/wp-content/uploads/2019/08/raid-0-disk-striping-1024x951.jpg)

---

# 🧱 Step 1: Initialize the New Disks



When new disks are attached to the server, Windows requires initialization.

**Procedure**

1️⃣ Open **Disk Management**

```
Server Manager → Tools → Computer Management → Disk Management
```

2️⃣ The **Initialize Disk** popup appears automatically.

![Image](https://learn.microsoft.com/en-us/windows-server/storage/disk-management/media/select-uninitialized-disk.png)

3️⃣ Select the newly added disks

```
Disk 1
Disk 2
Disk 3
```

4️⃣ Select partition style:

```
GPT (GUID Partition Table)
```

5️⃣ Click **OK**

✅ Result:

```
Disk Status = Online
Space Status = Unallocated
```

---

# ⚡ Step 2: Start the New Striped Volume Wizard


Now you create the RAID-0 array.

**Procedure**

1️⃣ Right-click **Unallocated space on Disk 1**

2️⃣ Select

```
New Striped Volume
```

![](https://onlinecomputertips.com/wp-content/uploads/2025/02/h456.jpg)

3️⃣ The wizard opens

4️⃣ Click

```
Next
```

---

# 🧩 Step 3: Select Disks for RAID-0

Here you choose which disks will participate in the RAID-0.

**Procedure**

1️⃣ Disk 1 is already selected

2️⃣ Add remaining disks:

```
Select Disk 2 → Click Add

```

![](https://media.geeksforgeeks.org/wp-content/uploads/20220218093517/14.png)

3️⃣ Leave **Maximum disk space (default)**

4️⃣ Click

```
Next
```

✅ Selected disks:

```
Disk 1
Disk 2
```

---

# 💾 Step 4: Assign Drive Letter

You must assign a drive letter so Windows can access the volume.

**Procedure**

1️⃣ Select

```
Assign the following drive letter
```

2️⃣ Example:

```
E:
```

3️⃣ Click

```
Next
```



---

# 🗂 Step 5: Format the RAID Volume









This step prepares the RAID array to store files.

**Configuration**

```
File System : NTFS
Allocation Unit Size : Default
Volume Label : RAID-0
Perform Quick Format : Enabled
```

Then click

```
Next
```

---

# ✅ Step 6: Finish RAID Configuration

1️⃣ Review the summary

2️⃣ Click

```
Finish
```

3️⃣ Warning appears:

```
Disks will be converted to Dynamic Disks
```

4️⃣ Click

```
Yes
```

---

# 🎯 Final Result

Disk Management will show:

```
Volume Name : RAID-0
Type        : Striped Volume
File System : NTFS
Status      : Healthy
Drive Letter: E:
Color       : Teal
```

The RAID-0 volume is now **ready for use**. 🚀

---

# ⚠️ Reality Check (Important)

Don't blindly think RAID-0 is good everywhere.

|Factor|Reality|
|---|---|
|Speed|Very fast ⚡|
|Fault Tolerance|None ❌|
|If 1 Disk Fails|Entire data lost 💀|
|Used In|Temp storage, cache, video editing|

Companies usually prefer:

```
RAID 1
RAID 5
RAID 10
```

because **data protection matters more than speed**.

---
