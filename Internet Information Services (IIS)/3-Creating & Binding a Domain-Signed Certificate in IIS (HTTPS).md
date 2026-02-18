# 🔐 Creating & Binding a Domain-Signed Certificate in IIS (HTTPS)

The process covers creating a domain certificate from your internal CA and binding it to a website to enable HTTPS.

---

# 🧾 Phase 1: Create a Domain Certificate in IIS

1️⃣ Open **Internet Information Services (IIS) Manager**

2️⃣ In **Connections** (left pane), click your server  
👉 Example: `SVR_1`

3️⃣ In the center pane, double-click **Server Certificates**

![image](https://s3.us-west-2.amazonaws.com/public-files.geocerts.com/support/je8JDCftRp6xHJYfwUGb)

4️⃣ In the **Actions** pane (right), click  
👉 **Create Domain Certificate…**

![image](https://s3.us-west-2.amazonaws.com/public-files.geocerts.com/support/gG8IAsz0Sb2ciqXu4iig)

5️⃣ **Distinguished Name Properties** → fill details:

- **Common name:** `salary.forward.in`
    
- **Organization:** `iforward`
    
- **Organizational unit:** `IT`
    
- **City/locality:** `Surat`
    
- **State/province:** `Gujarat`
    
- **Country/region:** `IN` (or correct region)
    
	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/3.png?raw=true)

6️⃣ Click **Next**

7️⃣ **Online Certification Authority**

- Click **Select…** → choose CA  
    👉 `forward-DC-CA` → **OK**
    
- **Friendly name:** `salary.forward.in`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/4.png?raw=true)

8️⃣ Click **Finish**

✅ Certificate now appears in **Server Certificates**

---

# 🌐 Phase 2.1: Bind Certificate to Website (Enable HTTPS) for SRV_1

1️⃣ In IIS left pane → expand **Sites**

2️⃣ Click target site  
👉 Example: **Default Web Site**

3️⃣ Right pane → click **Bindings…**

![image](https://www.ssl.com/wp-content/uploads/2020/02/iis-10-binding-02.png)

4️⃣ In **Site Bindings** → click **Add…**

![image](https://www.ssl.com/wp-content/uploads/2020/02/iis-10-binding-03.png)

5️⃣ **Add Site Binding** settings:

- **Type:** `https`
    
- **IP address:** `10.10.11.11`
    
- **Port:** `443`
    
- **Host name:** `salary.forward.in`
    
- **SSL certificate:** `salary.forward.in`

	![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/5.png?raw=true)

6️⃣ Click **OK**

7️⃣ Click **Close**

✅ HTTPS binding configured

---
# 🌐 Phase 2.2: Bind Certificate to Website (Enable HTTPS) for SRV_2

#### 👉 **DO same as** : phase 2.1 :Bind Certificate to Website (Enable HTTPS) for SRV_1


---
# ✅ Phase 3: Verify Secure Connection

1️⃣ Open browser (Edge / Chrome)

2️⃣ Navigate to:

```
https://salary.forward.in
```

3️⃣ If warning appears:

👉 **Advanced**  
👉 **Continue to salary.forward.in**

4️⃣ Site should load over **HTTPS**  
🔒 Secure connection active

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/(IIS)Creticate%20of%20https/6.png?raw=true)

---

# 🧩 Phase 4: Import Certificate to Browser (Optional)

(Needed if client doesn’t trust internal CA)

1️⃣ **Edge Settings** → Privacy, search, and services

2️⃣ Scroll to **Security** → **Manage certificates**

3️⃣ Go to **Trusted Root Certification Authorities**

4️⃣ Click **Import…** → **Next**

5️⃣ **Browse** → select `.cer` / `.crt` file → **Open**

6️⃣ Place in:  
👉 **Trusted Root Certification Authorities**

7️⃣ Click **Finish**

✅ Browser now trusts internal CA

---
