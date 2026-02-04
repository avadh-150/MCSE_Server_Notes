
---

## 🧠 FIRST: UNDERSTAND THE SCENARIO (NO CONFUSION)

- 🏢 **Domain joined PC** → `abc.com`
    
- 👤 **User account** → `tom@iforward.in`
    
- 🔗 **Trust** → Forest Trust (Two-way)
    
- 🔐 **Auth** → Kerberos via trust
    

If you think “PC must join iforward.in to login tom” → **WRONG** ❌  
That’s not how AD works.

---

## ✅ PREREQUISITES (CHECK OR IT WILL FAIL)

Before touching Windows 10:

✔ Forest trust is **working and verified**  
✔ DNS conditional forwarders are **correct**  
✔ User **tom** exists in **iforward.in**  
✔ Time sync OK (Kerberos) ⏱️  
✔ Windows 10 DNS points to **abc.com DC** (NOT iforward.in)

Check DNS on Windows 10:

```
ipconfig /all
```

DNS **must be abc.com DC IP** 🧠

---

## 🖥️ STEP 1: JOIN WINDOWS 10 TO `abc.com` DOMAIN

On **Windows 10 PC**:

1️⃣ Open **Run** → `sysdm.cpl`  
2️⃣ Go to **Computer Name** tab  
3️⃣ Click **Change…**  
4️⃣ Select **Domain**

```
abc.com
```

5️⃣ Click **OK**

👉 Enter **abc.com Domain Admin** credentials  
(not iforward.in admin ❌)

✔ You should see:  
**“Welcome to the abc.com domain”**

6️⃣ Restart the PC 🔁

If this fails → DNS or firewall is broken. Period. 🧨

---

## 🖥️ STEP 2: LOGIN WITH FOREIGN DOMAIN USER (THIS IS KEY)

After reboot, you’re at Windows login screen.

### ✅ CORRECT WAY

```
tom@iforward.in
```

Enter **tom’s password**  
Login 🚀

If trust + DNS are right → login works.  
If not → Kerberos ticket request fails ❌

---

## 🧠 STEP 3: WHAT ACTUALLY HAPPENS (KNOW THIS OR YOU’RE GUESSING)

1️⃣ Windows 10 contacts **abc.com DC**  
2️⃣ abc.com DC sees user belongs to **iforward.in**  
3️⃣ Trust referral sent  
4️⃣ Kerberos ticket issued by **iforward.in DC**  
5️⃣ Access granted via trust

No NTLM. No hacks. Pure Kerberos 🔐

---

## 🚫 COMMON FAILURES (READ THIS CAREFULLY)

❌ “User name or password is incorrect”  
→ Trust broken or time skew ⏱️

❌ Login screen doesn’t accept foreign user  
→ Trust is **External**, not Forest ❌

❌ Can login but can’t access resources  
→ Permissions NOT granted (auth ≠ authorization)

---

## 🔐 STEP 4 (OPTIONAL BUT REAL-WORLD): RESOURCE ACCESS

Login success ≠ access success ⚠️

If **Selective Authentication** was chosen:

- You MUST grant **Allowed to Authenticate** on target servers
    

If **Forest-wide Authentication**:

- Still need **NTFS / Share permissions**
    

Example on abc.com File Server:

```
Add iforward.in\tom to folder permissions
```

Trust only opens the door 🚪  
Permissions decide how far he walks 🧠

---
