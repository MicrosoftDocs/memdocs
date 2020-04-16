---
title: SQL configuration
titleSuffix: Configuration Manager
description: Use this diagram to start troubleshooting SQL configuration for Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual


ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# SQL configuration

In a multi-site hierarchy, Configuration Manager uses SQL replication to transfer data between sites. For more information, see [Database replication](/sccm/core/plan-design/hierarchy/database-replication).

Use the following diagram to start troubleshooting SQL configuration related to SQL Service Broker:

![Diagram to troubleshoot SQL configuration](media/sql-configuration.svg)

## Queries

This diagram has the following queries and actions:

### Check if SQL can deliver SSB messages

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## Remediation actions

### Remediate the issues reported from transmission_status

Common issues:

- Firewall configuration
- Network configuration
- SSB certificate misconfigured

### Run SQL profiler to trace SSB events

Run SQL profiler on the CAS and primary site database to trace events related to the SQL Service Broker:

- **Audit Broker Login**
- **Audit Broker Conversation**
- Events in **Broker** category
