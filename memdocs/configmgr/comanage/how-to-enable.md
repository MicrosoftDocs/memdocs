---
title: Enable co-management
titleSuffix: Configuration Manager
description: Quickly enable co-management in Configuration Manager to gain immediate value.
ms.date: 08/02/2021
ms.subservice: co-management
ms.service: configuration-manager
ms.topic: how-to
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to enable co-management in Configuration Manager

When you enable co-management, you can gain immediate value. Then once you're ready, you can start transitioning workloads as needed and if desired in your environment.

The phrase **Pilot group** is used throughout the co-management feature and configuration dialogs. A *pilot group* is a collection containing a subset of your Configuration Manager devices. Use a *pilot group* for your initial testing, adding devices as needed, until you're ready to move the workloads for all Configuration Manager devices. There isn't a time limit on how long a *pilot group* can be used for workloads. A *pilot group* can be used indefinitely if you don't wish to move the workload to all Configuration Manager devices.

Make sure the co-management prerequisites are set up before you start this process. For more information, see [Prerequisites](overview.md#prerequisites).

> [!TIP]
> As a companion to this article, we recommend using the [co-management setup guide](https://go.microsoft.com/fwlink/?linkid=2224782) when signed in to the Microsoft 365 admin center. This guide will customize your experience based on your environment.

## Enable co-management (Cloud Attach)

Starting in Configuration Manager version 2111, the co-management onboarding experience changed. The Cloud Attach Configuration Wizard makes it easier to enable co-management and other cloud features. You can choose a streamlined set of recommended defaults, or customize your cloud attach features. There's also a new built-in device collection for **Co-management Eligible Devices** to help you identify clients. For more information on enabling co-management, see [Enable cloud attach](../../cloud-attach/enable.md).

> [!NOTE]
> With the new wizard, you don't move workloads at the same time that you enable co-management. To move workloads, you'll edit the co-management properties after enabling cloud attach.

When you're enabling co-management, you can use the Azure public cloud, Azure Government cloud, or Azure China 21Vianet cloud (added in version 2006). To enable co-management, follow these instructions:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Attach** node. Select **Configure Cloud Attach** on the ribbon to open the Cloud Attach Configuration Wizard.

2. On the onboarding page of the wizard, for **Azure environment**, choose one of the following environments:

   - Azure public cloud
   - Azure US Government cloud<!--4075452-->
   - Azure China cloud (added in version 2006)<!--7133238-->
     
     > [!NOTE]
     > Update the Configuration Manager client to the latest version on your devices before you onboard to the Azure China cloud. <!--7630213--> 

   When you select the Azure China cloud or Azure Government cloud, the **Upload to Microsoft Endpoint Manager admin center** option for [tenant attach](../../tenant-attach/device-sync-actions.md) is disabled.

3. Select **Sign In**. Sign in as a Microsoft Entra Global Administrator, and then select **Next**. You sign in this one time for the purposes of this wizard. The credentials aren't stored or reused elsewhere.

4. On the **Enablement** page, choose the following settings:

   - **Automatic enrollment in Intune**: Enables automatic client enrollment in Intune for existing Configuration Manager clients. This option allows you to enable co-management on a subset of clients to initially test co-management and then roll out co-management by using a phased approach. If the user unenrolls a device, the device will be re-enrolled on the next evaluation of the policy. <!--3330596-->

      - **Pilot**: Only the Configuration Manager clients that are members of the **Intune Auto Enrollment** collection are automatically enrolled in Intune.
      - **All**: Enable automatic enrollment for all clients running Windows 10 version 1709 or later.
      - **None**: Disable automatic enrollment for all clients.


   - **Intune Auto Enrollment**: This collection should contain all of the clients that you want to onboard into co-management. It's essentially a superset of all the other staging collections.

   ![Screenshot of the wizard page for enabling automatic enrollment in Intune.](../media/3555750-co-management-onboarding-enablement.png)
      
   Automatic enrollment isn't immediate for all clients. This behavior helps enrollment scale better for large environments. Configuration Manager randomizes enrollment based on the number of clients. For example, if your environment has 100,000 clients, when you enable this setting, enrollment occurs over several days.<!--1358003-->

   A new co-managed device is now automatically enrolled in the Microsoft Intune service based on its Microsoft Entra device token. It doesn't need to wait for a user to sign in to the device for automatic enrollment to start. This change helps to reduce the number of devices with the enrollment status **Pending user sign in**.<!-- 4454491 --> To support this behavior, the device needs to be running Windows 10 version 1803 or later. For more information, see [Co-management enrollment status](../how-to-monitor.md#co-management-enrollment-status).
   
   If you already have devices enrolled in co-management, new devices are now enrolled immediately after they meet the [prerequisites](../overview.md#prerequisites).<!--4321130-->

5. For internet-based devices that are already enrolled in Intune, copy and save the command on the **Enablement** page. You'll use this command to install the Configuration Manager client as an app in Intune for internet-based devices. If you don't save this command now, you can review the co-management configuration at any time to get this command.

    > [!TIP]
    > The command appears only if you've met all of the prerequisites, such as setting up a cloud management gateway.<!-- MEMDocs#635 -->

6. On the **Workloads** page, for each workload, choose which device group to move over for management with Intune. For more information, see [Workloads](../workloads.md). 

   If you only want to enable co-management, you don't need to switch workloads now. You can switch workloads later. For more information, see [How to switch workloads](../how-to-switch-workloads.md).  

    - **Pilot Intune**: Switches the associated workload only for the devices in the pilot collections that you'll specify on the **Staging** page. Each workload can have a different pilot collection.
    - **Intune**: Switches the associated workload for all co-managed Windows 10 or later devices.  

   > [!Important]
   > Before you switch any workloads, make sure that you properly configure and deploy the corresponding workload in Intune. Make sure that workloads are always managed by one of the management tools for your devices.  

7. On the **Staging** page, specify the pilot collection for each of the workloads that are set to **Pilot Intune**.

   ![Screenshot of the Staging page of the Co-management Configuration Wizard, with options for specifying pilot collections.](../media/3555750-co-management-onboarding-staging.png)

8. To enable co-management, complete the wizard.


## Next steps

Now that you've enabled co-management, look at the following articles for immediate value you can gain in your environment:

- [Conditional Access](quickstart-conditional-access.md)  

- [Remote actions from Intune](quickstart-remote-actions.md)  

- [Client health](quickstart-client-health.md)  
