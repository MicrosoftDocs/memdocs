---
title: User Device Association - Intune Data Warehouse
description: The UserDeviceAssociation entity contains user device associations in your organization.
ms.date: 10/30/2024
ms.topic: reference
ms.reviewer: jamiesil
ms.collection:
- M365-identity-device-management
---
# Reference for User Device Association entity

The **userDeviceAssociation** entity contains user device associations in your organization.

## userDeviceAssociations


|        Name        |                                           Description                                            |        Example         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Unique identifier of the user in the data warehouse. (Surrogate key).               |          123           |
|     deviceKey      |                      Unique identifier of the device in the data warehouse.                      |          123           |
| createdDateTimeUTC |           Date and time when the user device association was created. Uses UTC format.           | 11/23/2016 12:00:00 AM |
|     isDeleted      | Indicates that the user unenrolled that device, and that the association is not current anymore. |       True/False       |
|  endedDateTimeUTC  |              Date and time in UTC when IsDeleted changed to <strong>True</strong>.               | 06/23/2017 12:00:00 AM |

## Next steps

- Learn more about the [Intune Data Warehouse](reports-nav-create-intune-reports.md).
