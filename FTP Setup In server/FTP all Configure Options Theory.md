You’re currently inside **Internet Information Services (IIS) Manager → `Sites → myftp`**.  
Right now your FTP site exists, but **upload will NOT work unless 3 things are configured correctly**:

1️⃣ **Authentication**  
2️⃣ **Authorization Rules**  
3️⃣ **NTFS Folder Permissions**

Most people configure only one of them and then wonder why upload fails. Let’s fix it properly. 🚀

---

# 1️⃣ Configure FTP Authentication (Allow Login) 🔐

![Image](https://learn.microsoft.com/en-us/iis/publish/using-the-ftp-service/configure-ftp-with-iis-manager-authentication-in-iis-7/_static/image77.png)

![Image](https://learn.microsoft.com/en-us/iis/publish/using-the-ftp-service/configure-ftp-with-iis-manager-authentication-in-iis-7/_static/image53.png)

![Image](https://learn.microsoft.com/en-us/iis/publish/using-the-ftp-service/configure-ftp-with-iis-manager-authentication-in-iis-7/_static/image11.jpg)


In your **myftp Home** window:

### Step

Click

```
FTP Authentication
```

You will see two options:

|Authentication|Setting|
|---|---|
|Anonymous Authentication|Disable|
|Basic Authentication|Enable|

### Do this

✔ Disable **Anonymous Authentication**  
✔ Enable **Basic Authentication**

Then click **Apply** on the right panel.

📌 Reason:  
Basic authentication allows **Windows user login**.

---

# 2️⃣ Configure FTP Authorization (Allow Upload Permission) 📂

![Image](https://learn.microsoft.com/en-us/iis/configuration/system.ftpserver/security/authorization/index/_static/image9.png)

![Image](https://learn.microsoft.com/en-us/iis/publish/using-the-ftp-service/configure-ftp-with-iis-manager-authentication-in-iis-7/_static/image13.jpg)

Now click:

```
FTP Authorization Rules
```

### Steps

Click:

```
Add Allow Rule
```

Configure:

|Setting|Value|
|---|---|
|Allow access to|Specified Users|
|User|Administrator (or your username)|
|Permissions|Read + Write|

Example:

```
User: Administrator
Permissions: Read, Write
```

Click **OK**

Then click **Apply**.

📌 If **Write is not enabled → Upload will fail**.

---

# 3️⃣ Configure NTFS Folder Permission (Most Important) ⚠️

FTP permission alone is **not enough**.  
Windows folder permission must also allow writing.

Go to your FTP folder.

Example:

```
D:\FTPData
```

### Steps

Right click folder → **Properties**

Go to

```
Security Tab
```

Click

```
Edit
```

Add your FTP user.

Example:

```
Administrator
```

Enable:

✔ Read  
✔ Write  
✔ Modify

Click **Apply → OK**

📌 If NTFS permission is missing → upload fails even if FTP shows write enabled.

---

# 4️⃣ Verify FTP Firewall Rules 🔥

FTP requires **Port 21** open.

Open:

```
Windows Defender Firewall
```

Go to:

```
Advanced Settings
```

Enable rule:

```
FTP Server (FTP Traffic-In)
```

Port used:

```
21
```

---

# 5️⃣ Test Upload Using FileZilla Client 🧪

Open **FileZilla Client**

Enter:

```
Host: 10.10.11.11
Username: Administrator
Password: ********
Port: 21
```

Click:

```
Quickconnect
```

After login you should see:

Left side → **Local computer**  
Right side → **FTP server folder**

Drag any file → right side.

Example:

```
test.txt
```

If configuration is correct → file uploads successfully.

---

# 6️⃣ What Your Current IIS Screen Means 🧠

From your screenshot (`myftp Home`) these icons control everything:

|Feature|Purpose|
|---|---|
|FTP Authentication|Login method|
|FTP Authorization Rules|Who can access|
|FTP Directory Browsing|Show file list|
|FTP Firewall Support|Passive mode|
|FTP Logging|Logs connections|
|FTP Messages|Banner messages|
|FTP Request Filtering|Block file types|
|FTP SSL Settings|FTPS encryption|
|FTP User Isolation|Separate user folders|

---

# 7️⃣ Quick Checklist (Upload Troubleshooting) ✅

If upload fails check:

✔ Basic Authentication enabled  
✔ Authorization Rule = Read + Write  
✔ Folder NTFS permission = Modify  
✔ FTP folder path correct  
✔ Firewall port 21 open

---

# ⚠️ Real Cybersecurity Note

Plain FTP is **very insecure**.

Problems:

❌ Password sent in clear text  
❌ Sniffable via Wireshark  
❌ Used in many breaches

Real companies use:

✔ **FTPS (FTP over SSL)**  
✔ **SFTP (SSH FTP)**

---
