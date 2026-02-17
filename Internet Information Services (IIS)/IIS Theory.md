## IIS on Windows Server 2022 — straight to the point ⚙️


 **Internet Information Services (IIS)** is a **flexible, secure, and manageable web server software developed by Microsoft for Windows operating systems**. 

- It hosts, deploys, and manages web applications and services, supporting HTTP, HTTPS, FTP, and SMTP. 

- It is used to **deliver content**, such as static HTML pages and dynamic web applications (e.g., ASP.NET, PHP), over the internet or intranet.

---

# What IIS actually does

- Serves **HTML / PHP / ASP.NET** sites 🌐
    
- Hosts **internal apps / APIs** 🧩
    
- Provides **HTTPS (SSL/TLS)** 🔒
    
- Supports **FTP** file hosting 📁
    
- Integrates with **Active Directory auth** 👤
    

If you plan cybersecurity + Windows infra → you must understand IIS attack surface (misconfig, outdated modules, weak TLS, etc.).

---

# Install IIS on Windows Server 2022

No fluff — exact steps 👇

### GUI method

1. **Server Manager**
    
2. Add Roles and Features
    
3. Role-based installation
    
4. Select server
    
5. Check **Web Server (IIS)**
    
6. Add features
    
7. Install
    

Done. IIS is live.

---

# Verify IIS working

Open browser on server:

```
http://localhost
```

If IIS installed correctly → you’ll see the default IIS page.

---

# IIS Manager (main console)

Open:

```
inetmgr
```

This is where everything happens:

- Sites
    
- App Pools
    
- Bindings
    
- Certificates
    
- Logs
    
- Auth
    

---

# IIS architecture (you need this)

![Image](https://learn.microsoft.com/en-us/iis/get-started/introduction-to-iis/introduction-to-iis-architecture/_static/image1.png)


Core components:

**HTTP.sys**  
Kernel driver handling HTTP requests.

**W3SVC**  
Web service managing IIS.

**Application Pool**  
Isolation boundary (each site runs separate worker).

**w3wp.exe**  
Worker process executing site code.

👉 If app crashes → pool recycles → other sites safe.

---

# Create your first website (real admin skill)

Steps:

1. Create folder:
    

```
C:\Sites\DemoSite
```

2. Put index.html inside
    
3. IIS Manager → Sites → Add Website
    

Fill:

- Site name: DemoSite
    
- Physical path: C:\Sites\DemoSite
    
- Binding: http / port 80
    

Start site.

Open:

```
http://server-ip
```

Site loads.

---

# Application Pools (critical concept)

Each site runs inside an App Pool.

Why it matters:

- Isolation
    
- Permissions
    
- Crash containment
    
- Performance tuning
    

Example:

```
Site A → Pool A
Site B → Pool B
```

If Pool A crashes → Site B unaffected.

---

# HTTPS on IIS

Real servers must use TLS.

Steps:

1. Install certificate
    
2. IIS → Site → Bindings
    
3. Add HTTPS
    
4. Select cert
    

Now:

```
https://server-ip
```

---

# Logs location (for security + troubleshooting)

Default:

```
C:\inetpub\logs\LogFiles
```

Learn to read them. Attack detection starts here.

---

# Default IIS root folder

```
C:\inetpub\wwwroot
```

This is default website path.

---

# Common IIS ports

- 80 → HTTP
    
- 443 → HTTPS
    
- 21 → FTP
    

---

# IIS security basics (non-negotiable)

If you run IIS insecurely → you get hacked. Simple.

Must do:

- Disable unused modules
    
- Enforce HTTPS
    
- Patch server
    
- Limit auth methods
    
- Disable directory browsing
    
- Use least-privilege App Pool identity

---

# Reality check for you 🎯

If you’re targeting:

- Sysadmin
    
- Windows admin
    
- Cybersecurity (blue team)
    
- SOC / Infra
    

Then IIS is mandatory skill — not optional.

You should be able to:

- Install
    
- Host site
    
- Configure HTTPS
    
- Read logs
    
- Understand App Pools
    
- Harden server
    

