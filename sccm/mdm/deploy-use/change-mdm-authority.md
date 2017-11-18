---
# required metadata

title: "Change your MDM authority"
titleSuffix: "Configuration Manager"
description: "Learn how to change the MDM authority from Configuration Manager (hybrid) to Intune standalone"
keywords:
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology:
    - configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49

---
# Change your MDM authority
Beginning in Configuration Manager version 1610, you can change your MDM authority without having to contact Microsoft Support and without having to unenroll and reenroll your existing managed devices. This article provides the steps to change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid) to Intune standalone. When you complete the steps in this article, devices will be managed by Microsoft Intune in the [Azure portal](https://portal.azure.com). 

> [!Note]    
> If you want to change an existing Microsoft Intune tenant, with the MDM authority set to Intune, to Configuration Manager (hybrid), see [Change the MDM authority](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> This article is to change your MDM authority when you have not previously migrated users. To change your MDM authority after you have [migrated a subset of users](migrate-hybridmdm-to-intunesa.md), see [Change your MDM authority](migrate-change-mdm-authority.md).

## Key Considerations
After you change to the new MDM authority, there will likely be transition time (up to eight hours) before the device checks in and synchronizes with the service. You must configure settings in the new MDM authority (Intune standalone) to ensure enrolled devices continue to be managed and protected after the change. Note the following considerations:
- Devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) replace the existing settings on the device.
- After you change the MDM authority, some of the basic settings (such as profiles) from the previous MDM authority (hybrid) remain on the device for up to seven days. It is recommended that you configure apps and settings (policies, profiles, apps, etc.) in the new MDM authority as soon as possible. Also, deploy the settings to the user groups that contain users who have existing enrolled devices. When a device connects to the service after the change in MDM authority, it receives new settings from the new MDM authority. Any newly targeted policies override existing policies on the device.
- After you change to the new MDM authority, the compliance data in the [Azure portal](https://portal.azure.com) can take up to a week to accurately report. However, the compliance states in Azure Active Directory and on the device will be accurate so the device will still be protected.
- Devices that don't have associated users (typically when you have iOS Device Enrollment Program or bulk enrollment scenarios) are not migrated to the new MDM authority. For those devices, you need to call support for assistance to move them to the new MDM authority.

## Prepare to change the MDM authority to Intune standalone
Review the following information to prepare for the change to the MDM authority:
- You must have Configuration Manager version 1610 or higher for the option to change the MDM authority to be available.
- It can take up to eight hours for a device to connect to the service after you change to the new MDM authority.
- Make sure all users that are currently managed by hybrid have an Intune/EMS license assigned to them prior to the change in MDM authority. Having the license ensures that the user and their devices are managed by Intune standalone after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Make sure that the Admin user account has an Intune/EMS license assigned and confirm that the Admin user account can sign in to Intune before the change to the MDM authority. The MDM authority should display **Set to Configuration Manager** (hybrid tenant) in Intune in the [Azure portal](https://portal.azure.com) prior to the change in MDM authority.
- In the Configuration Manager console, remove all Device Enrollment Manager roles. Go to **Administration** > **Cloud Services** > **Microsoft Intune Subscriptions**, select the Microsoft Intune subscription, click **Properties**, click the **Device Enrollment Manager** tab, and remove all Device Enrollment Manager roles.
- In the Configuration Manager console, remove existing device categories. Go to **Assets and Compliance** > **Overview** > **Device Collections**, choose **Manage Device Categories**, and remove existing device categories.
- There should be no noticeable impact to end users during the change in MDM authority. 

## Change the MDM authority to Intune standalone
The process to change the MDM authority to Intune standalone includes the following high-level steps:  
- In the Configuration Manager console, use the **Change MDM Authority to Microsoft Intune** option to remove the existing Microsoft Intune subscription.
- In Intune in the [Azure portal](https://portal.azure.com), set the new MDM authority to **Intune**.
- Configure the Apple APNs certificate by using the same APNs certificate that you renewed.
- In Intune in the [Azure portal](https://portal.azure.com), configure and deploy new settings and apps from the new MDM authority (Intune).
- The next time devices connect to the service, it will synchronize and receive the new settings from the new MDM authority.

#### To change the MDM authority to Intune standalone
1. In the Configuration Manager console, go to **Administration** &gt; **Overview** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and delete your existing Intune Subscription.
2. Select **Change MDM Authority to Microsoft Intune**, and then click **Next**.
   ![Download the APNs certificate request](./media/mdm-change-delete-subscription.png)
3. Sign in to the Intune tenant that you originally used when you set the MDM authority in Configuration Manager.
4. Click **Next** and complete the wizard.
5. The MDM authority is now set to **Microsoft Intune**. The Intune Subscription should no longer be displayed in the Microsoft Intune Subscriptions node of the Configuration Manager console. 
6. To verify that the MDM authority is set, take the following steps:
    a. Sign in to the [Azure portal](https://portal.azure.com) using the same Intune tenant that you used earlier. 
    b. Choose **More Services** > **Monitoring + Management** > **Intune** > **Device enrollment**. The MDM authority is displayed in the top-right section of the **Overview** blade. 

## Next steps
After the change in MDM authority is complete, review the following steps:
- When the Intune service detects that a tenant’s MDM authority has changed, it sends out a notification message to all the enrolled devices to check in and synchronize with the service (this is outside of the regularly scheduled check-in). Therefore, after the MDM authority for the tenant has been changed from hybrid to Intune standalone, all the devices that are powered on and online will connect with the service, receive the new MDM authority, and be managed by Intune standalone going forward. There will be no interruption to the management and protection of these devices.
- Devices that are either powered off or offline during (or shortly after) the change in MDM authority connect to and synchronize with the service under the new MDM authority when they are powered on and online.  
- Users can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Users can easily do this by using the Company Portal app and initiating a device compliance check.
- To validate that things are working correctly after devices have checked-in and synchronized with the service after the change in MDM authority, look for the devices in the [Azure portal](https://portal.azure.com). The devices that were previously managed by Configuration Manager (hybrid) will now be displayed as managed devices in Intune.    
- There is an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following remains on the device for up to seven days (or until the device connects with the new MDM authority and receives new settings that overwrite the existing ones):
    - E-mail profile
    - VPN profile
    - Cert profile
    - Wi-Fi profile
    - Configuration profiles
- Make sure the new settings that are intended to overwrite existing settings have the same name as the previous ones to ensure that the old settings are overwritten. Otherwise, the devices might end up with redundant profiles and policies.    

  > [!TIP]   
  > As a best practice, you should create all management settings and configurations, as well as deployments, shortly after the change to the MDM authority has completed. This helps to ensure that devices are protected and actively managed during the interim period.   
-  After you change the MDM authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:   
    - Enroll a new device
    - Make sure the newly enrolled device shows up in the [Azure portal](https://portal.azure.com).
    - Perform an action, such as Remote Lock, from the [Azure portal](https://portal.azure.com) to the device. If it is successful, the device is being managed by the new MDM authority.
- If you have issues with specific devices, you can unenroll and reenroll the devices to get them connected to the new authority and managed as quickly as possible.