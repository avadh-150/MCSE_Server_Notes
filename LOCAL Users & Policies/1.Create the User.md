Here’s a **clean, properly formatted, professional GitHub-ready README** with spacing, headings, lists, and no emoji clutter unless needed.
---
Got it — that output looks like garbage for a GitHub README.

# **How to Create a Local User in Windows Server 2022**

This guide explains two reliable methods to create a **local user account** in Windows Server 2022.

---

## **Method 1: Using `lusrmgr.msc`**

1. Press **Win + R** to open the Run dialog.
2. Type:

   ```
   lusrmgr.msc
   ```

   and press **Enter**.
3. In the left pane, select **Users**.
4. Right-click in the right pane → **New User**.
5. Enter:

   * Username
   * Full Name
   * Password
6. Configure any required options (e.g., *User must change password at next logon*).
7. Click **Create** → **Close**.
<img width="632" height="412" alt="image" src="https://github.com/user-attachments/assets/9d7b9f10-6902-41ab-980c-738d29748462" />

---

## **Method 2: Using Server Manager (Computer Management)**

1. Open **Server Manager**.
2. Select **Tools** (top-right).
3. Click **Computer Management**.
4. Navigate to:

   ```
   System Tools
   → Local Users and Groups
   → Users
   ```
5. Right-click **Users** → **New User**.
6. Enter username, password, and all required settings.
7. Click **Create**.

---

## **Notes**

* These steps create a **local user**, not a **domain user**.
* For domain users, use **Active Directory Users and Computers (ADUC)** instead.

---
