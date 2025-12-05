---
title: Step 8. Troubleshoot Microsoft Edge for Business Data Security
description: Step 8. Troubleshoot Microsoft Edge for Business corporate data security in Microsoft Intune.
ms.date: 12/05/2025
ms.topic: troubleshooting
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 8. Troubleshoot Microsoft Edge for Business Data Security

Troubleshooting app protection policies and app configuration policies (ACP) in Microsoft Intune can involve several different checks. This section consolidates the most common issues and resolutions so that you can quickly diagnose problems and restore your secure enterprise browser experience.

Successful app protection policy deployment relies on correct assignments, policy configuration, and platform dependencies. Use these quick checks before diving deeper into troubleshooting.

## Quick checks

Use this list when users report issues with Microsoft Edge for Business:

- **Verify policy assignment**  
  Ensure that app protection policies and app configuration policies are assigned to the correct user or device groups, and that Microsoft Edge for Business is in scope for those assignments.

- **Review policy settings**  
  Confirm that the required settings for the selected security level are properly defined. Misconfigured data-transfer, clipboard, or sign-in settings often cause issues.

- **Check Microsoft Edge version and OS support**  
  When Microsoft Edge crashes at launch or policies don't appear to apply, verify that both the OS version and Microsoft Edge version meet the minimum supported requirements.

- **Validate user sign-in**  
  App protection policies only apply when a user signs into Microsoft Edge for Business using their Microsoft Entra ID work account. Personal or local accounts won't receive policy enforcement.

- **Understand unmanaged share behavior**  
  On mobile devices, the system share extension can bypass some restrictions unless the device is managed. In these situations, Intune encrypts corporate data before it leaves the app.

- **Check app requirements**
  - **Microsoft Authenticator** is required when App-based Conditional Access is enabled.
  - **Company Portal (Android)** is required for APP enforcement even if the device isn't enrolled.

- **Confirm the configuration channel**  
  If ACP settings aren't applying, verify that you're using the correct configuration channel (managed apps vs. managed devices) and that identifiers, configuration keys, and JSON syntax match publisher documentation.

- **“Sign in with your work account” message**  
  This usually appears when the user signed in using an account that isn't targeted by the app protection policy or when the enrollment method doesn’t match what the policy requires.

## Policy deployment issues

### Settings Catalog policies not applying

- **Likely cause:** Device enrollment or sync issues  
- **How to fix:**
  - Verify device enrollment status and force sync from Company Portal

### App protection policies not enforcing

- **Likely cause:** User is signed into Edge with a personal profile  
- **How to fix:**
  - Confirm user signed into Edge with Entra ID account

### App configuration policies showing as failed

- **Likely cause:** JSON syntax errors or invalid configuration values  
- **How to fix:**
  - Validate JSON configuration syntax and policy values

### Conditional Access blocking unexpectedly

- **Likely cause:** Device compliance evaluation failure  
- **How to fix:**
  - Check device compliance status and reevaluate policies

### Policy conflicts between security levels

- **Likely cause:** Users or devices receiving multiple overlapping level assignments  
- **How to fix:**
  - Review group membership and policy assignments for overlaps

## Platform-specific issues

### Windows: Edge security baseline not applying

- **Likely cause:** Unsupported Windows build or Microsoft Edge version  
- **How to fix:**
  - Confirm the device is on a supported Windows 11 build.

### Windows: Application Guard not working

- **Likely cause:** Feature not enabled or missing virtualization support  
- **How to fix:**
  - Enable Windows Defender Application Guard.

### iOS/Android: APP policies not enforcing on BYOD

- **Likely cause:** User not enrolled in MAM or hasn’t completed the Company Portal/Authenticator flow  
- **How to fix:**
  - Guide the user through MAM enrollment.

### iOS/Android: ACP settings not applying

- **Likely cause:** Outdated Edge mobile app  
- **How to fix:**
  - Update to the latest Microsoft Edge mobile version.

### macOS: Settings Catalog policies failing

- **Likely cause:** macOS version below minimum requirements  
- **How to fix:**
  - Verify minimum supported macOS versions for the targeted policies.

## User experience issues

### Users at Level 3 reporting blocked websites

- **Likely cause:** Restrictive URL filtering  
- **Recommended action:** Review and expand allowed URLs through change process

### Mobile users unable to copy/paste

- **Likely cause:** App Protection Policy restrictions  
- **Recommended action:** Validate policy settings match intended restrictions

### Authentication prompts too frequent

- **Likely cause:** Aggressive Conditional Access settings  
- **Recommended action:** Review session timeout and reauthentication policies

### Features missing or disabled

- **Likely cause:** Level 3 feature restrictions  
- **Recommended action:** Confirm user assigned to correct security level group

## Advanced troubleshooting

### Policy conflicts

- **Diagnostic steps:**  
  1. Export current policies  
  2. Compare overlapping settings  
  3. Identify conflicting values  
- **Resolution path:**
  - Consolidate policies or adjust priority assignments

### Performance issues

- **Diagnostic steps:**  
  1. Check device resources  
  2. Review policy complexity  
  3. Monitor network latency  
- **Resolution path:**
  - Optimize policy scope and reduce setting conflicts

### Compliance gaps

- **Diagnostic steps:**  
  1. Run SCAP validation  
  2. Compare against framework requirements  
  3. Document exceptions  
- **Resolution path:**
  - Update policies to address gaps or document approved exceptions

## FAQ

**Does Microsoft Edge for Business require a separate download?**  
No. Microsoft Edge for Business is automatically triggered when a user signs in with a Microsoft Entra ID account.

**Is Windows Home edition supported for MAM for Windows?**  
Yes. MAM for Windows supports Windows Home edition.

**Will all policies and configurations previously set by IT be applied to Edge for Business?**  
Yes. Existing policies targeting Microsoft Edge are inherited when users sign in with their work profile.

**What effect does this have on users’ default browser settings?**  
There's no change to a user’s default browser settings.

**What happens to passwords, favorites, and related data?**  
Passwords, favorites, and browsing data in the work profile are preserved. Personal and work windows remain separated.

**How do MAM for Windows and Microsoft Edge management service differ?**  
If you use Intune, create app protection and app configuration policies to configure Microsoft Edge for Business.  
If you don't use Intune, use the Microsoft Edge management service.  
For more information, see: <https://aka.ms/EdgeSecurityWhitepaper>.

## Solution results

After completing this solution, you will:

- Configure Microsoft Edge for Business and Microsoft Application Management across multiple scenarios.
- Understand the app protection policy framework and how it strengthens data security.
- Implement Intune encryption and password single sign-on.
- Build a secure app configuration baseline.
- Configure Conditional Access policies for your organization.
- Understand the end-user experience after policy deployment.
- Apply troubleshooting patterns identified during Microsoft research and customer feedback.

> [!IMPORTANT]
> Security is a continuous process. Review and adjust your configurations as threats and requirements evolve.

Continue applying these strategies and patterns to strengthen and refine your secure enterprise browser deployment.
