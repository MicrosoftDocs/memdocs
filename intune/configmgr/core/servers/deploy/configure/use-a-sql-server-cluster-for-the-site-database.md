---
title: Failover cluster instance
titleSuffix: Configuration Manager
description: Use a SQL Server Always On failover cluster instance to host the Configuration Manager site database
ms.date: 10/08/2020
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Use a SQL Server Always On failover cluster instance for the site database

*Applies to: Configuration Manager (current branch)*

You can use a SQL Server Always On failover cluster instance to host the Configuration Manager site database. Failover cluster instances provide failover support for the entire instance of SQL Server and improve the reliability of the site database. However, it doesn't provide additional processing or load-balancing benefits. Failover cluster instances require the use of shared storage, which can be a single point of failure. Degradation in performance can occur, because the site server must find the active node of the failover cluster instance before it connects to the site database.

> [!IMPORTANT]
> To successfully set up of a failover cluster instance, use the documentation and procedures for SQL Server. For more information, see [Always On Failover Cluster Instances (SQL Server)](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).

Before you install Configuration Manager, prepare the failover cluster instance to support Configuration Manager. For more information, see [Prepare a clustered SQL Server instance](#bkmk_prepare).

During Configuration Manager setup, the Windows Volume Shadow Copy Service writer installs on each physical computer node of the Windows Server failover cluster. This service supports the **Backup Site Server** maintenance task.

After the site installs, Configuration Manager checks for changes to the cluster node each hour. Configuration Manager automatically manages any changes it finds that affect its component installs. For example, a node failover or the addition of a new node to the failover cluster instance.

## Supported options

Configuration Manager supports the following options for failover cluster instances used for the site database:

- A single instance cluster

- Multiple instance configurations

- Multiple active nodes

- Both a named or a default instance

## Prerequisites

- The site database server must be remote from the site server. The cluster can't include the site server.

    > [!NOTE]
    > The Configuration Manager setup process doesn't block installation of the site server role on a computer with the Windows role for Failover Clustering. SQL Server Always On availability groups require this role, so previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using an availability group and a site server in passive mode. For more information, see [High availability options](high-availability-options.md). <!--3607761, fka 1359132-->

- Add the computer account of the site server to the local **Administrators** group of each server in the cluster.

- To support Kerberos authentication, enable the **TCP/IP** network communication protocol for the network connection of each cluster node. The **Named pipes** protocol isn't required, but can be used to troubleshoot Kerberos authentication issues. The network protocol settings are configured in **SQL Server Configuration Manager**, under **SQL Server Network Configuration**.

- There are specific certificate requirements when you use a failover cluster instance for the site database. For more information, see the following articles:

  - [Install a certificate in an Always On failover cluster instance configuration](/sql/database-engine/configure-windows/manage-certificates#provision-failover-cluster-cert)

  - [PKI certificate requirements for Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#pki-certificates-for-servers)

  > [!NOTE]
  > If you don't pre-provision a certificate in SQL Server, Configuration Manager creates and provisions a self-signed certificate for SQL Server.<!-- 7099499 -->

## Limitations

### Installation and configuration

- Secondary sites can't use a failover cluster instance.

- When you specify a failover cluster instance, you can't set a custom file location for the site database.

### SMS Provider

You can't install the SMS Provider on a failover cluster instance. It's also not supported on a computer that runs as a node participating in the failover cluster instance.

### Data replication options

If you use **Distributed Views**, you can't use a failover cluster instance to host the site database.

### Backup and recovery

Configuration Manager doesn't support System Center Data Protection Manager (DPM) backup for failover cluster instances that use a named instance. It does support DPM backup on failover cluster instances that use the SQL Server default instance.

## <a name="bkmk_prepare"></a> Prepare a failover cluster instance

Here are the main tasks to complete to prepare your site database:

- Create the failover cluster instance to host the site database on an existing Windows Server failover cluster environment. For specific steps to install and set up a failover cluster instance, see the documentation specific to your version of SQL Server. For more information, see [Create a new SQL Server Always On failover cluster instance](/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup).

- On each computer in the failover cluster instance, place a file in the root folder of each drive where you don't want Configuration Manager to install site components. Name the file `NO_SMS_ON_DRIVE.SMS`. By default, Configuration Manager installs some components on each physical node, to support operations such as backup.

- Add the computer account of the site server to the local **Administrators** group of each Windows Server failover cluster node.

- In the failover cluster instance, assign the **sysadmin** SQL Server role to the user account that runs Configuration Manager setup.

## Install a new site

To install a site that uses a clustered site database, run Configuration Manager setup following your normal process for installing a site. On the **Database Information** page, specify the name of the failover cluster instance. The failover cluster instance name replaces the name of a single computer that runs SQL Server.

> [!IMPORTANT]
> Make sure to use the name of the SQL Server Always On failover cluster instance, not the Windows Server failover cluster. If you use the Windows Server failover cluster name, the site database installs on the local hard drive of the active Windows Server failover cluster node. This configuration prevents successful failover if that node fails.
