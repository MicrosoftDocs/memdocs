---
title: Reinit missing message
titleSuffix: Configuration Manager
description: Use this diagram to start troubleshooting a missing message with SQL replication reinit in Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual


ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Reinit missing message

In a multi-site hierarchy, Configuration Manager uses SQL replication to transfer data between sites. For more information, see [Database replication](/sccm/core/plan-design/hierarchy/database-replication).

Use the following diagram to start troubleshooting a missing message with SQL replication reinitialization (reinit):

![Diagram to troubleshoot reinit missing message](media/reinit-missing-message.svg)

## Queries

This diagram uses the following queries:

### Check if site replication hasn't finished reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### Get the TrackingGuid & Status from subscriber site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### Get the TrackingGuid & Status from the publishing site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## Remediation actions

### Version 1902 and later

To detect the issue and reinit, run the [Replication Link Analyzer](/sccm/core/servers/manage/monitor-replication#BKMK_RLA).

### Version 1810 and earlier

Run the following SQL query to get the `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Then use the `InitializeData` method on the `SMS_ReplicationGroup` WMI class with the following values:

- ReplicationGroupID: from the SQL query above
- SiteCode1: parent site
- SiteCode2: child site

For more information, see [InitializeData method in class SMS_ReplicationGroup](/sccm/develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup).

#### Example

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## Next steps

- [SQL replication reinitialization (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
