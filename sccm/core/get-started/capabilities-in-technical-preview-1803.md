---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1803.
ms.custom: na
ms.date: 03/27/2018 
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1803 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1803. You can install this version to update and add new capabilities to your technical preview site. 

Review the [Technical Preview](/sccm/core/get-started/technical-preview) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**The following are new features you can try out with this version.**  



 
## Pull-distribution points support cloud distribution points as source  
<!--1321554-->
Many customers use [pull-distribution points](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point) in remote or branch offices, which download content from a source distribution point across the WAN. If your remote offices have a better connection to the internet, or to reduce load on your WAN links, you can now use a [cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in Microsoft Azure as the source. When you add a source on the **Pull Distribution Point** tab of the distribution point properties, any cloud distribution point in the site is now listed as an available distribution point. The behavior of both site system roles remains the same otherwise. 

### Prerequisites
- The pull-distribution point needs internet access to communicate with Microsoft Azure.
- The content must be distributed to the source cloud distribution point.

> [!Note]  
> This feature does incur charges to your Azure subscription for data storage and network egress. For more information, see the [Cost of using cloud-based distribution](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_CloudDPCost).



## Partial download support in client peer cache to reduce WAN utilization
<!--1357346-->
Client peer cache sources can now divide content into parts. These parts minimize the network transfer to reduce WAN utilization.



## Maintenance windows in Software Center
<!--1358131-->
Software Center now displays the next scheduled maintenance window on the Installation Status tab.



## Custom tab for webpage in Software Center
<!--1358132-->
You can now create a customized tab to open a webpage in Software Center. This feature allows you to show content to your end users in a consistent, reliable way. The following list includes a few examples:
- Contact IT: information on how to contact your organization's IT department
- IT Support Center: IT self-service actions such as searching a knowledge base or opening a support ticket.
- End-user documentation: articles for users in your organization on various IT topics such as using applications or upgrading to Windows 10.


### Try it out!
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

1. In the Configuration Manager console, **Administration** workspace, **Client Settings** node, open the **Default Client Settings** policy.
2. Select the **Software Center** group.
3. For **Software Center settings**, click **Customize**.
4. Switch to the **Tabs** tab.
5. Enable the option to **Specify a custom tab for Software Center**.
	1. Enter a name in the **Tab name** text field. This name is what displays to the user in Software Center.
	2. Enter a valid URL in the **Content URL** text field. This URL is the content that Software Center displays when users click this tab.

> [!Tip]  
> Software Center uses Internet Explorer components for rendering the web page.


## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
