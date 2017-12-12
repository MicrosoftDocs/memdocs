---
title: "Technical Preview 1712 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1712 for System Center Configuration Manager."
ms.custom: na
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: angrobe
---
# Capabilities in Technical Preview 1712 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1712. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->


**The following are new features you can try out with this version.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->
## Improvements to Office 365 Client Management dashboard 
The Office 365 Client Management dashboard now displays a list of relevant devices when graph sections are selected. In the console, go to **Software Library** >**Overview** >**Office 365 Client Management**. The dashboard will be displayed on the right. Selecting criteria from the chart will show a list of devices.  
<!--1357281-->
    
## Change to the Surface Device Dashboard
The Surface dashboard now displays firmware versions for Surface devices rather than operating system version. In the console, go to **Monitoring** > **Surface Devices**. You can view the following:
- percent of Surfaces
- percent of Surface models
- top five firmware versions
 <!--1355788-->

## Change in the Configuration Manager client install  
As a result of your user voice feedback, [Silverlight is no longer installed on clients automatically.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  
## Improvements to the Configuration Manager console 
We have made the following improvements to the Configuration Manager console, which were a result of your user voice feedback.

- [Device list displays primary user](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): Device lists under Assets and Compliance, Devices, now display the primary user by default. The last logged on user can also be added as an optional column. <!-- 1357280 -->
- [Renamed collections display in existing collection membership rules](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): When a collection is a member of another collection and it is renamed, the new name is updated under membership rules.<!--1357282--> 
 




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## Next Steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
