---
title: Manage queries
titleSuffix: Configuration Manager
description: Learn how to manage your queries. Includes a table for detailed reference.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to manage queries in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article can help you manage queries in Configuration Manager.  

 For information about how to create queries, see [How to create queries](../../../core/servers/manage/create-queries.md).  

## Manage queries
 In the **Monitoring** workspace, select **Queries**, select the query to manage, and then select a management task.  

 The following table provides information about the management tasks.  

|Management task|Details| 
|---------------------|-------------|
|**Run**|Runs the selected query and displays the results in the Configuration Manager console.|
|**Install Client**|Opens the **Install Client Wizard**, which lets you install the Configuration Manager client on computers returned by the selected query.<br /><br /> This option isn't available for queries that return mobile devices, users, or user groups. <br /><br /> For more information about how to install Configuration Manager clients by using client push, see [Deploy clients to Windows computers](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Export**|Opens the **Export Objects Wizard**. This wizard lets you export the query to a Managed Object Format (MOF) file that you can then import at another site.
|**Move**|Opens the **Move Selected Items** dialog box. This dialog box lets you move the selected query to a folder that you previously created under the **Queries** node.|

## Next steps 
 [Create queries](../../../core/servers/manage/create-queries.md)
