---
# required metadata

title: Learn about using Windows Update for Business in Microsoft Intune - Azure | Microsoft Docs
description: Manage Windows 10 software updates by using Intune policy for Windows 10 update rings and Windows 10 feature updates for Windows Update for Business settings in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/25/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dudeso
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Manage Windows 10 software updates in Intune

Use Intune to manage the install of Windows 10 software updates from Windows Update for Business.

By using Windows Update for Business, you simplify the update management experience. You don't need to approve individual updates for groups of devices and can manage risk in your environments by configuring an update rollout strategy. Intune provides the ability to [configure update settings](windows-update-settings.md) on devices and gives you the ability to defer update installation. You can also prevent devices from installing features from new Windows versions to help keep them stable, while allowing those devices to continue installing updates for quality and security.

Intune stores only the update policy assignments, not the updates themselves. Devices access Windows Update directly for the updates.

Learn more about Windows 10 [*feature* and *quality* updates](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) in the Windows documentation.

## Policy types to manage updates

Intune provides the following policy types to manage updates:

- **Windows 10 update ring**: This policy is a collection of settings that configures when Windows 10 updates get installed.

  Update ring policies are supported for devices that run Windows 10 version 1607 or later.

- **Windows 10 feature updates** *(public preview)*: This policy updates devices to the Windows version you specify, and then freezes the feature set version on those devices. This version freeze remains in place until you choose to update them to a later Windows version. While the feature version remains static, devices can continue to install quality and security updates that are available for their feature version.

  Feature updates policies are supported for devices that run Windows 10 version 1709 or later.

You assign policies for Windows 10 update rings and Windows 10 feature updates to groups of devices. Use both policy types in the same Intune environment to manage updates for your Windows 10 devices.

<!-- moving out 


## Windows 10 update rings

## Windows 10 feature updates

*This feature is in public preview.*

With *Windows 10 feature updates*, you select the Windows feature version that you want devices to remain at, like Windows 10 version 1803 or version 1809. You can set a feature level of 1803 or later.  Windows 10 feature updates work in conjunction with Update Ring policies to prevent a device from receiving a Windows feature version greater than the value specified in the feature update policy.

When a device receives a Windows 10 feature updates policy:

- The device will update to the version of Windows specified in the policy. A device that already runs a later version of Windows remains at its current version. By freezing the version, the devices feature set remains stable for the duration of the policy.

  > [!NOTE]
  > A device won't install an update when it has a *safeguard hold* for that Windows version. When a device evaluates applicability of an update version, Windows creates the temporary safeguard hold if an unresolved known issue exists. Once the issue is resolved, the hold is removed and the device can then update.
  >
  > - Learn more about [safeguard holds](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) in the Windows documentation for *Feature Update Status*.
  > - To learn about known issues that can result in a safeguard hold, see [Windows 10 release information](/windows/release-information/) and then reference the relevant Windows version from the table of contents for that page.
  >
  >   For example, for Windows version 2004, open [Windows 10 release information](/windows/release-information/), and then from the left-hand pane, select *Version 2004* and then *Known issues and notifications*. The [resultant page](/windows/release-information/status-windows-10-2004) details known issues for that Windows version that might result in safeguard hold.
  >
  > While safeguard holds are not visible in Intune today, a future release will add the ability to report on them.

- Unlike using *Pause* with an update ring, which expires after 35 days, the Windows 10 feature updates policy remains in effect. Devices won't install a new Windows version until you modify or remove the Windows 10 feature updates policy. If you edit the policy to specify a newer version, devices can then install the features from that Windows version.


### Prerequisites for Windows 10 feature updates

The following prerequisites must be met to use Windows 10 feature updates in Intune.

- Devices must be enrolled in Intune MDM and be Hybrid AD joined, Azure AD joined, or Azure AD registered.
- To use the Feature Updates policy with Intune, devices must have telemetry turned on, with a minimum setting of [*Basic*](../configuration/device-restrictions-windows-10.md#reporting-and-telemetry). Telemetry is configured under *Reporting and Telemetry* as part of a [Device Restriction policy](../configuration/device-restrictions-configure.md).
  
  Devices that receive Feature Updates policy and that have telemetry set to *Not configured*, which means it's off, might install a later version of Windows than defined in the Feature Update policy. The prerequisite to require telemetry is under review as this feature moves towards general availability.

### Limitations for Windows 10 feature updates

- When you deploy a *Windows 10 feature update* policy to a device that also receives a *Windows 10 update ring* policy, review the update ring for the following configurations:
  - The **Feature update deferral period (days)** must be set to **0**.
  - Feature updates for the update ring must be *running*. They must not be paused.

- Windows 10 feature update policies cannot be applied during the Autopilot out of box experience (OOBE) and will only apply at the first Windows Update scan after a device has finished provisioning (which is typically a day).

- While Windows 10 feature updates remain in public preview, when co-managing devices with Configuration Manager and Intune, there is a limitation where feature update policies may not immediately take effect, causing devices to update to a later feature update than configured in Intune. This limitation will be removed with a future update to Configuration Manager.

- Only **device groups** are supported for Windows 10 feature update policies.  When the device checks in to the Windows Update service, the device's group membership is validated against the security groups assigned to the feature update policy settings for any feature update holds.  User groups are not supported.

- The current version of the Windows feature version may not be immediately visible in the Microsoft Endpoint Manager admin center after it is released.  Because a Windows feature version higher than the current version number will not be immediately available, there is no benefit to having the current feature version available.  For example, since Windows 10 feature update version 20H2 (2010) is the highest version of Windows 10 currently available, creating a feature update policy today that specifies Windows feature version 2010 is equivalent to not having a feature update policy since there is no higher feature update version of the OS to prevent from installing.  New version numbers are typically added in a monthly update soon after the feature update version is released.
  

### Create and assign Windows 10 feature updates

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Windows 10 Feature updates** > **Create**.

3. Under **Basics**, specify a name, a description (optional), and for **Feature update to deploy**, select the version of Windows with the feature set you want, and then select **Next**.

4. Under **Assignments**, choose **+ Select groups to include** and then assign the feature update deployment to one or more device or user groups. Select **Next** to continue.

5. Under **Review + create**, review the settings and select **Create** when ready to save the Windows 10 feature updates policy.  

### Manage Windows 10 feature updates

In the admin center, go to **Devices** > **Windows** > **Windows 10 Feature updates** and select the policy that you want to manage. The policy opens to its **Overview** pane.

From this pane, you can:

- Select **Delete** to delete the policy from Intune and remove it from devices.
- Select **Properties** to modify the deployment.  On the *Properties* pane, select **Edit** to open the *Deployment settings or Assignments*, where you can then modify the deployment.
- Select **End user update status** to view information about the policy.
-->

## Reporting on updates

To learn about report options for Windows 10 update ring policy and Windows 10 feature updates policy, see [Intune compliance reports for updates](windows-update-compliance-reports.md).

## Next steps

- [Use Windows 10 update rings in Intune](../protect/windows-10-update-rings-policy-in-intune)
- [Use Windows 10 feature updates in Intune](../protect/windows-10-feture-updates-policy-in-Intune)
- For more information, see [Manage updates using Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb) in the Windows documentation.
