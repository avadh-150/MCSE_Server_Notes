## 🧠 Purpose
This guide explains how to create a new **Security Group** in **Active Directory Users and Computers (ADUC)** in Windows Server 2022.

---

## 🪜 Steps to Create a Group

### **Step 1: Open Active Directory Users and Computers**
- Press **Win + R**, type `dsa.msc`, and press **Enter**.

### **Step 2: Navigate to Domain and Users Folder**
- Expand your domain (e.g., `iforward.in`) → click **Users**.

### **Step 3: Create a New Group**
- Click the **“Create a new group in the current container”** button in the toolbar.

📸 *Create Group Button Screenshot:*  

![Create Group Button](../MCSE%20Class%20Notes/img/Create%20Grp%20icon.png)

---

### **Step 4: Enter Group Details**
- In the **New Object – Group** window:
  - **Group name:** IT Team  
  - **Group scope:** Global  
  - **Group type:** Security  
- Click **OK** to create the group.

📸 *New Group Window:*  
![New Group Window](../MCSE%20Class%20Notes/img/Create%20Grp%20Popup.png)


---

### **Optional Method (Right-Click Method)**
1. Inside the **Users** container, right-click in the blank area or on the **Users** folder.  
2. Choose **New → Group**.  
3. Enter the group details (same as above).  
4. Click **OK** to create it.

---

## 📝 Notes
- **Group Scope**
  - *Domain Local:* Used to assign permissions within the same domain.  
  - *Global:* Used for grouping users with similar roles.  
  - *Universal:* Used across domains.
- **Group Type**
  - *Security:* Assign permissions.  
  - *Distribution:* Used for email lists.

---

You have successfully created a new **Security Group** named `IT Team` inside `iforward.in/Users`

---
## 🧍  Add Users to the Group 

### **Step 1: Open the Created Group**
- In **Active Directory Users and Computers**, go to:  
  `iforward.in → Users`
- Locate and double-click the **IT Team** group to open its **Properties**.

📸 *Open IT Team Properties Screenshot:*  
![Open IT Team Group](../MCSE%20Class%20Notes/img/IT%20TEAM%20Properties.png)

---

### **Step 2: Go to the Members Tab**
- In the group’s properties window, click on the **“Members”** tab.

📸 *Example Screenshot:*  
![Members Tab](../MCSE%20Class%20Notes/img/IT%20Team%20Grp%20Members.png)

---

### **Step 3: Add Users to the Group**
1. Click **Add**.
2. In the **Select Users, Contacts, Computers, or Service Accounts** window, type:
   ```
   user1; user2
   ```
3. Click **Check Names** → both names should underline (verified).  
4. Click **OK** to add them to the group.

📸 *Example Screenshot:*  
![Add Users Window](../MCSE%20Class%20Notes/img/adding%20user%20in%20grp.png)

---
### **Step 4: Confirm Membership**
- You’ll now see `user1` and `user2` listed as **members** of the **IT Team** group.  
- Click **Apply → OK** to save the changes.

📸 *Example Screenshot:*  
![Add Users Window](../MCSE%20Class%20Notes/img/member%20verification.png)

---
## 📝 Notes
- Adding users to groups helps manage permissions efficiently.  
- Instead of assigning permissions to individual users, assign them to the **group**.  
- When a new user joins the same role, just add them to that group to inherit permissions.

---
