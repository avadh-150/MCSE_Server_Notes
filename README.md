# MCSE_Server_Notes

📌 Project Title

Enterprise Server Configuration & Lab Setup


          Internet
              |
           NAT (GNS3)
              |
        R1 (Router)
         fa0/1 |
               | 
               |fa0/0
           --Switch ----- ------------
          |              |           |
     Windows Server     PC1 (VPCS)   PC2

## 📖 Overview

This project documents the configuration of a server environment used for learning, testing, and hands-on practice in system administration and cybersecurity concepts.

The setup includes domain services, networking, security policies, and client integration following real-world enterprise standards.

---

## 🖥️ Environment Details

| Item            | Value                  |
| --------------- | ---------------------- |
| Server OS       | Windows Server 2022    |
| Server Role     | Domain Controller      |
| Host Platform   | VMware Workstation     |
| Server Hostname | DC01                   |
| Domain Name     | iforward.in            |
| IP Address      | 10.10.11.10            |
| DNS Role        | Installed & Configured |
| AD DS           | Installed              |


Client Machines

| Client | OS              | Purpose                   |
| ------ | --------------- | ------------------------- |
| PC1    | Windows 10 / 11 | Domain-joined user system |
| PC2    | Windows 10 / 11 | Domain-joined user system |

---

## 🧱 Server Roles & Features Installed

* Active Directory Domain Services (AD DS)

* DNS Server

* Group Policy Management

* File Server (NTFS Permissions)

* FSRM (Quota & File Screening)

* Security Policies via GPO

* Windows Server Backup

---

## 🔐 Group Policy Configurations

### Applied at Domain Level

* Hide Recycle Bin

* Password & Account Policies

* Disable Credential Manager

* Security Baselines

### Applied at OU Level (IT OU)

* Show Recycle Bin (Override)

* Custom Desktop Policies

* Restricted User Permissions

  
## 📁 File Server Configuration

### NTFS Permissions

- Role-based access control
    
- Special permissions applied:
    
    - Users can **delete only files they own**
        
    - No permission to change ACLs
        
    - No ownership takeover
        

### FSRM Policies

- Quota applied on `My_Quota` folder
    
- File screening enabled for restricted file types
    
- Event Viewer logs monitored for violations

  - Permissions
    

---
## 🌐 Networking Configuration

|Component|Details|
|---|---|
|IP Assignment|Static (Server), DHCP (Clients)|
|DNS Resolution|Internal AD DNS|
|Gateway|Router via GNS3|
|NAT|Configured on Router|
|VPN|Site-to-Site IPsec (Lab)|

---

## 🧪 Lab Tools Used

- VMware Workstation
    
- GNS3
    
- Cisco IOS Routers
    
- Windows Server 2022
    
- Ubuntu Linux (Admin / GNS3 Host)
    

---

## 🔍 Verification & Testing

- Domain join verified (`sysdm.cpl`)
    
- DNS tested using `nslookup`
    
- GPO results checked via `gpresult /r`
    
- File access tested with standard users
    
- Event Viewer monitored for security logs
    

---

## 📌 Use Case

This lab simulates a **real enterprise environment** for:

- System Administration practice
    
- Active Directory management
    
- Network security fundamentals
    
- SOC & IT Support readiness
    

---

## 🚀 Future Improvements

- Implement WSUS
    
- Configure SIEM log forwarding
    
- Add MFA for domain users
    
- Harden server using CIS benchmarks
    

---

## 📄 Notes

This setup is **not theoretical**. Every configuration was tested manually to understand real-world behavior, limitations, and security impact.

---

## Author

👤 **AR** 

Aspiring Cybersecurity & System Administrator  
Hands-on with AD, GPO, Networking & Security Labs

👤**HT**

👤**SV** 

---
