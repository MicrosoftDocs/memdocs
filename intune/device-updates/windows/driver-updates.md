---
title: Learn about Windows Driver updates policy for Windows devices in Intune
description: Learn about using Microsoft Intune policy to manage Windows driver updates.
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: davguy; davidmeb; bryanke
---

# Windows Driver update management in Microsoft Intune

With Windows Driver Update Management in Microsoft Intune, you can review, approve for deployment and pause deployments of driver updates for your managed Windows devices. Intune and the Windows Autopatch take care of the heavy lifting to identify the applicable driver updates for devices that are assigned a driver updates policy. Intune and Windows Autopatch sort updates by categories that help you easily identify the recommended driver updates for all devices, or updates that might be considered optional for more limited use.

Using Windows driver update policies, you remain in control of which driver updates can install on your devices. You can:

- **Enable automatic approvals of recommended driver updates**. Policies set for automatic approval automatically approve and deploy each new driver update version that is considered a *recommended driver* for the devices assigned to the policy. Recommended drivers are typically the latest driver update published by the driver publisher that the publisher has marked as *required*. Drivers that aren't identified as the current recommended driver are also available as *other drivers*, which can be considered to be optional driver updates.

  Later, when a newer driver update from the OEM is released and identified as the current *recommended* driver update, Intune automatically adds it to the policy and moves the previously recommended driver to the list of other drivers.

  > [!TIP]
  > An approved recommended driver update that is moved to the *other drivers* list due to a newer recommended driver update becoming available, remains approved. When a newer recommended and approved driver update is available, Windows Autopatch installs only that latest approved version. If the latest approved update version is paused, Autopatch automatically offers the next most recent and approved update version, which is now on the *other drivers* list. This behavior ensures that the last known-good driver update version that was approved can continue to install on devices, while the more recent recommended version remains paused.

  With this policy configuration, you can also choose to review the available updates to selectively approve, pause, or decline *any* update that remains available for devices with the policy.

- **Configure policy to require manual approval of all updates**. This policy ensures that administrators must approve a driver update before it can be deployed. Newer versions of driver updates for devices with this policy are automatically added to the policy but remain inactive until approved.

Later, when a newer driver update from the OEM is recommended for a device in the policy, the policy status updates to indicate there are drivers pending your review. This status becomes a call to action to review the policy and decide if you want to approve deployment of the newest drivers to devices.

- **Manage which drivers are approved for deployment**. You can edit any driver update policy to modify which drivers are approved for deployment. You can pause the deployment of any individual driver update to stop its deployment to new devices, and then later reapprove the paused update to enable Windows Update to resume installing it on applicable devices.

Regardless of the policy configuration and the drivers included, only approved drivers can install on devices. Additionally, Windows Update only installs the latest available and approved update when the version is more recent than the one currently installed on the device.

Windows driver update management applies to:

- Windows

## Prerequisites

[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]

[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]

[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]

[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]

[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]


## Architecture

:::image type="content" source="./images/autopatch-ds.png" alt-text="A conceptual diagram of Windows driver update management." lightbox="./images/autopatch-ds.png" border="false":::

**Windows Driver Update Management architecture**:

1. Microsoft Intune provides the Microsoft Entra IDs and Intune policy settings for devices to Windows Autopatch. Intune also provides the list of driver approvals and pause commands to Windows Autopatch.
2. Windows Autopatch configures Windows Updates based on the information provided by Intune. Windows Updates provides the applicable driver update inventory per device ID.
3. Devices send data to Microsoft so that Windows Update can identify the applicable driver updates for a device during its regular Windows Update scans for updates.  Any approved updates install on the device.
4. Windows Autopatch reports Windows diagnostic data back to Intune for reports.

## Plan for driver updates

Before you create policies and manage the approval of drivers in your policies, we recommend constructing a driver update deployment plan that includes team members who can approve driver and firmware updates. Subjects to consider include:

- When to use *automatic* driver approvals vs using *manual* driver approvals.

- Use of deployment rings for driver update policies to limit installation of new driver updates to test groups of devices before broadly installing those updates on all devices. With this approach, your team can identify potential issues in an early ring before deploying updates broadly. Use of rings can provide you with time to pause a troublesome update in subsequent rings to delay or prevent its deployment. Examples of organizational approaches for rings include:

  - Structuring driver update policies for different device and hardware models, aligned with your organizational units, or a combination of both.

  - Using policy deferral periods for automatic updates and the *make available date* for manually approved updates, to align to your update rings for quality and feature updates schedules.

  You might also set the update availability for manually approved updates to match common update cycles like Microsoft's Patch Tuesday release. Alignment of schedules can help reduce extra system restarts that some driver updates require.

- Assign devices to only one driver update policy to help prevent a device from having its drivers managed through more than one policy. This can help avoid having a driver installed by one policy when you previously declined or paused that same update in a separate policy.
For more information about planning deployments, see [Create a deployment plan](/windows/deployment/update/create-deployment-plan) in the Windows deployment documentation.

## Next steps

- [Windows Driver update policies](driver-updates-policy.md)
- [Reports for Windows Driver updates policy](driver-updates-reports.md)
