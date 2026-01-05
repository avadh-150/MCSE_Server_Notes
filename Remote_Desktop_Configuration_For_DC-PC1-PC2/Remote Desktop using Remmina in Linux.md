## 🧠 Purpose
This guide explains how to install and configure **Remmina**, a remote desktop client for Linux, to connect to multiple systems such as **Domain Controller (DC)**, **PC1**, and **PC2** using the **RDP protocol**.

---
## 🧰 Part 1: Enable Remote Desktop on Windows Systems

Before connecting from Remmina, make sure **Remote Desktop** is enabled on each target system (DC, PC1, PC2).

### **Step 1: Open System Properties**
- On the Windows machine (e.g., DC, PC1, PC2), press:
  ```
  Win + R → sysdm.cpl → Enter
  ```

### **Step 2: Enable Remote Desktop**
- Go to the **Remote** tab.
- Under **Remote Desktop**, select:
  > “Allow remote connections to this computer.”
- Click **Apply → OK**.

### **Step 3: Allow RDP through Windows Firewall**
- Open **Windows Defender Firewall → Allow an app or feature through Windows Defender Firewall**.
- Make sure **Remote Desktop** is checked for both **Private** and **Public** networks.

### **Step 4: (Optional) Check RDP Port**
By default, Remote Desktop runs on **TCP port 3389**.  
You can verify it using PowerShell:
```powershell
Get-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' | Select-Object PortNumber
```

📸 *Example Screenshot:*  
![Enable Remote Desktop](MCSE%20Class%20Notes/img/RDP Enable Verification.png)

---


---


## 🪜 Part -2 Steps to Install Remmina

### **Step 1: Update Package List**
Open the terminal and run:
```bash
sudo apt update
```

### **Step 2: Install Remmina**
```bash
sudo apt install remmina -y
```

### **Step 3: (Optional) Install RDP and VNC Plugins**
If not included by default:
```bash
sudo apt install remmina-plugin-rdp remmina-plugin-vnc -y
```

### **Step 4: Launch Remmina**
You can open it from:
- Applications Menu → *Remmina*
- Or run this command:
```bash
remmina
```

---


## 🧩 Steps to Add a New Connection Profile

### **Step 1: Open Remmina**
Launch Remmina and click the **“+” (New Connection Profile)** button.

### **Step 2: Fill Connection Details**
In the **Remote Connection Profile** window, fill in details as follows:

| Field    | Example                       |
| -------- | ----------------------------- |
| Name     | DC.iforward.in                |
| Protocol | RDP - Remote Desktop Protocol |
| Server   | 10.10.11.10                   |
| Username | administrator@iforward.in     |
| Password | test@123                      |
| Domain   | iforward.in (optional)        |

📸 *Example Screenshot:*  
![Remmina Connection Profile](MCSE%20Class%20Notes/img/Adding Remote Machine Details.png)

Then click **Save and Connect**.

---
## 💻 Step 3: Add Multiple Systems

Repeat the same process for each system you want to connect to.

### 🔹 **For PC1**
| Field    | Value             |
| -------- | ----------------- |
| Name     | PC1.iforward.in   |
| Server   | 10.10.11.11       |
| Username | user1@iforward.in |
| Password | Test@123          |

### 🔹 **For PC2**
| Field    | Value             |
| -------- | ----------------- |
| Name     | PC2.iforward.in   |
| Server   | 10.10.11.12       |
| Username | user2@iforward.in |
| Password | Test@123          |

Each connection will appear in Remmina’s main window as a saved profile.

---
## 🚀 Step 4: Connect to the Systems
1. Double-click any saved connection (e.g., **DC.iforward.in**) to start RDP.
2. You’ll see the Windows login screen.
3. Enter the credentials if prompted and click **OK**.
4. You are now remotely connected to that machine.
📸 *Example Screenshot:*  
![Connected to Remote System](MCSE%20Class%20Notes/img/Remote Sucess.png)

---
---
## 📝 Notes
- Make sure **Remote Desktop** is enabled on the Windows machines.
- Ensure the systems (DC, PC1, PC2) are reachable via network and **firewall allows RDP (TCP 3389)**.
- If connection fails:
  - Check IP addresses and credentials.
  - Try `ping 10.10.11.10` to verify connectivity.
  - Ensure the **Remmina RDP plugin** is installed.

---
