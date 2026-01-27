
---
# 🎯 GOAL 1

### ❌ Block Credential Manager on **PC1**

### ✅ Allow Credential Manager on **PC2 + all others**

---

## 🔹 STEP 1: Create GPO (Block CM for PC1)

1. Open **Group Policy Management** 🧩
    
2. Right-click the OU where **PC1** exists
    
3. **Create a GPO**
    
    - Name: `GPO_Block_Credential_Manager_PC1`
        

---

## 🔹 STEP 2: Configure Policy

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

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-1-Credential%20Manager%20BLock.png?raw=true)
---

## 🔹 STEP 3: Scope ONLY PC1 (CRITICAL)

### ❌ Do NOT rely only on OU if other PCs are there

**Security Filtering**:

- Remove: `Authenticated Users`
- Click **Add** and select **PC1** (ensure "Computers" is checked in Object Types). 
    
- Add: `PC1$`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-1.1-Object%20Typers.png?raw=true)

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-1.5-check_name.png?raw=true)

✅ Done.  
Only PC1 is affected.

---

## 🔄 Result

- ❌ PC1 → Credential Manager BLOCKED
    
- ✅ PC2 + others → NORMAL (no policy applied)

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-2-Scope%20of%20PC1.png?raw=true)

---

# 🧪 VERIFICATION (DON’T SKIP)

On PC1 / PC2 run:

```cmd
gpupdate /force
gpresult /r
```

Then open:

```
Control Panel → Credential Manager
```


![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-2.5-CM_bolcked.png?raw=true)


If blocked → options greyed out or error appears 😎

---

# 🎯 GOAL 2 policy (REVERSE)

##### Here the link of GOAL 2 Policy ....... 