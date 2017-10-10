---
title: "Configure hardware inventory"
titleSuffix: "Configuration Manager"
description: "Set up hardware inventory for all clients or for a collection in System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7ms.author: andredmmanager: angrobe

---
# How to configure hardware inventory in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
This procedure configures the default client settings for hardware inventory and will apply to all the clients in your hierarchy. If you want these settings to apply to only some clients, create a custom device client setting and assign it to a collection that contains the devices that you want to use hardware inventory. See [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  If a client device receives hardware inventory settings from multiple sets of client settings, then the hardware inventory classes from each set of settings will be merged when the client reports hardware inventory.  

### To configure hardware inventory  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Default Settings** dialog box, choose **Hardware Inventory**.  

6.  In the **Device Settings** list, configure the following:  

    -   **Enable hardware inventory on clients** - Select **True**.  

    -   **Hardware inventory schedule** - Click **Schedule** to specify the interval at which clients collect hardware inventory.  

7.  Configure other [hardware inventory client settings](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) that you require.  

Client devices will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
