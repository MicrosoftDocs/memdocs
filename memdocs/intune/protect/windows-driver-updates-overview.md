---
# required metadata

title: Learn about Windows Driver updates policy for Windows 10 Windows 11 devices in Intune
description: Learn about using Microsoft Intune policy for Windows driver updates to manage driver updates on your Windows 10 and Windows 11 devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davguy; davidmeb; bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Windows Driver update management in Microsoft Intune

With Windows Driver Update Management in Microsoft Intune, you can review, approve for deployment and pause deployments of driver updates for your managed Windows 10 and Windows 11 devices. Intune and the Windows Update for Business (WUfB) deployment service (DS) take care of the heavy lifting to identify the applicable driver updates for devices that are assigned a driver updates policy. Intune and WUfB-DS sort updates by categories that help you easily identify the recommended driver updates for all devices, or updates that might be considered optional for more limited use.

Using Windows driver update policies, you remain in control of which driver updates install on your devices. You can:

- **Enable automatic approvals of recommended driver updates**. Policies set for automatic approval automatically approve and deploy each new driver update version that is considered a *recommended driver* for the devices assigned the policy. Recommended drivers are typically the latest driver update published by the driver publisher that the publisher has marked as *required*. Drivers that aren't identified as the current recommended driver are also available as *other drivers*.

  Later, when a newer driver update from the OEM is released and identified as the current *recommended* driver update, Intune automatically adds it to the policy and moves the previous recommended driver to the list of other drivers.

  > [!TIP]  
  > An approved recommended driver update that is moved to the *other drivers* list due to a newer recommended driver update becoming available, remains approved. When a newer recommended and approved driver update is available, WUfB-DS will install only that latest approved version. If the latest approved update version is paused, the deployment service will automatically offer the next most recent and approved update version, which is now on the *other drivers* list. This behavior ensures that the last known-good driver update version that was approved can continue to install on devices, while the more recent recommended version remains paused.

  With this policy configuration, you can also choose to review the available updates to selectively approve, pause, or decline *any* update that remains available for devices with the policy.

- **Configure policy to require manual approval of all updates**. This policy ensures that administrators must approve a driver update before it can be deployed. Newer versions of driver updates for devices with this policy are automatically added to the policy but remain inactive until approved.

Later, when a newer driver update from the OEM is recommended for a device in the policy, the policy status updates to indicate there are drivers pending your review. This status becomes a call to action to review the policy and decide if you want to approve deployment of the newest drivers to devices.

- **Manage which drivers are approved for deployment**. You can edit any driver update policy to modify which drivers are approved for deployment. You can pause the deployment of any individual driver update to stop its deployment to new devices, and then later reapprove the paused update to enable Windows Update to resume installing it on applicable devices.

Regardless of the policy configuration and the drivers included, only approved drivers can install on devices. Additionally, Windows Update only installs the latest available and approved update when the version is more recent than the one currently installed on the device.

Windows driver update management applies to:

- Windows 10
- Windows 11

## Prerequisites

To use Windows Driver Update management, your organization must have the following licenses, subscriptions, and network configurations: 

### Subscriptions

- **Intune**: Your tenant requires the *Microsoft Intune Plan 1* subscription.

- **Azure Active Directory (Azure AD)**: *Azure AD Free* (or greater) subscription.

### Device & Edition requirements

**Windows subscriptions and licenses**:

Your organization must have one of the following subscriptions that include a license for Windows Update for Business deployment service:

- Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows Virtual Desktop Access E3 or E5
- Microsoft 365 Business Premium

*Review your subscription details for applicability to Windows 11*.

If you’re blocked when creating new policies for capabilities that require WUfB-DS and you get your licenses to use WUfB through an Enterprise Agreement (EA), contact the source of your licenses such as your Microsoft account team or the partner who sold you the licenses. The account team or partner can confirm that your tenants’ licenses meet the WUfB-DS license requirements. See [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea).

**Windows editions**:

Driver updates are supported for the following Windows 10/11 editions:

- Pro
- Enterprise
- Education
- Education
- Pro for Workstations

> [!NOTE]  
> **Unsupported versions and editions**:  
> *Windows 10/11 Enterprise LTSC*: Windows Update for Business (WUfB) does not support the *Long Term Service Channel* release. Plan to use alternative patching methods, like WSUS or Configuration Manager.

**Devices must**:

- Run a version of Windows 10/11 that remains in support.

- Be enrolled in Intune MDM and be Hybrid AD joined or Azure AD joined.

- Have Telemetry turned on, with a minimum setting of [*Required*](../configuration/device-restrictions-windows-10.md#reporting-and-telemetry).

  Configure Telemetry as part of a Device Restriction policy for Windows 10/11. In the device restriction profile, under *Reporting and Telemetry*, configure **Share usage data** to use a minimum value of **Required**. Required is the default value. Values of **Enhanced (1903 and earlier)** or **Optional** are also supported. Devices with a value of *None* don't report the data that is required for driver updates policy.

- The *Microsoft Account Sign-In Assistant* (wlidsvc) must be able to run. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.

- Have access to the network endpoints required by Intune managed devices. See [Network endpoints](../fundamentals/intune-endpoints.md#access-for-managed-devices).

### Enable data collection for reports

To support reports for Windows Driver updates, you must enable the use of Windows diagnostic data in Intune. Its possible use of diagnostic data is already enabled for other reports, like Windows Feature updates and Expedited Quality update reports.
To enable use of Windows diagnostic data:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=210943) and go to **Tenant administration** > **Connectors and tokens** > **Windows data**.

2. Expand *Windows data* and ensure **Enable features that require Windows diagnostic data in processor configuration** is toggled to **On**.

For more information, see [Enable use of Windows diagnostic data by Intune](../protect/data-enable-windows-data.md).

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

For more information, see [Role-based access control for Microsoft Intune](../fundamentals/role-based-access-control.md).

## Architecture

:::image type="content" source="./media/windows-driver-updates-overview/wdum-architecture.png" alt-text="A conceptual diagram of Windows Driver Update Management." lightbox="./media/windows-driver-updates-overview/wdum-architecture.png":::
  
**Windows Driver Update Management architecture**:

1. Microsoft Intune provides Device Azure Active Directory IDs and Intune policy settings to WUfB-DS. Intune also provides the list of driver approvals and pause commands to WUfB-DS.
2. WUfB-DS configures Windows Updates based on the information provided by Intune. Windows Updates provides the applicable driver update inventory per device ID.
3. Devices send data to Microsoft so that Windows Update can identify the applicable driver updates for a device during its regular Windows Update scans for updates.  Any approved updates install on the device.
4. WUfB-DS reports Windows diagnostic data back to Intune for reports.

## Plan for driver updates

Before you create policies, and manage the approval of drivers in your policies, we recommend constructing a driver update deployment plan. 
Subjects to consider include:

- When to use *automatic* driver approvals vs using *manual* driver approvals.

- Use of deployment rings for driver update policies to limit installation of new driver updates to test groups of devices before broadly installing those updates on all devices. With this approach, your team can identify potential issues in an early ring before deploying updates broadly. Use of rings can provide you with time to pause a troublesome update in subsequent rings to delay or prevent its deployment. Examples of organizational approaches for rings include:

  - Structuring driver update policies for different device and hardware models, aligned with your organizational units, or a combination of both.
  - Using policy deferral periods for automatic updates and the *make available date* for manually approved updates, to align to your update rings for quality and feature updates schedules.

You might also set the update availability for manually approved updates to match common update cycles like Microsoft’s Patch Tuesday release. Alignment of schedules can help reduce extra system restarts that some driver updates require.

- Assign devices to only one driver update policy to help prevent a device from having its drivers managed through more than one policy. This can help avoid having a driver installed by one policy when you previously declined or paused that same update in a separate policy. 
For more information about planning deployments, see [Create a deployment plan](/windows/deployment/update/create-deployment-plan) in the Windows deployment documentation.

## Frequently asked Questions

### Do policies for driver updates support Assignment Filters?

- No. Driver Updates aren't currently supported with Assignment Filters.

### Can I use policy to roll back a driver update?

- No. WUfB doesn't currently support Driver rollback. While rollback could be scripted, there are too many potential variables to provide a useful sample script for doing so. If you must remove a driver, consider manual methods like PowerShell.

To help avoid issues that require rolling back a driver from large numbers of devices, use *deployment rings* to limit driver installation to small initial groups of devices. This approach allows time to evaluate the success or compatibility of a driver before broadly deploying it across your organization.

- For policies with manual approvals, you must review and manually approve each driver before it can deploy to devices. While more work than policies with automatic approvals, manual approval can help avoid issues with automatically approved drivers.
- If you use policies with automatic approval, plan to monitor the policy for early signs of problems. If a driver update problem is identified in an early deployment ring, you can then pause that same update in your other policies.

### Can I manage a device through multiple driver update policies?

- While use of multiple policies per device is supported, we don’t recommend doing so. Instead, we recommend adding devices to a single policy to avoid confusion of whether a driver for a device is or isn’t approved.

  Consider a device that receives driver updates from two policies. In one policy, a specific update is approved and in the other policy, that update is paused. Because the status of *approved* always wins, the driver installs on the device despite any other status for that update that is set in other policy.

### How can I reduce reboots on devices that receive driver updates?

- Because it’s not always clear in advance when an OEM releases a new update, or if that update requires a reboot, consider a regular pattern of update reviews. For policies with manual approval, when you approve drivers and set an *approval available date*, you can set that date to an event like the monthly Patch Tuesday, or any other time of your choosing. For policies with automatic approval, you could pause a newly added and then return to approve it. When you reapprove any paused update, you can set an *approval available date*.

  To help mitigate this type of recurring challenge, we're evaluating changes that can mitigate the need to manually coordinate driver updates with Patch Tuesday updates.

### Why has a driver disappeared from the list of available drivers my policy?

- When an OEM replaces a driver with a new recommended driver, the older driver can be moved to the *Other drivers* category. However, if that older driver is the same version or older than the drivers in use by all devices, that driver is entirely removed from the policy as there are no devices that can install it through Driver updates policies.

### How do I remove older drivers from the driver list of my policies?

- To ensure that the list of available drivers is up-to-date, drivers with older versions that than those already installed across all devices targeted by a policy are no longer applicable. These older drivers are removed from the driver list of previously deployed and active policies. Only drivers that can update the driver version currently installed on a device targeted by a policy remain available in the policy.

  Installing drivers with older versions than those already present on a device isn't possible through driver update management.

### What is the WUfB-DS synchronization frequency?

- Intune to WUfB-DS syncs run each day, and you can use the *Sync* option to run a synchronization on demand. The time to complete a synchronization depends on the device information involved but should usually take only a few minutes to complete.

  Devices sync with the WUfB-DS service each day when the device runs a Windows Update scan.

### What drivers are available to be managed?

- Any driver updates that are currently published to Windows Update and applicable to one or more devices in the policy are available through driver updates policies.

### What about drivers that update a BIOS that is password locked. How does this work?

- Updates that are published to Windows Update have a requirement to use a Windows mechanism that enables securely updating the firmware or driver without requiring the BIOS/UEFI to be unlocked.

### If a vendor has their own app for scanning and installing driver and firmware updates, is there a delay for update availability between their app and WUfB-DS?

- The possibility of a delay depends on the vendor or OEM who determines the availability of their updates. Because driver updates are digitally signed by the same portal before they're published to Windows Updates, it’s possible that a driver update becomes available through Windows Update before they become available via the vendors tools.

### Why do my devices have driver updates installed that didn't pass through an updates policy?

- These are likely *extension* drivers, which are “sub drivers” that a main driver can reference to be installed when the main driver is installed or updated. Extension drivers show up in the installed drivers or update history on the device, but aren't directly manageable.

### How quickly are paused updates actually paused?

- Pause is a best effort, and when an update is paused, WUfB-DS removes the approval. However, devices won’t know that an update is paused until it’s next scan for updates.
  - If a device hasn't yet scanned for the update, then the paused update isn’t offered, and *Pause* works as expected.
  - If a device scans for updates and discovers an update is paused that the device is in the process of downloading, installing, or waiting to restart, then Windows Update on the device attempts a “best effort” to remove that driver update from being installed. If it can't halt the install, the update completes its installation.
  - If an update completes its installation before the next scan for updates, nothing happens, and the update remains installed.

### Where can I learn more about the available drivers?

- You can get more information about drivers by copying the name and searching the catalog.update.microsoft.com website.

### How can I minimize device reboots when using driver updates policy?

- When you manually approve a driver or reapprove a paused driver, you can set the updates *approval available date* to be the date of the next *Patch Tuesday* event.

### Do driver updates policies update drivers for plug-in devices?

- Yes, if the driver updates are published to Windows Update by the OEM vendor.

### Which driver updates can my device users see?

- After a device is assigned to a driver update policy, optional drivers aren't shown to the end user. When the admin approves a driver update, it effectively becomes “required” and installs the next time the device scans for updates.

### How do I use driver management if I’m currently using Configuration Manager for updates?

- You can continue to use Configuration Manager for updates other than Drivers, or to start to move other update types to cloud management in Intune one at a time. First, ensure you're using [cloud attach](/mem/configmgr/cloud-attach/overview) or co-management, so that your devices are enrolled in Intune. Then, configure your driver policies in Intune to enroll devices and get them ready for management. After approximately one day, [set the policy]( /windows/client-management/mdm/policy-csp-update#setpolicydrivenupdatesourcefordriverupdates) *SetPolicyDrivenUpdateSourceForDriverUpdates* to a value of **0**, to scan for driver updates from Windows Update.

  > [!NOTE]  
  > You can move Feature update management to the cloud in Intune by using other similar policies. If using Update Ring policies in Intune, such as for Quality Updates, you also need enable co-management and assign the Windows Updates workload to Intune, or a pilot collection.

### Is there a way to set a deadline for drivers?

- The Quality Update deadline and grace period settings apply to drivers. The deadline starts from the time the driver is first offered to the device.

### Why does it take up to 24 hours for driver update inventory to be returned?

- To make driver inventory available, there are several steps that must be completed. The most important is that after the policy is submitted and devices are enrolled for management, Windows Updates must wait for each device to do its daily scan for updates. This process occurs daily, so it can take up to 24 hours for all healthy devices to check in. After this, Intune needs to process the results of the scan to provide the inventory of available driver updates.

## Next steps

- [Create Windows driver update policy](../protect/windows-driver-updates-policy.md)
- [Use Windows driver update reports](../protect/windows-update-reports.md#reports-for-windows-driver-updates-policy)