---
# required metadata

title: Enable Windows Backup for Organizations in Microsoft Intune  
titleSuffix: Microsoft Intune
description: Enable Windows backup and restore in Intune for employees or students.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: laurawi
ms.date: 08/18/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Windows Backup for Organizations in Microsoft Intune    

*Applies to: Windows 10, Windows 11*  

 > [!NOTE]
 > This feature is in public preview. For more information on what that means, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Enable users to securely sync their settings to the cloud and restore them on new or reimaged devices. Together, Microsoft Intune and Windows Backup for Organizations lets users back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device during enrollment. 

Windows Backup for Organizations is a feature that's made up of the [Windows backup and restore settings](/windows/configuration/windows-backup/catalog) and is an option that can: 

* Reduce migration overhead
* Minimize user disruption  
* Strengthen device resilience against incidents  
* Simplify your organization's transition to Windows 11

You can enable Windows backup and restore for devices in the Microsoft Intune admin center within the settings catalog, and under **Devices** > **Enrollment**. The restore setting is a tenant-wide setting that applies to all users. After you turn on the restore option, users turning on their devices for the first time see the corresponding restore page during device enrollment.  

## Benefits  

Windows Backup for Organizations ensures that users have a consistent and personalized experience across different devices. Benefits include:  

* Reduced troubleshooting: Confidently reset devices knowing that users can recover and return to previous settings.   
* Seamless experience: Smoothly transition from devices running Windows 10 to devices running Windows 11 using saved backups. 
* Enhanced productivity: Minimize downtime and maximize user productivity, whether resetting the device or reimaging, by restoring user settings to their preferred and familiar PC preferences.  

## Prerequisites 

To use the backup functionality, devices must be:  

* Microsoft Entra hybrid joined or Microsoft Entra joined.  
* Running a currently supported version of either Windows 10 or Windows 11. Supported versions include:  
  * Windows 10, version 22H2, build 19044.6216 or later
  * Windows 11, version 22H2, build 22621.5768 or later
  * Windows 11, version 23H2, build 22631.5768 or later
  * Windows 11, version 24H2, build 26100.4946 or later     

The restore feature is available on devices that meet the following requirements:  

- Must be [Microsoft Entra joined](/entra/identity/devices/concept-directory-join).  
- The restore feature is available on devices that are either on August 2025 cumulative update or meet the following requirements:
  * Windows 11, version 22H2, build 22621.3958 or later
  * Windows 11, version 23H2, build 22631.3958 or later
  * Windows 11, version 24H2, build 26100.1301 or later 
- The device user must have at least one backup profile.
- Enable the Install Windows quality updates policy. If you're on a build older than July 2025, verify that the setting **Install Windows quality updates** is enabled for your devices in order to leverage the feature. 
- If Autopilot is used, the Autopilot profile must be configured to use [user-driven mode](/autopilot/user-driven), not self-deploying mode.   

Additionally, you're required to configure these settings:   
- Configure the Windows quality updates setting, an [enrollment status page feature](windows-enrollment-status.md).     

## RBAC and tenant wide targeting 
The restore setting for Windows Backup for Organizations is a tenant-wide setting. This means the restore setting is either turned on or off for all Windows devices in a tenant. The default configuration is **Not configured**, which turns off the restore setting for all devices.  

To configure the restore setting, you must have Intune Service Administrator permissions.  

## Enrollment    

To enable Windows Backup for Organizations during enrollment, configure your backup and restore settings in the Microsoft Intune admin center. There are two areas where you need to configure settings: in the settings catalog, and under enrollment.  

Complete these steps to configure the backup settings in the settings catalog. 
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an [Intune service administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).
1. Go to **Devices** > **Managed devices** > **Configuration**.
1. Create a new policy.
   1. For **Platform**, select **Windows 10 and later**.
   2. For **Profile type**, select **Settings Catalog**.
1. Under the **Sync your settings** category, find the **Enable Windows backup** setting. Select the setting to enable it.
1. Finish the remaining steps to create your policy. Then select **Save**.  

Complete these steps to configure the restore setting for enrollment. 
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an [Intune service administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).  
1. Go to **Devices** > **Enrollment**.  
1. Select the **Windows** tab. 
1. Under **Enrollment options**, select **Windows Backup and Restore (preview)**.  
1. For **Show restore page**, select **On**. 

    > [!TIP]
    > Before a user can restore a backup, you have to set up the backup settings in the settings catalog. To go to the settings catalog, select **Go to Settings Catalog to configure backup settings**. 

1. Select **Save**.

The **Last modified** date updates to account for recent changes. Return to **Windows Backup and Restore** anytime to view and edit the setting again.   

## Known issues  
Known issues with Windows Backup for Organizations include: 

- This feature isn't supported in Government cloud or 21Vianet.  

- This feature doesn't work for shared or userless devices. 

- The restore feature isn't supported for versions earlier than Windows 11, version 22H2.  

- When corporate accounts are used on Hyper-V virtual machines (VM) with phishing-resistant multifactor authentication (MFA) enforced, users are prompted to authenticate using a security key or smart card. However, due to Hyper-V VM limitations, these authentication methods can't pass through, resulting in an undesirable UI experience and preventing users from completing the authentication process. 

>[!NOTE]
> This issue is specific to VMs, particularly when users initially sign in with weaker authentication methods (such as a password or authenticator app) and phishing-resistant MFA is subsequently enforced. 

- The restore feature isn't supported with the following provisioning methods:  

  - Hybrid Azure AD Join  
  - Workplace Join  
  - Self-deployment mode  
  - Windows Autopilot for pre-provisioned devices  
  - Windows Autopilot reset flow  
  - Manual enrollment through the Windows Settings app  
  - Enrollment via Group Policy  
  - Enrollment via Configuration Manager co-management  

- This feature isn't supported on the following SKUs.  

  |Edition| SKU | 
  | -----| ----- |
  |CloudEdition |CloudEdition, Windows 11 SE (203) |
  |CloudEditionN |CloudEditionN, Windows 11 SE N (202) |
  |Holographic |Windows 10 Holographic (136) |
  |IoTUAP |Windows 10 IoT Core (123) |
  |IoTUAPCommercial |Windows 10 IoT Core Commercial (131) |
  |PPIPro |Windows 10 TeamOS (119) |




