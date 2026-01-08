# Disable PowerShell Policy

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/pwsh_ou.png?raw=true)

---

## Phase 1: Configure the Block Policy


1. **Open Group Policy Management:** On your Domain Controller (or server)

2. Browse to the OU like **IT OU** right click and select “Create a GPO in this domain it Open's the **Group Policy Management Editor**. 
    
3. **Navigate to System Settings:** Go to `User Configuration` > `Policies` > `Administrative Templates` > `System`.
    
4. **Access App Restrictions:** Locate and double-click the setting **"Don't run specified Windows applications."**

	![image](https://www.top-password.com/blog/wp-content/uploads/2014/06/not-run-specified-windows-app.png)    

5. **Enable the Policy:** Select the **Enabled** radio button.
    
6. **List Blocked Apps:** Click the **Show...** button next to "List of disallowed applications."

	![image](https://www.top-password.com/blog/wp-content/uploads/2014/06/prevent-specific-windows-apps.png)

7. **Enter Executables:** In the "Value" column, enter the names of the executable files you want to block:
    
    - `powershell.exe`
        
    - `powershell_ise.exe`
        
    - `pwsh.exe` (if using PowerShell 7)
        
    - `cmd.exe`
        
8. **Save Changes:** Click **OK** on the list window, then **Apply** and **OK** on the main policy window.

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Powershell_block_all_app.png?raw=true)

---

## Phase 2: Force Policy Update

To ensure the changes take effect immediately without waiting for the background refresh:

1. Open a command interface (like PowerShell as an administrator before the policy hits).
    
2. Type the following command and press Enter:
    
    gpupdate /force
    
3. Wait for the confirmation message stating that the computer and user policies have updated successfully.
    

---

## Phase 3: Verification (Testing the Blocks)

### Testing as a Standard User

1. **Sign out** of the server and **Sign in** as a standard user (e.g., `User1`).
    
2. **Attempt to open PowerShell:** Search for "PowerShell" in the Start menu and click it. You should see a restriction message:
    
    > "This app has been blocked by your system administrator."
    
3. **Attempt to open Command Prompt:** Open `cmd`. You will likely see a message stating:
    
    > "The command prompt has been disabled by your administrator."
    

### Testing as an Administrator

1. **Sign out** and **Sign in** with an **Administrator account**.
    
2. **Verify access:** Attempt to open PowerShell. Because Group Policy Objects (GPOs) are often linked to specific Organizational Units (OUs), the Administrator may still have access if they are not within the scope of that specific policy, allowing them to manage the system while users remain restricted.
    