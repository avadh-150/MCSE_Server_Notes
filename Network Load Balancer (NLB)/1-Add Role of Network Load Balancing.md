
# 🖥️ Network Load Balancing (NLB) Installation – Windows Server 2022

**Servers:** SVR_1 and SVR_2

---

# 🚀 Phase 1: Installing NLB on SVR_1 & SVR_2

1️⃣ Open **Server Manager** on **SVR_1**.  
2️⃣ Click **Add roles and features** from the Dashboard.  
3️⃣ On the **Before you begin** screen → click **Next**.  
4️⃣ Select **Role-based or feature-based installation** → click **Next**.  
5️⃣ Ensure the correct server (**SVR_1.iforward.in**) is selected → click **Next**.  
6️⃣ On the **Server Roles** page → do **not** select anything → click **Next**.  
7️⃣ On the **Features** page → scroll down and check ✅ **Network Load Balancing**.  
8️⃣ In the pop-up → click **Add Features**.  

![image](https://4sysops.com/wp-content/uploads/2022/10/Adding-the-features-required-for-Network-Load-Balancing.png)

![image](https://www.poweradmin.com/blog/wp-content/uploads/2014/11/network-load-balancing-installation.png)

9️⃣ Click **Next**.  
🔟 Click **Install**.  
⏳ Wait until **Installation succeeded** appears.  
✔️ Click **Close**.

---

# 🔍 Phase 2: Verification

🌐 The video shows **IIS Manager** on **SVR_2** with **Default Web Site** running.

📁 Physical path:

```
C:\inetpub\wwwroot
```

📂 The user opens `C:\inetpub\wwwroot` on **both servers** to confirm web content (e.g., `index.html`) exists and is identical — ensuring the load balancer can serve the same site from both nodes.

---
