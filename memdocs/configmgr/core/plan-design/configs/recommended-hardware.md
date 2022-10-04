---
title: Recommended hardware
titleSuffix: Configuration Manager
description: Get hardware recommendations to help you scale your Configuration Manager environment beyond a basic deployment.
ms.date: 03/04/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Recommended hardware for Configuration Manager

*Applies to: Configuration Manager (current branch)*

The following recommendations are guidelines to help you scale your Configuration Manager environment to support more than a very basic deployment of sites, site systems, and clients. They aren't intended to cover all possible site and hierarchy configurations.  

Use the information in the following sections as a guide to help you plan for hardware. Make sure your hardware can meet the processing loads for clients and sites that use the available Configuration Manager features.

## Site systems

This section provides recommended hardware configurations for Configuration Manager site systems. Use these recommendations to support the maximum number of clients and use most or all Configuration Manager features. If your environment supports less than the maximum number of clients, and doesn't use all available features, it might require less resources. In general, the following key factors limit performance of the overall system:

1. Disk I/O performance

2. Available memory

3. CPU

For best performance, use RAID 10 configurations for all data drives and a 1-Gbps Ethernet network.

### Site servers

|Site configuration|CPU (cores)|Memory (GB)|Memory allocation for SQL Server (%)|
|-------------------------------|---------------|---------------|----------------------------------------|
|Stand-alone primary site server with a database site role on the same server <sup>[Note 1](#bkmk_note1)</sup>|16|96|80|
|Stand-alone primary site server with a remote site database|8|16|-|
|Remote database server for a stand-alone primary site|16|72|90|
|Central administration site server with a database site role on the same server <sup>[Note 1](#bkmk_note1)</sup>|20|128|80|
|Central administration site server with a remote site database|8|16|-|
|Remote database server for a central administration site|16|96|90|
|Child primary site with a database site role on the same server|16|96|80|
|Child primary site server with a remote site database|8|16|-|
|Remote database server for a child primary site|16|72|90|
|Secondary site server|8|16|-|

#### <a name="bkmk_note1"></a> Note 1: Collocated SQL

When you install the site server and SQL Server on the same computer, the deployment supports the maximum [sizing and scale numbers](size-and-scale-numbers.md) for sites and clients. This configuration can limit [high availability options](../../servers/deploy/configure/high-availability-options.md), like using a SQL Server Always On failover cluster instance. If you have a larger environment, because of the higher I/O requirements to support both roles on the same computer, consider using a remote SQL Server.

### Remote site system servers

The following guidance is for computers that hold a single site system role. Plan to adjust when you install multiple site system roles on the same computer.

|Site system role|CPU (cores)|Memory (GB)|Disk space (GB)|
|----------------------|---------------|---------------|--------------------|
|Management point|4|8|50|
|Distribution point|2|8|As required by the OS and to store content that you deploy|
|Software update point <sup>[Note 2](#bkmk_note2)</sup>|8|16|As required by the OS and to store updates that you deploy|
|All other site system roles|4|8|50|

#### <a name="bkmk_note2"></a> Note 2: WSUS configurations

The computer that hosts a software update point requires the following configurations for IIS application pools:

- Increase the **WsusPool Queue Length** to **2000**.

- Increase the **WsusPool Private Memory limit** by four times, or set it to **0** (unlimited).

### Disk space for site systems

Disk allocation and configuration contribute to the performance of Configuration Manager. Because each Configuration Manager environment is different, the values that you implement can vary from the following guidance.

For the best performance, place each object on a separate, dedicated RAID volume. For all data volumes for Configuration Manager and its database files, use RAID 10 for the best performance.

|Data usage|Minimum disk space|25,000 clients|50,000 clients|100,000 clients|150,000 clients|700,000 clients (central administration site)|
|----------|------------------|--------------|--------------|---------------|---------------|---------------------------------------------|
|Configuration Manager application and log files|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|
|Site database .mdf file|75 GB for every 25,000 clients|75 GB|150 GB|300 GB|500 GB|2 TB|
|Site database .ldf file|25 GB for every 25,000 clients|25 GB|50 GB|100 GB|150 GB|100 GB|
|Temp database files (.mdf and .ldf)|As needed|As needed|As needed|As needed|As needed|As needed|

For the Windows system disk, see sizing guidance for the installed OS version.

For content on distribution points, it depends upon your deployments. This guidance doesn't include the disk space required for the content library on the site server or distribution points. For more information, see [The content library](../../../core/plan-design/hierarchy/the-content-library.md).

When you plan for disk space requirements, consider the following guidelines:

- Each client requires about 5-10 MB of space in the database. This number depends upon the hierarchy type, the configuration, and the number of clients. The size can be less for larger environments. Smaller sites have greater database usage per client.<!-- SCCMDocs#1048 -->

- For the primary site's temp database, plan for a combined size that is 25% to 30% of the site database .mdf file. The actual size can be smaller or larger. It depends on the performance of the site server and the volume of incoming data over both short and long periods of time.

  > [!NOTE]
  > When you have 50,000 or more clients at a site, plan to use four or more temp database .mdf files.

- The temp database size for a central administration site is typically much smaller than for a primary site.

- If you use SQL Server Express for the secondary site database, it limits the database size to 10 GB.

## Clients

This section provides recommended hardware configurations for computers that you manage by using Configuration Manager client software.

### Client for Windows computers

The following minimum requirements are for Windows-based computers that you manage by using Configuration Manager, including embedded editions:

- **Processor and memory:** Refer to the processor and RAM requirements for the OS.

- **Disk space:** 500 MB of available disk space, with 5 GB recommended for the Configuration Manager client cache. If you use customized settings to install the Configuration Manager client, less disk space is required.

  - Use the client.msi property **SMSCACHESIZE** to set a cache size smaller than the default of 5120 MB. The minimum size is 1 MB. The following example creates a 2-MB cache: `CCMSetup.exe SMSCACHESIZE=2`

    For more information, see [About client installation properties](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > Installing the client with minimal disk space is useful for Windows Embedded devices that typically have smaller disk sizes than standard Windows computers.

The following minimum hardware requirements are for optional functionality in Configuration Manager:

- **OS deployment:** At least 384 MB of RAM

- **Software Center:** At least a 500-MHz processor

- **Remote Control:** For an optimal experience, at least a Pentium 4 Hyper-Threaded 3 GHz (single core) or comparable CPU, with at least 1-GB RAM.

## Configuration Manager console

The following minimum hardware requirements apply to each computer that runs the Configuration Manager console:

- Intel i3 or comparable CPU

- 2 GB of RAM

- 2 GB of disk space

|DPI setting|Minimum resolution|
|-----------|------------------|
|96 / 100%|1024 x 768|
|120 /125%|1280 x 960|
|144 / 150%|1600 x 1200|
|196 / 200%|2500 x 1600|

## Lab deployments

Use the following minimum hardware recommendations for lab and test deployments of Configuration Manager. These recommendations apply to all site types, up to 100 clients:

|Role|CPU (cores)|Memory (GB)|Disk space (GB)|
|----|-----------|-----------|---------------|
|Site and database server|2 - 4|8 - 12|100|
|Site system server|1 - 4|2 - 4|50|
|Client|1 - 2|1 - 3|30|

## Next steps

[Site size and performance guidelines](site-size-performance-guidelines.md)

[Site size and performance FAQ](../../understand/site-size-performance-faq.yml)
