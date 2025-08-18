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

 > [!NOTE]
 > This feature is in public preview. For more information on what that means, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Enable users to securely sync their settings to the cloud and restore them on new or reimaged devices. Together, Microsoft Intune and Windows Backup for Organization lets users back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device during enrollment. 

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
  * Windows 10, version 22H2, build 19045.5917 or later  
  * Windows 11, version 22H2, build 22621.5413 or later   
  * Windows 11, version 23H2, build 22631.5413 or later   
  * Windows 11, version 24H2, build 26100.4202 or later     

The restore feature is available on devices that meet the following requirements:  

- Must be [Microsoft Entra joined](/entra/identity/devices/concept-directory-join).  
- Must be running Windows 11, version 22H2 or later. 
- The device user must have at least one backup profile. 
- If Autopilot is used, the Autopilot profile must be configured to use [user-driven mode](/autopilot/user-driven), not self-deploying mode.   

Additionally, you're required to configure these settings: 
- [Add Microsoft Activity Feed Service to Conditional Access policy](#modify-conditional-access-policy).  
- Configure the Windows quality updates setting, an [enrollment status page feature](windows-enrollment-status.md).     

## RBAC and tenant wide targeting 
The restore setting for Windows Backup for Organizations is a tenant-wide setting. This means the restore setting is either turned on or off for all Windows devices in a tenant. The default configuration is **Not configured**, which turns off the restore setting for all devices.  

To configure the restore setting, you must have Intune Service Administrator permissions.  

## Modify Conditional Access policy  
The Microsoft Entra user's access token is used during restore operations to access the user’s backup data. If you have a Conditional Access policy that blocks Microsoft Intune from acquiring the Microsoft Entra user’s access token from the Microsoft Activity Feed Service, you might see one of the following error messages. 

  |Error title| Error description | 
  | -----| ----- |
  |You don't have access to this|Your sign-in was successful but you don't have the permissions to access this resource. |
  |You can't get there from here |This application contains sensitive information and can only be accessed from: Devices or client applications that meet TenantMonkey engagement compliance policy. If this is a personal device you can choose to let TenantMonkey manage your device by going to **Settings** > **Accounts** > **Access work or school** and clicking on **Connect**. When you're done come back and try again.   |

To view Conditional Access policies for your tenant, sign in to entra.microsoft.com and go to **Identity** > **Protection** > **Conditional Access**.  

A common policy that can block token acquisition is one that allows only cloud apps for compliant devices. Each Conditional Access policy needs to allow access to the Microsoft Activity Feed Service from noncompliant devices. Since the Microsoft Activity Feed Service token is acquired during the out-of-box-experience (OOBE), a new device is not yet compliant. You can add a Conditional Access policy to opt in to multifactor authentication (MFA) when accessing the Microsoft Activity Feed Service, which adds another security step.   

To configure access to the Microsoft Activity Feed Service, include the Microsoft Activity Feed Service in the list of cloud apps for Conditional Access. 

1. The service principal for the Microsoft Activity Feed Service app needs to be registered with your tenant. 
  1. Go to [Try Microsoft Graph APIs](https://developer.microsoft.com/graph/graph-explorer) and sign in with a tenant admin account. 
  1. If prompted to, provide consent to Graph Explorer.  
1. Select your account picture and choose **Consent to Permissions**. 
1. A pane opens with a list of permissions. Search for and expand **APIConnectors**.  
1. Select **Consent** for all permissions listed under **APIConnectors**. In the new window that opens, confirm that you're consenting to these permissions.   
1. In Graph Explorer, change the request type to **POST**.
1. For the URL, enter **https://graph.microsoft.com/v1.0/servicePrincipals**.  
1. In the body of the request, enter the following JSON snippet to add the app ID for the Microsoft Activity Feed Service:  

   ```json
   { 

      “appId”: “d32c68ad-72d2-4acb-a0c7-46bb2cf93873” 

   }  
   ```  
10. Select **Run query**. 

   > [!TIP]
   > If the request fails, select **Modify permissions** and consent to the Application.ReadWrite.All permission. Then try the request again.  

11. After the request is successful, return to the Conditional Access page in Microsoft Entra ID. You should see the Microsoft Activity Feed Service app in your Conditional Access policy list.  

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
> This issue is specific to VMs, particularly when users initially sign in with weaker authentication methods (such as a password or authenticator app) and phishing-resistant MFA is subsequently enforced. 

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




