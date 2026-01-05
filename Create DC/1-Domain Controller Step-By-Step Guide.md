# 🖥️ Windows Server 2022: From Workgroup to Domain Controller (AD DS + DNS)

## Step 1: Initial Setup
1. Log in to your Windows Server 2022 machine using **Administrator** privileges.
2. Assign a **static IP address**:
   - Press **Win** +**R** → type **ncpa.cpl** → Enter
   - **Right-click active adapter → Properties → IPv4 → Use the following IP address → Manual**.
   - And Turn off **IPv6**
   - Enable **IPv4** and set:
     ```
     IP Address: 192.168.1.10
     Subnet Mask: 255.255.255.0
     Default Gateway: 192.168.1.1
     Preferred DNS: 127.0.0.1 (or your DNS server)
     ```
4. Click **Save**.
   
   <img width="500" height="450" alt="image" src="https://github.com/user-attachments/assets/08346ec5-3b95-484a-93ee-c9699851fef2" />
---

## Step 2: Rename Computer (Optional but Recommended)
1. Open **Server Manager → Local Server**.
2. Click **Computer name** (shows `Workgroup` by default).
3. Click **Change** → enter a new **Computer name** (e.g., `DC01`).
4. Keep **Member of: Workgroup** selected.
5. Click **OK** → Restart when prompted.
<img width="282" height="178" alt="image" src="https://github.com/user-attachments/assets/85f0f920-d4e3-4ab3-95db-346ebfe3da75" />

---

## Step 3: Install Active Directory Domain Services (AD DS)
1. Open **Server Manager**.
2. Click **Manage → Add Roles and Features**.
3. Click **Next** until you reach **Server Roles**.
4. Select **Active Directory Domain Services**.
5. When prompted, click **Add Features**.
6. Click **Next → Next → Install**.
7. Wait for the installation to complete (no reboot yet).
	
	If you trouble in installation visite this https://activedirectorypro.com/install-ad-ds/
---

## Step 4: Promote the Server to a Domain Controller
1. In **Server Manager**, click the **Notification Flag (⚠️)** → choose **Promote this server to a domain controller**.
2. Select **Add a new forest**.
3. Enter your **Root domain name** (example: `example.local`).
4. Click **Next**.
   
   <img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/cb446ef0-7c9c-4cfe-b089-60dc0d211071" /><img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/d190d28f-df0e-4a39-a8bf-3bf1fd1aecb9" />


---

### Step 4a: Domain Controller Options
1. **Forest Functional Level:** Windows Server 2022  
2. **Domain Functional Level:** Windows Server 2022  
3. **Select the following options:**
   - ✅ DNS Server  
   - ✅ Global Catalog (GC)  
   - ☐ Read-only domain controller (RODC)
4. Set a **Directory Services Restore Mode (DSRM)** password.
5. Click **Next**.
   
<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/c5236819-0ca6-4067-9cf1-7237ece68c4b" />

---

### Step 4b: DNS Options
- You may see a warning:  
  “A delegation for this DNS server cannot be created...”  
  → Ignore it and click **Next**.

---

### Step 4c: Additional Options
- Confirm the **NetBIOS name** (default is fine).  
- Click **Next**.

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/5d77fa44-89d5-4887-8c67-f99a32764f0a" />

---

### Step 4d: Paths
- Keep default:

`Database folder: C:\Windows\NTDS`
`Log files folder: C:\Windows\NTDS`
`SYSVOL folder: C:\Windows\SYSVOL`

- Click **Next**.

<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/f2d2a5cb-c875-495f-90b7-2879f5cc0df1" />

---

### Step 4e: Review and Install
1. Review all settings.
2. Click **Install**.
3. The server will automatically **reboot** after installation.

<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/a3550e83-72c2-4145-bd34-5df200e576b5" />

---

## Step 5: Post-Installation Verification
1. Log in using your new **Domain Administrator** account:
	`DomainName\Administrator`
2. Open:
- **Server Manager → Tools → Active Directory Users and Computers**  
  → Confirm your new domain structure.
- **Server Manager → Tools → DNS**  
  → Verify your forward lookup zone is created.

---

## Step 6: Testing AD DS and DNS
Open **Command Prompt (cmd)** and run:
```cmd
nslookup
ping example.local
```
- If you get valid responses, your AD and DNS setup is working correctly.

## ✅ Result

🎉 Your Windows Server 2022 is now successfully configured as a **Domain Controller** with:

- Active Directory Domain Services (AD DS)
- DNS Server
- A new Forest and Domain (`example.local`)
- Static IP and fully functional authentication services

######  **Purpose:** _Windows Server 2022 AD DS + DNS Setup Guide
---

