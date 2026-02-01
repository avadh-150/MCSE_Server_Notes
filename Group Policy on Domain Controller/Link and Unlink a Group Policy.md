## 🔗 What does **“Linking a Group Policy”** REALLY mean?

**Brutal truth first** 👇

A **Group Policy Object (GPO)** does **nothing** by default.  
Creating a GPO ≠ applying a GPO ❌

👉 **Linking a GPO** means:

> Linking a **Group Policy** Object (GPO) means connecting a configured set of policies to specific **AD containers**—such as Sites, Domains, or Organizational Units (OUs)—to apply settings to users or computers. 
> A created GPO remains inactive until linked.

No link = no effect. Zero. Useless. 🧠⚠️

---

## 🧠 Where can a GPO be linked? (Know this or fail interviews)

- **Site** → affects computers in that site
    
- **Domain** → affects ALL users & computers
    
- **OU (Recommended)** → affects only objects inside that OU ✅
    

👉 **Best practice:** Always link to **OU**, not Domain.

---

## 🛠 STEP-BY-STEP: Link a Group Policy (CORRECT WAY)

### ✅ Step 1: Open Group Policy Management

- On **DC**
    
- `Server Manager` → `Tools` → **Group Policy Management**
    

---

### ✅ Step 2: Locate your Domain

```
Forest
 └── Domains
     └── iforward.in
```

---

### ✅ Step 3: Select Group Policy Objects

Example:

```
iforward.in
 └── Group Policy Objects
```

- Click **New**

![image](https://support.globalsign.com/application/files/4917/5205/4634/picture_2_1.jpg)

- Create the **NEW GPO**

![image](https://support.globalsign.com/application/files/9217/5205/4666/picture_3_1.jpg)

---

### ✅ Step 4: Link the GPO

- Right-Click the GPO, and select **Edit** 
	- Change any of the policies you want to apply in the Computer and\or User Configuration. Close the GPO Editor when you are done. _
	
	- Note: Check the Public Key Policies section for how to configure policies for Certificate Automation Manager.
		![image](https://support.globalsign.com/application/files/2317/5205/4958/picture_5.jpg)

- Right-click the **Group Policy Objects**
    
- Click **Link an Existing GPO**
    
- Select your GPO
    
- Click **OK**

![image](https://support.globalsign.com/application/files/7117/5205/4940/picture_6.jpg)

🎯 Done. The policy is now ACTIVE.

---

## ❌ How to **Unlink (Unapply) a GPO** (WITHOUT deleting it)

### ✅ Step-by-step:

1. Open **Group Policy Management**
    
2. Select the **OU**
    
3. Under **Linked Group Policy Objects**

### ✅ Delete GPO:

1. Right-click the GPO
    
2. Click **Delete**

	![image](https://cdn.infrasos.com/wp-content/uploads/2023/11/group-policy-management-confirmation-windo.webp)

🚨 **Important truth**:

- ❌ This does **NOT delete the GPO**
    
- ✅ It only removes the **link**
    
- GPO still exists in **Group Policy Objects**
    

---

## 🧷 What does **“Enforced”** mean? (This is where people screw up)

### 🔥 Brutal explanation:

**Enforce = “Shut up and obey”**

If a GPO is **Enforced**:

- Child OUs **CANNOT override it**
    
- Even **Block Inheritance** won’t stop it 😈
    

---

## 🛠 STEP-BY-STEP: Enforce a GPO

### ✅ Steps:

1. Open **Group Policy Management**
    
2. Go to the **OU / Domain** where GPO is linked
    
3. Under **Linked Group Policy Objects**
    
4. Right-click the GPO
    
5. Click **Enforced**
    

✔️ A **lock icon** appears 🔒

---

## ❌ How to **Remove Enforce**

- Right-click the GPO again
    
- Click **Enforced** (toggle OFF)
    

---

## 🧱 Block Inheritance vs Enforce (MEMORIZE THIS)

|Feature|Effect|
|---|---|
|**Block Inheritance**|Blocks parent GPOs ❌|
|**Enforced**|Overrides Block Inheritance ✅|
|Enforced + Block|**Enforced wins** 🏆|

👉 Interview answer:

> “Enforced GPOs cannot be blocked by child OUs even if Block Inheritance is enabled.”

---

## ⚡ Apply changes FAST (don’t wait 90 minutes like a noob)

On Client PC:

```cmd
gpupdate /force
```

Verify:

```cmd
gpresult /r
```


---

## 🧠 Real-World Scenario (EXAM / INTERVIEW GOLD)

> Company wants **Password Policy** for all users  
> ✔️ Link GPO at **Domain level**  
> ✔️ Enforce = **YES**

> USB Block only for Mumbai Office  
> ✔️ Create **Mumbai-Computers OU**  
> ✔️ Link GPO to that OU  
> ❌ Do NOT enforce

---
