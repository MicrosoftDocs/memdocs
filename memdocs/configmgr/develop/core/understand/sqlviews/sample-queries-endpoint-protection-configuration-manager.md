---
title: Sample queries for endpoint protection
titleSuffix: Configuration Manager
description: Sample queries that show how to join the most common Endpoint Protection views to other views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: c639ace8-52dd-4e91-92fa-e11e56878bd7
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for endpoint protection in Configuration Manager

The following sample queries demonstrate how to join the most common Endpoint Protection views to other views.

## Joining endpoint protection and collection views

The following query lists the deployment state of the Endpoint Protection client on all computers by using the **v_GS_EPDeploymentState** view. For each computer, it also adds the client name and site code by joining by **ResourceID** to the **v_ClientCollectionMembers** view.

```sql
    SELECT   v_GS_EPDeploymentState_1.ResourceID, v_ClientCollectionMembers.Name, v_ClientCollectionMembers.SiteCode, 
                     v_GS_EPDeploymentState_1.LastMessageTime, v_GS_EPDeploymentState_1.DeploymentState, v_GS_EPDeploymentState_1.Error, 
                     v_GS_EPDeploymentState_1.ErrorCode
    FROM    v_GS_EPDeploymentState AS v_GS_EPDeploymentState_1 INNER JOIN
            v_ClientCollectionMembers ON v_GS_EPDeploymentState_1.ResourceID = v_ClientCollectionMembers.ResourceID
```

## See also

[Endpoint protection views in Configuration Manager](endpoint-protection-views-configuration-manager.md)
