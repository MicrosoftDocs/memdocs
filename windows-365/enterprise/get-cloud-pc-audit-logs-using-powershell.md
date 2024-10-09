---
# required metadata
title: Get Windows 365 audit logs using PowerShell
titleSuffix:
description: Learn how to use PowerShell to retrieve Cloud PC audit logs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/20/2023
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Get Windows 365 audit logs

Audit logs for Windows 365 include a record of activities that generate a change in a Cloud PC. Create, update (edit), delete, assign, and remote actions all create audit events that administrators can review for most Cloud PC actions that go through Graph. By default, auditing is enabled for all customers. It can't be disabled.

## Who can access the data?

Users with the following permissions can review audit logs:

- Intune Service Administrator
- Global Administrator
- Administrators assigned to an Intune role with **Audit data - Read** permissions

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Send Windows 365 audit logs to diagnostic settings in Azure Monitor

Azure monitor's diagnostic settings let you export platform logs and metrics to the destination of your choice. You can create up to five different diagnostic settings to send different logs and metrics to independent destinations. For more information, see [Diagnostic settings in Azure Monitor](/azure/azure-monitor/essentials/diagnostic-settings).

### To create a diagnostic setting for sending logs

1. Make sure you have an Azure account.
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Diagnostic settings** (under **Azure monitor**)> **Add Diagnostic settings**.
3. Under **Logs**, select **Windows365AuditLogs**.
4. Under **Destination details**, select the destination and provide details.
5. Select **Save**.

## Use Graph API and PowerShell to retrieve audit events

To get audit log events for your Windows 365 tenant, follow these steps:

### Install the SDK

1. In PowerShell, run this command: ```Install-Module Microsoft.Graph.Beta -Scope CurrentUser -AllowClobber```
2. Verify the installation by running this command:```Get-InstalledModule Microsoft.Graph.Beta```
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

```Get-MgBetaDeviceManagementVirtualEndpointAuditEvent | Select-Object -Property Actor,ActivityDateTime,ActivityType,ActivityResult -ExpandProperty Actor | Format-Table UserId, UserPrincipalName, ActivityType, ActivityDateTime, ActivityResult```

#### Get a list of audit events

To get a list of audit events without the audit actor, use the following command:

```Get-MgBetaDeviceManagementVirtualEndpointAuditEvent```

To get all the events, use the **-All** parameter: ```Get-MgBetaDeviceManagementVirtualEndpointAuditEvent -All```

To get only the top N events, use the following parameters: ```Get-MgBetaDeviceManagementVirtualEndpointAuditEvent -All -Top {TopNumber}```

#### Get a single event by event ID

You can use the following command to get a single audit event, where you'll need to provide the {event ID}: ```Get-MgBetaDeviceManagementVirtualEndpointAuditEvent -CloudPcAuditEventId {event ID}```

<!-- ########################## -->
## Next steps

[Business continuity and disaster recovery](business-continuity-disaster-recovery.md).
