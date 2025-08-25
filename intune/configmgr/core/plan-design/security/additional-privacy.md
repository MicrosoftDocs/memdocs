---
title: Additional privacy information
titleSuffix: Configuration Manager
description: Learn about how Microsoft collects and uses data from Configuration Manager.
ms.date: 09/04/2018
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection:
    - tier3
    - essentials-privacy
ms.reviewer: mstewart
---

# Additional information about privacy for Configuration Manager

*Applies to: Configuration Manager (current branch)*


## Updates and servicing

Configuration Manager uses an update model that helps keep your environment current with the latest updates and features. This feature uses a site system role called the service connection point. You choose the server where to install this role.

For more information about collected information and how it's used, see [Usage data](#usage-data).



## Usage data

Configuration Manager collects diagnostics and usage data about itself, which Microsoft uses to improve the installation experience, quality, and security of future releases.
Diagnostics and usage data is enabled for each Configuration Manager hierarchy. It consists of SQL Server queries that run on a weekly basis on each primary site and at the central administration site. When the hierarchy uses a central administration site, the data from primary sites is then replicated to that site. At the top-level site of your hierarchy, the service connection point submits this information when it checks for updates. If the service connection point is in offline mode, the information is transferred by using the service connection tool.

Configuration Manager collects data only from the site's SQL Server database, and it doesn't collect data directly from clients or site servers.

Administrators can change the level of data that's collected by going to the **Usage Data** section of the Configuration Manager console.

For more information about usage data levels and settings, see [Diagnostics and usage data](../diagnostics/diagnostics-and-usage-data.md).


## Endpoint Protection

Microsoft Cloud Protection Service was formerly known as Microsoft Active Protection Service or MAPS.

The applicable products are System Center Endpoint Protection and the Endpoint Protection feature of Configuration Manager (to manage System Center Endpoint Protection and Windows Defender for Windows 10 or later).

The Microsoft Cloud Protection Service antimalware community is a voluntary worldwide online community that includes System Center Endpoint Protection users. When you join Microsoft Cloud Protection Service, System Center Endpoint Protection automatically sends information to Microsoft. Microsoft uses the information to determine software to investigate for potential threats and to help improve the effectiveness of System Center Endpoint Protection. This community helps stop the spread of new malicious software infections. If a Microsoft Cloud Protection Service report includes details about malware or potentially unwanted software that the Endpoint Protection client may be able to remove, Microsoft Cloud Protection Service downloads the latest signature to address it. Microsoft Cloud Protection Service can also find "false positives" and fix them. (False positives are where something originally identified as malware turns out not to be.)

Microsoft Cloud Protection Service reports include information about potential malware files, like file names, cryptographic hash, vendor, size, and date stamps. In addition, Microsoft Cloud Protection Service might collect full URLs to indicate the origin of the file. These URLs might occasionally have personal information like search terms or data that was entered in forms. Reports might also include actions that you took when Endpoint Protection notified you about unwanted software. Microsoft Cloud Protection Service reports include this information to help Microsoft gauge how effectively Endpoint Protection can detect and remove malware and potentially unwanted software and to attempt to identify new malware.

You can join Microsoft Cloud Protection Service if you have a basic or advanced membership. Basic member reports have the information described previously. Advanced member reports are more comprehensive and may include additional details about the software that Endpoint Protection detects, like the location of such software, file names, how the software operates, and how it has affected your computer. These reports and reports from other Endpoint Protection users who participate in Microsoft Cloud Protection Service help Microsoft researchers discover new threats more rapidly. Malware definitions are then created for programs that meet the analysis criteria, and the updated definitions are made available to all users through Microsoft Update.

To help detect and fix certain kinds of malware infections, the product regularly sends Microsoft Cloud Protection Service information about the security state of your PC. This information includes information about your PC's security settings and log files that describe the drivers and other software that load while your PC boots.

A number that uniquely identifies your PC is also sent. Also, Microsoft Cloud Protection Service may collect the IP addresses that the potential malware files connect to.

Microsoft Cloud Protection Service reports are used to improve Microsoft software and services. The reports might also be used for statistical or other testing or analytical purposes and to generate definitions. Only Microsoft employees, contractors, partners, and vendors who have a business need to use the reports can access them.

Microsoft Cloud Protection Service does not intentionally collect personal information. To the extent that Microsoft Cloud Protection Service collects any personal information, Microsoft does not use the information to identify you or contact you.

For more information, see [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).
