---
title: "View software inventory | Resource Explorer"
description: "Use Resource Explorer to view software inventory in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
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
author: andredm7
ms.author: andredm
manager: angrobe

---
# How to use Resource Explorer to view software inventory in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use Resource Explorer in System Center Configuration Manager to view information about software inventory that has been collected from computers in your hierarchy.  

> [!NOTE]  
>  Resource Explorer will not display any inventory data until a software inventory cycle has run on the client.  

 Resource Explorer provides the following software inventory information:  

-   **Software**:  

    -   **Collected Files** - Files that were collected during software inventory.  

    -   **File Details** - Files that were inventoried during software inventory that are not associated with a specific product or manufacturer.  

    -   **Last Software Scan** - Date and time of the last software inventory and file collection for the client computer.  

    -   **Product Details** - Software products that were inventoried by software inventory, grouped by manufacturer.  

## To run Resource Explorer from the Configuration Manager console  

1.  In the Configuration Manager console, choose **Assets and Compliance**

2.  In the **Assets and Compliance** workspace, choose **Devices** or open any collection that displays devices.  

3.  Choose the computer containing the inventory that you want to view and then, in the **Home** tab > **Devices** group, choose **Start** > **Resource Explorer**.

4.  You can right-click any item in the right-pane of the Resource Explorer window and choose **Properties** to view the collected inventory information in a more readable format.  
 
