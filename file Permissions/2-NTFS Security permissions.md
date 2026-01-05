# How to give **NTFS Security permissions** on a **Shared Folder**

⚠️ First hard truth (don’t skip this):

> **Share permissions ≠ NTFS permissions**  
> **Effective access = the MOST restrictive of the two**

**Best practice (non-negotiable):**

- Share permission → **Everyone : Full Control**
    
- NTFS permission → **Do the real security here**
---
## One-line summary (memorize this)

> **Share = open the door**  
> **NTFS = control what people can do inside**

---

## STEP 1: Create the folder (never use C:\ directly)

Example:

```
C:\data
```

❌ Do NOT share:

- `C:\`
    
- `C:\Windows`
    
- `C:\Users`
    

That’s rookie-level unsafe.

---

## STEP 2: Set NTFS permissions (THIS is the real security)

1. Right-click the folder
    
2. Click **Properties**
    
3. Go to **Security** tab
    
4. Click **Edit**
    

### Remove unnecessary users

- Remove:
    
    - Everyone (if present)
        
    - Individual users
        

### Add AD Group (correct way)

5. Click **Add**
    
6. Enter group name (example):
    
    ```
    IT Team
    ```
    
7. Click **Check Names** → OK
    

### Assign permission

- Select **Modify** (recommended for users)
    
- Click **Apply → OK**
    

✔ Users can:

- Read
    
- Save
    
- Modify
    
- Delete
    
- Rename
    

❌ Users cannot:

- Change ACL
    
- Take ownership
    

That’s exactly what you want.

---

## STEP 3: Advanced NTFS check (important but quick)

1. In **Security** tab → **Advanced**
   
     ![image](https://github.com/avadh-150/Server_notes/blob/main/MCSE%20Class%20Notes/img/security_tab%20advance%20option.png?raw=true)

    -  **Disable Inheritance**
      
      
      <img width="500" height="537" alt="image" src="https://github.com/user-attachments/assets/f8da775c-b8a5-46ef-be4a-7f8808b08ef9" />
      
      **Click on**
    - → Convert inherited permissions into explicit permissions on this object.

    **Remove the users only**
       - only keep `administrator` and `ststem`
   
   <img width="500" height="537" alt="image" src="https://github.com/user-attachments/assets/5eff42bc-e595-4a9f-b913-8b9099b9f02d" />

    **add It Teams Or Group Users**

   <img width="500" height="537" alt="image" src="https://github.com/user-attachments/assets/5bbb7ef9-5cf8-46f0-909e-5f229b42360d" />


3. Confirm:
    
    - Inheritance = **Enabled**
        
    - Administrators = **Full Control**
        
    - SYSTEM = **Full Control**
        

❌ Don’t break inheritance unless you know why  
❌ Don’t use **Deny**

---

## STEP 4: Share the folder (network access)

1. Right-click folder → **Properties**
    
2. Go to **Sharing**
    
3. Click **Advanced Sharing**
    
4. Check **Share this folder**
    
5. Click **Permissions**
    

### Set Share permissions (simple rule)

- Remove all
    
- Add **Everyone**
    
- Allow **Full Control**
    
- Click OK
    

👉 Yes, this is correct. Security is enforced by NTFS, not Share.

---

## STEP 5: Test effective access (this saves embarrassment)

1. Security tab → **Advanced**
    
2. Click **Effective Access**
    
3. Select a user
    
4. Click **View effective access**
    

This shows **real permissions**, not assumptions.

---

## Example: Correct enterprise setup

```
D:\data
 ├── bank record   
 ├── Finance  → Finance_Modify
 ├── cmd.exe
```   

Users go into groups.  
Groups get permissions.  
Never the other way around.

---
