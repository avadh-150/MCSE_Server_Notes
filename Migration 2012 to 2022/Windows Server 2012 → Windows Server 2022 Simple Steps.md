### 🔹 Active Directory Migration (Windows Server 2012 → Windows Server 2022)

1️⃣ Create **Windows Server 2022 VM**  

2️⃣ Configure **Static IP** on new server  

3️⃣ Set **DNS to Old Domain Controller IP**  

4️⃣ **Join Server 2022 to Existing Domain**  

5️⃣ Install **Active Directory Domain Services (AD DS)** Role  

6️⃣ **Promote Server 2022 as Additional Domain Controller**  

7️⃣ Verify **Active Directory Replication** 

`repadmin /replsummary`

8️⃣ Verify **DNS Replication**  

`dnsmgmt.msc`

9️⃣ Transfer **FSMO Roles** Server 2012 to Server 2022  

```
ntdsutil:roles
:connections
:connect to server Win2022(desnation_system_hostname)
:q
:transfer schame ,PDC,naming,infrastructure,rid master
:q
```

🔟 Verify FSMO role ownership  on Server 2022 

`netdom query fsmo`

1️⃣1️⃣ Update **DNS settings on clients to new DC**  

`it on DNS on it network Stack And Configure the New Dns Forworder`

1️⃣2️⃣ Verify **Authentication from new DC**  

1️⃣3️⃣ **Demote Old Domain Controller (Server 2012)** 

`Server manager -> manage -> Remove Roles and Feature`

1️⃣4️⃣ Remove **AD DS Role from Old Server** 

1️⃣5️⃣ Clean up **DNS and Active Directory Metadata**  

1️⃣6️⃣ Verify **Domain Health**  

1️⃣7️⃣ Confirm **Server 2022 is the only Domain Controller**

✅ Migration Complete 🎯