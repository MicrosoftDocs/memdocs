---
title: "How to use Resource Explorer to view software inventory in System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: barlanmsftmanager: angrobe

---
# How to use Resource Explorer to view software inventory in System Center Configuration Manager
Use Resource Explorer in System Center Configuration Manager to view information about software inventory that has been collected from computers in your hierarchy.  

> [!NOTE]  
>  Resource Explorer will not display any inventory data until a software inventory cycle has run on the client you are connecting to.  

 Resource Explorer in Configuration Manager contains the following sections related to software inventory:  

-   **Software** - The software section of Resource Explorer contains four sections:  

    -   **Collected Files** - Displays information about files that were collected during software inventory.  

    -   **File Details** - Displays information about files that were inventoried during software inventory that are not associated with a specific product or manufacturer.  

    -   **Last Software Scan** - Displays the date and time of the last software inventory and file collection that was run on the client computer.  

    -   **Product Details** - Displays information about the software products that were inventoried by software inventory, grouped by manufacturer.  

## To run Resource Explorer from the Configuration Manager console  
 Use the following procedure to run Resource Explorer in Configuration Manager.  

#### To run Resource Explorer from the Configuration Manager console  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Devices** or open any collection that displays devices.  

3.  Click the computer containing the inventory that you want to view and then, in the **Home** tab, in the **Devices** group, click **Start** and then click **Resource Explorer**. The **Resource Explorer** window will open.  

4.  You can right-click any item in the right-pane of the Resource Explorer window and then click **Properties** to open the *<item name\>***Properties** dialog box which can help you to view the collected inventory information in a more readable format.  

5.  When you are finished, close the **Resource Explorer** window.  

