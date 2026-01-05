

# Phase 3: Windows Server Backup install & configure.md

To install **Windows Server Backup** on Windows Server 2022, follow these step-by-step instructions based on the provided video:

### **Step 1: Open the Add Roles and Features Wizard**

- Open the **Server Manager** dashboard.
    
- Click on **Manage** in the top-right corner and select **Add Roles and Features**.
    
- On the **Before you begin** screen, review the prerequisites and click **Next**.
    

### **Step 2: Select Installation and Server**

- **Installation Type**: Select **Role-based or feature-based installation** and click **Next**.
    
- **Server Selection**: Ensure your local server is selected from the server pool and click **Next**.
    
- **Server Roles**: You do not need to add any roles for this task; simply click **Next** to proceed to the features section.
    

### **Step 3: Enable Windows Server Backup Feature**

- In the **Features** list, scroll down to find **Windows Server Backup**.

- Check the box next to **Windows Server Backup**.
    
- Click **Next**.
  
  <img width="786" height="560" alt="image" src="https://github.com/user-attachments/assets/1549b5ea-eaba-43b2-a2e2-dd064d9ddfea" />
    

### **Step 4: Confirm and Install**

- On the **Confirmation** screen, verify that "Windows Server Backup" is listed.

   <img width="786" height="560" alt="image" src="https://github.com/user-attachments/assets/66e615f9-1564-4c74-a5bc-903f69c8f1e9" />

- Click **Install**.
  
- Wait for the installation to complete. Once finished, click **Close**.

  <img width="786" height="560" alt="image" src="https://github.com/user-attachments/assets/8167e695-7a76-44bc-ba3a-ece8b3112b8d" />
    

### **Step 5: Verify the Installation**

---

## Part 1: Configuring a Backup Schedule

This process sets up an automatic, recurring backup of specific data.

1. **Open Windows Server Backup:** Navigate to **Tools** > **Windows Server Backup** in Server Manager.

    <img width="834" height="580" alt="image" src="https://github.com/user-attachments/assets/0b254954-bc0b-42f6-abe6-1f172c31bfca" />

2. **Start the Wizard:** In the right-hand **Actions** pane, click on **Backup Schedule...** and click **Next** on the Getting Started page.

    <img width="902" height="550" alt="image" src="https://github.com/user-attachments/assets/85923390-3a00-4487-8fe7-9967dbe9ace0" />

    <img width="664" height="311" alt="image" src="https://github.com/user-attachments/assets/cede9589-d8c4-4e0e-80b6-4509ddd141bc" />
   
3. **Select Backup Configuration:** Choose **Custom** (to select specific files or folders) and click **Next**.

   <img width="665" height="515" alt="image" src="https://github.com/user-attachments/assets/0c35fb54-54dc-4add-83bd-c8db52cc39b6" />

4. **Select Items for Backup:**
    
    - Click **Add Items**.
        
    - Expand the drive (e.g., Local Disk C:) and check the box for the specific folder you want to back up (in the video, the user selects the **"C data"** folder).
        
    - Click **OK**, then click **Next**.

      <img width="700" height="587" alt="image" src="https://github.com/user-attachments/assets/9cd9d0c4-20f7-4ef6-bdcc-9b2b132dee85" />

5. **Specify Backup Time:** Choose how often and at what time the backup should run (e.g., Once a day at 9:00 PM). Click **Next**.

   <img width="662" height="460" alt="image" src="https://github.com/user-attachments/assets/718bff98-7c37-472c-a312-e128e22241fc" />

6. **Select Destination Type:** Select **Back up to a hard disk that is dedicated for backups (recommended)**. Click **Next**.

   <img width="660" height="350" alt="image" src="https://github.com/user-attachments/assets/932eead1-ab7e-41f5-aee7-ea6576aa04e5" />

7. **Select Destination Disk:**
    
    - Click **Show All Available Disks...**.
        
    - Select your target backup disk (e.g., VMware Virtual Disk).
        
    - Click **OK**, then select the disk in the main list and click **Next**.

      <img width="648" height="497" alt="image" src="https://github.com/user-attachments/assets/50bafc05-e01c-4961-b865-2fef2fbc3ec7" />

    - A warning will appear stating the disk will be formatted. Click **Yes**.
        
8. **Confirmation:** Review your settings and click **Finish**. Once the summary shows success, click **Close**.

    <img width="648" height="497" alt="image" src="https://github.com/user-attachments/assets/efafb823-fd3f-4014-b955-526a357b6574" />


---

## Part 2: Performing an On-Demand Backup

*    Continue with this link : https://github.com/avadh-150/MCSE_Server_Notes/blob/main/Windows%20Server%20Backup/Phase%204%3A%20Back%20up%20Once%20%26%20Recoves%20Filer.md

---
