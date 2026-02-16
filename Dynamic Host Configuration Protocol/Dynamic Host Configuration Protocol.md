
# DHCP on Windows Server — What it actually is

**DHCP (Dynamic Host Configuration Protocol)** = automatic IP assignment service.

Instead of manually setting IP, gateway, DNS on every device (which is stupid at scale), DHCP server does it centrally.

👉 When a device joins network:

1. It asks: _“Anyone got IP?”_
    
2. DHCP server replies with IP config
    
3. Device uses it for lease time
    

That’s it.

---

# Why DHCP on Windows Server exists

In enterprise networks you need:

- Central IP control
    
- No duplicate IP conflicts
    
- Automatic DNS + gateway config
    
- Tracking of devices
    
- Integration with Active Directory
    

Consumer routers do DHCP too — but Windows DHCP is **enterprise-grade + AD-aware**.

---

# DHCP Architecture (Windows)

![Image](https://media.licdn.com/dms/image/v2/D4D12AQEK5ZzE2SbT4Q/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1688885346955?e=2147483647&t=_XG2JlhvEp5XOrKpeIIgL6wNEtbhkEpaxMYlICauXcA&v=beta)


Flow = **DORA** (remember this)

- **D**iscover → client broadcast
    
- **O**ffer → server offers IP
    
- **R**equest → client accepts
    
- **A**ck → server confirms lease
    

If you remember only one thing → remember DORA.

---

# Core DHCP Components (Windows Server)

These are the real things you configure:

### 1️⃣ Scope

IP range the server can give.

Example:

```
192.168.1.100 – 192.168.1.200
```

Without scope → DHCP useless.

---

### 2️⃣ Exclusion

IPs inside range you **don’t want auto-assigned**.

Example:

```
192.168.1.150–160 reserved for printers
```

---

### 3️⃣ Lease

How long device keeps IP.

Typical:

- Office → 8 days
    
- Wi-Fi → 8 hours
    
- Public → 1 hour
    

---

### 4️⃣ Reservation

Permanent IP for specific MAC.

Example:

```
Printer always gets 192.168.1.10
```

Still DHCP-managed — but fixed.

---

### 5️⃣ DHCP Options

Network config given with IP:

- Default Gateway (003)
    
- DNS Server (006)
    
- Domain Name (015)
    
- NTP, PXE, etc.
    

This is where real control lives.

---

# Windows DHCP + Active Directory

Windows DHCP must be **authorized in AD**.

Why?

So rogue DHCP servers don’t mess network.

If unauthorized:  
👉 Service runs  
👉 But gives NO IP

Classic beginner mistake.

---

# Real Enterprise Use Case

Example company network:

- VLAN 10 → Users
    
- VLAN 20 → Servers
    
- VLAN 30 → Wi-Fi
    

You create:

```
Scope 10 → 10.10.10.0/24
Scope 20 → 10.10.20.0/24
Scope 30 → 10.10.30.0/24
```

DHCP Relay on router forwards requests.

Windows DHCP handles all.

---

# DHCP Failover (important)

Production networks need redundancy.

Windows supports:

- Load balance
    
- Hot standby
    

So if DHCP1 dies → DHCP2 continues.

---

# Quick Setup Steps (Windows Server)

No nonsense:

1. Add Roles → DHCP Server
    
2. Complete post-install
    
3. Authorize in AD
    
4. Create Scope
    
5. Set Options (GW + DNS)
    
6. Activate scope
    

Done.

---
