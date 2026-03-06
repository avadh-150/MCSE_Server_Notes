## Network Load Balancer 🌐⚖️

A **network load balancer** distributes incoming network traffic across multiple servers so no single server gets overloaded.

-  **NLB** enhances the **availability and scalability** of Internet server applications such as those used on web, FTP, firewall, proxy, virtual private network (VPN), and other mission-critical servers.

Simple truth:  
👉 One server = single point of failure  
👉 Load balancer = high availability + scalability

- A **Cluster** in a network load balancer context is a group of independent, interconnected servers (nodes) acting as a single, unified system to handle network traffic.

- By sharing a single virtual IP address (VIP), the cluster provides high availability, fault tolerance, and improved performance by distributing requests among all nodes, ensuring if one fails, others take over. 

---

# What it does (real purpose)

- Spreads traffic across servers 🔄
    
- Prevents overload 🚫🔥
    
- Keeps service alive if one server dies 💀➡️🟢
    
- Improves performance ⚡
    

---

# Basic architecture

![Image](https://i.adroitacademy.com/blog/93638071.jpg)

Flow:

Client → Load Balancer → Server 1 / Server 2 / Server 3

---

# Example (IIS scenario)

You host website on:

- IIS-Server-1
    
- IIS-Server-2
    
- IIS-Server-3
    

Users connect to:

```
www.example.com
```

DNS → Load Balancer IP

Load balancer sends user to any healthy IIS server.

User doesn’t know which server served them.

---

# Types of load balancing

## L4 (Network Load Balancer)

Works at TCP/UDP level

Decisions based on:

- IP
    
- Port
    
- Connection
    

Fast ⚡  
No content awareness

Example:

- Windows NLB
    
- AWS NLB
    
- F5 L4 mode
    

---

## L7 (Application Load Balancer)

Works at HTTP/HTTPS level

Decisions based on:

- URL
    
- Hostname
    
- Cookies
    
- Headers
    

Smarter 🧠

Example:

- Reverse proxy
    
- Nginx
    
- HAProxy
    
- AWS ALB
    

---

# Windows Server NLB (what you study)

Microsoft built-in feature:

**Network Load Balancing (NLB)**

Lets multiple Windows servers share:

- one virtual IP
    
- one hostname
    

---

# NLB key concept

Each server keeps:

Same:

- site files
    
- config
    
- cert
    
- IP cluster
    

Different:

- host priority
    

---

# Traffic distribution methods

- Round robin 🔄
    
- Least connections
    
- Hash based
    

---

# Health checking

Load balancer tests servers:

If server fails ❌  
→ removed from pool

Users never see downtime.

---

# Why NLB matters for you (infra/security)

Real environments always use:

- Web farms
    
- App clusters
    
- HA services
    

Single server setups = amateur lab only.

---

# IIS + NLB real world

Companies run:

Load balancer  
→ multiple IIS servers  
→ shared backend (DB)

This is standard architecture.

---

# Brutal truth 🔥

If you want to work in:

- Sysadmin
    
- Cloud
    
- SOC
    
- Infra security
    
- DevOps
    

You must understand:

- Load balancing
    
- High availability
    
- Clustering
    
