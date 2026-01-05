Below is a **proper, step-by-step REPORT FORMAT** you can **submit, print, or upload to GitHub** for  
**Connect GNS3 ↔ VMware ↔ Windows Server 2022**.

No fluff. No theory dump. This is **exactly how labs are documented in real institutes**.

---

# LAB REPORT

## Connecting **GNS3 ↔ VMware ↔ Windows Server 2022**

---

## 1. Objective

To establish network connectivity between **GNS3**, **VMware Workstation**, and **Windows Server 2022** so that:

- GNS3 routers can communicate with VMware virtual machines
    
- Windows Server 2022 can act as a **Domain Controller**
    
- Client machines can access services through GNS3 routing and NAT
    

---

## 2. Network Topology

```
          Internet
              |
           NAT (GNS3)
              |
        R1 (Router)
         fa0/1 | fa0/0
                |
             Switch
          |              |
     Windows Server     PC1 (VPCS)
```

- **R1** acts as Default Gateway
    
- **Cloud (vmnet2)** bridges GNS3 and VMware
    
- All internal devices use `10.10.11.0/24`
    

---

## 3. IP Addressing Scheme

|Device|Interface|IP Address|Subnet Mask|Gateway|
|---|---|---|---|---|
|R1|fa0/0|10.10.11.1|255.255.255.0|—|
|Server 2022|NIC|10.10.11.10|255.255.255.0|10.10.11.1|
|PC1|eth0|10.10.11.11|255.255.255.0|10.10.11.1|

---

## 4. Step-by-Step Configuration

---

### Step 1: Configure VMware Network (Host-Only)

1. Open **VMware Workstation**
    
2. Go to **Edit → Virtual Network Editor**
    
3. Select **vmnet2**
    
4. Set:
    
    - Network Type: **Host-Only**
        
    - Subnet: `10.10.11.0 /24`
        
5. Apply settings
    

Purpose:

> Allows VMware VMs to communicate with GNS3 via Cloud node.

---
### Step 2: Configure Windows Server 2022 Network

Inside **Windows Server 2022**:

1. Open `ncpa.cpl`
    
2. Right-click Ethernet → Properties
    
3. Select IPv4 → Properties
    
4. Configure:
    

```
IP Address : 10.10.11.10
Subnet     : 255.255.255.0
Gateway    : 10.10.11.1
DNS        : 127.0.0.1
```

5. Save settings
    

---

### Step 3: Add Cloud Node in GNS3

1. Open **GNS3**
    
2. Drag **Cloud** node into workspace
    
3. Right-click Cloud → Configure
    
4. Under Ethernet Interfaces:
    
    - Select **vmnet2**
        
    - Click **Add**
        
5. Click OK
    

This bridges **GNS3 ↔ VMware**.

---

### Step 4: Build GNS3 Topology

1. Add:
    
    - Router (R1)
        
    - Switch
        
    - PC1 (VPCS)
        
2. Connect:
    
    - R1 fa0/0 → Switch
        
    - Switch → PC1
        
    - Switch → Cloud (vmnet2)
        
    - R1 fa0/1 → NAT node
        

---

### Step 5: Configure Router R1

Access router CLI and enter:

```bash
enable
conf t

interface fa0/0
 ip address 10.10.11.1 255.255.255.0
 ip nat inside
 no shutdown

interface fa0/1
 ip address dhcp
 ip nat outside
 no shutdown

access-list 1 permit 10.10.11.0 0.0.0.255
ip nat inside source list 1 interface fa0/1 overload

ip route 0.0.0.0 0.0.0.0 fa0/1
end
```

Purpose:

- fa0/0 → LAN
    
- fa0/1 → Internet
    
- NAT provides outbound connectivity
    

---

### Step 6: Configure PC1 (VPCS)

In PC1 console:

```bash
ip 10.10.11.11 255.255.255.0 10.10.11.1
save
```

---

## 6. Verification & Testing

### From Windows Server 2022:

```cmd
ping 10.10.11.1
ping 10.10.11.11
ping 8.8.8.8
```

### From Router:

```bash
ping 10.10.11.10
show ip nat translations
```

### From PC1:

```bash
ping 10.10.11.10
ping 8.8.8.8
```

Expected Result:

- All devices communicate successfully
    
- Internet reachable via NAT
    
- VMware ↔ GNS3 connectivity confirmed
    

---

## 7. Result

The connection between **GNS3**, **VMware**, and **Windows Server 2022** was successfully established.  
The server is reachable from GNS3 devices, and routing/NAT functions correctly.

---

## 8. Conclusion

This lab demonstrates how enterprise environments integrate:

- Virtualization platforms
    
- Network emulators
    
- Windows Server infrastructure
    

The setup is suitable for:

- Active Directory labs
    
- Domain join testing
    
- GPO enforcement
    
- Routing & NAT simulations
    

---
