
---

# 🖥️ FTP User Authentication Setup (Windows + FileZilla Server)

This process includes **four major phases**:

1️⃣ Create a **Windows local user**  
2️⃣ Configure the user in **FileZilla Server**  
3️⃣ Set **shared folder permissions**  
4️⃣ Connect using **FileZilla Client**

---

# Phase 1 — Create a Local Windows User 👤

![Image](https://downloads.admindroid.com/images/how-to-images/active-directory/get-password-never-expire-users-list-ad/disable-never-expire-option-for-user-in-ad.png?v=6004_01)

Before configuring the FTP server, create a **dedicated Windows account**.

---
### Enable the Basic Authentication

![Image](https://learn.microsoft.com/en-us/iis/publish/using-the-ftp-service/configure-ftp-with-iis-manager-authentication-in-iis-7/_static/image53.png)

---

### Step 1 — Open Computer Management

Open the Start Menu and search:

```id="whs7v3"
Computer Management
```

---

### Step 2 — Navigate to Users

In the left panel:

```id="hhob1j"
System Tools
   └── Local Users and Groups
          └── Users
```

---

### Step 3 — Create New User

Right-click inside the **Users** panel.

Select:

```id="vkt65t"
New User
```

---

### Step 4 — Enter User Details

Example:

```id="hjthlk"
User name : user1
Password : Test@123
```

Then configure options:

✔ Uncheck **User must change password at next logon**  
✔ Check **Password never expires**

Click:

```id="tbnolb"
Create → Close
```

📌 This user will be used for **FTP login authentication**.

---

# Phase 4 — Connect Using FileZilla Client 🌐

Now connect from a client machine using **FileZilla Client**.

---

### Step 1 — Open FileZilla Client

Launch:

**FileZilla Client**

---

### Step 2 — Enter Connection Details

Fill the **Quickconnect bar**:

```id="flq57p"
Host : 10.10.11.11
Username : user1
Password : Test@123
Port : 21
```

---

### Step 3 — Connect

Click:

```id="b2tk53"
Quickconnect
```

---

### Step 4 — Certificate Warning (If TLS Enabled)

If prompted:

```id="10gqgl"
Unknown certificate
```

Click:

```id="ybfh7h"
OK
```

to trust the connection.

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FTP/login%20user%20in%20filezilla.png?raw=true)

---

# After Successful Connection ✅

You will see:

Left side → **Local Computer Files**  
Right side → **FTP Server Files**

You can now:

⬆ Upload files  
⬇ Download files  
🗑 Delete files

Simply **drag and drop files** between panels.

---

# Real Network Example 🏢

Example company setup:

```id="caw39y"
Server IP : 10.10.11.11
FTP Folder : C:\ftp_files
User : ftp_user
```

Employees connect using:

```id="gns9ko"
ftp://10.10.11.11
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FTP/successfully%20login%20.png?raw=true)

This allows **secure file sharing inside the organization network**.

---

# Security Reality (Important) 🔐

Standard FTP has major weaknesses.

Problems:

❌ Password transmitted in clear text  
❌ Easily sniffed using packet capture tools  
❌ Vulnerable on public networks

Better alternatives used in companies:

✔ **FTPS (FTP over SSL/TLS)**  
✔ **SFTP (SSH File Transfer Protocol)**

---

