---
# required metadata
title: Get Cloud PC audit logs using PowerShell
titleSuffix:
description: Learn how to use PowerShell to retrieve Cloud PC audit logs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/26/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Get Cloud PC audit logs by using PowerShell

Audit logs include a record of activities that generate a change in a Cloud PC. Create, update (edit), delete, assign, and remote actions all create audit events that administrators can review for most Cloud PC actions. By default, auditing is enabled for all customers. It can't be disabled.

## Who can access the data?

Users with the following permissions can review audit logs:

- Global Administrator
- Intune Service Administrator
- Administrators assigned to an Intune role with Audit data - Read permissions

## Use Graph API and PowerShell to retrieve audit events

To get audit log events for up to a year, run the following PowerShell script:

<!--waiting for script to be provided-->

<!-- ########################## -->
## Next steps

[Learn more about monitoring Cloud PC](monitor-cloud-pc.md).