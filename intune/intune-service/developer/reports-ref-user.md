---
title: User - Intune Data Warehouse
description: Reference topic for the User category of entity collections in the Intune Data Warehouse API.
ms.date: 10/30/2024
ms.topic: reference
ms.reviewer: jamiesil
ms.collection:
- M365-identity-device-management
---

# Reference for User entity

The **Users** category contains the **user** entity that defines user properties in the data model.

## users

The **user** entity lists all the Microsoft Entra users with assigned licenses in your enterprise.

The **user** entity collection contains user data. These records include user states during the data collection period, even if the user has been removed. For example, a user may be added to Intune and then removed during the course of the last month. While this user is not present at the time of the report, the user and state are present in the data from the prior month. You could create a report that would show the duration of the user's historic presence in your data.

|          Property          |                                                                                                           Description                                                                                                          |                Example               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Unique identifier of the user in the data warehouse -   surrogate key.                                                                                                                                                         | 123                                  |
| userId                     | Unique identifier of the user - similar to UserKey, but is   a natural key.                                                                                                                                                    | 00aa00aa-bb11-cc22-dd33-44ee44ee44ee |
| userEmail                  | Email address of the user.                                                                                                                                                                                                     | John@contoso.com                    |
| userPrincipalName                        | User principal name of the user.                                                                                                                                                                                               | John@contoso.com                    |
| displayName                | Display name of the user.                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | Specifies if this user is Intune licensed or not.                                                                                                                                                                              | True/False                           |
| isDeleted                  | Indicates whether all of the user's licenses have expired   and whether the user was therefore removed from Intune. For a single record,   this flag does not change. Instead, a new record is created for a new user   state. | True/False                           |
| RowLastModifiedDateTimeUTC | Date and time in UTC when the record was last modified in   the data warehouse                                                                                                                                                 | 11/23/2016 0:00                      |


## Next steps
- You can use the **Current User** entity collection to limit the user data to users who are currently active. For more information, see [Reference for current user entity](reports-ref-data-model.md).
- To learn more about how the data warehouse tracks a user's lifetime in Intune, see [User lifetime representation in the Intune Data Warehouse](reports-ref-user-timeline.md).
