
---

# 🔐 Windows Server Account Policies – Password Policy Configuration (GPO)


> 🎯 **Scope:** Domain-wide password policy configuration  
> 🛑 **Important:** These settings must be applied at the **domain level**, not at the OU level.

---

## 🧭 Phase 1: Open Group Policy Management

1. Open **Server Manager** 🖥️
    
2. Click **Tools** (top-right)
    
3. Select **Group Policy Management**
    
4. In the left pane, expand:
    
    ```
    Forest
     └── Domains
         └── iforward.in
			   └──  Default Domain Policy      
    ```
    

---

## 🗂 Phase 2: Edit Default Domain Policy

1. Right-click **Default Domain Policy**
    
2. Click **Edit**
    

⚠️ **Why Default Domain Policy?**  
Password policies are part of **Account Policies**, which are processed **only by Domain Controllers** when linked at the **domain root**.  
Linking this GPO to an OU will **NOT** affect domain users — only local machine accounts.

---

## 🔍 Phase 3: Navigate to Password Policy

In the **Group Policy Management Editor**, follow this path:

```
Computer Configuration
 └── Policies
     └── Windows Settings
         └── Security Settings
             └── Account Policies
                 └── Password Policy
```

![image](https://www.it-react.com/wp-content/uploads/2020/02/password_requirements1.jpg)

---

## ⚙️ Phase 4: Configure Password Policy Settings
    
| **Setting**                                       | **Recommendation / Explanation**                                                                                                                                               |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 🔁**Enforce password history**                    | Determines how many unique new passwords must be used before an old one can be reused (e.g., **24 passwords remembered**).                                                     |
| ⏳**Maximum password age**                         | Sets the timeframe before a user is forced to change their password (e.g., **42 days**).                                                                                       |
| ⛔**Minimum password age**                         | Prevents users from immediately changing their password back to an old one (e.g., **1 day**).                                                                                  |
| 🔢**Minimum password length**                     | Sets the minimum number of characters required (e.g., **7 or 14 characters**).                                                                                                 |
| 🔐**Complexity requirements**                     | If **Enabled**, passwords must contain 3 of 4 categories: Uppercase - (A through Z), Lowercase(a through z), Numbers (0 through 9), and Symbols (- - for example, !, $, #, %). |
| ⚠️**Store passwords using reversible encryption** | Should generally be **Disabled** unless required by specific legacy applications, as it is less secure.                                                                        |
![image](https://i.sstatic.net/GytdS.png)

### ⚙️ Configure Minimum Password Length

6️⃣ Double-click **Minimum password length**  

![image](https://i0.wp.com/techdirectarchive.com/wp-content/uploads/2022/07/Define-Various-Password-Policies.jpg?resize=650%2C400&ssl=1)

7️⃣ Check ✅ **Define this policy setting**  
8️⃣ Set the value:

- Example:
    
    - `7` → basic security ❌
        
    - `12–14` → strong security ✅
        

9️⃣ Click **OK**

![image](https://i0.wp.com/techdirectarchive.com/wp-content/uploads/2022/07/Minimum-Password-length-set-to-14.jpg?resize=417%2C515&ssl=1)


![image](https://i0.wp.com/techdirectarchive.com/wp-content/uploads/2022/07/Minimum-Password-length-changed-to-14-1.jpg?resize=505%2C251&ssl=1)

---

## 🚀 Phase 5: Apply the Policy Immediately

1. Close the Group Policy Editor
    
2. Open **Command Prompt** as Administrator
    
3. Run:
    

```bash
gpupdate /force
```

4. Follows the PowerShell command:
    
    ```
		Get-ADDefaultDomainPassword Policy
    ```
    
	![image](https://i0.wp.com/techdirectarchive.com/wp-content/uploads/2022/07/Access-minimum-password-length-with-PowerShell.jpg?resize=650%2C359&ssl=1)
	
---

## 🧠 Key Takeaways (READ THIS)

- ✅ Password Policies are **Account Policies**
    
- ❌ They **do NOT work** when linked to an OU for domain users
    
- ✅ They **MUST** be configured in a GPO linked to the **Domain Root**
    
- 🔒 OU-linked Account Policies affect **local accounts only**
    

---
