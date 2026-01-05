# 1️⃣ Create FILE SCREENING 
---
**Step 1: Open the Create File Screen window**

GO TO:-
```
FSRM →
    File Screening Management → 
                        File Screens → 
```

* **File Screen Templete :**  Create it First

    Templete name : **Add you "CUSTOM_NAME"**

    Choose Mode: **Active**

    File Groups:(select file group to block)
  
     **Choose name which you want to Block:**

<img width="1020" height="650" alt="image" src="https://github.com/user-attachments/assets/a655c3c0-b907-4db5-b0d9-9b2d777c87ca" />


Notification: **Event Viewer**

<img width="768" height="550" alt="image" src="https://github.com/user-attachments/assets/6c5ea211-3b9b-4eb4-9d07-34f5dbc7a169" />

---
 
**Step 2: Create File Screen**

GO TO

* File Screen 

* right-click File Screens, and then click Create File Screen…
  
<img width="1024" height="728" alt="image" src="https://github.com/user-attachments/assets/8d6c0e3b-e3e6-48b8-ab06-c9412a81d00d" />

* Set Path

* Click Browse

* Select:

`C:\My_Quota`

* Choose : **Choose name which you want to Block**

* Click OK

<img width="768" height="577" alt="image" src="https://github.com/user-attachments/assets/6e425d76-dca8-43fb-a182-1f4195691082" />

---
**CUSTOM**
    Extenssion Bolck

 ```
*.mp4
*.mkv
*.avi
*.mov
*.mp3
*.iso
*.zip
*.rar
```

   <img width="216" height="233" alt="image" src="https://github.com/user-attachments/assets/2214b2a6-cfb9-425a-be0c-59af3e904baf" />

**VIEW THW FILE SCREEN MANAGEMENT**

<img width="406" height="124" alt="image" src="https://github.com/user-attachments/assets/ea6d5192-003a-40e0-94db-25582504a643" />


**Result:**

- Files blocked instantly
    
- Event logged

<img width="768" height="574" alt="image" src="https://github.com/user-attachments/assets/b8abc855-2497-4338-9e8f-e8a719cfe33e" />

---

**Storage Reports (weekly, automated)**

Enable:

- **Largest files**
    
- **Files by type**
    
- **Quota usage**
    

Schedule: **Weekly**  
Export: Email PDF to IT

Admins who don’t review reports are blind.

---

# 4️⃣ Testing checklist (DO THIS)

From a normal user account:

- ✅ Create normal files
    
- ❌ Copy `.mp4` → should fail
    
- ❌ Copy `.exe` → should fail
    
- ❌ Exceed quota → write blocked
    
- ✅ Admin folder allows scripts

  ---
“I used hard quotas with Custom templates, active file screening to block media and executables, **Event Viewer** alerts at 85/95/100 percent, and admin exceptions. This prevented disk exhaustion and reduced malware risk.”

IF you have facing any issue visite this line and again step by step Configure the Quota : https://mizitechinfo.wordpress.com/2013/08/20/step-by-step-manage-file-server-using-fsrm-file-screening-in-windows-server-2012-r2/
