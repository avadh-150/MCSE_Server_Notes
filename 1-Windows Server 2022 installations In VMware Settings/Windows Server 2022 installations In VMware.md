I’ll give you the **correct, lab-ready, no-nonsense** way to install **Windows Server 2022 on VMware Workstation**. Follow it exactly. If something breaks, it’s because you skipped a step.

---
 initial setup and configuration of a **Windows Server 2022** virtual machine using **VMware Workstation Pro**.

---

## Phase 1: Creating the Virtual Machine

1. **Launch the Wizard:** Go to `File` > `New Virtual Machine`.

	![Image](https://images.minitool.com/partitionwizard.com/images/uploads/2024/12/create-a-windows-server-2022-virtual-machine-with-vmware-4.png)

2. **Configuration Type:** Select **Custom (advanced)** and click Next.

    ![Image](https://images.openai.com/thumbnails/url/W7x77Xicu5mZUVJSUGylr5-al1xUWVCSmqJbkpRnoJdeXJJYkpmsl5yfq5-Zm5ieWmxfaAuUsXL0S7F0Tw7Mcypy9df1cjUz988yd7XM8wl3MjEv8A81Dq5ydPQu9vbIMwgpyPN28TMIK7dwjA9UKwYALjQknA)
    
3. **Hardware Compatibility:** Ensure it is set to the latest version (Workstation 25H2).
    
4. **Guest OS Installation:** Select **"I will install the operating system later"** to skip immediate ISO mounting.
    
5. **Select Guest OS:** * Set Guest operating system to **Microsoft Windows**.
    
    - Set Version to **Windows Server 2022**.
        
6. **Naming & Location:** * Name the VM (e.g., "Windows Server 2022").
    
    - Click **Browse** to choose a specific storage path. In the video, a new folder named **"DC"** is created within the data directory for organization.

		![Image](https://images.minitool.com/partitionwizard.com/images/uploads/2024/12/create-a-windows-server-2022-virtual-machine-with-vmware-7.png)

7. **Firmware Type:** Select **UEFI** (standard for modern Windows Servers).Leave Recommended -----
    

---

## Phase 2: Hardware Resources

1. **Processors:** Select the desired count (uses 4 processors with 2 core each).
    
2. **Memory:** Allocate RAM. The video increases the default to **5792 MB** (approx. 5.6 GB).
    
3. **Network Type:** Select the initial network connection (initially set to **NAT** or **Host-only**).
    
4. **I/O & Disk Type:** Accept defaults (**LSI Logic SAS** and **NVMe**). Leave Recommended -----
    
5. **Disk Capacity:** * Change "Maximum disk size" to **80 GB**.
    
    - Select **"Store virtual disk as a single file"** for better performance.
        
6. **Finish:** Click **Finish** to create the VM shell.
    

---

## Phase 3: Advanced Settings & Network Editor

1. **Mounting the ISO:**
    
    - Go to **Edit virtual machine settings**.
        
    - Select **CD/DVD (SATA)**.
        
    - Choose **Use ISO image file**, browse, and select your `Win2k22server_ISO.iso`.
        
2. **Custom Networking:**
    
    - Under **Network Adapter**, change the setting to **Custom: Specific virtual network**.
        
    - The video selects `/dev/vmnet2`.

	<img width="1912" height="967" alt="image" src="https://github.com/user-attachments/assets/e43ccc5b-310b-46f4-a9e5-19157ea1d815" />
	
3. **Virtual Network Editor:**
    
    - The user goes to `Edit` > `Virtual Network Editor`.
        
    - The configuration of various subnets (vmnet2, etc.) to ensure the VM is on a specific private network (e.g., `10.10.11.0`).

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Virtual%20Network%20editor.png?raw=true)

4. **Save:** Click **Save** (or OK) to finalize all hardware changes.
    

---

## Phase 4: Power On & Start Installation

1. Click **Power on this virtual machine**
    
2. Windows Setup loads
    

![Image](https://www.nhr.com.sa/wp-content/uploads/2024/10/01-Install-Windows-Server-2022.png)


---

## Phase 5: Windows Server Installation

1. Select:
    
    - Language
        
    - Time
        
    - Keyboard
        
2. Click **Next**
    
3. Click **Install Now**

	![image](https://images.minitool.com/partitionwizard.com/images/uploads/2024/12/create-a-windows-server-2022-virtual-machine-with-vmware-12.png)
	

---

## Phase 6: Select Windows Server Edition (CRITICAL)

You will see options like:

- Windows Server 2022 Datacenter  (Desktop Experience)** ✅
  
👉 **Choose:**

```
Windows Server 2022 Datacenter Evaluation (Desktop Experience)
```

⚠️ If you pick **Core**, there is **NO GUI**.  
Beginners pick Core and then panic. Don’t.

![Image](https://static.packt-cdn.com/products/9781804615096/graphics/image/B18864_01_21.jpg)

---
## Phase 7. Select the **Custom:

**Install Microsoft Server Operating System only (advanced)** 
option as the installation type to clean install Windows Server 2022 virtual machine.

![image](https://images.minitool.com/partitionwizard.com/images/uploads/2024/12/create-a-windows-server-2022-virtual-machine-with-vmware-14.png)

---

## Phase 8: Disk Partition

1. Select the unallocated disk
    
2. Click **Next**

	![image](https://images.minitool.com/partitionwizard.com/images/uploads/2024/12/create-a-windows-server-2022-virtual-machine-with-vmware-15.png)

Windows copies files and reboots automatically.

---

## Phase 9. Wait for While 

* The process may take you some time depending on the system’s performance. It will copy operating system files, install features and updates, and configure settings. So, patiently wait for the installation to complete.

![Image](https://images.minitool.com/partitionwizard.com/images/uploads/2024/12/create-a-windows-server-2022-virtual-machine-with-vmware-16.png)

---

## Phase 10: Set Administrator Password

After reboot:

1. Set **Administrator password**
    
2. Confirm password
    
3. Click **Finish**
    

![Image](https://www.reneelab.com/wp-content/uploads/sites/2/2023/08/default-admin-account-password.png)


---

## Step 12: Login to Server

- Press: `Ctrl + Alt + Insert` (VMware equivalent)
    
- Username:
    
    ```
    Administrator
    ```
    
- Enter password
    

You are now inside **Windows Server 2022**

---

## Step 13: Post-Installation MUST-DO (Don’t skip)

### 1. Install VMware Tools

```
VM → Install VMware Tools
```

- Improves display
    
- Fixes mouse issues
    
- Improves network & performance
    

### 2. Rename Server

```
Server Manager → Local Server → Computer Name
```

### 3. Set Static IP

```
ncpa.cpl → IPv4 → Manual IP
```

### 4. Windows Update (optional but recommended)

---
