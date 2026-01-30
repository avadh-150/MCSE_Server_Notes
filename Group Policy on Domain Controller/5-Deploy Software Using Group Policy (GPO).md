
# 🚀 Deploy Notepad++ Using Group Policy (GPO) — **Simple & Correct Way**

⚠️ **Important truth first**  
GPO software deployment:

- ✅ Works **ONLY with .MSI files**
    
- ✅ Installs during **startup (Computer Configuration)**
    
- ❌ Will NOT work from a local path like `C:\`
    
- ❌ Will NOT install instantly after `gpupdate` (restart is mandatory)

---

## 🔹 STEP 1: Prepare the Software Share (MOST COMMON FAILURE POINT)

🎯 **Goal:** Make the installer accessible to all domain computers.

1. Copy `npp.msi` to:
    
    ```
    C:\Software
    ```
    
2. Right-click **Software** folder → **Properties**

	![image](https://activedirectorypro.com/wp-content/uploads/2022/01/gpo-deploy-software-1.webp)

3. Go to **Sharing** tab → **Advanced Sharing**
    
    - ✅ Check **Share this folder**
        
    - Share name: `Software$`
    
4. Click **Permissions**
    
    - Add **Everyone**
        
    - Allow **Full CONTROL**

	![image]()

5. Final UNC path must look like:
    
    ```
    \\DC\Software\npp.msi
    ```
    
---

## 🔹 STEP 2: Create and Link the GPO

🎯 **Goal:** Tell AD _which computers_ should get Notepad++

1. Open **Group Policy Management**
    
    ```
    gpmc.msc
    ```
    
2. Navigate to:
    
    ```
    Domain → iforward.in
    ```
    
3. Right-click the OU →  
    **Create a GPO in this domain and Link it here**
    
4. Name it:
    
    ```
    Notepad++ Deployment Policy
    ```
    

---

## 🔹 STEP 3: Add the Software Package (THIS IS WHERE PEOPLE SCREW UP)

🎯 **Goal:** Assign Notepad++ to machines

1. Right-click the `Notepad++ Deployment Policy` GPO→ **Edit**
    
2. Go to:
    
    ```
    Computer Configuration
    → Policies
    → Software Settings
    → Software Installation
    ```
    
3. Right-click → **New → Package**
    
4. **Manually type the UNC path**:
    
    ```
    \\DC\Software\npp.msi
    ```
    
    ❌ DO NOT browse using C:\  
    ❌ DO NOT use mapped drives
    
5. When prompted:
    
    - Select **Published**
        
    - Click **OK**

| Mode           | Works With                         | Behavior                                  |
| -------------- | ---------------------------------- | ----------------------------------------- |
| **Published**  | User Configuration only            | User installs manually from Control Panel |
| **Assigned**   | Computer or User                   | Auto-installs                             |
| **Your setup** | Computer Configuration + Published | ❌ DOES NOTHING                            |
 6. Right-click **Notepad++**
    
7. Click **Properties**

✅ This means:  
👉 Software installs automatically at next boot

---


## 🔹 STEP 4: Verify Deployment Options (Optional but Correct)

Still in **Deployment tab**:

✔️ Keep checked:

- ✅ Install this application at logon
    

❌ Optional:

- ⛔ Uninstall when falls out of scope (only if you want auto-removal)
    

UI Option:

- **Maximum** → shows installer progress
    
- **Basic** → silent install
    

Pick **Maximum** for learning/demo 👨‍💻

---

## 🔹 STEP 5: Apply Policy on Client Machine

🎯 **Goal:** Force the client to pull the policy

On **PC1** (Run as Administrator):

```cmd
gpupdate /force
```

You’ll see:

> Software installation requires a restart

✔️ Type **Y**  
 
✔️ Restart the PC

💡 **Truth bomb:**  
Software installs **ONLY during startup**, not while logged in 😐

---

## 🔹 STEP 6: Confirm Installation

🎯 **Goal:** Verify success

After reboot:

- You’ll see:
    
    ```
    Installing managed software Notepad++
    ```
    
- Log in
    
- Search **Notepad++** in Start Menu
    

✅ If it’s there → deployment succeeded 🎉  
❌ If not → check Event Viewer → GroupPolicy logs

---
