---
title: "Plan the site database"
titleSuffix: "Configuration Manager"
description: "Consider the site database and the site database server role as you plan your System Center Configuration Manager hierarchy."
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Plan for the site database for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The site database server is a computer that runs a supported version of Microsoft SQL Server. SQL Server is used to store information for Configuration Manager sites. Each site in a Configuration Manager hierarchy contains a site database and a server that is assigned the site database server role.  

-   For central administration sites and primary sites, you can install SQL Server on the site server, or you can install SQL Server on a computer other than the site server.  

-   For secondary sites, you can use SQL Server Express instead of a full SQL Server installation. The database server must, however, be run on the secondary site server.  

-  For SQL Availability Group usage the Database Recovery Model must be set to FULL  

-  For non-SQL Availability Group usage the Database Recovery Model must be set to SIMPLE  

Further information on SQL Recovery Modes can be found in [Recovery Models (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

The following SQL Server configurations can be used to host the site database:  

-   The default instance of SQL Server  

-   A named instance on a single computer running SQL Server  

-   A named instance on a clustered instance of SQL Server  

-   A SQL Server AlwaysOn availability group (beginning with version 1602 of System Center Configuration Manager)


To host the site database, the SQL Server must meet the requirements detailed in [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## Remote database server location considerations  

If you use a remote database server computer, ensure that the intervening network connection is a high-availability, high-bandwidth network connection. The site server and some site system roles must constantly communicate with the remote server that is hosting the site database.

-   The amount of bandwidth required for communications to the database server depends on a combination of many different site and client configurations. Therefore, the actual bandwidth required cannot be adequately predicted.  

-   Each computer that runs the SMS Provider and that connects to the site database increases network bandwidth requirements.  

-   The computer that runs SQL Server must be located in a domain that has two-way trust with the site server and all computers running the SMS Provider.  

-   You cannot use a clustered SQL Server for the site database server when the site database is co-located with the site server.  


Typically, a site system server supports site system roles from only a single Configuration Manager site. You can, however, use different instances of SQL Server, on clustered or non-clustered servers running SQL Server, to host a database from different Configuration Manager sites. To support databases from different sites, you must configure each instance of SQL Server to use unique ports for communication.  
