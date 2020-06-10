---
title: Always On Failover Cluster Insatnce
titleSuffix: Configuration Manager
description: Use an Always On failover cluster instance to host the Configuration Manager site database
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Use an Always On failover cluster instance for the site database

*Applies to: Configuration Manager (current branch)*

You can use an Always On failover cluster instance (FCI) to host the Configuration Manager site database. FCIs provide failover support for the entire instance of SQL Server and improves the reliability of the site database. However, it doesn't provide additional processing or load-balancing benefits. Additionally, FCIs require the use of shared storage which is considered a single point of failure. Degradation in performance can occur, because the site server must find the active node of the SQL Server cluster before it connects to the site database.  

> [!IMPORTANT]  
> Successful set up of an FCI relies on documentation and procedures provided in the SQL Server documentation library.  


Before you install Configuration Manager, prepare the FCI to support Configuration Manager. For more information, see [Prepare a clustered SQL Server instance](#bkmk_prepare).

During Configuration Manager setup, the Windows Volume Shadow Copy Service writer installs on each physical computer node of the Windows Server failover cluster (WSFC). This service supports the **Backup Site Server** maintenance task.  

After the site installs, Configuration Manager checks for changes to the cluster node each hour. Configuration Manager automatically manages any changes that are found that affect its component installs. For example, a node failover, or the addition of a new node to the FCI.  



## Supported options

The following options are supported for FCIs used as the site database:

- A single instance cluster  

- Multiple instance configurations  

- Multiple active nodes  

- Both a named or a default instance  



## Prerequisites

Be aware of the following prerequisites:  

- The site database must be remote from the site server. The cluster can't include the site system server.  

    > [!Note]  
    > Starting in version 1810, the Configuration Manager setup process no longer blocks installation of the site server role on a computer with the Windows role for Failover Clustering. Previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using a SQL cluster and a site server in passive mode. For more information, see [High availability options](high-availability-options.md). <!--3607761, fka 1359132-->  

- Add the computer account of the site server to the local **Administrators** group of each server in the cluster.  

- To support Kerberos authentication, enable the **TCP/IP** network communication protocol for the network connection of each SQL Server cluster node. The **Named pipes** protocol isn't required, but can be used to troubleshoot Kerberos authentication issues. The network protocol settings are configured in **SQL Server Configuration Manager**, under **SQL Server Network Configuration**.  

- There are specific certificate requirements when you use a SQL Server cluster for the site database. For more information, see the following articles:
  - [Install a certificate in an Always On failover cluster instance configuration](https://docs.microsoft.com/sql/database-engine/configure-windows/manage-certificates?view=sql-server-ver15#provision-failover-cluster-cert)
  - [PKI certificate requirements for Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > If you don't pre-provision a certificate in SQL Server, Configuration Manager creates and provisions a self-signed certificate for SQL Server.<!-- 7099499 -->

## Limitations

Consider the following limitations:  


### Installation and configuration

- Secondary sites can't use a FCI.  

- When you specify a FCI, the option to specify non-default file locations for the site database isn't available.  


### SMS Provider

You can't install an instance of the SMS Provider on an FCI. It's also not supported on a computer that runs as a node participating in the FCI.  


### Data replication options

If you use **Distributed Views**, you can't use an FCI to host the site database.  


### Backup and recovery

Configuration Manager doesn't support Data Protection Manager (DPM) backup for FCIs that uses a named instance. It does support DPM backup on FCIs that are installed as a default instance.  



## <a name="bkmk_prepare"></a> Prepare a clustered SQL Server instance  

Here are the main tasks to complete to prepare your site database:

- Create the FCI to host the site database on an existing WSFC environment. For specific steps to install and set up a FCI see the documentation specific to your version of SQL Server. For more information, see [Create a new Always On Failover Cluster Instance](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-always-on-failover-cluster-instance-setup?view=sql-server-2017).  

- On each computer in the FCI, place a file in the root folder of each drive where you don't want Configuration Manager to install site components. Name the file `NO_SMS_ON_DRIVE.SMS`. By default, Configuration Manager installs some components on each physical node, to support operations such as backup.  

- Add the computer account of the site server to the local **Administrators** group of each WSFC node.  

- In the FCI, assign the **sysadmin** SQL Server role to the user account that runs Configuration Manager setup.  


### To install a new site using a clustered SQL Server  

To install a site that uses a clustered site database, run Configuration Manager setup following your normal process for installing a site, with the following alteration:  

- On the **Database Information** page, specify the name of the FCI that will host the site database. The FCI name replaces the name of a local computer that runs SQL Server.  

    > [!IMPORTANT]  
    > When you enter the name of the FCI, don't enter the name of the WSFC. If you use the WSFC name, the site database installs on the local hard drive of the active WSFC node. This prevents successful failover if that node fails.  
