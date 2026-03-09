Based on your lab:

- **Domain:** `iforward.in`
    
- **FTP Server:** SRV1 – 10.10.11.11 (IIS FTP)
    
- **Client:** Win10 – 10.10.11.13
    
- **Users:** `ftpuser, user1, user2, s1, s2`
    
- **Password for all:** `Test@123`
    
- **Authentication:** Anonymous / Basic
    
- **Authorization:** All Users / Anonymous Users / Specified Users / Specified Roles or Groups
    
- **Permissions:** Read / Write
    

Configured using **Microsoft Internet Information Services**.

Below is the **complete practical table** showing **login requirement, credentials, and outcome**.

---

# FTP Authentication + Authorization + Permission Possibilities

|#|Authentication|Authorization|Permission|Login Required|Username|Password|Who Can Access|What They Can Do|
|---|---|---|---|---|---|---|---|---|
|1|Anonymous|Anonymous Users|Read|❌ No|Not required|Not required|Anyone from client|Download only|
|2|Anonymous|Anonymous Users|Read + Write|❌ No|Not required|Not required|Anyone|Upload + Download|
|3|Anonymous|All Users|Read|❌ No|Not required|Not required|Anyone|Download|
|4|Anonymous|All Users|Read + Write|❌ No|Not required|Not required|Anyone|Upload + Download|
|5|Basic|All Users|Read|✔ Yes|Any domain user (ftpuser/user1/user2/s1/s2)|Test@123|All domain users|Download|
|6|Basic|All Users|Write|✔ Yes|Any domain user|Test@123|All domain users|Upload|
|7|Basic|All Users|Read + Write|✔ Yes|Any domain user|Test@123|All domain users|Upload + Download|
|8|Basic|Specified Users|Read|✔ Yes|Only specified user (example: ftpuser)|Test@123|Only selected user|Download|
|9|Basic|Specified Users|Write|✔ Yes|Only specified user|Test@123|Only selected user|Upload|
|10|Basic|Specified Users|Read + Write|✔ Yes|Only specified user|Test@123|Only selected user|Upload + Download|
|11|Basic|Specified Roles / Groups|Read|✔ Yes|Any user inside that group|Test@123|Group members only|Download|
|12|Basic|Specified Roles / Groups|Write|✔ Yes|Any user inside that group|Test@123|Group members only|Upload|
|13|Basic|Specified Roles / Groups|Read + Write|✔ Yes|Any user inside group|Test@123|Group members only|Upload + Download|

---

# Example Login From Your Win10 Client

### Anonymous FTP

No credentials required

```
ftp 10.10.11.11
```

Login automatically as **anonymous**

---

### Basic Authentication Example

```
ftp 10.10.11.11
```

Login:

```
Username: ftpuser
Password: Test@123
```

---

# Example Scenario (Specified Users)

If configuration is:

Authentication

```
Basic
```

Authorization

```
Specified Users
```

User allowed:

```
ftpuser
```

Permission

```
Read + Write
```

Result:

|User|Login|Access|
|---|---|---|
|ftpuser|ftpuser / Test@123|Upload + Download|
|user1|user1 / Test@123|❌ Access denied|
|user2|user2 / Test@123|❌ Access denied|

---

# Important Real-World Behavior (Lab Tip)

Even if FTP allows **Write**, upload will fail if **NTFS permissions** are missing.

Example FTP folder:

```
c:\FTP
```

Permissions required:

|Action|NTFS Permission|
|---|---|
|Download|Read|
|Upload|Write / Modify|

Otherwise error:

```
550 Access is denied
```

---
