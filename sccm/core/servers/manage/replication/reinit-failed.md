---
title: Reinit failed
titleSuffix: Configuration Manager
description: Use this diagram to start troubleshooting SQL replication reinit failures with Configuration Manager
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 14c6c369-9f7e-4a7e-83be-73091f094899
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Reinit failed

In a multi-site hierarchy, Configuration Manager uses SQL replication to transfer data between sites. For more information, see [Database replication](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_dbrep).

Use the following diagram to start troubleshooting SQL replication reinitialization (reinit) failures:

![Diagram to troubleshoot reinit failed](media/reinit-failed.svg)

### Queries

This diagram uses the following queries:

#### Check if site replication hasn't finished reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

#### Get the TrackingGuid & ReplicationGroup from the subscriber site

```sql
SELECT RequestTrackingGUID, rg.ReplicationGroup
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus = 99
```

### Remediation actions

#### Version 1902 and later

Run the Replication Link Analyzer to detect the issue and reinit.

#### Version 1810 and earlier

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
