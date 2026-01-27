
---
# 🎯 GOAL 2 (REVERSE)

### ❌ Block Credential Manager on **PC2** and All Other PC

### ✅ Allow Credential Manager **ONLY on PC1**

👉 **THIS CANNOT BE DONE from IT OU ALONE**  
Because IT OU contains **only PC1**

---

# ✅ PROPER & CLEAN SOLUTION 

## 🔥 STEP 0: Accept the truth

To block **PC2 + all others**, your GPO must be linked to a container that **contains PC2 + others**

That container is usually:

```
Domain root
OR
A parent Computers OU
```

---

## 🔹 STEP 1: Where to CREATE the REVERSE GPO (IMPORTANT)

📍 **DO NOT create this one in IT OU**

Create it here 👇

```
Group Policy Management
 └─ Domains
    └─ iforward.in   ✅ (Domain root)
```

Right-click **iforward.in** →  

   👉 `Create a GPO in this domain, and Link it here`

Name:

```
Block Credential Manager In All Other PC but Except only PC1
```

💥 This ensures PC2 and every other PC can be targeted.

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3-create%20the%20GPO%20in%20root%20domain.png?raw=true)

---

## 🔹 STEP 2: Configure Credential Manager (Same settings)

Go to:

```
   > Computer Configuration
    > Windows Settings
    > Security Settings
    > System Services
    > **Credential Manager**
```

### Proper Steps to Configure the Service:


6. Scroll down the list of services in the right-hand pane until you find **Credential Manager**.
    
7. Double-click it.
    
8. Check the box for **Define this policy setting**.
    
9. Select **Disabled** as the service startup mode.
    
10. Click **OK**.

No change here. Policy logic stays the same 🔒

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-1-Credential%20Manager%20BLock.png?raw=true)
  
---

## 🔹 STEP 3: Security Filtering (THIS DEFINES WHO GETS HIT)

### 3️⃣1 In **Scope** tab

❌ Remove:

```
Authenticated Users
```

✅ Add:

```
Domain Computers
```

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3.1-domain%20Computer%20added.png?raw=true)


![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3.2-Show%20the%20Domain%20IN%20scope%20tab.png?raw=true)


👉 This blocks **ALL computers in the domain**

---

## 🔹 STEP 4: EXCLUDE PC1 (Exception Logic)

Go to:

```
Delegation → Advanced
```

Add:

```
PC1$
```

Set permissions:

- Go TO The Deny Column

| Permission         | Setting |
| ------------------ | ------- |
| Read               | ❌ Deny  |
| Apply Group Policy | ❌ Deny  |

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3.3-pc1%20Deny%20permits%5C.png?raw=true)

🔥 This is what allows PC1 while blocking everyone else.

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3.4-show%20the%20Delegation%20tab.png?raw=true)

---
## 🔹 STEP 5: EXCLUDE PC1 (Exception Logic)

### ❗ IMPORTANT DISTINCTION (DO NOT MISS THIS)

### 🔹 Unlink The GPO of First Create the to Block Only PC1

What you did:

- ✅ **Unlink** (safe)
    
- ❌ NOT deleted (also correct)
    

Why this matters:

- Unlink = GPO exists but **does not apply**
    
- Delete = GPO is gone forever 💀
    
![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3.5-Unlink%20the%20Pc%201%20policy.png?raw=true)

👉 You chose the **safe, professional option**

---

## 🔄 FINAL RESULT (NO CONFUSION NOW)

| Computer      | CM Result | Why           |
| ------------- | --------- | ------------- |
| PC1           | ✅ ALLOWED | Explicit DENY |
| PC2           | ❌ BLOCKED | Domain GPO    |
| Any future PC | ❌ BLOCKED | Auto          |

---

## 🧪 VERIFICATION (MANDATORY)

On PC1 & PC2:

```cmd
gpupdate /force
gpresult /r
```

Check:

```
Control Panel → Credential Manager
```

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-3.6-Block%20the%20All%20other%20PC%20.png?raw=true)

---
