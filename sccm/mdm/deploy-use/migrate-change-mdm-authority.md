---
title: Change your MDM authority to Intune
titleSuffix: Configuration Manager
description: Learn how to change the MDM authority from Configuration Manager (hybrid) to Intune standalone.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
---

# Change your MDM authority to Intune standalone

*Applies to: System Center Configuration Manager (Current Branch)*    

You can change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid MDM) to Intune standalone. Changing the tenant-level MDM authority to Intune is the final phase in the process to [migrate hybrid MDM users and devices to Intune standalone](migrate-hybridmdm-to-intunesa.md) in the cloud-only configuration.    

> [!Important]    
> To change your MDM authority without first migrating hybrid MDM users to Intune, see [Change your MDM authority](change-mdm-authority.md).

This article provides information about how to change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid) to Intune standalone. It assumes you've already completed the following steps:
- Used the [Intune Data Import tool](migrate-import-data.md) to import Configuration Manager objects to Intune. 
- [Prepared Intune for user migration](migrate-prepare-intune.md) to make sure users and their devices continue to be managed after they're migrated.
- [Changed the MDM authority for specific users (mixed MDM authority)](migrate-mixed-authority.md) to start managing user devices from the Azure portal.


## Users and devices that haven't been migrated
You've already migrated many users and tested Intune functionality to make sure things are working as expected. You've configured policies, profiles, and apps in Intune, and you've thoroughly tested the objects on devices. There should be no new configurations required for your tenant-level policies after the change in MDM authority. However, for users and devices that you haven't previously migrated, review the following information about what to expect after the change in MDM authority:    

- There's likely a transition time of up to eight hours before the device checks in and synchronizes with the service.  

- Your devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) replace the existing settings on the device.  

- Some of the basic settings (such as profiles) from the previous MDM authority (hybrid) remain on the device for up to seven days.  

- Devices that don't have associated users aren't migrated to the new MDM authority. These devices are typically with scenarios for iOS Device Enrollment Program or bulk enrollment. For those devices, you need to call support for assistance to move them to the new MDM authority.



## Prerequisites
Review the following information to prepare for the change to the MDM authority:
- You must have Configuration Manager version 1610 or higher for the option to change the MDM authority to be available.
- Make sure to assign an Intune/EMS license to all users currently managed by hybrid MDM. The license makes sure that the user and their devices are managed by Intune standalone after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Make sure that the Admin user account has an Intune/EMS license assigned.

## Change the MDM authority to Intune
Use the following procedure to change the tenant-level MDM authority to Intune.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Intune Subscription** node. Delete your existing Intune Subscription.  

2. Select **Change MDM Authority to Microsoft Intune**, and then select **Next**.

    ![Remove Microsoft Intune subscription dialog](media/mdm-change-delete-subscription.png)  

3. Sign in to the Intune tenant that you originally used when you set the MDM authority in Configuration Manager. Select **Next** and complete the wizard.

    The MDM authority is now reset. The Intune Subscription is no longer displayed in the Microsoft Intune Subscriptions node of the Configuration Manager console.  

4. Sign in to the [Intune portal](https://aka.ms/IntunePortal).

5. Select **Device enrollment**.  

6. In the Device enrollment Overview, see the **MDM authority** property.

   > [!Important]    
   > Don't use the Intune classic console. Sign in to Intune in the Azure portal.  

7. Confirm that the MDM authority has been changed to **Microsoft Intune**. 



## Next steps

After the change in MDM authority is complete, review the following information:

- There should be no noticeable impact to end users during the change in MDM authority.  

- You don't have to reconfigure tenant-level policies.  

- If you need to edit tenant-level policies, do this action from Intune in the Azure portal.  

- If you have issues with specific devices, unenroll and reenroll the devices. This action gets them connected to the new authority and managed as quickly as possible.


#### Validate new device enrollment
After you change the MDM authority, use the following steps to validate that new devices are enrolled successfully to the new authority:   
1. Enroll a new device
2. Make sure the newly enrolled device shows up in Intune
3. Start a device action from the Intune portal, such as [remote lock](https://docs.microsoft.com/intune/device-remote-lock). If it's successful, the device is successfully managed by the new MDM authority.


#### For users and devices that you haven't previously migrated

- Verify that devices are now displayed in the **Devices** page as managed devices. Before they're displayed, these devices must check in and synchronize with the service after the change in MDM authority. 

- When the Intune service detects that a tenant's MDM authority has changed, it sends out a notification message to all enrolled devices. It instructs devices to check in and synchronize with the service. This notification happens outside of the regularly scheduled check-in. After you change the MDM authority for the tenant from hybrid to Intune standalone, all online devices connect with the service. They receive the new MDM authority, and then are managed by Intune standalone from now on. There's no interruption to the management and protection of these devices.

- For devices that are offline during or shortly after the change in MDM authority, they connect to and synchronize with the service under the new MDM authority when they're powered on and online.  

- You can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Use the Company Portal app to start a device compliance check.

- There's an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To make sure that the device remains protected and functional during this interim period, the following profiles remain on the device for up to seven days. They can also remain until the device connects with the new MDM authority and receives new settings that overwrite the existing ones:
    - E-mail profile
    - VPN profile
    - Cert profile
    - Wi-Fi profile
    - Configuration profiles

- For devices that aren't associated with a user, call support to help change the MDM authority. 

#### <a name="bkmk-ki-dep"></a> Apple DEP device records
<!--ICM 105091970-->
After you complete the migration from hybrid MDM, you may notice Apple DEP device records remain in the Configuration Manager console. Once you change the MDM authority to Intune, you can't remove these devices from Configuration Manager. 

There are two workarounds:

- If you see this behavior before you change the MDM authority, then delete the DEP records from Configuration Manager.  

- If you've already migrated, and are still using Configuration Manager, then use the following SQL command on the site database to remove the records:  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```
