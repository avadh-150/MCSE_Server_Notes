

This is a **no‑fluff, exam + real‑world focused book** built from your class notes. If you understand this end‑to‑end, you’re not guessing anymore — you actually know how Windows Server & AD work.

---

## Chapter 1: Local System & Administrative Tools

### 1.1 System Utilities (Local Machine)

|Tool|Command|Purpose|
|---|---|---|
|System Properties|`sysdm.cpl`|Computer name, domain join, system info|
|Network Adapter|`ncpa.cpl`|Manage NICs, IP settings|
|Firewall|`firewall.cpl`|Windows Defender Firewall rules|
|Local Users & Groups|`lusrmgr.msc`|Create/manage **local** users|
|Group Policy Editor|`gpedit.msc`|Local Group Policy (non‑domain)|
|Force GP Update|`gpupdate /force`|Apply policies immediately|

⚠️ **Reality check**: `gpedit.msc` works only on **local machines**. In domains, it’s mostly irrelevant.

---

### 1.2 Local Database (SAM)

- **Path**: `C:\Windows\System32\Config\SAM`
    
- Stores:
    
    - Local user accounts
        
    - Password hashes
        

⚠️ **Critical**: If someone gets SAM + SYSTEM files → password cracking is possible. This is why physical security matters.

---

## Chapter 2: What Is a Domain (No BS Explanation)

A **domain** is a **centralized authentication and management boundary**.

Without a domain:

- Every PC manages users separately
    
- No central policy
    
- No scalability
    

With a domain:

- Central user database
    
- Central policies
    
- Single login across machines
    

👉 Domains exist to **control chaos**.

---

## Chapter 3: Active Directory (AD) – Core Concepts

### 3.1 What Is Active Directory?

Active Directory is a **directory service** that:

- Stores objects (users, computers, groups)
    
- Authenticates users
    
- Authorizes access
    

Think of AD as:

> A **database + authentication engine + policy engine**

---

### 3.2 Domain Controller (DC)

A **Domain Controller**:

- Runs **AD DS role**
    
- Stores the AD database
    
- Handles authentication (Kerberos, NTLM)
    

Key files:

- **AD Database**: `C:\Windows\NTDS\ntds.dit`
    
- **SYSVOL**: `C:\Windows\SYSVOL`
    

⚠️ If DC is compromised → **entire domain is compromised**.

---

## Chapter 4: Creating a Domain (Step‑by‑Step Logic)

### 4.1 Install AD DS Role

1. Open **Server Manager**
    
2. Add Roles → **Active Directory Domain Services**
    

---

### 4.2 Promote Server to Domain Controller

- Choose **Add a new forest**
    
- Provide domain name (example: `corp.local`)
    
- Set **DSRM password** (important for recovery)
    

Outcome:

- Server becomes DC
    
- AD database created
    
- DNS installed automatically
    

---

## Chapter 5: Organizational Units (OU)

### 5.1 What Is an OU?

OU is a **logical container** used to:

- Organize users/computers
    
- Apply Group Policies
    
- Delegate admin control
    

Example structure:

```
corp.local
 ├── Admins
 ├── HR
 ├── IT
 └── Computers
```

⚠️ GPOs apply to **OUs**, not to individual users directly.

---

## Chapter 6: Group Policy (Domain Level)

### 6.1 Group Policy Management

- Tool: `gpmc.msc`
    
- Policy storage:
    
    - **SYSVOL**: `C:\Windows\SYSVOL`
        

Types:

- Computer Configuration
    
- User Configuration
    

⚠️ `gpedit.msc` ≠ `gpmc.msc`

---

### 6.2 Group Policy Processing Order (LSDOU)

1. Local
    
2. Site
    
3. Domain
    
4. OU
    

Last applied policy wins.

---

## Chapter 7: DNS in Active Directory

### 7.1 Why DNS Is Mandatory

AD **cannot work without DNS**.

Functions:

- Name → IP resolution
    
- Service location (SRV records)
    

Port used:

- **53 (TCP/UDP)**
    

---

### 7.2 DNS Zones

|Zone Type|Meaning|
|---|---|
|Forward Lookup|Name → IP|
|Reverse Lookup|IP → Name|

Common record:

- **A Record** → Hostname to IPv4
    

Tool:

- `dnsmgmt.msc`
    

---

## Chapter 8: Directory Access Tools

|Tool|Purpose|
|---|---|
|`dsa.msc`|Active Directory Users & Computers|
|`dnsmgmt.msc`|DNS Manager|
|`gpmc.msc`|Group Policy Management|

---

## Chapter 9: Real‑World Security Notes

- Protect **Domain Controllers** first
    
- Monitor access to:
    
    - `ntds.dit`
        
    - SYSVOL
        
- DNS misconfiguration breaks AD
    
- GPO mistakes can lock out entire org
    

---

## Final Advice (Straight Talk)

If you:

- Understand AD database paths
    
- Know why DNS is critical
    
- Can explain OU + GPO flow
    

Then you’re **above average already**.

Next logical step:

- AD attacks (Pass‑the‑Hash, Kerberoasting)
    
- Backup & recovery of AD
    
- Read‑only Domain Controllers (RODC)
    

---

**This is a foundation book. Master this before moving to security exploitation.**