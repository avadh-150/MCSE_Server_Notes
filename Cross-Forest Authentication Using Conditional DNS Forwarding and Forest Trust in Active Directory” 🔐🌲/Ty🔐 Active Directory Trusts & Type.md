## Trust in Active Directory — what it actually means

A **trust** in **Active Directory** is a **secure relationship between domains or forests** that allows users in one domain to **authenticate and access resources** in another domain — without creating duplicate accounts.

Think of it as:

👉 _“I accept your identity — prove who you are, and I’ll let you in.”_ 🔐

No copying users. No syncing passwords. Just **authentication recognition** between boundaries.
![Image](https://learn.microsoft.com/en-us/entra/identity/domain-services/media/concepts-forest-trust/kerberos-over-forest-trust-process-diagram.png)

![Image](https://learn.microsoft.com/en-us/entra/identity/domain-services/media/concepts-forest-trust/trust-relationships.png)

---
## Trusts allow:

✅ Users from Domain A to access files/apps in Domain B  
✅ Centralized identity without account duplication  
✅ Controlled collaboration between environments

---

## How it works internally 🔍

When a user tries to access a resource in another domain:

1️⃣ User authenticates in their home domain  
2️⃣ A secure trust path validates that identity  
3️⃣ The target domain checks permissions  
4️⃣ Access is granted or denied

Authentication travels **through the trust**, not around it.

No trust → authentication request is rejected ❌

---

## Types of trusts you’ll see 🧠

### 🔹 Parent–Child Trust (automatic)

Created when you make a child domain.

Example:

```
abc.com → child → ukdc.abc.com
```

Trust is:

✔ Automatic  
✔ Two-way  
✔ Transitive

Meaning authentication flows across the domain tree.

---

### 🔹 Tree-Root Trust

Created when adding another domain tree in the same forest.

Trust is:

✔ Still automatic + transitive.

---

### 🔹 External Trust

- Manual, non-transitive, one-way or two-way relationship between a **domain in one forest** and **a domain in other forest** and **separate forest.**

- It is primarily used to share resources between two distinct organizations (e.g., a supplier and a vendor) without merging their infrastructures.

Trust Can be:

➡ One-way — only one side trusts  
➡ Two-way — both trust
➡ **Non-transitive**

---

### 🔹 Forest-Root Trust

Full trust between entire forests.

All domains inside can authenticate (if allowed).

Used in mergers or large org setups.

Trust is:

✔ Manually created  
✔ Two-way OR One-way 
✔ Transitive

---

## Key properties you must understand 💡

### Direction

👉 **One-way trust**  
Domain A trusts B — B users can access A resources.

👉 **Two-way trust**  
Both domains trust each other.

---

## Transitivity

### 🔁 Transitive Trust — trust extends beyond direct domains  

```
A trusts B
B trusts C
→ A trusts C
```

### 🚫 **Non-transitive** — limited only to the defined pair
```
A trusts B
B trusts C
→ A DOES NOT trust C
```

---

## Real-world example 🧪

You create:

```
abc.com (parent)
└── udc.abc.com (child)
```

User **Tom** exists in parent.

Tom logs into child PC:

✔ Child domain trusts parent  
✔ Authentication request travels trust path  
✔ Tom is verified  
✔ Login succeeds

Without trust → login fails immediately 🚫

---

## Bottom line 🎯

A trust is:

> **A secure authentication bridge between domains/forests.**

It does NOT:

❌ Copy accounts  
❌ Share passwords  
❌ Merge domains

It ONLY:

✅ Validates identity across boundaries

---