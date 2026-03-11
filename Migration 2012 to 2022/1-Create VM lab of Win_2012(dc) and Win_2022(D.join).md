
To create the **VM lab environment** like shown in your image (1 Domain Controller + 1 Domain-Joined Server connected to GNS3), follow these steps. This is a **common MCSE / Active Directory lab setup**.

---

## 1️⃣ Create Two Virtual Machines in VMware

You need **2 VMs**:

| VM Name    | OS                                | Purpose              |
| ---------- | --------------------------------- | -------------------- |
| **dc2012** | Windows Server 2012 / 2016 / 2019 | Domain Controller    |
| **Win2022**   | Windows Server 2022               | Domain-Joined Server |

### Steps

1. Open **VMware Workstation**
    
2. Click **Create New Virtual Machine**
    
3. Select **Typical**
    
4. Choose **Installer ISO** of Windows Server
    
5. Set VM name:
    
    - `dc2012`
        
    - `Win2022`
        
6. Set disk size (40–60 GB recommended)
    
7. RAM:
    
    - DC → **4 GB**
        
    - Server → **4 GB**
        

---

## 2️⃣ Connect VM Network to GNS3

Both VMs must connect to the **same network**.

### Steps

1. Open **VM Settings**
    
2. Go to **Network Adapter**
    
3. Select:
    

```
Custom: VMnet (used by GNS3)
```

OR

```
VMnet1 / VMnet2 (same network for both VMs)
```

Then connect that network to **GNS3 Cloud node**.

---

## 3️⃣ Configure Static IP Address

### On Domain Controller (dc2012)

Go to:

```
Control Panel
Network and Sharing Center
Change Adapter Settings
Ethernet → Properties
Internet Protocol Version 4 (IPv4)
```

Set:

```
IP Address: 10.10.11.20
Subnet Mask: 255.255.255.0
Default Gateway: 10.10.11.1 (optional)
Preferred DNS: 10.10.11.20
```

---

### On Server (Win2022)

Set:

```
IP Address: 10.10.11.21
Subnet Mask: 255.255.255.0
Default Gateway: 10.10.11.1
Preferred DNS: 10.10.11.20
```

**Important:** DNS must point to **Domain Controller IP**.

---

## 4️⃣ Install Active Directory (Domain Controller)

On **dc2012**

Open **Server Manager**

```
Manage
Add Roles and Features
```

Install:

```
Active Directory Domain Services (AD DS)
DNS Server
```

After installation click:

```
Promote this server to Domain Controller
```

Select:

```
Add new forest
```

Domain name example:

```
iforward.in
```

Set **DSRM password** → Install → Restart.

---

## 5️⃣ Change Hostname

Rename computers:

### Domain Controller

```
dc2012
```

### Server

```
Win2022
```

Restart both machines.

---

## 6️⃣ Join Server to Domain

On **Win2022**

Go to:

```
System Properties
Computer Name
Change
```

Select:

```
Domain
```

Enter:

```
iforward.in
```

Login using domain admin:

```
Administrator
```

Restart the server.

---

## 7️⃣ Verify Domain Join

Login on **Win2022** using:

```
iforward\Administrator
```

Run:

```
ping dc2012.iforward.in
```

If ping works → **Lab is ready**.

---

✅ Final Lab Structure

```
dc2012 (Domain Controller)
IP: 10.10.11.20
FQDN: dc2012.iforward.in

Win2022 (Domain Server)
IP: 10.10.11.21
Domain Joined
```

Both connected to **GNS3 network**.


