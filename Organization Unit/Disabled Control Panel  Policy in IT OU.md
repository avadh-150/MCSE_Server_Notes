
### Phase 1: Create and Configure the GPO

1. **Open Group Policy Management:** Launch the Group Policy Management console on your Domain Controller.
    
2. **Create a New GPO:** Right-click on **IT Organizational Unit (OU)**, select **Create a GPO in this domain, and Link it here...**, and name it (e.g., "Disable control panel policy").
    
3. **Edit the GPO:** Right-click the newly created GPO and select **Edit**.
    
4. **Navigate to Control Panel Settings:** In the Group Policy Management Editor, go to:
    
    - `User Configuration` > `Policies` > `Administrative Templates` > `Control Panel`.
        
5. **Enable the Restriction:** Double-click the setting **Prohibit access to Control Panel and PC settings**.
    
6. **Set to Enabled:** Select the **Enabled** radio button, then click **Apply** and **OK**.
    

### Phase 2: Force the Policy Update

1. **Open Command Interface:** Launch a command prompt or PowerShell window.
    
2. Run Update Command: Type the following command and press Enter to apply the changes immediately:
    
    gpupdate /force.
    
3. **Verify Success:** Ensure the message "User Policy update has completed successfully" appears.
    

### Phase 3: Verification

1. **Test Access:** Attempt to open the **Control Panel** or **Settings** from the Start menu or search bar.
    
2. **Confirm Restriction:** A "Restrictions" dialogue box should appear stating:
    
    > "This operation has been cancelled due to restrictions in effect on this computer. Please contact your system administrator.".
    

Would you like to know how to exclude certain administrative users from this restriction so they can still manage the system?