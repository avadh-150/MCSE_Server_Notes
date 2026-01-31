
---
# 🧠 Active Directory Sites & Services 

---

## 🎯 What This Configuration ACTUALLY Does (Read This First)

Active Directory **Sites** are about **network speed and replication**, not permissions.

If you skip this:

- Clients may authenticate to a **remote DC**
    
- Logons become slow 🐌
    
- Replication wastes WAN bandwidth 🌐
    

This setup ensures:  
✔ Users talk to the **nearest DC**  
✔ Replication is **controlled and efficient**

If you don’t have multiple subnets or locations, Sites are pointless. Period. ❌

---
# ✅ Proper Setup for **MUMBAI** and **SURAT**


## 🔹 Step 1: Open Active Directory Sites and Services

📍 **Where:** Domain Controller

1. Click **Start** → open **Server Manager**
    
2. Top-right → **Tools**
    
3. Click **Active Directory Sites and Services**
    

✅ This console controls **physical topology**, not logical AD objects.

---

## 🎯 Final Design (Lock This in Your Head First 🧠)

| Location      | Site Name  | Subnet            | Device |
| ------------- | ---------- | ----------------- | ------ |
| Mumbai Office | **MUMBAI** | `192.168.20.0/24` | DC+PC1 |
| Surat Office  | **SURAT**  | `172.16.1.0/24`   | ADC    |

- **DC (Main DC)** → MUMBAI
    
- **ADC (Additional DC)** → SURAT
    

This is what you are implementing. Nothing else. ❌

---

## 🔹 Step 2: Create TWO Sites (Correct Way)

📍 **Purpose:** Represent two physical office locations 🏢🏢

### ▶ Create SURAT Site

1. Open **Active Directory Sites and Services**
    
2. In left pane, right-click **Sites**
    
3. Click **New Site**
    
4. Enter:
    
    - **Site Name:** `SURAT`
        
    - **Site Link:** `DEFAULTIPSITELINK`
        
5. Click **OK**
    
6. Read the warning → click **OK**
    

✅ SURAT site created

---

### ▶ Create MUMBAI Site

7. Again, right-click **Sites**
    
8. Click **New Site**
    
9. Enter:
    
    - **Site Name:** `MUMBAI`
        
    - **Site Link:** `DEFAULTIPSITELINK`
        
10. Click **OK**
    
11. Click **OK** on the warning
    

✅ Now you have **2 sites: MUMBAI & SURAT**

⚠️ At this point, **sites do NOTHING** without subnets. Zero intelligence yet.

---

## 🔹 Step 3: Create and Assign Subnets (THIS IS THE BRAIN 🧠)

📍 **Purpose:** AD uses subnets to decide **which site a machine belongs to**

---

### ▶ Create SURAT Subnet

1. Expand **Sites**
    
2. Right-click **Subnets** → **New Subnet**
    
3. Enter:
    
    - **Prefix:** `172.16.1.0/24`
        
4. Under **Select a site**, choose **SURAT**
    
5. Click **OK**
    

✅ Any machine with IP `172.16.1.x` now belongs to **SURAT site**

---

### ▶ Create MUMBAI Subnet

6. Right-click **Subnets** → **New Subnet**
    
7. Enter:
    
    - **Prefix:** `192.168.20.0/24`
        
8. Under **Select a site**, choose **MUMBAI**
    
9. Click **OK**
    

✅ Any machine with IP `192.168.20.x` now belongs to **MUMBAI site**

---

## 🔹 Step 4: Move Domain Controllers to Correct Sites (VERY IMPORTANT)

📍 **Purpose:** Tell AD where each DC physically exists

---

### ▶ Move Main DC to MUMBAI Site

1. Expand **Default-First-Site-Name**
    
2. Expand **Servers**
    
3. Right-click **DC (Main Domain Controller)**
    
4. Click **Move**
    
5. Select **MUMBAI**
    
6. Click **OK**
    

✅ Main DC is now logically placed in **MUMBAI**

---

### ▶ Move ADC to SURAT Site

7. Still under **Default-First-Site-Name → Servers**
    
8. Right-click **ADC (Additional DC)**
    
9. Click **Move**
    
10. Select **SURAT**
    
11. Click **OK**
    

✅ ADC is now logically placed in **SURAT**

---

## ✅ Final State (If This Isn’t True, You’re Wrong ❌)

✔ MUMBAI site  
  ↳ Subnet: `192.168.20.0/24`  
  ↳ DC placed inside

✔ SURAT site  
  ↳ Subnet: `172.16.1.0/24`  
  ↳ ADC placed inside

   ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/SIte%20to%20services/2-site%20and%20services.png?raw=true) 

✔ No DC left in **Default-First-Site-Name** (except lab leftovers)

---

## 🔹 Step 5: Configure Site Links & Replication Behavior

📍 **Purpose:** Control **how and when** sites replicate

1. Expand **Inter-Site Transports**
    
2. Click **IP**
    
3. Right-click **DEFAULTIPSITELINK** → **Properties**
    

Configure:

- **Cost:**
    
    - Lower = preferred path
        
    - Use higher cost for slow WAN links 🐢
        
- **Replication Interval:**
    
    - 15 min (fast links)
        
    - 180 min (WAN links)
        
- **Schedule:**
    
    - Restrict replication to off-hours if needed
        

Click **OK**

   ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/SIte%20to%20services/4-Create%20the%20site%20link.png?raw=true)

⚠️ Don’t blindly lower cost everywhere.  
You’ll flood WAN links and regret it.

---

## 🧠 Final Mental Model (If You Can’t Explain This, You Don’t Know It)

- **Site** = Physical location 🏢
    
- **Subnet** = How AD identifies the location 🌐
    
- **DC in Site** = Where authentication & replication happen
    
- **Site Link** = Controls replication traffic 🚦
    

If any one of these is missing → configuration is incomplete ❌

---
