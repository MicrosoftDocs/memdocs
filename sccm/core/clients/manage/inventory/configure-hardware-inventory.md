---
title: "Configure hardware inventory | System Center Configuration Manager"
description: "Set up hardware inventory for all clients or for a collection in System Center Configuration Manager."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: barlanmsftmanager: angrobe

---
# How to configure hardware inventory in System Center Configuration Manager
Use the following steps to configure System Center Configuration Manager hardware inventory for your site.  

 This procedure configures the default client settings for hardware inventory and will apply to all the clients in your hierarchy. If you want these settings to apply to only some clients, create a custom device client setting and assign it to a collection that contains the devices that you want to use hardware inventory. For more information about how to create custom device settings, see [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  If a client device receives hardware inventory settings from multiple sets of client settings, then the hardware inventory classes from each set of settings will be merged when the client reports hardware inventory.  

### To configure hardware inventory  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Settings** dialog box, click **Hardware Inventory**.  

6.  In the **Device Settings** list, configure the following:  

    -   **Enable hardware inventory on clients** - From the drop-down list, select **True**.  

    -   **Hardware inventory schedule** - Specify the interval at which clients collect hardware inventory. Use the default value of **7 days** or click **Schedule** to configure a custom interval.  

7.  Configure any other client settings that you require. For a list of hardware inventory client settings that you can configure, see the [Hardware Inventory](../../../../core/clients/deploy/about-client-settings.md#BKMK_HardwareInventoryDeviceSettings) section in the [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) topic.  

8.  Click **OK** to close the **Default Settings** dialog box.  

 Client devices will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
