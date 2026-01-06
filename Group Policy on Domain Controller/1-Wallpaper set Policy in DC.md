
### Step 1: Prepare and Share the Wallpaper

For a GPO to work, the client machine must be able to "reach" the image file over the network.

1. **Create a Folder:** On your DC, create a folder (e.g., `C:\Image$`). $ this sign is for Hide this folder
    
2. **Add the Image:** Put your wallpaper image (e.g., `wp.jpg`) inside that folder.
    
3. **Share the Folder:**
    
    - Right-click the folder > **Properties** > **Sharing** tab > **Advanced Sharing**.
        
    - Check **Share this folder**.
        
    - Click **Permissions**, ensure **Everyone** has **Read** access.

      <img width="363" height="450" alt="image" src="https://github.com/user-attachments/assets/b929bdc2-bd97-41ff-82be-46344138194d" />

    - Click **OK** twice.
        
4. **Copy the Network Path:** Note the path, which should look like `\\DC\image$\wp.jpg`.

5. **Give Read Only Permissions for `Image$`** : Right-Click on `Image$` folder GO TO **properties**

   * Go to Security tab

   * Click Edit

   * Remove unnecessary users

    * Remove:

    * Everyone (if present)

    * Groups of users

    * Add AD Group (correct way)

    * Click Add

    * Enter group name (example):

    `Users`

   * Click Check Names → OK
     
---

### Step 2: Create the Group Policy Object (GPO)

1. **Open Management Tool:** Open **Server Manager** > **Tools** > **Group Policy Management**.

    <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/603257ed-e512-4abe-823c-e039cb557a5d" />

2. **Create GPO:**
    
    - Expand your forest and domain.
        
    - Right-click your **Domain Name** or a specific **OU** (where PC1’s users are located).
        
    - Select **Create a GPO in this domain, and Link it here...**.
    
    <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/34f85a55-1c9f-4205-a7b6-4aab20d10004" />

      
    - Name it `Wallpaper_Policy` and click **OK**.
    

    <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/487fc447-26ac-4fa9-802a-d110ab09cfec" />

---

### Step 3: Configure the Policy Settings

1. **Edit the GPO:** Right-click the new `Wallpaper_Policy` and click **Edit**.

    <img width="1004" height="768" alt="image" src="https://github.com/user-attachments/assets/32edf8fe-e289-4a25-ad1b-e025d460c485" />
    
2. **Navigate to the Setting:**
    
    - Go to: **User Configuration** > **Policies** > **Administrative Templates** > **Desktop** > **Desktop**.

    <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/40ac73d3-b525-4035-9102-b850800ee7b9" />
        
3. **Enable Wallpaper:**
    
    - On the right side, double-click **Desktop Wallpaper**.

      <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/7ecdc4a3-9ef8-438c-8d80-42b14451b29e" />

    - Select **Enabled**.
        
    - **Wallpaper Name:** Paste the **UNC Network Path** from Step 1 (e.g., `\\DC\image$\wp.jpg`).
        
    - **Wallpaper Style:** Choose **Fill** or **Center** (the video uses Center/Fill for best results).
        
    - Click **Apply** and **OK**.

      <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/9547f59a-bb49-414c-8dd7-5782ee51c346" />
---

### Step 4: Verify on PC1

1. Force Update: On PC1, open the Command Prompt and type:
    
    gpupdate /force
    
2. **Log Off/On:** The wallpaper usually requires a fresh login. **Sign out** of PC1 and sign back in.

   <img width="1304" height="768" alt="image" src="https://github.com/user-attachments/assets/caba7975-859a-443c-abf8-f4f0db2ea567" />

    
4. **Result:** The desktop background should now be the image you chose. If you right-click the desktop to change it manually, you will see a message: _"Some settings are managed by your organization,"_ meaning the policy is working.
    
