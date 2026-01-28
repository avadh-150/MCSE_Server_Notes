
---
# 🔐 Fine-Grained Password Policy (FGPP) in Active Directory

---

## 🛠 Method 1: Create FGPP using Active Directory Administrative Center (GUI)

### 🧭 Step 1: Open ADAC

1️⃣ Open **Server Manager**  
2️⃣ Go to **Tools** → **Active Directory Administrative Center**

  ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/1-FGPP.png?raw=true)

---

### 🗂 Step 2: Navigate to Password Settings Container

3️⃣ In ADAC, click your **Domain Name**  
4️⃣ Select **System**  
5️⃣ Open **Password Settings Container**

  ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/2-fgpp.png?raw=true)

---

### ➕ Step 3: Create a New Password Policy

6️⃣ Click **New** → **Password Settings**

<img width="452" height="238" alt="image" src="https://github.com/user-attachments/assets/c409eaa9-54bc-404d-8ecd-76183150b6fa" />

---
### ⚙️ Step 4: Configure Password Settings (PSO)

| Setting                         | Example Value | Reality Check                  |
| ------------------------------- | ------------- | ------------------------------ |
| 🔤 **Name**                     | `Boos`        | Must be unique                 |
| 🧮 **Precedence**               | `1`           | Lower number = higher priority |
| 🔁 **Enforce password history** | `24`          | Stops reuse                    |
| ⏳ **Maximum password age**      | `30 days`     | Shorter = safer                |
| ⛔ **Minimum password age**      | `1 day`       | Prevents instant reset         |
| 🔢 **Minimum password length**  | `14`          | Anything less is weak          |
| 🔐 **Password complexity**      | Enabled       | Mandatory                      |
| 🔒 **Reversible encryption**    | Disabled      | Always                         |

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/3-Fine-Grained%20Password%20Policy.png?raw=true)

---

### 🎯 Step 5: Assign the Policy

7️⃣ In **Directly Applies To**, click **Add**  
8️⃣ Select:

- 👤 Specific users **OR**
    
- 👥 Global Security Groups  
    9️⃣ Click **OK** → **Create**

    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/4-ADD.png?raw=true)

    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/5-Success.png?raw=true)
---

## 🚀 Step 6: Force Policy Update (Optional)

```bash
gpupdate /force
```

⚠️ FGPP is evaluated during **password change**, not login.

---

## 🧪 Verify FGPP (DO NOT SKIP)

### 🔎 Using Command Prompt

```bash
net user username /domain
```

Check:

```
Minimum password length
```

---
### * Reset the Password 🔐

- Right-click the **user account** `Boss User`
    
- Click **Reset Password**
    
![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/6-userboss.png?raw=true)

⚠️ You’ll see a security warning — that’s normal.  
Click **Proceed**

---

### 4️⃣ Set the New Password

- Enter the **New password**
    
- Confirm the password
    

Optional (but important):

☑️ **User must change password at next logon** → Best practice  
☐ User cannot change password → Only for service accounts  
☐ Password never expires → Only if you like security incidents

Click **OK**

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/7-reset_pass.png?raw=true)

---

### 5️⃣ Confirm Success ✅

You’ll see:

> _The password for <username> has been reset._

That’s it. No reboot. No gpupdate. .

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Group%20Policy/Fine-Grained%20Password%20Policy/8-done.png?raw=true)

---
