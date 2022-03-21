---
title: How to use Resource Explorer
titleSuffix: Configuration Manager
description: Use Resource Explorer to view hardware inventory in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# How to use Resource Explorer to view hardware inventory in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use Resource Explorer in Configuration Manager to view information about hardware inventory. The site collects this information from clients in your hierarchy.  

> [!Tip]  
>  Resource Explorer doesn't display any data until a hardware inventory cycle runs on the client to which you're connecting.  



## Overview

Resource Explorer has the following sections related to hardware inventory:  

- **Hardware**: Shows the most recent hardware inventory collected from the specified client device.  

    - The **Workstation Status** node shows the time and date of the last hardware inventory from the device.  

- **Hardware History**: A history of inventoried items that changed since the last hardware inventory cycle.  

    - Expand an item to see a **Current** node and one or more nodes with the historical date. Compare the information in the current node to one of the historical nodes to see the items that changed.  

> [!NOTE]  
> By default, Configuration Manager deletes hardware inventory data that's been inactive for 90 days. Adjust this number of days in the **Delete Aged Inventory History** site maintenance task. For more information, see [Maintenance tasks](../../../servers/manage/maintenance-tasks.md).  



## <a name="bkmk_open"></a> How to open Resource Explorer   

1.  In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Devices** node. You can also select any collection in the **Device Collections** node.  

2.  Select a device. In the ribbon, on the **Home** tab and **Devices** group, click **Start**, and then select **Resource Explorer**.   

> [!Tip]  
> In Resource Explorer, right-click an item in the right results pane for additional actions. Click **Properties** to view that item in a different format.  



## <a name="bkmk_bigint"></a> Use of large integer values
<!--1357880-->
In Configuration Manager versions 1802 and prior, hardware inventory has a limit for integers larger than 4,294,967,296 (2^32). This limit can be reached for attributes such as hard drive sizes in bytes. The management point doesn't process integer values above this limit, so no value is stored in the database. 

Starting in version 1806, the limit is increased to 18,446,744,073,709,551,616 (2^64). 

For a property with a value that doesn't change, like total disk size, you may not immediately see the value after upgrading the site. Most hardware inventory is a delta report. The client only sends values that change. To work around this behavior, add another property to the same class. This action causes the client to update all properties in the class that changed. 



## See also

Resource Explorer also shows Software Inventory. For more information, see [How to use Resource Explorer to view software inventory](use-resource-explorer-to-view-software-inventory.md).
