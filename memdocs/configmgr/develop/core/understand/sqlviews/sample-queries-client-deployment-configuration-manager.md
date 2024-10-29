---
title: Sample queries for client deployment
titleSuffix: Configuration Manager
description: Sample queries that show how to join the most common client deployment views to other views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: 66e102b8-f80c-4dc8-b39c-e2a5a50c74a6
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for client deployment in Configuration Manager

The following sample queries demonstrate how to join the most common client deployment views to other views.

The following sample query demonstrates how to join client deployment views with other views. Client deployment views will most often use the **MachineID** column, which is the same as the **ResourceID** column in other views, and **NetBiosName** column when joining to other views.

## Joining client deployment and discovery views

This query retrieves the NetBIOS name for client computers that have provided client deployment status, the user name, assigned site, time of last state message, and state name. The results are sorted by deployment state and then NetBIOS name. The query joins the **v_ClientDeploymentState** client deployment view with the **v_R_System** discovery view by using the **ResourceID** column, and the **v_ClientDeployment** view with the **v_StateNames** status view by using the **LastMessageStateID** and **StateID** columns, respectively. The retrieved information is filtered by the topic type of **800**, which includes only state messages for client deployment.

```sql
    SELECT v_ClientDeploymentState.NetBiosName AS Computer, 
    ��v_R_System.User_Name0 AS [User], 
    ��v_ClientDeploymentState.AssignedSiteCode AS [Assigned Site], 
    ��v_ClientDeploymentState.LastMessageTime AS [Last Message], 
    ��v_StateNames.StateName AS State 
    FROM v_ClientDeploymentState INNER JOIN v_R_System ON 
    ��v_ClientDeploymentState.SMSID = v_R_System.SMS_Unique_Identifier0 INNER JOIN v_StateNames ON 
    ��v_ClientDeploymentState.LastMessageStateID = v_StateNames.StateID 
    WHERE (v_StateNames.TopicType = 800) 
    ORDER BY State, Computer 
```

## See also

[Client deployment views in Configuration Manager](client-deployment-views-configuration-manager.md)
