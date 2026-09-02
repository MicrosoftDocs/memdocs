---
title: Integrate Windows Update client policies
titleSuffix: Configuration Manager
description: Use Configuration Manager together with Windows Update client policies (formerly Windows Update for Business). Understand co-management scenarios, scan source policies, common pitfalls, and how to troubleshoot update source problems.
ms.date: 08/31/2026
ms.service: configuration-manager
ms.subservice: software-updates
ms.topic: how-to
author: sccmavenger
ms.author: dannygu
manager: laurawi
ms.reviewer:
  - umaikhan
  - brianhun
  - payur
  - hugowu
  - qiani
ms.collection: tier3
appliesto:
  - ✅ Configuration Manager (current branch)
---

# Integrate Windows Update client policies with Configuration Manager

> [!TIP]
> **Windows Update for Business** is the former brand name for the **Windows Update client policies** feature, and still appears in some Windows documentation. It isn't the same thing as **Dual Scan**, which is a separate legacy client behavior (described later in this article) where a device scans Windows Update directly for OS updates even while WSUS is configured.

Windows Update client policies keep Windows 10 and later devices up-to-date with security defenses and feature updates when they scan directly against the Windows Update (WU) service. Configuration Manager can differentiate between devices that use Windows Update client policies and devices that use Windows Server Update Services (WSUS), and works alongside Microsoft Intune when devices are co-managed.

Integrating Windows Update client policies with Configuration Manager means the device gets its Windows (OS) updates directly from the Windows Update service instead of from Configuration Manager. This direct-scan behavior is provided by the Windows Update client policies feature. On Windows 10 and Windows Server 2022, it's enabled through the legacy Dual Scan mechanism.

While a device is in this state, those Windows updates report as **Unknown** in Configuration Manager, and aren't counted toward the overall compliance percentage, because Configuration Manager isn't aware of the updates that Windows Update delivers.

> [!NOTE]
> The exact compliance state depends on whether Configuration Manager still scans those updates. If the Windows updates are filtered out of the Configuration Manager scan, they show as **Unknown** and aren't counted. If Configuration Manager still scans them and finds them already installed or not applicable, they can instead show as **Compliant** or **Not Required**.

This article covers how Configuration Manager interacts with Windows Update client policies, what happens when co-management workloads move between Configuration Manager and Intune, how the Windows scan source policies affect update behavior, and how to troubleshoot when devices don't scan against the source you expect.

For the Windows-side reference on the scan source policy, see [Use Windows Update client policies and Windows Server Update Services (WSUS) together](/windows/deployment/update/wufb-wsus).

> [!WARNING]
> If you're using co-management and you've moved the [Windows Update policies](../../comanage/workloads.md#windows-update-policies) workload to Intune, your devices get their [Windows Update client policies from Intune](/mem/intune-service/protect/windows-update-for-business-configure). The Configuration Manager slider position doesn't automatically clean up the policy settings that Intune, or another authority, previously wrote to the device. See [Co-management with Microsoft Intune](#co-management-with-microsoft-intune).

## Configuration Manager features affected when clients get updates from Windows Update

Some Configuration Manager features aren't available when clients are configured to receive updates from Windows Update, which includes Windows Update client policies or Windows Insider builds:

- **Software update compliance reporting**:

  - Configuration Manager isn't aware of the updates that are published to Windows Update. Clients that are configured to receive updates from Windows Update display **Unknown** for those updates in the Configuration Manager console.
  - Troubleshooting overall compliance status is harder, because **Unknown** status previously applied only to clients that hadn't reported scan status back from WSUS. It now also includes clients that receive updates from Windows Update.
  - Definition update compliance is part of overall update compliance reporting, and doesn't work as expected either.

- **Endpoint Protection reporting** for Microsoft Defender that's based on update compliance status doesn't return accurate results, because of the missing scan data.

- **Microsoft app updates**: Configuration Manager can't deploy or report compliance on Microsoft app updates for clients that use Windows Update client policies to receive updates. This limitation includes updates for Microsoft 365 Apps, Internet Explorer, Microsoft Edge, and Visual Studio.

- **Third-party updates**: Configuration Manager can still deploy third-party updates that are published to WSUS and managed through Configuration Manager. If you don't want any third-party updates installed on clients that use Windows Update client policies, disable the [Enable software updates on clients](../../core/clients/deploy/about-client-settings.md#software-updates) client setting.

- **Client deployment**: Configuration Manager full client deployment that uses the software updates infrastructure doesn't work for clients that use Windows Update client policies to receive updates.

## Windows Update scan source policies

The **scan source policy** lets Windows choose, per update category (Driver, Feature, Quality, Other), whether to fetch that category from WSUS or from Windows Update. Its Group Policy name is **Specify source service for specific classes of Windows Updates**.

It supersedes the older Dual Scan behavior on Windows 11 and Windows Server 2025. On Windows 10 and Windows Server 2022, it works alongside Dual Scan, which still gates it. For the general Windows documentation, see [Use Windows Update client policies and Windows Server Update Services (WSUS) together](/windows/deployment/update/wufb-wsus).

### The scan source primary switch

For any per-category scan source value to take effect, this primary switch must be present and set to `1`, under the `\AU` subkey:

`HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseUpdateClassPolicySource = 1`

If the value is placed anywhere other than `\AU`, the Windows Update agent ignores it. See [Pitfall - UseUpdateClassPolicySource at the wrong path](#pitfall---useupdateclasspolicysource-at-the-wrong-path).

The four category values live under `HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate`:

- `SetPolicyDrivenUpdateSourceForDriverUpdates`
- `SetPolicyDrivenUpdateSourceForFeatureUpdates`
- `SetPolicyDrivenUpdateSourceForOtherUpdates`
- `SetPolicyDrivenUpdateSourceForQualityUpdates`

Each category value takes one of the following values:

- `1` - get this category from WSUS.
- `0` - get this category from Windows Update / Windows Update client policies.

> [!IMPORTANT]
> If you configure the scan source policy, configure all four category values. Windows Update doesn't support a partial configuration. For more information, see [Pitfall - Partial scan source configuration](#pitfall---partial-scan-source-configuration).

### Behavior on Windows 10

On Windows 10, the legacy Dual Scan switch (`DisableDualScan`) still gates whether the scan source policies actually retrieve updates from Windows Update. The following table uses Feature Updates (FU) and Quality Updates (QU) as an example.

| WSUS configured | DisableDualScan | Scan source policy for FU/QU | Behavior |
|---|---|---|---|
| Yes | `1` (enabled) | Set to Windows Update | Gets the FU/QU from WSUS |
| Yes | Not configured | Set to Windows Update | Gets the FU/QU from Windows Update |
| Yes | Not configured | Set to WSUS | Gets the FU/QU from WSUS |
| Yes | `0` (disabled) | Set to WSUS | Gets the FU/QU from WSUS |

> [!IMPORTANT]
> On Windows 10, `DisableDualScan` is the switch that controls whether the scan source policies can retrieve updates from Windows Update. Pointing a category at Windows Update is itself what turns on the dual-scan channel the client uses to reach Windows Update, so no separate deferral policy is required.
>
> If you also enable `DisableDualScan`, that channel is severed: in-catalog Feature and Quality updates fall back to WSUS, and Windows Update-only content (Features on Demand, RSAT, optional features, language packs) fails to install. Don't enable `DisableDualScan` for a category that you point at Windows Update.
>
> On devices historically managed by Configuration Manager, `DisableDualScan = 1` is often already present because earlier Configuration Manager versions set it. That's why scan source policies can appear to have no effect until you remove that value.

> [!NOTE]
> Windows Server 2022 follows the Windows 10 behavior. `DisableDualScan` is honored, and gates whether the scan source policies retrieve updates from Windows Update.
>
> The scan source policies require Windows 10, version 2004 or later, or Windows Server 2022. On Windows Server 2016 and Windows Server 2019, they don't apply at all, and only `DisableDualScan` governs whether the client uses WSUS for Windows updates.
>
> Windows Server 2022 is build 20348, part of the Windows 10 servicing generation, below the Windows 11 build 22000 boundary where `DisableDualScan` became inert. Windows Server 2025 (build 26100) follows the Windows 11 behavior, where `DisableDualScan` has no effect.

#### Feature and Quality update source at a glance

| WSUS wired | Deferral policy or scan source = Windows Update | Operating system | Feature/Quality source |
|---|---|---|---|
| Yes | No | Any | WSUS |
| Yes | Yes | Windows 10, `DisableDualScan` not `1` | Windows Update (Dual Scan) |
| Yes | Yes | Windows 10, `DisableDualScan = 1` | WSUS for in-catalog updates. Windows Update-only content, such as Features on Demand, fails |
| Yes | Yes | Windows 11 or Windows Server 2025 | Windows Update (Dual Scan). The switch is inert |

Drivers and third-party content are never part of this reroute. They stay on WSUS unless you separately point them at Windows Update.

> [!TIP]
> **Keep Features on Demand, optional features, and language packs installable from the Windows UI even when WSUS is your update source.**
>
> A common admin request is for users to still be able to install optional features from **Settings** > **Optional features** on WSUS-managed devices. The following combination lets Features on Demand and language packs flow from Windows Update while WSUS continues to own feature and quality updates:
>
> - **WSUS server policy**: configured (`UseWUServer`, `WUServer`).
> - **DisableDualScan**: any value works (`0`, `1`, or not configured).
> - **Scan source policy**: not configured, or not configured for the Quality Updates category, because Features on Demand are treated as Quality Updates for scan source purposes.
> - **Specify settings for optional component installation and component repair**: on Windows 10 (non-UUP servicing), configure it to allow Windows Update as the source repository. On UUP-based builds (Windows 11 and later, and Windows Server 2025), leave this policy **Not Configured**. The OS sources optional content from Windows Update by default, and configuring it can interfere with UUP acquisition.
>
> For the full policy configuration, see [How to make Features on Demand and language packs available when you're using WSUS or Configuration Manager](/windows/deployment/update/fod-and-lang-packs).

### Behavior on Windows 11

On Windows 11, `DisableDualScan` has no effect. Only the WSUS configuration and the scan source policy matter:

| WSUS policy configuration | Windows Update client policies configured | Scan source policy | Update behavior |
|---|---|---|---|
| WSUS configured (`UseWUServer`, `WUServer`) | Not configured | Not configured | Updates from WSUS |
| WSUS configured (`UseWUServer`, `WUServer`) | Configured | Not configured | Updates from Windows Update |
| WSUS configured (`UseWUServer`, `WUServer`) | Configured | Configured | Updates from whichever source the scan source policy specifies, per category |

### What Configuration Manager does with scan source policies today

On Configuration Manager version 2503 with update rollup 32851084, or version 2509, with [KB 36495448](../../hotfix/2509/36495448.md) installed, Configuration Manager doesn't set or remove any of the four `SetPolicyDrivenUpdateSourceFor*` values, and doesn't set `UseUpdateClassPolicySource`. You own these settings, through Group Policy or Intune Windows Update client policies.

If you're upgrading from an earlier build, existing devices that were left in a partial scan source state by prior Configuration Manager versions have those partial values cleaned up once by the client. A one-time flag, `HKLM\SOFTWARE\Microsoft\CCM\SoftwareUpdates\isScanSourcePolicyRemoved2`, is set to prevent the cleanup from running again.

For the full version-by-version history of how Configuration Manager has managed scan source policies over time, see [Appendix: Configuration Manager version history for scan source policies](#appendix-configuration-manager-version-history-for-scan-source-policies).

## Co-management with Microsoft Intune

Co-managed devices are managed by both Configuration Manager and Intune. The [Windows Update policies](../../comanage/workloads.md#windows-update-policies) co-management workload slider determines which authority controls Windows updates.

### The Windows Update policies workload slider

The **Windows Update policies** workload has three positions in the Configuration Manager console: **Configuration Manager**, **Pilot Intune**, and **Intune**. The device's effective co-management capabilities value reflects the slider position. For example, `8197` means Configuration Manager owns updates, and `8213` means Intune owns updates.

| Slider position | Who delivers Windows updates | Who delivers third-party updates (if enabled) |
|---|---|---|
| Configuration Manager | Configuration Manager (WSUS) | Configuration Manager |
| Pilot Intune (piloted collection only) | Intune (Windows Update client policies) | Configuration Manager |
| Intune | Intune (Windows Update client policies) | Configuration Manager |

> [!IMPORTANT]
> Starting with Configuration Manager 2503 HFRU and 2509, once [KB 36495448](../../hotfix/2509/36495448.md) is applied, the Configuration Manager client no longer sets or removes Windows Update scan source policies. Ownership of these settings is now yours, through Group Policy or Intune Windows Update client policies.
>
> The slider position tells Configuration Manager how to behave, but it doesn't automatically clean up the policy settings that another authority, for example Intune, previously wrote to the device. See [Pitfall - The co-management slider isn't authoritative](#pitfall---the-co-management-slider-isnt-authoritative) for how to verify what's actually in effect on a device.

> [!NOTE]
> The **Windows Update policies** workload slider governs only Windows updates. Configuration Manager keeps delivering third-party updates as long as the [Software Updates](../../core/clients/deploy/about-client-settings.md#software-updates) client setting stays enabled (**Yes**). Set that client setting to **No** only for Windows Autopatch, which requires Configuration Manager to be out of the update path entirely.

### Moving the workload back to Configuration Manager

When you move the **Windows Update policies** workload from Intune back to Configuration Manager, the Intune-authored Windows Update client policy state on the device isn't automatically removed. Devices might continue to scan against Windows Update or Microsoft Update instead of WSUS.

- **Symptom**: After the slider is moved back to Configuration Manager and a machine policy cycle is complete, the device still scans against Windows Update or Microsoft Update instead of WSUS. Confirm this per update category (Driver, Feature, Quality, Other) rather than relying on `IsDefaultAUService`, which reports only a single default service and is unreliable once scan source policies are configured. For more information, see [Troubleshoot](#troubleshoot).

- **Cause**: The MDM Update CSP state under `HKLM\SOFTWARE\Microsoft\PolicyManager\current\device\Update` persists after the Intune assignment is revoked. Before KB 36495448, this behavior was masked because Configuration Manager overwrote scan source policies on every policy cycle.

- **Applies to**: Configuration Manager 2503 HFRU and 2509 with KB 36495448 installed, and later releases that inherit this behavior.

- **Resolution**: See [Clean up after moving the workload back to Configuration Manager](#clean-up-after-moving-the-workload-back-to-configuration-manager). As a best practice, remove or reassign the device's Intune Windows Update client policy assignment before you flip the workload slider. Alternatively, point the affected categories back to WSUS with the scan source policy to override the residual Intune state.

## Common scenarios

### Scenario 1 - Configuration Manager manages all updates (no co-management)

- **Slider**: Not applicable, because the device isn't co-managed, or set to **Configuration Manager**.
- **Setup**: Configuration Manager is configured with a software update point (SUP) backed by WSUS. **Client Settings** > **Software Updates** is enabled.
- **Windows Update scan source policies**: Leave them unconfigured, or set all four to `1` through Group Policy with `UseUpdateClassPolicySource = 1` under `\AU` for defense in depth.
- **Result**: All updates flow from WSUS. Configuration Manager reports compliance normally.

### Scenario 2 - Co-management, Intune manages Windows updates

- **Slider**: **Pilot Intune** or **Intune**.
- **Setup**: Intune Windows Update client policies, such as feature update profiles, quality update profiles, and update rings, are assigned to the device.
- **Windows Update scan source policies**: Managed by Intune Windows Update client policies. Don't also configure these values through Group Policy. You create a configuration pitfall if the two authorities disagree.
- **Result**: Windows updates flow from Windows Update. Configuration Manager compliance for those updates shows **Unknown**, because Configuration Manager isn't aware of updates delivered by Windows Update. Devices managed this way appear as **Unknown** in software update compliance reports, and aren't counted toward the overall compliance percentage. See [Identify clients that use Windows Update client policies for Windows updates](#identify-clients-that-use-windows-update-client-policies-for-windows-updates).

Per class, this routing is governed by the Intune enrollment rather than by a scan source policy, and no Group Policy gate applies:

| Update class | Source |
|---|---|
| Feature | Windows Update |
| Quality | Windows Update |
| Driver | Windows Update, or WSUS when drivers are excluded in the Intune configuration |

To confirm the effective per-category source on a device, check the resolved policy state. For more information, see [Determine the effective update authority per update category](#1-determine-the-effective-update-authority-per-update-category).

### Scenario 3a - Co-management with third-party updates in Configuration Manager, before KB 36495448

> [!WARNING]
> If your Configuration Manager site is on 2503 HFRU or 2509 and you use this scenario, install [KB 36495448](../../hotfix/2509/36495448.md). Without the hotfix, Configuration Manager sets a partial scan source configuration that can silently redirect Feature and Quality updates to WSUS.

- **Slider**: **Intune** for the Windows Update policies workload.
- **Third-party updates**: Enabled in **Client Settings** > **Software Updates** > [Enable third-party software updates](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates), delivered through WSUS and Configuration Manager.
- **Client behavior (defect)**: Configuration Manager writes only two scan source values:

  - `HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseUpdateClassPolicySource = 1`
  - `HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\SetPolicyDrivenUpdateSourceForOtherUpdates = 1`

  The other three category values (Driver, Feature, Quality) aren't set, and are removed if they exist.

- **Impact**: Windows Update doesn't support partial scan source configurations. The Windows Update agent might assume all categories should follow the same source, so Feature Updates and Quality Updates that you intended to come from Intune are silently redirected to WSUS and Configuration Manager.
- **How to detect**: In the resolved policy state, the gate is on, but `SetPolicyDrivenUpdateSourceForFeatureUpdates` and `SetPolicyDrivenUpdateSourceForQualityUpdates` are absent. For more information, see [Determine the effective update authority per update category](#1-determine-the-effective-update-authority-per-update-category).
- **Fix**: Install [KB 36495448](../../hotfix/2509/36495448.md), which moves the device into Scenario 3b.

### Scenario 3b - Co-management with third-party updates in Configuration Manager, with KB 36495448 installed

- **Slider**: **Intune** for the Windows Update policies workload.
- **Third-party updates**: Enabled in Configuration Manager, delivered through WSUS and Configuration Manager.
- **Windows Update scan source policies**: Configuration Manager doesn't set or remove any scan source values. Any partial state left over from Scenario 3a is cleaned up once, and `HKLM\SOFTWARE\Microsoft\CCM\SoftwareUpdates\isScanSourcePolicyRemoved2` is set to `1` to prevent repeated cleanup.
- **Result**: Feature and Quality updates come from Intune, as intended. Drivers come from Intune or WSUS per your Intune configuration. Third-party updates continue to flow from Configuration Manager, because they don't depend on scan source policies.
- **Recommendation**: For finer control per update category, configure the scan source policy explicitly through Intune Windows Update client policies or Group Policy. Make sure that you set all four category values, to avoid recreating the partial-configuration pitfall.

### Scenario 4 - Moving the workload back from Intune to Configuration Manager

- **Slider**: Moved from **Intune** to **Configuration Manager**.
- **What happens**: Configuration Manager begins delivering updates through its SUP and WSUS again, but the Intune-authored Windows Update client policy state under `HKLM\SOFTWARE\Microsoft\PolicyManager\current\device\Update` isn't removed. The Windows Update agent still honors it.
- **Result**: Devices continue to scan against Windows Update. See [Clean up after moving the workload back to Configuration Manager](#clean-up-after-moving-the-workload-back-to-configuration-manager).
- **What to check**: Verify per class (Feature, Quality, Driver) in the [resolved policy state](#1-determine-the-effective-update-authority-per-update-category), rather than using `IsDefaultAUService`, which reports only one default service. On Windows 10, you can force WSUS-only with `DisableDualScan = 1`. On Windows 11 and Windows Server 2025, that switch is inert, so you must remove the residual Intune deferral or enrollment.

### Scenario 5 - Newly provisioned co-managed device

- **Provisioning**: Windows Autopilot or a Windows PE task sequence hands off to Intune and Configuration Manager enrollment.
- **Behavior**: If Intune already assigned Windows Update client policies before Configuration Manager arrives, which is common with Autopilot, the device receives Windows updates from Intune from the start. Configuration Manager with KB 36495448 installed doesn't try to change scan source policies, so the initial Intune configuration stays authoritative.
- **What to check**: Confirm the effective scan source with the [Troubleshoot](#troubleshoot) checks before you deploy software update deployments from Configuration Manager to the device.

> [!NOTE]
> Using Windows Autopatch? Autopatch requires the **Windows Update policies** workload to be on Intune, and the Configuration Manager software update client setting to be **No** on those devices. For more information, see [Windows Autopatch prerequisites](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites) and [Co-management workloads](../../comanage/workloads.md#windows-update-policies).

### Scenario 6 - Unintentional Dual Scan

This scenario covers WSUS being wired alongside a leftover deferral from Windows Update client policies, with no Intune involved.

- **Setup**: WSUS is configured (`UseWUServer = 1`), and a leftover deferral from Windows Update client policies, or a scan source value of Windows Update, is present, with no Intune management of Windows updates.
- **Result**: Feature and Quality updates move to Windows Update through Dual Scan, while drivers and third-party content stay on WSUS, even though nobody is deliberately managing Windows Update client policies. This is the common unintentional Dual Scan pattern.
- **Fix**: Remove the stray defer and pause values, and any scan source value set to Windows Update. On Windows 10, `DisableDualScan = 1` also forces WSUS-only. On Windows 11 and Windows Server 2025, that switch is inert, so you must remove the deferral itself.

### Scenario 7 - Deliberate scan source split

- **Setup**: You intentionally route classes with the scan source policy. For example, Feature and Quality updates to Windows Update, and Driver updates to WSUS, through Group Policy or Intune Windows Update client policies.
- **Configuration**: Set all four category values, plus the gate (`UseUpdateClassPolicySource = 1` under `\AU` for the Group Policy path). A partial set recreates the Scenario 3a pitfall.
- **Result**: Each class scans the source that you selected. Verify the effective routing in the [resolved policy state](#1-determine-the-effective-update-authority-per-update-category).

## Common pitfalls and gotchas

### Pitfall - Partial scan source configuration

Windows Update doesn't support setting only some of the four `SetPolicyDrivenUpdateSourceFor*` values. If any are missing while `UseUpdateClassPolicySource = 1`, the Windows Update agent might treat all categories as if they follow the same source. This behavior silently redirects Feature and Quality updates that you didn't intend to move.

- **How to detect**: Run the category values inspection under [Troubleshoot](#troubleshoot). If some values are set and others aren't, that's a partial configuration.
- **Fix**: Always configure all four values together, Driver, Feature, Quality, and Other, plus `UseUpdateClassPolicySource = 1` at the `\AU` subkey.

### Pitfall - UseUpdateClassPolicySource at the wrong path

The primary switch must be at:

`HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseUpdateClassPolicySource`

It must not be at the following path, where it's ignored:

`HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\UseUpdateClassPolicySource`

The Configuration Manager 2409 and 2503 RTM defect wrote to the wrong path. Clients with KB 36495448 installed remove the wrong-path value automatically, but if you're inspecting a device manually, always check both locations.

### Pitfall - Windows Update-only content fails when categories are pinned to WSUS

When scan source policies pin Feature or Quality updates to WSUS, several Windows components that normally fetch content directly from Windows Update can fail, because the OS treats WSUS as the authoritative source for the pinned categories.

Affected surfaces include:

- Features on Demand
- RSAT
- Optional features
- Language packs
- Microsoft Defender platform updates

If you set the scan source to WSUS, also configure the **Specify settings for optional component installation and component repair** policy, so those components can still reach Windows Update. This guidance applies to Windows 10 (non-UUP) servicing. On UUP-based builds, such as Windows 11 and later, leave that policy **Not Configured**, because the OS already sources optional content from Windows Update by default. For more information, see [How to make Features on Demand and language packs available when you're using WSUS or Configuration Manager](/windows/deployment/update/fod-and-lang-packs).

### Pitfall - Legacy Dual Scan values still on the device

Before scan source policies existed, environments used the `DisableDualScan` policy and defer or pause values under `HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate`.

On Windows 11, `DisableDualScan` has no effect. On Windows 10, a leftover `DisableDualScan = 1` suppresses the dual-scan channel that the scan source policies use to reach Windows Update, so any category that you pointed at Windows Update stops being retrieved.

Remove these values if you find them:

- `DeferFeatureUpdates` and `DeferFeatureUpdatesPeriodInDays`
- `DeferQualityUpdates` and `DeferQualityUpdatesPeriodInDays`
- `PauseFeatureUpdates` and `PauseFeatureUpdatesStartTime`
- `PauseQualityUpdates` and `PauseQualityUpdatesStartTime`
- `DeferUpgrade`
- `ExcludeWUDriversInQualityUpdate`
- `DisableDualScan`

### Pitfall - The co-management slider isn't authoritative

The **Windows Update policies** slider tells Configuration Manager whether it considers the workload owned. It doesn't move the local policy state that actually decides where the Windows Update agent scans.

Before KB 36495448, Configuration Manager overwrote scan source policies on every policy cycle, which had the side effect of resetting a device whenever the slider changed. That behavior is intentionally gone. As a result:

- Moving the slider to Intune doesn't automatically remove scan source values written by an earlier Configuration Manager version, a GPO, or a direct registry edit.
- Moving the slider back to Configuration Manager doesn't remove Intune-authored Windows Update client policy state, which lives under the MDM PolicyManager path.

Don't rely on the slider alone. Always confirm the effective policy on the device by using the [Troubleshoot](#troubleshoot) checks, especially [Inspect the MDM PolicyManager](#4-inspect-the-mdm-policymanager-on-co-managed-devices).

### Pitfall - Multiple policy providers on the same device

`HKLM\SOFTWARE\Microsoft\PolicyManager\current\device\Update` shows every enrolled MDM authority that wrote an Update policy. On a single co-managed device, you might see Intune, Windows Autopatch, a third-party MDM, and Group Policy all writing overlapping values. When you troubleshoot, always determine the winning provider for each value. For more information, see [Inspect the MDM PolicyManager](#4-inspect-the-mdm-policymanager-on-co-managed-devices).

## Identify clients that use Windows Update client policies for Windows updates
<a name="identify-clients-that-use-wufb-for-windows-updates"></a>

Use this procedure to identify clients that use Windows Update client policies to get Windows updates and upgrades. Then configure those clients to stop scanning WSUS, and disable the Configuration Manager software updates workflow for them.

### Prerequisites
<a name="prerequisites-for-wufb"></a>
<a name="BKMK_WUfB"></a>

- Windows 10 or later (Pro, Enterprise, Education, or Education Pro edition).
- [Windows Update client policies](/windows/deployment/update/waas-manage-updates-wufb) deployed, and clients configured to get Windows updates and upgrades from Windows Update.

### To identify clients that use Windows Update client policies
<a name="to-identify-clients-that-use-windows-update-for-business"></a>

The most reliable per-device signal that Windows updates come from Windows Update client policies, rather than WSUS, is in `WindowsUpdate.log`:

`Update filtered by policy: 6964AAB4-C5B5-43BD-A17D-FFB4346A8E1D.100`

The `6964AAB4-C5B5-43BD-A17D-FFB4346A8E1D` category is the Windows product. When Windows updates are filtered by policy, Windows Update client policies are the authority for those updates on the device.

Don't rely on the WSUS `UseWUServer` value alone. A device managed by Windows Update client policies can still have WSUS configured for other content, for example third-party updates, so `UseWUServer` being present or absent doesn't tell you where Windows updates come from.

To evaluate the scan source state across many devices, use CMPivot. For example, inspect the Windows Update `AU` registry key:

```kusto
Registry('hklm:\software\policies\Microsoft\Windows\Windowsupdate\AU') | where property == 'UseWUServer'
```

Combine this query with the `UseUpdateClassPolicySource` primary switch and the four `SetPolicyDrivenUpdateSourceFor*` category values to find devices whose Windows updates are routed to Windows Update. Then create a device collection from the results.

Create a client agent setting that disables the software update workflow, and deploy it to the collection of Windows Update-managed devices. Do this only when Configuration Manager isn't managing any updates on the device, including third-party updates.

Devices managed through Windows Update client policies display **Unknown** in the compliance status, and aren't counted in the overall compliance percentage.

## Configure deferral policies with Windows Update client policies
<a name="configure-windows-update-for-business-deferral-policies"></a>

You can configure deferral policies for Windows 10 or later Feature and Quality updates from within the Configuration Manager console. Manage them in the **Windows Update for Business Policies** node under **Software Library** > **Windows Servicing**.

> [!TIP]
> For most co-managed environments, deferral configuration is now done more centrally through Intune Windows Update client policies, such as feature update profiles, quality update profiles, and update rings. Use the in-console **Windows Update for Business Policies** node for standalone Configuration Manager environments, or when you must configure deferrals for devices that aren't enrolled in Intune.

> [!NOTE]
> You can set deferral policies for Windows Insider. For more information, see [Getting started with Windows Insider Program for Business](/windows-insider/business/server-get-started).

### Prerequisites for deferral policies

- Windows 10 or later.
- Devices managed by Windows Update client policies must have internet connectivity.

### To create a deferral policy
<a name="to-create-a-windows-update-for-business-deferral-policy"></a>

1. In the Configuration Manager console, go to **Software Library** > **Windows Servicing** > **Windows Update for Business Policies**.
1. On the **Home** tab, in the **Create** group, select **Create Windows Update for Business Policy**.
1. On the **General** page, provide a name and description.
1. On the **Deferral Policies** page, configure whether to defer or pause Feature Updates. Feature Updates are new features for Windows. After you set the **Branch readiness level**, you can specify whether and for how long the device defers receiving Feature Updates after they become available from Microsoft.

    - **Branch readiness level**: Semi-Annual Channel (Targeted), Semi-Annual Channel, or a Windows Insider build.

        > [!NOTE]
        > Semi-Annual Channel and Semi-Annual Channel (Targeted) are Windows 10 legacy branch models. Windows 10, version 22H2 is the final Windows 10 release, and there's no successor. On Windows 11, only the annual servicing channel applies. Set the branch readiness level to the value appropriate for the client OS that you're targeting.
        >
        > If you deploy a policy for **Semi-Annual Channel (Targeted)** to Windows 10, version 1903 or later, the deployment fails with the error `0x8004100c`.

    - **Deferral period (days)**: Up to 365 days from release.
    - **Pause Feature Updates starting**: Pauses Feature Updates for up to 35 days from the specified start date. After the pause period expires, the device scans Windows Update for applicable updates. After that scan, you can pause again. Clear the checkbox to unpause.

1. On the same **Deferral Policies** page, configure whether to defer or pause Quality Updates. Quality Updates are fixes and improvements to existing Windows functionality, and are typically published on the second Tuesday of each month, though Microsoft can release them at any time.

    - **Deferral period (days)**: Up to 30 days from release.
    - **Pause Quality Updates starting**: Pauses Quality Updates for up to 35 days from the specified start date. After the pause period expires, the device scans Windows Update for applicable updates. After that scan, you can pause again. Clear the checkbox to unpause.

1. Select **Install updates from other Microsoft Products** to apply deferral settings to Microsoft Update in addition to Windows Update.
1. Select **Include drivers with Windows Update** to allow driver updates from Windows Update. Clear the setting to exclude drivers.
1. Complete the wizard.

### To deploy a deferral policy
<a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>

1. In the Configuration Manager console, go to **Software Library** > **Windows Servicing** > **Windows Update for Business Policies**.
1. On the **Home** tab, in the **Deployment** group, select **Deploy Windows Update for Business Policy**.
1. Configure the following settings:

    - **Configuration policy to deploy**: The policy to deploy.
    - **Collection**: The target collection.
    - **Allow remediation outside the maintenance window**: Enable this option to let policy settings remediate the value outside of the maintenance window. For more information, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).
    - **Schedule**: The compliance evaluation schedule, either simple or custom.

1. Complete the wizard.

## Troubleshoot

Use these checks from top to bottom when a device isn't scanning against the source that you expect.

### 1. Determine the effective update authority per update category

Windows selects its update source per update category (Driver, Feature, Quality, Other). A single default-service check, `IsDefaultAUService`, is no longer reliable once scan source or Windows Update client policies are configured, because it reports only one default service and can't show per-category routing.

Instead, resolve the effective authority for each category from the policy state on the device: the scan source primary switch, the four `SetPolicyDrivenUpdateSourceFor*` category values, the WSUS and Dual Scan configuration, and the MDM PolicyManager state. The checks in this section walk through each of those in order.

The most reliable single location is the resolved policy state that the Windows Update agent commits after each policy refresh:

```powershell
$policyState = 'HKLM:\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\PolicyState'
Get-ItemProperty -Path $policyState -ErrorAction SilentlyContinue |
    Select-Object UseUpdateClassPolicySource,
                  SetPolicyDrivenUpdateSourceForFeatureUpdates,
                  SetPolicyDrivenUpdateSourceForQualityUpdates,
                  SetPolicyDrivenUpdateSourceForDriverUpdates,
                  SetPolicyDrivenUpdateSourceForOtherUpdates,
                  IsDeferralIsActive,
                  IsWUfBDualScanActive
```

This state already reflects the Group Policy versus Intune arbitration and the `UseWUServer` requirement, so it shows what the agent actually honors, rather than what was merely authored. In the per-category values, `0` means Windows Update and `1` means WSUS. `IsWUfBDualScanActive` is the client's own verdict on whether Feature and Quality updates are being routed to Windows Update.

> [!NOTE]
> The `UseUpdateClassPolicySource` gate applies only to Group Policy-authored scan source values. Policy delivered by Intune has no such gate, so a device can honor a scan source that Intune set even when the Group Policy gate is absent.
>
> Comparing this resolved state against the authored values under `HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate` tells you whether a configured value is actually in effect, or is being ignored because the gate is off or the value is at the wrong path.

### 2. Inspect the primary switch

```powershell
# Correct location.
Get-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' `
    -Name 'UseUpdateClassPolicySource' -ErrorAction SilentlyContinue

# Wrong location. If this returns a value, remove it.
Get-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate' `
    -Name 'UseUpdateClassPolicySource' -ErrorAction SilentlyContinue
```

### 3. Inspect the four category values

```powershell
$wuau = 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate'
'SetPolicyDrivenUpdateSourceForDriverUpdates',
'SetPolicyDrivenUpdateSourceForFeatureUpdates',
'SetPolicyDrivenUpdateSourceForOtherUpdates',
'SetPolicyDrivenUpdateSourceForQualityUpdates' | ForEach-Object {
    [PSCustomObject]@{
        Value = $_
        Data  = (Get-ItemProperty -Path $wuau -Name $_ -ErrorAction SilentlyContinue).$_
    }
}
```

All four values should be set if you're using scan source policies. If some are set while others aren't, and `UseUpdateClassPolicySource = 1`, you have a partial configuration.

> [!NOTE]
> After you change any Windows Update policy, either a registry value or a Group Policy setting, restart the Windows Update service with `Restart-Service wuauserv` and trigger a new scan so that the agent rereads the policy. Changes don't take effect until the agent reloads.

### 4. Inspect the MDM PolicyManager on co-managed devices

```powershell
# Effective device-scope Update CSP values, which is what Windows sees today.
Get-ChildItem 'HKLM:\SOFTWARE\Microsoft\PolicyManager\current\device\Update' `
    -ErrorAction SilentlyContinue |
    Select-Object PSChildName

# Which MDM provider wrote each Update CSP value?
Get-ChildItem 'HKLM:\SOFTWARE\Microsoft\PolicyManager\providers' -ErrorAction SilentlyContinue |
    ForEach-Object {
        $prov = $_.PSChildName
        Get-ChildItem "$($_.PSPath)\default\device\Update" -ErrorAction SilentlyContinue |
            Select-Object @{n='Provider';e={$prov}}, @{n='Setting';e={$_.PSChildName}}
    }
```

Values under `\current\device\Update` mean that an MDM authority, such as Intune, Windows Autopatch, or a third-party MDM, configured Windows Update policy on this device. If you see multiple providers, check the winning provider on each conflicting value.

### 5. Read WindowsUpdate.log

`WindowsUpdate.log` is essential in co-managed environments, because it shows the service that each scan or download actually used.

```powershell
Get-WindowsUpdateLog -LogPath "$env:USERPROFILE\Desktop\WindowsUpdate.log"
```

Look for the following fields:

| Field | Interpretation |
|---|---|
| `Service ID {7971F918-A847-4430-9279-4A52D1EFE18D}` | Microsoft Update |
| `Service ID {9482F4B4-E343-43B6-B170-9A65BC822C77}` | Windows Update |
| `Service ID {3DA21691-E39D-4DA6-8A4B-B43877BCB1B7}` | WSUS or Configuration Manager |
| `WSUS server: https://…` | The configured WSUS endpoint |
| `[SLS] Making request with URL HTTPS://sls.update.microsoft.com/…` | The client contacted the Microsoft Service Locator Service, which is used by Windows Update and Microsoft Update, but not WSUS |
| `Flighting ID` | The update was delivered through Windows Update flighting, for example Intune or Autopatch |
| `Deployment ID` | The update belongs to a specific deployment, such as an Intune update ring or Windows Autopatch |
| `Update filtered by policy: 6964AAB4-C5B5-43BD-A17D-FFB4346A8E1D.100` | Windows updates are filtered out of the WSUS scan by Windows Update client policies. The `6964AAB4-C5B5-43BD-A17D-FFB4346A8E1D` category is the Windows product |

If `WSUS server:` is set correctly but the agent still calls `sls.update.microsoft.com`, either Dual Scan is engaged on Windows 10, or a scan source policy is redirecting a category to Windows Update.

### 6. Read WUAHandler.log

`%windir%\CCM\Logs\WUAHandler.log` records the actions of the Configuration Manager Windows Update handler. Enable verbose and debug logging on the Configuration Manager client to see these lines. All of the `SourceManager::PolicySettings` lines appear only with debug and verbose logging enabled.

- `Enabling WUA Managed server policy to use server: <wsus>`: Configuration Manager pointed Windows Update at WSUS.
- `Group policy settings were overwritten by a higher authority (Domain Controller)`: A GPO is winning over what Configuration Manager set.
- `SourceManager::PolicySettings - Windows Update client policies disabled.`: Intune isn't managing Windows Update client policies on this device. This is the branch used after KB 36495448.
- `SourceManager::PolicySettings - Remove UseUpdateClassPolicySource for Windows Update client policies disabled`: The one-shot cleanup of any legacy scan source state is about to run. This happens on the first run only, after KB 36495448.
- `SourceManager::PolicySettings - Set isScanSourcePolicyRemoved to true to avoid remove again.`: The one-shot cleanup completed, and won't repeat.
- `SourceManager::PolicySettings - For ConfigMgr 2503 HFRU and 2509 and correct the partial setting behavior.`: The partial-state cleanup from Scenario 3a is running.
- `Setting UseUpdateClassPolicySource to 0`: Appears once during the cleanup after KB 36495448, when the flag wasn't yet set. On versions before the hotfix, the same log line appears whenever Configuration Manager writes the value.

### Clean up after moving the workload back to Configuration Manager

Run this script on the affected device after you move the **Windows Update policies** workload from Intune back to Configuration Manager, and after a Configuration Manager machine policy cycle is complete.

> [!CAUTION]
> This script deletes registry keys under the Windows MDM PolicyManager hive, and removes an MDM WMI instance. Test it in a lab first.
>
> If the device is still enrolled in Intune, Intune might reapply the removed policy on its next MDM sync. To avoid a reapply loop, unassign the device from the Windows Update ring in Intune before you run the script, or move the device out of the targeted Intune group.

```powershell
# 1. Remove residual MDM CSP registry state for Update policy.
# Clear only the 'current' node. The 'default' node holds baseline state and must not be deleted.
$path = 'HKLM:\SOFTWARE\Microsoft\PolicyManager\current\device\Update'
if (Test-Path $path) {
    Remove-Item -Path $path -Recurse -Force -ErrorAction SilentlyContinue
}

# 2. Remove the MDM WMI instance that mirrors the CSP.
Get-CimInstance -Namespace 'root\cimv2\mdm\dmmap' `
    -ClassName  'MDM_Policy_Config01_Update02' `
    -Filter     "InstanceID='Update' AND ParentID='./Vendor/MSFT/Policy/Config'" |
    Remove-CimInstance -ErrorAction SilentlyContinue

# 3. Clear any leftover scan source values from earlier Configuration Manager versions.
$wuau = 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate'
$au   = "$wuau\AU"
Remove-ItemProperty -Path $au   -Name 'UseUpdateClassPolicySource' -ErrorAction SilentlyContinue
Remove-ItemProperty -Path $wuau -Name 'UseUpdateClassPolicySource' -ErrorAction SilentlyContinue
'SetPolicyDrivenUpdateSourceForDriverUpdates',
'SetPolicyDrivenUpdateSourceForFeatureUpdates',
'SetPolicyDrivenUpdateSourceForOtherUpdates',
'SetPolicyDrivenUpdateSourceForQualityUpdates' | ForEach-Object {
    Remove-ItemProperty -Path $wuau -Name $_ -ErrorAction SilentlyContinue
}

# 4. Force the Windows Update agent to reselect its source.
Restart-Service wuauserv -Force
gpupdate /force
Start-Sleep -Seconds 30

# 5. Verify.
(New-Object -ComObject 'Microsoft.Update.ServiceManager').Services |
    Where-Object IsDefaultAUService | Select-Object -ExpandProperty Name
```

The expected result is **Windows Server Update Service**, if WSUS is configured. Once scan source policies are set, `IsDefaultAUService` reports only one default service, so also verify per category by using the checks earlier in this section, or the `Enabling WUA Managed server policy to use server:` entry in `WUAHandler.log`.

Then trigger a **Machine Policy Retrieval & Evaluation Cycle** from the Configuration Manager client, and confirm that `WUAHandler.log` writes the expected `WUServer` value.

## Appendix: Configuration Manager version history for scan source policies

Use this table to correlate what a device might currently have on disk with the Configuration Manager version that put it there. This table is primarily useful when you investigate why a device is scanning against an unexpected source, or when you plan an upgrade path.

| Configuration Manager version | Behavior |
|---|---|
| 2111 | Wrote the four `SetPolicyDrivenUpdateSourceFor*` values, but didn't set the `UseUpdateClassPolicySource` primary switch. The category policies existed on disk, but had no effect. |
| 2303 + KB 25073607 | Started setting `UseUpdateClassPolicySource = 1`. The category policies became effective, so for the first time devices actually scanned per category. Customers began seeing Features on Demand, RSAT, optional feature, language pack, and Defender platform update failures, because those components were now pinned to WSUS. |
| 2403 + KB 28458764 | Stopped writing the category values, but didn't remove existing ones. Devices upgraded from earlier builds still had the values set to `1`, and new installations didn't. Administrators could manage the values themselves. |
| 2409 and 2503 RTM | Intended to set `UseUpdateClassPolicySource = 0` under `\AU` to disable scan source enforcement. A defect wrote the value to `…\WindowsUpdate\UseUpdateClassPolicySource`, missing the `\AU` subkey, so the Windows Update agent ignored it. Effective behavior on upgraded clients didn't change. |
| 2503 HFRU and 2509, before KB 36495448 | Corrected the wrong-path defect, and removed the incorrectly placed value. However, when Intune managed Windows updates and third-party updates were enabled in Configuration Manager, the client set only `UseUpdateClassPolicySource = 1` and `SetPolicyDrivenUpdateSourceForOtherUpdates = 1`, and removed the other three category values. This behavior created the partial-configuration problem described in Scenario 3a. |
| 2503 HFRU or 2509, with KB 36495448 | Configuration Manager stops touching scan source policies entirely on co-managed devices. It cleans up any partial state left by the behavior before the hotfix once, and sets `HKLM\SOFTWARE\Microsoft\CCM\SoftwareUpdates\isScanSourcePolicyRemoved2 = 1` to prevent repeated cleanup. |

## Related content

- [Use Windows Update client policies and Windows Server Update Services (WSUS) together](/windows/deployment/update/wufb-wsus)
- [Co-management workloads](../../comanage/workloads.md#windows-update-policies)
- [Client settings - Software Updates](../../core/clients/deploy/about-client-settings.md#software-updates)
- [Client settings - Enable third-party software updates](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)
- [Manage Windows Update client policies from Intune](/mem/intune-service/protect/windows-update-for-business-configure)
- [Windows Autopatch prerequisites](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites)
- [How to make Features on Demand and language packs available when you're using WSUS or Configuration Manager](/windows/deployment/update/fod-and-lang-packs)
- [Policy CSP - Update](/windows/client-management/mdm/policy-csp-update)
- [KB 36495448 - Software update management client fix for Configuration Manager versions 2503, 2509](../../hotfix/2509/36495448.md)
