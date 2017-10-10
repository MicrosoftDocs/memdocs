---
title: "Configure software inventory"
description: "Configure software inventory, and exclude folders from software inventory in Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
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
author: andredm7ms.author: andredmmanager: angrobe

---
# How to configure software inventory in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
 This procedure configures the default client settings for software inventory and will apply to all the computers in your hierarchy. If you want to apply these settings to only some computers, create a custom device client setting and assign it to a collection that contains the computers that you want to use software inventory. For more information about how to create custom device settings, see [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

## To configure software inventory  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings**  **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  In the **Default Settings** dialog box, choose **Software Inventory**.  

6.  In the **Device Settings** list, configure the following values:  

    -   **Enable software inventory on clients** - From the drop-down list, select **True**.  

    -   **Schedule software inventory and file collection schedule** - Configures the interval at which clients collect software inventory and files.   

7.  Configure the client settings that you require. For a list of software inventory client settings that you can configure, see the [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#software-inventory) section in the [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) topic.  

 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  


## To exclude folders from software inventory  

1.  Using Notepad.exe, create an empty file named **Skpswi.dat**.  

2.  Right click the **Skpswi.dat** file and click **Properties**. In the file properties for the Skpswi.dat file, select the **Hidden** attribute.  

3.  Place the **Skpswi.dat** file at the root of each client hard drive or folder structure that you want to exclude from software inventory.  

> [!NOTE]  
>  Software inventory will not inventory the client drive again unless this file is deleted from the drive on the client computer.