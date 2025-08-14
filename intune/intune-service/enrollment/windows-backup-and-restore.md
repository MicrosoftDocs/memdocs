---
# required metadata

title: Enable Windows backup and restore  
titleSuffix: Microsoft Intune
description: Enable Windows backup and restore in Intune for employees or students.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: laurawi
ms.date: 08/14/2025
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

Enable users to securely sync their settings to the cloud and restore them on new or reimaged devices. Together, Microsoft Intune and Windows Backup for Organization lets users back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device during enrollment. The restore option is presented to users on its own screen during device enrollment.   

Windows Backup for Organizations is a feature that's comprised of the backup and restore settings and is an option that can: 

* Reduce migration overhead
* Minimize user disruption  
* Strengthen device resilience against incidents  
* Simplify your organization's transition to Windows 11

You can enable Windows backup and restore for devices in the Microsoft Intune admin center under **Devices** > **Enrollment**. After you turn on the restore option, users turning their devices on for the first time see the corresponding restore page during device enrollment. This is a tenant wide setting, so it applies to all users.  

## Benefits  

Windows Backup for Organizations ensures that users have a consistent and personalized experience across different devices. Benefits include:  

* Reduced troubleshooting: Confidently reset devices knowing that users can recover and return to previous settings.   
* Seamless experience: Smoothly transition from devices running Windows 10 to devices running Windows 11 using saved backups. 
* Enhanced productivity: Minimize downtime and maximize user productivity, whether resetting the device or reimaging, by restoring user settings to their preferred and familiar PC preferences.  

## Prerequisites 

To use the backup functionality, devices must be:  

* Microsoft Entra hybrid joined or Microsoft Entra joined.  
* Running a current supported version of either Windows 10 or Windows 11. Supported versions include:  
  * Windows 10, version 22H2, build 19045.5917 or later  
  * Windows 11, version 22H2, build 22621.5413 or later   
  * Windows 11, version 23H2, build 22631.5413 or later   
  * Windows 11, version 24H2, build 26100.4202 or later     

The restore feature is available on devices that meet the following requirements:  

- Windows 11, version 22H2 or later.
- The device user must have at least one backup profile. 
- If Autopilot is used, the Autopilot profile must be configured to use [user-driven mode](), not self-deploying mode.  
- Must be [Microsoft Entra joined]().  

Additionally, you are required to configure these settings: 
- [AFS configuration]()
- [NDUP configuration]() must be turned on

## RBAC and tenant wide targeting 
The restore setting for Windows Backup for Organizations is a tenant-wide setting. This means the restore setting is either turned on or off for all Windows devices in a tenant. The default configuration is **Not configured**, which turns off the restore setting for all devices.  

To configure the restore setting, you must have Intune Service Administrator permissions.  

## Erollment    

To enable Windows Backup for Organization during enrollment, configure your backup and restore settings in the Microsoft Intune admin center. There are two areas where you need to configure settings: in the settings catalog, and under enrollment.  

Complete these steps to configure the backup settings in the settings catalog. 
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an [Intune service administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).
2. Go to **Devices** > **Managed devices** > **Configuration**.
3. Create a new policy. For **Platform**, select **Windows 10 and later**, and for **Profile type**, select **Settings Catalog**.
4. Under the **Sync your settings** category, find the **Enable Windows backup** setting. Select the setting to enable it.
5. Finish the remaining steps to create your policy. Then select **Save**.  

Complete these steps to configure the restore setting for enrollment. 
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an [Intune service administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).  
2. Go to **Devices** > **Enrollment**.  
3. Select the **Windows** tab. 
4. Under **Enrollment options**, select **Windows Backup and Restore (preview)**.  
5. For **Show restore page**, select **On**. 

    > [!TIP]
    > Before a user can restore a backup, you have to set up the backup settings in the settings catalog. To go to the settings catalog, select **Go to Settings Catalog to configure backup settings**. 

6. Select **Save**.

The **Last modified** date updates to account for recent changes. Return to **Windows Backup and Restore** anytime to view and edit the setting again.   




