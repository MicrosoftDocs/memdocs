---
title: Plan the site database
titleSuffix: Configuration Manager
description: Consider the site database and the site database server role as you plan your Configuration Manager hierarchy.
ms.date: 10/08/2020
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Plan for the site database for Configuration Manager

*Applies to: Configuration Manager (current branch)*

The site database server is a computer that runs a supported version of Microsoft SQL Server. SQL Server is used to store information for Configuration Manager sites. Each site in a Configuration Manager hierarchy contains a site database and a server that is assigned the site database server role.  

- For central administration sites and primary sites, you can install SQL Server on the site server, or you can install SQL Server on a computer other than the site server.  

- For secondary sites, you can use SQL Server Express instead of a full SQL Server installation. The database server must, however, be run on the secondary site server.  

- For SQL Server Always On availability groups, set the database recovery model to FULL.

- For non-availability group configurations, set the database recovery model to SIMPLE.

Further information on SQL Server Recovery Modes can be found in [Recovery Models (SQL Server)](/sql/relational-databases/backup-restore/recovery-models-sql-server).

The following SQL Server configurations can be used to host the site database:  

- The default instance of SQL Server  

- A named instance on a single computer running SQL Server  

- A named instance on a failover cluster instance of SQL Server

- A SQL Server Always On availability group

To host the site database, the SQL Server must meet the requirements detailed in [Support for SQL Server versions for Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).

## Remote database server location considerations  

If you use a remote database server computer, ensure that the intervening network connection is a high-availability, high-bandwidth network connection. The site server and some site system roles must constantly communicate with the remote server that is hosting the site database.

- The amount of bandwidth required for communications to the database server depends on a combination of many different site and client configurations. Therefore, the actual bandwidth required cannot be adequately predicted.

- Each computer that runs the SMS Provider and that connects to the site database increases network bandwidth requirements.

- The computer that runs SQL Server must be located in a domain that has two-way trust with the site server and all computers running the SMS Provider.

- You can't use a failover cluster instance of SQL Server for the site database server when the site database is co-located with the site server.  

Typically, a site system server supports site system roles from only a single Configuration Manager site. You can, however, use different instances of SQL Server to host a database from different Configuration Manager sites. To support databases from different sites, configure each instance of SQL Server to use unique ports for communication.
