---

# IIS Installation & Configuration on Windows Server 🖥️🌐

---

# 🧩 Part 1: Installing the IIS Role

**File:** `add role of IIS part-1.webm`

### 1️⃣ Open Server Manager

Launch the **Server Manager** dashboard from the taskbar or Start menu.

### 2️⃣ Add Roles and Features

Click **Manage** (top-right) → **Add Roles and Features**.

### 3️⃣ Before You Begin

On the wizard splash screen, click **Next**.

### 4️⃣ Installation Type

Select **Role-based or feature-based installation** → **Next**.

### 5️⃣ Server Selection

Ensure your local server is selected from the server pool → **Next**.

![image](https://kaas.hpcloud.hp.com/PROD/v2/renderbinary/8738960/8837426/publication-troubleshooting-group-series/iis-4)
### 6️⃣ Server Roles

- Scroll down and locate **Web Server (IIS)** 🌐
    
- Check the box
    
- Popup appears → click **Add Features**
    
- Click **Next**

![image](https://kaas.hpcloud.hp.com/PROD/v2/renderbinary/8738960/8837382/publication-troubleshooting-group-series/iis-5)

### 7️⃣ Features

Leave default selections → **Next**.

### 8️⃣ Web Server Role (IIS) Info

Review IIS description → **Next**.

### 9️⃣ Role Services

- Customize IIS services (ASP.NET, FTP, etc.) ⚙️
    
- For standard setup → keep defaults
    
- Click **Next**
    

### 🔟 Confirmation

Review selections → **Install**.

![image](https://kaas.hpcloud.hp.com/PROD/v2/renderbinary/8738960/8837406/publication-troubleshooting-group-series/iis-10)
### ✅ Completion

Wait until **Installation succeeded** appears → **Close**.

---

# ⚙️ Part 2: Configuring & Testing IIS
### 1️⃣ Locate Web Root Folder

Open **File Explorer** 📁  
Navigate to:

![image](https://images.minitool.com/minitool.com/images/uploads/news/2020/05/what-is-inetpub-folder/what-is-inetpub-folder-1.png)

![image](https://cdn.mos.cms.futurecdn.net/w2s3fnvmZHuvK2d9mhnXkD-1136-80.jpg.webp)

```
C:\inetpub\wwwroot
```

This folder contains:

- `iisstart.htm`
    
- IIS background image  
    👉 These files generate the default IIS webpage.
	- Also You can **Choose the Your website** And Put it on  **`C:\inetpub\wwwroot`** this path.

---
