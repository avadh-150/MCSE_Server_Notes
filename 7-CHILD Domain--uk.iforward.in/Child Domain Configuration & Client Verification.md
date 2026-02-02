
---
# **Child Domain Configuration & Client Verification – Step-by-Step Guide** 🖥️🌐

---
## **Objective** 🎯

Configure a **Child Domain Controller** and verify **user authentication and network connectivity** from a domain-joined client PC.

---

## **Environment Overview** 🧱

- **Parent Domain:** iforward.in
    
- **Child Domain:** uk.iforward.in
    
- **Domain Controller:** UKDC
    
- **Client Machine:** PC1
    
- **OS:** Windows Server 2022 / Windows Client
    
- **User Account:** jeson
    

---

## **Part 1: Child Domain Controller Configuration (UKDC)** 🛠️

---

### **Step 1: Login to Domain Controller** 🔐

1. Log in to the Windows Server 2022 VM.
    
2. Use the credentials:
    
    - **Username:** [administrator@uk.iforward.in](mailto:administrator@uk.iforward.in)


---

### **Step 2: Create a New Domain User** 👤

1. Open **Active Directory Users and Computers**
    
    - Run: `dsa.msc`
        
2. Navigate to:
    
    ```
    uk.iforward.in → Users
    ```
    
3. Right-click → **New → User**
    
4. Enter user details:
    
    - **First Name:** jeson
        
    - **User Logon Name:** jeson
        
5. Click **Next**
    
6. Set password and configure options:
    
    - ❌ User must change password at next logon
        
    - ✅ Password never expires
        
7. Click **Next → Finish**
    

✔️ **User account successfully created**

---

### **Step 3: Verify DNS Configuration** 🌍

1. Open **DNS Manager**
    
    - Run: `dnsmgmt.msc`
        
2. Right-click **UKDC** → **Properties**
    
3. Open **Forwarders** tab
    
4. Verify Parent DC IP is present:
    
    ```
    10.10.11.10
    ```
    
5. Navigate to:
    
    ```
    Forward Lookup Zones → uk.iforward.in
    ```
    
6. Verify host records:
    
    - Example:
        
        ```
        PC1 → 10.10.11.15
        ```
        
7. DNS on Dc like **DNS Delegation**


✔️ **DNS resolution confirmed**

---

### **Step 4: Verify Domain Trust Relationship** 🔗 

####  On (UKDC) [uk.iforward.in] Child domain
	
1. Open **Active Directory Domains and Trusts** 
    
2. Right-click **uk.iforward.in** → **Properties**
    
3. Open **Trusts** tab
    
4. Confirm:
    
    - **Parent Domain:** iforward.in
        
    - **Incoming Trust:** Present
        
    - **Outgoing Trust:** Present
        
#### On DC [iforward.in] Parent (Root) domain

1. Open **Active Directory Domains and Trusts** 
    
2. Right-click **iforward.in** → **Properties**
    
3. Open **Trusts** tab
    
4. Confirm:
    
    - **Child Domain:** uk.iforward.in
        
    - **Incoming Trust:** Child
        
    - **Outgoing Trust:** Child


✔️ **Parent–Child trust verified**

---

## **Part 2: Client PC Verification (PC1)** 💻

---

### **Step 5: Login Using Child Domain User** 🔑

1. Start **PC1**
    
2. Select **Other user**
    
3. Login with:
    
    ```
    jeson@uk.iforward.in
    ```
    
4. Wait for first-time profile setup
    

✔️ **Domain login successful**

---

### **Step 6: Verify Logged-In User** 🧪

1. Open **Command Prompt**
    
2. Run:
    
    ```cmd
    whoami
    ```
    
3. Expected output:
    
    ```
    uk\jeson
    ```
    

✔️ **User authenticated from child domain**

---

### **Step 7: Test Network Connectivity to Parent DC** 📡

1. In Command Prompt, run:
    
    ```cmd
    ping 10.10.11.10
    ```
    
2. Expected result:
    
    - Replies received
        
    - **0% packet loss**
        

✔️ **Network connectivity confirmed**

---

## **Final Verification Summary** ✅

|Component|Status|
|---|---|
|Child Domain User|✔️ Created|
|DNS Forwarder|✔️ Working|
|Trust Relationship|✔️ Valid|
|Client Login|✔️ Successful|
|Network Connectivity|✔️ Verified|

---
