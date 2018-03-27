---
title: Privacy statement - additional information
titleSuffix: Configuration Manager
description: Learn about how Microsoft collects and uses data from System Center Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: 5
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Additional information about privacy for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


## Updates and servicing
System Center Configuration Manager introduces a new update model that helps keep your Configuration Manager deployment current with the latest updates and features. When installed, this feature adds a new site system role that's called the service connection point on a site server that an admin chooses. For details about collected information and how it is used, see the Usage data section in this article.


## Usage data
System Center Configuration Manager collects diagnostics and usage data about itself, which Microsoft uses to improve the installation experience, quality, and security of future releases.
Diagnostics and Usage Data is enabled for each System Center Configuration Manager hierarchy. It consists of SQL Server queries that run on a weekly basis on each primary site and at the central administration site. When the hierarchy uses a central administration site, the data from primary sites is then replicated to that site. At the top-level site of your hierarchy, the service connection point submits this information when it checks for updates. If the service connection point is in offline mode, the information is transferred by using the service connection tool.

Configuration Manager collects data only from the site's SQL server database, and it does not collect data directly from clients or site servers.

Admins can change the level of data that's collected by going to the **Usage Data** section of the Configuration Manager console.

For more information, see the "Learn more" articles about usage data levels and settings in the [Diagnostics and usage data for System Center Configuration Manager](https://go.microsoft.com/fwlink/?LinkID=626566) article.


## Customer Experience Improvement Program

> [!Note]  
> Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

The Customer Experience Improvement Program (CEIP) collects basic information from the Configuration Manager console about your hardware configuration and how you use our software and services to identify trends and usage patterns. CEIP also collects the type and number of errors that you encounter, software and hardware performance, and the speed of services. We do not collect your name, address, or other contact information. No CEIP data is collected from client computers.

We use this information to improve the quality, reliability, and performance of Microsoft software and services.

For more about the information that's collected, processed, or transmitted by CEIP, see the [CEIP privacy statement](https://go.microsoft.com/fwlink/?LinkID=525211).

## Operations Management Suite Connector
The Microsoft Operations Management Suite Connector syncs data, such as collections, from System Center Configuration Manager to Microsoft Operations Management Suite. The Microsoft Azure subscription ID and secret key are stored in the Configuration Manager database when an admin configures the feature. Both the Azure Active Directory client secret and the Microsoft Operations Management Suite workspace shared key are stored in the on-premises System Center Configuration Manager database. All communications between System Center Configuration Manager and Microsoft Operations Management Suite use HTTPS. No additional information about the collections is provided to Microsoft outside of randomized telemetry data. For details about the information that Microsoft Operations Management Suite collects, see [Log analytics security](https://go.microsoft.com/fwlink/?LinkId=823545).

## Asset Intelligence
Asset Intelligence lets IT admins define, track, and proactively manage conformity with configuration standards. Metering and reporting on the deployment and use of both physical and virtual applications helps organizations make better business decisions about software licensing and maintain compliance with licensing agreements. After collecting usage data from Configuration Manager clients, admins can use different features to view the data, including collections, queries, and reporting.

During each synchronization, a catalog of known software is downloaded from Microsoft. IT admins can choose to send Microsoft information about uncategorized software titles that are discovered within their organizations to be researched and added to the catalog. Prior to uploading this information, a dialog box shows data that is going to be uploaded. Uploaded data cannot be recalled. Asset Intelligence does not send information about users and computers or license usage to Microsoft.

After a software title is uploaded, Microsoft researchers identify, categorize, and then make that knowledge available to all other customers who use this feature and other consumers of the catalog. Any uploaded software title becomes public. The application and its categorization become part of the catalog and then can be downloaded to other consumers of the catalog. Before you configure Asset Intelligence data collection and decide whether to submit information to Microsoft, consider the privacy requirements of your organization.

Asset Intelligence is not enabled in System Center Configuration Manager by default. Uploading of uncategorized titles never occurs automatically, and the system is not designed for this task to be automated. You must manually select and approve the upload of each software title.

## Endpoint Protection
Microsoft Cloud Protection Service was formerly known as Microsoft Active Protection Service or MAPS.
The applicable products are System Center Endpoint Protection and the Endpoint Protection feature of System Center Configuration Manager (to manage System Center Endpoint Protection and Windows Defender for Windows 10). This feature is not implemented for System Center Endpoint Protection for Linux or System Center Endpoint Protection for Mac.

The Microsoft Cloud Protection Service antimalware community is a voluntary worldwide online community that includes System Center Endpoint Protection users. When you join Microsoft Cloud Protection Service, System Center Endpoint Protection automatically sends information to Microsoft. Microsoft uses the information to determine software to investigate for potential threats and to help improve the effectiveness of System Center Endpoint Protection. This community helps stop the spread of new malicious software infections. If a Microsoft Cloud Protection Service report includes details about malware or potentially unwanted software that the Endpoint Protection client may be able to remove, Microsoft Cloud Protection Service downloads the latest signature to address it. Microsoft Cloud Protection Service can also find "false positives" (where something originally identified as malware turns out not to be) and fix them.

Microsoft Cloud Protection Service reports include information about potential malware files, like file names, cryptographic hash, vendor, size, and date stamps. In addition, Microsoft Cloud Protection Service might collect full URLs to indicate the origin of the file. These URLs might occasionally have personal information like search terms or data that was entered in forms. Reports might also include actions that you took when Endpoint Protection notified you about unwanted software. Microsoft Cloud Protection Service reports include this information to help Microsoft gauge how effectively Endpoint Protection can detect and remove malware and potentially unwanted software and to attempt to identify new malware.

You can join Microsoft Cloud Protection Service if you have a basic or advanced membership. Basic member reports have the information described previously. Advanced member reports are more comprehensive and may include additional details about the software that Endpoint Protection detects, like the location of such software, file names, how the software operates, and how it has affected your computer. These reports and reports from other Endpoint Protection users who participate in Microsoft Cloud Protection Service help Microsoft researchers discover new threats more rapidly. Malware definitions are then created for programs that meet the analysis criteria, and the updated definitions are made available to all users through Microsoft Update.

To help detect and fix certain kinds of malware infections, the product regularly sends Microsoft Cloud Protection Service information about the security state of your PC. This information includes information about your PC's security settings and log files that describe the drivers and other software that load while your PC boots.
A number that uniquely identifies your PC is also sent. Also, Microsoft Cloud Protection Service may collect the IP addresses that the potential malware files connect to.

Microsoft Cloud Protection Service reports are used to improve Microsoft software and services. The reports might also be used for statistical or other testing or analytical purposes and to generate definitions. Only Microsoft employees, contractors, partners, and vendors who have a business need to use the reports can access them.

Microsoft Cloud Protection Service does not intentionally collect personal information. To the extent that Microsoft Cloud Protection Service collects any personal information, Microsoft does not use the information to identify you or contact you.

Additional details about collected data can be found in the product documentation at [Endpoint Protection in System Center Configuration Manager](https://go.microsoft.com/fwlink/?LinkId=823547).

## Site Hierarchy – Geographical View with Bing Maps
Site Hierarchy - Geographical View lets you use maps that Microsoft Bing Maps provides to view your Configuration Manager physical server topology. To enable this feature, location information that you provide is sent from your server to the Bing Maps Web service.

Microsoft uses the information to operate and improve Microsoft Bing Maps and other Microsoft sites and services. For more information, see the [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=823548).
You can choose not to use the Geographical View for the Site Hierarchy. The Hierarchy Diagram view lets you see the hierarchy and does not use the Bing Maps service.

## Microsoft Intune subscription
Customers who bought a subscription to Microsoft Intune can use Configuration Manager to manage their mobile devices that are connected through Microsoft Intune. [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=262214) applies to the Microsoft online services, which includes Microsoft Intune. If customers also have a Microsoft Intune subscription, the [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=262214) should be read in conjunction with this privacy statement.

All communications with Microsoft Intune use HTTPS. To configure the Microsoft Intune subscription and to download the Certificate Signing Request (CSR) that's needed to configure iOS support, an admin must sign in to Microsoft Intune by using work account and password. These credentials are not stored within Configuration Manager. All other communications with Microsoft Intune are authenticated by using PKI certificates that Microsoft Intune automatically generates.

To manage devices that are connected to Microsoft Intune, some information is sent to and received from Microsoft Intune. This information includes the User Principal Name (UPN) of all users who are assigned to the service and device inventory information for those devices that are managed by Microsoft Intune. Metadata, like application name, publisher, and version, for content that is assigned to Manage.Microsoft.com distribution points is sent to Microsoft Intune. The actual binary content that's assigned to a Manage.Microsoft.com distribution point is encrypted before it is uploaded to Microsoft Intune.

This feature is not configured by default. Admins control the content that is transferred to the Manage.Microsoft.com distribution point and the users who are assigned to the service. The feature can be removed at any time.
