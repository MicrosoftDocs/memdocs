---
# required metadata

title: Learn about Windows Driver updates policy for Windows 10 Windows 11 devices in Intune
description: Learn about using Microsoft Intune policy to manage Windows driver updates on your Windows 10 and Windows 11 devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 09/10/2024
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
- ContentEnagagementFY24 
- sub-updates
---

# Windows Driver update management in Microsoft Intune

With Windows Driver Update Management in Microsoft Intune, you can review, approve for deployment and pause deployments of driver updates for your managed Windows 10 and Windows 11 devices. Intune and the Windows Update for Business deployment service (DS) take care of the heavy lifting to identify the applicable driver updates for devices that are assigned a driver updates policy. Intune and Windows Autopatch sort updates by categories that help you easily identify the recommended driver updates for all devices, or updates that might be considered optional for more limited use.

Using Windows driver update policies, you remain in control of which driver updates can install on your devices. You can:

- **Enable automatic approvals of recommended driver updates**. Policies set for automatic approval automatically approve and deploy each new driver update version that is considered a *recommended driver* for the devices assigned to the policy. Recommended drivers are typically the latest driver update published by the driver publisher that the publisher has marked as *required*. Drivers that aren't identified as the current recommended driver are also available as *other drivers*, which can be considered to be optional driver updates.

  Later, when a newer driver update from the OEM is released and identified as the current *recommended* driver update, Intune automatically adds it to the policy and moves the previously recommended driver to the list of other drivers.

  > [!TIP]  
  > An approved recommended driver update that is moved to the *other drivers* list due to a newer recommended driver update becoming available, remains approved. When a newer recommended and approved driver update is available, Windows Autopatch will install only that latest approved version. If the latest approved update version is paused, the deployment service will automatically offer the next most recent and approved update version, which is now on the *other drivers* list. This behavior ensures that the last known-good driver update version that was approved can continue to install on devices, while the more recent recommended version remains paused.

  With this policy configuration, you can also choose to review the available updates to selectively approve, pause, or decline *any* update that remains available for devices with the policy.

- **Configure policy to require manual approval of all updates**. This policy ensures that administrators must approve a driver update before it can be deployed. Newer versions of driver updates for devices with this policy are automatically added to the policy but remain inactive until approved.

Later, when a newer driver update from the OEM is recommended for a device in the policy, the policy status updates to indicate there are drivers pending your review. This status becomes a call to action to review the policy and decide if you want to approve deployment of the newest drivers to devices.

- **Manage which drivers are approved for deployment**. You can edit any driver update policy to modify which drivers are approved for deployment. You can pause the deployment of any individual driver update to stop its deployment to new devices, and then later reapprove the paused update to enable Windows Update to resume installing it on applicable devices.

Regardless of the policy configuration and the drivers included, only approved drivers can install on devices. Additionally, Windows Update only installs the latest available and approved update when the version is more recent than the one currently installed on the device.

Windows driver update management applies to:

- Windows 10
- Windows 11

## Prerequisites

> [!IMPORTANT]
> This feature is not supported on GCC cloud environment.
>
> [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea) is not applicable to GCC and GCC High/DoD cloud environments for WuFB-DS capabilities.

To use Windows Driver Update management, your organization must have the following licenses, subscriptions, and network configurations: 

### Subscriptions

- **Intune**: Your tenant requires the *Microsoft Intune Plan 1* subscription.

- **Microsoft Entra ID**: *Microsoft Entra ID Free* (or greater) subscription.

**Windows subscriptions and licenses**:

Your organization must have one of the following subscriptions that include a license for Windows Update for Business deployment service:

- Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows Virtual Desktop Access E3 or E5
- Microsoft 365 Business Premium

*Review your subscription details for applicability to Windows 11*.

If you're blocked when creating new policies for capabilities that require Windows Autopatch and you get your licenses to use Windows Update for Business through an Enterprise Agreement (EA), contact the source of your licenses such as your Microsoft account team or the partner who sold you the licenses. The account team or partner can confirm that your tenants' licenses meet the Windows Autopatch license requirements. See [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea).

### Device & Edition requirements

**Windows editions**:

Driver updates are supported for the following Windows 10/11 editions:

- Pro
- Enterprise
- Education
- Pro for Workstations

> [!NOTE]  
> **Unsupported versions and editions**:  
> *Windows 10/11 Enterprise LTSC*: Feature updates, Driver updates, and Expedited Quality Update policies under Quality updates, available under the **Windows 10 and later** blade don't support the *Long Term Service Channel* (LTSC) release. Plan to use Update rings policies in Intune.

**Devices must**:

- Run a version of Windows 10/11 that remains in support.

- Be enrolled in Intune MDM and be Hybrid AD joined or Microsoft Entra joined.

- Have Telemetry turned on and configured to report a minimum data level of *Basic* as defined in [Changes to Windows diagnostic data collection](/windows/privacy/changes-to-windows-diagnostic-data-collection) in the Windows documentation.  

  You can use one of the following Intune device configuration profile paths to configure Telemetry for Windows 10 or Windows 11 devices:
  - **[Device restriction template](../configuration/device-restrictions-windows-10.md)**: With this profile, set **Share usage data** to **Required**. *Optional* is also supported.
  - **[Settings catalog](../configuration/settings-catalog.md)**: From the Settings catalog, add **Allow Telemetry** from the **System** category, and set it to **Basic**. *Full* is also supported.

  For more information about Windows Telemetry settings, including both current and past setting options from Windows, see [Changes to Windows diagnostic data collection](/windows/privacy/changes-to-windows-diagnostic-data-collection) in the Windows documentation.

- The *Microsoft Account Sign-In Assistant* (wlidsvc) must be able to run. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.

- Have access to the network endpoints required by Intune managed devices. See [Network endpoints](../fundamentals/intune-endpoints.md#access-for-managed-devices).

### Enable data collection for reports

To support reports for Windows Driver updates, you must enable the use of Windows diagnostic data in Intune. It's possible that diagnostic data is already enabled for other reports, like Windows Feature updates and Expedited Quality update reports.
To enable the use of Windows diagnostic data:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Connectors and tokens** > **Windows data**.

2. Expand *Windows data* and ensure the setting **Enable features that require Windows diagnostic data in processor configuration** is toggled to **On**.

For more information, see [Enable use of Windows diagnostic data by Intune](data-enable-windows-data.md).

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

### Limitations for Workplace Joined devices

Intune policies for *Driver updates for Windows 10 and later* require the use of Windows Update for Business and [Windows Update for Business deployment service](/windows/deployment/update/deployment-service-overview#capabilities-of-the-windows-update-for-business-deployment-service) (WUfB ds). Where Windows Update for Business supports WPJ devices, Windows Update for Business ds provides for other capabilities that aren't supported for WPJ devices.

For more information about WPJ limitations for Intune Windows Update policies, see [Policy limitations for Workplace Joined devices](windows-update-for-business-configure.md) in *Manage Windows 10 and Windows 11 software updates in Intune*.

## Architecture

:::image type="content" source="./media/windows-driver-updates-overview/wdum-architecture.png" alt-text="A conceptual diagram of Windows Driver Update Management." lightbox="./media/windows-driver-updates-overview/wdum-architecture.png":::
  
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

## Frequently Asked Questions

### Do policies for driver updates support Assignment Filters?

- No. Driver Updates aren't currently supported with Assignment Filters.

### Can I apply driver updates policy during Autopilot?

- No. Driver Updates aren't supported during autopilot at this time.

### Can I use policy to roll back a driver update?

- No. Windows Update for Business doesn't currently support Driver rollback. While rollback could be scripted, there are too many potential variables to provide a useful sample script for doing so. If you must remove a driver, consider manual methods like PowerShell.

To help avoid issues that require rolling back a driver from large numbers of devices, use *deployment rings* to limit driver installation to small initial groups of devices. This approach allows time to evaluate the success or compatibility of a driver before broadly deploying it across your organization.

- For policies with manual approvals, you must review and manually approve each driver before it can deploy to devices. While more work than policies with automatic approvals, manual approval can help avoid issues with automatically approved drivers.
- If you use policies with automatic approval, plan to monitor the policy for early signs of problems. If a driver update problem is identified in an early deployment ring, you can then pause that same update in your other policies.

### Can I manage a device through multiple driver update policies?

- While the use of multiple policies per device is supported, we don't recommend doing so. Instead, we recommend adding devices to a single policy to avoid confusion about whether a driver for a device is or isn't approved.

  Consider a device that receives driver updates from two policies. In one policy, a specific update is approved and in the other policy, that update is paused. Because the status of *approved* always wins, the driver installs on the device despite any other status for that update that is set in any other policy.

### How can I reduce reboots on devices that receive driver updates?

- Because it's not always clear in advance when an OEM releases a new update, or if that update requires a reboot, consider a regular pattern of update reviews.

  - For policies with manual approval, when you approve drivers and set an *approval available date*, you can set that date to an event like the monthly Patch Tuesday, or any other time of your choosing. 
  - For policies with automatic approval, you could pause a newly added and then return to approve it. When you reapprove any paused update, you can set an *approval available date*.

  To help mitigate this type of recurring challenge, we're evaluating changes that can mitigate the need to manually coordinate driver updates with *Patch Tuesday* updates.

### Why has a driver disappeared from the list of available drivers in my policy?

- When an OEM replaces a driver with a new recommended driver, the older driver can be moved to the *Other drivers* category. However, if that older driver is the same version or older than the drivers in use by all devices, that driver is entirely removed from the policy as there are no devices that can install it through Driver updates policies.

### How do I remove older drivers from the driver list of my policies?

- To ensure that the list of available drivers is up-to-date, drivers with older versions than those already installed across all devices targeted by a policy are no longer applicable. These older drivers are removed from the driver list of previously deployed and active policies. Only drivers that can update the driver version currently installed on a device targeted by a policy remain available in the policy.

  Installing drivers with older versions than those already present on a device isn't possible through driver update management.

### What is the Windows Autopatch synchronization frequency?

- Intune to Windows Autopatch syncs run each day, and you can use the *Sync* option to run a synchronization on demand. The time to complete a synchronization depends on the device information involved but should usually take only a few minutes to complete.

  Devices sync with the Windows Autopatch service each day when the device runs a Windows Update scan.

### What drivers are available to be managed?

- Any driver updates that are currently published to Windows Update and applicable to one or more devices in the policy are available through driver updates policies.

### What about drivers that update a BIOS that is password locked. How does this work?

- Updates that are published to Windows Update have a requirement to use a Windows mechanism that enables securely updating the firmware or driver without requiring the BIOS/UEFI to be unlocked.

### If a vendor has their own app for scanning and installing driver and firmware updates, is there a delay in update availability between their app and Windows Autopatch?

- The possibility of a delay depends on the vendor or OEM who determines the availability of their updates. Because driver updates are digitally signed by the same portal before they're published to Windows Updates, driver updates might become available through Windows Update before they become available via the vendors tools.

### Why do my devices have driver updates installed that didn't pass through an updates policy?

- These are likely *extension* drivers, which are "sub drivers" that a main driver can reference to be installed when the main driver is installed or updated. Extension drivers show up in the installed drivers or update history on the device, but aren't directly manageable. Because extension drivers don't function without base drivers, it's safe to allow them to install.
- Plug and Play can also install drivers automatically. When Windows detects new hardware or software (such as a mouse, keyboard, or webcam) without an existing driver, it installs the latest driver to ensure the component functions immediately. After the initial installation, any future updates to these drivers will require approval.

### How quickly are paused updates actually paused?

- Pause is a best effort, and when an update is paused, Windows Autopatch removes the approval. However, devices won't know that an update is paused until it's next scan for updates.
  - If a device hasn't yet scanned for the update, then the paused update isn't offered, and *Pause* works as expected.
  - If a device scans for updates and discovers an update is paused and that the device is in the process of downloading, installing, or waiting to restart, then Windows Update on the device attempts a "best effort" to remove that driver update from being installed. If it can't halt the installation, the update completes its installation.
  - If an update completes its installation before the next scan for updates, nothing happens, and the update remains installed.

### Where can I learn more about the available drivers?

- You can get more information about drivers by copying the name and searching the catalog.update.microsoft.com website.

### Do driver updates policies update drivers for plug-in devices?

- Yes, if the driver updates are published to Windows Update by the OEM vendor.

### Which driver updates can my device users see?

- After a device is assigned to a driver update policy, optional drivers aren't shown to the end user. When the admin approves a driver update, it effectively becomes "required" and installs the next time the device scans for updates.

### How do I use driver management if I'm currently using Configuration Manager for updates?

You can continue to use Configuration Manager for updates other than Drivers, or start to move other update types to cloud management in Intune one at a time. To do this, first, enable [cloud attach](../../configmgr/cloud-attach/overview.md) or co-management in your Configuration Manager hierarchy to enroll your managed devices in Intune.

The recommended and preferred path to embrace cloud based updates is to move the [Windows Update](../../configmgr/comanage/workloads.md#windows-update-policies) workload to Intune. If your organization isn't ready for this, you can use the Driver and Firmware management capability in Intune without moving the workload by completing the following steps:

> [!NOTE]
> The following procedure only works and is supported for managed Windows 11 devices. For Windows 10 devices, we recommend moving the Windows Update workload in the Configuration Manager co-management settings to Intune. Alternatively, configure the Windows Update workload to the Pilot setting and specify a collection containing the in-scope Windows 10 managed devices.

   1. Leave the [Windows Update](../../configmgr/comanage/workloads.md#windows-update-policies) workload set to Configuration Manager.

   2. Configure your driver policies in Intune to enroll devices and get them ready for management as detailed at [Manage policy for Windows Driver updates with Microsoft Intune](windows-driver-updates-policy.md).

   3. Configure a domain-based group policy to configure **Windows Update** as the source for **Driver Updates** using the [Specify source for specific classes of Windows Updates policy](/windows/deployment/update/wufb-wsus).

      > [!NOTE]
      > Because Configuration Manager uses a local group policy to configure the update source policy, using Intune or a CSP to attempt to configure these same settings result in an undefined and unpredictable device state.

   4. Enable [data collection](windows-update-reports.md#configuring-for-client-data-reporting) in Intune for devices that you wish to deploy drivers and firmware to.

   5. [Optional] Enforce allowing diagnostic data submission using a policy. Diagnostic data submission to Microsoft enables the use of [Windows Update reports for Microsoft Intune](windows-update-reports.md).

      > [!NOTE]
      > By default, diagnostic data submission to Microsoft is allowed on Windows devices. Disabling diagnostic data collection prevents the use of Windows Update reports for Microsoft Intune from reporting any update information for your managed devices.

      Configure the **Allow Diagnostic data** setting to **Optional** or **Required** using a domain-based group policy or Intune. For more information on how to complete this task, go to:

         - [Use Group Policy to manage diagnostic data collection](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#use-group-policy-to-manage-diagnostic-data-collection)
         
         - [Use MDM to manage diagnostic data collection](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#use-mdm-to-manage-diagnostic-data-collection)

   6. [Optional] Enable device name collection in diagnostic data. For more information on configuration using a domain-based group policy or Intune, see [Diagnostic data requirements](/windows/deployment/update/wufb-reports-prerequisites#diagnostic-data-requirements).

      > [!NOTE]
      > Using Intune to configure any of the diagnostic data settings mentioned earlier requires that you move the [Device Configuration](../../configmgr/comanage/workloads.md#device-configuration) co-management workload to Intune.

   You can move Feature update management to the cloud in Intune by configuring a [Feature update](windows-10-feature-updates.md) policy in Intune and setting the **Feature Updates** setting to **Windows Update** using the [Specify source for specific classes of Windows Updates policy](/windows/deployment/update/wufb-wsus) group policy.
   
   Using Update Ring policies in Intune for Quality or Feature Updates requires you to move the **Windows Update** workload to Intune.

### Is there a way to set a deadline for drivers?

The Quality Update deadline and grace period settings apply to drivers.

Here are some more details on when deadlines are applied to drivers:

- A driver is approved to be made available (manually or automatically) on a date. This is shown as the First Deployment.
- On first or initial scan the approved driver is offered to the device. The date the client's update scan initially discovered the update is also the start date and time for the deadline.
- The deadline calculation for both quality and feature updates is based off the time the client's update scan initially discovered the update. See [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines)

### How do I set deferrals for drivers?

- The deferral period set for Quality Updates within the Update Rings policy does not apply to drivers that are approved using the Driver Update Policy. Instead, use the deferral setting in the Driver policy to set a deferral.  In fact, using multiple driver policies with different deferral settings to create driver deployment rings is highly recommended. Remember to only assign a device to one driver policy.

### Are the user experience settings from an Update Ring policy applied for driver updates?

- Yes, user experience settings such as automatic update behavior, active hours, notifications, and so on, are applied for driver updates as well.

### Why does it take up to 24 hours for the driver update inventory to be returned?

- To make driver inventory available, there are several steps that must be completed. The most important is that after the policy is submitted and devices are enrolled for management, Windows Updates must wait for each device to do its daily scan for updates. This process occurs daily, so it can take up to 24 hours for all healthy devices to check in. After this, Intune needs to process the results of the scan to provide the inventory of available driver updates.

## Next steps

- [Create a Windows driver update policy](windows-driver-updates-policy.md)
- [Use Windows driver update reports](windows-update-reports.md#reports-for-windows-driver-updates-policy)
