---
title: "Setup reference"
titleSuffix: "Configuration Manager"
description: "Review this reference to help you prepare to install a Configuration Manager site or hierarchy."
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby


---
# Reference for Configuration Manager Setup

*Applies to: Configuration Manager (current branch)*

Configuration Manager Setup provides links to several topics that are detailed in the following sections. The information presented here can help you prepare  to install a Configuration Manager site or hierarchy, and help prepare you for some of the decisions you must make during the installation.  


##  <a name="bkmk_start"></a> Before you begin  
Before you install new Configuration Manager sites, make sure you have reviewed the following information, which can help set the stage for a successful deployment design:  

-   [Fundamentals of Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Plan for Configuration Manager infrastructure](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Prepare to install Configuration Manager sites](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Assess server readiness  
Before you begin the installation of a new site, make sure that the site server and the remote site system servers you plan to use for the site (for example, the server that hosts the site database) meet all prerequisite configurations. These topics in the documentation library can help:  

-   [Supported configurations for Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Prerequisite Checker](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clients for additional operating systems  
You can download client software for Configuration Manager from the Microsoft Download Center for the following operating systems:  

- macOS (Apple)
- UNIX
- Linux

Use the following links to download clients for the version of Configuration Manager you use:  

- [Microsoft Endpoint Configuration Manager - macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Microsoft Configuration Manager clients for additional operating systems](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="bkmk_usage"></a> Usage data levels and settings  
When you install your first Configuration Manager site, Configuration Manager automatically installs and configures a new site system role, the **service connection point**,  on the site server. The service connection point has these default settings:  

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

For more information, including disclosure of the details collected by each level, see [Diagnostics and usage data for Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

To view the Configuration Manager Privacy Statement on-line, go to [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527).
