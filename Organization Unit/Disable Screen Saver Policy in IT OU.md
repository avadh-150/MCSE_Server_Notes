
---
# Disable Screen Saver Policy

## Phase 1: Create and Edit the GPO

1. **Open Group Policy Management:** Press `Win + R`, type `gpmc.msc`, and hit Enter.
    
2. **Create a New GPO:** Navigate to **IT Organizational Unit (OU)**, right-click it, and select **"Create a GPO in this domain, and Link it here..."**.
    
3. **Name the GPO:** Name it something clear, such as `Screen Saver Block Policy`.
    
4. **Open Editor:** Right-click the new GPO and select **Edit**.
    
5. **Navigate to Personalization:** In the Group Policy Management Editor, follow this path:
    
    - **User Configuration** > **Policies** > **Administrative Templates** > **Control Panel** > **Personalization**.
        

---

## Phase 2: Configure the Policies

To effectively disable and lock down the screen saver, you must configure these three specific settings:

| **Policy Setting**                | **State**    | **Impact**                                                               |
| --------------------------------- | ------------ | ------------------------------------------------------------------------ |
| **Enable screen saver**           | **Disabled** | Turns off the screen saver functionality entirely.                       |


---

## Phase 3: Apply and Test

1. **Link the GPO:** Ensure the GPO is linked to the OU containing the **Users** (not the computers), as this is a User Configuration policy.
    
2. Force Update: On the client machine, open the Command Prompt and run:
    
    gpupdate /force
    
3. **Verify on Client:**
    
    - Go to **Settings** > **Personalization** > **Lock Screen**.
        
    - Scroll down to **Screen saver settings**.
        
    - The options should be greyed out, and a message should appear stating: _"Some of these settings are hidden or managed by your organization."_
        

---
