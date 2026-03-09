
---

# 🖥️ FTP Server Setup on Windows Server 2022 (Using IIS)

This guide explains how to configure an **FTP Server using IIS (Internet Information Services)** on **Windows Server 2022** so users can upload and download files from a shared folder.

---

# Phase 1 — Install IIS and FTP Services ⚙️

### Steps

1️⃣ Open **Server Manager**

```
Start Menu → Server Manager
```

2️⃣ Click

```
Manage → Add Roles and Features
```

3️⃣ In the wizard:

```
Installation Type → Role-based or feature-based installation
```

Click **Next**

---

4️⃣ Select your server from **Server Pool**

Click **Next**

---

5️⃣ In **Server Roles**

Enable:

```
Web Server (IIS)
```

Click **Next**

![image](https://i0.wp.com/serverdecode.com/wp-content/uploads/2023/09/server-roles-web-iis.webp?w=786&quality=78&strip=all&ssl=1)

---

6️⃣ In **Role Services**, expand:

```
Web Server → FTP Server
```

Enable these options:

✅ **FTP Service**  
 **X**  **FTP Extensibility**

Also make sure this is installed:

```
Web Management Tools → IIS Management Console
```
![](https://i0.wp.com/serverdecode.com/wp-content/uploads/2023/09/ftp-server-role-windows.webp?w=786&quality=78&strip=all&ssl=1)

---

7️⃣ Click

```
Next → Install
```

Wait for installation to complete.

---

# Phase 2 — Create FTP Shared Folder 📂

Before creating the FTP site, prepare a folder.

Example:

```
D:\FTP-Data
```

Steps:

1️⃣ Create folder

```
D:\FTP-Data
```

2️⃣ Right click → **Properties**

3️⃣ Go to **Security**

Add your user (example):

```
Administrator
or
FTPUser
```

Give permissions:

✅ Read  
✅ Write

---

# Phase 3 — Configure FTP Site in IIS 🌐

### Steps

1️⃣ Open **IIS Manager**

```
Start → Administrative Tools → Internet Information Services (IIS) Manager
```

---

2️⃣ In the **Connections Panel**

```
Server Name → Sites
```

Right Click

```
Sites → Add FTP Site
```

![](https://neoserver.site/sites/neoserver.site/files/pictures/Setup%20FTP%20Win2016%20--%20add%20FTP%20site.png)

---

### Site Information

Enter:

```
FTP Site Name : MyFTPServer
Physical Path : C:\FTP-Data
```

Click **Next**

![](https://neoserver.site/sites/neoserver.site/files/pictures/Setup%20FTP%20Win2016%20--%20add%20FTP%20site%20name.png)

---

### Binding and SSL

Configure:

```
IP Address : All Unassigned
Port : 21
SSL : No SSL
```

⚠️ Note:  
For production environments, **Use SSL (FTPS)** instead of plain FTP.

Click **Next**

---

### Authentication & Authorization

Authentication:

✅ **Basic**

Authorization:

```
Allow access to : Specified Users
Username : Administrator
```

Permissions:

✅ Read  
✅ Write

Click **Finish**

![](https://dx86q6oq7ry0e.cloudfront.net/uploads/media/blog/a48%40server-panel.net/2023/06/15/image-20230615123020-4.jpg)

 

---

# Phase 4 — Configure Windows Firewall 🔥

![Image](https://support.amcrest.com/hc/article_attachments/360036219951/WF3.PNG)

FTP uses **Port 21**, so it must be allowed through the firewall.

### Steps

1️⃣ Open

```
Windows Defender Firewall
```

2️⃣ Click

```
Allow an app through firewall
```

3️⃣ Click

```
Change Settings
```

4️⃣ Find

```
FTP Server
```

Enable:

✅ Private  
✅ Public

Click **OK**

---

# Phase 5 — Test the FTP Server 🧪

Now test whether the FTP server works.

---

### Step 1 — ADD the Record in DNS

Open **Command Prompt**

```
dnsmgmt.msc
```

Example output:

```
add A Record
```

---

### Step 2 — Connect to FTP

Open **File Explorer**

Type:

```
ftp://10.10.11.11:21 Or ftp://ftp.iforward.in:21
```

---

### Step 3 — Login

Enter:

```
Username : Windows Username
Password : Windows Password
```

If configured correctly, you will see the contents of:

```
C:\FTP-Data
```

You can now:

⬆ Upload files  
⬇ Download files

---

# Real World Example (Company Scenario) 🏢

Example company **ABC Pvt Ltd**

Server:

```
FTP Server IP : 192.168.10.5
Folder : D:\CompanyData
```

Employees connect using:

```
ftp://192.168.10.5
```

Use cases:

• Designers upload project files  
• Backup servers send logs  
• Remote branches transfer data

---

# Important Security Notes ⚠️

Plain FTP is **NOT secure**.

Problems:

❌ Password sent in **clear text**  
❌ Can be sniffed by attackers

Better alternatives:

✔ **FTPS (FTP over SSL)**  
✔ **SFTP (SSH File Transfer Protocol)**

Real companies rarely use **plain FTP anymore**.

---

# Quick Architecture Overview 🧠

```
Client PC
   │
   │ FTP Request
   ▼
Firewall (Port 21 Open)
   │
   ▼
Windows Server 2022
   │
   ├─ IIS FTP Service
   │
   ▼
Shared Folder (D:\FTP-Data)
```

---

