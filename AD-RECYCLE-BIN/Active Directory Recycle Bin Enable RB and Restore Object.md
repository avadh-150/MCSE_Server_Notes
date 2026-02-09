
## Active Directory Recycle Bin — what it really is

**Active Directory Recycle Bin** is a recovery feature that lets you restore deleted AD objects **completely intact** — not partially, not rebuilt — but exactly as they were.

Think:

> delete mistake → click restore → everything comes back

![Image](https://www.manageengine.com/ad-recovery-manager/images/recover-nested-ou-in-ad-workflow.jpg)

**Default lifetime:**  
≈ **180 days** (depends on forest settings)

```

Active
  ↓ delete
Deleted (recoverable) —— 180 days
  ↓ expires
Recycled (stripped) —— 180 days
  ↓ cleanup
Permanent deletion

```
---

## What problem it solves 🧠

Before this feature existed:

When you deleted a user…

```
User → tombstoned → most attributes stripped
```

---

With Recycle Bin enabled:

```
Delete → object preserved → full attribute recovery
```

You get back:

✅ SID  
✅ group memberships  
✅ passwords  
✅ OU location  
✅ permissions

Basically — nothing is lost.

---

## What you can restore 🔄

👉 Users  
👉 Groups  
👉 Computers  
👉 OUs (with children)  
👉 Contacts

All with original identity intact.

---
## Enable Active Directory Recycle Bin — the correct way
### ⚠️ Before you start (non-negotiable checks)

✅ All domain controllers must run **Windows Server 2008 R2 or newer**  
✅ Forest Functional Level must be **Windows Server 2008 R2+**  
✅ You must be **Enterprise Admin**

If this isn’t true, the option will be greyed out.

---

## Step-by-step — enable it

1️⃣ Log into a **Domain Controller**

2️⃣ Open:

```
Server Manager → Tools → Active Directory Administrative Center
```

3️⃣ In the left panel:

```
Click your domain name(iforward.in)
```

4️⃣ On the right **Tasks** pane:

```
Click → Enable Recycle Bin
```

![Image](https://www.sidekicktech.com/field-notes/enable-active-directory-recycle-bin/adac-enable-recycle-bin.png)

5️⃣ Confirm the warning dialog

6️⃣ Wait a few seconds — done.

There is **no reboot** required.


![image](https://petri.com/wp-content/uploads/2022/11/Screenshot-2022-11-17-143201.png.webp)


![image](https://petri.com/wp-content/uploads/2022/11/Screenshot-2022-11-17-143356.png.webp)

---

## Verify it actually worked

Inside ADAC:

```
Domain → Deleted Objects container appears
```

If you see it → Recycle Bin is active.

![image](https://petri.com/wp-content/uploads/2022/11/Screenshot-2022-11-17-143606-1-1536x810.png.webp)

---

Alright — you deleted the **Tom** user. Good. Now you’ll restore it properly instead of recreating it and breaking SID/group history. Here’s the exact workflow. ⚙️🗑️➡️👤

## Restore a deleted user in ADAC (Tom)


![Image](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/adac/media/advanced-ad-ds-management-using-active-directory-administrative-center--level-200-/adds_adac_tr_restoresingle.gif)

### Step-by-step

1️⃣ Open **Active Directory Administrative Center**

```
Server Manager → Tools → AD Administrative Center
```

---

2️⃣ Expand your domain

You’ll now see a container named:

```
Deleted Objects
```

Click it.

---

3️⃣ Find the deleted user

Look for:

```
Tom
```

You’ll see it with a deleted icon.

---

4️⃣ Restore it

Right panel → choose one:

👉 **Restore**  
(restores to original OU)

OR

👉 **Restore To…**  
(choose a different OU)

Click → confirm.

Done. ✅

---

## Verify restoration

Check:

```
Users / original OU → Tom appears again
```

Test login if needed.

---

## What just happened internally 🧠

When you deleted Tom:

```
User → moved to Deleted Objects → attributes preserved
```

Restore:

```
Object + SID + group memberships = recovered
```

No rebuild required. No broken permissions.

---
