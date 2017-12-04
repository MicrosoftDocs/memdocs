---
title: "Setup reference"
titleSuffix: "Configuration Manager"
description: "Review this reference to help you prepare to install a Configuration Manager site or hierarchy."
ms.custom: na
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: mestew
ms.author: mstewart
manager: angrobe

---
# Reference for System Center Configuration Manager Setup

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Setup provides links to several topics that are detailed in the following sections. The information presented here can help you prepare  to install a Configuration Manager site or hierarchy, and help prepare you for some of the decisions you must make during the installation.  


##  <a name="bkmk_start"></a> Before you begin  
Before you install new Configuration Manager sites, make sure you have reviewed the following information, which can help set the stage for a successful deployment design:  

-   [Fundamentals of System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Plan for System Center Configuration Manager infrastructure](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Prepare to install System Center Configuration Manager sites](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Assess server readiness  
Before you begin the installation of a new site, make sure that the site server and the remote site system servers you plan to use for the site (for example, the server that hosts the site database) meet all prerequisite configurations. These topics in the documentation library can help:  

-   [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Prerequisite Checker](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clients for additional operating systems  
You can download client software for Configuration Manager from the Microsoft Download Center for the following operating systems:  

-   Mac   (Apple)  
-   UNIX  
-   Linux  

Use the following links to download clients for the version of Configuration Manager you use:  

-   See [Microsoft System Center Configuration Manager - Clients for Additional Operating Systems](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> Usage data levels and settings  
When you install your first System Center Configuration Manager site, Configuration Manager automatically installs and configures a new site system role, the **service connection point**,  on the site server. The service connection point has these default settings:  

-   **Online** mode (an offline mode also is available)  
-   **Enhanced** data collection level (two other data collection levels, Basic and Full, also are available)  

When the service connection point site system role is online, Microsoft can automatically collect diagnostics and usage information over the Internet. Information that is collected helps us:  

-   Identify and troubleshoot problems  
-   Improve our products and service  
-   Identify updates for Configuration Manager that apply to the version of Configuration Manager you use  

### Levels of data collection  
Data collection includes these three levels:

-   **Basic** includes data about setup and upgrade, like the number of sites and which Configuration Manager features are enabled. No personally identifiable information is transmitted.  

-   **Enhanced** includes the data in the Basic level setting, plus it transmits data about the hierarchy, how each feature is used (frequency and duration), and enhanced diagnostic information like the memory state of your server when a system or app crash occurs. No personally identifiable data is transmitted.  

-   **Full** includes the data in the Basic and Enhanced level settings, and it also sends advanced diagnostic information like system files and memory snapshots. This option might include personally identifiable information, but we won't use that information to identify or contact you, or to target advertising to you.  

For more information, including disclosure of the details collected by each level, see [Diagnostics and usage data for System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

To view the System Center Configuration Manager Privacy Statement on-line, go to [http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527).
