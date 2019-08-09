---
title: Global data reinit
titleSuffix: Configuration Manager
description: Use this diagram to start troubleshooting SQL replication reinit for site data in a Configuration Manager hierarchy
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# SQL replication

In a multi-site hierarchy, Configuration Manager uses SQL replication to transfer data between sites. For more information, see [Database replication](/sccm/core/plan-design/hierarchy/database-replication).

Use the following diagram to start troubleshooting SQL replication reinitialization (reinit) for site data in a Configuration Manager hierarchy:

![Diagram to troubleshoot site data reinit](media/site-data-reinit.svg)

## Queries

This diagram uses the following queries:

### Check if site replication hasn't finished reinit

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### Get the TrackingGuid & Status from the CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### Get the TrackingGuid & Status from the primary site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### Check primary site isn’t in maintenance mode

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### Check request status for the tracking ID

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## Next steps

- [Reinit missing message](/sccm/core/servers/manage/replication/reinit-missing-message)
- [Global data reinit](/sccm/core/servers/manage/replication/global-data-reinit)
