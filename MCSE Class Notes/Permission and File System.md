### Permission

Permissions define the type of access granted to a user, group, or computer to access resources

Permissions can be applied to resources such as files, folders, and printers

### File System

- NTFS – Security Features – 1993
    
- FAT – Does not have security features
    

---

### Types of Permissions

- **List** – Only see file and folders
    
- **Read** – Can see & read content
    
- **Read & Execute** – Can read content and execute programs
    
- **Modify** – Can write on existing file and create new file
    
- **Full Control** – Everything
    

Reference:  
[https://netwrix.com/en/resources/blog/ntfs-permissions-tools/](https://netwrix.com/en/resources/blog/ntfs-permissions-tools/)

---

## Types of Permission (NTFS)

✓ Inherited Permission – Permission obtained from parent  
✓ Explicit Permission – Permission given by admin

✓ If a user has Read access in one group and Modify access in another group, final permission is Modify

✓ Access-based Enumeration (ABE) – Hides files and folders from users who do not have permission

---

## Share Permission vs NTFS Permission

When Share and NTFS permissions are used together, **the most restrictive permission wins**

Example:

- Share = Read, NTFS = Full Control → Result = Read
    
- Share = Full Control, NTFS = Read → Result = Read
    

---

## Best Practice for NTFS Permissions

✓ Assign permissions to groups instead of users  
✓ Simplifies management when roles change  
✓ Enforce principle of least privilege

Grant **Administrators** group Full Control  
Grant **System** group Full Control

---

## File Server Resource Manager (FSRM)

- File screening to block / allow file types
    
- Quota to apply quota to folders
    

---

## Shadow Copy

✓ Shadow Copies is a technology included in Microsoft Windows

- Allows manual and automatic backup of volumes
    
- Cannot exclude any file — applies to entire volume
    
- Default 64 shadow copies (can be increased to 512)
    

Example:  
If 65th shadow copy is created, the oldest one is deleted

✓ Shadow copies can be stored on another drive

---
