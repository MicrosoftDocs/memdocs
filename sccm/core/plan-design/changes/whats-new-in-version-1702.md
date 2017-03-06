---
title: "New version 1702 | Microsoft Docs"
description: "Get details about changes and new capabilities introduced in version 1702 of System Center Configuration Manager."
ms.custom: na
ms.date:  03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: "NOINDEX, NOFOLLOW"
---
# What&#39;s new in version 1702 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1702 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1606 or 1610. It is also available as a baseline version you can use when installing a new deployment.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1702 of Configuration Manager.  


## Data Warehouse service point
Use the Data Warehouse service point to store and report on long-term historical data for your Configuration Manager deployment.

The data warehouse supports up to 2 TB of data, with timestamps for change tracking. Storage of data is accomplished by automated synchronizations from the Configuration Manager site database to the data warehouse database. This information is then accessible from your Reporting Services point.

For more information, see [The Data Warehouse service point](/sccm/core/servers/manage/data-warehouse).




## Content library cleanup tool
Use the [content library cleanup tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) to remove content from distribution points when that content is no longer associated with an application.




## Improvements for in-console search
The following are improvements to using search in the Configuration Manager console:
 - **Object Path:**  
  Many objects now support a column named **Object Path**.  When you search and include this column in your display results, you can view the path to each object. For example, if you run a search for apps in the Applications node and are also searching sub-nodes, the *Object Path* column in the results pane will show you the path to each object that is returned.   

- **Preservation of search text:**  
  When you enter text into the search text box, and then switch between searching a sub-node and the current node, the text that you typed will now persist and remain available for a new search without having to reenter it.

- **Preservation of your decision to search sub-nodes:**  
 The option that you choose for searching the *current node* or *all sub-nodes* now persists when you change the node you are working in. This new behavior means that you do not need to constantly reset this decision as you move around the console. By default, when you open the console the option is to search only the current node.
