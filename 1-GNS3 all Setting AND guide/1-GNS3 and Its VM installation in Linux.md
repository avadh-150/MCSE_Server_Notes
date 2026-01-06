

---

## PART 1: Install **GNS3 on Linux (Ubuntu/Debian-based)**

![image](https://linux.how2shout.com/wp-content/uploads/2024/06/Installing-GNS3-server-on-Ubuntu-24.04.webp)

### 1️⃣ Prerequisites (don’t ignore this)

- **64-bit OS**
    
- **At least 8 GB RAM** (16 GB recommended for labs)
    
- **Virtualization enabled (Intel VT-x / AMD-V)**  
    Check:
    

```bash
lscpu | grep Virtualization
```

If this shows **nothing**, stop. Enable virtualization in BIOS.

---

### 2️⃣ Install GNS3 (official method)

Run **exactly** this:

```bash
sudo add-apt-repository ppa:gns3/ppa
sudo apt update
sudo apt install gns3-gui gns3-server
```

When prompted:

- **Non-superusers capture packets?** → ✅ YES
    
- **Install Wireshark dumpcap as root?** → ✅ YES
    

If you say NO here, packet capture will break.

---

### 3️⃣ Add user to required groups

```bash
sudo usermod -aG ubridge,libvirt,kvm,wireshark $USER
```

Then **REBOOT**.  
No reboot = permissions won’t apply.

---

### 4️⃣ Launch GNS3

```bash
gns3
```

First launch wizard:

- Choose **Run appliances in a virtual machine (recommended)**  
    We’ll handle that in Part 2.
    

---

## PART 2: Install **GNS3 VM using VMware**


### Step 1
After logging in to GNS3, [directly access the web page](https://www.gns3.com/software/download-vm) where the virtual machine platforms are located. Then click on the Download button in the category appropriate for the virtualization program installed on your computer and save the zip file to your computer.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-01.webp)


---

### Step 2
After downloading the GNS3.VM.Workstation.2.2.55.1.zip file to your computer, open the terminal by pressing CTRL + ALT + T and execute the “unzip FileName.zip” command to extract the archived file to the folder.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-02.webp)

---

### Step 3
Open your VMware Workstation 16 Pro software, and click File / Open from the tool menu to import the GNS3 VM.ova file.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-03.webp)

---
### Step 4
Select and open the GNS3 VM.ova file, which is an installed virtual machine file.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-04.webp)

---
### Step 5
When the Import Virtual Machine window opens, select a location where you want to back up the VM, or you can choose to back up to the default location.

After configuring the server name and location, click the Import button.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-05.webp)

---


### Step 6
Wait while importing the GNS3 Server VM on VMware on your Linux Mint system.
Step 7

After adding the GNS3 virtual machine, open its settings, and, after viewing the processor’s hardware settings, increase the number of virtual processors and cores and enable the features under Virtualization Engine.

- Virtualize Intel VT-x/EPT or AMD-V/RVI
- Virtualize CPU Performance Counters
- Virtualize IOMMU (IO Memory Management Unit)
![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-06.webp)

---
### Step 7
Open VMware → **Open a Virtual Machine** → Select `.ova`

Recommended settings:

- **RAM**: 4 GB minimum (8 GB if you can)
    
- **CPU**: 2–4 cores
    
- **Network**: NAT
    

Power **ON** the VM.

If VM doesn’t start → your BIOS virtualization is OFF.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-07.webp)

---

### Step 8
After turning on the GNS3 server, you can check its version, virtualization platform, IP address, and port number or Web-Ui address.

![Image](https://img.sysnettechsolutions.com/Linux-Mint-GNS3-VM-10.webp)

---
