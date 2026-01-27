

# Plan of Credential Manager Block Custom Policy
---
### **Clear & Easy-to-Understand Version**

I have **one Domain Controller (DC)**.  
Two client computers — **PC1** and **PC2** — are joined to this domain.

I want to configure **Group Policy for Credential Manager** with the following behavior:

---

### 🔒 **Policy Scenario 1**

- **Block Credential Manager on PC1**
    
- **Allow Credential Manager on all other domain computers**, including **PC2**
    

👉 Meaning:  
PC1 **cannot** store or use saved credentials,  
but PC2 and any other PCs **can**.

---

### 🔄 **Policy Scenario 2 (Reverse Policy)**

- **Block Credential Manager on PC2**
    
- **Allow Credential Manager only on PC1**
    

👉 Meaning:  
PC2 **cannot** store or use saved credentials,  
but PC1 **is allowed** to use Credential Manager.

---
My words✅🔥
"
- i have DC  
- PC1 and PC2  is connected to Dc
- in DC i wanna to make the Group policy for Credential manager to block pc1 and 
	- allow to any pc like PC2 and also create it revers like CM block PC2 any other PC but it allow to access in PC1 only .
"
---
# 🎯 GOAL 1 of Policy 

##### Here the link of GOAL 1 Policy [Like Here](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/Group%20Policy%20on%20Domain%20Controller/Credential%20Manager%20Custom%20Block%20GP/2-Policy%20Scenario%201%20(allow%20all%2C%20block%20only%20PC1).md) 
