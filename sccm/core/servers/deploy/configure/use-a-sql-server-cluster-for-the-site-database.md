---
title: SQL Server cluster
titleSuffix: Configuration Manager
description: Use a SQL Server cluster to host the Configuration Manager site database
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Use a SQL Server cluster for the site database

*Applies to: Configuration Manager (current branch)*

You can use a SQL Server Failover cluster to host the Configuration Manager site database. A cluster provides failover support and improves the reliability of the site database. However, it doesn't provide additional processing or load-balancing benefits. Additionally, a SQL Server Failover cluster uses shared storage and introduces a single point of failure. Degradation in performance can occur, because the site server must find the active node of the SQL Server cluster before it connects to the site database.  

> [!IMPORTANT]  
> Successful set up of SQL Server clusters relies on documentation and procedures provided in the SQL Server documentation library.  


Before you install Configuration Manager, prepare the SQL Server cluster to support Configuration Manager. For more information, see [Prepare a clustered SQL Server instance](#bkmk_prepare).

During Configuration Manager setup, the Windows Volume Shadow Copy Service writer installs on each physical computer node of the Microsoft Windows Server cluster. This service supports the **Backup Site Server** maintenance task.  

After the site installs, Configuration Manager checks for changes to the cluster node each hour. Configuration Manager automatically manages any changes that are found that affect its component installs. For example, a node failover, or the addition of a new node to the SQL Server cluster.  



## Supported options

The following options are supported for SQL Server failover clusters used as the site database:

- A single instance cluster  

- Multiple instance configurations  

- Multiple active nodes  

- Both a named or a default instance  



## Prerequisites

Be aware of the following prerequisites:  

- The site database must be remote from the site server. The cluster can't include the site system server.  

    > [!Note]  
    > Starting in version 1810, the Configuration Manager setup process no longer blocks installation of the site server role on a computer with the Windows role for Failover Clustering. Previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using a SQL cluster and a site server in passive mode. For more information, see [High availability options](/sccm/core/servers/deploy/configure/high-availability-options). <!--3607761, fka 1359132-->  

- Add the computer account of the site server to the local **Administrators** group of each server in the cluster.  

- To support Kerberos authentication, enable the **TCP/IP** network communication protocol for the network connection of each SQL Server cluster node. The **Named pipes** protocol isn't required, but can be used to troubleshoot Kerberos authentication issues. The network protocol settings are configured in **SQL Server Configuration Manager**, under **SQL Server Network Configuration**.  

- If you use a public key infrastructure (PKI), see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements). There are specific certificate requirements when you use a SQL Server cluster for the site database.  



## Limitations

Consider the following limitations:  


### Installation and configuration

- Secondary sites can't use a SQL Server cluster.  

- When you specify a SQL Server cluster, the option to specify non-default file locations for the site database isn't available.  


### SMS Provider

You can't install an instance of the SMS Provider on a SQL Server cluster. It's also not supported on a computer that runs as a clustered SQL Server node.  


### Data replication options

If you use **Distributed Views**, you can't use a SQL Server cluster to host the site database.  


### Backup and recovery

Configuration Manager doesn't support Data Protection Manager (DPM) backup for a SQL Server cluster that uses a named instance. It does support DPM backup on a SQL Server cluster that uses the default instance of SQL Server.  



## <a name="bkmk_prepare"></a> Prepare a clustered SQL Server instance  

Here are the main tasks to complete to prepare your site database:

- Create the virtual SQL Server cluster to host the site database on an existing Windows Server cluster environment. For specific steps to install and set up a SQL Server cluster, see the documentation specific to your version of SQL Server. For more information, see [Create a new SQL Server Failover Cluster](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- On each computer in the SQL Server cluster, place a file in the root folder of each drive where you don't want Configuration Manager to install site components. Name the file `NO_SMS_ON_DRIVE.SMS`. By default, Configuration Manager installs some components on each physical node, to support operations such as backup.  

- Add the computer account of the site server to the local **Administrators** group of each Windows Server cluster node computer.  

- In the virtual SQL Server instance, assign the **sysadmin** SQL Server role to the user account that runs Configuration Manager setup.  


### To install a new site using a clustered SQL Server  

To install a site that uses a clustered site database, run Configuration Manager setup following your normal process for installing a site, with the following alteration:  

- On the **Database Information** page, specify the name of the virtual SQL Server cluster instance that will host the site database. The virtual instance replaces the name of the computer that runs SQL Server.  

    > [!IMPORTANT]  
    > When you enter the name of the virtual SQL Server cluster instance, don't enter the virtual Windows Server name created by the Windows Server cluster. If you use the virtual Windows Server name, the site database installs on the local hard drive of the active Windows Server cluster node. This prevents successful failover if that node fails.  
