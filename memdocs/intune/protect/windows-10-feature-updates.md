---
# required metadata

title: Configure Windows 10 feature updates policy in Intune - Azure | Microsoft Docs
description: Create and manage Intune policy for Windows 10 feature updates. Configure and deploy policy to maintain the Windows feature version of Windows 10 devices you manage with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/07/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidmeb; bryanke 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Windows 10 feature updates policy in Intune

*This feature is in public preview.*

With *Windows 10 feature updates* in Intune, you can select the Windows [feature update](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) version that you want devices to remain at, like Windows 10 version 1803 or version 1809. Intune supports setting a feature level of 1803 or later.

Windows 10 feature updates policies work with your *Windows 10 update ring* policies to prevent a device from receiving a Windows feature version that’s later than the value specified in the feature updates policy.

When a device receives a Windows 10 feature updates policy:

- The device updates to the version of Windows specified in the policy. A device that already runs a later version of Windows remains at its current version. By freezing the version, the devices feature set remains stable for the duration of the policy.

  > [!NOTE]
  > A device won't install an update when it has a *safeguard hold* for that Windows version. When a device evaluates applicability of an update version, Windows creates the temporary safeguard hold if an unresolved known issue exists. Once the issue is resolved, the hold is removed and the device can then update.
  >
  > - Learn more about [safeguard holds](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) in the Windows documentation for *Feature Update Status*.
  > - To learn about known issues that can result in a safeguard hold, see [Windows 10 release information](/windows/release-information/) and then reference the relevant Windows version from the table of contents for that page.
  >
  >   For example, for Windows version 2004, open [Windows 10 release information](/windows/release-information/), and then from the left-hand pane, select *Version 2004* and then *Known issues and notifications*. The [resultant page](/windows/release-information/status-windows-10-2004) details known issues for that Windows version that might result in safeguard hold.

- Unlike using *Pause* with an update ring, which expires after 35 days, the Windows 10 feature updates policy remains in effect. Devices won't install a new Windows version until you modify or remove the Windows 10 feature updates policy. If you edit the policy to specify a newer version, devices can then install the features from that Windows version.

## Prerequisites

Intune’s Windows 10 feature updates requires the following prerequisites:

- In addition to a license for Intune, your organization must have one of the following subscriptions:
  - Windows 10 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
  - Windows 10 Education A3 or A5 (included in Microsoft 365 A3 or A5)
  - Windows Virtual Desktop Access E3 or E5

- Devices must:  
  - Run Windows 10 version 1709 or later.
  - Be enrolled in Intune MDM and be Hybrid AD joined or Azure AD joined.
  - Have Telemetry turned on, with a minimum setting of [*Basic*](../configuration/device-restrictions-windows-10.md#reporting-and-telemetry).

    Devices that receive a feature updates policy and that have Telemetry set to *Not configured* (off), might install a later version of Windows than defined in the feature updates policy. The prerequisite to require Telemetry is under review as this feature moves towards general availability.
  
    Configure Telemetry as part of a [Device Restriction policy](../configuration/device-restrictions-configure.md) for Windows 10 or later. In the device restriction profile, under *Reporting and Telemetry*, configure the **Share usage data** with a minimum value of **Basic**. Values of **Enhanced** or **Full** are also supported.

  - Have Microsoft Sign-In Assistant (wlidsvc) running. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates are not being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are).

- Feature updates are supported for the following Windows 10 editions:  
  - Windows 10 Pro
  - Windows 10 Enterprise
  - Windows 10 Pro Education
  - Windows 10 Education

  > [!NOTE]
  > **Unsupported versions and editions**:  
  > *Windows 10 Enterprise LTSC*: Windows Update for Business (WUfB) does not support the *Long Term Service Channel* release. Plan to use alternative patching methods, like WSUS or Configuration Manager.

## Limitations for Windows 10 feature updates policy

- When you deploy a *Windows 10 feature updates* policy to a device that also receives a *Windows 10 update ring* policy, review the update ring for the following configurations:
  - The **Feature update deferral period (days)** must be set to **0**.
  - Feature updates for the update ring must be *running*. They must not be paused.

- Windows 10 feature updates policies cannot be applied during the Autopilot out of box experience (OOBE). Instead, the policies apply at the first Windows Update scan after a device has finished provisioning, which is typically a day.

- While this feature is in preview and you co-manage devices with Configuration Manager, there is a limitation where feature updates policies might not immediately take effect. This delay can result in devices updating to a later feature update version than as configured policy.

  For an alternative method to restrict the Windows 10 feature update versions that are offered to devices enrolled in Intune, see [Use the TargetReleaseVersion policy CSP to manage Windows 10 feature updates for co-managed devices](/troubleshoot/mem/intune/create-feature-update-hold-co-managed-devices). 

- When the device checks in to the Windows Update service, the device's group membership is validated against the security groups assigned to the feature updates policy settings for any feature update holds.

## Create and assign Windows 10 feature updates policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Windows 10 Feature updates** > **Create profile**.

3. Under **Basics**, specify a name, a description (optional), and for **Feature update to deploy**, select the version of Windows with the feature set you want, and then select **Next**.

4. Under **Assignments**, choose **+ Select groups to include** and then assign the feature updates deployment to one or more device groups. Select **Next** to continue.

5. Under **Review + create**, review the settings. When ready to save the Windows 10 feature updates policy, select **Create**.  

## Manage Windows 10 feature updates policy

In the admin center, go to **Devices** > **Windows** > **Windows 10 Feature updates** and select the policy that you want to manage. The policy opens to its **Overview** pane.

From this pane, you can:

- Select **Delete** to delete the policy from Intune and remove it from devices.
- Select **Properties** to modify the deployment.  On the *Properties* pane, select **Edit** to open the *Deployment settings or Assignments*, where you can then modify the deployment.
- Select **End user update status** to view information about the policy.

## Validation and reporting

There are multiple options to get in-depth reporting for Windows 10 updates with Intune. To learn more, see [Intune compliance reports](../protect/windows-update-compliance-reports.md).

## Next steps

- [Use Windows 10 update rings in Intune](../protect/windows-10-update-rings.md)
- Use [Intune compliance reports](../protect/windows-update-compliance-reports.md) for Windows 10 updates
