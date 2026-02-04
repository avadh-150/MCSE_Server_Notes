
---
## 🧠 What is a Conditional Forwarder? 

A **Conditional Forwarder** is a **DNS rule** that says:

> “If a DNS query is for _THIS specific domain_, send it to _THAT specific DNS server_.”

That’s it.

---

## 🎯 Goal 

On **DC of iforward.in (10.10.11.10)**  
➡ Forward all DNS queries for **abc.com**  
➡ To **abc.com DNS server (10.10.11.20)**

---

## 🧠 Network Prerequisites (DON’T SKIP)

Before touching DNS:

✔ Ping works both ways

```
ping 10.10.11.20
```

✔ Ports open:

- TCP/UDP 53 (DNS)
    
- TCP 88 (Kerberos – later)
    
- TCP 389 (LDAP – later)
    

✔ Each DC uses **itself** as Preferred DNS  
❌ Never point DC to external DNS

If this isn’t done → stop here 😐

---

## 🛠️ Step-by-Step: Create Conditional Forwarder ON DC

**On DC: iforward.in (10.10.11.10)**

### 🔹 Step 1: Open DNS Manager

1. Login to **iforward.in DC**
    
2. Open **Server Manager**
    
3. Go to **Tools → DNS**

---

### 🔹 Step 2: Go to Conditional Forwarders

1. Expand your server name
    
2. Right-click **Conditional Forwarders**
    
3. Click **New Conditional Forwarder…**

![image](https://www.readandexecute.com/wp-content/uploads/2018/05/2018-04-29-13_43_56-DNS-Manager.png)

---

### 🔹 Step 3: Configure Forwarder (THIS PART MATTERS)

Fill **exactly** like this 👇

|Field|Value|
|---|---|
|**DNS Domain**|`abc.com`|
|**IP Address**|`10.10.11.20`|

⚠️ DO NOT type iforward.in here  
⚠️ Domain name must match **other forest**

Click **Add** after entering IP.

---

### 🔹 Step 4: Replication Scope (Important Decision)

You’ll see:

> **Store this conditional forwarder in Active Directory**

✅ **CHECK THIS**

Choose:

- ☑ **All DNS servers in this forest**
    

👉 This ensures:

- All DCs in **iforward.in** know abc.com
    
- No single point of failure
    

Click **OK**

 ![Image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/1.png?raw=true)  

---

### 🔍 Check Conditional Forwarder Exists

In DNS Manager:

- Conditional Forwarders
    
- You should see **abc.com → 10.10.11.20**

 ![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/2.png?raw=true)


---
## 🎯 Scenario (Lock This In Your Head)
    
---

## 🛠️ Step-by-Step: Conditional Forwarder on abc.com DC

### 🔹 Step 1: Open DNS Manager

1. Login to **abc.com Domain Controller**
    
2. Open **Server Manager**
    
3. Click **Tools → DNS**

---

### 🔹 Step 2: Navigate to Conditional Forwarders

1. Expand the server name (**abc.com DC**)
    
2. Right-click **Conditional Forwarders**
    
3. Click **New Conditional Forwarder…**

    ![image](https://www.readandexecute.com/wp-content/uploads/2018/05/2018-04-29-13_43_56-DNS-Manager.png)


---

### 🔹 Step 3: Configure the Forwarder (NO MISTAKES HERE)

Fill it **exactly** like this 👇

|Field|Value|
|---|---|
|**DNS Domain**|`iforward.in`|
|**IP Address**|`10.10.11.10`|

👉 Click **Add** after entering the IP  
👉 You should see it listed below

---

### 🔹 Step 4: Store in Active Directory (IMPORTANT)

✅ Check **“Store this conditional forwarder in Active Directory”**

Select:

- ☑ **All DNS servers in this forest**

Why?

- Replication across abc.com DCs
    
- No single-DC dependency
    
- This is production-correct behavior 💼🔥
    

Click **OK**

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/4.png?raw=true)

---

### 🔍 Check Conditional Forwarder Exists

In DNS Manager:

- Conditional Forwarders
    
- You should see **iforward.com → 10.10.11.10**

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/5.png?raw=true)

---

## ✅ Verification (Don’t Guess — TEST)

### 🔍 DNS Test from abc.com or Iforward.in-DC

Run: On abc.com PC

```
ping dc.iforward.in 
OR
nslookup dc.iforward.in
```
![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/6.png?raw=true)

Run: On iforward.in PC

```
nslookup abc.com
OR
Ping abc.com
```

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/7.png?raw=true)

---
