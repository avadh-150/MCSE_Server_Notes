
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

---

## ✅ Verification (If You Skip This, You’re Guessing)

### 🔍 Test DNS Resolution

Run on iforward.in DC:

```
nslookup dc1.abc.com
```

or

```
nslookup abc.com
```

Expected:  
✔ Response from **10.10.11.20**  
✔ No timeout

---

### 🔍 Check Conditional Forwarder Exists

In DNS Manager:

- Conditional Forwarders
    
- You should see **abc.com → 10.10.11.20**

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

---

## ✅ Verification (Don’t Guess — TEST)

### 🔍 DNS Test from abc.com or Iforward.in-DC

Run: On abc.com PC

```
ping dc.iforward.in 
OR
nslookup dc.iforward.in
```

Run: On iforward.in PC

```
nslookup abc.com
OR
Ping abc.com
```

Expected result:


---
