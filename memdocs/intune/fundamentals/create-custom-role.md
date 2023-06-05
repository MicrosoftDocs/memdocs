---
# required metadata

title: Create a custom role in Intune
description: Learn how to create a custom role in Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 06/20/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Create a custom role in Intune

You can create a custom Intune role that includes any permissions required for a specific job function. For example, if an IT department group manages applications, policies, and configuration profiles, you can add all those permissions together in one custom role. After creating a custom role, you can [assign](assign-role.md)
 it to any users that need those permissions.

To create, edit, or assign roles, your account must have one of the following permissions in Azure AD:
- **Global Administrator**
- **Intune Service Administrator**

## To create a custom role

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > **Create**.

2. On the **Basics** page, enter a name and description for the new role, then choose **Next**.

3. On the **Permissions** page, choose the permissions you want to use with this role.

4. On the **Scope (Tags)** page, choose the tags for this role. When this role is assigned to a user, that user can access resources that also have these tags. Choose **Next**.

5. On the **Review + create** page, when you're done, choose **Create**. The new role is displayed in the list on the **Intune roles - All roles** blade.

## Copy a role

You can also copy an existing role.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > select the checkbox for a role in the list > **Duplicate**.

2. On the **Basics** page, enter a name. Make sure to use a unique name.

3. All the permissions and scope tags from the original role will already be selected. You can subsequently change the duplicate role's **Name**, **Description**, **Permissions**, and **Scope (Tags)**.

4. After you've made all the changes that you want, choose **Next** to get to the **Review + create** page. Select **Create**. 

## Custom role permissions

> [!NOTE]
> You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change does not apply to Intune for Education tenants who still need to assign the **Managed apps** permission.

The following permissions are available when creating custom roles.

| Permission | Description |
| --- | --- |
| Android FOTA/Assign | Assign Android firmware over-the-air (FOTA) deployments to Azure AD security groups. |
| Android FOTA/Delete | Delete and cancel pending Android firmware over-the-air (FOTA) deployments and delete deployment history. |
| Android FOTA/Create | Create and manage all aspects of Android firmware over-the-air (FOTA) deployments. |
| Android FOTA/Read | View Android firmware over-the-air (FOTA) deployments, including history and reporting. |
| Android FOTA/Update | Change existing Android firmware over-the-air (FOTA) deployments and cancel firmware deployments. |
| Android for work/Read | View the Android for Work configuration used to sync applications with the Play for Work store or view the Android for Work enrollment prerequisites and enrollment profiles. | 
| Android for work/Update app sync | Manage or change the Android for Work configuration used to sync applications with the Play for Work store, or sync the apps you've approved from the store with Intune. | 
| Android for work/Update onboarding | Manage or change the Android for work configuration used to enroll Android for Work devices or manage the Android for Work enrollment profiles. | 
| Audit data/Read | View all Intune audit data for this tenant. | 
| Certificate Connector/Modify | Add, remove, or modify certificate connectors required to support certificate issuance. | 
| Certificate Connector/Read | View certificate connectors required to support certificate issuance. | 
| Cloud attached devices\View collections | Displays the *Collections* page for Configuration Manager cloud attached devices |
| Cloud attached devices\View resource explorer | Displays the *Resource explorer* page for Configuration Manager cloud attached devices |
| Cloud attached devices\View timeline | Displays the *Timeline* page for Configuration Manager cloud attached devices |
| Cloud attached devices\View software updates | Displays the *Software updates* page for Configuration Manager cloud attached devices |
| Cloud attached devices\View scripts | Displays the *Scripts* page for Configuration Manager cloud attached devices |
| Cloud attached devices\Run script | Displays the *Run script* action and allows the user to run scripts on Configuration Manager cloud attached devices |
| Cloud attached devices\Run CMPivot query | Displays the *CMPivot* page for Configuration Manager cloud attached devices |
| Cloud attached devices\View client details | Displays the *Client details* page for Configuration Manager cloud attached devices |
| Cloud attached devices\View applications | Displays the *Applications* page for Configuration Manager cloud attached devices |
| Cloud attached devices\Take application actions | Displays application actions in the *Applications* page and allows the user to take application actions on Configuration Manager cloud attached devices |
| Corporate device identifiers/Create | Create new corporate device identifiers or import a CSV file containing a list of corporate device identifiers. | 
| Corporate device identifiers/Delete | Delete IMEI or serial numbers used as corporate device identifiers. | 
| Corporate device identifiers/Read | View the IMEI or serial numbers used as corporate device identifiers. | 
| Corporate device identifiers/Update | Change IMEI or serial numbers used as corporate device identifiers. | 
| Customization/Assign | Assign customization options for the Company Portal. | 
| Customization/Create | Create customization options for the Company Portal. | 
| Customization/Delete | Delete customization options for the Company Portal. | 
| Customization/Read | Read customization options for the Company Portal. | 
| Customization/Update | Update customization options for the Company Portal. | 
| Derived Credentials/Modify | Configure the Derived Credentials for your Microsoft Intune tenant. | 
| Derived Credentials/Read | View the Derived Credentials for your Microsoft Intune tenant. | 
| Device compliance policies/Assign | Assign device compliance policies to Azure AD security groups, and assign Exchange on-premises access to Azure AD security groups. | 
| Device compliance policies/Create | Create new device compliance policies. | 
| Device compliance policies/Delete | Delete device compliance policies or delete Exchange ActiveSync connectors. | 
| Device compliance policies/Read | View device compliance policies and the list of Exchange Active Sync Connectors, or view the settings for Exchange on-premises access. | 
| Device compliance policies/Update | Change device compliance policies, Exchange ActiveSync connectors and Exchange on-premises access settings. | 
| Device compliance policies/View reports | View, generate, and export device compliance reports. | 
| Device configurations/Assign | Assign device configuration profiles or assign device enrollment restrictions to Azure AD security groups. | 
| Device configurations/Create | Create new device configuration profiles, or create new device enrollment restrictions. | 
| Device configurations/Delete | Delete device configuration profiles, or delete device enrollment restrictions. | 
| Device configurations/Read | View device configuration profiles, or view device enrollment restrictions. | 
| Device configurations/Update | Change device configuration profiles, or change device enrollment restrictions. | 
| Device configurations/View Reports | View, generate, and export device configuration reports. | 
| Device enrollment managers/Read | View the list of device enrollment manager accounts. | 
| Device enrollment managers/Update | Create new device enrollment manager accounts, or delete device enrollment manager accounts. | 
| Endpoint Analytics/Create | Create new baselines and edit endpoint analytics settings. | 
| Endpoint Analytics/Delete | Edit endpoint analytics settings and delete baselines. | 
| Endpoint Analytics/Read | View endpoint analytics scores and performance reports. | 
| Endpoint Analytics/Update | Edit endpoint analytics settings and baselines. | 
| Endpoint protection reports/Read | View endpoint protection reports. | 
| Enrollment programs/Assign profile | Manage Windows Autopilot deployment profile assignment settings. | 
| Enrollment programs/Create device | Import Apple devices for the Device Enrollment Program, Apple School or Business Manager, Apple Configurator or Windows Autopilot devices. | 
| Enrollment programs/Create profile | Create new profiles for the Device Enrollment Program, Apple School Manager, Apple Configurator, or Windows Autopilot. | 
| Enrollment programs/Create token | Download the Apple Device Enrollment Program or Apple School Manager token .pem file. | 
| Enrollment programs/Delete device | Delete Apple devices for the Device Enrollment Program, Apple School or Business Manager, Apple Configurator or Windows Autopilot devices. | 
| Enrollment programs/Delete profile | Delete profiles for the Device Enrollment Program, Apple School Manager, Apple Configurator, or Windows Autopilot. | 
| Enrollment programs/Delete token | Delete Apple Device Enrollment Program or Apple School Manager token .pem file(s). | 
| Enrollment programs/Read device | View Apple devices for the Device Enrollment Program, Apple School Manager, Apple Configurator, or Windows Autopilot devices. | 
| Enrollment programs/Read profile | View profiles for the Device Enrollment Program, Apple School Manager, Apple Configurator, or Windows Autopilot. | 
| Enrollment programs/Read token | View the Apple Device Enrollment Program or Apple School Manager token status. | 
| Enrollment programs/Sync device | Initiate the Sync command for Windows Autopilot devices. | 
| Enrollment programs/Update profile | Manage profiles for the Device Enrollment Program, Apple School Manager, Apple Configurator, or Windows Autopilot. | 
| Enrollment programs/Update token | Upload the Apple Device Enrollment or Apple School Manager token and sync Apple Device Enrollment Program or Apple School Manager devices. | 
| [Filters/Create](/mem/intune/fundamentals/filters#create-a-filter) | Create new filter. | 
| [Filters/Delete](/mem/intune/fundamentals/filters#delete-a-filter)| Delete filters. | 
| Filters/Read | View filters.  | 
| [Filters/Update](/mem/intune/fundamentals/filters#change-an-existing-filter) | Edit filters. | 
| Intune data warehouse/Read | View all data and reports from the data warehouse. Data can be used by Power BI or other reporting services. | 
| Managed apps/Assign | Assign application protection policies to Azure AD security groups. | 
| Managed apps/Create | Create new application protection policies. | 
| Managed apps/Delete | Delete application protection policies. | 
| Managed apps/Read | View application protection policies and status. | 
| Managed apps/Update | Change application protection policies, or delete pending wipe requests for protected apps. | 
| Managed apps/Wipe | Create a wipe request to selectively remove company data from a protected app.  | 
| Managed devices/Delete | Delete Intune managed devices. Deleted devices can no longer be managed by Intune, and the device can no longer access company resources. Company data may be wiped from the device if a user tries to check-in after it is deleted. | 
| Managed devices/Read | View Intune managed devices.  | 
| Managed devices/Set primary user | Choose, change, or remove the primary user of a managed device. This permission must be used in combination with the managed devices read and update permissions. | 
| Managed devices/Update | Change settings or ownership properties of a managed device. This permission does not enable remote actions for devices. To perform remote actions on the device, grant one or more of the Remote Task permissions. | 
| Managed devices/View reports | Generate, view, or export reports for managed devices. | 
| Managed Google Play/Modify | Modify the settings for synchronizing Managed Google Play apps with Microsoft Intune. | 
| Managed Google Play/Read | Display the settings for synchronizing Managed Google Play apps with Microsoft Intune. | 
| Microsoft Defender ATP/Read | View the connection between Microsoft Intune and Microsoft Defender ATP. | 
| Microsoft Store For Business/Modify | Modify the settings for synchronizing Microsoft Store for Business apps with Microsoft Intune. | 
| Microsoft Store For Business/Read | View the settings for synchronizing Microsoft Store for Business apps with Microsoft Intune. | 
| Microsoft Tunnel Gateway/Create | Create Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. | 
| Microsoft Tunnel Gateway/Delete | Delete Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. | 
| Microsoft Tunnel Gateway/Read | View Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. | 
| Microsoft Tunnel Gateway/Update | Update Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. | 
| Mobile apps/Assign | Assign mobile applications or eBooks to Azure AD security groups. | 
| Mobile apps/Create | Add new mobile applications to Intune such as store apps, line-of-business apps, web-links or built-in apps. You can also add books purchased through the Apple Volume Purchase Program or add eBook categories. You can setup iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. | 
| Mobile apps/Delete | Delete mobile applications such as store apps, line-of-business apps, web-links or built-in apps. You can also delete books purchased through the Apple Volume Purchase Program or delete eBook categories. You can delete iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. | 
| Mobile apps/Read | View mobile applications such as store apps, line-of-business apps, web-links or built-in apps. You can also view books purchased through the Apple Volume Purchase Program or add eBook categories. You can view iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. | 
| Mobile apps/Relate | Create relationships with other managed apps using Dependencies and Supersedence features. Without this permission, IT admins are not able to add App dependency or supersedence relationships when creating or editing Win32 apps. |
| Mobile apps/Update | Manage mobile applications such as store apps, line-of-business apps, web-links or built-in apps. You can also manage books purchased through the Apple Volume Purchase Program or add eBook categories. You can manage iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. | 
|Mobile apps/View reports| View reports on mobile applications such as store apps, line-of-business apps, web links, and built-in apps. |
| Mobile Threat Defense/Modify | Add, remove, or modify the Mobile Threat Defense connectors between Intune and your chosen MTD vendors | 
| Mobile Threat Defense/Read | View the Mobile Threat Defense connectors between Intune and your chosen MTD vendors | 
| Organization/Create | Create tenant settings such as device categories and Exchange connectors. | 
| Organization/Delete | Delete tenant settings such as device categories and Exchange Connectors. | 
| Organization/Read | View tenant settings such as device categories and Exchange Connectors. This permission is required to activate all enrollment workflows. | 
| Organization/Update | Manage tenant settings, device categories and Exchange Connectors. |
| Organizational messages/Create | Create organizational messages. |
| Organizational messages/Read | Read organizational messages. |
| Organizational messages/Update | Cancel organizational messages. |
| Organizational messages/Delete | Delete organizational messages. |
| Organization messages/Assign | Assign organizational messages. |
| Organizational messages/Update organizational message control | Enable or block organizational messages directly from Microsoft, while allowing admin messages to display. | 
| Partner Device Management/Modify | Configure the Compliance Connector for Jamf. | 
| Partner Device Management/Read | View the Compliance Connector for Jamf. | 
| Policy Sets/Assign | Assign Policy Sets to Azure AD security groups. | 
| Policy Sets/Create | Create a new Policy Set. | 
| Policy Sets/Delete | Delete Policy Sets. | 
| Policy Sets/Read | View Policy Sets. | 
| Policy Sets/Update | Change a Policy Set, or add items to a Policy Set. | 
| Remote assistance connectors/Read | View the status of the TeamViewer connector and Remote Help. This permission is not required to initiate remote assistance requests for devices. | 
| Remote assistance connectors/Update | Manage the state of the TeamViewer connector and Remote Help. This permission also requires the Remote assistance connectors Read permission to view the status of the TeamViewer connector and Remote Help. | 
| Remote assistance connectors/View reports | View, generate and export Remote Help sessions and monitor reports. | 
| Remote Help app/Elevation | Elevation allows the helper to enter UAC credentials when prompted on the sharer's device when Remote Help is enabled. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access. | 
| Remote Help app/Take full control | Take full control allows the helper to view and control the sharer's device when Remote Help is enabled. | 
| Remote Help app/View screen | View screen allows the helper to view the sharer's device when Remote Help is enabled. | 
| Remote tasks/Bypass activation lock | Remove the Activation Lock from supervised devices without requiring the user's Apple ID and password. This may be required if a user leaves the company and returns the device; without the user's Apple ID and password, there is no way to reactivate the device. Or, you need to reassign some devices to a different department during a device refresh in your organization. You can only reassign devices that do not have Activation Lock enabled. You must also have the Managed Device Read permission to view devices in the Azure portal before initiating this remote task. | 
| Remote tasks/Clean PC | Initiate a Fresh start device action. This action removes any apps that are installed on a Windows 10 PC that is running the Creators Update. Then, it automatically updates the PC to the latest version of Windows. | 
| Remote tasks/Collect diagnostics | Collect device diagnostics | 
| Remote tasks/Disable lost mode | Turn off the lost mode for an iOS device. | 
| Remote tasks/Enable lost mode | Initiate lost mode on lost or stolen iOS devices. This mode lets you enter a message and a phone number that appears on the lock screen of the device. To use lost mode, the device must be a corporate-owned iOS device that is in supervised mode. | 
| Remote tasks/Enable Windows IntuneAgent | Enable Windows Intune agent. | 
| Remote tasks/Get filevault key. | Get Mac FileVault key. | 
| Remote tasks/Initiate Configuration Manager action | Initiate a remote action on a device managed by Configuration Manager. | 
| Remote tasks/Locate device | View the location of a lost or stolen corporate-owned device on a map. Can locate supervised iOS/iPadOS devices, Android dedicated devices (COSU), and Windows devices. |  
| Remote tasks/Manage shared device users | Log out the user with the current session on a shared device.  This action does not delete users from a shared device, it will only force the user with a current session to be logged out. | 
| Remote tasks/Offer remote assistance | Initiate a remote assistance session with a user's device by using a remote assistance provider. The remote assistance option for your provider must be enabled for your tenant. | 
| Remote tasks/Play lost mode sound | Initiate the lost mode ring sound on a device that has been placed in MDM Lost mode. | 
| Remote tasks/Reboot now | Initiates a device restart. This causes the device you choose to be restarted. The device owner isn't automatically notified of the restart, and they might lose work. | 
| Remote tasks/Remote lock | The Remote lock device action locks the device. To unlock the device, the device owner enters their passcode. You can remotely lock devices that have a PIN or password set. Devices that don't have a PIN or password can't be remotely locked. | 
| Remote tasks/Reset passcode | Initiates a forced removal of the passcode, and requires the device user to set a new passcode. Supported on iOS devices, and certain later versions of Android and Android for work. Not supported on older Android versions, macOS, or Windows. | 
| Remote tasks/Retire | Initiates a retire action for a device. Also called remove company data. The Remove company data action removes managed app data (where applicable), settings, and email profiles that were assigned by using Intune. The device is removed from Intune management. This happens the next time the device checks in and receives the remote Remove company data action. Remove company data leaves the user's personal data on the device. | 
| Remote tasks/Revoke App Licenses | Revokes any iOS VPP application licenses that have been associated with the device. | 
| Remote tasks/Rotate BitLockerKeys (preview) | Initiates a key rotation for BitLocker Recovery Passwords on the device. | 
| Remote tasks/Rotate filevault key. | Rotate Mac FileVault key. | 
| Remote tasks/Send custom notifications | Allows admin to send customized notifications to devices. Devices receive notifications in Company Portal. | 
| Remote tasks/Set device name | Set or change the name of a device.  | 
| Remote tasks/Shut down | Initiates a shutdown of the device, and will automatically close all applications and running services and leave the device in a powered-off state. | 
| Remote tasks/Sync devices. | Initiates a sync operation on the device and forces the selected device to immediately check in with Intune. When a device checks in, it immediately receives any pending actions or policies that have been assigned to it. | 
| Remote tasks/Update cellular data plan | Activate the data plan for cellular iOS/iPadOS devices that support eSIM.  | 
| Remote tasks/Update device account | Allows changing the device account associated with Surface Hub devices, and set authentication options such as password rotation. | 
| Remote tasks/Windows defender | Initiates a Windows Defender signature update. | 
| Remote tasks/Wipe | Initiates a wipe of the device. Also called a factory reset. The Factory reset action restores a device to its factory default settings. The user data is kept or wiped depending on whether or not you choose the Retain enrollment state and user account checkbox. | 
| Roles/Assign | Assign Intune built-in or custom roles to Azure AD security groups | 
| Roles/Create | Create new Intune custom roles. Built-in roles are created by Intune automatically. | 
| Roles/Delete | Delete a custom Intune role. You cannot delete built-in roles. | 
| Roles/Read | View permissions, role assignments, member groups and scope groups for any built-in or custom Intune role. | 
| Roles/Update | Update custom role permissions and role assignments for built-in or custom roles. Role assignments define the administrators and end user scope for the role.  | 
| Security baselines/Assign | Assign Security Baseline profiles to Azure AD security groups. | 
| Security baselines/Create | Create new Security Baseline profiles. | 
| Security baselines/Delete | Delete Security Baseline profiles. | 
| Security baselines/Read | View Security Baseline profiles or profiles reporting or Template reporting for all Security Baseline workspace. | 
| Security baselines/Update | Update Security Baseline profiles. | 
| Security tasks/Read | View security tasks. | 
| Security tasks/Update | Update security tasks. | 
| Terms and conditions/Assign | Assign terms and conditions to Azure AD security groups. | 
| Terms and conditions/Create | Create new terms and conditions. | 
| Terms and conditions/Delete | Delete an existing terms and conditions. | 
| Terms and conditions/Read | View terms and conditions. | 
| Terms and conditions/Update | Manage existing terms and conditions but not assignments. | 
| Windows Enterprise Certificate/Modify | Add, remove, or modify the code-signing certificate used to distribute line-of-business apps to your managed Windows devices. | 
| Windows Enterprise Certificate/Read | View the code-signing certificate used to distribute line-of-business apps to your managed Windows devices. | 

## Next steps
- [Assign a role to a user](assign-role.md)
- [Learn more about role-based access control in Intune](role-based-access-control.md)


