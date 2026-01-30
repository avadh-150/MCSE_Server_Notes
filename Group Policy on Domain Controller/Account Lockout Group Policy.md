### **Account Lockout Policy** 
within a Windows Server Active Directory environment using VMware Workstation.

![image](https://activedirectorypro.com/wp-content/uploads/2022/10/account-lockout-policy-default-settings.webp)

The following steps provide in Below:

### Phase 1: Configuring the Group Policy (On the Domain Controller)

1. Open the **Group Policy Management Editor**.

![image](https://activedirectorypro.com/wp-content/uploads/2022/10/edit-default-domain-controller-policy.webp)

2. Navigate to: `Computer Configuration` > `Policies` > `Windows Settings` > `Security Settings` > `Account Policies` > **Account Lockout Policy**.
    
3. Double-click on **Account lockout threshold**.

	![image](https://www.windows-active-directory.com/wp-content/uploads/2021/06/gpme-2.png)


4. Check the box **Define this policy setting** and set the value to **2 invalid logon attempts**.
    
5. Click **Apply**. A "Suggested Value Changes" window will appear notifying you that the "Account lockout duration" and "Reset account lockout counter after" will both be set to **30 minutes** by default. Click **OK** on both windows.

    ![image](https://activedirectorypro.com/wp-content/uploads/2022/10/modify-account-lockout-policy.webp)

---

### Phase 2: Updating the Policy (On the Client Machine)

1. Switch to the client machine (e.g., PC1).
    
2. Open the **Start Menu**, type `cmd` or `gpupdate /force`, and run the command.
    
3. Wait for the message: **"Computer Policy update has completed successfully."**
    
4. Log off the current user to return to the sign-in screen.
    

---

### Phase 3: Testing the Lockout

1. On the login screen for **user1**, intentionally enter the **wrong password** 5 times.
    
2. After the 5  failed attempt, the system will display the following message:
    
    > "The referenced account is currently locked out and may not be logged on to."
    
3. Click **OK**.

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/User%20is%20Loked.png?raw=true)
	
---

### Phase 4: Unlocking the Account (On the Domain Controller)

1. Return to the Domain Controller and open **Active Directory Users and Computers**.
    
2. Navigate to the folder containing your user (e.g., the **Users** container or a specific OU like **HR**).
    
3. Right-click on **user1** and select **Properties**.
    
4. Go to the **Account** tab.
    
5. Look for the text: _"Unlock account. This account is currently locked out on this Active Directory Domain Controller."_
    
6. Check the box for **Unlock account**.
    
7. Click **Apply** and then **OK**.

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/unlock%20acounts.png?raw=true)

---

### Phase 5: Verification

1. Switch back to the client machine (**PC1**).
    
2. Enter the **correct password** for **user1**.
    
3. The user should now log in successfully without the lockout message appearing.
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/Login%20is%20Done.png?raw=true)