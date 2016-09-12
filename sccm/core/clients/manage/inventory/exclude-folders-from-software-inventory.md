---
title: "How to exclude folders from software inventory in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: barlanmsft
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to exclude folders from software inventory in System Center Configuration Manager
Use the following steps to configure System Center Configuration Manager software inventory for your site.  

 This procedure configures the default client settings for software inventory and will apply to all the computers in your hierarchy. If you want these settings to apply to only some computers, create a custom device client setting and assign it to a collection that contains the computers that you want to use software inventory. For more information about how to create custom device settings, see [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

### To configure software inventory  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  Click **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  In the **Default Settings** dialog box, click **Software Inventory**.  

6.  In the **Device Settings** list, configure the following values:  

    -   **Enable software inventory on clients** – From the drop-down list, select **True**.  

    -   **Schedule software inventory and file collection schedule** – Configures the interval at which clients collect software inventory and files. Use the default value of **7 days** or click **Schedule** to configure a custom interval.  

7.  Configure the client settings that you require. For a list of software inventory client settings that you can configure, see the [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#BKMK_SoftInventoryDeviceSettings) section in the [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) topic.  

8.  Click **OK** to close the **Configure Client Setting** dialog box.  

 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
