---
title: Create a custom role in Intune
description: Learn how to create a custom role in Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 02/04/2026
ms.topic: article
ms.collection:
  - M365-identity-device-management
---

# Create a custom role in Intune

You can create a custom Intune role that includes any permissions required for a specific job function. For example, if an IT department group manages applications, policies, and configuration profiles, you can add all those permissions together in one custom role. After creating a custom role, you can [assign](assign-role.md) it to any users that need those permissions.

> [!NOTE]
> **Enhanced Security**: [!INCLUDE [multi-admin-approval-rbac](../includes/multi-admin-approval-rbac.md)]

To create, edit, or assign roles, your account must have the following role in Microsoft Entra ID:

- Intune Service Administrator

## To create a custom role

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > **Create**.

2. On the **Basics** page, enter a name and description for the new role, then choose **Next**.

3. On the **Permissions** page, choose the permissions you want to use with this role.

4. On the **Scope (Tags)** page, choose the tags for this role. When this role is assigned to a user, that user can access resources that also have these tags. Choose **Next**.

5. On the **Review + create** page, when you're done, choose **Create**. The new role is displayed in the list on the **Intune roles - All roles** page.

## Copy a role

You can also copy an existing role.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > select the checkbox for a role in the list > **Duplicate**.

2. On the **Basics** page, enter a name. Make sure to use a unique name.

3. All the permissions and scope tags from the original role are already selected. You can later change the duplicate role's **Name**, **Description**, **Permissions**, and **Scope (Tags)**.

4. After you make all the changes that you want, choose **Next** to get to the **Review + create** page. Select **Create**.

## Custom role permissions

The following permissions are available when creating custom roles.

> [!TIP]
> For a list of permissions for each Intune built-in role, see [Intune built-in roles and their permissions](../fundamentals/role-based-access-control-reference.md).

### Admin tasks

| Permission | Action | Description |
| --- | --- | --- |
| Admin tasks | Create | Allows creation of new device management administrative tasks |
| Admin tasks | Delete | Allows deletion of device management administrative tasks |
| Admin tasks | Read | Allows read access to device management administrative tasks |
| Admin tasks | Update | Allows updating of device management administrative task properties and status |

### Android Enterprise

| Permission | Action | Description |
| --- | --- | --- |
| Android Enterprise | Enrollment time device membership assignment for Android Enterprise | Allows Intune to assign devices to Microsoft Entra ID groups during enrollment. |
| Android Enterprise | Read | View the Android Enterprise configuration used to sync applications with the Managed Google Play store or view the Android Enterprise enrollment prerequisites and enrollment profiles. |
| Android Enterprise | Update app sync | Manage or change the Managed Google Play configuration used to sync applications with the Managed Google Play store, or sync the apps you approved from the store with Intune. |
| Android Enterprise | Update enrollment profiles | Manage or change Android Enterprise Device Owner enrollment profiles used to enroll devices. |
| Android Enterprise | Update onboarding | Manage or change the Android Enterprise binding to Managed Google Play and other account-wide configurations. |

### Android FOTA

| Permission | Action | Description |
| --- | --- | --- |
| Android FOTA | Assign | Assign Android firmware over-the-air (FOTA) deployments to Microsoft Entra security groups. |
| Android FOTA | Create | Create and manage all aspects of Android firmware over-the-air (FOTA) deployments. |
| Android FOTA | Delete | Delete and cancel pending Android firmware over-the-air (FOTA) deployments and delete deployment history. |
| Android FOTA | Read | View Android firmware over-the-air (FOTA) deployments, including history and reporting. |
| Android FOTA | Update | Change existing Android firmware over-the-air (FOTA) deployments and cancel firmware deployments. |

### App Control for Business

| Permission | Action | Description |
| --- | --- | --- |
| App Control for Business | Assign | Assign App Control for Business profiles to Microsoft Entra security groups. |
| App Control for Business | Create | Create new App Control for Business profiles. |
| App Control for Business | Delete | Delete App Control for Business profiles. |
| App Control for Business | Read | Read App Control for Business profiles. |
| App Control for Business | Update | Update App Control for Business profiles. |
| App Control for Business | View Reports | Generate, view, or export reports for App Control for Business profiles. |

### Attack Surface Reduction

| Permission | Action | Description |
| --- | --- | --- |
| Attack Surface Reduction | Assign | Assign Attack Surface Reduction (ASR) profiles to Microsoft Entra security groups. |
| Attack Surface Reduction | Create | Create new Attack Surface Reduction (ASR) profiles. |
| Attack Surface Reduction | Delete | Delete Attack Surface Reduction (ASR) profiles. |
| Attack Surface Reduction | Read | Read Attack Surface Reduction (ASR) profiles. |
| Attack Surface Reduction | Update | Update Attack Surface Reduction (ASR) profiles. |
| Attack Surface Reduction | View Reports | Generate, view, or export reports for Attack Surface Reduction (ASR) profiles. |

### Audit data

| Permission | Action | Description |
| --- | --- | --- |
| Audit data | Read | View all Intune audit data for this tenant. |

### Certificate Connector

| Permission | Action | Description |
| --- | --- | --- |
| Certificate Connector | Modify | Add, remove, or modify certificate connectors required to support certificate issuance. |
| Certificate Connector | Read | View certificate connectors required to support certificate issuance. |

### Chrome Enterprise

| Permission | Action | Description |
| --- | --- | --- |
| Chrome Enterprise | Delete connection settings | Delete the organization's Chrome Enterprise connection settings. |
| Chrome Enterprise | Read | View the organization's Chrome Enterprise connection settings and device details for Chrome OS devices. |
| Chrome Enterprise | Update connection settings | Manage or change the organization's Chrome Enterprise connection settings. |

### Cloud attached devices

| Permission | Action | Description |
| --- | --- | --- |
| Cloud attached devices | Enroll Now | Enrolls an eligible CM device into comanagement. |
| Cloud attached devices | Run CMPivot query | Will hide or show the CMPivot blade. |
| Cloud attached devices | Run script | Will hide or show the Run script action in the Scripts blade. |
| Cloud attached devices | Take application actions | Will hide or show the actions available in the Applications blade. |
| Cloud attached devices | View applications | Will hide or show the Applications blade. |
| Cloud attached devices | View client details | Will hide or show the Client details blade. |
| Cloud attached devices | View collections | Will hide or show the Collections blade. |
| Cloud attached devices | View resource explorer | Will hide or show the Resource explorer blade. |
| Cloud attached devices | View scripts | Will hide or show the Scripts blade. |
| Cloud attached devices | View software updates | Will hide or show the Software updates blade. |
| Cloud attached devices | View timeline | Will hide or show the Timeline blade. |

### Cloud PKI

| Permission | Action | Description |
| --- | --- | --- |
| Cloud PKI | Create certificate authorities (CAs) | Create certificate authorities (CAs) |
| Cloud PKI | Disable and reenable CAs | Disable and reenable CAs |
| Cloud PKI | Read CAs | Read CAs and the leaf certificates issued by them |
| Cloud PKI | Revoke issued leaf certificates | Revoke issued leaf certificates |

### Corporate device identifiers

| Permission | Action | Description |
| --- | --- | --- |
| Corporate device identifiers | Create | Create new corporate device identifiers or import a CSV file containing a list of corporate device identifiers. |
| Corporate device identifiers | Delete | Delete IMEI or serial numbers used as corporate device identifiers. |
| Corporate device identifiers | Read | View the IMEI or serial numbers used as corporate device identifiers. |
| Corporate device identifiers | Update | Change IMEI or serial numbers used as corporate device identifiers. |

### Customization

| Permission | Action | Description |
| --- | --- | --- |
| Customization | Assign | Assign customization options for the Company Portal. |
| Customization | Create | Create customization options for the Company Portal. |
| Customization | Delete | Delete customization options for the Company Portal. |
| Customization | Read | Read customization options for the Company Portal. |
| Customization | Update | Update customization options for the Company Portal. |

### Deployment Plans

| Permission | Action | Description |
| --- | --- | --- |
| Deployment Plans | Create | Create Deployment Plans |
| Deployment Plans | Delete | Delete Deployment Plans |
| Deployment Plans | Read | Read Deployment Plans |
| Deployment Plans | Update | Update Deployment Plans |

### Derived Credentials

| Permission | Action | Description |
| --- | --- | --- |
| Derived Credentials | Modify | Configure the Derived Credentials for your Microsoft Intune tenant. |
| Derived Credentials | Read | View the Derived Credentials for your Microsoft Intune tenant. |

### Device compliance policies

| Permission | Action | Description |
| --- | --- | --- |
| Device compliance policies | Assign | Assign device compliance policies to Microsoft Entra security groups, and assign Exchange on-premises access to Microsoft Entra security groups. |
| Device compliance policies | Create | Create new device compliance policies. |
| Device compliance policies | Delete | Delete device compliance policies or delete Exchange ActiveSync connectors. |
| Device compliance policies | Read | View device compliance policies and the list of Exchange Active Sync Connectors, or view the settings for Exchange on-premises access. |
| Device compliance policies | Update | Change device compliance policies, Exchange ActiveSync connectors, and Exchange on-premises access settings. |
| Device compliance policies | View reports | View, generate, and export device compliance reports. |

### Device configurations

| Permission | Action | Description |
| --- | --- | --- |
| Device configurations | Assign | Assign device configuration profiles or assign device enrollment restrictions to Microsoft Entra security groups. |
| Device configurations | Create | Create new device configuration profiles, or create new device enrollment restrictions. |
| Device configurations | Delete | Delete device configuration profiles, or delete device enrollment restrictions. |
| Device configurations | Read | View device configuration profiles, or view device enrollment restrictions. |
| Device configurations | Update | Change device configuration profiles, or change device enrollment restrictions. |
| Device configurations | Update Windows Backup and Restore | Change Windows Backup and Restore settings. |
| Device configurations | View Reports | View, generate, and export device configuration reports. |

### Device enrollment managers

| Permission | Action | Description |
| --- | --- | --- |
| Device enrollment managers | Read | View the list of device enrollment manager accounts. |
| Device enrollment managers | Update | Create new device enrollment manager accounts, or delete device enrollment manager accounts. |

### Endpoint Analytics

| Permission | Action | Description |
| --- | --- | --- |
| Endpoint Analytics | Create | Create new baselines and edit endpoint analytics settings. |
| Endpoint Analytics | Delete | Edit endpoint analytics settings and delete baselines. |
| Endpoint Analytics | Read | View endpoint analytics scores and performance reports. |
| Endpoint Analytics | Update | Edit endpoint analytics settings and baselines. |

### Endpoint Detection and Response

| Permission | Action | Description |
| --- | --- | --- |
| Endpoint Detection and Response | Assign | Assign Endpoint Detection and Response (EDR) profiles to Microsoft Entra security groups. |
| Endpoint Detection and Response | Create | Create new Endpoint Detection and Response (EDR) profiles. |
| Endpoint Detection and Response | Delete | Delete Endpoint Detection and Response (EDR) profiles. |
| Endpoint Detection and Response | Read | Read Endpoint Detection and Response (EDR) profiles. |
| Endpoint Detection and Response | Update | Update Endpoint Detection and Response (EDR) profiles. |
| Endpoint Detection and Response | View Reports | Generate, view, or export reports for Endpoint Detection and Response (EDR) profiles. |

### Endpoint Privilege Management Elevation Requests

| Permission | Action | Description |
| --- | --- | --- |
| Endpoint Privilege Management Elevation Requests | Modify elevation requests | Allows administrators to approve, deny, or revoke Endpoint Privilege Management (EPM) support approved requests from end users. |
| Endpoint Privilege Management Elevation Requests | View elevation requests | Allows administrators to view Endpoint Privilege Management (EPM) support approved requests. |

### Endpoint Privilege Management Policy Authoring

| Permission | Action | Description |
| --- | --- | --- |
| Endpoint Privilege Management Policy Authoring | Assign | Allows administrators to assign Endpoint Privilege Management (EPM) policies. |
| Endpoint Privilege Management Policy Authoring | Create | Allows administrators to create Endpoint Privilege Management (EPM) policies. |
| Endpoint Privilege Management Policy Authoring | Delete | Allows administrators to delete Endpoint Privilege Management (EPM) policies. |
| Endpoint Privilege Management Policy Authoring | Read | Allows administrators to read Endpoint Privilege Management (EPM) policies. |
| Endpoint Privilege Management Policy Authoring | Update | Allows administrators to update Endpoint Privilege Management (EPM) policies. |
| Endpoint Privilege Management Policy Authoring | View Reports | Allows administrators to view Endpoint Privilege Management (EPM) reports. |

### Endpoint protection reports

| Permission | Action | Description |
| --- | --- | --- |
| Endpoint protection reports | Read | View endpoint protection reports. |

### Enrollment programs

| Permission | Action | Description |
| --- | --- | --- |
| Enrollment programs | Assign profile | Assign profiles for Automated Device Enrollment, Apple School Manager, Apple Business Manager, Apple Configurator, or Windows Autopilot. |
| Enrollment programs | Create device | Import Apple devices for Apple Configurator. |
| Enrollment programs | Create profile | Create new profiles for the Automated Device Enrollment, Apple School Manager, Apple Configurator, or Windows Autopilot. |
| Enrollment programs | Create token | Download the Apple Automated Device Enrollment or Apple School Manager token .pem file. |
| Enrollment programs | Delete device | Delete Apple devices for the Automated Device Enrollment, Apple School Manager, or Apple Configurator |
| Enrollment programs | Delete profile | Delete profiles for the Automated Device Enrollment, Apple School Manager, Apple Configurator, or Windows Autopilot. |
| Enrollment programs | Delete token | Delete Apple Automated Device Enrollment or Apple School Manager token .pem files. |
| Enrollment programs | Enrollment time device membership assignment | Allows Intune to assign devices to Entra ID groups during enrollment. |
| Enrollment programs | Read device | View Apple devices for the Automated Device Enrollment, Apple School Manager, Apple Configurator, or Windows Autopilot devices. |
| Enrollment programs | Read profile | View profiles for the Automated Device Enrollment, Apple School Manager, Apple Configurator, or Windows Autopilot. |
| Enrollment programs | Read token | View the Apple Automated Device Enrollment or Apple School Manager token status. |
| Enrollment programs | Release Apple devices | Release Apple ADE (automated device enrollment) enrolled devices from Apple Business or School Manager and Intune |
| Enrollment programs | Rotate macOS admin password | Rotate local admin account password for macOS devices enrolled through Apple's automated device enrollment |
| Enrollment programs | Sync device | Initiate the Sync command for Windows Autopilot devices. |
| Enrollment programs | Update profile | Manage profiles for the Automated Device Enrollment, Apple School Manager, Apple Configurator, or Windows Autopilot. |
| Enrollment programs | Update token | Upload the Apple Device Enrollment or Apple School Manager token and sync Apple Automated Device Enrollment or Apple School Manager devices. |
| Enrollment programs | View macOS admin password | View local admin account password for macOS devices enrolled through Apple's automated device enrollment |

### Filters

| Permission | Action | Description |
| --- | --- | --- |
| Filters | Create | Create new filter. Learn more https://go.microsoft.com/fwlink/?linkid=2135625 |
| Filters | Delete | Delete filters. Learn more https://go.microsoft.com/fwlink/?linkid=2135625 |
| Filters | Read | View filters. Learn more https://go.microsoft.com/fwlink/?linkid=2135625 |
| Filters | Update | Edit filters. Learn more https://go.microsoft.com/fwlink/?linkid=2135625 |

### Intune data warehouse

| Permission | Action | Description |
| --- | --- | --- |
| Intune data warehouse | Read | View all data and reports from the data warehouse. Data can be used by Power BI or other reporting services. |

### Managed apps

| Permission | Action | Description |
| --- | --- | --- |
| Managed apps | Assign | Assign application protection policies to Microsoft Entra security groups. |
| Managed apps | Create | Create new application protection policies. |
| Managed apps | Delete | Delete application protection policies. |
| Managed apps | Read | View application protection policies and status. |
| Managed apps | Update | Change application protection policies, or delete pending wipe requests for protected apps. |
| Managed apps | Wipe | Create a wipe request to selectively remove company data from a protected app.  |

### Managed Device Cleanup Rules

| Permission | Action | Description |
| --- | --- | --- |
| Managed Device Cleanup Rules | Update | Change the managed device cleanup rules. |

### Managed Device Cleanup Settings

| Permission | Action | Description |
| --- | --- | --- |
| Managed Device Cleanup Settings | Update | Change the managed device cleanup settings. |

### Managed devices

| Permission | Action | Description |
| --- | --- | --- |
| Managed devices | Delete | Delete Intune managed devices. Deleted devices can no longer be managed by Intune, and the device can no longer access company resources. Company data may be wiped from the device if a user tries to check in after it's deleted. |
| Managed devices | Query | Allows Intune to query a managed device for the purposes of retrieving detailed inventory information, device state, or other properties of a managed device from the device itself. |
| Managed devices | Read | View Intune managed devices.  |
| Managed devices | Read Bios Password | Read BIOS password for devices with managed BIOS and firmware configuration. |
| Managed devices | Set primary user | Choose, change, or remove the primary user of a managed device. This permission must be used in combination with the managed devices read and update permissions. |
| Managed devices | Update | Change settings or ownership properties of a managed device. This permission doesn't enable remote actions for devices. To perform remote actions on the device, grant one or more of the Remote Task permissions. |
| Managed devices | View reports | Generate, view, or export reports for managed devices. |

### Managed Google Play

| Permission | Action | Description |
| --- | --- | --- |
| Managed Google Play | Modify | Modify the settings for synchronizing Managed Google Play apps with Microsoft Intune. |
| Managed Google Play | Read |  View the settings for synchronizing Managed Google Play apps with Microsoft Intune. |

### Microsoft Defender ATP

| Permission | Action | Description |
| --- | --- | --- |
| Microsoft Defender ATP | Read | View the connection between Microsoft Intune and Microsoft Defender ATP. |

### Microsoft Store For Business

| Permission | Action | Description |
| --- | --- | --- |
| Microsoft Store For Business | Modify | Modify the settings for synchronizing Microsoft Store for Business apps with Microsoft Intune. |
| Microsoft Store For Business | Read | View the settings for synchronizing Microsoft Store for Business apps with Microsoft Intune. |

### Microsoft Tunnel Gateway

| Permission | Action | Description |
| --- | --- | --- |
| Microsoft Tunnel Gateway | Create | Create Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. |
| Microsoft Tunnel Gateway | Delete | Delete Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. |
| Microsoft Tunnel Gateway | Read | View Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. |
| Microsoft Tunnel Gateway | Update | Update Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel. |

### Mobile apps

| Permission | Action | Description |
| --- | --- | --- |
| Mobile apps | Assign | Assign mobile applications or eBooks to Microsoft Entra security groups. |
| Mobile apps | Create | Add new mobile applications to Intune such as store apps, line-of-business apps, web-links, or built-in apps. You can also add books purchased through the Apple Volume Purchase Program or add eBook categories. You can set up iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. *See the note following this table regarding Apple Volume Purchase Program (VPP) apps.* |
| Mobile apps | Delete | Delete mobile applications such as store apps, line-of-business apps, web-links, or built-in apps. You can also delete books purchased through the Apple Volume Purchase Program or delete eBook categories. You can delete iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. *See the note following this table regarding Apple Volume Purchase Program (VPP) apps.*|
| Mobile apps | Read | View mobile applications such as store apps, line-of-business apps, web-links, or built-in apps. You can also view books purchased through the Apple Volume Purchase Program or add eBook categories. You can view iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. *See the note following this table regarding Apple Volume Purchase Program (VPP) apps.* |
| Mobile apps | Relate | Create relationships with other managed apps using Dependencies and Supersedence features. |
| Mobile apps | Update | Manage mobile applications such as store apps, line-of-business apps, web-links, or built-in apps. You can also manage books purchased through the Apple Volume Purchase Program or add eBook categories. You can manage iOS VPP Tokens, Windows Symantec certificates, Windows side loading keys, app categories, or the Android for Work connection. The Mobile Applications Create permission may be required for certain application update scenarios. *See the note following this table regarding Apple Volume Purchase Program (VPP) apps.* |


> [!NOTE]
> You can view and manage Apple Volume Purchase Program (VPP) apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change doesn't apply to Intune for Education tenants who still need to assign the **Managed apps** permission.

### Mobile Threat Defense

| Permission | Action | Description |
| --- | --- | --- |
| Mobile Threat Defense | Modify | Add, remove, or modify the Mobile Threat Defense connectors between Intune and your chosen MTD vendors |
| Mobile Threat Defense | Read | View the Mobile Threat Defense connectors between Intune and your chosen MTD vendors |

### Multi Admin Approval

| Permission | Action | Description |
| --- | --- | --- |
| Multi Admin Approval | Approval for Multi Admin Approval | Approve or reject approval requests for Multi Admin Approval configuration. |
| Multi Admin Approval | Create access policy | Create access policies for Multi Admin Approval. |
| Multi Admin Approval | Delete access policy | Delete access policies for Multi Admin Approval. |
| Multi Admin Approval | Read access policy | Read access policies for Multi Admin Approval. |
| Multi Admin Approval | Update access policy | Update access policies for Multi Admin Approval. |

### Operating System Recovery Configurations

| Permission | Action | Description |
| --- | --- | --- |
| Operating System Recovery Configurations | Assign Profiles | Assign Operating System Recovery profiles. |
| Operating System Recovery Configurations | Create Profiles | Create Operating System Recovery profiles. |
| Operating System Recovery Configurations | Delete Profiles | Delete Operating System Recovery profiles. |
| Operating System Recovery Configurations | Read Profiles | Read Operating System Recovery profiles. |
| Operating System Recovery Configurations | Update Profiles | Update Operating System Recovery profiles. |

### Organization

| Permission | Action | Description |
| --- | --- | --- |
| Organization | Create | Create tenant settings such as device categories and Exchange connectors. |
| Organization | Delete | Delete tenant settings such as device categories and Exchange Connectors. |
| Organization | Read | View tenant settings such as device categories and Exchange Connectors. This permission is required to activate all enrollment workflows. |
| Organization | Update | Manage tenant settings, device categories, and Exchange Connectors. |

### Organizational Messages

| Permission | Action | Description |
| --- | --- | --- |
| Organizational Messages | Assign | Assign organizational messages. |
| Organizational Messages | Create | Create and assign organizational messages. |
| Organizational Messages | Delete | Delete organizational messages. |
| Organizational Messages | Read | Read organizational messages. |
| Organizational Messages | Update | Cancel organizational messages. |
| Organizational Messages | Update organizational message control | Enable or block organizational messages directly from Microsoft, while allowing admin messages to display. |

### Partner Device Management

| Permission | Action | Description |
| --- | --- | --- |
| Partner Device Management | Modify | Configure the Compliance Connector for Jamf. |
| Partner Device Management | Read | View the Compliance Connector for Jamf. |

### Policy Sets

| Permission | Action | Description |
| --- | --- | --- |
| Policy Sets | Assign | Assign Policy Sets to Microsoft Entra security groups. |
| Policy Sets | Create | Create a new Policy Set. |
| Policy Sets | Delete | Delete Policy Sets. |
| Policy Sets | Read | View Policy Sets. |
| Policy Sets | Update | Change a Policy Set, or add items to a Policy Set. |

### Quiet Time policies

| Permission | Action | Description |
| --- | --- | --- |
| Quiet Time policies | Assign | Assign quiet time policies to Microsoft Entra security groups. |
| Quiet Time policies | Create | Create new quiet time policies. |
| Quiet Time policies | Delete | Delete quiet time policies. |
| Quiet Time policies | Read | View device quiet time policies. |
| Quiet Time policies | Update | Change quiet time policies. |
| Quiet Time policies | View Reports | View, generate, and export quiet time policy reports. |

### Remote assistance connectors

| Permission | Action | Description |
| --- | --- | --- |
| Remote assistance connectors | Read | View the status of the TeamViewer connector and remote help. This permission isn't required to initiate remote assistance requests for devices. |
| Remote assistance connectors | Update | Manage the state of the TeamViewer connector and remote help. This permission also requires the Remote assistance connectors \\| Read permission to view the status of the TeamViewer connector and remote help. |
| Remote assistance connectors | View reports | View, generate and export remote help sessions and monitor reports. |

### Remote Help app

| Permission | Action | Description |
| --- | --- | --- |
| Remote Help app | Elevation | For Windows devices, elevation allows the helper to enter UAC credentials when prompted on the sharer's device when remote help is enabled. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access. |
| Remote Help app | Take full control | Take full control allows the helper to view and control the sharer's device when Remote Help is enabled for all platforms we support. |
| Remote Help app | Unattended control | For Android devices, unattended control starts Remote Help as soon as the helper selects a new session, without a sharer having to grant access. |
| Remote Help app | View screen | View screen allows the helper to view the sharer's device when Remote Help is enabled for all platforms we support. |

### Remote tasks
<!-- This permission/action pulled via graph is pending review.  
| Remote tasks | Change organizational unit | Move a Chrome Enterprise device to an existing organizational unit in your Google Workspace domain. |  -->

| Permission | Action | Description |
| --- | --- | --- |
| Remote tasks | Bypass activation lock | Remove the Activation Lock from supervised devices without requiring the user's Apple ID and password. This may be required if a user leaves the company and returns the device; without the user's Apple ID and password, there's no way to reactivate the device. Or, you need to reassign some devices to a different department during a device refresh in your organization. You can only reassign devices that don't have Activation Lock enabled. You must also have the *Managed Device > Read* permission to view devices in the Azure portal before initiating this remote task. |
| Remote tasks | Change assignments | Allows IT Admin to initiate a change assignments action. Action allows the selection of assigned applications and configuration to be removed from a device. Additionally, previously removed applications and configuration to be restored on the device. | 
| Remote tasks | Clean PC | Initiate a Fresh start device action. This action removes any apps that are installed on a Windows 10 PC that's running the Creators Update. Then, it automatically updates the PC to the latest version of Windows. |
| Remote tasks | Collect diagnostics | Collect device diagnostics |
| Remote tasks | Disable lost mode | Turn off lost mode for an iOS or ChromeOS device. |
| Remote tasks | Enable lost mode | Initiate lost mode on lost or stolen iOS or ChromeOS devices. This mode lets you enter a message and a phone number that appears on the lock screen of the device. To use lost mode, the device must be a corporate-owned iOS device that is in supervised mode. |
| Remote tasks | Enable Windows IntuneAgent | Enable Windows Intune agent. |
| Remote tasks | Get FileVault key. | Get Mac FileVault key. |
| Remote tasks | Indicates remote device action to initiate Mobile Device Management (MDM) attestation if device is capable for it. |  |
| Remote tasks | Initiate Configuration Manager action | Initiate a remote action on a device managed by Configuration Manager. |
| Remote tasks | Locate device | View the location of a lost or stolen corporate-owned device on a map. Can locate supervised iOS/iPadOS devices, Android dedicated devices (COSU), and Windows devices. |
| Remote tasks | Manage shared device users | Sign out the user with the current session on a shared device.  This action doesn't delete users from a shared device, it only forces the user with a current session to be logged out. |
| Remote tasks | Offboard | Offboard the devices associated with a user, when the user is leaving the organization. |
| Remote tasks | Offer remote assistance | Initiate a remote assistance session with a user's device by using a remote assistance provider. The remote assistance option for your provider must be enabled for your tenant. |
| Remote tasks | Play sound to locate lost devices | Play a sound to locate lost Android dedicated devices, or iOS devices placed in MDM lost mode. |
| Remote tasks | Reboot now | Initiates a device restart. This causes the device you choose to be restarted. The device owner isn't automatically notified of the restart, and they might lose work. |
| Remote tasks | Recover MDM Key | Initiate Mobile Device Management (MDM) certificate's private key recovery with TPM attestation |
| Remote tasks | Remote lock | The Remote lock device action locks the device. To unlock the device, the device owner enters their passcode. You can remotely lock devices that have a PIN or password set. Devices that don't have a PIN or password can't be remotely locked. |
| Remote tasks | Remove Device Firmware Configuration Interface Management. | Allows admin to initiate removal of device from Device Firmware Configuration Interface management before deleting the Intune and Autopilot records. |
| Remote tasks | Reset passcode | Initiates a forced removal of the passcode, and requires the device user to set a new passcode. Supported on iOS devices, and certain later versions of Android and Android for work. Not supported on older Android versions, macOS, or Windows. |
| Remote tasks | Restore Managed Home Screen | Manually restore Managed Home Screen on Android Enterprise devices to return them to kiosk mode from a temporarily suspended state. Complements the temporary suspend action for complete kiosk mode management. |
| Remote tasks | Retire | Initiates a retire action for a device. Also called remove company data. The Remove company data action removes managed app data (where applicable), settings, and email profiles that were assigned by using Intune. The device is removed from Intune management. This happens the next time the device checks in and receives the remote Remove company data action. Remove company data leaves the user's personal data on the device. For ChromeOS devices, this starts a deprovision action. |
| Remote tasks | Revoke App Licenses | Revokes any iOS VPP application licenses that have been associated with the device. |
| Remote tasks | Rotate BitLockerKeys (preview) | Initiates a key rotation for BitLocker Recovery Passwords on the device. |
| Remote tasks | Rotate FileVault key. | Rotate Mac FileVault key. |
| Remote tasks | Rotate Local Admin Password | Initiates a manual rotation for the local admin password on the device |
| Remote tasks | Rotate macOS recovery lock password | Rotate the recovery lock password for macOS devices |
| Remote tasks | Run Pause Configuration Refresh | Initiate On Demand pause configuration refresh |
| Remote tasks | Run Remediation | Initiate On Demand Proactive Remediation |
| Remote tasks | Send custom notifications | Allows admin to send customized notifications to devices. Devices receive notifications in Company Portal. |
| Remote tasks | Set device name | Set or change the name of a device.  |
| Remote tasks | Shut down | Initiates a shutdown of the device, and will automatically close all applications and running services and leave the device in a powered-off state. |
| Remote tasks | Sync devices. | Initiates a sync operation on the device and forces the selected device to immediately check in with Intune. When a device checks in, it immediately receives any pending actions or policies that have been assigned to it. |
| Remote tasks | Temporarily suspend Managed Home Screen | Remotely suspend Managed Home Screen on Android Enterprise devices in kiosk mode, allowing temporary access to the default launcher experience. Supports automatic restoration after a configured time period without requiring user interaction or PIN sharing. |
| Remote tasks | Update cellular data plan | Activate the data plan for cellular iOS/iPadOS devices that support eSIM.  |
| Remote tasks | Update device account | Allows changing the device account associated with Surface Hub devices, and set authentication options such as password rotation. |
| Remote tasks | View macOS recovery lock password | View the recovery lock password in the Recovery Keys blade of macOS devices |
| Remote tasks | Windows Defender | Initiates a Windows Defender signature update. |
| Remote tasks | Wipe | Initiates a wipe of the device. Also called a "factory reset." The Factory reset action restores a device to its factory default settings. The user data is kept or wiped depending on whether or not you choose the Retain enrollment state and user account checkbox. For ChromeOS devices, this starts either a wipe or a factory reset (Powerwash) action. |

### Roles

| Permission | Action | Description |
| --- | --- | --- |
| Roles | Assign | Assign Intune built-in or custom roles to Microsoft Entra security groups |
| Roles | Create | Create new Intune custom roles. Built-in roles are created by Intune automatically. |
| Roles | Delete | Delete a custom Intune role. You can't delete built-in roles. |
| Roles | Read | View permissions, role assignments, member groups, and scope groups for any built-in or custom Intune role. |
| Roles | Update | Update custom role permissions and role assignments for built-in or custom roles. Role assignments define the administrators and end user scope for the role.  |

### Security baselines

| Permission | Action | Description |
| --- | --- | --- |
| Security baselines | Assign | Assign Security Baseline profiles to Microsoft Entra security groups. |
| Security baselines | Create | Create new Security Baseline profiles. |
| Security baselines | Delete | Delete Security Baseline profiles. |
| Security baselines | Read | View Security Baseline profiles or profiles reporting or Template reporting for all Security Baseline workspace. |
| Security baselines | Update | Update Security Baseline profiles. |

### Security tasks

| Permission | Action | Description |
| --- | --- | --- |
| Security tasks | Read | View security tasks. |
| Security tasks | Update | Update security tasks. |

### ServiceNow

| Permission | Action | Description |
| --- | --- | --- |
| ServiceNow | Update Connector | Update ServiceNow connection. |
| ServiceNow | View Incidents | View incidents from ServiceNow. |

### Telecom expenses

| Permission | Action | Description |
| --- | --- | --- |
| Telecom expenses | Read | View settings and status of telecom expense partner connector. The telecom expense partner connector feature was deprecated and this permission is no longer supported after June  2025. |
| Telecom expenses | Update | Modify or activate telecom expense management partner connector. The telecom expense partner connector feature is deprecated and this permission is no longer supported after June, 2025. |

### Tenant attached recommendations

| Permission | Action | Description |
| --- | --- | --- |
| Tenant attached recommendations | Read | View Tenant attached recommendations. Recommendations are methods to improve site health and device management experience. |

### Terms and conditions

| Permission | Action | Description |
| --- | --- | --- |
| Terms and conditions | Assign | Assign terms and conditions to Microsoft Entra security groups. |
| Terms and conditions | Create | Create new terms and conditions. |
| Terms and conditions | Delete | Delete an existing terms and conditions. |
| Terms and conditions | Read | View terms and conditions. |
| Terms and conditions | Update | Manage existing terms and conditions but not assignments. |

### Windows Enterprise Certificate

| Permission | Action | Description |
| --- | --- | --- |
| Windows Enterprise Certificate | Modify | Add, remove, or modify the code-signing certificate used to distribute line-of-business apps to your managed Windows devices. |
| Windows Enterprise Certificate | Read | View the code-signing certificate used to distribute line-of-business apps to your managed Windows devices. |

## Next steps

- [Assign a role to a user](assign-role.md)
- [Learn more about role-based access control in Intune](role-based-access-control.md)
