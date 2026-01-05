Based on the video provided, here are the step-by-step instructions for creating and properly deleting an **Organizational Unit (OU)** in Active Directory on Windows Server 2022.

---

## Part 1: How to Create an OU

1. Run `dsa.msc`  |OR|  Open **Active Directory Users and Computers**.
    
2. **Right-click** on the domain name or the container where you want to place the new OU.

    like : `iforward.in`
    
3. Navigate to **New** > **Organizational Unit**.

    <img width="763" height="532" alt="image" src="https://github.com/user-attachments/assets/3706bd91-86fb-423c-b0f0-0f901aff2906" />
    
4. In the "New Object – Organizational Unit" dialog box:
    
    - **Name:** Type the name for your OU (e.g., "IT" or "HR").

        <img width="449" height="380" alt="image" src="https://github.com/user-attachments/assets/b21f0019-a4f3-4afe-980b-9ec87e330cb0" />

    - **Protection:** Ensure the box **"Protect container from accidental deletion"** is checked (this is enabled by default to prevent mistakes).

4. Click **OK**. Your new OU will now appear in the list.

   <img width="766" height="534" alt="image" src="https://github.com/user-attachments/assets/f7debee6-45df-45a5-b344-cdeee0a4a8f4" />
    
---

## Part 2: How to Delete an OU

If you try to delete an OU immediately by right-clicking it and selecting **Delete**, you will likely receive an error message: _"You do not have sufficient privileges to delete it, or this object is protected from accidental deletion."_

To delete it, you must first disable that protection:

1. Click on the **View** menu at the top of the Active Directory window.

2. Select **Advanced Features**. (The screen will refresh and show more hidden containers).

   <img width="608" height="306" alt="image" src="https://github.com/user-attachments/assets/47fd9314-e96c-41ec-a241-8457851ae0af" />

3. **Right-click** the OU you want to delete and select **Properties**.

   <img width="761" height="567" alt="image" src="https://github.com/user-attachments/assets/a470dacc-b706-4cfe-a5f3-baf516718173" />
    
4. Click on the **Object** tab.

5. **Uncheck** the box that says **"Protect object from accidental deletion"**.

7. Click **Apply** and then **OK**.
    
   <img width="411" height="457" alt="image" src="https://github.com/user-attachments/assets/04a013a2-e43e-4b96-84d0-68a6ced5ea8e" />

   <img width="608" height="387" alt="image" src="https://github.com/user-attachments/assets/50665e78-870c-46b3-8d4a-70556bfbfcc4" />
    
8. Now, **right-click** the OU again, select **Delete**, and click **Yes** to confirm. The OU will now be successfully removed.
    
    <img width="608" height="387" alt="image" src="https://github.com/user-attachments/assets/f70436aa-3dd3-4670-ac6e-ef721371599e" />

    <img width="762" height="524" alt="image" src="https://github.com/user-attachments/assets/da36f580-128c-4324-bb75-fac2da38147b" />

---

### Pro-Tip

After deleting the OU, it is a good idea to go back to the **View** menu and uncheck **Advanced Features** to simplify your workspace and prevent accidental changes to system containers.

---

# The Correct Design

*  Best practice:
```
OU=IT
 ├─ OU=Users
 │   └─ User1
 └─ OU=Computers
     └─ PC1
```

 Then:

User GPOs → link to Users OU

Computer GPOs → link to Computers OU

---

### User Move in IT OU

   1.Go to Users container (or wherever User1 is)

   2.Right-click User1

   3.Click Move

   4.Select OU = IT

   5.Click OK

---

### PC1 Move in IT OU

   1.Go to Computers container

   2.Right-click PC1

   3.Click Move

   <img width="258" height="195" alt="image" src="https://github.com/user-attachments/assets/d277009e-8d18-4b4f-b4d9-834195b01a6e" />
    
   4.Select OU = IT

   5.Click OK
   
