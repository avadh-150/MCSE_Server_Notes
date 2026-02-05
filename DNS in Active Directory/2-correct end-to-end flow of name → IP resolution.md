Here’s the **clean, correct end-to-end flow** of **name → IP resolution** from a client PC — with the missing steps filled in and the logic fixed. Some of your wording mixed roles (root DNS vs local cache), so this version reflects how it _actually_ works in Windows DNS resolution. ⚙️🧠

---

## ✅ Complete Name → IP Resolution Process

### **1️⃣ Application generates request**

User/app asks for an IP of `flipkart.com`.

---

### **2️⃣ PC checks Hosts file**

Local static mapping is checked first.

📍Location:  
`C:\Windows\System32\drivers\etc\hosts`

---

### **3️⃣ PC checks DNS cache**

If previously resolved and TTL is valid → use cached IP.

---

### **4️⃣ PC sends recursive query to configured DNS server**

Usually the domain controller or ISP DNS.

---

### **5️⃣ DNS server checks its local sources**

The server tries to resolve without leaving its environment:

#### ✔ Primary zone (Forward Lookup Zone)

![image](https://www.c-sharpcorner.com/UploadFile/cd7c2e/how-to-apply-only-secure-dynamic-updates-to-the-forward-look/Images/record%205.jpg)

---
#### ✔ Secondary zone is  (uk.iforward.in)

![image](https://github.com/avadh-150/MCSE_Server_Notes/raw/main/MCSE%20Class%20Notes/img/Zones/secondary%20zone/4-verify.png?raw=true)

---
#### ✔ DNS Delegation  

- In Parent DNS Automatically an entry for child domain is created
    which is know as DNS delegation
    
»  DNS delegation consist of Child domain’s DNS name and IP

»  DNS delegation created only for child domain

---
#### ✔ Stub zone  

- A **Stub Zone** is a **DNS zone that contains ONLY enough data to find the authoritative DNS servers rather than the entire zone data** 
  ![image](https://1.bp.blogspot.com/-LDH9qmUPcg4/Xbp2ONRACsI/AAAAAAAABAk/gLJHndzh4jgZ10LwxFetOc4UarNoGlX0gCEwYBhgL/s1600/14_confirm_zone_transfer.png)

---
#### ✔ Conditional forwarders  

- > “If a DNS query is for _THIS specific domain_, send it to _THAT specific DNS server_.”

![image](https://github.com/avadh-150/MCSE_Server_Notes/raw/main/MCSE%20Class%20Notes/img/04-02-DNS%20and%20Trust%20connect%202%20frests/Conditional%20Forwarder/5.png?raw=true)

---
#### ✔ Forwarders

- A **blind forwarder** in DNS (often configured as "forward only" in BIND) is a DNS server that is instructed to send all queries if OR it cannot answer locally.

![image](https://i.sstatic.net/PVN5v.png)


---

### **6️⃣ DNS server forwards query**

If a forwarder exists (example: Google DNS `8.8.8.8`):

DNS server sends recursive query to the forwarder.

If no forwarder:

DNS server performs **iterative resolution** starting from root hints → TLD → authoritative server.

---

### **7️⃣ External DNS resolution occurs**

Forwarder/root path resolves:

```
Root DNS → .com TLD → Flipkart authoritative DNS
```

Authoritative server returns the correct IP.

---

### **8️⃣ DNS server caches the result**

Your **local DNS server**, not root DNS, stores the answer based on TTL.

This speeds up future requests.

---

### **9️⃣ DNS server replies to PC**

Resolved IP is returned to the client.

---

### **🔟 PC caches the result**

Client stores IP locally until TTL expires.

---

## 🔥 Visual Flow (mental model)

```
PC → Hosts → Cache → DNS Server
                   ↓
            Local Zones Check
                   ↓
             Forwarder / Root
                   ↓
         Authoritative DNS → IP
                   ↓
        Cache → Reply → Cache
```

---

## ⚠ Important correction

The response is **NOT stored in root DNS cache** — root servers don’t cache for your environment.

Caching happens only on:

✅ Your local DNS server  
✅ The client PC

---
