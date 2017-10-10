---
title: "Configuring power management"
titleSuffix: "Configuration Manager"
description: "Set up power management in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98ms.author: angrobemanager: angrobe

---
# Configuring power management in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Before you can use power management in System Center Configuration Manager, you must perform the following configuration steps.  

## Enable and configure power management client settings  
 This procedure configures the default client settings for power management and will apply to all the computers in your hierarchy. If you want these settings to apply to only some computers, create a custom device client setting and assign it to a collection that contains the computers that you want to use power management. For more information about how to create custom device settings, see [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### To enable power management and configure client settings  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Client Settings** dialog box, click **Power Management**.  

6.  Configure the following value for the power management client settings:  

    -   **Allow power management of devices** – From the drop-down list, select **True** to enable power management.  

7.  Configure the client settings that you require. For a list of power management client settings that you can configure, see the [Power Management](../../../../core/clients/deploy/about-client-settings.md#power-management) section in the [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) topic.  

8.  Click **OK** to close the **Default Client Settings** dialog box.  

 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## Exclude computers from power management  
 You can prevent collections of computers from receiving power management settings. If a computer is a member of any collection that is excluded from power management settings, that computer does not apply power management settings, even if it is a member of another collection that applies power management settings.  

 You might want to exclude computers from power management for any of the following reasons:  

-   You have a business requirement for computers to be turned on at all times.  

-   You have created a control collection of computers on which you do not want to apply power management settings.  

-   Some of your computers are incapable of applying power management settings.  

-   You want to exclude computers that run Windows Server from power management.  

> [!NOTE]  
>  If the option **Allow users to exclude their device from power management** is configured in client settings, users can exclude their own computers from power management by using Software Center.  

 To find out which computers have been excluded from power management, run the report **Computers Excluded**. For more information about this report see [Computers Excluded](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) in [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Power settings that are applied to computers that run Windows XP or Windows Server 2003 are not reverted to their original values, even if you exclude the computer from power management. On later versions of Windows, excluding a computer from power management causes all power settings to be reverted to their original values. You cannot revert individual power settings to their original values.  

#### To exclude a collection of computers from power management  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**.  

3.  In the **Device Collections** list, select the collection that you want to exclude from power management and then, in the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the **Power Management** tab of the *<Collection Name\>***Properties** dialog box, select **Never apply power management settings to computers in this collection**.  

5.  Click **OK** to close the *<Collection Name\>***Properties** dialog box and to save your settings.  
