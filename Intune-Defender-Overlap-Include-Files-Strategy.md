# Intune-Defender Content Overlap: Shared Include Files Strategy

**Date:** February 18, 2026  
**Purpose:** Eliminate content drift between Intune and Defender documentation by using shared include files for overlapping procedural content.

---

## Executive Summary

**Problem:** Intune and Defender documentation currently duplicate identical procedures (e.g., "create ASR policy in Intune"), leading to maintenance burden and content drift.

**Solution:** Move authoritative procedural content into include files owned by the canonical product, then share those includes cross-repository using Microsoft Learn's `~/repo-name/path` syntax.

**Benefits:**
- Single source of truth for each procedure
- No content drift between doc sets
- Clear ownership by canonical product
- Reduced maintenance overhead

---

## Criteria for Include Files vs. Bridges

### ✅ Good for Include Files
- Identical procedures (same click-path in same console)
- Identical prerequisite lists that must stay in sync
- Identical setting definitions/behavior descriptions
- Content that must be word-for-word identical

### ❌ Not for Include Files (use bridges/links instead)
- Content requiring unique contextual intro/framing per article
- Content that might diverge based on audience (IT Pro vs Security Ops)
- High-level conceptual explanations that need product-specific perspective

---

## Recommended Include Files

### **Intune-Owned Includes**
Location: `intune/includes/endpoint-security/`

#### 1. `create-asr-policy-intune.md`
**Content:**
- Full "create ASR policy in Intune" wizard steps
- Navigation: Endpoint security → Attack surface reduction → Create policy
- Steps: Platform selection, profile selection, basics, configuration settings, assignments, scope tags, review + create

**Canonical source article:**
- URL: https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-asr-policy
- Extract from: "Create a policy" or "How to create" section

**Where to include:**
- **Intune articles (same-repo):**
  - `intune/intune-service/protect/endpoint-security-asr-policy.md`
  
- **Defender articles (cross-repo):**
  - `enable-attack-surface-reduction.md`
  - `attack-surface-reduction-rules-deployment-test.md`

**Cross-repo include syntax for Defender:**
```markdown
[!INCLUDE [Create ASR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]
```

---

#### 2. `create-edr-policy-intune.md`
**Content:**
- Full "deploy EDR policy with Intune" procedure
- Navigation: Endpoint security → Endpoint detection and response → Create policy
- Steps: Onboarding package configuration, profile configuration, assignments

**Canonical source article:**
- URL: https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-edr-policy
- Extract from: Core deployment procedure section

**Where to include:**
- **Intune articles (same-repo):**
  - `intune/intune-service/protect/endpoint-security-edr-policy.md`
  
- **Defender articles (cross-repo):**
  - `onboarding-endpoint-manager.md`

**Cross-repo include syntax for Defender:**
```markdown
[!INCLUDE [Deploy EDR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-edr-policy-intune.md)]
```

---

#### 3. `create-antivirus-policy-intune.md`
**Content:**
- Generic "create Endpoint security > Antivirus policy" procedure
- Navigation: Endpoint security → Antivirus → Create policy
- Steps: Platform/profile selection, basics, configuration settings, assignments
- Note: Keep generic; setting-specific callouts stay in consuming articles

**Canonical source article:**
- URL: https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy
- Extract from: "Create policy" procedure section

**Where to include:**
- **Intune articles (same-repo):**
  - `intune/intune-service/protect/endpoint-security-antivirus-policy.md`
  
- **Defender articles (cross-repo):**
  - `use-intune-config-manager-microsoft-defender-antivirus.md`
  - `configure-real-time-protection-microsoft-defender-antivirus.md` (in "Manage with Intune" section)
  - `enable-cloud-protection-microsoft-defender-antivirus.md` (in "Use Intune" section)

**Cross-repo include syntax for Defender:**
```markdown
[!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]
```

---

#### 4. `create-firewall-policy-intune.md`
**Content:**
- "Create Endpoint security > Firewall policy" procedure
- Navigation: Endpoint security → Firewall → Create policy
- Steps: Platform/profile selection, settings configuration, assignments

**Canonical source article:**
- URL: https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-firewall-policy
- Extract from: Policy creation procedure

**Where to include:**
- **Intune articles (same-repo):**
  - `intune/intune-service/protect/endpoint-security-firewall-policy.md`
  
- **Defender articles (cross-repo):**
  - `manage-security-policies.md` (if it currently duplicates Intune steps)

**Cross-repo include syntax for Defender:**
```markdown
[!INCLUDE [Create Firewall policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-firewall-policy-intune.md)]
```

---

### **Defender-Owned Includes**
Location: `defender-docs/includes/` (or equivalent in Defender repository)

**Note:** These cannot be implemented in the Intune repository. They must be created by the Defender content team.

#### 5. `verify-asr-rules.md`
**Content:**
- Testing/validation guidance for ASR rules
- Audit mode deployment strategy
- What signals/telemetry to monitor
- Verification steps in Defender portal

**Canonical source article:**
- URL: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment-test
- Extract from: Testing and validation sections

**Where to include:**
- **Defender articles (same-repo):**
  - `attack-surface-reduction-rules-deployment-test.md`
  
- **Intune articles (cross-repo):**
  - `intune/intune-service/protect/endpoint-security-asr-policy.md` (add validation section)

**Cross-repo include syntax for Intune:**
```markdown
[!INCLUDE [Verify ASR rules](~/defender-docs/includes/verify-asr-rules.md)]
```

---

#### 6. `verify-onboarding-status.md`
**Content:**
- How to verify devices are onboarded to Defender for Endpoint
- Onboarding status tracking
- Troubleshooting onboarding failures
- Expected timelines

**Canonical source article:**
- URL: https://learn.microsoft.com/en-us/defender-endpoint/configure-machines-onboarding
- Extract from: Verification and troubleshooting sections

**Where to include:**
- **Defender articles (same-repo):**
  - `configure-machines-onboarding.md`
  
- **Intune articles (cross-repo):**
  - `intune/intune-service/protect/endpoint-security-edr-policy.md` (add post-deployment verification section)

**Cross-repo include syntax for Intune:**
```markdown
[!INCLUDE [Verify onboarding status](~/defender-docs/includes/verify-onboarding-status.md)]
```

---

## Implementation Instructions

### **Phase 1: Create Intune-Owned Include Files**

**Who:** Intune content team  
**Where:** `memdocs-pr` repository  
**When:** Can be done immediately

#### Step 1: Create directory structure
```bash
mkdir -p intune/includes/endpoint-security
```

#### Step 2: Create include files
Create the following 4 files in `intune/includes/endpoint-security/`:
1. `create-asr-policy-intune.md`
2. `create-edr-policy-intune.md`
3. `create-antivirus-policy-intune.md`
4. `create-firewall-policy-intune.md`

#### Step 3: Extract content into includes
For each include file:
1. Open the canonical source article
2. Locate the procedural section (wizard steps)
3. Copy the complete procedure
4. Ensure it's self-contained (no dependencies on surrounding context)
5. Use relative links where appropriate
6. Start with appropriate heading level (typically `##` or `###`)

**Include file template:**
```markdown
## Create [Policy Type] policy in Intune

1. Sign in to the [Microsoft Intune admin center](https://intune.microsoft.com).
2. Go to **Endpoint security** > **[Policy Type]** > **Create policy**.
3. [Complete wizard steps...]
4. Select **Review + create** > **Create**.

For more information about [specific aspects], see [related article](link).
```

#### Step 4: Update Intune articles to reference includes
In each canonical Intune article, replace the duplicated procedure with:
```markdown
[!INCLUDE [Create ASR policy in Intune](../includes/endpoint-security/create-asr-policy-intune.md)]
```

Use the appropriate relative path based on the article's location.

---

### **Phase 2: Enable Cross-Repo Consumption in Defender Docs**

**Who:** Defender content team  
**Where:** `defender-docs` repository (or equivalent)  
**When:** After Phase 1 is complete and merged

#### Step 1: Configure dependent repositories

In the **Defender repository**, locate `.openpublishing.publish.config.json`.

Add or update the `dependent_repositories` section:
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
- Adjust the `url` if using a different repository host
- Adjust the `branch` if your default branch is not `main`
- If `dependent_repositories` already exists, add memdocs-pr to the array

#### Step 2: Reference Intune includes in Defender articles

In Defender markdown files, replace duplicated Intune procedures with cross-repo include syntax.

**Example for ASR article:**

**File:** `enable-attack-surface-reduction.md`

**Find this section:**
```markdown
## Configure ASR with Intune

1. Go to the Microsoft Intune admin center...
2. Navigate to Endpoint security...
[...full duplicated procedure...]
```

**Replace with:**
```markdown
## Configure ASR with Intune

[!INCLUDE [Create ASR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]

> [!TIP]
> After creating the policy, use the guidance below to test and validate ASR rules.
```

**Syntax rules:**
- Always use `~/memdocs-pr/` prefix for cross-repo references
- Path after `memdocs-pr/` is relative to the root of that repository
- Use forward slashes `/` even on Windows

#### Step 3: Build and validate locally

```bash
# In the Defender repository
docfx build

# Check build output for:
# - Broken include references
# - Missing content warnings
# - Link validation errors
```

#### Step 4: Common troubleshooting

| Issue | Solution |
|-------|----------|
| "Include file not found" | Verify the path is correct and the file exists in memdocs-pr |
| "Dependent repository not configured" | Add memdocs-pr to `.openpublishing.publish.config.json` |
| Content renders but looks wrong | Check heading levels in the include file |
| Relative links broken | Convert to absolute learn.microsoft.com URLs in the include |

---

### **Phase 3: Create Defender-Owned Includes (Optional Reciprocal)**

**Who:** Defender content team  
**Where:** `defender-docs` repository  
**When:** After Phase 2 is stable

#### Step 1: Create Defender includes directory
```bash
mkdir -p includes
```

#### Step 2: Create Defender-owned include files
Create:
- `includes/verify-asr-rules.md`
- `includes/verify-onboarding-status.md`

Extract content from canonical Defender articles (verification/troubleshooting sections).

#### Step 3: Configure reciprocal dependency in Intune repo

In **memdocs-pr repository**, update `.openpublishing.publish.config.json`:
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

#### Step 4: Reference Defender includes in Intune articles

In Intune articles, add post-deployment verification sections:

**Example:**
```markdown
## Verify ASR rules deployment

After creating and assigning the ASR policy in Intune, verify that rules are working as expected.

[!INCLUDE [Verify ASR rules](~/defender-docs/includes/verify-asr-rules.md)]
```

---

## Article-by-Article Edit Map

### **Intune Articles to Update**

#### Article: `endpoint-security-asr-policy.md`
**Location:** `intune/intune-service/protect/endpoint-security-asr-policy.md`

**Edit:**
1. Create include file from the "Create policy" section
2. Replace procedure with: `[!INCLUDE [Create ASR policy](../includes/endpoint-security/create-asr-policy-intune.md)]`
3. Add new section: "Validate deployment" with cross-repo include to Defender's verify-asr-rules.md (when available)

---

#### Article: `endpoint-security-edr-policy.md`
**Location:** `intune/intune-service/protect/endpoint-security-edr-policy.md`

**Edit:**
1. Create include file from deployment procedure
2. Replace procedure with: `[!INCLUDE [Deploy EDR policy](../includes/endpoint-security/create-edr-policy-intune.md)]`
3. Add new section: "Verify onboarding" linking to Defender verification guidance

---

#### Article: `endpoint-security-antivirus-policy.md`
**Location:** `intune/intune-service/protect/endpoint-security-antivirus-policy.md`

**Edit:**
1. Create include file from generic policy creation procedure
2. Replace procedure with: `[!INCLUDE [Create Antivirus policy](../includes/endpoint-security/create-antivirus-policy-intune.md)]`

---

#### Article: `endpoint-security-firewall-policy.md`
**Location:** `intune/intune-service/protect/endpoint-security-firewall-policy.md`

**Edit:**
1. Create include file from policy creation procedure
2. Replace procedure with: `[!INCLUDE [Create Firewall policy](../includes/endpoint-security/create-firewall-policy-intune.md)]`

---

### **Defender Articles to Update** (Instructions for Defender team)

#### Article: `enable-attack-surface-reduction.md`
**Location:** `defender-endpoint/enable-attack-surface-reduction.md`

**Current state:** Contains full duplicated Intune wizard steps

**Required edit:**
1. Locate the "Configure with Intune" section
2. Replace full Intune procedure with cross-repo include:
   ```markdown
   [!INCLUDE [Create ASR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]
   ```
3. Keep Defender-specific context before/after the include (exclusions guidance, method comparison, etc.)

---

#### Article: `attack-surface-reduction-rules-deployment-test.md`
**Location:** `defender-endpoint/attack-surface-reduction-rules-deployment-test.md`

**Current state:** Contains Intune policy creation steps as part of testing guidance

**Required edit:**
1. Locate any "Create policy in Intune" walkthrough
2. Replace with short bridge + cross-repo include:
   ```markdown
   ### Configure the policy
   
   [!INCLUDE [Create ASR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]
   
   After creating the policy, continue with testing guidance below.
   ```
3. Keep all testing strategy, audit mode guidance, and validation steps (this is Defender-owned unique content)

---

#### Article: `onboarding-endpoint-manager.md`
**Location:** `defender-endpoint/onboarding-endpoint-manager.md`

**Current state:** Contains full Intune EDR policy wizard steps

**Required edit:**
1. Locate the Intune EDR policy creation procedure
2. Replace with cross-repo include:
   ```markdown
   [!INCLUDE [Deploy EDR policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-edr-policy-intune.md)]
   ```
3. Keep Defender-owned content: prerequisites, onboarding package download/semantics, verification, troubleshooting

---

#### Article: `use-intune-config-manager-microsoft-defender-antivirus.md`
**Location:** `defender-endpoint/use-intune-config-manager-microsoft-defender-antivirus.md`

**Current state:** Contains generic Intune antivirus policy creation steps

**Required edit:**
1. Locate "Configure in Intune" section with wizard steps
2. Replace with cross-repo include:
   ```markdown
   [!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]
   ```
3. Keep Defender-specific content: setting behavior explanations, tamper protection notes, security guidance

---

#### Article: `configure-real-time-protection-microsoft-defender-antivirus.md`
**Location:** `defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus.md`  
**Section:** "Manage antivirus settings with Microsoft Intune"

**Current state:** Contains full Intune policy creation table

**Required edit:**
1. Locate the section heading "Manage antivirus settings with Microsoft Intune"
2. Replace the detailed procedure table with cross-repo include:
   ```markdown
   ## Manage antivirus settings with Microsoft Intune
   
   [!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]
   ```
3. Keep any real-time protection-specific setting notes

---

#### Article: `enable-cloud-protection-microsoft-defender-antivirus.md`
**Location:** `defender-endpoint/enable-cloud-protection-microsoft-defender-antivirus.md`  
**Section:** "Use Microsoft Intune to turn on cloud protection"

**Current state:** Contains Intune policy creation with specific settings callouts

**Required edit:**
1. Keep scenario-specific intro and setting callouts ("Allow Cloud Protection", "Submit Samples Consent")
2. Replace generic wizard steps with cross-repo include:
   ```markdown
   To configure these settings using Intune:
   
   [!INCLUDE [Create Antivirus policy in Intune](~/memdocs-pr/intune/includes/endpoint-security/create-antivirus-policy-intune.md)]
   
   When configuring settings in the policy:
   - Set **Allow Cloud Protection** to **Allowed**
   - Set **Submit Samples Consent** to **Send safe samples automatically** or **Send all samples automatically**
   ```

---

#### Article: `manage-security-policies.md`
**Location:** `defender-endpoint/manage-security-policies.md`

**Current state:** Describes endpoint security policy types and portal UX

**Required edit (light touch):**
1. Keep Defender portal navigation and permissions guidance
2. If the article currently contains detailed Intune configuration steps for any policy type, replace with:
   ```markdown
   For detailed configuration guidance for each policy type, see:
   - Firewall: [Firewall policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-firewall-policy)
   - Antivirus: [Antivirus policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy)
   - ASR: [Attack surface reduction policy in Intune](https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-asr-policy)
   ```

---

## Content Extraction Guidelines

### What to Include in the Include File

✅ **Include:**
- Step-by-step wizard navigation
- UI element names (exactly as they appear)
- Required vs optional steps
- Default values/recommendations
- Screenshots (if they add critical clarity)
- Links to related conceptual content

❌ **Exclude:**
- Product-specific intro/rationale (keep in consuming article)
- "Why you'd use this" (keep in consuming article)
- Prerequisites unique to one scenario (keep in consuming article)
- Post-deployment validation (unless it's Intune-specific; otherwise link to Defender)

### Include File Best Practices

1. **Start with a heading:**
   ```markdown
   ## Create [Policy Type] policy in Intune
   ```

2. **Use numbered steps:**
   ```markdown
   1. Sign in to the [Microsoft Intune admin center](https://intune.microsoft.com).
   2. Go to **Endpoint security** > **Antivirus** > **Create policy**.
   ```

3. **Be explicit about UI elements:**
   - Use **bold** for exact UI strings: **Create policy**, **Assignments**, **Next**
   - Use italics for user input: *Enter a name for the policy*

4. **Include terminal conditions:**
   ```markdown
   6. Select **Review + create** > **Create**. The policy appears in the policy list.
   ```

5. **Add links to deep-dive content:**
   ```markdown
   For detailed setting descriptions, see [Setting reference](link).
   ```

6. **Keep it version-agnostic:**
   - Avoid "In version X.Y.Z, this changed to..."
   - If version-specific nuances exist, note them but keep the core procedure generic

---

## Rollout Timeline

### Week 1-2: Intune Implementation
- Create `intune/includes/endpoint-security/` directory
- Extract content from 4 canonical Intune articles into include files
- Update Intune articles to reference includes (same-repo)
- Test local build
- Submit PR for Intune repository

### Week 3: Defender Configuration
- Merge Intune PR (makes includes available)
- Defender team: Configure `dependent_repositories` in `.openpublishing.publish.config.json`
- Test cross-repo include resolution in Defender build

### Week 4-5: Defender Article Updates
- Update Defender articles to reference Intune includes (cross-repo syntax)
- Remove duplicated Intune procedures
- Test build and validate all links
- Submit PR for Defender repository

### Week 6: Reciprocal Validation (Optional)
- Defender team: Create Defender-owned includes (verify-asr-rules.md, verify-onboarding-status.md)
- Intune team: Configure reciprocal dependency on defender-docs
- Intune team: Add validation sections referencing Defender includes

---

## Validation Checklist

### Before Merging Intune PR
- [ ] All 4 include files created in correct location
- [ ] Each include is self-contained and renders correctly in isolation
- [ ] Intune articles correctly reference includes using relative paths
- [ ] Local build succeeds with no warnings
- [ ] Manual review: each consuming article flows naturally with the include
- [ ] Links within includes are valid (relative or absolute)

### Before Merging Defender PR
- [ ] `dependent_repositories` configured in Defender `.openpublishing.publish.config.json`
- [ ] Cross-repo include syntax is correct (`~/memdocs-pr/...`)
- [ ] Each Defender article retains unique Defender-owned context
- [ ] Local build succeeds and includes render correctly
- [ ] Manual review: flow between Defender context and Intune include is natural
- [ ] All removed content is truly duplicative (no unique Defender steps lost)

### Post-Merge Monitoring
- [ ] Published pages render correctly on learn.microsoft.com
- [ ] No broken links or missing content errors
- [ ] Cross-repo includes display properly (not raw include syntax)
- [ ] Reader feedback: articles still make sense and are complete

---

## Maintenance Notes

### When Intune UI Changes
- **Who updates:** Intune content team
- **Where:** Update the canonical include file in `intune/includes/endpoint-security/`
- **Propagation:** Changes automatically appear in all Defender articles that reference the include (no action needed from Defender team)

### When Defender Guidance Changes
- **Who updates:** Defender content team
- **Where:** Update Defender-owned content surrounding the include
- **Note:** Do not modify the include; it's Intune-owned

### Include File Versioning
- If a procedure changes significantly and old/new versions must coexist temporarily:
  - Create a new include file with a version suffix: `create-asr-policy-intune-v2.md`
  - Update consuming articles to reference the appropriate version
  - Deprecate the old include once all content migrates

---

## FAQ

**Q: What if the Intune procedure is slightly different for Defender scenarios?**  
**A:** Keep the include generic; add Defender-specific variations as notes *around* the include in the Defender article.

**Q: Can we use includes for conceptual content, not just procedures?**  
**A:** Yes, but use sparingly. Concepts often need product-specific framing. Includes work best for "objective truth" content (procedures, settings definitions, prerequisite lists).

**Q: What if the Defender repository is on a different branch cadence?**  
**A:** The `dependent_repositories` configuration specifies the branch. You can pin to `main` or a specific release branch. Coordinate with both teams on branch strategy.

**Q: Can we nest includes (include within an include)?**  
**A:** Technically yes, but avoid it—it makes maintenance complex and builds slower. If you need nested content, consider restructuring.

**Q: What about localization?**  
**A:** The localization system handles cross-repo includes correctly. The English include file will be localized once, and all consuming articles (Intune and Defender) will get the localized version.

**Q: How do we handle broken cross-repo includes during outages?**  
**A:** If the dependent repository is temporarily unavailable during build, the build will fail. This is correct behavior—it prevents publishing incomplete content. Coordinate deployment windows with both teams.

---

## Success Criteria

### Short-term (3 months)
- [ ] Zero duplicated Intune procedures in Defender docs
- [ ] All cross-repo includes rendering correctly in production
- [ ] Maintenance burden reduced (measure: time to update ASR procedure across both doc sets)

### Long-term (6-12 months)
- [ ] Content drift eliminated (audit: check for any reintroduced duplication)
- [ ] Reader feedback: articles remain clear and complete
- [ ] Establish pattern for future cross-product features (apply to new overlaps as they arise)

---

## Contact & Ownership

**Intune Content Team:**
- Responsible for: Creating and maintaining Intune-owned include files
- Responsible for: Reviewing Defender PRs that add references to Intune includes

**Defender Content Team:**
- Responsible for: Configuring cross-repo dependencies in Defender repository
- Responsible for: Updating Defender articles to reference Intune includes
- Responsible for: Creating and maintaining Defender-owned include files (verification/troubleshooting)

**Coordination:**
- Schedule monthly sync to review include file health
- Notify the other team when major UI/procedure changes are coming
- Share PR links when cross-repo includes are added/modified

---

## Appendix: Technical Reference

### Cross-Repo Include Syntax
```markdown
[!INCLUDE [Display text](~/repository-name/path/to/file.md)]
```

**Components:**
- `~/` = root of the dependent repository
- `repository-name` = the `path_to_root` value from `.openpublishing.publish.config.json`
- `path/to/file.md` = path relative to repository root

**Example:**
```markdown
[!INCLUDE [Create ASR policy](~/memdocs-pr/intune/includes/endpoint-security/create-asr-policy-intune.md)]
```

### Dependent Repository Configuration
**File:** `.openpublishing.publish.config.json`

```json
{
  "dependent_repositories": [
    {
      "path_to_root": "memdocs-pr",
      "url": "https://github.com/MicrosoftDocs/memdocs-pr",
      "branch": "main",
      "branch_mapping": {}
    }
  ]
}
```

**Parameters:**
- `path_to_root`: Logical name used in include syntax
- `url`: GitHub repository URL
- `branch`: Default branch to pull includes from
- `branch_mapping`: (Optional) Map local branches to different dependent branches

---

**End of Document**
