
---
# 🔐 Fine-Grained Password Policy (FGPP) in Active Directory

---

## 🛠 Method 1: Create FGPP using Active Directory Administrative Center (GUI)

### 🧭 Step 1: Open ADAC

1️⃣ Open **Server Manager**  
2️⃣ Go to **Tools** → **Active Directory Administrative Center**

---

### 🗂 Step 2: Navigate to Password Settings Container

3️⃣ In ADAC, click your **Domain Name**  
4️⃣ Select **System**  
5️⃣ Open **Password Settings Container**

---

### ➕ Step 3: Create a New Password Policy

6️⃣ Click **New** → **Password Settings**
![image](https://specopssoft.com/wp-content/uploads/2018/03/Password-settings-new.png)

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

---

### 🎯 Step 5: Assign the Policy

7️⃣ In **Directly Applies To**, click **Add**  
8️⃣ Select:

- 👤 Specific users **OR**
    
- 👥 Global Security Groups  
    9️⃣ Click **OK** → **Create**
    

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

---

### 5️⃣ Confirm Success ✅

You’ll see:

> _The password for <username> has been reset._

That’s it. No reboot. No gpupdate. .