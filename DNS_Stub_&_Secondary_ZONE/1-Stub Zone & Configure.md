## **Stub Zone (DNS)** ⚙️🔥

---
### **What a Stub Zone ACTUALLY is** 🧠

A **Stub Zone** is a **DNS zone that contains ONLY enough data to find the authoritative DNS servers rather than the entire zone data**
Nothing more. Nothing less.

It stores **ONLY**:

- **SOA record** 📌
    
- **NS records** 📌
    
- **A / AAAA records of those NS servers** 📌

- A DNS zone requires a mandatory **Start of Authority** (SOA) record (defining primary server, admin contact, and serial number) and at least two **Name Server** (NS) records (designating authoritative servers)

- These NS records often require **A records** (IPv4) or AAAA (IPv6) to map the hostname to an IP address

👉 **No host records. No users. No services.**

---

# 🔹 PART 1: STUB ZONE – STEP-BY-STEP (CORRECT WAY) ⚙️🧠

👉 **Use this when you want PROPER DNS delegation**

## ✅ Allow to Transfer Zone from UKDC (If you skip this, it WILL FAIL ❌)

On **Master DNS (10.10.11.15 – tree.com)**:

1. Open **DNS Manager**
    
2. Right-click `uk.iforward.in` → **Properties**
    
3. Go to **Zone Transfers**

	
4. ✅ Check **Allow zone transfers**
    
5. ✅ Select **Only to the following servers**
    
6. Add IP: `10.10.11.10` (Parent DNS)
    
7. Apply ✔️
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Zones/stub%20Zone/1-zone%20tra.png?raw=true)

Also ensure:

- DNS service running
    
- Firewall allows TCP/UDP 53
    

---

## 🔧 Create Stub Zone (Parent DNS – iforward.in)

1. **Server Manager → Tools → DNS**
    
2. Right-click **Forward Lookup Zones** → **New Zone**

	![image](https://www.easy365manager.com/wp-content/uploads/StubZone_01.png)

3. Click **Next**

	![image](https://1.bp.blogspot.com/-S09EYi6NuBQ/Xbp2QN27CUI/AAAAAAAABAQ/-3fDtFnSxx4jJGV6v7-qEdhqnfT946KZACEwYBhgL/s1600/6_next_on_welcome_screen.png)

4. Select **Stub Zone**
		
	- ✅ Check **Store the zone in Active Directory**

		
	![image](https://1.bp.blogspot.com/-c5wfDISkKvs/Xbp2Qnz7x0I/AAAAAAAABAU/VUO0D2jQcjULCKUfUm-keEdFTdPLUjVDwCEwYBhgL/s1600/7_select_stub_zone.png)

5. Click **Next**
    
6. Replication Scope → **Default** → Next

	![image](https://1.bp.blogspot.com/-KqDArhNr_kE/Xbp2QoaJb_I/AAAAAAAABAY/lxwjdUxrWeM7O1x5k8vmkNsTbOi8IHEXgCEwYBhgL/s1600/8_choose_replication_scope.png)

7. Zone Name → `tree.com` → Next

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Zones/stub%20Zone/2-tree.com.png?raw=true)
	
8. Master DNS Server → `10.10.11.15`
	
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Zones/stub%20Zone/3-ip%20ukdc.png?raw=true)
    
9. Next → **Finish**
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Zones/stub%20Zone/4-finish.png?raw=true)

---

## 🔄 Verify Stub Zone (NON-NEGOTIABLE)

1. Expand `tree.com`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Zones/stub%20Zone/5-tree.png?raw=true)
	
2. You MUST see:
    
    - SOA
        
    - NS records
        
3. If empty → Right-click → **Transfer from Master**
    
4. If still empty → your **zone transfer is broken** (not Stub Zone)
    

💀 **No records = no delegation = fail**

  ![image](https://1.bp.blogspot.com/-LDH9qmUPcg4/Xbp2ONRACsI/AAAAAAAABAk/gLJHndzh4jgZ10LwxFetOc4UarNoGlX0gCEwYBhgL/s1600/14_confirm_zone_transfer.png)


---

