## 🔐 Active Directory (AD) Groups — Clean Overview

![image](https://ars.els-cdn.com/content/image/3-s2.0-B978193183694450009X-f03-23-9781931836944.jpg)


**Active Directory (AD) groups** are **container objects** used to manage user, computer, and object permissions efficiently ⚙️.

- Instead of assigning permissions individually, you assign them to groups — which keeps environments organized and scalable 📦.

There are **two main group types**, plus **scopes** that define where and how groups function 🌐.

#### For example,
- say in an organization 100 employees need to be given access to a printer, the system administrator, instead of assigning permission to each user (which will be time-consuming and hectic), can put them in a group and assign permission to the group.

---

## 🧩 Types of AD Groups

### 🛡️ Security Groups

- Used to assign permissions to shared resources 📁  
    (files, folders, printers, applications)
    
- Used in **Group Policy** rights assignment ⚡
    
- Core tool for access control 🔒
    

### 📧 Distribution Groups

- Used strictly for **email distribution lists** ✉️  
    (Microsoft Exchange and similar systems)
    
- Cannot assign permissions 🚫
    

---

## 🌍 Group Scopes

Scopes determine **where** a group can be used and **who** can belong to it.

### 🏠 Domain Local

- Grants permissions to resources **within the same domain** 🏢
    
- Can contain members from **any domain** 🌐
	- User and computer accounts, global groups, and universal groups from any domain.
    
- Visibility limited to its own domain 👁️
  
- Managing resources **within a domain**.
    

### 🌐 Global

- Organizes users with similar roles or departments 👥
    
- Members must come from the **same domain** 🧭
    
- Can receive permissions in **any domain** 🔄
    

### 🌎 Universal

- Designed for **multi-domain forests** 🌳
    
- Members can come from **any domain**
    
- Visible forest-wide 👀
    

---

## 🏛️ Common Default Groups

Active Directory includes built-in administrative groups ⚙️:

- 👑 **Domain Admins** — Full control over the domain
    
- 👤 **Domain Users** — Default membership for all users
    
- 🖥️ **Domain Controllers** — All DC machines in the domain
    
- 🛠️ **Administrators** — High-level system permissions
    

![image](https://www.windows-active-directory.com/wp-content/uploads/2021/07/group.png)

---

## ✅ Best Practices for Using Groups

### 🔁 AGDLP Method

A structured permission model:

**A → G → DL → P**

👉 Accounts → Global Groups → Domain Local Groups → Permissions  

Keeps access predictable and manageable 📊

### 🧱 Nested Groups

- Place groups inside other groups to simplify administration 🧩
    
- Reduces duplication and mistakes ⚡
    

### 🔍 Security Discipline

- Regular audits prevent permission sprawl 🚨
    
- Apply **least privilege** principle at all times 🔒
    

---
