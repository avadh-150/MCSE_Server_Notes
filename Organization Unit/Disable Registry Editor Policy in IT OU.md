To disable the Registry Editor (**regedit**) specifically for the **IT OU** via your Domain Controller, follow these steps.

### Phase 1: Create and Link the GPO

1. On your Domain Controller, open **Group Policy Management** (`gpmc.msc`).
    
2. Expand your Forest and Domain to find the **IT** OU.
    
3. Right-click the **IT OU** and select **Create a GPO in this domain, and Link it here...**.
    
4. Name the GPO
		```
		Disable Registry Editor - IT
		```
  5. and click **OK**.  

---

### Phase 2: Configure the Registry Restriction

1. Right-click your new GPO (`Disable Registry Editor - IT`) and select **Edit**.
    
2. In the Group Policy Management Editor, navigate to:
    
    > **User Configuration** > **Policies** > **Administrative Templates** > **System**
    
3. In the right-hand pane, find and double-click the policy:
    
    "Prevent access to registry editing tools"

   <img width="640" height="450" alt="image" src="https://github.com/user-attachments/assets/f1817f85-efcb-4901-afc9-802032fad8d7" />

4. Select **Enabled**.
    
5. Under the "Options" box on the left, you will see: **Disable regedit from running silently?**
    
    - Set this to **Yes**.
        
    - _Why?_ This prevents users from bypasssing the block by using `.reg` files or command-line scripts to change the registry in the background.
        
6. Click **Apply** and **OK**.
    
	<img width="640" height="594" alt="image" src="https://github.com/user-attachments/assets/52f2226c-ae39-40da-af6c-46a5f7356d9d" />

---

### Phase 3: Force the Update on PC1

1. Log in to **PC1** using an account that belongs to the **IT OU**.
    
2. Open the Command Prompt and run:
        
    ```
    gpupdate /force
    ```
    
3. Try to open the Registry Editor by typing `regedit` in the Start menu. You should see a message stating: _"Registry editing has been disabled by your administrator."_

   <img width="640" height="214" alt="image" src="https://github.com/user-attachments/assets/62d422ce-e5b0-4538-a3a9-011cb7e239d9" />


---
