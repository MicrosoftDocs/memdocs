---
# required metadata

title: Use custom compliance settings for Linux and Windows devices in Microsoft Intune
description: Manage custom compliance settings for Linux and Windows devices by using JSON files and discovery scripts in Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/19/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use custom compliance policies and settings for Linux and Windows devices with Microsoft Intune

Expanding on Intune’s built-in device compliance options, use policies for custom compliance settings for managed Linux and Windows devices. Custom settings provide flexibility to base compliance on the settings that are available on a device without having to wait for Intune to add these settings.

This feature applies to:

- Linux – Ubuntu Desktop, version 20.04 LTS and 22.04 LTS
- Windows 10/11

Before you can add custom settings to a policy, you’ll need to prepare a JSON file, and a detection script for use with each supported platform. Both the script and JSON become part of the compliance policy. Each compliance policy supports a single script, and each script can detect multiple settings:

- The JSON file defines the custom settings and the values that are considered as compliant. You can also configure messages for users to tell them how to restore compliance for each setting. You add your JSON file while creating a compliance policy, just after you select a discovery script for that policy.

- Scripts are specific to different platforms and delivered to devices through the compliance policy. When policy is evaluated, the script detects the settings from the JSON file, and then reports the results to Intune. Windows uses a PowerShell script and Linux uses a POSIX-compliant shell script.

  The scripts must be uploaded to the Microsoft Endpoint Manager admin center before you create a compliance policy. You select the script when you’re configuring a policy to support custom settings.

After you’ve deployed custom compliance settings and devices have reported back, you'll be able to view the results alongside the built-in compliance setting details in the Microsoft Endpoint Manager admin center.  Custom compliance settings can be used for conditional access decisions, the same way built-in compliance settings are.  Together they form a compound rule set, equally affecting the device compliance state.

## Prerequisites

- **Azure Active Directory (Azure AD) joined** devices, *including* hybrid Azure AD-joined devices. 

  Hybrid Azure AD-joined devices are devices that are joined to Azure AD and also joined to on-premises Active Directory. For more information, see [Plan your hybrid Azure AD join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan).

- **Azure AD registered/Workplace joined (WPJ)**

  Devices [registered](/azure/active-directory/user-help/user-help-register-device-on-network) in Azure Active Directory (AAD), see [Workplace Join as a seamless second factor authentication](/windows-server/identity/ad-fs/operations/join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications#BKMK_DRS) for more information. Typically these are Bring Your Own Device (BYOD) devices which have had a work or school account added via Settings>Accounts>Access work or school. 

  On WPJ devices, device context PowerShell scripts work, but user context PowerShell scripts are ignored. 

- **Discovery script** - A PowerShell for Windows or a POSIX-compliant shell script for Linux that you create. The script runs on a device to discover the custom settings defined in your JSON file. The script returns the configuration value of those settings to Intune. You need to upload your script to the Microsoft Endpoint Manager admin center before you create a compliance policy and then select the script you want to use when creating a policy.

  To create a custom compliance script, see [Custom compliance discovery scripts for Microsoft Intune](../protect/compliance-custom-script.md).

- **JSON file** - The  JSON file defines the custom settings and the value that is to be considered as compliant and can contain messages for users on how to restore the device to compliance for the setting. For guidance on creating a JSON for custom compliance, see [Custom compliance JSON files](compliance-custom-json.md).

## Create a policy with custom compliance settings

Before you begin to create a policy that will include custom settings, review the [prerequisites](#prerequisites).

You must first upload an applicable discovery script to Intune, and have a ready JSON to add while creating the policy.

When ready, use the normal procedure to [create a compliance policy](create-compliance-policy.md), which includes platform specific instructions for adding custom settings to the policy. Custom settings are added while on the Configuration settings page by configuring the option for *Custom Compliance*.

> [!NOTE]  
> When a Windows device receives a compliance policy with custom settings, it checks for the presence of [Intune Management Extensions](../apps/intune-management-extension.md). If not found, the device runs an MSI that installs the extensions, enabling the client to download and run PowerShell scripts that are part of a compliance policy, and to upload compliance results. Actions managed by the services include:
>
> - Checking for new or updated PowerShell scripts every eight hours.
> - Running the discovery scripts every eight hours.
> - Running scripts that download when a user selects Check Compliance on the device. However, there is no check for new or updated scripts when Check Compliance is run.
>
> It is not possible to push notifications to a device to enable custom compliance to run on demand.

## Monitor custom compliance policy

Use the following methods to view details about a device’s compliance status.

- For both Linux and Windows devices, you can view per-setting device compliance details for custom compliance settings in the Microsoft Endpoint Manager admin center.

  In the admin center go to **Reports** > **Device compliance**, and then select the **Reports** tab. Select the tile for **Noncompliant devices and settings**, and then use the drop-down menus to configure the report. Be sure to select a platform for the OS, and then select **Generate** report.

  For more information, see [Monitor Intune Device compliance policies](../protect/compliance-policy-monitor.md).

- On a Linux device, you can open the Intune app to view the device’s status:

  - **Compliant** – Your device is compliant with your organization’s policies and should be able to access organizational resources.
  - **Checking status** – Intune is currently evaluating the devices compliance to your organization’s policies.
  - **Not compliant** – The device doesn’t meet your organization’s device and security requirements and might not have access to your organization’s resources.

  When the device status is *Not compliant*, select **View issues** to see details about issues that must be addressed to bring that device into compliance. For information on resolving common issues, see [Additional troubleshooting for Linux devices](#additional-troubleshooting-for-linux-devices).

## Troubleshoot custom compliance for devices

### Custom settings aren’t evaluated

Check the device compliance reports for the following error codes and insight into the problem:

- 65007: Script returned failure  
- 65008: Setting missing in the script result
- 65009: Invalid json for the discovered setting
- 65010: Invalid datatype for the discovered setting

On Windows you can add the following line at the end of the PowerShell script to return errors related to the PowerShell script, ensure the following line is at the end of the PowerShell script file: `return $hash | ConvertTo-Json -Compress`

### PowerShell or POSIX-compliant shell scripts aren’t visible to select, or remain visible after being deleted

Refresh the current view. If the issue persists, cancel the policy creation flow, and start again.

### After an issue on a device is fixed, subsequent syncs don’t identify the issue as resolved and compliant

It can take up to eight hours before a noncompliant status shows as compliant after a change to the device.

### Can a user manually check for compliance after fixing an issue on a device in order to identify if the issue is resolved and compliant? 

- On Windows, a user can go to the [Company Portal website](https://portal.manage.microsoft.com) and trigger a sync to update the device status after fixing a non-compliant custom compliance setting.

- On Linux, a user can open the *Microsoft Intune app* and select **Refresh** on either the device details page or the compliance issues page to start a new check-in with Intune.

### Why aren’t more operators and operands supported?

Contact your account manager to request the addition of specific operators and operands. They can then be considered for a future update.

### Why can’t I apply multiple discovery scripts to one custom compliance policy?

Policies support the use of a single script. However, each script supports checking for multiple compliance values.

## Additional troubleshooting for Linux devices

To identify settings that aren't compliant for a device:

- [In the Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can identify devices that aren't compliant with policy. **Navigate** to **Reports** > **Device compliance**, select the *Reports* tab, and then select the tile for **Noncompliant devices and settings**. Use the drop-downs to configure the report you want, and then select **Generate** report.

The admin center displays a separate line for each setting that isn’t compliant on a device.  

- **On the Linux device**, open the Microsoft Intune app and view the *Update device settings* page.

The following sections discuss common issues and resolutions for issues that users of Linux devices might encounter.

#### Operating system distro and version

Users of devices that don’t meet the device compliance configuration for Linux distribution or operating system versions, might receive a message that indicates the need to upgrade or downgrade the device operating system.  

To be compliant with the *Allowed Distros* setting, devices Linux distribution and version must meet minimum, maximum, and type requirements. If necessary, install a different version or distribution of Linux to bring the device into compliance.

#### Password complexity

Users of devices that don’t meet the device compliance configuration for password complexity requirements might receive a message that indicates they must use a strong password.

To be compliant with *Password Policy* settings, configure the Linux system to use passwords that meet those requirements. Common organization requirements include:

- Passwords that include a minimum number of letters, digits, or special characters
- Passwords of a minimum length

#### Device encryption

Users of devices that don’t meet compliance settings for disk and partition encryption might receive a message that they must encrypt the device drives.

To be compliant with the *Require Device Encryption* setting, device-level encryption is required for writable fixed disks on the Linux device.

There are several options for disk and partition encryption on Linux operating systems. Intune recognizes any encryption system that uses the underlying dm-crypt subsystem. This subsystem has been standard on Linux systems for some time. The preferred method of setting up dm-crypt is to use the LUKS format with the cryptsetup tool.

The following is general guidance when encrypting disk and partitions:

- Encrypting Linux system volumes after installation is possible, but potentially time consuming. We recommend setting up disk encryption while installing the operating system.
- Not all filesystem partitions need to be encrypted for a device to meet organizational standards. The following aren't evaluated by the built-in device encryption settings:
  - Read-only partitions
  - Pseudo-filesystems, like `/proc` or `tmpfs`
  - The `/boot` or `/boot/efi` partitions

#### Refresh your compliance status on Linux devices

After making changes to a device to bring it into compliance, refresh the device status with Intune:  

- If the Microsoft Intune app is still running, select **Refresh** on the device details page, or on the compliance issues page to start a new check-in with Intune.
- If the Microsoft Intune app isn't running, sign into the app, which will start a new check-in.
- After installation, the Microsoft Intune app periodically checks-in with Intune on its own, so long as the device is on, and a user is signed in to it.

## Next steps

- [Create a compliance policy](../protect/create-compliance-policy.md)
