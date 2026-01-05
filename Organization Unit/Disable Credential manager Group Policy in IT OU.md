To disable the **Credential Manager** (the ability to store network passwords) on a specific PC via Group Policy, you need to use the Group Policy Management Console (GPMC) on your Domain Controller.1

---
### Phase 1: Configure the Group Policy Object (GPO)

1. Open **Group Policy Management** (`gpmc.msc`) on your Domain Controller.
    
2. Right-click **IT OU** and select **Create a GPO in this domain, and Link it here...**.
    
3. Name it 

	```
	Disable Credential Manager Policy
	```
    
4. Right-click **`Disable Credential Manager Policy`** and select **Edit**.
    
5. In the Group Policy Management Editor, navigate to:
```
	Computer Configuration
    > Windows Settings
    > Security Settings
    > System Services
```
### Proper Steps to Configure the Service:

  <img width="709" height="366" alt="image" src="https://github.com/user-attachments/assets/10f9fc50-eae6-4606-b1e5-7f5f01e25a28" />

6. Scroll down the list of services in the right-hand pane until you find **Credential Manager**.
    
7. Double-click it.
    
8. Check the box for **Define this policy setting**.
    
9. Select **Disabled** as the service startup mode.
    
10. Click **OK**.    

---

### Phase 3: Apply the Policy to PC1

1. Go to **PC1**.
    
2. Open the Command Prompt as Administrator.
    
3. Run the following command to force the update:
    ```
    gpupdate /force
    ```
    
4. **Restart the computer.** A restart is required for this specific security policy to take full effect.
    
---
