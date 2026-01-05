---

---
## 🔑 Core Active Directory Ports (Non-Negotiable)

|     Port | Protocol | Service                  | Why it exists (plain truth)                                             |
| -------: | -------- | ------------------------ | ----------------------------------------------------------------------- |
|   **53** | TCP/UDP  | DNS                      | AD **dies without DNS**. If DNS is broken, AD is broken. Period.        |
|   **88** | TCP/UDP  | Kerberos                 | Authentication. No Kerberos = no secure logons.                         |
|  **135** | TCP      | RPC Endpoint Mapper      | Used to discover dynamic RPC ports. Often blocked → AD breaks silently. |
|  **389** | TCP/UDP  | LDAP                     | AD DB Directory queries, authentication (non-secure).                   |
|  **445** | TCP      | SMB/CIFS                 | SYSVOL, Group Policy, file replication. Absolutely critical.            |
|  **464** | TCP/UDP  | Kerberos Password Change | Password resets and changes.                                            |
| **3268** | TCP      | Global Catalog           | Forest-wide searches (logons in multi-domain forests).                  |
| **3269** | TCP      | Global Catalog over SSL  | Same as above, but encrypted.                                           |

---

## 🔐 Secure Versions (If You Care About Security — You Should)

|Port|Protocol|Service|
|--:|---|---|
|**636**|TCP|LDAPS (LDAP over SSL)|
|**3269**|TCP|Global Catalog over SSL|

If you’re still using plain LDAP (389) in production without LDAPS, you’re **asking** for credential exposure.

---

## 🔄 Replication & Internal AD Plumbing

|Port|Protocol|Service|Reality check|
|--:|---|---|---|
|**5722**|TCP|DFS Replication|SYSVOL replication (modern AD).|
|**9389**|TCP|AD Web Services|Required for PowerShell AD module, ADAC.|
|**49152–65535**|TCP|Dynamic RPC|Yes, this range is huge. Yes, it’s ugly. Yes, AD needs it unless restricted.|

> 🔴 **Most firewall “AD issues” are actually RPC dynamic port issues.**

---

## 🧱 Firewall Reality (Brutal Truth)

If someone tells you:

> “We opened 389 and 445, AD should work”

They are **wrong**.

At minimum between Domain Controllers:

- 53
    
- 88
    
- 135
    
- 389 / 636
    
- 445
    
- 5722
    
- **Dynamic RPC range**
    

Best practice:

- **Restrict RPC range** (e.g. 50000–51000)
    
- Open only that range instead of 49152–65535
    

---

## 🛠️ Typical AD Scenarios → Required Ports

### Domain Join

- 53, 88, 389, 445, 135 + RPC
    

### User Logon

- 53, 88, 445, 3268/3269
    

### Group Policy Not Applying

- 445 ❌ blocked → GPO fails
    
- DFSR (5722) ❌ blocked → SYSVOL issues
    

### Replication Failing

- RPC ports blocked → replication silently breaks

---

## What LDAP actually is

**LDAP (Lightweight Directory Access Protocol)** is a **read/write protocol** used to query and modify directory data.

That’s it.

- It **does NOT authenticate users by itself**
    
- It **does NOT store passwords in plaintext**
    
- It **does NOT replace Kerberos**
    

LDAP is just how clients **talk to a directory** (like Active Directory).

---

## Where LDAP fits in Active Directory

Active Directory is a **directory service**  
LDAP is **one of the protocols** used to access it

AD uses:

- **LDAP** → query users, groups, computers
    
- **Kerberos** → authentication
    
- **DNS** → service discovery
    
- **SMB** → SYSVOL, GPOs
    

If you think LDAP = login, your mental model is broken.

---

## LDAP Ports (No Excuses to Get This Wrong)

|Port|Service|Reality|
|--:|---|---|
|**389/TCP,UDP**|LDAP|Unencrypted. Credentials can be sniffed.|
|**636/TCP**|LDAPS|Encrypted. This is what production should use.|
|**3268/TCP**|Global Catalog LDAP|Forest-wide queries.|
|**3269/TCP**|Global Catalog LDAPS|Secure forest-wide queries.|

> If you’re still using **389 with simple bind** in 2025, that’s a security failure.

---

## LDAP Bind (This is where people screw up)

A **bind** is how a client identifies itself to LDAP.

### Bind types:

1. **Anonymous bind**
    
    - Usually disabled (good)
        
2. **Simple bind**
    
    - Username + password
        
    - **Requires LDAPS** or credentials leak
        
3. **SASL bind (Kerberos / NTLM)**
    
    - Secure
        
    - Preferred in Windows environments
        

**Simple bind over port 389 = credentials in cleartext.**  
No debate.

---

## LDAP Data Model (Know this or stay confused)

LDAP is hierarchical, not relational.

Example DN:

```
CN=AR,CN=Users,DC=example,DC=com
```

- **DN** = Distinguished Name (unique path)
    
- **CN** = Common Name
    
- **OU** = Organizational Unit
    
- **DC** = Domain Component
    

LDAP does not use tables.  
If you think in SQL terms, you’ll misuse it.

---

## What LDAP is commonly used for

Real-world uses (not theory):

- App authentication (GitLab, Jenkins, VPNs)
    
- User & group lookup
    
- Authorization decisions (group membership)
    
- Email address resolution
    
- Central identity source
    

LDAP is **identity plumbing**, not an auth system by itself.

---

## LDAP vs Kerberos (Stop Mixing Them)

|LDAP|Kerberos|
|---|---|
|Directory access|Authentication protocol|
|Query users/groups|Proves identity|
|Can modify directory|Issues tickets|
|Works with many systems|Windows-first|

In AD:

- Login → **Kerberos**
    
- User info lookup → **LDAP**
    

They complement each other. One does not replace the other.
