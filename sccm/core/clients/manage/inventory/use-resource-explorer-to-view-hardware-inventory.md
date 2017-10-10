---
title: "View hardware inventory with Resource Explorer"
description: "Use Resource Explorer to view hardware inventory in System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: andredm7
ms.author: andredm
manager: angrobe

---
# How to use Resource Explorer to view hardware inventory in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use Resource Explorer in System Center Configuration Manager to view information about hardware inventory that has been collected from clients in your hierarchy.  

> [!NOTE]  
>  Resource Explorer will not display any inventory data until a hardware inventory cycle has run on the client you are connecting to.  

 Resource Explorer has the following sections related to hardware inventory:  

-   **Hardware** - Contains the most recent hardware inventory collected from the specified client device.  **Workstation Status** has the time and date when the device last performed a hardware inventory.  

-   **Hardware History** - Contains a history of inventoried items that have changed since the last hardware inventory took place. Each item contains a **Current** node and one or more *<date\>* nodes. You can compare the information in the current node to one of the historical nodes to discover items that have changed .  

    > [!NOTE]  
    >  Configuration Manager retains hardware inventory history for the number of days you specify in the **Delete Aged Inventory History** site maintenance task  

> [!NOTE]  
>  For information about how to view hardware inventory from clients that run Linux and UNIX, see [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### How to run Resource Explorer from the Configuration Manager console  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Devices**, or open any collection that displays devices.  

3.  Choose the computer containing the inventory that you want to view and then, on the **Home** tab > **Devices** group, choose **Start** >  **Resource Explorer**.   

4.  Right-click any item in the right-pane of the **Resource Explorer** window and choose **Properties** to open the *<item name\>***Properties** dialog box to view the collected inventory information in a more readable format.  

