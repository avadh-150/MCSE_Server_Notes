## WHAT `dsa.msc` IS (GET THIS STRAIGHT)

`dsa.msc` = **Active Directory Users and Computers** snap-in.  
It **only works on a Domain Controller** or a machine with RSAT installed.

If you run it on a non-DC without RSAT → it won’t open. That’s expected.

---

## STEP 1: OPEN `dsa.msc` (CORRECT WAY)

On **Windows Server 2022 (DC)**:

1. Press **Win + R**
    
2. Type:
    
    ```
    dsa.msc
    ```
    
3. Press **Enter**
    

If this fails → AD DS is not installed or the server is not a DC.

**or**

1. Open **Server Manager**
    
2. Go to **Tools → Active Directory Users and Computers**

---

## STEP 2: CREATE A DOMAIN USER (USING `dsa.msc`)

1. In **Active Directory Users and Computers**
    
2. Expand:
    
    ```
    Domain → lab.local (example)
    ```
    
3. Right-click **Users** (or your custom OU)
    
4. Click **New → User**
<img width="451" height="385" alt="image" src="https://github.com/user-attachments/assets/3b11a976-44c2-4696-a62f-5e64a8151c51" />

Fill properly:

- First name: `Test`
    
- User logon name: `testuser`
    

Click **Next**

Password screen:

- Set password
    
- ❌ Uncheck _User must change password_
    
- ✅ Check _Password never expires_ (lab only)
    

Finish.

User is now a **DOMAIN USER**, not local. Important distinction.

**Properties like :**






You’re inside **User → Properties** in **`dsa.msc`**. This window controls **how the user exists and behaves in the domain**. Misconfigure this and login breaks. Period.  
I’ll go **tab by tab**, only what actually matters.

---

## **1. General**

- **What it is:** Identity info (name, description, email)
    
- **Used for:** Address book, admin clarity
    
- **Does NOT affect login**
    
- **Reality:** Safe to edit, low risk

  <img width="414" height="498" alt="image" src="https://github.com/user-attachments/assets/b21befd6-8911-4673-9bff-574a4a94e3cb" />
  
---

## **2. Address**

- Purely organizational
    
- Zero impact on authentication or security
    
- Useful only in real corporate environments
  
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/b1e78076-2867-48ec-9671-426257bcf8dd" />

---

## **3. Account** ⚠️ (MOST IMPORTANT TAB)

This is the tab in your screenshot. This is where people screw up.

### **User logon name**

- `Radadiya@avadh.in`
    
- Used for **UPN login**
    
- Must match domain suffix
    

### **User logon name (pre-Windows 2000)**

- `AVADH\Radadiya`
    
- Used by legacy systems
    
- Still important internally
    

### **Logon Hours…**

- Restricts **when** the user can log in
    
- If blocked → login fails even with correct password
    
- Lab users: leave unrestricted
    

### **Log On To…**

- Restricts **which PCs** user can log into
    
- If you restrict and forget the PC name → instant lockout
    
- Default = all computers (correct for labs)
    
![Image](https://activedirectorypro.com/wp-content/uploads/2023/02/ad-user-logon-hours-1.webp?utm_source=chatgpt.com)
### **Account options (read carefully)**

✔ **User must change password at next logon**

- Good for real users
    
- Bad for labs (causes confusion)
    

✔ **Password never expires**

- Labs: ✅ yes
    
- Production: ❌ no
    

❌ **Store password using reversible encryption**

- Basically plaintext
    
- Only for ancient apps
    
- Using this = security failure

### **Account expires**

- Auto-disable user after date
    
- Common exam trick
    
- If expired → login denied, no warning
    

---

## **4. Profile**

Controls **what environment loads after login**

- **Profile path** → Roaming profile
    
- **Logon script** → `.bat` or `.ps1`
    
- **Home folder** → Network drive mapping
    

If you don’t configure these, nothing breaks.

<img width="428" height="340" alt="image" src="https://github.com/user-attachments/assets/9075dd52-d780-4373-964c-cd957b6673c0" />

---

## **5. Member Of** ⚠️ (PRIVILEGE CONTROL)

- Shows **groups**
    
- Groups = permissions
    
- Want admin? Add to:
    
    - ❌ Domain Admins (dangerous)
        
    - ✅ Custom admin group (best practice)
        

Hard truth: **Groups matter more than users** in AD.

<img width="432" height="300" alt="image" src="https://github.com/user-attachments/assets/d09d6134-bb93-494e-8d87-b8afdc59981e" />

---

## **8. Sessions**

- Controls session timeout
    
- RDP-specific
    
- Optional
    

---

## **9. Remote Desktop Services Profile**

- RDS-specific profile path
    
- Ignore unless using Remote Desktop Services
    
---
![Image](https://www.windows-active-directory.com/wp-content/uploads/2021/06/attribute-editor.png?utm_source=chatgpt.com)
