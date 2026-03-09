
---

# 🖥️ FileZilla Server Installation & Configuration Guide (Windows)

---

# Phase 1 — Install FileZilla Client ⚙️

![Image](https://images.cloudclusters.io/1a653e84527149d18b26421825517508/install-filezilla-server-1.png)

### Step-by-Step Installation

1️⃣ **Run the Installer**

Double-click the FileZilla Server setup file.

---

2️⃣ **Accept License Agreement**

Click:

```
I Agree
```

---

3️⃣ **Choose Components**

Keep default settings.

Typical components installed:

✔ FileZilla Server  
✔ Administrative Interface

Click:

```
Next
```

---

4️⃣ **Installation Location**

Default location:

```
C:\Program Files\FileZilla Server
```

Click:

```
Next
```

---

6️⃣ **Startup Settings**

Select:

```
Start if any user logs on
```

Click:

```
Install
```

---

7️⃣ **Finish Installation**

Once installation completes:

Click:

```
Close
```

The **FileZilla Server interface will open automatically**.

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FTP/6.png?raw=true)

---


![Image](https://i0.wp.com/raw.githubusercontent.com/WordPress/Advanced-administration-handbook/main/assets/filezilla_1.gif?ssl=1)

When the **Connect to Server** window appears:

---

# Phase 2 — Create FTP User Account 👤

FTP users must be created before someone can access the server.

### Steps

1️⃣ Go to:

```
Edit → Users
```

---

2️⃣ Click:

```
Add
```

---

3️⃣ Enter a username

Example:

```
user1
```

Click **OK**

---

4️⃣ Enable password protection

✔ Check:

```
Password
```

Enter a secure password.

Example:

```
Test@123
```

---

# Phase 3 — Test FTP Connection 🧪

Now verify that the FTP server works.

---

### Method 1 — Using Browser

Enter:

```
ftp://ftp.iforward.in
```

Replace with your **server IP address**.

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FTP/5.png?raw=true)

---

### Method 2 — Using FTP Client

Use **FileZilla Client**.

Connection settings:

```
Host : ftp.iforward.in
Username : -
Password : -
Port : 21
```

- there is **no username and password** Bcz we use the FTP as **Anonymous**. 

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FTP/7.png?raw=true)

---

After login, you should see the **shared folder contents**.

You can now:

⬆ Upload files  

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FTP/8.png?raw=true)

⬇ Download files

---

