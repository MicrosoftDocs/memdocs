---
title: Windows Feature Update Policies
description: Learn about Windows feature update polies and how to manage them in Microsoft Intune.
ms.date: 01/14/2026
ms.topic: how-to
ms.reviewer: davidmeb; bryanke; davguy
---

# Manage Windows feature update policies


Feature update policies in Microsoft Intune let you control which Windows version devices are offered and when that version can install. You can use these policies to target a specific Windows release, upgrade devices to a newer version, or ensure devices remain on a designated version until you're ready to move forward.

If a device already runs a newer Windows version than the one specified in the policy, the device isn't downgraded and continues running its current version. By controlling version targeting, feature update policies help maintain version consistency, reduce unexpected upgrades, and align OS updates with application readiness and organizational rollout plans.

Unlike pausing feature updates in update rings—which automatically expires after 35 days—a feature update policy remains in effect until you modify or remove it. When a feature update installs, the latest applicable monthly quality update is included as part of the upgrade.

For information about controlling the availability of feature update offers, see [Rollout options for Windows Updates](rollout-options.md).

> [!NOTE]
> A device won't install an update when it has a [*safeguard hold*](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) for that Windows version. When a device evaluates applicability of an update version, Windows creates the temporary safeguard hold if an unresolved known issue exists. Once the issue is resolved, the hold is removed and the device can then update.
>
> - To learn about known issues that can result in a safeguard hold, see the applicable Windows release information and then reference the relevant Windows version from the table of contents for that page: [Windows 11 release information](/windows/release-health/windows11-release-information).

## Create and assign feature update policies

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows**.
1. Select **Windows updates** > **Feature updates**.
1. Select **Create profile**.
1. Under **Deployment settings**:
   - Specify a **Name** and an optional **Description** for the feature updates deployment.
   - From the **Feature update to deploy** dropdown, select the Windows version you want to deploy. Only versions of Windows that remain in support are available to select.
   - Select either:
       - **Make available to users as a required update**: the device will automatically install the update based on device settings.
       - **Make available to users as an optional update**: selected updates are made available to users as an optional update. The rollout settings still control when the update is available to the device but then the user must choose to install the update before it is installed on the device. This option requires a license for Windows Autopatch.
1. Under **Rollout options**, configure how and when the update is made available to devices that receive this policy. For more information, see [Rollout options for Windows Updates](rollout-options.md).
1. Select **Next**
1. Under **Assignments**, assign the policy to one or more device groups. Select **Next** to continue.
1. Under **Review + create**, review the settings. When ready to save the policy, select **Create**.


## User experience

The user experience depends on whether the update is offered as required or optional.\
When a feature update is made available as an **Optional** update, users must navigate to **Windows Update** in device settings to see and choose to install the update. Users must select **Download** to begin installation. If they don't take action, the update isn't installed unless an admin later changes the update to **Required**.

This experience matches the optional update behavior users see on personal Windows devices. It's recommended that administrators notify users through organizational communication channels when an optional feature update is available.

### Switching update availability

If an update is changed from **Optional** to **Required**:

- Devices that already installed the update aren't affected.
- Devices that haven't started the update install it automatically during the next update scan.

If an update is changed from **Required** to **Optional**:

- Devices that have already completed installation aren't affected.
- Devices that are pending restart typically continue installation as a required update.
- Only devices that haven't started installation, or are early in the process, switch to optional behavior.


## How feature update policies are evaluated

When a device is targeted by multiple feature update policies, Windows Update evaluates all applicable policies and determines which feature update to offer.

Keep the following behavior in mind:

- Each feature update policy can target only one Windows version. A device targeted by multiple policies can therefore be eligible for multiple feature updates.
- The Windows Update service offers only one feature update to a device at a time and always selects the **latest applicable version**.
- Windows 11 feature updates are always considered later versions than Windows 10 feature updates. If a Windows 10 device is targeted by both Windows 10 and Windows 11 feature update policies, the Windows 11 update is offered because upgrading from Windows 10 to Windows 11 is a supported path.
- To avoid unintended targeting, use **When a device isn't capable of running Windows 11, install the latest Windows 10 feature update**. This option ensures that devices evaluated as ineligible for Windows 11 receive the most recent supported Windows 10 feature update instead.

> [!NOTE]
> If two policies target the same feature update version for the same device, and one policy is configured as **Required** while the other is **Optional**, the update is offered as **Required**.


## Manage Winodws feature update policies

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows**.
1. Select **Windows updates** > **Feature updates**.

For each profile you can view:

- **Feature Update Version**: The feature update version in the profile.

- **Assigned**: If the profile is assigned to one or more groups.

- **Support**: The status of the feature update:
  - **Supported**: The feature update version is in support and can deploy to devices.
  - **Support Ending** - The feature update version is within two months of its support end date.
  - **Not supported**: Support for the feature update has expired and it no longer deploys to devices.

- **Support End Date**: The end of support date for the feature update version.
> [!NOTE]
> The date provided is for the Enterprise and Education editions of Windows.  To find the support dates for other editions supported by Windows Autopatch, see the [Microsoft Product Lifecycle site](https://aka.ms/lifecycle).

Selecting a profile from the list opens the profiles **Overview** pane where you can:

- Select **Delete** to delete the policy from Intune and remove it from devices.
- Select **Properties** to modify the deployment.  On the *Properties* pane, select **Edit** to open the *Deployment settings or Assignments*, where you can then modify the deployment.

> [!NOTE]
> The End user update status Last Scanned Time value will return *Not scanned yet* until a user logs on and Update Session Orchestrator (USO) scan is initiated. For more information on the Unified Update Platform (UUP) architecture and related components, see [Get started with Windows Update](/windows/deployment/update/windows-update-overview).


## Co-management considerations

If you co-manage devices with Configuration Manager, feature update policies might not immediately take effect on devices when you newly configure the [Windows Update policies workload](../../configmgr/comanage/workloads.md#windows-update-policies) to Intune. This delay is temporary but can initially result in devices updating to a later feature update version than is configured in the policy.

To prevent this initial delay from impacting your co-managed devices:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows**.
1. Select **Windows updates** > **Feature updates**.
1. Select **Create profile**.
1. For **Deployment settings**, enter a name and a description for the policy. Then, specify the feature update you want devices to be running.
1. Complete the policy configuration, including assigning the policy to devices. The policy deploys to devices, though any device that already has the version you've selected, or a newer version, won't be offered the update.\
   Monitor the report for the policy. To do so, go to **Reports** > **Windows Updates** > **Reports** tab > **Feature Updates report**. Select the policy you created and then generate the report.
1. Devices that have a state of *OfferReady* or later, are enrolled for feature updates and protected from updating to anything newer than the update you specified in step 3. See [Use the Windows feature updates (Organizational) report](feature-updates-reports.md#accessing-feature-updates-reports).
1. With devices enrolled for updates and protected, you can safely change the *Windows Update policies* workload from Configuration Manager to Intune. See, [Switch workloads to Intune](/configmgr/comanage/how-to-switch-workloads) in the co-management documentation.


## Move from update ring deferrals to feature update policies

When managing Windows feature updates in Intune, you can use either update ring deferrals or feature update policies to control which Windows versions devices can install. If you use feature update policies, Microsoft recommends that you stop using feature update deferrals in update ring policies.

Combining feature update deferrals with feature update policies adds unnecessary complexity and can delay or block feature updates. While update rings can continue to manage user experience settings—such as restart behavior and notifications—feature update policies should be the primary mechanism for controlling feature update versions.

When both policy types apply to a device, the conditions of both must be met before an update is offered. This evaluation can lead to unintended blocking of feature updates if deferrals remain configured.

### Plan the transition

Plan the transition from update ring deferrals to feature update policies to ensure Windows Update offers the updates you expect.

When Intune Windows update policies are created or modified, policy details are sent to the Windows Update service, which evaluates update applicability for each device. This evaluation typically completes within 10 minutes, but in some cases can take longer.

If a device scans for updates after a deferral is removed but before Windows Update finishes processing the feature update policy, the device might be offered a feature update you didn't intend to deploy.

### Switch to feature update policies

Use the following process to ensure Windows Update processes the feature update policy before feature update deferrals are removed:

1. In the Microsoft Intune admin center, create a feature update policy that targets the desired Windows version and assign it to the appropriate devices. After the policy is assigned, allow several minutes for Windows Update to process the policy.
1. Review the [Windows feature updates (Organizational)](feature-updates-reports.md#accessing-feature-updates-reports) report for the policy and verify that devices show a state of **OfferReady**. This state indicates that Windows Update has completed policy processing.
1. After all targeted devices report **OfferReady**, update the applicable [update ring policy](update-rings.md) and set **Feature update deferral period (days)** to **0**.

## Next steps

- [Manage Windows Feature Updates](feature-updates.md)
- [Reports for Windows Feature Update Policies](feature-updates-reports.md)

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431