## 🧪 **`dcdiag` command** — if you don’t use this, you’re guessing, not troubleshooting ❌

![Image](https://4sysops.com/wp-content/uploads/2019/04/Use-DcDiag-with-PowerShell-to-check-domain-controller-health.png)

![Image](https://lazyadmin.nl/wp-content/uploads/2023/08/image-20.png)

![Image](https://windowstechno.com/wp-content/uploads/2022/08/DCDIAG-Replications.png)

I’ll be blunt: **`dcdiag` is the first command a real AD admin runs when things smell wrong**.  
If you skip it and jump to random fixes, you’re doing amateur-hour admin work 😬🔥

---

## 🧠 What `dcdiag` ACTUALLY does

`dcdiag` = **Domain Controller Diagnostic Tool**

It:

- Tests **health of a Domain Controller**
    
- Checks **AD DS, DNS, replication, FSMO**
    
- Flags **misconfigurations & failures**
    

This is NOT optional in production. 🧠⚙️

---

## ▶️ Basic Command (minimum you should know)

```powershell
dcdiag
```

What it tests:

- Connectivity
    
- Advertising
    
- Services
    
- Replication
    
- FSMO awareness
    

If you don’t understand the output → study more 📚❌

---

## 🎯 Most Useful `dcdiag` Commands (real-world)

### 🔹 Test DNS (MOST COMMON FAILURE)

```powershell
dcdiag /test:dns
```

If DNS is broken, **AD is broken**. No debate. 🚨

---

### 🔹 Run on ALL DCs

```powershell
dcdiag /e
```

Enterprise-wide check. Use this **before blaming replication**.

---

### 🔹 Verbose output (for real troubleshooting)

```powershell
dcdiag /v
```

More data. More truth. More responsibility 😈

---

### 🔹 Specific DC

```powershell
dcdiag /s:DC01
```

Targeted testing. Stop guessing.

---

### 🔹 Specific test only

```powershell
dcdiag /test:replications
```

or

```powershell
dcdiag /test:services
```

Precision > noise 🎯

---

## 📊 Common Tests You MUST recognize

|Test|Meaning|
|---|---|
|Connectivity|Can DC talk to others|
|Advertising|DC advertising itself properly|
|Replications|AD replication health|
|FSMOCheck|FSMO role availability|
|Services|AD-related services running|
|DNS|SRV records, zone health|

If **Advertising fails** → clients won’t find DCs ❌  
If **Replication fails** → inconsistent AD 💣

---

## 🚨 Typical Errors (and what they REALLY mean)

- ❌ **DNS failure** → Wrong DNS server set on DC
    
- ❌ **Replication error** → USN rollback / network issue
    
- ❌ **FSMOCheck failed** → Role holder unreachable
    
- ❌ **Advertising failed** → DC not usable for logons
    

Stop rebooting and “hoping” — read the output 📖😡

---

## 🛠️ Best Practice (non-negotiable)

- Run `dcdiag` **after every DC promotion**
    
- Run it **before production changes**
    
- Run it **when users complain about login**
    
- Run it **before touching FSMO roles**
    

---
