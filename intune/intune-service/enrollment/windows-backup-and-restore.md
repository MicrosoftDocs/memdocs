---
# required metadata

title: Enable Windows backup and restore  
titleSuffix: Microsoft Intune
description: Enable Windows backup and restore in Intune for employees or students.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: laurawi
ms.date: 08/1/2025
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

# Set up Windows backup and restore  

*Applies to: Windows 10, Windows 11*

Enable users to securely sync their settings to the cloud and restore them on new or reimaged devices. When used together, the Microsoft Intune Windows backup and restore settings let users back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device during enrollment. The restore option is presented to users on its own screen during device enrollment.   

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
* Running a current supported version of either Windows 10 or Windows 11.  

To take full advantage of the feature and also restore settings on new or reimaged Windows devices, you must have:  

- Windows 11, version 22H2 and later
- Microsoft Entra joined devices
- An active Microsoft Intune test tenant 
- Microsoft Intune service administrator permissions  

You also need to be part of [Microsoft Management Customer Connection Program (CCP)](https://techcommunity.microsoft.com/blog/windows-itpro-blog/innovate-with-the-microsoft-management-customer-connection-program/4284753). If you're not a current member, [opt in to Join MMCCP](aka.ms/JoinMMCCP).  

## Enable Windows backup and restore   
 
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an [Intune service administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).  
2. Go to **Devices** > **Enrollment**.  
3. Select the **Windows** tab. 
4. Under **Enrollment options**, select **Windows Backup and Restore**.  
7. For **Show restore page**, select **On**. 

>[!TIP]
> Before a user can restore a backup, you have to set up the backup settings in the settings catalog. To go to the settings catalog, select **Go to Settings Catalog to configure backup settings**. For more information about backup settings, see []().  

8. Select **Save**.

The **Last modified** date updates to account for your recent changes. Return to **Windows Backup and Restore** anytime to view and edit the setting again.   

## Reporting  




<!-- >> [!div class="mx-imgBorder"]
> ![Example image of an enrollment notification configured in Intune, notifying the recipient that a device named *Nia's iPhone" was enrolled, and includes HTML elements such as bolded font and a hyperlink, device details, contact information, and privacy statement.](./media/enrollment-notifications/enrollment-notification-message.png) -->




