# Intune-Defender Overlap: Current Status & Next Steps

**Date:** February 18, 2026  
**Status:** Ready to implement Phase 1 (Intune includes)  
**Reference:** See [Intune-Defender-Overlap-Include-Files-Strategy.md](Intune-Defender-Overlap-Include-Files-Strategy.md) for full strategy

---

## Current State

### ✅ Completed
- [x] Identified all content overlaps between Intune and Defender docs
- [x] Defined ownership model (Intune owns procedures, Defender owns validation)
- [x] Created comprehensive strategy document with implementation instructions
- [x] Mapped out all 6 include files (4 Intune, 2 Defender)
- [x] Documented cross-repo include syntax and configuration steps

### 🟡 Ready to Execute
- [ ] **Phase 1: Create 4 Intune-owned include files** ← YOU ARE HERE
- [ ] **Phase 2: Update Intune articles to reference includes**

### ⏸️ Waiting (Defender Team)
- [ ] Phase 3: Configure Defender repo for cross-repo includes
- [ ] Phase 4: Update Defender articles to reference Intune includes
- [ ] Phase 5: Create 2 Defender-owned include files
- [ ] Phase 6: Update Intune articles to reference Defender includes

---

## Next Action: Create Intune Includes (I can do this now)

When you're ready to continue, I will:

### Step 1: Create include directory
```bash
mkdir -p intune/includes/endpoint-security
```

### Step 2: Read canonical source articles
- `intune/intune-service/protect/endpoint-security-asr-policy.md`
- `intune/intune-service/protect/endpoint-security-edr-policy.md`
- `intune/intune-service/protect/endpoint-security-antivirus-policy.md`
- `intune/intune-service/protect/endpoint-security-firewall-policy.md`

### Step 3: Extract procedures into 4 include files
- `intune/includes/endpoint-security/create-asr-policy-intune.md`
- `intune/includes/endpoint-security/create-edr-policy-intune.md`
- `intune/includes/endpoint-security/create-antivirus-policy-intune.md`
- `intune/includes/endpoint-security/create-firewall-policy-intune.md`

### Step 4: Update Intune articles to reference the includes
Replace inline procedures with `[!INCLUDE ...]` statements.

**To resume:** Just say "Create the 4 Intune includes now" and I'll execute all steps.

---

## Instructions for Defender Team (Phases 3-6)

### Phase 3: Configure Defender Repo for Cross-Repo Includes

**File to edit:** `defender-docs/.openpublishing.publish.config.json` (or equivalent)

**What to add:**
```json
{
  "dependent_repositories": [
    {
      "path_to_root": "memdocs-pr",
      "url": "https://github.com/MicrosoftDocs/memdocs-pr",
      "branch": "main"
    }
  ]
}
```

**Notes:**
- If `dependent_repositories` already exists, add `memdocs-pr` to the array
- Adjust `branch` if your default branch is different
- This enables Defender articles to reference Intune includes

---

### Phase 4: Update Defender Articles to Reference Intune Includes

Replace duplicated Intune procedures in the following Defender articles with cross-repo include statements.

#### Article 1: `enable-attack-surface-reduction.md`
**Location:** `defender-endpoint/enable-attack-surface-reduction.md`

**Find:** Section with full Intune wizard steps (usually under "Configure ASR with Intune" or similar)

**Replace with:**
```markdown
## Configure ASR with Intune

[!INCLUDE [Create ASR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]

> [!TIP]
> After creating the policy, use the guidance below to test and validate ASR rules.
```

**Keep:** All Defender-specific context (exclusions guidance, method comparison, security rationale)

---

#### Article 2: `attack-surface-reduction-rules-deployment-test.md`
**Location:** `defender-endpoint/attack-surface-reduction-rules-deployment-test.md`

**Find:** Any "Create policy in Intune" walkthrough

**Replace with:**
```markdown
### Configure the policy

[!INCLUDE [Create ASR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]

After creating the policy, continue with testing guidance below.
```

**Keep:** All testing strategy, audit mode guidance, validation steps

---

#### Article 3: `onboarding-endpoint-manager.md`
**Location:** `defender-endpoint/onboarding-endpoint-manager.md`

**Find:** Full Intune EDR policy wizard steps

**Replace with:**
```markdown
## Deploy onboarding with Intune

[!INCLUDE [Deploy EDR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-edr-policy-intune.md)]

After deployment, use the guidance below to verify onboarding status and troubleshoot issues.
```

**Keep:** Prerequisites, onboarding package download/semantics, verification, troubleshooting

---

#### Article 4: `use-intune-config-manager-microsoft-defender-antivirus.md`
**Location:** `defender-endpoint/use-intune-config-manager-microsoft-defender-antivirus.md`

**Find:** "Configure in Intune" section with full wizard steps

**Replace with:**
```markdown
## Configure Microsoft Defender Antivirus with Intune

[!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]
```

**Keep:** Setting behavior explanations, tamper protection notes, security guidance

---

#### Article 5: `configure-real-time-protection-microsoft-defender-antivirus.md`
**Location:** `defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus.md`  
**Section:** "Manage antivirus settings with Microsoft Intune"

**Find:** Full Intune policy creation table/steps

**Replace with:**
```markdown
## Manage antivirus settings with Microsoft Intune

[!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]
```

**Keep:** Real-time protection-specific setting notes and behavior guidance

---

#### Article 6: `enable-cloud-protection-microsoft-defender-antivirus.md`
**Location:** `defender-endpoint/enable-cloud-protection-microsoft-defender-antivirus.md`  
**Section:** "Use Microsoft Intune to turn on cloud protection"

**Find:** Intune policy creation with settings callouts

**Replace with:**
```markdown
## Use Microsoft Intune to turn on cloud protection

To configure cloud protection settings using Intune:

[!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]

When configuring settings in the policy:
- Set **Allow Cloud Protection** to **Allowed**
- Set **Submit Samples Consent** to **Send safe samples automatically** or **Send all samples automatically**
```

**Keep:** Scenario-specific intro and setting callouts unique to cloud protection

---

#### Article 7: `manage-security-policies.md` (light touch)
**Location:** `defender-endpoint/manage-security-policies.md`

**Find:** Any detailed Intune configuration steps (if present)

**Replace with:**
```markdown
For detailed configuration guidance for each policy type, see:
- Firewall: [Firewall policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-firewall-policy)
- Antivirus: [Antivirus policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy)
- ASR: [Attack surface reduction policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-asr-policy)
- EDR: [Endpoint detection and response policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-edr-policy)
```

**Keep:** All Defender portal navigation, permissions, portal policy lifecycle guidance

---

### Phase 5: Create Defender-Owned Include Files

**Who:** Defender content team  
**What:** Create 2 include files for verification/troubleshooting guidance  
**Why:** So Intune articles can point to authoritative Defender validation steps

#### Include 1: `verify-asr-rules.md`

**File to create:** `defender-docs/includes/verify-asr-rules.md` (or equivalent path)

**Content to extract from:**
- Source: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment-test
- Extract: Testing/validation sections (audit mode strategy, what signals to monitor, verification steps in Defender portal)

**What to include:**
- How to verify ASR rules are working
- Audit mode deployment strategy
- What telemetry/signals to monitor in Defender portal
- How to confirm rules are blocking/auditing as expected
- Common validation scenarios

**What to exclude:**
- Intune policy creation steps (already in Intune include)
- High-level conceptual "what is ASR" content (keep in main articles)

**Template structure:**
```markdown
## Verify ASR rules deployment

After deploying ASR rules, verify they're working as expected.

### Test in audit mode first

[Steps to set rules to audit mode and monitor...]

### Monitor ASR events

[How to view ASR events in Defender portal...]

### Validate rule behavior

[Verification scenarios and expected outcomes...]
```

---

#### Include 2: `verify-onboarding-status.md`

**File to create:** `defender-docs/includes/verify-onboarding-status.md` (or equivalent path)

**Content to extract from:**
- Source: https://learn.microsoft.com/en-us/defender-endpoint/configure-machines-onboarding
- Extract: Onboarding verification and troubleshooting sections

**What to include:**
- How to verify devices are onboarded to Defender for Endpoint
- Where to check onboarding status in Defender portal
- Expected timelines for onboarding to complete
- Troubleshooting onboarding failures
- What "healthy onboarded" looks like

**What to exclude:**
- Intune EDR policy creation steps (already in Intune include)
- Initial prerequisites/requirements (keep in main articles)

**Template structure:**
```markdown
## Verify onboarding status

After deploying the EDR policy, verify that devices are onboarded to Microsoft Defender for Endpoint.

### Check onboarding status

[How to view onboarding status in Defender portal...]

### Expected timelines

[How long onboarding takes...]

### Troubleshoot onboarding issues

[Common issues and resolutions...]
```

---

### Phase 6: Configure Intune Repo to Reference Defender Includes

**Who:** Intune content team (I can help with this when Defender includes are ready)

**File to edit:** `memdocs-pr/.openpublishing.publish.config.json`

**What to add:**
```json
{
  "dependent_repositories": [
    {
      "path_to_root": "defender-docs",
      "url": "https://github.com/MicrosoftDocs/defender-docs",
      "branch": "main"
    }
  ]
}
```

**Then update Intune articles:**

#### Update: `endpoint-security-asr-policy.md`
Add new section after policy creation:
```markdown
## Verify ASR rules deployment

After creating and assigning the ASR policy in Intune, verify that rules are working as expected.

[!INCLUDE [Verify ASR rules](~/defender-docs/includes/verify-asr-rules.md)]
```

#### Update: `endpoint-security-edr-policy.md`
Add new section after policy deployment:
```markdown
## Verify onboarding

After the EDR policy is deployed, verify onboarding status in Microsoft Defender for Endpoint.

[!INCLUDE [Verify onboarding status](~/defender-docs/includes/verify-onboarding-status.md)]
```

---

## Quick Reference: Cross-Repo Include Syntax

### Defender articles referencing Intune includes:
```markdown
[!INCLUDE [Display text](~/memdocs-pr/intune/includes/endpoint-security/filename.md)]
```

### Intune articles referencing Defender includes:
```markdown
[!INCLUDE [Display text](~/defender-docs/includes/filename.md)]
```

**Key rules:**
- `~/` = root of dependent repository
- Repository name matches `path_to_root` in `.openpublishing.publish.config.json`
- Use forward slashes `/` even on Windows
- Path is relative to repository root

---

## Validation Checklist (for Defender Team)

After implementing Phases 3-4:
- [ ] `dependent_repositories` configured correctly
- [ ] All 7 Defender articles updated with cross-repo includes
- [ ] Local build succeeds (`docfx build`)
- [ ] No "include file not found" errors
- [ ] Each article still flows naturally with included content
- [ ] All Defender-owned unique content preserved (not deleted)
- [ ] Cross-repo includes display properly (not raw include syntax)

After implementing Phase 5:
- [ ] 2 Defender include files created
- [ ] Each include is self-contained
- [ ] Content extracted from correct canonical sources
- [ ] Heading levels appropriate (typically `##`)
- [ ] Links within includes are absolute URLs (not relative)

---

## Contact Points

**Intune Team (me):**
- Ready to create 4 Intune includes immediately
- Ready to update Intune articles to reference includes
- Available to configure reciprocal dependency when Defender includes are ready

**Defender Team (your partners):**
- Need to configure cross-repo dependency (Phase 3)
- Need to update 7 Defender articles (Phase 4)
- Need to create 2 Defender includes (Phase 5)

**Coordination:**
- Phase 1-2 (Intune) can start immediately
- Phase 3-4 (Defender) can start after Phase 1-2 merge
- Phase 5-6 (reciprocal) optional but recommended

---

## When You Return

**To resume Intune work:** Say "Create the 4 Intune includes now"

**To help Defender team:** Share this file or the full strategy document

**To check status:** Review the checkboxes in "Current State" section above

---

**End of Status Document**
