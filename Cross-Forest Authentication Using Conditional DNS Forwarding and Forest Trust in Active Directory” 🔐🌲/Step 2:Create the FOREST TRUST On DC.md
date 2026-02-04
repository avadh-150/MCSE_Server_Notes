
---
## 🔴 BEFORE YOU EVEN TOUCH THE TRUST WIZARD (DON’T SKIP THIS)

If any of these are wrong, **trust creation will FAIL** 💥

✅ Conditional Forwarders

- `iforward.in` DC → forward `abc.com` → `10.10.11.20`
    
- `abc.com` DC → forward `iforward.in` → `10.10.11.10`
    
✅ Forest Functional Level

- **Both forests MUST be Windows Server 2003 or higher**
    
- Otherwise **Forest Trust option will be GREYED OUT** ❌
    
✅ Firewall

- TCP/UDP **88, 389, 445, 53, 135**
    
- Dynamic RPC ports open 🔥
    
---

## 🧠 WHAT YOU ARE ACTUALLY CREATING (UNDERSTAND THIS)

You are creating a:

✔ **Forest Trust**  
✔ **Kerberos-based**  
✔ **Transitive**  
✔ **Two-way** (in your example)

This is **NOT** an External Trust (that’s NTLM + non-transitive).  
Forest Trust = modern, clean, enterprise-grade 🧠

---

## 🚀 STEP-BY-STEP: CREATE THE TRUST (REAL WORLD FLOW)


![Image](https://0xdarkvortex.dev/assets/images/0014-active-directory-penetration-dojo-creation-of-forest-trustpart-3/Trust_types-1024x602.jpg)

---

### 🟢 STEP 1: Open Trust Console (ON PDC – NOT RANDOM DC)

On **iforward.in PDC Emulator** 👑

```
Server Manager → Tools → Active Directory Domains and Trusts
```

Right-click **iforward.in**  
👉 **Properties**  
👉 **Trusts tab**  
👉 **New Trust…**

Click **Next** ▶️

---

### 🟢 STEP 2: Trust Name

**Trust Name:**

```
abc.com
```

⚠️ Use **FQDN**, not NetBIOS.  
Click **Next**

---

### 🟢 STEP 3: Trust Type (THIS IS CRITICAL)

You will see:

- **External trust:**
	- A nontransitive trust between a domain and another domain outside the forest, bounded by the domains in the relationship ❌
    
- **Forest trust:** 
	- A transitive trust between two forests that allows users in any domain in one forest to be authenticated in any domain in the other forest. ✅

👉 **Select: Forest Trust**

Click **Next**

![image](https://cdn.ttgtmedia.com/digitalguide/images/Misc/kcip_tip_1.jpg)

---

### 🟢 STEP 4: Direction of Trust

Choose:  
👉 **Two-way**

This means:

- abc.com trusts iforward.in
    
- iforward.in trusts abc.com
    

Click **Next**

 ![image](https://cdn.ttgtmedia.com/digitalguide/images/Misc/kcip_tip_2.jpg)

- **Two-way:** Users in both domains can authenticate in the other. 
- **One-way, incoming:** Users in the current domain can be authenticated in the specified domain. 
- **One-way, outgoing:** Users in the specified domain can be authenticated in the current domain.

---

### 🟢 STEP 5: Sides of Trust

Select:  
👉 **Both this domain and the specified domain**
- selected the option to create both ends of the trust.

This saves you from manually creating trust on the other side 💡

Click **Next**

![image](https://cdn.ttgtmedia.com/digitalguide/images/Misc/kcip_tip_3.jpg)

---

### 🟢 STEP 6: Authentication – Specified Forest

Same question, opposite direction.

👉 Again select **Forest-wide authentication**

Click **Next**

---

### 🟢 STEP 7: Authentication – Local Forest (IMPORTANT)

**Outgoing Trust Authentication Level – Local Forest**

Choose ONE:

✔ **Forest-wide authentication**

- This option gives users from the other network broad access to all resources in your network by default. 

- It's best used when both networks belong to the **same organization**

✔ **Selective authentication**

- Users from the other network are denied access to everything by default. An administrator must specifically allow access to **individual** computers or servers

- used in **different organizations**
    
Click **Next**

![image](https://cdn.ttgtmedia.com/digitalguide/images/Misc/kcip_tip_4.jpg)

---
### 🟢 STEP 8: Outgoing Trust Authentication Level – Specified Forest

👉  The questions are the same here to allow you to select Forest Wide or Selective Authentication, from the remote forest to the local forest.


Click **Next** 

---
### 🟢 STEP 9: Review & Create

You’ll see a **summary screen**  
👉 Verify:

- Trust Type: Forest
    
- Direction: Two-way
    
- Authentication: Forest-wide
    

Click **Next** → Trust gets created 🛠️

---
### 🟢 STEP 10: Confirm the Trust (DO NOT SKIP)

You will be asked:

✔ Confirm outgoing trust? → **YES** 


✔ Confirm incoming trust? → **YES**

If confirmation fails → DNS or time is broken. No excuses 🧨

---

## ✅ FINAL VERIFICATION

Back in **Trusts tab**, you should see ON DC of **[iforward.in]:**

✔ `abc.com`  
✔ Type: **Forest**  
✔ Direction: **Two-way**


Back in **Trusts tab**, you should see ON dc of **[abc.in]:**

✔ `iforward.com`  
✔ Type: **Forest**  
✔ Direction: **Two-way**



---

## 🧠 COMMON MISTAKES I’M CALLING OUT

❌ Creating trust before DNS forwarders  
❌ Using External Trust “because it worked”  
❌ Wrong forest functional level  
❌ Time skew ignored  
❌ Running wizard on random DC, not PDC  
❌ Selecting Selective Auth without understanding permissions

If you do any of the above, you’re **guessing, not administering** 🤦‍♂️
👊

---