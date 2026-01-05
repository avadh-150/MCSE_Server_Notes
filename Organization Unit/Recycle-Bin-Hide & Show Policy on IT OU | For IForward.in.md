# GOAL (Crystal Clear)

1. **Recycle Bin = HIDDEN** for **entire domain** → `iforward.in`
    
2. **Recycle Bin = SHOWN** only for users in **IT OU**
   
---
### Step 1: Create Domain-Level GPO

On DC:

```
gpmc.msc
```

1. Expand domain **iforward.in**
    
2. Right-click **iforward.in**
    
3. Click **Create a GPO in this domain, and Link it here**
    
4. Name it:
    
    ```
    Domain - Hide Recycle Bin
    ```
    
## Part 2: Configuring the Group Policy

1. **Open Group Policy Management:** On your Domain Controller, open the **Group Policy Management** console.
    
2. **Create/Edit a GPO:** Right-click on your desired Organizational Unit (OU) like **IT OU** or existing policy (it's named `Recycle-Bin-Hide-Policy`) and select **Edit**.
    
3. **Navigate to the Setting:** In the Group Policy Management Editor, follow this path:

```
	User Configuration
		└─ Administrative Templates
			└─ Desktop
			    └─ Remove Recycle Bin icon from desktop
```

   <img width="900" height="673" alt="image" src="https://github.com/user-attachments/assets/2740cf10-b353-49c4-88d6-8ab66281269c" />

1. **Enable the Policy:** * In the right-hand pane, find and double-click **Remove Recycle Bin icon from desktop**.
    
    - Select the **Enabled** radio button.
        
    - Click **Apply** and then **OK**.
        
	<img width="699" height="641" alt="image" src="https://github.com/user-attachments/assets/cc5d81e3-2d41-420e-8565-b693431db134" />

---

## Part 3: Applying and Verifying the Policy

Once the policy is set, you need to ensure the client machine receives the update.

1. **Update Policy:** On the client machine, open the Command Prompt and type

2. `gpupdate /force` 
    
3. **Sign In:** Sign in with the user account that is subject to the GPO (e.g., `User1`).

   <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/6685abed-c9ca-4301-b6e3-840a64ab7fb6" />

5. **Check Desktop:** Notice that the Recycle Bin icon is now **hidden** from the desktop.
    
   <img width="314" height="310" alt="image" src="https://github.com/user-attachments/assets/d82facb8-89b7-4213-befb-6b62e6496668" />

---

## Part 4: Accessing the Recycle Bin when Hidden

If a user needs to access the Recycle Bin while the icon is hidden, the video demonstrates a manual workaround:

1. **Open File Explorer:** Press `Win + E`.
    
2. **Use the Address Bar:** Click on the small arrow in the address bar or type directly into it.
    
3. **Search/Type:** The video shows searching for the path or using the command:
    
    - `shell:RecycleBinFolder`
        
4. **Open:** This will open the Recycle Bin folder even if the icon is missing from the desktop.
    

---

