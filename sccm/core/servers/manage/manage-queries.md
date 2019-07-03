---
title: "Manage queries"
titleSuffix: "Configuration Manager"
description: "Learn how to manage your queries. Includes a table for detailed reference."
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---
# How to manage queries in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article can help you manage queries in System Center Configuration Manager.  

 For information about how to create queries, see [How to create queries in System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## Manage queries
 In the **Monitoring** workspace, select **Queries**, select the query to manage, and then select a management task.  

 The following table provides information about the management tasks.  

|Management task|Details| 
|---------------------|-------------|
|**Run**|Runs the selected query and displays the results in the Configuration Manager console.|
|**Install Client**|Opens the **Install Client Wizard**, which lets you install the Configuration Manager client on computers returned by the selected query.<br /><br /> This option isn't available for queries that return mobile devices, users, or user groups. <br /><br /> For more information about how to install Configuration Manager clients by using client push, see [Deploy clients to Windows computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).| 
|**Export**|Opens the **Export Objects Wizard**, which lets you export the query to a Managed Object Format (MOF) file that can then be imported at another site.
|**Move**|Opens the **Move Selected Items** dialog box, which lets you move the selected query to a folder that you previously created under the **Queries** node.|

## Next steps 
 [Create queries in System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
