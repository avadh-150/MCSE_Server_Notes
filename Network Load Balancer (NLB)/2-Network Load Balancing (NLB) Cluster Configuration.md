Perfect 👍 — here’s your same content polished, structured, and with clean emojis added (no wording changes, only formatting + visuals).

---

# 🌐 Network Load Balancing (NLB) Cluster Configuration – Windows Server 2022

---

# 🧩 Part 1: Creating the Initial Cluster

---

### 1️⃣ Open NLB Manager

- In **Server Manager** → click **Tools** (top right).
    
- Select **Network Load Balancing Manager**.
    
	![image](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/12/1112.png?w=768&h=378)
---

### 2️⃣ Start New Cluster Wizard

- Right-click **Network Load Balancing Clusters** (left pane).
    
- Select **New Cluster**.
    
	![image](https://4sysops.com/wp-content/uploads/2022/10/Creating-a-new-NLB-cluster.png)
---

### 3️⃣ Connect to First Host

- In **Host** box → enter IP/hostname (e.g., `10.10.11.11).
    
- Click **Connect**.
    
- Select interface (e.g., `Ethernet0`).
    
- Click **Next**.
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/1.png?raw=true)
	
---

### 4️⃣ Configure Host Parameters

- Set **Priority (Unique host identifier)** → `1`.
    
- Ensure **Initial host state** = **Started**.
    
- Click **Next**.
    
	![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/2.png?raw=true)
---

### 5️⃣ Add Cluster IP Address

- Click **Add**.
    
- Enter Virtual Cluster IP → `10.10.11.201`.
    
- Subnet mask auto-fills → `255.255.255.0`.
    
- Click **OK** → **Next**.
    
	![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/3.png?raw=true)
---

### 6️⃣ Configure Cluster Parameters

- **Full internet name** → `www.Avnash-L.in`.
    
- **Cluster operation mode** → **Multicast**.
    
- Click **Next**.

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/4.png?raw=true)

---

### 7️⃣ Edit Port Rules

- Select default rule → click **Edit**.
    
- **Filtering mode** → **Multiple host**.
    
- **Affinity** → **Single** (or as required).
    
- Click **OK** → **Finish**.
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/5.png?raw=true)
---

### 8️⃣ Verify Cluster Status

⏳ Wait until node status turns green and shows **Converged**.

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/6.png?raw=true)

---

# ➕ Part 2: Adding a Second Server to the Cluster

---

### 1️⃣ Select Add to Cluster

- In **NLB Manager** → right-click cluster (`www.iforward.in[10.10.11.201]`)

- Select **Add Host to Cluster**.

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/7.png?raw=true)

---

### 2️⃣ Connect to Second Host

- In **Host** → enter IP (e.g., `10.10.11.12`).
    
- Click **Connect**.
    
- Select interface (e.g., `Ethernet0`).
    
- Click **Next**.
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/8.png?raw=true)
---

### 3️⃣ Configure Host Parameters

- **Priority** → `2` (must differ from first).
    
- **Initial host state** → **Started**.
    
- Click **Next**.
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/9.png?raw=true)
---

### 4️⃣ Confirm Port Rules

- Rules auto-match first node.
    
- Click **Finish**.

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/5.png?raw=true)

---

### 5️⃣ Monitor Convergence

📜 Check log (bottom panel):

- “Initial host state: started”
    
- “The configuration change has been applied.”
    

✅ Both servers (`SVR_1` and `SVR_2`) should show **Status: Converged**.

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/NLB/2%20Cluster%20added%20of%20SVR_1%20&%20SVR-2.png?raw=true)

---

