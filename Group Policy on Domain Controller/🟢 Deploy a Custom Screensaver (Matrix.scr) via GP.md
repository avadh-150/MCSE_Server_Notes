
---

# 🟢 Deploy a Custom Screensaver (Matrix.scr) via GPO — **Correct & Understandable Way**

⚠️ **Hard truth upfront (don’t skip):**

- Screensaver GPOs work under **USER Configuration**, not Computer ❗
    
- GPO **does NOT copy** the `.scr` file automatically ❗
    
- If the `.scr` file does not exist on the client → **policy fails silently** ❌
    
- Using `C:\software` works **only if that folder exists on every PC**

    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/1-softward-$%20folder.png?raw=true)

---

## 🔹 PHASE 1: Prepare the Screensaver File (MOST IMPORTANT)

🎯 **Goal:** Make sure every client has access to `matrix.scr`

### Option A (Best Practice – Recommended) ✅

1. Copy `matrix.scr` to:
    
    ```
    \\DC\Software$\matrix.scr
    ```
    
2. Ensure:
    
    - **Domain Users** → Read
        
    - **Domain Computers** → Read
        

👉 This avoids missing-file issues 💯

---

### Option B (What the video does – Risky but works) ⚠️

1. Place the file at:
    
    ```
    C:\software\matrix.scr
    ```
    
2. **You must manually copy this folder to EVERY client PC**
    
    - GPO will NOT do this for you ❌
        

If even one PC doesn’t have it → screensaver won’t load 😤

---

## 🔹 PHASE 2: Create and Link the GPO

🎯 **Goal:** Apply the policy to users

1. Open:
    
    ```
    gpmc.msc
    ```
    
1. Right-click the **[iforward.in]**  
    
2. Select:
    
    ```
    Create a GPO in this domain, and Link it here
    ```
    
3. Name it:
    
    ```
    Matrix_Screensaver_Deployment_Policy
    ```
    
    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/2-GPO.png?raw=true)

---

## 🔹 PHASE 3: Navigate to Correct Policy Location

📍 **Exact path (this matters):**

```
User Configuration
→ Policies
→ Administrative Templates
→ Control Panel
→ Personalization
```

   ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/3-location.png?raw=true)

If you configure this under **Computer Configuration**, it will NOT work 🚫

---

## 🔹 PHASE 4: Configure Policies (EXACT SETTINGS)

### ✅ 1. Enable Screen Saver

- Policy: **Enable screen saver**
    
- Set to: **Enabled**
    
- Click **OK**
    
   ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/4-enbled%20.png?raw=true)

📌 Without this, nothing else matters ❌

---

### ✅ 2. Force Specific Screen Saver (CORE SETTING)

- Policy: **Force specific screen saver**
    
- Set to: **Enabled**
    
- Path:
     
  (better):
    
    ```
    \\DC\Software$\matrix.scr
    ```
    
- Click **OK**

    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/5-specific%20saver%20load.png?raw=true)

⚠️ Path must be **identical on every client**

---

### ✅ 3. Password Protect Screen Saver

- Policy: **Password protect the screen saver**
    
- Set to: **Enabled**
    
- Click **OK**
    

🔐 This forces login after screensaver exits

---

### ✅ 4. Screen Saver Timeout

- Policy: **Screen saver timeout**
    
- Set to: **Enabled**
    
- Value:
    
    - `900` → 15 minutes (real-world)
        
    - `15` → testing only
        
    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/6-timeout.png?raw=true)

⏱️ Value is in **seconds**, not minutes (people screw this up a lot)

---

## 🔹 PHASE 5: Apply & Test on Client

On the target PC (logged in as domain user):

```cmd
gpupdate /force
```

Then either:

- Wait for timeout ⏳      - `15` → Seconds

    OR
    
- Press `Win + L` (lock screen) 🔒

    ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Custom%20Screen_Saver%20GP/8.png?raw=true)
    
👉 After inactivity, **Matrix screensaver should appear** 🟩💻

---

