---
title: Windows driver updates policy frequently asked questions
description: Frequently asked questions about Windows driver updates policies in Microsoft Intune.
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: davguy; davidmeb; bryanke
---

# Driver updates frequently asked questions

## Do policies for driver updates support Assignment Filters?

- No. Driver Updates aren't currently supported with Assignment Filters.

## Can I apply driver updates policy during Windows Autopilot?

- No. Driver Updates aren't supported during Windows Autopilot at this time.

> [!NOTE]
> Windows applies critical updates during Windows Autopilot. These updates may include critical driver updates that have not yet been approved by an admin.

## Can I use policy to roll back a driver update?

- No. Windows Update client policies don't currently support driver rollback. While rollback could be scripted, there are too many potential variables to provide a useful sample script for doing so. If you must remove a driver, consider manual methods like PowerShell.

To help avoid issues that require rolling back a driver from large numbers of devices, use *deployment rings* to limit driver installation to small initial groups of devices. This approach allows time to evaluate the success or compatibility of a driver before broadly deploying it across your organization.

- For policies with manual approvals, you must review and manually approve each driver before it can deploy to devices. While more work than policies with automatic approvals, manual approval can help avoid issues with automatically approved drivers.
- If you use policies with automatic approval, plan to monitor the policy for early signs of problems. If a driver update problem is identified in an early deployment ring, you can then pause that same update in your other policies.

## Can I manage a device through multiple driver update policies?

- While the use of multiple policies per device is supported, we don't recommend doing so. Instead, we recommend adding devices to a single policy to avoid confusion about whether a driver for a device is or isn't approved.

  Consider a device that receives driver updates from two policies. In one policy, a specific update is approved and in the other policy, that update is paused. Because the status of *approved* always wins, the driver installs on the device despite any other status for that update that is set in any other policy.

## How can I reduce reboots on devices that receive driver updates?

- Because it's not always clear in advance when an OEM releases a new update, or if that update requires a reboot, consider a regular pattern of update reviews.

  - For policies with manual approval, when you approve drivers and set an *approval available date*, you can set that date to an event like the monthly Patch Tuesday, or any other time of your choosing.
  - For policies with automatic approval, you could pause a newly added and then return to approve it. When you reapprove any paused update, you can set an *approval available date*.

  To help mitigate this type of recurring challenge, we're evaluating changes that can mitigate the need to manually coordinate driver updates with *Patch Tuesday* updates.

## Why has a driver disappeared from the list of available drivers in my policy?

- When an OEM replaces a driver with a new recommended driver, the older driver can be moved to the *Other drivers* category. However, if that older driver is the same version or older than the drivers in use by all devices, that driver is entirely removed from the policy as there are no devices that can install it through Driver updates policies.

## How do I remove older drivers from the driver list of my policies?

- To ensure that the list of available drivers is up-to-date, drivers with older versions than those already installed across all devices targeted by a policy are no longer applicable. These older drivers are removed from the driver list of previously deployed and active policies. Only drivers that can update the driver version currently installed on a device targeted by a policy remain available in the policy.

  Installing drivers with older versions than those already present on a device isn't possible through driver update management.

## What is the Windows Autopatch synchronization frequency?

- Intune to Windows Autopatch syncs run each day, and you can use the *Sync* option to run a synchronization on demand. The time to complete a synchronization depends on the device information involved but should usually take only a few minutes to complete.

  Devices sync with the Windows Autopatch service each day when the device runs a Windows Update scan.

## What drivers are available to be managed?

- Any driver updates that are currently published to Windows Update and applicable to one or more devices in the policy are available through driver updates policies.

## What about drivers that update a BIOS that is password locked. How does this work?

- Updates that are published to Windows Update have a requirement to use a Windows mechanism that enables securely updating the firmware or driver without requiring the BIOS/UEFI to be unlocked.

## If a vendor has their own app for scanning and installing driver and firmware updates, is there a delay in update availability between their app and Windows Autopatch?

- The possibility of a delay depends on the vendor or OEM who determines the availability of their updates. Because driver updates are digitally signed by the same portal before they're published to Windows Updates, driver updates might become available through Windows Update before they become available via the vendors tools.

## Why do my devices have driver updates installed that didn't pass through an updates policy?

- These are likely *extension* drivers, which are "sub drivers" that a main driver can reference to be installed when the main driver is installed or updated. Extension drivers show up in the installed drivers or update history on the device, but aren't directly manageable. Because extension drivers don't function without base drivers, it's safe to allow them to install.
- Plug and Play can also install drivers automatically. When Windows detects new hardware or software (such as a mouse, keyboard, or webcam) without an existing driver, it installs the latest driver to ensure the component functions immediately. After the initial installation, any future updates to these drivers will require approval.

## How quickly are paused updates actually paused?

- Pause is a best effort, and when an update is paused, Windows Autopatch removes the approval. However, devices won't know that an update is paused until it's next scan for updates.
  - If a device hasn't yet scanned for the update, then the paused update isn't offered, and *Pause* works as expected.
  - If a device scans for updates and discovers an update is paused and that the device is in the process of downloading, installing, or waiting to restart, then Windows Update on the device attempts a "best effort" to remove that driver update from being installed. If it can't halt the installation, the update completes its installation.
  - If an update completes its installation before the next scan for updates, nothing happens, and the update remains installed.

## Where can I learn more about the available drivers?

- You can get more information about drivers by copying the name and searching the catalog.update.microsoft.com website.

## Do driver updates policies update drivers for plug-in devices?

- Yes, if the driver updates are published to Windows Update by the OEM vendor.

## Which driver updates can my device users see?

- After a device is assigned to a driver update policy, optional drivers aren't shown to the end user. When the admin approves a driver update, it effectively becomes "required" and installs the next time the device scans for updates.

## How do I use driver management if I'm currently using Configuration Manager for updates?

You can continue to use Configuration Manager for updates other than Drivers, or start to move other update types to cloud management in Intune one at a time. To do this, first, enable [cloud attach](../../configmgr/cloud-attach/overview.md) or co-management in your Configuration Manager hierarchy to enroll your managed devices in Intune.

The recommended and preferred path to embrace cloud based updates is to move the [Windows Update](../../configmgr/comanage/workloads.md#windows-update-policies) workload to Intune. If your organization isn't ready for this, you can use the Driver and Firmware management capability in Intune without moving the workload by completing the following steps:

> [!NOTE]
> The following procedure only works and is supported for managed Windows 11 devices. For Windows 10 devices, we recommend moving the Windows Update workload in the Configuration Manager co-management settings to Intune. Alternatively, configure the Windows Update workload to the Pilot setting and specify a collection containing the in-scope Windows 10 managed devices.

   1. Leave the [Windows Update](../../configmgr/comanage/workloads.md#windows-update-policies) workload set to Configuration Manager.
   2. Configure your driver policies in Intune to enroll devices and get them ready for management as detailed at [Manage policy for Windows Driver updates with Microsoft Intune](driver-updates-policy.md).
   3. Configure a domain-based group policy to configure **Windows Update** as the source for **Driver Updates** using the [Specify source for specific classes of Windows Updates policy](/windows/deployment/update/wufb-wsus).
      > [!NOTE]
      > Because Configuration Manager uses a local group policy to configure the update source policy, using Intune or a CSP to attempt to configure these same settings result in an undefined and unpredictable device state.
   4. Enable [data collection](driver-updates-reports.md#configuring-for-client-data-reporting) in Intune for devices that you wish to deploy drivers and firmware to.
   5. [Optional] Enforce allowing diagnostic data submission using a policy. Diagnostic data submission to Microsoft enables the use of [Windows Update reports for Microsoft Intune](driver-updates-reports.md).
      > [!NOTE]
      > By default, diagnostic data submission to Microsoft is allowed on Windows devices. Disabling diagnostic data collection prevents the use of Windows Update reports for Microsoft Intune from reporting any update information for your managed devices.

      Configure the **Allow Diagnostic data** setting to **Optional** or **Required** using a domain-based group policy or Intune. For more information on how to complete this task, go to:

         - [Use Group Policy to manage diagnostic data collection](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#use-group-policy-to-manage-diagnostic-data-collection)

         - [Use MDM to manage diagnostic data collection](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#use-mdm-to-manage-diagnostic-data-collection)

   6. [Optional] Enable device name collection in diagnostic data. For more information on configuration using a domain-based group policy or Intune, see [Diagnostic data requirements](/windows/deployment/update/wufb-reports-prerequisites#diagnostic-data-requirements).

      > [!NOTE]
      > Using Intune to configure any of the diagnostic data settings mentioned earlier requires that you move the [Device Configuration](../../configmgr/comanage/workloads.md#device-configuration) co-management workload to Intune.

   You can move Feature update management to the cloud in Intune by configuring a [Feature update](feature-updates.md) policy in Intune and setting the **Feature Updates** setting to **Windows Update** using the [Specify source for specific classes of Windows Updates policy](/windows/deployment/update/wufb-wsus) group policy.

   Using Update Ring policies in Intune for Quality or Feature Updates requires you to move the **Windows Update** workload to Intune.

## Is there a way to set a deadline for drivers?

The Quality Update deadline and grace period settings apply to drivers.

Here are some more details on when deadlines are applied to drivers:

- A driver is approved to be made available (manually or automatically) on a date. This is shown as the First Deployment.
- On first or initial scan the approved driver is offered to the device. The date the client's update scan initially discovered the update is also the start date and time for the deadline.
- The deadline calculation for both quality and feature updates is based off the time the client's update scan initially discovered the update. See [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines)

## How do I set deferrals for drivers?

- The deferral period set for Quality Updates within the Update Rings policy does not apply to drivers that are approved using the Driver Update Policy. Instead, use the deferral setting in the Driver policy to set a deferral.  In fact, using multiple driver policies with different deferral settings to create driver deployment rings is highly recommended. Remember to only assign a device to one driver policy.

> [!NOTE]
> The deferral period only applies to automatically approved driver and firmware updates. An admin must specify the date to start offering a driver with any manual approval.

## Are the user experience settings from an Update Ring policy applied for driver updates?

- Yes, user experience settings such as automatic update behavior, active hours, notifications, and so on, are applied for driver updates as well.

## Why does it take up to 24 hours for the driver update inventory to be returned?

- To make driver inventory available, there are several steps that must be completed. The most important is that after the policy is submitted and devices are enrolled for management, Windows Updates must wait for each device to do its daily scan for updates. This process occurs daily, so it can take up to 24 hours for all healthy devices to check in. After this, Intune needs to process the results of the scan to provide the inventory of available driver updates.

## Next steps

- [Create a Windows driver update policy](driver-updates-policy.md)
- [Use Windows driver update reports](driver-updates-reports.md)
