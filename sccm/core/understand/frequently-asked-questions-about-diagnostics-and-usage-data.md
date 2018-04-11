---
title: Diagnostic and usage data FAQ
titleSuffix: Configuration Manager
description: Find frequently asked questions about diagnostic and usage data for System Center Configuration Manager.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Frequently asked questions about diagnostics and usage data for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides answers to frequently asked questions about diagnostic and usage data in Configuration Manager.

## FAQs

###  <a name="bkmk_off"></a> How do I turn off telemetry?  
Telemetry can't be turned off. However, you can choose the level of telemetry data that's collected. To help manage when telemetry data is submitted, use the service connection point in offline mode.

The current branch of Configuration Manager needs to be updated on a regular basis to support new versions of Windows 10 and Microsoft Intune. Microsoft requires at least the basic level of diagnostic and usage data. This data is used to keep the product up-to-date, improve the update experience, and improve the quality and security of the product.

###  <a name="bkmk_retention"></a> What is the data retention period?  
 Diagnostic and usage data is stored for one year.  

###  <a name="bkmk_update"></a> Is diagnostics and usage data sent when installing or updating the product?  
 No. Diagnostics and usage data is only sent after the site is installed and operational.  

###  <a name="bkmk_frequency"></a> How frequently is the data sent?  
 The SQL stored procedures run every seven days from the date the site is installed. In online mode, the service connection point is configured to upload the data after the queries run. In offline mode, the administrator uses the service connection tool to upload the data. (The data isn't initially available for offline use until seven days after the site is installed.)  

###  <a name="bkmk_network"></a> Can the data be used to form a network map?  
 As shown in the description of the levels of diagnostic and usage data, site details include time zone information from each site. This information can provide insight into the broad geolocation and global dispersion of sites in a hierarchy. This data doesn't include any network details, such as IP addresses or more detailed geographic information. For more information, see the list of [diagnostics and usage data articles](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles), and find the levels of diagnostic and usage data collection for the version you're using.


###  <a name="bkmk_tables"></a> Can you see data in custom tables?  
 No. Configuration Manager collects diagnostics and usage data via SQL stored procedures. These stored procedures run against default product tables in the database. All of these SQL tables are prefixed with **TEL_**. As part of the SQL schema detection query, all table names are hashed for comparison against the known defaults. This behavior determines that custom tables exist in the database. The presence of custom tables informs that the database schema is extended from the default. It doesn't include any of the data stored within those tables.  

###  <a name="bkmk_databases"></a> Can you see names of other databases, or can you see data in other databases? 
 No. The stored procedures to collect data are limited to the site database.  

### <a name="bkmk_gdpr"></a> Is Configuration Manager subject to the General Data Protection Regulation (GDPR)?
 No. Configuration Manager isn't subject to GDPR oversight. It is an on-premises product that you directly deploy, manage, and operate. The diagnostics and usage data that Microsoft collects improves the installation experience, quality, and security of future releases. This data is subject to GDPR oversight. No end-user identification information (EUII) or end-user pseudonymous identifiers (EUPI) are collected and transmitted to Microsoft. For more information about GDPR, see the [Microsoft Trust Center on GDPR](https://microsoft.com/gdpr). For more information about Configuration Manager data, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## See also  
 [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
