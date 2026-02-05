
---

## 🌲 Forest Level Trust (aka **Forest Trust**)

### What it ACTUALLY is

A **Forest Trust** is a trust **between TWO ENTIRE FORESTS**, not just domains.  
This means **every domain** in Forest A can potentially trust **every domain** in Forest B. 🌐⚠️

» Within **forest all domain** have **by default trust relationship among**
**each other**

» Within a forest all DC have **same schema** and **configuration**
**partitions**

» Two forest **do not have trust by default**

» Users from local forest will **not be able to login** to the **specified forest** and vice
versa

» Two way to create a trust between forest

---

## 🔑 Core Characteristics (No confusion allowed)

|Property|Value|
|---|---|
|Scope|🌲 Entire Forest|
|Direction|One-way 🔁 or Two-way 🔄|
|Transitivity|✅ Transitive|
|Creation|Manual|
|Requirement|Forest Functional Level ≥ 2003|
|Risk Level|🔥🔥 VERY HIGH|

---

## 🧠 How Forest Trust REALLY Works

Example:

```
Forest A: iforward.in
Forest B: partner.local
```

If a **two-way forest trust** exists:

- Users in **iforward.in** can access resources in **partner.local**
    
- Users in **partner.local** can access resources in **iforward.in**
    
- Trust flows across **ALL domains automatically**
    

👉 This is **NOT** limited to one domain unless you restrict it.

---

## 🚨 Communicate with 2 Different Forest

#### DNS setup between forest

» **DNS of local forest must know the DNS of**
**specified forest**

» So, we need to **create DNS conditional forwarders** in both forest

» dnsmgmt.msc > **Conditional forwarder**

» Then **we create the trust** 

---

## 🧱 Trust Modes (YOU MUST KNOW THIS)

### 1️⃣ Forest-wide Authentication (DANGEROUS)

- Default option 😐
    
- All users in trusted forest are authenticated automatically
    
- Massive exposure 🚨
    

### 2️⃣ Selective Authentication (SMART)

- Users must be **explicitly allowed**
    
- Requires permissions on target servers
    
- Limits lateral movement 🛡️
    

👉 **Real admins ALWAYS use Selective Authentication**  
If they don’t, they’re reckless or lazy.

---

## 🔁 One-Way vs Two-Way Forest Trust

### 🔹 One-Way Forest Trust (Recommended)

```
Forest A  ----trusts---->  Forest B
```
### 🔹 Two-Way Forest Trust (High Risk)

```
Forest A  <----trusts---->  Forest B
```
---

## 🎯 Real-World Use Case (Legit)

- Company mergers 🤝
    
- Long-term partnerships
    
- Shared applications (Exchange, SharePoint, SAP)
    

❗ NOT for:

- Temporary vendors
    
- Untrusted partners
    
- “Just testing” labs (you’ll forget and regret it)
    

---

## 💀 Interview Kill Question (Know this answer)

**Q:** Why is Forest Trust dangerous from a security standpoint?

**A:**  
Because it is **transitive across all domains**, increases **Kerberos trust paths**, and enables **cross-forest lateral movement** if not restricted with **Selective Authentication**.

If you can’t say that confidently → you’re not ready 🧠🔥

---

