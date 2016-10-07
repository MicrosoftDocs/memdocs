---
title: "Setup reference | System Center Configuration Manager"
description: "Review this reference to help you prepare to install a Configuration Manager site or hierarchy."
ms.custom: na
ms.date: 01/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brendunsms.author: brendunsmanager: angrobe

---
# Reference for System Center Configuration Manager Setup
System Center Configuration Manager Setup provides links to several topics where are detailed in the following sections. The information in the following sections can help you prepare  to install a Configuration Manager site or hierarchy, and help prepare you for some of the decisions you must make during the installation:  

-   [Before you begin](#bkmk_start)  

-   [Assess server readiness](#bkmk_assess)  

-   [Clients for additional operating systems](#bkmk_Addclients)  

-   [Diagnostics and usage data for System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="bkmk_start"></a> Before you begin  
 Before installing new Configuration Manager sites, ensure you have reviewed the following information which can help set the stage for a successful deployment design:  

-   [Fundamentals of System Center Configuration Manager](../../../../core/understand/fundamentals.md)  

-   [Plan for System Center Configuration Manager infrastructure](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [Prepare to install System Center Configuration Manager sites](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Assess server readiness  
 Before beginning the installation of a new site, ensure the site server and remote site system servers you plan to use for the site (like the server that host the site database) meet all  prerequisite configurations. The following topics in the documentation library can help:  

-   [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  

-   [Prerequisite Checker](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="bkmk_Addclients"></a> Clients for additional operating systems  
 You can download client software for Configuration Manager from the Microsoft download center for the following operating systems:  

-   Mac   (Apple)  

-   UNIX  

-   Linux  

**Use the following links to download clients for the version of Configuration Manager you use:**  

-   [System Center Configuration Manager (current branch)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 and System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="bkmk_usage"></a> Usage data levels and settings  
When you install your first System Center Configuration Manager site, it automatically installs and configures a new site system role on the site server, the **service connection point** with the following default settings:  

-   **Online** mode   (an offline mode is also supported)  

-   A data collection level of **Enhanced** (two other data collection levels, Basic and Full, are supported)  

When this role is online, it enables Microsoft to automatically collect diagnostics and usage information over the Internet. Information that is collected helps us:  

-   Identify and troubleshoot problems  

-   Improve our products and service  

-   Identify updates for Configuration Manager that apply to the version of Configuration Manager you use  

The three levels of data collection include:  

-   **Basic** includes data about setup and upgrade like the number of sites and which Configuration Manager features are enabled. No personally identifiable information will be transmitted.  

-   **Enhanced** includes the data in the Basic setting plus transmits data about the hierarchy, how each feature is used (frequency and duration), and enhanced diagnostic information like the memory state of your server when a system or app crash occurs. No personally identifiable data will be transmitted.  

-   **Full** includes the data in the Basic and Enhanced settings and also sends advanced diagnostic information like system files and memory snapshots. This option may include personally identifiable information, but we won't use that information to identify or contact you, or target advertising to you.  

For more information including disclosure of the details collected by each level, see [Diagnostics and usage data for System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

[System Center Configuration Manager Privacy Statement](http://go.microsoft.com/fwlink/?LinkID=626527)
