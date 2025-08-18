---
# required metadata

title: Enable Windows backup and restore in Microsoft Intune  
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

Enable users to securely sync their settings to the cloud and restore them on new or reimaged devices. Together, Microsoft Intune and Windows Backup for Organization lets users back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device during enrollment. The restore option is presented to users on its own screen during device enrollment.   

Windows Backup for Organizations is a feature that's comprised of the [Windows backup and restore settings](/windows/configuration/windows-backup/catalog) and is an option that can: 

* Reduce migration overhead
* Minimize user disruption  
* Strengthen device resilience against incidents  
* Simplify your organization's transition to Windows 11

You can enable Windows backup and restore for devices in the Microsoft Intune admin center under **Devices** > **Enrollment**. After you turn on the restore option, users turning on their devices for the first time see the corresponding restore page during device enrollment. This is a tenant wide setting, so it applies to all users.  

## Benefits  

Windows Backup for Organizations ensures that users have a consistent and personalized experience across different devices. Benefits include:  

* Reduced troubleshooting: Confidently reset devices knowing that users can recover and return to previous settings.   
* Seamless experience: Smoothly transition from devices running Windows 10 to devices running Windows 11 using saved backups. 
* Enhanced productivity: Minimize downtime and maximize user productivity, whether resetting the device or reimaging, by restoring user settings to their preferred and familiar PC preferences.  

## Prerequisites 

To use the backup functionality, devices must be:  

* Microsoft Entra hybrid joined or Microsoft Entra joined.  
* Running a currently supported version of either Windows 10 or Windows 11. Supported versions include:  
  * Windows 10, version 22H2, build 19045.5917 or later  
  * Windows 11, version 22H2, build 22621.5413 or later   
  * Windows 11, version 23H2, build 22631.5413 or later   
  * Windows 11, version 24H2, build 26100.4202 or later     

The restore feature is available on devices that meet the following requirements:  

- Windows 11, version 22H2 or later.
- The device user must have at least one backup profile. 
- If Autopilot is used, the Autopilot profile must be configured to use [user-driven mode](), not self-deploying mode.  
- Must be [Microsoft Entra joined]().  

Additionally, you're required to configure these settings: 
- [AFS configuration]()
- [NDUP configuration]() must be turned on

## RBAC and tenant wide targeting 
The restore setting for Windows Backup for Organizations is a tenant-wide setting. This means the restore setting is either turned on or off for all Windows devices in a tenant. The default configuration is **Not configured**, which turns off the restore setting for all devices.  

To configure the restore setting, you must have Intune Service Administrator permissions.  

## Modify Conditional Access policy  
The Microsoft Entra user's access token is used during restore operations to access the user’s backup data. If you have a Conditional Access policy that blocks Microsoft Intune from acquiring the Microsoft Entra user’s access token from the Microsoft Activity Feed Service (AFS), you might see one of the following error messages. 

  |Error title| Error description | 
  | -----| ----- |
  |You don't have access to this|Your sign-in was successful but you don't have the permissions to access this resource. |
  |You can't get there from here |This application contains sensitive information and can only be accessed from: Devices or client applications that meet TenantMonkey engagement compliance policy. If this is a personal device you can choose to let TenantMonkey manage your device by going to **Settings** > **Accounts** > **Access work or school** and clicking on **Connect**. When you're done come back and try again.   |

To view Conditional Access policies for your tenant, sign in to entra.microsoft.com and go to **Identity** > **Protection** > **Conditional Access**.  

A common policy that can block token acquisition is one that allows cloud apps only for compliant devices. The CA policies need to allow access to the Microsoft Activity Feed Service (AFS) from non-compliant devices. Since the AFS token is acquired during OOBE, the device is not yet compliant. You can add a CA policy to opt-in to Multi-Factor Authentication (MFA) when accessing the AFS as an additional security step. 



## Enrollment    

To enable Windows Backup for Organization during enrollment, configure your backup and restore settings in the Microsoft Intune admin center. There are two areas where you need to configure settings: in the settings catalog, and under enrollment.  

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
Known issues with Windows Backup for Organization include: 

- This feature isn't supported in Government cloud.  

- This feature doesn't work for shared or userless devices. 

- The restore feature isn't supported for versions earlier than Windows 11, version 22H2.  

- When corporate accounts are used on Hyper-V virtual machines (VM) with phishing-resistant multifactor authentication (MFA) enforced, users are prompted to authenticate using a security key or smart card. However, due to Hyper-V VM limitations, these authentication methods can't pass through, resulting in an undesirable UI experience and preventing users from completing the authentication process. 

>[!NOTE]
> This issue is specific to VMs, particularly when users initially sign in with weaker authentication methods (such as a password or authenticator app) and phising-resistant MFA is subsequently enforced. 

- This feature isn't supported with the following provisioning methods:  

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




