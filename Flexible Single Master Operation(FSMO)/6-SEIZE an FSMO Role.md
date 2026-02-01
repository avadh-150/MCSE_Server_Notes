## 🔥 **How to SEIZE an FSMO Role from ADC to DC** ☠️

---

## 🧠 Scenario Assumption (important)

- ❌ **ADC is DEAD** (crashed, disk failure, deleted VM)
    
- ❌ ADC will **NEVER** come back online
    
- ✅ You want to seize FSMO roles to **DC**
    

If this assumption is wrong → STOP HERE 🚫

---

## 🛑 Step 0: Confirm current FSMO holder (MANDATORY)

Run on **DC**:

```powershell
netdom query fsmo
```

Confirm roles are still pointing to **ADC**.  
If you don’t verify this → you’re reckless ❌

---

## ⚠️ Step 1: Log in to DC (Administrator)

- **DC is Completely Fail not Responses** AND **Crash**

- At this Senario We **Transfer the All FSMO 'ROLEs' to ADC** 
  

---

## 🔥 Step 2: Start NTDSUTIL On ADC

```powershell
ntdsutil
```

You are now holding a loaded gun 😈

![image](https://techijack.com/wp-content/uploads/2019/04/ntdsutil.png)

---

## 🔁 Step 3: Enter FSMO role management

```powershell
roles
```

 ![image](https://techijack.com/wp-content/uploads/2019/04/roles.png)

---

## 🔌 Step 4: Connect to the NEW DC (target)

```powershell
connections
connect to server ADC
quit
```

![image](https://techijack.com/wp-content/uploads/2019/04/quit-fsmo.png)

⚠️ **You connect to the DC that will RECEIVE the role**, NOT the dead ADC.

---

## ⚡ Step 5: SEIZE the required FSMO role

Now issue **ONLY the role you need** 👇

![image](https://i.ytimg.com/vi/yzd7lXhZ_3I/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLDAmDPIvTCT3nz-NEVTfiSvbFP1Zw)

### 🔹 Seize PDC Emulator

```powershell
seize pdc
```

---
### 🔹 Seize RID Master

```powershell
seize rid master
```

---
### 🔹 Seize Infrastructure Master

```powershell
seize infrastructure master
```

---
### 🔹 Seize Schema Master

```powershell
seize schema master
```

![image](https://techijack.com/wp-content/uploads/2019/04/Seize-schema-master.png)

![image](https://techijack.com/wp-content/uploads/2019/04/role-seizure.png)

---
### 🔹 Seize Domain Naming Master

```powershell
seize domain naming master
```

⛔ Do NOT seize all blindly unless ADC is completely destroyed.

---

## 🚨 What you WILL see (don’t panic)

- Transfer will **fail first** ❌
    
- Then NTDSUTIL **forces seizure** ✅
    
- This is expected behavior
    

If transfer succeeds → ADC wasn’t dead → YOU MESSED UP 😡

---

## ✅ Step 6: Exit NTDSUTIL

```powershell
quit
quit
```

---

## 🔍 Step 7: VERIFY FSMO roles (NON-OPTIONAL)

```powershell
C:\Users> netdom query FSMO
    
Schema master      			ADC.iforward.in
Domain naming master		ADC.iforward.in
PDC							ADC.iforward.in
RID pool manager			ADC.iforward.in
Infrastructure master		ADC.iforward.in

The command completed successfully.
      
C:\Users>  
```

All roles must now show **ADC**.

If they don’t → you failed ❌

---

## 🧠 Which roles are SAFE vs DANGEROUS to seize?

|Role|Seize Risk|
|---|---|
|PDC Emulator|🔥 High impact|
|RID Master|🔥 High impact|
|Infrastructure Master|Medium|
|Schema Master|⚠️ Extreme|
|Domain Naming Master|⚠️ Extreme|

Forest roles = **only seize if absolutely unavoidable**.

---

## 🧠 Interview Kill Question 💀

**Q:** When should FSMO roles be seized?

**Correct answer:**

> “Only when the original FSMO role holder is permanently unavailable and cannot be recovered.”

Anything else = rejection ❌

---
