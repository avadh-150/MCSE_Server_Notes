## Part 2: Performing an On-Demand Backup

This allows you to run a backup immediately using the settings you just created.

1. **Start Backup:** In the right-hand **Actions** pane, click **Backup Once...**.

   <img width="900" height="650" alt="image" src="https://github.com/user-attachments/assets/c76caf8e-12fc-49d5-9df9-ac2151cf193b" />
    
2. **Backup Options:** Choose **Scheduled backup options** (this uses the items and settings you configured in Part 1). Click **Next**.

   <img width="529" height="444" alt="image" src="https://github.com/user-attachments/assets/35f8531b-9da1-4224-ace2-cd28b06e6952" />
    
3. **Confirmation:** Review the backup details and click **Backup**.

   <img width="529" height="444" alt="image" src="https://github.com/user-attachments/assets/abe31208-c993-4c83-9228-b6d57128f9a0" />

4. **Monitor Progress:** A window will show the status (e.g., "Creating shadow copy of volumes").

   <img width="529" height="444" alt="image" src="https://github.com/user-attachments/assets/3b656a7c-373a-4eef-a3e2-a22b3891d33e" />

5. **Complete:** Once the status changes to **Completed**, click **Close**. You will now see the successful backup listed in the **Messages** and **Status** sections of the main dashboard.

   <img width="1248" height="502" alt="image" src="https://github.com/user-attachments/assets/62f2b7a9-9c34-471a-8b9d-682049778984" />


---

# Recover the Backup From `c:\data`

### Part 1: Recover a Scheduled Backup

1. **Open Windows Server Backup:** Go to **Server Manager**, click **Tools** in the top-right corner, and select **Windows Server Backup**.

2. **Access the Wizard:** In the right-hand **Actions** pane, click **Backup Schedule...**. Click **Next** on the "Getting Started" screen.

    <img width="654" height="501" alt="image" src="https://github.com/user-attachments/assets/0c8f9655-0171-4657-9ab6-3e9ee43509dc" />
    
3. **Select Configuration:** Choose **Custom** to pick specific folders and click **Next**.

   <img width="654" height="501" alt="image" src="https://github.com/user-attachments/assets/ad5b61ae-fa40-4ad4-b807-b05aab0ef9ec" />

4. **Select Backup Location**: 

   <img width="654" height="501" alt="image" src="https://github.com/user-attachments/assets/66703976-9327-4bf0-8cd2-10f3b6bc8dd0" />

5. **Select the Server**:

   <img width="654" height="501" alt="image" src="https://github.com/user-attachments/assets/3d168c29-fb40-4a11-ba95-e3ad422229cc" />
        
6. **Select Time:** Get your preferred time. Click **Next**.

   <img width="654" height="501" alt="image" src="https://github.com/user-attachments/assets/1b4301ce-a3bf-4219-b071-a6f6743350a5" />

8. **Select the Recovery Type:** Next, select the **recovery type**. You can choose files and folders (recover specific files), volumes, and system state.

   <img width="742" height="580" alt="image" src="https://github.com/user-attachments/assets/ee29e26c-96e1-4f3b-b7f1-1bafa70c5d5b" />

10. **Select Recovery Items:**
    
    - Locate the files and folders you want to recover.  Click Next.
      
      <img width="621" height="502" alt="image" src="https://github.com/user-attachments/assets/dcda915d-550a-4c2c-8c8a-23824ac48aec" />

11. **Select Specific Recovery Opt** Specify where the files should be restored to on the local computer.  Click Next

    <img width="631" height="495" alt="image" src="https://github.com/user-attachments/assets/9783584a-fec9-4835-a222-597e9d0267fb" />

12. **Verify** : Verify the settings | files |folders and click Recover when ready.

13. **Final Step** : Recovery Progress and Click Close...

   <img width="654" height="501" alt="image" src="https://github.com/user-attachments/assets/bcdc755a-fb77-41dd-ac62-51070eead18d" />
 
---
