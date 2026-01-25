
## 3️⃣ RID Master 🆔

![image](https://media.licdn.com/dms/image/v2/D4E22AQG-0Id1G4EMdA/feedshare-shrink_800/B4EZsm73xZHMAg-/0/1765884793116?e=1770854400&v=beta&t=jSazgQyVUbDkUj4oYvRZrc2UaCuN5ajhJjxELIqSF4Y)


**What it does**

- The **RID Master (Relative Identifier Master)** is a **domain-level FSMO role** responsible for allocating **unique pools of Relative Identifiers** (RIDs) to other (DCs) in the domain.

- ensuring every security principal (user, group, computer) it **gets** OR **attaches** a **unique Security Identifier (SID)** when created. 

	-  A domain SID that's the same for all SIDs created in a domain.
	-  A relative ID (RID) that's unique for each security principal SID created in a domain.

- It manages the global pool of available RIDs, granting blocks to DCs as needed, **preventing SID conflicts**, and handling object moves between domains
    
- RID = part of SID (Security Identifier)
    
**Why it matters**

- Every user, group, computer = needs unique SID
    
**Failure impact**

- ❌ Eventually cannot create users/groups/computers
    
- ⚠️ Existing objects still work
    

**Reality check**

> RID Master down long enough = AD admin nightmare 🔥

---

### Part 1: Transferring the Domain Naming Master Role

To transfer the **Domain Naming Master** and **RID Master** FSMO roles to an **Additional Domain Controller (ADC)** . follow this step-by-step :

OPEN .... **Active Directory Domains and Trusts** console.

1. **Open the Console:** In Server Manager, click **Tools** and select **Active Directory Domains and Trusts**.

![Image](https://camo.githubusercontent.com/b86c2de8336deed9db4627ce9522d4dd97248c59debf300670b9e5e4238b376e/68747470733a2f2f6d696c6f736572646f762e6f72672f77702d636f6e74656e742f75706c6f6164732f323032312f31302f7365727665722d6d616e616765722d6d6d632d6163746976652d6469726563746f72792e706e67)
	
2. **Connect to the ADC:**
    
    - Right-click the top-level node (e.g., **Active Directory Domains and Trusts [DC.forward.in]**) and select **Change Active Directory Domain Controller...**.
        
    - Select your target ADC (e.g., **ADC.forward.in**) from the list and click **OK**.
        
3. **Initiate the Transfer:**
    
    - Right-click the top-level node (now showing as connected to the ADC) and select **Operations Master...**.
        
    - In the dialog box, ensure the ADC is listed as the target and click **Change**.
        
    - Confirm the transfer by clicking **Yes**.
        
    - A success message will confirm: "The operations master role was successfully transferred".
        

---
### Part 2: Verification

After performing the transfers, you can verify the current role holders using the Command Prompt.

1. **Open Command Prompt** and type: `netdom query fsmo`.
    
2. **Check the Output:** The list will display which server holds each of the five roles.
    
    - The **Domain naming master** should now be **ADC.forward.in**.
        
    - The **RID pool manager** (RID Master) should now be **ADC.forward.in**.

	
			C:\Users> netdom query FSMO
    
			Schema master      		ADC.iforward.in
			Domain naming master	ADC.iforward.in
			PDC						DC.iforward.in
			RID pool manager		ADC.iforward.in
			Infrastructure master	DC.iforward.in

    		The command completed successfully.
      
			C:\Users>  
