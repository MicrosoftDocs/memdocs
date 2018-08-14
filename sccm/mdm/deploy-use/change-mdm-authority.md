---
title: Change your MDM authority
titleSuffix: Configuration Manager
description: Learn how to change the MDM authority from Configuration Manager (hybrid) to Intune standalone
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
---

# Change your MDM authority

*Applies to: System Center Configuration Manager (Current Branch)*

You can change your MDM authority without having to contact Microsoft Support and without having to unenroll and reenroll your existing managed devices. This article provides the steps to change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid) to Intune standalone. When you complete the steps in this article, devices are managed by Microsoft Intune in the [Azure portal](https://portal.azure.com). 

This article is to change your MDM authority when you've not previously migrated users. To change your MDM authority after you've [migrated a subset of users](migrate-hybridmdm-to-intunesa.md), see [Change your MDM authority](migrate-change-mdm-authority.md).

> [!Important]  
> As of August 13, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## Key Considerations

After you change the MDM authority, expect a transition time of up to eight hours. It can take this long before the device checks in and synchronizes with the service. To ensure enrolled devices continue to be managed and protected after the change, configure settings directly in Intune. Note the following considerations:

- Devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) replace the existing settings on the device.  

- After you change the MDM authority, some of the basic settings (such as profiles) from the previous MDM authority (hybrid) remain on the device for up to seven days. It is recommended that you configure apps and settings (policies, profiles, apps, etc.) in the new MDM authority as soon as possible. Also, deploy the settings to the user groups that contain users who have existing enrolled devices. When a device connects to the service after the change in MDM authority, it receives new settings from the new MDM authority. Any newly targeted policies override existing policies on the device.  

- After you change to the new MDM authority, the compliance data in the [Azure portal](https://portal.azure.com) can take up to a week to accurately report. However, the compliance states in Azure Active Directory and on the device are accurate. The device is still protected.  

- Devices that don't have associated users aren't migrated to the new MDM authority. This behavior is typically when you have iOS Device Enrollment Program or bulk enrollment scenarios. For those devices, call support for assistance to move them to the new MDM authority.  



## Prepare to change the MDM authority to Intune standalone

Review the following information to prepare for the change to the MDM authority:

- It can take up to eight hours for a device to connect to the service after you change to the new MDM authority.  

- Make sure all users that are currently managed by hybrid have an Intune/EMS license assigned to them prior to the change in MDM authority. This license ensures that the user and their devices are managed by Intune standalone after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).  

- Make sure that the Admin user account has an Intune/EMS license assigned. Confirm that the Admin user account can sign in to Intune before the change to the MDM authority. The MDM authority should display **Set to Configuration Manager** (hybrid tenant) in Intune in the [Azure portal](https://portal.azure.com) prior to the change in MDM authority.  

- There should be no noticeable impact to end users during the change in MDM authority. 



## Change the MDM authority to Intune standalone

The process to change the MDM authority to Intune standalone includes the following high-level steps:  

- In the Configuration Manager console, use the **Change MDM Authority to Microsoft Intune** option to remove the existing Microsoft Intune subscription.  

- In Intune in the [Azure portal](https://portal.azure.com), configure and deploy new settings and apps from the new MDM authority (Intune).  

- The next time devices connect to the service, it will synchronize and receive the new settings from the new MDM authority.  

#### To change the MDM authority to Intune standalone
1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Microsoft Intune Subscription** node. Delete your existing Intune Subscription.  

2. Select **Change MDM Authority to Microsoft Intune**, and then click **Next**.  

   ![Remove Microsoft Intune Subscription Wizard, Introduction page](./media/mdm-change-delete-subscription.png)

3. Sign in to the Intune tenant that you originally used when you set the MDM authority in Configuration Manager.  

4. Click **Next** and complete the wizard.  

5. The MDM authority is now set to **Microsoft Intune**. The Intune Subscription doesn't display in the Microsoft Intune Subscriptions node of the Configuration Manager console.  

6. To verify that the MDM authority is set, take the following steps:  

    1. Sign in to the [Azure portal](https://portal.azure.com) using the same Intune tenant that you used earlier.  

    2. Choose **All Services** > **Intune** > **Device enrollment**. The MDM authority is displayed in the top-right section of **Overview**.  



## Next steps

After the change in MDM authority is complete, review the following steps:  

- When the Intune service detects that a tenant’s MDM authority has changed, it sends out a notification message to all the enrolled devices to check in and synchronize with the service. This behavior is outside of the regularly scheduled check-in. Therefore, after you change the MDM authority for the tenant from hybrid to Intune standalone, all the devices that are powered on and online connect with the service, receive the new MDM authority, and are managed by Intune standalone. There is no interruption to the management and protection of these devices.  

- Devices that are either powered off or offline during (or shortly after) the change in MDM authority connect to and synchronize with the service under the new MDM authority when they are powered on and online.   

- Users can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Users can easily do this action by using the Company Portal app and initiating a device compliance check.  

- To validate that things are working correctly after devices have checked-in and synchronized with the service after the change in MDM authority, look for the devices in the [Azure portal](https://portal.azure.com). The devices that were previously managed by Configuration Manager (hybrid) now display as managed devices in Intune.    

- There is an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following profiles remain on the device for up to seven days (or until the device connects with the new MDM authority and receives new settings that overwrite the existing ones):  
    - E-mail profile
    - VPN profile
    - Cert profile
    - Wi-Fi profile
    - Configuration profiles  

- To overwrite the old settings, make sure the new settings that are intended to overwrite existing settings have the same name as the previous ones. Otherwise, the devices might end up with redundant profiles and policies.    

  > [!TIP]   
  > Create all management settings and configurations, as well as deployments, shortly after the change to the MDM authority has completed. This action helps to protect and actively manage devices during the interim period.   

-  After you change the MDM authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:   

    - Enroll a new device  

    - Make sure the newly enrolled device shows up in the [Azure portal](https://portal.azure.com).  

    - Perform an action, such as Remote Lock, from the [Azure portal](https://portal.azure.com) to the device. If it's successful, the device is being managed by the new MDM authority.  
    
- If you have issues with specific devices, unenroll and reenroll the devices. This action connects to the new authority and managed as quickly as possible.  

- If you've enabled [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) as a hybrid tenant and then migrate your tenant to Intune standalone, the Android for Work setting under enrollment restrictions may show as blocked instead of allow. Manually set it to **Allow** to re-enable Android for Work enrollment.<!--512117-->  

- After changing MDM authority, the Apple VPP token and associated [volume-purchased iOS apps](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps) aren't automatically removed. To cleanup this information, follow the steps in [Delete an Apple VPP token](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps#delete-an-apple-vpp-token). Once the operation completes, the site removes the token. It also removes from the Licensed Store App node any application metadata for that token.<!--SCCMDocs issue 579-->  

    In rare occurrences, you may see an error that the site couldn't delete management object.  

    - If the token isn't visible, ignore the error  

    - If the token is still listed, retry to delete it  

