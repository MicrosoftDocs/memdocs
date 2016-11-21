---
title: "Recommended hardware | Microsoft Docs"
description: "Get hardware recommendations to help you scale your System Center Configuration Manager environment beyond a basic deployment."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
caps.latest.revision: 26
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Recommended hardware for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
The following recommendations are guidelines  to help you scale your System Center Configuration Manager environment to support more than a very basic deployment of sites, sites systems, and clients. They are not intended to cover all possible site and hierarchy configurations.  

 Use this information in the following sections as a guide to help you plan for hardware that can meet the processing loads for clients and sites that use the available Configuration Manager features with the default configurations.  


##  <a name="bkmk_ScaleSieSystems"></a> Site systems  
 This section identifies recommended hardware configurations for Configuration Manager site systems for  deployments that support the maximum number of clients and use most or all Configuration Manager features. Deployments that support less than  the maximum number of clients and that do not use all available features can  require fewer computer resources. In general, the key factors that limit performance of the overall system include the following, in order:  

1.  Disk I/O performance  

2.  Available memory  

3.  CPU  

For best performance, use RAID 10 configurations for all data drives and 1Gbps Ethernet network  

###  <a name="bkmk_ScaleSiteServer"></a> Site servers  

|Stand-alone primary site|CPU cores|Memory GB|Memory % allocation for SQL Server|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Stand-alone primary site server with database site role on the same server<sup>1</sup>|16|96|80|  
|Stand-alone primary site server with a remote site database|8|16|-|  
|Remote database server for a stand-alone primary site|16|64|90|  
|Central administration site server with database site role on the same server<sup>1</sup>|16|96|80|  
|Central administration site server with a remote site database|8|16|-|  
|Remote database server for a central administration site|16|96|90|  
|Child primary site with database site role on the same server|16|96|80|  
|Child primary site server with a remote site database|8|16|-|  
|Remote database server for a child primary site|16|64|90|  
|Secondary site server|8|16|-|  

 <sup>1</sup> When the site server and SQL Server are installed on the same computer, the deployment supports the maximum [Sizing and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers) for sites and clients. However, this configuration can limit [High availability options for System Center Configuration Manager](/sccm/protect/understand/high-availability-options) like using a SQL Server cluster.  Additionally, because of the higher I/O requirements needed to support both SQL Server and the Configuration Manager Site Server when running both on the same computer, customers with larger deployments should consider using a configuration with a remote SQL Server machine.  

###  <a name="bkmk_RemoteSiteSystem"></a> Remote site system servers  
 These following guidance is for computers that hold a single site system role. Plan to make adjustments when you install multiple site system roles on the same computer.  

|Site system role|CPU cores|Memory GB|Disk space: GB|  
|----------------------|---------------|---------------|--------------------|  
|Management point|4|8|50|  
|Distribution point|2|8|As required by the operating system and to store content you deploy|  
|Application Catalog, with the web service and website on the site system computer|4|16|50|  
|Software update point<sup>1</sup>|8|16|As required by the operating system and to store updates you deploy|  
|All other site system roles|4|8|50|  

 <sup>1</sup> The computer that hosts a software update point requires the following configurations for IIS Application Pools:  

-   Increase the **WsusPool Queue Length** to **2000**  

-   Increase the **WsusPool Private Memory limit** x4 times, or set to **0** (unlimited)  

###  <a name="bkmk_DiskSpace"></a> Disk space for site systems  
 Disk allocation and configuration contributes to the performance of Configuration Manager. Because each Configuration Manager environment is different, the values you implement can vary from the following guidance.  

 For the best performance, place each object on a separate, dedicated RAID volume. For all data volumes (Configuration Manager and its database files), use RAID 10 for the best performance.  

|Data usage|Minimum disk space|25,000 clients|50,000 clients|100,000 clients|150,000 clients|700,000 clients (Central administration site)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Operating system|See guidance for the operating system.|See guidance for the operating system.|See guidance for the operating system.|See guidance for the operating system.|See guidance for the operating system.|See guidance for the operating system.|  
|Configuration Manager Application and Log Files|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Site database .mdf file|75 GB for every 25,000 clients|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Site database .ldf file|25 GB for every 25,000 clients|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Temp database files (.mdf and .ldf)|As needed|As needed|As needed|As needed|As needed|As needed|  
|Content (distribution point shares)|As needed<sup>1</sup>|As needed<sup>1</sup>|As needed<sup>1</sup>|As needed<sup>1</sup>|As needed<sup>1</sup>|As needed<sup>1</sup>|  

 <sup>1</sup> The disk space guidance does not include the space required for content that is located in the content library on the site server or distribution points. For information about planning for the content library, see [The content library](../../../core/plan-design/hierarchy/the-content-library.md).  

 In addition to the preceding guidance, consider the following guidelines when you plan for disk space requirements:  

-   Each client requires approximately 5 MB of space.  

-   When planning for the size of the Temp database for a primary site, plan for a combined size that is 25% to 30% of the site database .mdf file. The actual size can be significantly smaller, or larger, and depends on the performance of the site server and the volume of incoming data over both short and long periods of time.  

    > [!NOTE]  
    >  When you have 50,000 or more clients at a site, plan to use 4 or more Temp database .mdf files.  

-   The Temp database size for a central administration site is typically much smaller than that for a primary site.  

-   The secondary site database is limited in size to the following:  

    -   SQL Server 2012 Express: 10 GB  

    -   SQL Server 2014 Express: 10 GB  

##  <a name="bkmk_ScaleClient"></a> Clients  
 This section identifies recommended hardware configurations for computers that are managed by installing Configuration Manager client software.  

### Client for Windows computers  
 The following are minimum requirements for Windows-based computers that you manage with Configuration Manager, including Embedded operating systems:  

-   **Processor and memory:** Refer to the processor and RAM requirements for the computers operating system.  

-   **Disk space:** 500MB available disk space, with 5GB recommended for the Configuration Manager client cache. Less disk space is required if you use customized settings to install the Configuration Manager client:  

    -   Use the CCMSetup command-line property /skipprereq to avoid installing files that the client does not require. For example, **CCMSetup.exe /skipprereq:silverlight.exe** if the client will not use the Application Catalog.  

    -   Use the Client.msi property SMSCACHESIZE to set a cache file that is smaller than the default of 5120 MB. The minimum size is 1 MB. For example, **CCMSetup.exe SMSCachesize=2** creates a cache that is 2 MB in size.  

    For more information about these client installation settings, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    >  Installing the client with minimal disk space is useful for Windows Embedded devices that typically have smaller disk sizes than standard Windows computers.  

 The following are additional minimum hardware requirements for optional functionality in Configuration Manager.  

-   **Operating system deployment:** 384MB of RAM  

-   **Software Center:** 500MHz processor  

-   **Remote Control:** Pentium 4 Hyper-Threaded 3GHz (single core) or comparable CPU, with at least a 1GB RAM for optimal experience  

### Client for Linux and UNIX  
 The following are minimum requirements for Linux and UNIX servers that you manage with Configuration Manager.  

|Requirement|Details|  
|-----------------|-------------|  
|Processor and memory|Refer to the processor and RAM requirements for the computer's operating system.|  
|Disk space|500 MB available disk space, with 5 GB recommended for the Configuration Manager client cache.|  
|Network connectivity|Configuration Manager client computers must have network connectivity to Configuration Manager site systems to enable management.|  

##  <a name="bkmk_ScaleConsole"></a> Configuration Manager console  
 The requirements in the following table apply to each computer that runs Configuration Manager console.  

 **Minimum hardware configuration:**  

-   Intel i3 or comparable CPU  

-   2 GB of RAM  

-   2 GB of disk space.  

|DPI setting|Minimum resolution|  
|-----------------|------------------------|  
|96 / 100%|1024x768|  
|120 /125%|1280x960|  
|144 / 150%|1600x1200|  
|196 / 200%|2500x1600|  

 **Support for PowerShell:**  

 When you install support for PowerShell on a computer that runs the Configuration Manager console, you can run PowerShell cmdlets on that computer to manage Configuration Manager. The following minimum versions are supported:  

-   PowerShell 3.0  

-   PowerShell 4.0  

In addition to PowerShell, Windows Management Framework (WMF) 3.0 and 4.0 are supported.   
You can install PowerShell before or after the Configuration Manager console installs.  

##  <a name="bkmk_ScaleLab"></a> Lab deployments  
 Use the following minimum hardware recommendations for lab and test deployments of Configuration Manager. These  recommendations apply to all site types and for use with up to 100 clients:  

|Role|CPU cores|Memory (GB)|Disk space (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Site and database server|2 - 4|7 - 12|100|  
|Site system server|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
