## 🔁 DFS Replication Setup — Clean Step-by-Step Guide 🚀

Software console: Windows Server  
Tool used: **DFS Management**

![](https://learn.microsoft.com/en-us/windows-server/storage/dfs-replication/media/dfsr-overview.gif)

---

# 🧩 Phase 1 — Create DFS Replication Group

```
👉 Perform on SVR_1
```

---

### 🔹 Launch Replication Wizard

1️⃣ Open:

```
DFS Management
```

2️⃣ Right-click:

```
Replication → New Replication Group
```

---

### 🔹 Group Basics

3️⃣ Select:

```
Multipurpose replication group
→ Next
```

![](https://www.poweradmin.com/blog/wp-content/uploads/2014/09/replication-group-type-02.png)

4️⃣ Enter details:

```
Name → Confiler
Description → backup replication services
Domain → iforward.in
→ Next
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/3-DFS%20replication/1.png?raw=true)

---

### 🔹 Add Members

5️⃣ Click:

```
Add
```

Add servers:

```
SVR_1
SVR_2
```

✔ Check Names → OK → Next

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/3-DFS%20replication/2.png?raw=true)

---

### 🔹 Topology

6️⃣ Choose:

```
Full mesh
```

👉 All servers replicate with each other  
→ Next

![image](https://www.poweradmin.com/blog/wp-content/uploads/2014/09/replication-topology-selection-05.png)

---

### 🔹 Schedule & Bandwidth

7️⃣ Keep default:

```
Replicate continuously
Bandwidth → Full
```

→ Next

![image](https://www.poweradmin.com/blog/wp-content/uploads/2014/09/replication-group-schedule-bandwidth-06.png)

---

### 🔹 Primary Member

8️⃣ Select:

```
SVR_1
```

👉 Initial data source  
→ Next

---

### 🔹 Folder to Replicate

9️⃣ Click:

```
Add → Browse
```

Select:

```
C:\salesdata_mumbai
```

(Optional: verify permissions)

👉 OK → Next

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/3-DFS%20replication/3.png?raw=true)

---

### 🔹 Destination Folder

🔟 Select member:

```
SVR_2 → Edit
```

Configure:

```
Enabled → Yes
Browse → C:\live_backup
```

👉 OK → Next

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/3-DFS%20replication/4.png?raw=true)

---

### 🔹 Create Group

1️⃣1️⃣ Review summary:

```
Create
```

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/3-DFS%20replication/5.png?raw=true)
****

2️⃣ Confirmation:

✔ All tasks → Success  
Click:

```
Close → OK
```

![image](https://4sysops.com/wp-content/uploads/2022/04/DFS-Replication-configuration-completes-successfully.png)

⚠ Replication delay notice is normal.

---

# ✅ Phase 2 — Verify Replication

---

## 📂 Test on Source (SVR_1)

1️⃣ Navigate to:

```
C:\salesdata_mumbai
```

2️⃣ Create folder:

```
lighthub
```

3️⃣ Inside folder:

```
New text file
```

Example name:

```
replication_test
```

4️⃣ Add text → Save → Close

---

## 📂 Check Destination (SVR_2)

1️⃣ Navigate to:

```
C:\live_backup
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/3-DFS%20replication/6.png?raw=true)

2️⃣ Verify:

✔ Folder appears  
✔ File appears  
✔ Content matches

👉 Replication working 🎯

---

# 🧠 Quick Replication Flow

```
Create group 🔁
      ↓
Add members 🖥️
      ↓
Select folders 📁
      ↓
Sync data ⚡
      ↓
Verify copy ✅
```

---
