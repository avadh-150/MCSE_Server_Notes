# Active Directory Recycle Bin 
---

## What is the AD Recycle Bin?

The Active Directory Recycle Bin is a forest-level feature that preserves deleted Active Directory objects in a fully-restorable state, including all non-sensitive attributes (group membership, DNSHostName, userPrincipalName, etc.). When enabled, deletions mark objects as `isDeleted = TRUE` and the object remains recoverable with full attributes — unlike tombstoning which strips many attributes.

> **Important:** Enabling the Recycle Bin is irreversible for that forest: it cannot be disabled once turned on.


## Why use it / Benefits

- Restore deleted users, groups, OUs, computer objects with all attributes intact (no need for authoritative restore or system state backups).
- Faster recoveries with lower operational impact than performing offline restores from backup media.
- Maintains group membership and other attributes that tombstoned objects lose, reducing manual reconfiguration after restore.
- Auditability: easier to locate deleted objects and review deletion time, deleted-by metadata.


## Minimum requirements (prerequisites)

1. **Forest functional level**: Must be at least **Windows Server 2008 R2** (the Recycle Bin feature was introduced in 2008 R2). If your forest functional level is lower, raise it first (plan carefully).
2. **Permissions**: You must be a member of **Enterprise Admins** (or have equivalent permissions) to enable the feature.
3. **Replication healthy**: All domain controllers should be replicating successfully before enabling — enabling is a forest-wide AD schema/behavior change.
4. **Backups / change control**: Create an AD backup and document the planned change (cannot be reversed).


## Important concepts and retention windows

- **Deleted object lifecycle**:
  1. **Deleted state (logically deleted)** — the object is flagged but many attributes remain when Recycle Bin is enabled.
  2. **Recycled / Tombstoned** — older AD behaviors: after tombstone lifetime the object metadata is removed and object cannot be fully restored.

- **Tombstone lifetime vs. Recycle retention**:
  - **TombstoneLifetime** (an attribute on the `Directory Service` object in the `Configuration` partition) governs how long tombstoned objects remain before being garbage-collected by DCs. The actual configured value can vary depending on when AD was created and your environment settings.
  - **Recycle Bin / Deleted object retention**: If the Recycle Bin is enabled, deleted objects remain in the Deleted Objects container and are recoverable until they are garbage-collected — effectively controlled by the same lifecycle mechanisms and replication. **Do not rely on a fixed day-count without checking your environment.**

- **Best practice**: **Check** your forest's `TombstoneLifetime` (and `msDS-DeletedObjectLifetime` if present in modern ADs) using PowerShell before relying on a specific retention window.


## GUI: Enable Recycle Bin (ADAC) — Step-by-step

> **Path:** `Server Manager` → `Tools` → **Active Directory Administrative Center (ADAC)** → Select your forest (e.g., `IFORWARD (Local)`) → **Enable Recycle Bin** (or from the ADAC navigation pane: `Tree: <Forest Name> -> Enable Recycle Bin`).

1. Open **Server Manager** on a management server or DC with AD tools installed.
2. Click **Tools** → **Active Directory Administrative Center**.
3. In ADAC, in the left navigation pane expand your forest. Usually the top node is the **Forest root** (e.g., `IFORWARD (Local)` or your forest display name).
4. Right-click the forest node (or use the **Tasks** / **Enable** link shown in the **Active Directory Administrative Center** main pane) and click **Enable Recycle Bin**.
5. A confirmation dialog will appear indicating this is a forest-level, irreversible change. Review the dialog and confirm (you must be Enterprise Admins to continue).
6. After enabling, replicate and verify on all domain controllers.

**Notes:**
- ADAC will show status if Recycle Bin is enabled.
- If the option is greyed out, check forest functional level and admin permissions.


## PowerShell: Enable / Verify / Restore — Commands

> Use AD PowerShell module (ActiveDirectory). Run on a machine with RSAT/AD PowerShell module installed.

### Import the module (if needed)

```powershell
Import-Module ActiveDirectory
```

### 1) Check forest functional level

```powershell
Get-ADForest | Select-Object ForestMode
```

If `ForestMode` is below `Windows2008R2Forest`, raise it only after planning.

### 2) Verify whether Recycle Bin is enabled

```powershell
(Get-ADOptionalFeature -Filter 'name -like "Recycle Bin*"').EnabledScopes
```

or more explicitly:

```powershell
Get-ADObject -SearchBase "CN=Deleted Objects,DC=forestRootDomain,DC=com" -LDAPFilter "(objectClass=*)" -IncludeDeletedObjects
```

(Use the correct search base for your forest root domain.)

### 3) Enable Recycle Bin (forest-level)

```powershell
# Replace <ForestDN> with your forest's distinguished name, e.g. "DC=iforward,DC=local"
Enable-ADOptionalFeature -Identity "Recycle Bin Feature" -Scope ForestOrConfigurationSet -Target "<ForestDN>"
```

Example (conceptual):

```powershell
Enable-ADOptionalFeature -Identity "Recycle Bin Feature" -Scope ForestOrConfigurationSet -Target "DC=iforward,DC=local"
```

**Important:** After you run this, the change replicates to all DCs and cannot be reversed.

### 4) Check tombstone lifetime and deleted object lifetime

```powershell
# Tombstone lifetime (Config partition)
Get-ADObject -SearchBase 'CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=domain,DC=local' -Properties tombstoneLifetime

# For modern environments msDS-DeletedObjectLifetime may be present in domain/forest
Get-ADObject -SearchBase 'CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=domain,DC=local' -Properties msDS-DeletedObjectLifetime
```

### 5) Restore a deleted object with PowerShell

```powershell
# Find deleted object (use -IncludeDeletedObjects)
$del = Get-ADObject -Filter 'displayName -like "*John*"' -IncludeDeletedObjects -Properties *

# Restore
Restore-ADObject -Identity $del
```

If multiple objects returned, refine the filter by distinguishedName, objectGUID, or sAMAccountName.


## Restore deleted objects (ADAC GUI) — Step-by-step

1. Open **Active Directory Administrative Center (ADAC)**.
2. In the left pane, click your forest, then click the domain node you want to inspect.
3. In the main page under **Tasks** or the domain node, click **Deleted Objects** (or find `Deleted Objects` in the navigation tree).
4. Browse the list — you will see deleted items with `Deleted` icons; select the object to restore.
5. Right-click the object → **Restore** or **Restore To...** (choose `Restore To...` if you need to change its parent OU during restore).
6. Confirm restore and verify the object appears back in the original (or chosen) container.

**Notes:**
- ADAC shows properties and attributes of the deleted object before restore so you can verify membership and attributes.


## Cross-domain / Forest considerations (verification & notes)

- **Forest-level feature**: The Recycle Bin is enabled at the **forest** level and therefore affects all domains within the forest.
- **Cross-domain restore**: You cannot restore objects into a different forest with the built-in Recycle Bin — restores are within the same forest. You can restore into a different domain in the forest if you use `Restore To...` and have appropriate permissions, but be mindful of domain-specific constraints (e.g., SIDHistory, domain local groups, domain-specific attributes).
- **Verification steps across domains**:
  1. After enabling, run `Get-ADOptionalFeature` in each domain to confirm the feature is visible and replication completed.
  2. Check replication status (`repadmin /replsummary`) to ensure all DCs across domains have received the change.


## Troubleshooting & checks

- **Enable option greyed out**: Check forest functional level and your account is in **Enterprise Admins**.
- **Cannot find deleted objects**: Use `Get-ADObject -IncludeDeletedObjects` to search; ADAC may filter by default.
- **Object missing attributes after restore**: If Recycle Bin was NOT enabled at deletion time, restore will be partial (tombstoned) and many attributes were already removed — you cannot recover those attributes from Recycle Bin.
- **Replication issues**: If DCs show inconsistent results, run `repadmin /showrepl` and `dcdiag` to fix replication before enabling.


## Quick checklist for change control / roll-out

- [ ] Confirm forest function level `>= Windows Server 2008 R2`.
- [ ] Back up System State of at least one writable DC.
- [ ] Ensure Enterprise Admins approves the irreversible change.
- [ ] Verify AD replication health across all DCs.
- [ ] Test the restore process in a lab/controlled OU first.
- [ ] Enable Recycle Bin and monitor replication.

---
### Final notes
- Enabling AD Recycle Bin is a one-time, forest-scoped action with great benefit for quick recoveries, but it must be planned (forest functional level, backups, replication checks).
---

