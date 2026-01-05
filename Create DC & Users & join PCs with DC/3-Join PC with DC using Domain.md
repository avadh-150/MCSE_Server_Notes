
---

## Preconditions (don’t skip, this is where most people screw up)

1. **DC Server 2022**
    
    - AD DS + DNS **installed and promoted**
        
    - Domain name exists (example: `iforward.in`)
        
    - Static IP set on DC (example: `10.10.11.10`)
        
2. **PC1 (Client machine)**
    
    - Network connectivity to DC (same network / routed properly)
        
    - **DNS MUST point to the DC IP** — not router, not Google DNS  
        👉 This is the #1 reason domain join fails.
        

---

## Step 1: Configure DNS on PC1 & 2 (mandatory)

On **PC1 & 2**:

1. Press `Win + R` → type `ncpa.cpl`
    
2. Right-click **Ethernet / Wi-Fi** → Properties
    
3. Select **Internet Protocol Version 4 (IPv4)** → Properties
    
4. Set:
    
    ```
    Preferred DNS server: 10.10.11.10   (DC IP)
    Alternate DNS: (leave blank)
    ```
    
5. Click **OK**

![Image](https://www.groovypost.com/wp-content/uploads/2021/11/8-IPv4-IP-properties.jpg)

![Image](https://images.ctfassets.net/xwxknivhjv1b/649xkLROBw9TNyZUCHPRtc/953ae0404a0280085963620e38102fa8/change_dns_settings_5.png)



⚠️ If DNS is wrong → domain join **will not work**, period.

---

## Step 2: Verify connectivity (don’t assume)

Open **Command Prompt** on PC1:

```cmd
ping 10.10.11.10
nslookup iforward.in
```

Expected:

- Ping replies ✔️
    
- `nslookup` resolves to DC IP ✔️
    

If this fails → **fix network/DNS first**, don’t move ahead like an amateur.

---

## Step 3: Join PC1 to the Domain (GUI method)

1. Press `Win + R` → `sysdm.cpl`
    
2. Go to **Computer Name** tab
    
3. Click **Change**
    
4. Select **Domain**
    
5. Enter domain name:
    
    ```
    iforward.in
    ```
    
6. Click **OK**
    
7. Enter **Domain Admin credentials**
    
    ```
    Username: iforward\Administrator
    Password: ********
    ```
    

![Image](https://www.groovypost.com/wp-content/uploads/2015/09/Join-a-domain-dialog.jpeg)

![Image](https://www.top-password.com/blog/wp-content/uploads/2018/11/change-windows-domain-or-workgroup.png)

If credentials are correct → you’ll see:

> “Welcome to the iforward.in domain”

8. Restart PC1 when prompted
    

---

## Step 4: Verify on Domain Controller

On **DC Server 2022**:

1. Open **Active Directory Users and Computers**
    
2. Go to:
    
    ```
    Domain → Computers
    ```
    
3. You should see **PC1**
    
If it’s there → domain join is **successful**.

<img width="785" height="550" alt="image" src="https://github.com/user-attachments/assets/bf5567a1-6033-4d1c-9edf-eab6cb1f4f16" />

---

## Step 5 (Optional but professional): Move PC1 to correct OU

Since you already mentioned **IT OU** earlier:

1. Right-click **PC1**
    
2. Move → **IT OU**
    
3. Apply GPOs as needed
    

---
