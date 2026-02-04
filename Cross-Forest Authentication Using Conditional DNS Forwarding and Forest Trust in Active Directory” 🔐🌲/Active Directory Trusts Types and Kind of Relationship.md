
---

# 🔐 Active Directory Trusts

There are **TWO different classifications** people confuse:

1️⃣ **TYPE of Trust** → _Direction_  
2️⃣ **KIND of Trust** → _Relationship / Scope_

If you mix these up = instant fail ❌

---

## 1️⃣ **TYPE of TRUST (Direction-based)**

👉 This answers: **“Who trusts whom?”**

![Image](https://learn.microsoft.com/en-us/entra/identity/domain-services/media/concepts-forest-trust/kerberos-over-forest-trust-process-diagram.png)

![Image](https://learn.microsoft.com/en-us/entra/identity/domain-services/media/concepts-forest-trust/trust-relationships.png)

### 🔹 One-Way Trust

```
Domain A  ----trusts---->  Domain B
```

- Users from **Domain B** can Access OR Authenticate **Domain A**
    
- Domain A users **cannot** access OR Authenticate Domain B
    

📌 Think like this:  
**Access flows in ONE direction**

🧠 Real-world use:

- Partner company
    
- Vendor access
    
- External authentication
    

⚠️ Security note:  
This is **safer** than two-way. Less attack surface 🛡️

---

### 🔹 Two-Way Trust

```
Domain A  <----trusts---->  Domain B
```

- Users from both domains can access OR Authenticate each other
    
- Mutual trust
    

🧠 Real-world use:

- Internal company domains
    
- Same organization, different regions
    

⚠️ Reality check:

- If one domain is compromised → the other is at risk 😈
    

---

## 2️⃣ **KIND of TRUST (Relationship-based)**

👉 This answers: **“What kind of relationship is this?”**

---
### 🔹 Parent–Child Trust

- Automatically created
    
- Between **parent domain** and **child domain**
    
- **Two-way**
    
- **Transitive**
    

Example:

```
iforward.in
   |
   └── uk.iforward.in
```

📌 No admin action needed  
📌 Exists by default

---

### 🔹 Tree-Root Trust

- Between **two trees in same forest**
    
- Automatically created
    
- **Two-way**
    
- **Transitive**
    

Example:

```
iforward.in
anotherdomain.in
(same forest)
```

---

### 🔹 External Trust

- Between **two separate forests**
    
- Manual creation
    
- **Non-transitive**
    
- Can be **One-way or Two-way**
    

🧠 Use case:

- Legacy domains
    
- Partner company
    
- NT4 / old AD compatibility
    

⚠️ Security note:  
Stops trust from spreading — **very controlled** 🔒

---

### 🔹 Forest Trust (🔥 IMPORTANT 🔥)

- Between **two different forests**
    
- Manual creation
    
- **Transitive**
    
- Can be **One-way or Two-way**
    

🧠 Use case:

- Company mergers
    
- Shared resources across organizations
    

⚠️ Requirement:

- Forest Functional Level ≥ **Windows Server 2003**
    

⚠️ Attack reality:

- Forest trust = **forest-level risk**
    
- One compromised forest can laterally move 😬
    
---
## 🧠 TRANSITIVE vs NON-TRANSITIVE (Don’t screw this up)

### 🔁 Transitive Trust

Trust extends automatically

```
A trusts B
B trusts C
→ A trusts C
```

### 🚫 Non-Transitive Trust

Trust stops at one level

```
A trusts B
B trusts C
→ A DOES NOT trust C
```

---

## 🔥 EXAM / INTERVIEW TRUTH TABLE

| Category          | Options                                   |
| ----------------- | ----------------------------------------- |
| **Type of Trust** | One-Way, Two-Way                          |
| **Kind of Trust** | Parent-Child, Tree-Root, External, Forest |
| **Transitivity**  | Transitive, Non-Transitive                |

---

