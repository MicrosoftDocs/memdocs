---
# required metadata
title: User - Intune Data Warehouse
titleSuffix: Microsoft Intune
description: Reference topic for the User category of entity collections in the Intune Data Warehouse API.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: C29A6EEA-72B7-427E-9601-E05B408F3BB0

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Reference for User entity

The **Users** category contains the **user** entity that defines user properties in the data model.

## users

The **user** entity lists all the Azure Active Directory (Azure AD) users with assigned licenses in your enterprise.

The **user** entity collection contains user data. These records include user states during the data collection period, even if the user has been removed. For example, a user may be added to Intune and then removed during the course of the last month. While this user is not present at the time of the report, the user and state are present in the data from the prior month. You could create a report that would show the duration of the user's historic presence in your data.

|          Property          |                                                                                                           Description                                                                                                          |                Example               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Unique identifier of the user in the data warehouse -   surrogate key.                                                                                                                                                         | 123                                  |
| userId                     | Unique identifier of the user - similar to UserKey, but is   a natural key.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| userEmail                  | Email address of the user.                                                                                                                                                                                                     | John@contoso.com                    |
| userPrincipalName                        | User principal name of the user.                                                                                                                                                                                               | John@contoso.com                    |
| displayName                | Display name of the user.                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | Specifies if this user is Intune licensed or not.                                                                                                                                                                              | True/False                           |
| isDeleted                  | Indicates whether all of the user's licenses have expired   and whether the user was therefore removed from Intune. For a single record,   this flag does not change. Instead, a new record is created for a new user   state. | True/False                           |
| RowLastModifiedDateTimeUTC | Date and time in UTC when the record was last modified in   the data warehouse                                                                                                                                                 | 11/23/2016 0:00                      |


## Next steps
- You can use the **Current User** entity collection to limit the user data to users who are currently active. For more information, see [Reference for current user entity](reports-ref-data-model.md).
- To learn more about how the data warehouse tracks a user's lifetime in Intune, see [User lifetime representation in the Intune Data Warehouse](reports-ref-user-timeline.md).
