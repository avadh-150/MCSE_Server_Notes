## 🗂️ DFS Namespace + Folder Setup + GPO Drive Mapping — Clean Guide 🚀

![image](https://learn.microsoft.com/en-us/windows-server/storage/dfs-namespaces/media/dfs-overview.png)

 - **DFS Namespace** is a Windows Server feature that organized file shares into a single logical path such as `\\iforward.in\Namespace`
 
 - This allows users to access files through a single, unified path (e.g., `\\iforward.in\Public`)

---

# 🧭 Part 1 — Create DFS Namespace

Software console: Windows Server  
Tool used: DFS Management

```
👉 Do this on SVR_1
```

### 🔹 Steps

1️⃣ Open:

```
DFS Management
```

![image](https://www.thesolving.com/wp-content/uploads/2015/09/How-to-configure-Distributed-File-System-01.png)

2️⃣ Right-click:

```
Namespaces → New Namespace
```

![image](https://www.thesolving.com/wp-content/uploads/2015/09/How-to-configure-Distributed-File-System-02.png)

3️⃣ Namespace server:

```
Type: SVR_1
→ Next
```

   ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/1-svr_name.png?raw=true)

4️⃣ Namespace name:

```
Salesdata
→ Next
```

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/2-publish%20name.png?raw=true)

5️⃣ Namespace type:

✅ Domain-based namespace  
✅ Enable Windows Server 2008 mode

→ Next

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/3-path.png?raw=true)

6️⃣ Review:

```
Create → Close

```

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/4-review.png?raw=true)

![image](https://www.thesolving.com/wp-content/uploads/2015/09/How-to-configure-Distributed-File-System-07.png)

✅ Namespace created:

```
\\iforward.in\Salesdata
```

---

# 📁 Part 2 — Add Shared Folders to Namespace

```
Goal → Link real folders into DFS namespace
```

---

## 🏙️ Add Mumbai Folder

1️⃣ Right-click namespace:

```
\\iforward.in\Salesdata
→ New Folder
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/5-namespace%20create.png?raw=true)

2️⃣ Folder name:

```
Sales Mumbai
```

3️⃣ Click:

```
Add → Browse
```

4️⃣ Select:

```
Server: SVR_1
Folder: salesdata_mumbai
```

👉 OK → OK

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/6-path.png?raw=true)

---

## 🌄 Add Pune Folder

1️⃣ Right-click namespace again:

```
New Folder
```

2️⃣ Folder name:

```
Sales Pune
```

3️⃣ Click:

```
Add → Browse
```

4️⃣ Change server:

```
SVR_2
→ salesdata_pune
```

👉 OK → OK

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/7-change%20srv-2.png?raw=true)



![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/8-namespace%20finish.png?raw=true)


---

# 🖥️ Part 3 — Map DFS Drive Using Group Policy

Tool used: Group Policy Management

```
👉 Do this on Domain Controller
```

---

### 🔹 Create GPO

1️⃣ Open:

```
Group Policy Management
```

2️⃣ Right-click domain:

```
iforward.in
→ Create a GPO and link it here
```

3️⃣ Name:

```
Namespace Map Drive
→ OK
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/8.5-sales%20folder%20in%20DC.png?raw=true)

---

### 🔹 Edit GPO

1️⃣ Right-click GPO:

```
Edit
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/9.5-create%20the%20GPO.png?raw=true)

2️⃣ Navigate:

```
User Configuration
→ Preferences
→ Windows Settings
→ Drive Maps
```

3️⃣ Right-click empty space:

```
New → Mapped Drive
```

---

### 🔹 Drive Settings

#### General Tab

```
Action → Create
Location → \\iforward.in\Salesdata
Label → Sales Data
Drive Letter → S:
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/9-create%20mapp%20drive.png?raw=true)

---

#### Common Tab

✅ Check:

```
Item-level targeting                      → Targeting
```

Add rule:

```
New Item → Computer Name
Type → SVR_1
→ OK
```

👉 Apply → OK

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/9.6-traggeting.png?raw=true)

---

# 🔄 Part 4 — Force Policy Update + Verify

```
👉 Do this on target machines
```

---

### 🔹 Update Policy

1️⃣ Open Command Prompt:

```
gpupdate /force
```

2️⃣ Log out → log back in

---

### 🔹 Verify

Open:

```
File Explorer → This PC
```

✅ You should see:

```
Sales Data (S:)
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/DFS/2-%20DFS%20namespace%20+%20drive%20mapped/10-finish.png?raw=true)

Inside:

```
Sales Mumbai
Sales Pune
```

Drive mapping successful 🎯

---

# 🧠 Quick Workflow Overview

```
Create namespace 🗂️
     ↓
Add folders 📁
     ↓
Create GPO ⚙️
     ↓
Map drive 💻
     ↓
Verify ✅
```

---
