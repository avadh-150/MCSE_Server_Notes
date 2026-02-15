## 🗂️ DFS Setup — Clean, Structured Step-by-Step Guide 🚀

---
# 📁 Part 1 — Initial Folder Setup (On Each Server)

👉 Purpose: create shared folders that DFS will use

```
📌 Do this on SVR_1 and SVR_2 separately
```

### 🔹 Steps

1️⃣ Open **File Explorer** → go to:

```
This PC → Local Disk (C:)
```

2️⃣ Create a new folder:

- **SVR_2** → `salesdata_pune`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/1-Share%20folder%20and%20ROle%20add/1-puna%20folder.png?raw=true)

- **SVR_1** → `salesdata_mumbai`

	![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/1-Share%20folder%20and%20ROle%20add/3-mumbai%20folder.png?raw=true)

3️⃣ Open the folder → create:

```
Right click → New → Text Document
```

Rename example:

```
salesdata 2022 On SVR-2

Salesdata 2026 on SVR-1 
```


4️⃣ Share the folder:

```
Right click folder → Properties
→ Sharing tab
→ Advanced Sharing
```

5️⃣ Enable sharing:

✅ Check → **Share this folder**

6️⃣ Click **Permissions**:

✅ Allow **Everyone** (or required users)

👉 Click **OK → OK → Close**

- **SVR_1** → `salesdata_Mumbai`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/1-Share%20folder%20and%20ROle%20add/5-mumbai%20+%20share%20.png?raw=true)

- **SVR_2** → `salesdata_Pune`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/1-Share%20folder%20and%20ROle%20add/6-pune+share.png?raw=true)

---

# ⚙️ Part 2 — Install DFS Roles (On Each Server)

👉 Installs DFS Namespace + Replication  
Software involved: Windows Server

---

### 🔹 Installation Flow

1️⃣ Open:

```
Server Manager
```

2️⃣ Click:

```
Manage → Add Roles and Features
```

3️⃣ Wizard opens → click:

```
Next
```

4️⃣ Select:

```
Role-based or feature-based installation
→ Next
```

5️⃣ Choose server:

```
SVR_1 or SVR_2
→ Next
```

6️⃣ Expand:

```
File and Storage Services
→ File and iSCSI Services
```

7️⃣ Select:

✅ **DFS Namespaces**

- **DFS Namespaces** enables you to group shared folders located on different servers into one or more logically structured namespaces.
-  Each namespace appears to users as a single shared folder with a series of subfolders. However, the underlying structure of the namespace can consist of numerous shared folders located on different servers and in multiple sites.

👉 Click **Add Features**

8️⃣ Select:

✅ **DFS Replication**

- DFS Replication is a multimaster replication engine that enables you to synchronize folders on multiple servers across local or wide area network (WAN) network connections.
- It uses the Remote Differential Compression (RDC) protocol to update only the portions of files that have changed since the last replication. DFS Replication can be used in conjunction with DFS Namespaces, or by itself

9️⃣ Click:

```
Next → Next
```

🔟 Confirmation screen:

```
Install
```

⏳ Wait until:

```
Installation succeeded
```

✅ Click **Close**

![image](https://eu-images.contentstack.com/v3/assets/blt07f68461ccd75245/blt1735e245c9ccfeae/6650756a8bf0ee9bf7f811c6/DFS_201.jpg?width=1280&auto=webp&quality=80&disable=upscale)

---

# 🌐 Part 3 — Connectivity + DFS Tool Verification

👉 Ensures servers communicate + DFS console works

---

### 🔹 Network Test

1️⃣ Open:

```
Command Prompt
```

2️⃣ Run ping test:

```
ping SVR_1
ping SVR_2
```

✅ Successful replies = network OK

---

### 🔹 DFS Console Check

1️⃣ Open:

```
Server Manager
→ Tools
→ DFS Management
```

2️⃣ Verify console shows:

```
Namespaces
Replication
```

   👉 Ready for DFS configuration 🎯

   ![image](https://www.thesolving.com/wp-content/uploads/2015/09/How-to-configure-Distributed-File-System-01.png)

---

# 🧠 Quick Visual Workflow

```
Create folders 📁
      ↓
Share folders 🔓
      ↓
Install DFS roles ⚙️
      ↓
Ping test 🌐
      ↓
Open DFS console 🗂️
```

---

