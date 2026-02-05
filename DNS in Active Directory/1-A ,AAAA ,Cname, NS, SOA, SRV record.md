
---

## 🧠 A Record — _IPv4 address mapping_

![Image](https://cf-assets.www.cloudflare.com/slt3lc6tev37/6Cxvsc4NOvmU4pPkKbkDmP/a7588a4c8a3c187e9175a40fa1b3d548/dns_record_request_sequence_authoritative_nameserver.png)

![Image](https://miro.medium.com/1%2AgoSb1oow5UBNF3KkzvOX8A.png)

![Image](https://image.hostingraja.in/images/articles/aisa-help/connect-point-domain-in-hostingraja-to-another-server.png)

**What it does**

Maps a hostname → IPv4 address.

👉 This is the most basic DNS record.

Example:

```
server.abc.com → 192.168.1.10
```

When a device asks:

> “Where is server.abc.com?”

DNS answers with an IPv4 address.

**Used for**

✅ Web servers  
✅ Domain controllers  
✅ Any IPv4 reachable host

No A record → name doesn’t resolve → connection fails.

---

## 🌍 AAAA Record — _IPv6 address mapping_


![Image](https://library.mosse-institute.com/_images/dns.png)

![Image](https://substackcdn.com/image/fetch/f_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F96fbf5fc-bf5d-4047-b058-f48f6f3b3a30_1600x1432.png)

Same idea as an A record…

…but for **IPv6**.

Example:

```
server.abc.com → 2001:db8::1
```

Modern networks rely on this.

**Used for**

✅ IPv6-enabled servers  
✅ Future-proof networking

Think:

> A = IPv4  
> AAAA = IPv6

---

## 🔗 CNAME Record — _Alias / nickname_


![Image](https://static.colinbarker.me.uk/img/blog/2024/12/DNSandCnamesBlogPost-ResolverIssue.jpg)


Creates an alias pointing to another hostname — not an IP.

Example:

```
mail.abc.com → server.abc.com
```

DNS resolves:

```
mail → server → IP
```

**Used for**

✅ Friendly names  
✅ Service aliases  
✅ Redirect-style naming

Important:

❌ CNAME never points directly to IP  
❌ You cannot mix CNAME with other records for the same name

---

## 🧭 NS Record — _Name server authority_

![image](https://mymeasi.wordpress.com/wp-content/uploads/2019/10/image-33.png)

Defines:

> “Which DNS server is responsible for this domain?”
> Metadata that **identifies which servers are authoritative for a specific DNS zone.**

Example:

```
abc.com → ns1.abc.com
```

This enables DNS delegation and hierarchy.

**Used for**

✅ Domain authority  
✅ Zone delegation  
✅ DNS infrastructure

Without NS → domain authority is undefined.

---

## 📜 SOA Record — _Start of Authority_

![Image](https://www.mcmcse.com/microsoft/guides/70-411/images/dns_zones2.jpg)

The **master record** of a DNS zone.

- **SOA (Start of Authority)** record as the **"Configuration File"** or the **"Metadata Header"** for that specific slice of the internet (the Zone).

- While A records and NS records are the _data_ (the phone numbers and addresses), the SOA record is the **set of rules** that governs how that data is shared and cached across the world.
### Components of an SOA Record

- **Primary Server:** The hostname of the primary DNS server (usually your main Domain Controller) that holds the master copy of the zone.
    
- **Responsible Person:** The email address of the administrator. (Note: In DNS records, the `@` symbol is replaced by a `.`, so `admin.domain.com` actually means `admin@domain.com`).
    
- **Serial Number:** A version number for the zone. Every time you make a change (like adding a new host), this number increases. Secondary servers check this number to see if they need to update their records.
    
- **Refresh Interval:** How often secondary servers should check with the primary DC for updates.
    
- **Retry Interval:** How long a secondary server should wait before trying again if a refresh fails.
    
- **Expire Limit:** If the secondary server can’t reach the primary DC for this amount of time, it will stop answering queries for that zone (as the data is considered too old to be reliable).
    
- **Minimum (default) TTL:** The "Time to Live." This tells other DNS servers how long they should cache the information before asking your DC for it again.
---

## 🎯 SRV(Service) Record — _Service locator_

Tells clients:

> “Where is the service running?”

- these are essential DNS records that allow clients to locate Active Directory services, such as LDAP, Kerberos, and GC. They are automatically registered by the Netlogon service
Example:

```
_ldap._tcp.dc._msdcs.abc.com → domain controller
```

Critical for:

✅ Active Directory login  
✅ Kerberos  
✅ VoIP  
✅ Messaging systems

Includes:

- Priority
    
- Weight
    
- Port
    
- Target server
    

Without SRV → services become invisible.

---

## 🔥 Quick Reality Summary

|Record|Purpose|
|---|---|
|A|Host → IPv4|
|AAAA|Host → IPv6|
|CNAME|Alias → hostname|
|NS|Domain authority|
|SOA|Zone control metadata|
|SRV|Service discovery|

---

