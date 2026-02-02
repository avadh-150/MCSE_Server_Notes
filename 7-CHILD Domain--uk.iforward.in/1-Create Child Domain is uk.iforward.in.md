
---

# ✅ COMPLETE STEP-BY-STEP: CREATE A CHILD DOMAIN (REAL WORLD + INTERVIEW SAFE)

---

## ⚠️ BEFORE YOU START — HARD RULES (READ THIS OR FAIL)

- ❌ Creating user **Tom** is **NOT REQUIRED**  
    → Video noise. Ignore it in real life & interviews.
    
- ✅ Static IP + Parent DNS = **MANDATORY**
    
- ✅ You MUST be **Enterprise Admin**
    
- ❌ If DNS is wrong → **Child Domain WILL FAIL**
    

---

## 🟢 PHASE 1: PRE-CHECKS (NON-NEGOTIABLE)

### 🔹 Step 1: Creating User `Tom`  on DC



---

### 🔹 Step 2: Configure Static IP (Child Server) on ukdc PC

1. Open **Network Adapter Settings**
    
2. IPv4 → Properties
    
3. Set:
    

```
IP Address:    10.10.11.15
Subnet Mask:   255.255.255.0
Gateway:       10.10.11.1
Preferred DNS: 10.10.11.10   ← PARENT DC ONLY
```

🚨 **DO NOT** put 8.8.8.8  
🚨 **DO NOT** put itself yet

👉 This is the #1 reason Child Domains fail 💀

---

### 🔹 Step 3: Verify DNS Resolution

```cmd
nslookup iforward.in
```

Must resolve to **Parent DC IP** ✅

---

## 🟢 PHASE 2: INSTALL AD DS ROLE

### 🔹 Step 4: Add AD DS Role

1. Open **Server Manager**

2. Click **Add Roles and Features**

	 ![Image](https://www.manageengine.com/log-management/cyber-security/images/promote-server-to-domain-controller-guide-01.png)

3. Next → Next
    
4. Select **Role-based or feature-based**
    
5. Select local server (`UKDC`)
    
6. Check ✅ **Active Directory Domain Services**

	![image](https://activedirectorypro.com/wp-content/uploads/2024/12/install-ad-ds-5.webp)

7. Click **Add Features**

	![image](https://activedirectorypro.com/wp-content/uploads/2024/12/install-ad-ds-6.webp)
	
8. Next → Next → Install

	![Image](https://www.server-world.info/en/Windows_Server_2016/active_directory/img/10.png)

9. Wait → Close

	![Image](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/media/install-active-directory-domain-services--level-100-/adds_smi_smpromotes.gif)


⚠️ This does **NOT** make it a DC yet.

---

## 🟢 PHASE 3: PROMOTE TO CHILD DOMAIN CONTROLLER


---

### 🔹 Step 5: Start Promotion Wizard

1. Server Manager → ⚠️ **Notification Flag**
    
2. Click **Promote this server to a domain controller**
    

---

### 🔹 Step 6: Deployment Configuration

Select:

- ✅ **Add a new domain to an existing forest**
    
- ✅ **Child Domain**
    

Enter:

```
Parent Domain Name : iforward.in

New Domain name :    uk
```
 
➡️ Resulting FQDN:

```
uk.iforward.in
```

Click **Next**

---

### 🔹 Step 7: Domain Controller Options

Check:

- ✅ DNS Server
    
- ✅ Global Catalog
    

Set:

```
Site Name: Default-First-Site-Name
DSRM Password: (Strong password)
```

Click **Next**

---

### 🔹 Step 8: DNS Delegation (IMPORTANT 🔥)

You will see:

```
☑ Create DNS delegation
```

#### 🔍 What this REALLY means:

- Parent DNS (`iforward.in`)
    
- Creates delegation for:
    

```
uk.iforward.in → Child DC IP
```

📌 **Why this matters**  
Without delegation:

- Parent users **cannot locate child DC**
    
- Logins FAIL
    
- Trust breaks
    
- AD becomes unusable
    

⚠️ If Parent DNS is **Windows DNS + AD-integrated**  
→ You can safely click **Next**

Click **Next**

---

### 🔹 Step 9: NetBIOS Name

Auto-generated:

```
UK
```

✅ Accept → Next

---

### 🔹 Step 10: Paths

Leave defaults:

```
Database: C:\Windows\NTDS
Logs:     C:\Windows\NTDS
SYSVOL:   C:\Windows\SYSVOL
```

Click **Next**

---

### 🔹 Step 11: Review Options

Confirm:

```
Forest: iforward.in
Child:  uk.iforward.in
```

Click **Next**

---

## 🟢 PHASE 4: POST-INSTALL VERIFICATION

After reboot:

### 🔹 Step 12: Verify Domain

```cmd
systeminfo | findstr Domain
```

Should show:

```
Domain: uk.iforward.in
```

---

### 🔹 Step 13: Verify DNS Zones

Open **DNS Manager** on Parent DC:

- Forward Lookup Zones:
    
    - iforward.in
        
    - uk.iforward.in ✅
        

---
