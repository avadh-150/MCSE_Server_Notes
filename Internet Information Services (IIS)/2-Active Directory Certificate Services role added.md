
# 🛡️ Active Directory Certificate Services (AD CS) Installation & Configuration Guide

---

# 📦 Part 1: Installing the AD CS Role

1️⃣ Open **Server Manager** on your **Server DC** virtual machine.  
2️⃣ Click **Manage** (top-right) → **Add Roles and Features**.  
3️⃣ Click **Next** on:

- Before You Begin
    
- Installation Type
    

4️⃣ **Server Selection:**  
✔ Ensure your local server is selected → **Next**

5️⃣ **Server Roles:**  
✔ Check **Active Directory Certificate Services**  
👉 Popup appears → ✔ Include management tools → **Add Features**

6️⃣ Click **Next** through:

- Features
    
- AD CS introduction
    

7️⃣ **Role Services:**  
✔ Certification Authority

8️⃣ ✔ Certification Authority Web Enrollment  
👉 IIS popup appears → **Add Features** → **Next**

9️⃣ Click **Next** through:

- Web Server Role (IIS)
    
- Role Services
    

🔟 **Confirmation:**  
👉 Click **Install**

✅ When status = **Installation succeeded** → **Close**

![image](https://vcloud-lab.com/files/resized/663313/1170;631;4982f19037280d2812b3bf4dcabf0364f9e43b69.png)

---

# ⚙️ Part 2: Post-Deployment Configuration

1️⃣ In **Server Manager**, click ⚑ **Notification Flag**  
👉 **Configure Active Directory Certificate Services**

2️⃣ **Credentials:**  
✔ Administrator account → **Next**

3️⃣ **Role Services:**  
✔ Certification Authority  
✔ Certification Authority Web Enrollment → **Next**

4️⃣ **Setup Type:**  
✔ Enterprise CA → **Next**

5️⃣ **CA Type:**  
✔ Root CA → **Next**

6️⃣ **Private Key:**  
✔ Create a new private key → **Next**

![image](https://vcloud-lab.com/files/resized/663315/1170;861;704366cec2b9f60f0bb547a2810f9db2ac8e55fc.png)

7️⃣ **Cryptography:**  
✔ Default settings

- RSA Microsoft Software KSP
    
- 2048-bit
    
- SHA256  
    👉 **Next**
    

8️⃣ **CA Name:**  
✔ Keep default (example: `iforward-Server-DC-CA`) → **Next**

9️⃣ **Validity Period:**  
✔ Default: **5 Years** → **Next**

![image](https://miro.medium.com/v2/resize:fit:786/format:webp/1*rM2a2dAMGjlU_j2pGwpiEA.png)

🔟 **Certificate Database:**  
✔ Default locations → **Next**

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/1.png?raw=true)

1️⃣1️⃣ **Confirmatihttps://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/2.png?raw=trueon:**  
👉 Click **Configure**

✅ Status: **Configuration succeeded** → **Close**

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/2.png?raw=true)

---

# 🔄 Part 3: Updating Group Policy

(Ensures all domain systems trust the new CA)

1️⃣ Open **Search bar**  
2️⃣ Type:

```
gpupdate /force
```

3️⃣ Press **Enter**

4️⃣ Repeat on:

- SVR_1
    
- SVR_2
    
- Other domain servers
    

---

# 🌐 Part 4: Verify Installation (IIS)

1️⃣ **Server Manager** → **Tools** → **IIS Manager**

2️⃣ Expand your server node

3️⃣ Navigate:  
**Default Web Site → CertSrv**

✅ If present → Web enrollment is working  
👉 Users can request certificates via browser

---
Done. 👍