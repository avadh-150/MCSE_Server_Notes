
# 🧩 Install DHCP Server Role (Windows Server)

## 🚀 Open Role Installation

1️⃣ Open **Server Manager**  
2️⃣ Click **Manage** (top right)  
3️⃣ Select **Add Roles and Features**

4️⃣ Select:  
✅ **Role-based or feature-based installation**  
➡️ Click **Next**

5️⃣ Choose your server from pool  
(e.g., `SVR_1.forward.in`)  
➡️ Click **Next**

6️⃣ Check:  
☑️ **DHCP Server**

7️⃣ Popup appears → click:  
✅ **Add Features**
➡️ Click **Next**

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-3-600x427.jpg)

8️⃣ Leave default features  
➡️ Click **Next**

9️⃣ Read info → click **Next**

🔟 Click **Install**

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-6-600x429.jpg)

⏳ Wait until completed

# 🛡️ DHCP Security Groups & Authorization in Active Directory

1. Create a “Security Group” to manage this DHCP server. There are two of them:

- DHCP Administrators - group members have full rights to manage the DHCP server;
- DHCP Users - members of the group can view server settings and a list of connected devices.

2. Authorization of a DHCP server in Active Directory (if it is joined to a domain). This setting is necessary to avoid the appearance of extraneous DHCP servers on the network. The server must be authorized for the DHCP service to start:

![Authorization of a DHCP server in Active Directory](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-7-450x331.jpg)

- Enter the administrator credentials and click on the “Commit” button. If the server is not joined to the domain, then select the last item:

![Enter the administrator credentials](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/1-authorized%20tab.png?raw=true)

- If everything is done correctly, the wizard notifies that the configuration was successful:

![The wizard notifies that the configuration was successful](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-9-450x332.jpg)

---

# 🖥️ DHCP Scope Configuration on Windows Server

**Step-by-Step Guide**

---

# 🚀 Part 1: Initialize New Scope Wizard

1️⃣ Open **Server Manager**  
2️⃣ Click **Tools** (top right) → select **DHCP**  

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-10-600x431.jpg)

3️⃣ In DHCP console, expand your server (e.g., `svr_1.forward.in`)  
4️⃣ Expand **IPv4**  
5️⃣ Right-click **IPv4** → **New Scope…**  

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-11-600x404.jpg)

6️⃣ When wizard opens → click **Next** ➡️

---

# 🏷️ Part 2: Scope Name & IP Range

7️⃣ **Scope Name**

- Name: `VLAN 10`
    
- Description: `This is DHCP IT Department Server-VLAN 10`  
    ➡️ Click **Next**

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/1.png?raw=true)

8️⃣ **IP Address Range**

- Start IP: `10.10.11.1`
    
- End IP: `10.10.11.254`
    
- Length: `24`
    
- Subnet Mask: `255.255.255.0`  
    ➡️ Click **Next**

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/2.png?raw=true)

---

# ⛔ Part 3: Exclusions & Lease

9️⃣ **Add Exclusions**

- Start: `10.10.11.1`
    
- End: `10.10.11.10`
    
- Click **Add** ➕  
    ➡️ Click **Next**

	![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/3.png?raw=true)

🔟 **Lease Duration**

- Keep default: **8 days** (or adjust)  
    ➡️ Click **Next**

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-15.jpg)

---

# ⚙️ Part 4: DHCP Options

1️⃣1️⃣ Select:  
✅ _Yes, I want to configure these options now_  
➡️ Click **Next**

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-16.jpg)

---

### 🌐 Router (Default Gateway)

1️⃣2️⃣

- IP: `10.10.11.1`
    
- Click **Add** ➕  
    ➡️ Click **Next**

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/4.png?raw=true)

---

### 🧭 Domain & DNS

1️⃣3️⃣

- Parent domain: `forward.in` (auto)
    
- DNS Server: `10.10.11.10` present  
    ➡️ Click **Next**

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/5.png?raw=true)

---

### 🪟 WINS

1️⃣4️⃣

- Leave blank  
    ➡️ Click **Next**
    

---

# ✅ Part 5: Activate & Verify

1️⃣5️⃣ Select:  
✅ _Yes, I want to activate this scope now_  
➡️ Click **Next**

![image](https://serverspace.io/wp-content/uploads/2020/05/dhcp-server-20.jpg)

1️⃣6️⃣ Click **Finish**

---

# 🔎 Verification in DHCP Console

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/6.png?raw=true)


1️⃣7️⃣ Expand:  
**Scope [10.10.11.0] VLAN 10**

1️⃣8️⃣ Click **Address Pool**  
✔️ Range: `10.10.11.1 – 10.10.11.254`  
✔️ Exclusion: `10.10.11.1 – 10.10.11.10`

1️⃣9️⃣ Click **Reservations**  
➡️ Manage fixed IP assignments

---

# 🔎 Verification in SRV_2 

### Set the IP address as a DHCP 

![image](https://progressive.kvh.com/Help/V3help/54-0890/Network_Configuration/Win10_DHCP_arrows.png)

and 

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/DHCP/DHCP%20ip%20assign.png?raw=true)

