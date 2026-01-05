# Windows Server & Active Directory Notes

## Topics

1. Workgroup
    
2. Domain
    
3. DNS
    
4. Active Directory Ports
    

---

## 1. Workgroup

### Definition

WORKGROUP is collection of PC with INDIVIDUAL MANAGEMENT  
BY DEFAULT all PC are in WORKGROUP Mode : `sysdm.cpl`

There is no CENTRALIZED DATABASE for AUTHENTICATION  
Each PC is Having its own LOCAL DB

### What is Workgroup?

USERNAME AND PASSWORD are created LOCALLY on PC  
`lusrmgr.msc` is the command to create users in LOCAL DATABASE

LOCAL DATABASE name is **SAM DATABASE** stored at below location:

```
C:\Windows\System32\Config\SAM
```

Above is Default Path it CANNOT be changed

### Local Policy

LOCAL POLICY on each PC is access using command `gpedit.msc`

Local Policy is stored at below location:

```
C:\windows\system32\GroupPolicy
```

Management of PC is INDIVIDUAL hence difficult  
WORKGROUP is a PHYSICAL Boundary

---

## 2. Domain

### What is Domain?

DOMAIN is a logical boundary managed by DOMAIN CONTROLLER (DC)

Domain consists of object  
User, Computer, Printer, OU are known as OBJECT

DOMAIN CONTROLLER (DC) is a Server which has ACTIVE DIRECTORY SERVICE Installed in it

DOMAIN MODE is not there BY default

We install ACTIVE DIRECTORY SERVICE on SERVER and then create a DOMAIN eg..

```
iforward.in
```

After which this server becomes DOMAIN CONTROLLER (DC)

### Centralized Database

In DOMAIN there is CENTRALIZED DB for Authentication  
The UserName and Password are stored in that DB

`dsa.msc` command is used to access centralized DB

Centralized DB name is **NTDS.dit** and stored at below location:

```
C:\Windows\NTDS\ntds.dit
```

### Group Policy

Also a folder is created for storing GROUP POLICY at below location:

```
C:\Windows\sysvol
```

GROUP POLICY is accessed using command `gpmc.msc`

Above is the default path, it can be changed but should be on Local drive of server

Management of all PC is centralized done from DC

---

## 3. DNS

DNS keeps a DB of NAME to PC  
DNS uses port **53**

In DNS there is **Forward Lookup Zone** (means name to IP)

The name and IP combination in DNS is known as **“A” records**

To access DNS Manager in server we use command:

```
dnsmgmt.msc
```

---

## 4. Active Directory Ports

### Important AD Ports

- Port **88** – Kerberos authentication service
    
- Port **464** – Kerberos Password Change service
    
- Port **389** – LDAP Service
    
- Port **3268 / 3269** – Global Catalog Service
    
- Ports **49152–65535** – Dynamic Ports used for replication
    
- Port **445** – SMB Protocol used for File Sharing
    

### Active Directory Port Explanation

LDAP is protocol to access AD DB

Kerberos is an authentication protocol that is used to verify the identity of a user

The Kerberos protocol uses strong secret-key Cryptography so that a user can prove its identity to a server in a secure way

### Common Ports

- HTTP – 80
    
- HTTPS – 443
    
- DNS – 53
    

SP >> Any port  
DP >> Specific port

---

## Active Directory (AD) Database

✓ AD is a service that provides centralized control for all objects in our domain  
✓ The server configured with AD is known as domain controller

AD provides centralized database and centralized management and allows administrator to control the entire domain using a domain controller

✓ Data is stored as object in AD  
✓ Object means – User, computer, group, printer, OU  
✓ Each object consists of attributes

Example:  
User (Object) – Name, address, telephone (attributes)

---

### Files Related to AD

- **NTDS.DIT** – AD database
    
- **EDB.log** – AD transaction logs
    
    - If DC crash, AD can replay logs to recover changes
        
    - User created and modified, password changes, group modify
        
- **RES1.log & RES2.log** – reserved log files
    
- **TEMP.edb** – temporary file
    
- **EDB.chk** – checkpoint file for which logs written to ntds.dit from edb.log
    

---

### Active Directory Benefits

- Provide centralized database
    
- Provide centralized management using group policy
    
- The ntds.dit file supports over 1 billion objects and up to 16 TB in size
    
- We can use up to 1200 domain controller in a single domain
    
- Unlimited domain support in a forest (Microsoft recommends not more than 10 domains per forest)
    
- Active Directory (AD) depends on DNS
    

---

## Domain (Summary)

Domain is a logical grouping of OBJECT like user, computer, and group for the purpose of management and security

Creating the initial domain controller in a network also creates the domain — you cannot have a domain without at least one domain controller

Each domain is identified by a DNS domain name

---
