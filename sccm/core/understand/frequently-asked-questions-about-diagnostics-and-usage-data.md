---
title: "Diagnostic data FAQ"
titleSuffix: "Configuration Manager"
description: "Find frequently asked questions about diagnostic and usage data for System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Frequently asked questions about diagnostics and usage data for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The following are frequently asked questions about diagnostic and usage data for System Center Configuration Manager:  

###  <a name="bkmk_off"></a> How do I turn off telemetry?  
Telemetry cannot be turned off. However, you can choose the level of telemetry data that's collected. You can also use a service connection point in offline mode to help manage when telemetry data is submitted.

The current branch of Configuration Manager needs to be updated on a regular basis to support new versions of Windows 10 and Microsoft Intune. Microsoft requires at least the basic level of diagnostic and usage data to keep the product up to date, improve the update experience, and improve the quality and security of the product.

###  <a name="bkmk_retention"></a> What is the data retention period?  
 Diagnostic and usage data is retained for one year.  

###  <a name="bkmk_update"></a> Is diagnostics and usage data sent when installing or updating the product?  
 No. Diagnostics and usage data is only sent after the site is installed and operational.  

###  <a name="bkmk_frequency"></a> How frequently is the data sent?  
 The SQL stored procedures run every seven days (from the date the site is installed). In online mode, the service connection point is configured to upload the data after the queries run. In offline mode, the administrator uses the service connection tool to upload the data. (Note that the data is not initially available for offline use until seven days after the site is installed.)  

###  <a name="bkmk_network"></a> Can the data be used to form a network map?  
 As shown in the description of the levels of diagnostic usage data collection for System Center Configuration Manager, site details include time zone information from each site. This information can provide insight into the broad geolocation and global dispersion of sites in a hierarchy. However, no network details are collected, (such IP addresses or more detailed geographic information).
 - [Diagnostic data for 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Diagnostic data for 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Diagnostic data for 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> Can you see data in custom tables?  
 No. Diagnostics and usage data is collected via SQL stored procedures against default product tables in the database (all of which are prefixed with **TEL_** ). As part of the SQL schema detection query, all table names are hashed for comparison against the known defaults. This can determine that custom tables exist in the database (that the database schema is extended from the default) but not any of the data contained within those tables.  

###  <a name="bkmk_databases"></a> Can you see names of other databases, or can you see data in other databases?  
 No. The stored procedures to collect data are limited to the site database.  

## See also  
 [Diagnostics and usage data for System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)
