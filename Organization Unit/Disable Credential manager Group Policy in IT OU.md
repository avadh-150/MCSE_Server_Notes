
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

   ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/CM%20Block%20in%20Custom/CMC-1-Credential%20Manager%20BLock.png?raw=true)

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
