

# Phase 2: Initializing the Disk in Windows Server    

---

    `Once the hardware is added, you must tell Windows how to use it.`

1. **Power On:** Start the virtual machine and log in as an **Administrator**.
    
2. **Open Disk Management:** 
    
    - Right-click the **Start button** or search for "Disk Management."
        
    - Alternatively, type `diskmgmt.msc` in the search bar and press Enter.
        
3. **Initialize Disk:** A popup labeled "Initialize Disk" should appear automatically detecting the new 10GB drive (Disk 1).
    
    - Select **GPT (Guid Partition Table)** and click **OK**.

      <img width="699" height="527" alt="image" src="https://github.com/user-attachments/assets/8ae59c5e-6615-4cc9-8ca1-ee915ce830ea" />  

4. **Create New Volume:**
    
    - Find the area labeled **10.00 GB Unallocated** (marked with a black bar).
        
    - Right-click the unallocated space and select **New Simple Volume...**.

      <img width="698" height="550" alt="image" src="https://github.com/user-attachments/assets/a0029afa-637d-48da-9e5c-a4fd614da277" />
        
5. **New Simple Volume Wizard:**

      <img width="698" height="550" alt="image" src="https://github.com/user-attachments/assets/9b13a851-3282-4b68-91d9-595220e187ab" />

    - **Size:** Leave it at the maximum amount (approx. 10239 MB). Click **Next**.
        
    - **Drive Letter:** Assign a letter (the video uses **E**). Click **Next**.
        
    - **Format Settings:**
        
        - File system: **NTFS**.
            
        - Volume label: Rename this to **Back-UP Drive**.

          <img width="1024" height="509" alt="image" src="https://github.com/user-attachments/assets/e28576cb-3d93-43c7-bc61-26dc6c3b6564" />

    - Click **Next**, then **Finish**.

      <img width="648" height="497" alt="image" src="https://github.com/user-attachments/assets/6a4b967e-a554-44f7-b72e-7fe2b7f1fa2e" />
