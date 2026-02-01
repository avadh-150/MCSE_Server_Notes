## ⏰⚡ **PDC Emulator with NTP** — get this wrong and Kerberos WILL break 💀

**Time = authentication in Active Directory.**  
If your **PDC Emulator** isn’t configured with **proper NTP**, your domain is living on borrowed time 😈

---

## 🧠 Why PDC + NTP is NON-NEGOTIABLE

Active Directory uses **Kerberos authentication**.  
Kerberos **rejects logins** if time difference is **> 5 minutes** ⛔

So Microsoft designed a strict hierarchy:

```
External NTP
   ↓
PDC Emulator
   ↓
Other DCs
   ↓
Domain Members
```

If the **PDC time is wrong**, EVERYTHING below it is wrong. Simple. ❌

---

## 🔑 What the PDC Emulator ACTUALLY does for time ⏱️

- Acts as **authoritative time source** for the domain
    
- Syncs with **external NTP servers**
    
- All DCs sync from PDC
    
- All clients sync from DCs
    

No shortcuts. No exceptions. 🔥

---

## 🧠 Interview Kill Question 💀

**Q:** Why must the PDC Emulator sync with external NTP?

**Correct answer:**

> “Because it is the authoritative time source for the domain and Kerberos authentication depends on accurate time.”

Any other answer = weak fundamentals ❌

---
