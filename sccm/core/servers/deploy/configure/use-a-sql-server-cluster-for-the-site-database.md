---
title: "SQL Server cluster"
titleSuffix: "Configuration Manager"
description: "Use a SQL Server cluster to host the System Center Configuration Manager site database. Includes information about supported options."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: angrobe

---
# Use a SQL Server cluster for the System Center Configuration Manager site database

*Applies to: System Center Configuration Manager (Current Branch)*


 You can use a SQL Server cluster to host the System Center Configuration Manager site database. The site database is the only site system role supported on a Server cluster.  

> [!IMPORTANT]  
>  Successful set up of SQL Server clusters relies on documentation and procedures provided in the SQL Server documentation library.  

 A cluster can provide failover support and improve the reliability of the site database. However, it does not provide additional processing or load balancing benefits. In fact, degradation in performance can occur, because the site server must find the active node of the SQL Server cluster before it connects to the site database.  

 Before you install Configuration Manager, you must prepare the SQL Server cluster to support Configuration Manager. (See the prerequisites later in this section.)  

 During Configuration Manager setup, the Windows Volume Shadow Copy Service writer installs on each physical computer node of the Microsoft Windows Server cluster. This supports the **Backup Site Server** maintenance task.  

 After the site installs, Configuration Manager checks for changes to the cluster node each hour. Configuration Manager automatically manages any changes that are found that affect Configuration Manager component installations (like a node failover, or the addition of a new node to the SQL Server cluster).  

## Supported options for using a SQL Server failover cluster

The following options are supported for SQL Server failover clusters used as the site database:

-   A single instance cluster  

-   Multiple instance configuration  

-   Multiple active nodes  

-   Both a named or a default instance  

Be aware of the following prerequisites:  

-   The site database must be remote from the site server. (The cluster cannot include the site system server.)  

-   You must add the computer account of the site server to the Local Administrators group of each server in the cluster.  

-   To support Kerberos authentication, the **TCP/IP** network communication protocol must be enabled for the network connection of each SQL Server cluster node. **Named pipes** is not required, but can be used to troubleshoot Kerberos authentication issues. The network protocol settings are configured in **SQL Server Configuration Manager**, under **SQL Server Network Configuration**.  

-   If you use a PKI, see PKI Certificate Requirements for Configuration Manager for specific certificate requirements when you use a SQL Server cluster for the site database.  

Consider the following limitations:  

-   **Installation and configuration:**  

    -   Secondary sites cannot use a SQL Server cluster.  

    -   The option to specify non-default file locations for the site database is not available when you specify a SQL Server cluster.  

-   **SMS Provider:**  

    -   It is not supported to install an instance of the SMS Provider on a SQL Server cluster, or on a computer that runs as a clustered SQL Server node.  

-   **Data replication options:**  

    -   If you will use **Distributed Views**, you cannot use a SQL Server cluster to host the site database.  

-   **Backup and recovery:**  

    -   Configuration Manager does not support Data Protection Manager (DPM) backup for a SQL Server cluster that uses a named instance. It does, however, support DPM backup on a SQL Server cluster that uses the default instance of SQL Server.  

## Prepare a clustered SQL Server instance for the site database  

Here are the main tasks to complete in order to prepare your site database:

-   Create the virtual SQL Server cluster to host the site database on an existing Windows Server cluster environment. For specific steps to install and set up a SQL Server cluster, see the documentation specific to your version of SQL Server. For example, if you are using SQL Server 2008 R2, see [Installing a SQL Server 2008 R2 Failover Cluster](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   On each computer in the SQL Server cluster, you can place a file in the root folder of each drive where you do not want Configuration Manager to install site components. The file should be named **NO_SMS_ON_DRIVE.SMS**. By default, Configuration Manager installs some components on each physical node, to support operations such as backup.  

-   Add the computer account of the site server to the **Local Administrators** group of each Windows Server cluster node computer.  

-   In the virtual SQL Server instance, assign the **sysadmin** SQL Server role to the user account that will run Configuration Manager setup.  

### To install a new site using a clustered SQL Server  
 To install a site that uses a clustered site database, run Configuration Manager setup following your normal process for installing a site, with the following alteration:  

-   On the **Database Information** page, specify the name of the virtual SQL Server cluster instance that will host the site database. The virtual instance replaces the name of the computer that runs SQL Server.  

    > [!IMPORTANT]  
    >  When you enter the name of the virtual SQL Server cluster instance, do not enter the virtual Windows Server name created by the Windows Server cluster. If you use the virtual Windows Server name, the site database installs on the local hard drive of the active Windows Server cluster node. This prevents successful failover if that node fails.  
