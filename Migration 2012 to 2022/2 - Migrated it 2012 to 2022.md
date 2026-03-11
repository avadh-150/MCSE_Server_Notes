
Since you want to use this **2-server lab for migration practice**, I’ll explain **what migration means, why we build this lab, and how the work is done step-by-step**.

Your current lab:

| Server                 | Role                  | IP          |
| ---------------------- | --------------------- | ----------- |
| **dc2012**             | Old Domain Controller | 10.10.11.20 |
| **Win2022 (Server 2022)** | New Server            | 10.10.11.21 |

This setup simulates a **real company upgrade scenario**.

---

# 1️⃣ Why We Create This Migration Lab

In companies, old servers eventually become outdated.

Example:

|Old Infrastructure|New Infrastructure|
|---|---|
|Windows Server 2012|Windows Server 2022|
|Old hardware|New hardware|
|Old AD/DNS|Updated AD/DNS|

So companies perform **Active Directory Migration**.

### Real-world example

Company running:

```
DC01 (Windows Server 2012)
```

But Microsoft support ends, so they install:

```
DC02 (Windows Server 2022)
```

Then **migrate everything**:

- Active Directory
    
- DNS
    
- Users
    
- Groups
    
- Policies
    
- FSMO roles
    

After migration they **remove the old DC**.

Your lab is **simulating exactly this process**.

---

# 2️⃣ Goal of Your Migration Lab

You will simulate this:

```
OLD DC (dc2012)
        ↓
NEW DC (Win2022 - Server 2022)
```

Final result:

```
Win2022 becomes the main Domain Controller
dc2012 is removed
```

---

# 3️⃣ Step-by-Step Migration Process

## Step 1 — Create the Old Domain

On **dc2012**

Install:

```
Active Directory Domain Services
DNS
```

Create domain:

```
iforward.in
```

Result:

```
dc2012.iforward.in
IP: 10.10.11.20
```

This server is **original domain controller**.

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/manager-%3Eremove%20roles%20and%20feature.png?raw=true)

---

## Step 2 — Join New Server to Domain

On **Win2022 (Server 2022)**

Join the domain:

```
iforward.in
```

Now structure becomes:

```
dc2012 (Domain Controller)
Win2022 (Member Server)
```

---

## Step 3 — Promote New Server to Domain Controller

Now convert **Win2022 → Domain Controller**.

Install role:

```
Active Directory Domain Services
```

Then click:

```
Promote this server to domain controller
```

Select:

```
Add a domain controller to existing domain
```

Domain:

```
iforward.in
```

Now environment becomes:

```
dc2012  → Domain Controller
Win2022    → Domain Controller
```

You now have **2 Domain Controllers**.

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/dc2022%20is%20dc.png?raw=true)

---

# 4️⃣ What Happens After Promotion

Important services replicate automatically:

|Service|What happens|
|---|---|
|Active Directory|Replicated|
|Users|Replicated|
|Groups|Replicated|
|DNS zones|Replicated|
|GPO|Replicated|

Both servers now have **same AD database**.

- **Users**
![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/Replicate%20users.png?raw=true)

- **GPO**
![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/Replicate%20GPO.png?raw=true)

---

# 5️⃣ Transfer FSMO Roles ON Win2022

Now you move **FSMO roles** to new server.

FSMO roles are **5 critical AD roles**.

|Role|Purpose|
|---|---|
|Schema Master|Controls schema changes|
|Domain Naming Master|Adds/removes domains|
|RID Master|Generates SID numbers|
|PDC Emulator|Password & time sync|
|Infrastructure Master|Updates cross-domain references|

Transfer them to **Win2022**.

Check roles:

```
netdom query fsmo
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/FSMO%20role%20transfer%20to%202022.png?raw=true)

---

# 6️⃣ Make New Server Primary DNS

Now ensure DNS clients use:

```
10.10.11.21
```

instead of:

```
10.10.11.20
```

This ensures **Win2022 handles authentication**.

---

# 7️⃣ Demote the Old Domain Controller

Once migration is confirmed working:

On **dc2012**:

```
Server Manager
Remove Roles
AD DS
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/Remove%20ADDS+DNS.png?raw=true)

This **demotes the server**.

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/Demote%20the%20DC.png?raw=true)


Now infrastructure becomes:

```
Win2022 (Windows Server 2022)
Domain Controller
DNS
Active Directory
Configure the New Dns Forworder 
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/set%20new%20dns%20forwarder.png?raw=true)

---

# 8️⃣ Final Infrastructure

```
Domain: iforward.in

Win2022 (Server 2022)
IP: 10.10.11.21
Role:
✔ Domain Controller
✔ DNS
✔ FSMO Roles
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/finish%20the%20win2022%20is%20now%20dc.png?raw=true)

Old server **dc2012 is removed**.

### After Migrating dc2012 it change the Schema Version 

like **Before** Migrate the **Schema Version is 69**

![](https://theitbros.com/wp-content/uploads/2018/03/Active_Directory_Schema_configuration.png)

**After Migrating dc2012 it change the Schema Version to 88**

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/schema_version%20is%20Change%20to%2088.png?raw=true)

---

# 9️⃣ Why Companies Do This

Reasons:

|Reason|Explanation|
|---|---|
|Security|New OS has patches|
|Performance|Better hardware|
|Support|Old server unsupported|
|Features|New AD features|

---

# 🔟 Skills You Learn From This Lab

This lab teaches **real enterprise tasks**:

✔ Active Directory migration  
✔ Domain controller promotion  
✔ FSMO transfer  
✔ DNS replication  
✔ DC demotion  
✔ Server upgrade strategy

These are **very common tasks in jobs like**:

- System Administrator
    
- Windows Administrator
    
- Infrastructure Engineer
    
- Cloud Engineer
    

---

💡 Since you are learning **MCSE / Windows Server**, I can also show you the **full professional migration lab used by Microsoft trainers**:

```
Client PC
    │
    │
Router (GNS3)
    │
    │
DC2012 (Old DC)
    │
    │
DC2022 (New DC)
```

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Migration%202012%20to%202022/dc12%20see%20the%20DC%20on%20dsa.msc.png?raw=true)

This lab lets you practice:

- AD Migration
    
- DNS Migration
    
- DFSR
    
- Failover Cluster
    
- AD Backup & Recovery
    

