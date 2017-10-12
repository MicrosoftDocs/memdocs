---
title: "Manage queries"
titleSuffix: "Configuration Manager"
description: "Learn how to manage your queries. Includes a table for detailed reference."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
caps.latest.revision: 6
caps.handback.revision: 0
author: andredm7ms.author: andredmmanager: angrobe

---
# How to manage queries in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Use the information in this topic to help you manage queries in System Center Configuration Manager.  

 For information about how to create queries, see [How to create queries in System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## How to manage queries  
 In the **Monitoring** workspace, select **Queries**, select the query to manage, and then select a management task.  

 Use the following table for more information about the management tasks that might require some information before you select them.  

|Management task|Details|More information|  
|---------------------|-------------|----------------------|  
|**Run**|Runs the selected query and displays the results in the Configuration Manager console.|No additional information.|  
|**Install Client**|Opens the **Install Client Wizard** that lets you install the Configuration Manager client on computers returned by the selected query.<br /><br /> This option is not available for queries that return mobile devices, users, or user groups.|For more information about how to install Configuration Manager clients by using client push, see [Deploy clients to Windows computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Export**|Opens the **Export Objects Wizard** that lets you export this query to a Managed Object Format (MOF) file that can then be imported at another site.|No additional information.|  
|**Move**|Opens the **Move Selected Items** dialog box where you can move the selected query to a folder that you previously created under the **Queries** node.|No additional information.|  

## See Also  
 [Operations and maintenance for queries in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
