
---

# 🧠 Network Configuration & Verification (Clean + Understandable)

### 🎯 Goal (Understand This First)

- **DC** and **PC1** are on **192.168.20.0/24**
    
- **PC2** is on a **different subnet (172.16.1.0/24)**
    
- **All machines use the DC as DNS**
    
- We verify **cross-subnet communication + DNS behavior**

---

## 🔹 Phase 1: Configure Domain Controller (DC) IP

📍 **Machine:** Domain Controller

1. Press `Win + R` → type `ncpa.cpl` → Enter
    
2. Right-click **Ethernet** → **Properties**
    
3. Select **IPv4** → **Properties**
    
4. Set:
    
    - **IP Address:** `192.168.20.10`
        
    - **Subnet Mask:** `255.255.255.0`
        
    - **Default Gateway:** `192.168.20.1`
        
    - **Preferred DNS:** `192.168.20.10` (itself)
        

✅ DC must always point to **itself as DNS**.  
If you mess this up, AD breaks. Period. 💥

---

## 🔹 Phase 2: Configure PC1 (Same Subnet as DC)

📍 **Machine:** PC1

1. `Win + R` → `ncpa.cpl`
    
2. Ethernet → **Properties**
    
3. IPv4 → **Properties**
    
4. Set:
    
    - **IP Address:** `192.168.20.11`
        
    - **Subnet Mask:** `255.255.255.0`
        
    - **Default Gateway:** `192.168.20.1`
        
    - **Preferred DNS:** `192.168.20.10` (DC)
        

✅ This is **correct AD client configuration**  
❌ Never point DNS to Google or router in a domain. Ever. 🚫

---

## 🔹 Phase 3: Configure PC2 (Different Subnet – This Is the Key Part)

📍 **Machine:** ADC-PC2

1. `Win + R` → `ncpa.cpl`
    
2. Ethernet → **Properties**
    
3. IPv4 → **Properties**
    
4. Set:
    
    - **IP Address:** `172.16.1.10`
        
    - **Subnet Mask:** `255.255.255.0`
        
    - **Default Gateway:** `172.16.1.1`
        
    - **Preferred DNS:** `192.168.20.10` (DC)
        

⚠️ **Important Warning :**  PC2 is NOW ADC OR create the PC2 as a ADC... 

---

## 🔹 Phase 4: Refresh DNS Zone on DC

📍 **Machine:** DC

1. Open **DNS Manager**
    
2. Expand **Forward Lookup Zones**
    
3. Right-click `iforward.in`
    
4. Click **Reload** or **Refresh**
    

✅ This forces the DC to update DNS records instead of waiting.

---

## 🔹 Phase 5: Final Verification (This Proves Everything Works)

### ✅ From DC

Open Command Prompt and run:

```
ping 172.16.1.10
```

✔ Confirms routing + reachability

Then:

```
ping -t 172.16.1.10
```

✔ Confirms **stable connectivity**, not just luck 🎯

---

### ✅ From PC2

Open Command Prompt:

```
ipconfig /all
```

Verify:

- **IP Address:** `172.16.1.10`
    
- **DNS Server:** `192.168.20.10`
    
- **Primary DNS Suffix:** `iforward.in`
    

If DNS suffix is missing → AD/DNS is NOT working ❌  
No excuses.

---
