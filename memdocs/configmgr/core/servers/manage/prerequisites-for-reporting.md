---
title: Prerequisites for reporting
titleSuffix: Configuration Manager
description: Understand various dependencies that impact your use of reporting in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Prerequisites for reporting in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Reporting in Configuration Manager has the following dependencies:

- SQL Server Reporting Services
- Reporting services point
- Power BI Report Server (optional, starting in version 2002)

## SQL Server Reporting Services

Before you can use reporting in Configuration Manager, install and configure SQL Server Reporting Services.

For more information about planning and deploying Reporting Services, see the [Install SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Install the Reporting Services database on either the default instance or a named instance of a 64-bit SQL Server installation. Colocate the SQL Server instance with the site system server, or configure it on a remote computer.

Configuration Manager supports the same versions of SQL Server for reporting as it does for the site database. For more information, see [Supported SQL Server versions](/configmgr/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions).

## Reporting services point

Before you can use reporting in Configuration Manager, configure the reporting services point site system role.

For more information, see [Site and site system prerequisites](/configmgr/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012RSpoint).

## Power BI Report Server

Starting in version 2002, you can integrate reporting with Power BI Report Server. For more information including prerequisites, see [Integrate with Power BI Report Server](/configmgr/core/servers/manage/powerbi-report-server).

## Next steps

[Configure reporting](/configmgr/core/servers/manage/configuring-reporting)
