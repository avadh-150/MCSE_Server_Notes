**Active Directory Database (AD DB)** — this is where people _think_ they understand AD and then prove they don’t. Let’s fix that.

---

## What “AD DB” actually is

Active Directory stores its data in a **single logical database** called:

```
NTDS.DIT
```

That’s it. No MySQL. No tables you can open. No “just query it directly”.

If you try to treat it like a normal DB, you’ll corrupt your domain.

---

## Core AD Database Components (Know all 4 or you don’t know AD)

| Component        | Purpose          | Reality                                    |
| ---------------- | ---------------- | ------------------------------------------ |
| **NTDS.DIT**     | Main AD database | Users, groups, computers, hashes, policies |
| **EDB.log**      | Transaction logs | Write-ahead logging (prevents corruption)  |
| **EDB CHK file** | Checkpoint       | Tracks committed transactions              |
| **RES1 / RES2**  | Reserved space   | Emergency disk-full protection             |

Default path:

```
C:\Windows\NTDS\
```

---

## What’s inside NTDS.DIT (High-level, not fantasy)

Stored objects:

- Users
    
- Groups
    
- Computers
    
- OUs
    
- GPO metadata
    
- Trusts
    
- Security descriptors
    
- **Password hashes (NOT plaintext)**
    

Stored engine:

- **Extensible Storage Engine (ESE / JET Blue)**
    

This is a Microsoft database engine — **not** SQL Server.

---

## Password Storage (Critical Security Reality)

AD **never stores plaintext passwords**.

It stores:

- **NTLM hash**
    
- **Kerberos keys** (derived from password)
    

That’s why:

- Hash theft = total domain compromise
    
- Protecting **Domain Controllers** is non-negotiable
    

If an attacker gets NTDS.DIT + SYSTEM hive → game over.

---

## AD Replication (This is where DB matters)

AD uses **multi-master replication**.

Key facts:

- Every DC has its **own copy** of NTDS.DIT
    
- Changes replicate via **RPC**
    
- Uses **Update Sequence Numbers (USN)**
    

No “primary DB”.  
No single master (FSMO ≠ DB master).

---

## Transaction & Recovery Model

AD uses **write-ahead logging**:

1. Change written to **EDB.log**
    
2. Change committed to **NTDS.DIT**
    
3. Checkpoint updated
    

Why this matters:

- Sudden power loss ≠ corrupted DB (usually)
    
- Logs are required for recovery
    

Deleting logs blindly is how amateurs destroy AD.

---

## AD DB vs SYSVOL (People mix these up)

|NTDS.DIT|SYSVOL|
|---|---|
|Directory data|Files & scripts|
|Stored in ESE DB|Stored as filesystem|
|Replicated via AD|Replicated via DFSR|
|Contains passwords|Contains GPO files|

They are **not the same thing**.

---

## Backup & Restore (No Shortcuts)

Supported methods only:

- **System State Backup**
    
- **Bare Metal Backup**
    

Restore types:

- **Authoritative** → Force replication of restored data
    
- **Non-authoritative** → Sync from other DCs
    

Copying NTDS.DIT manually ≠ backup.

---

## Security Reality (Read carefully)

If someone gets:

- `NTDS.DIT`
    
- `SYSTEM` registry hive
    

They can:

- Dump all password hashes
    
- Perform pass-the-hash
    
- Forge Kerberos tickets (Golden Ticket)
    

This is **why DCs are Tier-0 assets**.

---
## Bottom Line

Active Directory DB is:

- **Central identity brain**
    
- **Single point of catastrophic failure**
    
- **Not forgiving of mistakes**

