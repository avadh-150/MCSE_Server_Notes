## 2️⃣ Domain Naming Master 🌍

**What it does**

- Controls **adding/removing domains** in the forest

- forest-wide (FSMO) role responsible for **managing the addition or removal of domains** and application partitions, ensuring unique namespace across the Active Directory forest

- It ensures **NO Duplication of domain names** across the forest by managing the Partitions container.
    
- Required for:
    
    - Creating new domains
        
    - Removing existing domains
        

**Failure impact**

- ❌ Cannot add/remove domains
    
- ✅ Existing domains work fine
    

**Hard reality**

> Small org with one domain? This role sleeps all day 😴  
> Big forest? It matters.

---
### 1. Connect to the Target Domain Controller

- To transfer the **Domain Naming Master** FSMO role to an **Additional Domain Controller (ADC)**  follow these steps:

- Open **Active Directory Domains and Trusts** from the Tools menu in Server Manager.

![image](https://miloserdov.org/wp-content/uploads/2021/10/server-manager-mmc-active-directory.png)

- Right-click the top-level node, **Active Directory Domains and Trusts [DC.forward.in]**, and select **Change Active Directory Domain Controller...**.
    
- In the list of available controllers, select your target ADC (e.g., **ADC.forward.in**) and click **OK**.
    

### 2. Access the Operations Master Menu

Once connected to the ADC, you can initiate the transfer.

- Right-click the top-level node **Active Directory Domains and Trusts [ADC.forward.in]** again.
    
- Select **Operations Master...** from the context menu.

![image](https://www.dtonias.com/wp-content/uploads/2018/01/transfer-fsmo-roles-dc-04.png)

### 3. Perform the Role Transfer

The "Operations Master" dialog box will appear, showing the current role holder and the target machine.

  <img width="587" height="619" alt="image" src="https://github.com/user-attachments/assets/077e5500-92b5-4c89-a308-361c03255c5a" />


- Verify that the target machine (ADC.forward.in) is listed in the bottom field as the recipient.
	
- Click the **Change** button.

	<img width="303" height="247" alt="image" src="https://github.com/user-attachments/assets/4f3c9871-e3b0-4544-a797-bc7cc056b2c2" />
	<img width="303" height="247" alt="image" src="https://github.com/user-attachments/assets/5d8b2ccf-8c33-4406-9246-9b978f2a4b98" />
	<img width="303" height="247" alt="image" src="https://github.com/user-attachments/assets/21862052-8b12-44fa-b7b5-86b2457b3afc" />

- Confirm the transfer by clicking **Yes** when the confirmation dialog appears.
    
- Once completed, a success message will confirm: "The operations master role was successfully transferred".
    

### 4. Verify the Transfer via Command Line

To ensure all roles are correctly assigned, you can use the command prompt.

- Open the Command Prompt and type the following command:
    
    `netdom query fsmo`.

  ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/FSMO-8-Domain%20name%20master.png?raw=true)
    
- The output should list **ADC.forward.in** (or your specific ADC name) as the current **Domain naming master**.
    

Would you like me to walk you through transferring the other four FSMO roles (Schema, RID, PDC, and Infrastructure) as well?
