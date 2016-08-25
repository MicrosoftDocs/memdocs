---
title: "How to use Resource Explorer to view hardware inventory in System Center Configuration Manager"
ms.custom: na
ms.date: 2016-04-15
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
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
# How to use Resource Explorer to view hardware inventory in System Center Configuration Manager
Use Resource Explorer in System Center Configuration Manager to view information about hardware inventory that has been collected from clients in your hierarchy.  
  
> [!NOTE]  
>  Resource Explorer will not display any inventory data until a hardware inventory cycle has run on the client you are connecting to.  
  
 Resource Explorer in Configuration Manager contains the following sections related to hardware inventory:  
  
-   **Hardware** - Contains the most recent hardware inventory collected from the specified Configuration Manager client device. You can review the inventory item **Workstation Status** to discover the time and date when the device last performed a hardware inventory.  
  
-   **Hardware History** – Contains a history of inventoried items that have changed since the last hardware inventory was performed. Each item in the list contains a **Current** node and one or more *<date\>* nodes. You can compare the information in the current node to one of the historical nodes to discover items that have changed in the client computers hardware inventory.  
  
    > [!NOTE]  
    >  Configuration Manager retains hardware inventory history for the number of days you specify in the **Delete Aged Inventory History** site maintenance task  
  
> [!NOTE]  
>  For information about how to view hardware inventory from clients that run Linux and UNIX, see [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  
  
### How to run Resource Explorer from the Configuration Manager console  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, click **Devices** or open any collection that displays devices.  
  
3.  Click the computer containing the inventory that you want to view and then, in the **Home** tab, in the **Devices** group, click **Start** and then click **Resource Explorer**. The **Resource Explorer** window will open.  
  
4.  You can right-click any item in the right-pane of the **Resource Explorer** window and then click **Properties** to open the *<item name\>***Properties** dialog box which can help you to view the collected inventory information in a more readable format.  
  
5.  When you are finished, close the **Resource Explorer** window.  
  
## See Also  
 [Operations and maintenance for hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/operations-and-maintenance-for-hardware-inventory.md)