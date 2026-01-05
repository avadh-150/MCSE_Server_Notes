
## KDC (Key Distribution Center) — the real thing

**KDC** is a **Kerberos component**, not a separate server type.

In **Active Directory**:

> **Every Domain Controller is a KDC**

No extra role. No separate install. No magic box.

---

## What the KDC actually does (no myths)

The KDC has **one job**:  
**issue Kerberos tickets** so identities can be proven **without sending passwords**.

That’s it.

It consists of **two logical services**:

### 1️⃣ AS (Authentication Service)

- Verifies the user
    
- Issues **TGT (Ticket Granting Ticket)**
    

### 2️⃣ TGS (Ticket Granting Service)

- Issues **service tickets**
    
- Lets users access resources (SMB, LDAP, HTTP, etc.)
    

---

## Kerberos flow (you must know this cold)

### Step 1 – Login

Client → KDC (AS)

- Uses password-derived key
    
- Gets **TGT**
    

### Step 2 – Access service

Client → KDC (TGS)

- Presents TGT
    
- Requests service ticket
    

### Step 3 – Access resource

Client → Server

- Presents service ticket
    
- Server trusts the KDC → access granted
    

🔴 **Password is never sent over the network**

If you think it is, your understanding is broken.

---

## KDC Ports (memorize, don’t guess)

|Port|Protocol|Purpose|
|--:|---|---|
|**88**|TCP/UDP|Kerberos (KDC)|
|**464**|TCP/UDP|Password change|
|**389 / 636**|TCP|LDAP (used _with_ Kerberos, not instead)|

If port **88** is blocked → **domain logons fail**.

---

## Where KDC data lives (important)

KDC secrets are stored in:

- **NTDS.DIT**
    
- Memory of the DC
    
- Protected by SYSTEM account
    

This is why:

- Dumping NTDS = Kerberos compromise
    
- Golden Ticket attacks are possible
    

---

## KDC ≠ LDAP (Stop mixing them)

|KDC|LDAP|
|---|---|
|Authentication|Directory access|
|Issues tickets|Queries objects|
|Uses Kerberos|Uses LDAP protocol|
|Port 88|Port 389/636|

Login = **Kerberos (KDC)**  
User lookup = **LDAP**

Different tools. Different jobs.

---

## KDC Failure = Domain Failure

If all KDCs are down:

- No user logins
    
- No service authentication
    
- Cached logins only (temporary)
    

This is why **DC redundancy matters**.

---

## Security Reality (Read carefully)

If an attacker:

- Gets **KRBTGT account hash**
    
- Controls a DC
    

They can:

- Forge tickets
    
- Create **Golden Tickets**
    
- Stay invisible for years
