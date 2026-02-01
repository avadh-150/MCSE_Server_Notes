## 🧱 FSMO Roles (Know this or get rejected in interviews)

You must know **what you’re moving** before touching anything:

1️⃣ Schema Master  
2️⃣ Domain Naming Master  
3️⃣ RID Master  
4️⃣ PDC Emulator  
5️⃣ Infrastructure Master

---

## ✅ Preconditions (Don’t be stupid here ❌)

✔ Target DC **must be online**  
✔ Target DC **must be healthy** (`dcdiag` should pass)  
✔ You must be **Enterprise Admin / Schema Admin**  
✔ Use **transfer**, NOT seize (seize is for dead DCs ☠️)

---

## 🔧 Transfer FSMO Roles using `ntdsutil` (CLI Only)

![Image](https://www.dtonias.com/wp-content/uploads/2018/01/transfer-fsmo-roles-dc-11.png.webp)

![Image](https://cdn.dannymoran.com/images/posts/find-fsmo-roles-using-command-prompt-cmd.png)

![Image](https://saeedchowdry.wordpress.com/wp-content/uploads/2015/09/netdom-query.jpg)

### 🔹 Step 1: Open Command Prompt as Administrator

On the **DC that will RECEIVE the roles**.

---

### 🔹 Step 2: Start NTDSUTIL

```cmd
ntdsutil
```

---

### 🔹 Step 3: Enter FSMO Maintenance Mode

```cmd
roles
```

---

### 🔹 Step 4: Connect to the Target DC

```cmd
connections
```

```cmd
connect to server <TargetDCName>
```

Example:

```cmd
connect to server DC
```

If it says **“Connected to DC”**, you’re good 👍  
Now exit connections:

```cmd
quit
```

---

### 🔹 Step 5: Transfer FSMO Roles (ONE BY ONE)

👉 **Schema Master**

```cmd
transfer schema master
```

👉 **Domain Naming Master**

```cmd
transfer naming master
```

👉 **RID Master**

```cmd
transfer rid master
```

👉 **PDC Emulator** (MOST IMPORTANT)

```cmd
transfer pdc
```

👉 **Infrastructure Master**

```cmd
transfer infrastructure master
```

⚠️ **Type `YES` when prompted** — that’s the confirmation.

---

### 🔹 Step 6: Exit NTDSUTIL

```cmd
quit
quit
```

---

## 🔍 Verify FSMO Roles (MANDATORY ✅)

If you don’t verify, you’re careless.

```cmd
netdom query fsmo
```

You should see **all roles owned by the new DC**.
