---
title: Configure software inventory
titleSuffix: Configuration Manager
description: Configure software inventory, and exclude folders from software inventory in Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to configure software inventory in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This procedure configures the default client settings for software inventory and applies to all the computers in your hierarchy. If you want to apply these settings to only some computers, create a custom device client setting and assign it to a collection. For more information about how to create custom device settings, see [How to configure client settings](../../../../core/clients/deploy/configure-client-settings.md).   

## To configure software inventory  

1. In the Configuration Manager console, choose **Administration** > **Client Settings**  **Default Client Settings**.  

2. On the **Home** tab, in the **Properties** group, choose **Properties**.  

3. In the **Default Settings** dialog box, choose **Software Inventory**.  

4. In the **Device Settings** list, configure the following values:  

   -   **Enable software inventory on clients** - From the drop-down list, select **True**.  

   -   **Schedule software inventory and file collection schedule** - Configures the interval at which clients collect software inventory and files.   

5. Configure the client settings that you require. The [Software inventory](../../../../core/clients/deploy/about-client-settings.md#software-inventory) section of the [About client settings](../../../../core/clients/deploy/about-client-settings.md) article has a list of the client settings.  

   Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Error code 80041006 in inventoryprovider.log means the WMI provider is out of memory. That is, the memory quota limit for a provider has been hit and inventory provider cannot continue.
   > In this case, the inventory agent creates a report with 0 entries so no inventory items are reported. <br/>
   > A possible solution for this error would be to reduce the scope of the software inventory collection. In circumstances when the error occurs after limiting the inventory scope, increasing the [MemoryPerHost](https://techcommunity.microsoft.com/t5/ask-the-performance-team/memory-and-handle-quotas-in-the-wmi-provider-service/ba-p/373319) property defined in the [_ProviderHostQuotaConfiguration](/windows/win32/wmisdk/--providerhostquotaconfiguration) class can provide a solution.

<!--SMS.480648 include WMI Out of memory tip -->


## To exclude folders from software inventory  

1.  Using Notepad.exe, create an empty file named **Skpswi.dat**.  

2.  Right-click the **Skpswi.dat** file and click **Properties**. In the file properties for the Skpswi.dat file, select the **Hidden** attribute.  

3.  Place the **Skpswi.dat** file at the root of each client hard drive or folder structure that you want to exclude from software inventory.  

> [!NOTE]  
>  Software inventory will not inventory the client drive again unless this file is deleted from the drive on the client computer.