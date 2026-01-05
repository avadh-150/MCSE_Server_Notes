FSRM is a Windows Server role used to manage and control file server storage using quotas, file screening, and storage reports to prevent misuse, improve security, and monitor disk usage.

---

- FSRM = **control + visibility + prevention**
- Ignore it → disks fill, malware spreads, you look bad

## What FSRM actually does (no fluff)

### 1. **Quota Management**

Controls **how much disk space users or folders can consume**.

- **Hard quota** → limit enforced. Hit the cap, writes fail. Period.
    
- **Soft quota** → no enforcement, just monitoring (useful for planning, not security).


**Reality check:**  
If you care about preventing disk exhaustion, **hard quotas are mandatory**. Soft quotas are for reports, not protection.

**Quota srmsvc Event_id : 12325**

---

### 2. **File Screening**

Blocks or allows **specific file types**.

Examples:

- Block `.mp4`, `.mkv`, `.avi` → stops movie storage
    
- Block `.exe`, `.bat`, `.ps1` → reduces malware risk
    
- Allow-only approach → safest but more admin effort
**Active screening** = block  
**Passive screening** = allow but log

**Blunt truth:**  
If users can upload EXEs to a shared folder, your server is misconfigured. End of story.

**screening id : 8215**

---

### 3. **Storage Reports**

Gives visibility into **what’s eating your disk**.

Reports include:

- Largest files
    
- Duplicate files
    
- File type distribution
    
- Files by owner
    
- Quota usage
    

**Why it matters:**  
Admins who don’t run storage reports always get surprised when disks fill up. That’s incompetence, not bad luck.

---

### 4. **File Classification (Advanced)**

Tags files based on:

- File type
    
- Location
    
- Content
    
- Custom rules
    

Used with **Dynamic Access Control** (DAC).

