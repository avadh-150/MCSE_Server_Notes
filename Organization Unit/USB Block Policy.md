# 🔒 USB Access Block Policy (PC & User)

## Step 1: Create OU for USB Block
Open **gpmc.msc** and create a new Organizational Unit named `USB Block`.

📸 Example Screenshot:  
![Create OU for USB Block](../MCSE%20Class%20Notes/img/usb_ou.png)

---

## Step 2: Create GPO for Computer Policy
**Path:**  
`Computer Configuration → Administrative Templates → System → Removable Storage Access`

Enable:
- **All Removable Storage classes: Deny all access**

📸 Example Screenshot:  
![USB Computer Policy](../MCSE%20Class%20Notes/img/Usb_comp_policy.png)

---

## Step 3: User Policy
**Path:**  
`User Configuration → Administrative Templates → System → Removable Storage Access`

Enable:
- **All Removable Storage classes: Deny all access**

📸 Example Screenshot:  
![USB User Policy](../MCSE%20Class%20Notes/img/usb_user_policy.png)

---

## Step 4: Verification
1. Login as a user under `USB Block` OU.  
2. Insert a USB device.  
3. Access should be denied or invisible in File Explorer.

📸 Example Screenshot:  
![USB Policy Verification (Computer)](../MCSE%20Class%20Notes/img/usb_comp_verifi.png)  
![USB Policy Verification (User)](../MCSE%20Class%20Notes/img/usb_user_veri.png)
