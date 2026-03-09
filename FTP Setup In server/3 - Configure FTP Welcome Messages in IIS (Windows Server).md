
---

# 🖥️ Configure FTP Welcome Messages in IIS (Windows Server)

FTP messages are used to display **custom text when a client connects or disconnects** from the FTP server.

These messages help with:

✔ Server identification  
✔ Legal warnings  
✔ Instructions for users

Example used in companies:

```
Authorized users only. All activities are logged.
```

---

# Phase 1 — Configure FTP Messages in IIS Manager ⚙️

### Step 1 — Open IIS Manager

On the Windows Server:

```
Start → Administrative Tools → Internet Information Services (IIS) Manager
```

---

### Step 2 — Select the FTP Site

In the **Connections Panel (Left Side)**:

```
Server Name
   └── Sites
        └── myftp
```

Click **your FTP site**.

Example:

```
myftp
```

---

### Step 3 — Open FTP Messages

In the **center panel**, locate:

```
FTP Messages
```

Double-click it.

---

### Step 4 — Configure the Banner Message

In **Banner Text Box**, enter:

```
Welcome to this FTP site
This is FORWARD old data and directory access.......=========
```

📌 Banner message appears **before login**.

---

### Step 5 — Configure Welcome Message

In **Welcome Text Box**, enter:

```
Welcome to this FTP site.
```

📌 This appears **after successful login**.

---

### Step 6 — Configure Exit Message

In **Exit Text Box**, enter:

```
cd/
```

📌 This message appears **when the user disconnects**.

---

### Step 7 — Apply Settings

On the **right side (Actions Panel)**:

Click

```
Apply
```

Then return back to **FTP Site Home**.

---

# Phase 2 — Verify the FTP Server Locally 🔍

Admins should **always test locally first before client testing**.

The video demonstrates **4 different verification methods**.

---

# Method 1 — Test Using FileZilla Client

Open **FileZilla Client**.

Enter:

```
Host: 10.10.11.11
```

Click:

```
Quickconnect
```

---

### FTP Server Response Example

In the **top log window**, you will see:

```
220 Welcome to this FTP site
220 This is FORWARD old data and directory access.......=========
```

After login:

```
230 Welcome to this FTP site.
```

📌 FTP Status Codes

|Code|Meaning|
|---|---|
|220|Server ready|
|230|Login successful|

---

# Method 2 — Test via Web Browser 🌐

Open any browser.

Type:

```
ftp://ftp.forward.in
```

or

```
ftp://10.10.11.11
```

You should see:

```
Index of /
```

This confirms:

✔ FTP server running  
✔ Directory access working

---

# Method 3 — Test Using Command Prompt 💻

Open **Command Prompt**

Type:

```
ftp 10.10.11.11
```

Press **Enter**

You should see:

```
220 Welcome to this FTP site
This is FORWARD old data and directory access.......=========
```

This confirms **Banner message works correctly**.

---

# Method 4 — Test Using Telnet 🔎

This checks **port-level connectivity**.

In Command Prompt type:

```
telnet 10.10.11.11 21
```

Output:

```
220 Welcome to this FTP site
```

This confirms:

✔ FTP service running  
✔ Port 21 reachable

You can type:

```
help
```

to see FTP commands.

---

# Phase 3 — Access FTP from Client Machine 🖥️

Now move to **client computer**.

Example client machine:

```
SVR_2
```

---

### Step 1 — Open FileZilla Client

Launch:

**FileZilla Client**

---

### Step 2 — Connect to FTP Server

Enter in Quickconnect bar:

```
Host : 10.10.11.11
Username : (blank for anonymous)
Password : (blank)
Port : 21
```

Click:

```
Quickconnect
```

---

### Step 3 — View Connection Messages

In the **log panel**, you will see:

```
220 Welcome to this FTP site
This is FORWARD old data and directory access.......=========
```

Then:

```
230 Welcome to this FTP site.
```

This confirms the **FTP banner and welcome messages are working correctly**.

---
# FTP Connection Flow (What Actually Happens) 🔄

```
Client connects to FTP server
        │
        ▼
Server sends Banner Message (220)
        │
        ▼
User authentication
        │
        ▼
Server sends Welcome Message (230)
        │
        ▼
User accesses files
        │
        ▼
User disconnects
        │
        ▼
Exit Message displayed
```

---
