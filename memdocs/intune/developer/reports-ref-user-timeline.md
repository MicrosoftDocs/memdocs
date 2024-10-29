---
# required metadata
title: Data Warehouse User Entity Timeline
titleSuffix: Microsoft Intune 
description: Learn how the Microsoft Intune Data Warehouse represents Users in a timeline.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: 363D148E-688F-4830-B6DE-AB4FE3648817

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---

# User lifetime representation in the Microsoft Intune Data Warehouse

You can use the month of data snapshots stored in the Intune Data Warehouse to answer questions about time-based trends. For example, you can look at the number of users being added over a month. You might also ask about the number of users who have been removed from the system.

To provide this type insight, the data warehouse stores historical information. The data warehouse can track the lifetime of an entity. The warehouse records when an entity was created, when the state of the entity changes, and when an entity is deleted. With the history captured with daily snapshots of quantitative measurements, you can compare one day to the previous day, and so on.

Working with entity lifetimes can be confusing since your entities are changing state. That means if you look at a snapshot on day 30, a user record may not exist in an active state in the data. On day 29 the entity record may exist as active. And then before day 28, the user didn't exist at all.

This scenario may be clearer if you walk through the lifetime of an entity.

Assume a user, **John Smith**, gets assigned a license on 06/01/2017, then the **User** table would have the following entry: 
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
|--|--|--|--|--|
| John Smith | FALSE | 06/01/2017 | 12/31/9999 | TRUE
 
John Smith gives up his license on 07/25/2017. The **User** table has the following entries. Changes in existing records are `marked`. 

| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
|--|--|--|--|--|
| John Smith | FALSE | 06/01/2017 | `07/26/2017` | `FALSE` 
| John Smith | TRUE | 07/26/2017 | 12/31/9999 | TRUE 

The first row indicates John Smith existed in Intune from 06/01/2017 to 07/25/2017. The second record indicates that the user was deleted on 07/25/2017 and is no longer present in Intune.

Now let assume John Smith gets a new license assigned on 08/31/2017, then the User table would have the following entries:
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
|--|--|--|--|--|
| John Smith | FALSE | 06/01/2017 | 07/26/2017 | FALSE 
| John Smith | TRUE | 07/26/2017 | `08/31/2017` | `FALSE` 
| John Smith | FALSE | 08/31/2017 | 12/31/9999 | TRUE 
 
A person wanting to see the current state of all users would want to apply a filter where `IsCurrent = TRUE`. 
 
A person wanting to see only existing users would want to apply a filter where `IsCurrent = TRUE AND IsDeleted = FALSE`.

## Dimension tables in the entity lifetime

In order to store the history of state changes in entities, Intune doesn't delete records. Instead it marks the record as deleted. This is called a soft-delete. The dimension tables use various metadata columns to track the lifetime of records. 

The most commonly used metadata columns are: 

| Metadata Property Name  | Interpretation of Values |
|--|--|
| IsDeleted | Indicates whether the entity was deleted in Intune. |
| StartDateInclusiveUTC  | The UTC date the entity was loaded into the Intune Data Warehouse. The entity may have been created before it was imported into the Intune Data Warehouse. |
| DeletedDateUTC  | The UTC date that the entity was deleted in Intune. |  

Any metadata column starting with the prefix **Row**, such as **RowLastModifiedDateTimeUTC**, indicates when a record was created or modified in the Intune Data Warehouse. The warehouse is downstream from the data in Intune. This value has no relationship to the lifetime of the entity in Intune.  
 
Any person wanting to see only those dimension entities that currently exist would want to apply a filter where **IsDeleted = FALSE**.

## Next steps

- To learn more about the **Current User** entity, see [Reference for current user entity](reports-ref-data-model.md).
- To learn more about the **User** entity, see [Reference for user entity](reports-ref-user.md).
