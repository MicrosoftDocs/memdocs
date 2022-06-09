---
# required metadata

title: Update Windows BIOS features using MDM policies in Microsoft Intune
description: Learn more about the Device Firmware Configuration Interface (DFCI) profile to manage UEFI settings in Microsoft Intune. To use DFCI profiles, create Azure AD security groups, the Windows Autopilot deployment profile, and the Enrollment State Page profile.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/21/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---
 
# Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune

When you use Intune to manage Autopilot devices, you can manage UEFI (BIOS) settings after they're enrolled using the Device Firmware Configuration Interface (DFCI). For an overview of benefits, scenarios, and prerequisites, see [Overview of DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/).

DFCI enables Windows to pass management commands from Intune to UEFI (Unified Extensible Firmware Interface).

In Intune, use this feature to control BIOS settings. Typically, firmware is more resilient to malicious attacks. It limits end users control over the BIOS, which is good in a compromised situation.

This feature applies to:

- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and later on supported UEFI

For example, you use Windows client devices in a secure environment, and want to disable the camera. You can disable the camera at the firmware-layer, so it doesn't matter what the end user does. Reinstalling the OS or wiping the computer won't turn the camera back on. In another example, lock down the boot options to prevent users from booting up another OS, or an older version of Windows that doesn't have the same security features.

When you reinstall an older Windows version, install a separate OS, or format the hard drive, you can't override DFCI management. This feature can prevent malware from communicating with OS processes, including elevated OS processes. DFCI's trust chain uses public key cryptography, and doesn't depend on local UEFI (BIOS) password security. This layer of security blocks local users from accessing managed settings from the device's UEFI (BIOS) menus.

## Before you begin

- The device manufacturer must have DFCI added to their UEFI firmware in the manufacturing process, or as a firmware update you install. Work with your device vendors to determine [the manufacturers that support DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/#oems-that-support-dfci), or the firmware version needed to use DFCI.

- The device must be registered for Windows Autopilot by a [Microsoft Cloud Solution Provider (CSP) partner](https://partner.microsoft.com/cloud-solution-provider), or registered directly by the OEM. 

  Devices manually registered for Autopilot, such as [imported from a csv file](../../autopilot/add-devices.md#add-devices), aren't allowed to use DFCI. By design, DFCI management requires external attestation of the device's commercial acquisition through an OEM or a Microsoft CSP partner registration to Windows Autopilot.

  Once your device is registered, its serial number is shown in the list of Windows Autopilot devices.

  For more information on Autopilot, including any requirements, see [Windows Autopilot registration overview](../../autopilot/registration-overview.md).

## Create your Azure AD security groups

Autopilot deployment profiles are assigned to Azure AD security groups. Be sure to create groups that include your DFCI-supported devices. For DFCI devices, most organization may create device groups, instead of user groups. Consider the following scenarios:

- Human Resources (HR) has different Windows devices. For security reasons, you don't want anyone in this group to use the camera on the devices. In this scenario, you can create an HR security users group so the policy applies to users in the HR group, whatever the device type.

- On the manufacturing floor, you have 10 devices. On all devices, you want to prevent booting the devices from a USB device. In this scenario, you can create a security devices group, and add these 10 devices to the group.

For more information on creating groups in Intune, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

## Create the profiles

To use DFCI, create the following profiles, and assign them to your group.

### Create an Autopilot deployment profile

This profile sets up and pre-configures new devices. The following article lists the steps to create the profile:

- [Autopilot deployment profile](../../autopilot/profiles.md)

### Create an Enrollment State Page profile

This profile makes sure that devices are verified and enabled for DFCI during the Windows setup. It's highly recommended to use this profile to block device use until all apps and profiles are installed.

The following article lists the steps to create the profile:

- [Enrollment State Page profile](../enrollment/windows-enrollment-status.md) 

### Create the DFCI profile in Intune

This profile includes the DFCI settings you configure.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

   - **Platform**: Choose **Windows 10 and later**.
   - **Profile**: Select **Templates** > **Device Firmware Configuration Interface**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your policies so you can easily identify them later. For example, a good profile name is **Windows: Configure DFCI settings on Windows devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

   Select **Next**.
6. In **Configuration settings**, configure the settings you want to control in the UEFI firmware layer. For a list of all the settings, and what they do, go to:

    - [Windows DFCI settings](device-firmware-configuration-interface-windows-settings.md)

    Select **Next**.

7. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).
   Select **Next**.
8. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).
   Select **Next**.
9. In **Review + create**, review your settings and select **Create**. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Assign the profiles, and reboot

Be sure to [assign](../configuration/device-profile-assign.md) the profiles to your Azure AD security groups that include your DFCI devices. The profile can be assigned when it's created, or after.

When the device runs the Windows Autopilot, during the Enrollment Status page, DFCI may force a reboot. This first reboot enrolls UEFI to Intune. 

If you want to confirm the device is enrolled, you can reboot the device again, but it's not required. Use the device manufacturer's instructions to open the UEFI menu, and confirm UEFI is now managed.

The next time the device syncs with Intune, Windows receives the DFCI settings. Reboot the device. This third reboot is required for UEFI to receive the DFCI settings from Windows.

## Update existing DFCI settings

If you want to change existing DFCI settings on devices that are in use, you can. In your existing DFCI profile, change the settings, and save your changes. Since the profile is already assigned, the new DFCI settings take effect when:

1. The device checks in with the Intune service to review profile updates. Check-ins happen at various times. For more information, see [when devices get a policy, profile, or app updates](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).
2. To enforce the new settings, reboot the device [remotely](../remote-actions/device-restart.md) or locally.

You can also [signal devices to check in](../remote-actions/device-sync.md). After a successful sync, [signal to reboot](../remote-actions/device-restart.md).

>[!NOTE]
> Deleting the DFCI profile, or removing a device from the group assigned to the profile doesn't remove DFCI settings or re-enable the UEFI (BIOS) menus. If you want to stop using DFCI, then update your existing DFCI profile. For more information on the steps, see [retire the device](#retire) in this article.

## Reuse, retire, or recover the device

### Reuse

If you plan to reset Windows to repurpose the device, then [wipe the device](../remote-actions/devices-wipe.md). Do **not** remove the Autopilot device record.

After wiping the device, move the device to the group assigned the new DFCI and Autopilot profiles. Be sure to reboot the device to rerun Windows setup.

### Retire

When you're ready to retire the device and release it from management, update the DFCI profile to the UEFI (BIOS) settings you want at the exit state. Typically, you want all settings enabled. For example:

1. Open your DFCI profile (**Devices** > **Configuration profiles**).
2. Change the **Allow local user to change UEFI (BIOS) settings** to **Only not configured settings**.
3. Set all other settings to **Not configured**.
4. Save your settings.

These steps unlock the device's UEFI (BIOS) menus. The values remain the same as the profile (**Enabled** or **Disabled**), and aren't set back to any default OS values.

You're now ready to wipe the device. Once the device is wiped, delete the Autopilot record. Deleting the record prevents the device from automatically re-enrolling when it reboots.

> [!TIP]
> To remove Surface devices from DFCI enrollment, see [removing DFCI management](/surface/surface-manage-dfci-guide#removing-dfci-management).

### Recover

If you wipe a device, and delete the Autopilot record before unlocking the UEFI (BIOS) menus, then the menus remain locked. Intune can't send profile updates to unlock it.

To unlock the device, open the UEFI (BIOS) menu, and refresh management from network. Recovery unlocks the menus, but leaves all UEFI (BIOS) settings set to the values in the previous Intune DFCI profile.

## End user impact

When the DFCI policy is applied, local users can't change settings configured by DFCI, even if the UEFI (BIOS) menu is password protected. Depending on the settings you configure, end users may receive errors that hardware components aren't found, or can't be diagnosed. Be sure to provide documentation to end users explaining the options you've disabled.  

## Next steps

After the [profile is assigned](device-profile-assign.md), [monitor its status](device-profile-monitor.md).
