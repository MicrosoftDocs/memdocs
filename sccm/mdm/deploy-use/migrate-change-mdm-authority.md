---
title: Change your MDM authority to Intune
titleSuffix: "Configuration Manager"
description: "Learn how to change the MDM authority from Configuration Manager (hybrid) to Intune standalone."
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
---

# Change your MDM authority to Intune standalone

*Applies to: System Center Configuration Manager (Current Branch)*    

You can change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid MDM) to Intune standalone. Changing the tenant-level MDM authority to Intune is the final phase in the process to [migrate hybrid MDM users and devices to Intune standalone](migrate-hybridmdm-to-intunesa.md) in the cloud-only configuration.    

> [!Important]    
> To change your MDM authority without first migrating hybrid MDM users to Intune, see [Change your MDM authority](change-mdm-authority.md).

This article provides information about how to change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid) to Intune standalone and assumes that you have already completed the following steps:
- Used the [Intune Data Import tool](migrate-import-data.md) to import Configuration Manager objects to Intune. 
- [Prepared Intune for user migration](migrate-prepare-intune.md) to ensure users and their devices continue to be managed after they are migrated.
- [Changed the MDM authority for specific users (mixed MDM authority)](migrate-mixed-authority.md) to start managing user devices from the Azure portal.


## Users and devices that have not been migrated
You have already migrated many users and tested Intune functionality to make sure things are working as expected. Therefore, your policies, profiles, apps, etc. have been configured in Intune and you have thoroughly tested the objects on devices. There should be no new configurations required for your tenant-level policies after the change in MDM authority. However, for users and devices that have not been previously migrated, review the following information about what to expect after the change in MDM authority:    
- There is likely a transition time (up to eight hours) before the device checks in and synchronizes with the service.
- Your devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) replace the existing settings on the device.
- Some of the basic settings (such as profiles) from the previous MDM authority (hybrid) remain on the device for up to seven days. 
- Devices that don't have associated users (typically when you have iOS Device Enrollment Program or bulk enrollment scenarios) are not migrated to the new MDM authority. For those devices, you need to call support for assistance to move them to the new MDM authority.

## Prerequisites
Review the following information to prepare for the change to the MDM authority:
- You must have Configuration Manager version 1610 or higher for the option to change the MDM authority to be available.
- Make sure all users that are currently managed by hybrid MDM have an Intune/EMS license assigned to them prior to the change in MDM authority. Having the license ensures that the user and their devices are managed by Intune standalone after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Make sure that the Admin user account has an Intune/EMS license assigned.

## Change the MDM authority to Intune
Use the following procedure to change the tenant-level MDM authority to Intune.

1.	In the Configuration Manager console, go to **Administration** &gt; **Overview** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and delete your existing Intune Subscription.
2.	Select **Change MDM Authority to Microsoft Intune**, and then click **Next**.

    ![Remove Microsoft Intune subscription dialog](media/mdm-change-delete-subscription.png)
3.	Sign in to the Intune tenant that you originally used when you set the MDM authority in Configuration Manager.
4.	Click **Next** and complete the wizard.
5.	The MDM authority is now reset. The Intune Subscription is no longer displayed in the Microsoft Intune Subscriptions node of the Configuration Manager console.
6.	Log in to the [Intune in the Azure portal](https://portal.azure.com/#@AzureO365Intune.onmicrosoft.com/blade/Microsoft_Intune_Enrollment/OverviewBlade/overview) using the same Intune tenant you used earlier.    

  > [!Important]    
  > Do not use the Intune classic console. You must log in to Intune in the Azure portal.
7.	Confirm that the MDM authority has been changed to **Microsoft Intune**. 

## Next steps
After the change in MDM authority is complete, review the following information:
- There should be no noticeable impact to end users during the change in MDM authority. 
- You do not have to reconfigure tenant-level policies. 
- You can edit tenant-level policies from Intune in the Azure portal after the change in MDM authority.
-  After you change the MDM authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:   
    - Enroll a new device
    - Make sure the newly enrolled device shows up in Intune.
    - Perform an action, such as Remote Lock, from the administration console to the device. If it is successful, the device is being managed by the new MDM authority.
- If you have issues with specific devices, you can unenroll and reenroll the devices to get them connected to the new authority and managed as quickly as possible.
- For users and devices that have not been previously migrated:
    - Verify that devices are now displayed in the **Devices** blade as managed devices. These devices must check in and synchronize with the service after the change in MDM authority before they are displayed. 
    - When the Intune service detects that a tenant’s MDM authority has changed, it sends out a notification message to all the enrolled devices to check in and synchronize with the service (outside of the regularly scheduled check-in). Therefore, after the MDM authority for the tenant has been changed from hybrid to Intune standalone, all the devices that are powered on and online connect with the service, receive the new MDM authority, and be managed by Intune standalone from now on. There is no interruption to the management and protection of these devices.
    - Devices that are either powered off or offline during (or shortly after) the change in MDM authority connect to and synchronize with the service under the new MDM authority when they are powered on and online.  
    - Users can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Users can easily do check in by using the Company Portal app and initiating a device compliance check.
    - There is an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following profiles remain on the device for up to seven days (or until the device connects with the new MDM authority and receives new settings that overwrite the existing ones):
        - E-mail profile
        - VPN profile
        - Cert profile
        - Wi-Fi profile
        - Configuration profiles
    - Call support to help change the MDM authority for devices that are not associated with a user. 
