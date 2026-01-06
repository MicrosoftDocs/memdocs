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

> [!IMPORTANT]
> This feature isn't supported on GCC cloud environment.
>
> [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea) isn't applicable to GCC and GCC High/DoD cloud environments for Windows Autopatch capabilities.

To use Windows Driver Update management, your organization must have the following licenses, subscriptions, and network configurations:

### Subscriptions

- **Intune**: Your tenant requires the *Microsoft Intune Plan 1* subscription.

- **Microsoft Entra ID**: *Microsoft Entra ID Free* (or greater) subscription.

**Windows subscriptions and licenses**:

Your organization must have one of the following subscriptions that include a license for Windows Autopatch:

- Windows Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows Virtual Desktop Access E3 or E5
- Microsoft 365 Business Premium

*Review your subscription details for applicability to Windows 11*.

If you're blocked when creating new policies for capabilities that require Windows Autopatch and you get your licenses to use Windows Update client policies through an Enterprise Agreement (EA), contact the source of your licenses such as your Microsoft account team or the partner who sold you the licenses. The account team or partner can confirm that your tenants' licenses meet the Windows Autopatch license requirements. See [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea).

### Device & Edition requirements

**Windows editions**:

Driver updates are supported for the following Windows editions:

- Pro
- Enterprise
- Education
- Pro for Workstations

> [!NOTE]
> **Unsupported versions and editions**:
> *Windows Enterprise LTSC*: Feature updates, Driver updates, and Expedited Quality Update policies under Quality updates, don't support the *Long Term Service Channel* (LTSC) release. Plan to use Update rings policies in Intune.


:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> Feature update policies supports devices that are:
> - Enrolled in Intune
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
>
> Devices must also meet the following requirements:
> - Telemetry must be turned on, with a minimum setting of [*Required*](../../intune-service/configuration/device-restrictions-windows-10.md#reporting-and-telemetry).
>    Devices that receive a feature updates policy and that have Telemetry set to *Not configured* (off), might install a later version of Windows than defined in the feature updates policy.
>
>    To configure Telemetry as using the Settings catalog:
> 
>    1. [Create a Settings catalog policy](/intune/intune-service/configuration/settings-catalog) for the Windows platform and use the following setting:
> 
>      | Category | Setting name | Value |
>      |--|--|--|
>      | **System** | Allow Telemetry | **Basic** or **Full** |
> 
>     1. Assign the policy to a group that contains as members the devices that you want to configure.
> 
> - The *Microsoft Account Sign-In Assistant* (wlidsvc) must be able to run. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.
> - Have access to endpoints. To get a detailed list of endpoints required for the associated services listed here, see [Network endpoints](../../intune-service/fundamentals/intune-endpoints.md#access-for-managed-devices).
>    - [Windows Update](/windows/privacy/manage-windows-1809-endpoints#windows-update)
>    - Windows Autopatch

:::column-end:::
:::row-end:::


### GCC High support

Intune policy for Driver Updates isn't currently supported with GCC High environments.

### RBAC requirements

To manage Windows Driver updates, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permissions:

- **Device configurations**:
  - Assign
  - Create
  - Delete
  - View Reports
  - Update
  - Read

You can add the *Device configurations* permission with one or more rights to your own custom RBAC roles or use one the built-in **Policy and Profile manager** role, which includes these rights.

For more information, see [Role-based access control for Microsoft Intune](../../intune-service/fundamentals/role-based-access-control.md).

### Limitations for Workplace Joined devices

Intune policies for *Driver updates* require the use of Windows Update client policies and [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). Where Windows Update client policies supports WPJ devices, Windows Autopatch provides for other capabilities that aren't supported for WPJ devices.

For more information about WPJ limitations for Intune Windows Update policies, see [Policy limitations for Workplace Joined devices](configure.md).

## Architecture

:::image type="content" source="./images/driver-updates/wdum-architecture.png" alt-text="A conceptual diagram of Windows Driver Update Management." lightbox="./images/driver-updates/wdum-architecture.png":::

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

- [Create a Windows driver update policy](driver-updates-policy.md)
- [Use Windows driver update reports](reports.md#reports-for-windows-driver-updates-policy)
