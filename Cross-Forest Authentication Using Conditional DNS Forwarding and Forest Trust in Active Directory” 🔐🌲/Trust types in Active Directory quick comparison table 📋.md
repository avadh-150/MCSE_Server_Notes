## Trust types in **Active Directory** — quick comparison table 📋

Here’s the clean side-by-side view you want — focused on **how they’re created**, **direction**, **transitivity**, and a **short purpose**.

|Trust Type|Created|Direction|Transitivity|Short definition|
|---|---|---|---|---|
|**Parent–Child**|Automatic|Two-way|Transitive|Links parent and child domains inside the same forest for seamless authentication|
|**Tree-Root**|Automatic|Two-way|Transitive|Connects separate domain trees within one forest|
|**External**|Manual|One-way or Two-way|Non-transitive|Direct trust between domains in different forests without extending trust beyond them|
|**Forest**|Manual|One-way or Two-way|Transitive|Full authentication trust between entire forests|
|**Shortcut**|Manual|Two-way|Transitive|Speeds up authentication between distant domains in the same forest|

---
