## **Secondary Zone (DNS)** ⚙️💣

![Image](https://cdn.hostadvice.com/2023/11/final-primary-vs-secondary-dns-servers-what-s-the-difference-1.png)

---

### **What a Secondary Zone REALLY is** 🧠

- A **secondary DNS zone** is a **read-only**, **replicated copy of a primary DNS zone** used for load balancing and fault tolerance.

- it cannot accept direct updates, but rather fetches data via zone transfers from a designated master server

- Primary to secondary DNS zone **replication** typically occurs **within 15 minutes to 3 hours**, depending on the Start of Authority (SOA) refresh interval and NOTIFY settings

That’s it.  
If you think it’s smarter than that — you’re wrong ❌

It gets its data via **Zone Transfer (AXFR / IXFR)** from the Primary.

---

### **What It Stores** 📦

✔️ **ALL records**

- A / AAAA
    
- CNAME
    
- MX
    
- SRV 
    
- NS
    
- SOA
    

Unlike Stub Zone, this is a **FULL COPY** 🧨

---

### **When You ACTUALLY Need a Secondary Zone** ✅

Use it when:

- Primary DNS is a **single point of failure**
    
- You need **local DNS resolution** in remote sites
    
- You’re running **non-AD DNS (BIND ↔ Windows)**
    
- External DNS providers need a copy of your zone
    

If none of these apply → **don’t use it**.

---

### **Secondary Zone vs Stub Zone (Stop Mixing These)** 🚨

|Feature|Secondary Zone|Stub Zone|
|---|---|---|
|Stores full records|✅ YES|❌ NO|
|Editable|❌ NO|❌ NO|
|Bandwidth|🔴 Heavy|🟢 Light|
|Used for redundancy|✅ YES|❌ NO|
|Used for delegation|❌ NO|✅ YES|

👉 **Wrong choice here = bad DNS design**

---
# **DNS Secondary Zone Configuration & Verification (Step-by-Step Lab Guide)** 🧠🛠️

---
## **Objective** 🎯

To configure a **Secondary DNS Zone** on a Domain Controller and verify successful **zone transfer (replication)** from the Master DNS server.

---

## **Environment Used** 🧪

- **Primary (Master) DNS Server:** `uk_hostname`
    
- **Secondary DNS Server:** `DC`
    
- **Zone Name:** `uk.iforward.in`
    
- **Master DNS IP:** `10.10.11.15`

---

## **Phase 1: Create the Secondary DNS Zone (On Secondary Server – DC)** 🔁

📍 **Performed on:** `DC`

1. Open **DNS Manager**
    
    - `Server Manager` → `Tools` → `DNS`
        
2. Expand the DNS server
    
    - Expand **Forward Lookup Zones**
        
3. Launch New Zone Wizard
    
    - Right-click **Forward Lookup Zones** → **New Zone…**
        
4. Wizard – Welcome Screen
    
    - Click **Next**

		![image](https://www.readandexecute.com/wp-content/uploads/2018/05/2018-04-29-19_04_05-New-Zone-Wizard.png)

5. Zone Type Selection
    
    - Select **Secondary zone**
        
    - ❌ Ensure **“Store the zone in Active Directory”** is **unchecked**
        
    - Click **Next**

		![image](https://www.readandexecute.com/wp-content/uploads/2018/05/2018-04-29-19_04_24-New-Zone-Wizard.png)

6. Zone Name
    
    - Enter: `uk.iforward.in`
        
    - Click **Next**
        
7. Master DNS Server Configuration
    
    - Enter IP: `10.10.11.15`
        
    - Press **Enter**
        
    - ✅ Green checkmark confirms validation
        
    - Click **Next**
        
8. Finish Wizard
    
    - Review summary
        
    - Click **Finish**
        

✅ **Expected Result:**  
`sk.Armand.in` appears under **Forward Lookup Zones** with a **read-only** icon.

---

## **Phase 2: Add DNS Record on Master Server (Primary Zone)** 🧩

📍 **Performed on:** `sk_hostname` (Master DNS)

1. Open **DNS Manager**
    
2. Navigate to the Zone
    
    - **Forward Lookup Zones** → `uk.iforward.in`
        
3. Create Host (A) Record
    
    - Right-click empty area → **New Host (A or AAAA)…**
        
4. Enter Record Details
    
    - **Name:** `youtube`
        
    - **IP Address:** `195.16.10.1`
        
5. Save Record
    
    - Click **Add Host**
        
    - Click **OK** → **Done**
        
6. Refresh Zone
    
    - Right-click `uk.iforward.in` → **Refresh**
        

✅ **Expected Result:**  
The `youtube` A-record is visible on the **Master DNS server**.

---

## **Phase 3: Verify Zone Transfer on Secondary Server (DC)** 🔍

📍 **Performed on:** `DC`

1. Open **DNS Manager**
    
2. Navigate to Secondary Zone
    
    - **Forward Lookup Zones** → `uk.iforward.in`
        
3. Initial Observation
    
    - `youtube` record is **not visible yet** (normal behavior)
        
4. Force Zone Transfer
    
    - Right-click `sk.Armand.in` → **Transfer from Master**
        
    - Click **Yes** when prompted
        
5. Refresh Zone
    
    - Right-click zone → **Refresh**
        
6. Verification
    
    - Confirm **Host (A) record:**
        
        - `youtube` → `195.16.10.1`
            

✅ **Expected Result:**  
Record appears → **Zone transfer successful**

---
