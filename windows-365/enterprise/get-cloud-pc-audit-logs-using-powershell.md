---
# required metadata
title: Get Windows 365 audit logs using PowerShell
titleSuffix:
description: Learn how to use PowerShell to retrieve Cloud PC audit logs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
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

# Get Windows 365 audit logs by using PowerShell

Audit logs for Windows 365 include a record of activities that generate a change in a Cloud PC. Create, update (edit), delete, assign, and remote actions all create audit events that administrators can review for most Cloud PC actions that go through Graph. By default, auditing is enabled for all customers. It can't be disabled.

## Who can access the data?

Users with the following permissions can review audit logs:

- Global Administrator
- Intune Service Administrator
- Administrators assigned to an Intune role with **Audit data - Read** permissions

## Use Graph API and PowerShell to retrieve audit events

To get audit log events for up to seven days for your Windows 365 tenant, follow these steps:

### Install the SDK

1. In PowerShell, run this command: ```Install-Module Microsoft.Graph -Scope CurrentUser```
2. Verify the installation by running this command:```Get-InstalledModule Microsoft.Graph```
3. To get all Cloud PC Graph endpoints, run this command: ```Get-Command -Module Microsoft.Graph* *virtualEndpoint*```

### Sign in 

1. Run either of these two commands:
    - ```Connect-MgGraph -Scopes "CloudPC.ReadWrite.All"```
    - ```Connect-MgGraph -Scopes "CloudPC.Read.All"```
2. On the resulting web page, sign in to your tenant with a user account that has the appropriate read and/or write permissions.
3. Switch to the Graph beta environment by using this command: ```Select-MgProfile -Name "beta"```

### Get audit data

You can view audit data in multiple ways.

#### Get entire list of audit events, including the audit actor

To get the entire list of audit events including the actor (person who performed the action), use the following command:

```Get-MgDeviceManagementVirtualEndpointAuditEvent | Select-Object -Property Actor,ActivityDateTime,ActivityType,ActivityResult -ExpandProperty Actor | Format-Table UserId, UserPrincipalName, ActivityType, ActivityDateTime, ActivityResult```

#### Get a list of audit events

To get a list of audit events without the audit actor, use the following command:

```Get-MgDeviceManagementVirtualEndpointAuditEvent```

To get all the events, use the **-All** parameter: ```Get-MgDeviceManagementVirtualEndpointAuditEvent -All```

To get only the top N events, use the following parameters: ```Get-MgDeviceManagementVirtualEndpointAuditEvent -All -Top {TopNumber}```

#### Get a single event by event ID

You can use the following command to get a single audit event, where you will need to provide the {event ID}: ```Get-MgDeviceManagementVirtualEndpointAuditEvent -CloudPcAuditEventId {event ID}```

<!-- ########################## -->
## Next steps

[Business continuity and disaster recovery](business-continuity-disaster-recovery.md).
