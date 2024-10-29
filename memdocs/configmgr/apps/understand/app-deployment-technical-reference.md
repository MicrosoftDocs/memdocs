---
title: Troubleshooting application deployment technical reference
titleSuffix: Configuration Manager
description: Technical reference for troubleshooting application deployment in Configuration Manager.
ms.date: 11/04/2019
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: troubleshooting
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Technical Reference for Application Deployment in Configuration Manager

*Applies to: Configuration Manager (current branch)*

In this article, you'll learn how application deployments work.

## Before You Begin

When troubleshooting application deployments, there are multiple items that can be useful when reviewing client logs. These items include:

- Application CI ID
- Application Unique ID
- Deployment Type Unique ID
- Application Deployment Unique ID (also known as Assignment Unique ID)
- Application Deployment Purpose
- Content Unique ID
- Collection ID and Name
- Collection Type

To simplify troubleshooting, you can run a SQL query similar to below against the Configuration Manager database to obtain the information listed above.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> When you execute this query, you **must** use the Application Name listed in the General Information tab of Application Properties, instead of using the Localized application name listed in the Software Center tab of Application properties.

## Next Steps

- [Application Deployment Policy](deployment-policy-technical-reference.md)
