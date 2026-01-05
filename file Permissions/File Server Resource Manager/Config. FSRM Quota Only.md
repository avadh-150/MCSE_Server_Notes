## How FSRM is installed (quick)

1. **Server Manager**
2. Add Roles and Features
3. **File and Storage Services**
4. **File Server Resource Manager**

![Image](https://redmondmag.com/articles/2014/09/25/~/media/ECG/redmondmag/Images/2014/09/FSRM_Fig1.ashx)

5. Install → Tools → FSRM
    
# 0️⃣ Ground rules (read this or stop)

- **Do NOT apply this on C:** or app/data volumes
    
- **This is for user file shares only**
    
- **Quota = Hard OR Soft**
    
- **Screening = Active OR Passive**
    
- **Admins are exempt**(legally free)
# 1️⃣ Folder structure (clean and predictable)

Example:

```
C:\My_Quota 
	├── Some File 
	├── Some Folder
	└── etc.. 
```
You apply FSRM at **`C\My_Quota`**, not on random subfolders.
# 2️⃣ Create an enterprise-grade QUOTA TEMPLATE

**Why template first?**  
Because enterprise admins don’t configure quotas folder-by-folder like amateurs.
### Steps

1. Open **FSRM**
    
2. Go to **Quota Management → Quota Templates**
    
3. **Create Quota Template**
   
   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/f33b96a6-62cc-463f-8638-0e4b41823b78" />
	<img width="388" height="486" alt="image" src="https://github.com/user-attachments/assets/1c142006-a898-4954-8bbb-46757c22b85b" />

### Notifications (mandatory)

Configure **ALL** of these:(use Event Viewer tool)

- **75%** → Warning email to user + IT
    
- **90%** → Critical warning
    
- **100%** → Final alert (writes blocked)
# 3️⃣ Apply quota to `My_Quota`


1. **Quota Management → Quotas**
    
2. **Create Quota**
 
<img width="500" height="412" alt="image" src="https://github.com/user-attachments/assets/f0599a6f-03c2-48f3-8fe7-843c3f84a86a" />

3. Path:
    
    `C:\My_Quota`
    
4. Choose **Create Quota on Path**
    
5. Select template: `Custom Templete, have you Created.`

	<img width="321" height="397" alt="image" src="https://github.com/user-attachments/assets/029e1458-6f1d-43ac-bb7b-5a7896bf9aff" />
6. Then Click on `Create`:
	<img width="1041" height="238" alt="image" src="https://github.com/user-attachments/assets/999828dc-1ad5-4c0a-96df-a750d49ad0fd" />

✅ Now every subfolder inherits control  

# Result :

1. **Event Viewer**

Hard quota reached (100%)
Trigger:
User exceeds 95 %

Event Viewer result

Level: ⚠️ Warning

Event ID: **12325** OR 8215 / 8213 (varies by build)

Source: SRMSVC
   <img width="1500" height="613" alt="image" src="https://github.com/user-attachments/assets/8d2ffef5-b725-45eb-a24a-f85cdabaf812" />


IF you have facing any issue visite this line and again step by step Configure the Quota 
https://www.rootusers.com/configure-quotas-with-file-server-resource-manager-fsrm/ 

OR

* full Quota + Screening ...

https://www.manageengine.com/products/active-directory-audit/how-to/how-to-set-up-fsrm.html
