---
title: "System Center Configuration Manager privacy statement - Configuration Manager Cmdlet Library"
description: "Learn about how Microsoft collects and uses data from a System Center Configuration Manager deployment."
ms.custom: na
ms.date: 09/19/2016
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
author: Brendunsmanager: angrobe
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
# Additional information about Privacy for System Center Configuration Manager

## Updates and Servicing
System Center Configuration Manager introduces a new update model that helps keep your Configuration Manager deployment current with the latest updates and features. When installed, this feature adds a new site system role on a site server that administrator chooses called the service connection point. For details about what information is collected and how it is used, see the Usage Data section of this statement.


## Usage Data
System Center Configuration Manager collects diagnostics and usage data about itself which is used by Microsoft to improve the installation experience, quality, and security of future releases.
Diagnostics and Usage Data is enabled for each System Center Configuration Manager hierarchy. It consists of SQL Server queries that run on a weekly basis on each primary site and at central administration site. When the hierarchy uses a central administration site, the data from primary sites is then replicated to that site. At the top-level site of your hierarchy, the service connection point submits this information when it checks for updates. If the service connection point is in offline mode, the information is transferred by using the service connection tool.

Configuration Manager only collects data from the sites SQL server database, and does not collect data directly from clients or site servers.

Administrators can change the level of data collected by going to the "Usage Data" section of the Configuration Manager console.

For more information, see the "Learn More" article about Usage Data Levels and Settings at [http://go.microsoft.com/fwlink/?LinkID=626566](http://go.microsoft.com/fwlink/?LinkID=626566).


## Customer Experience Improvement Program
The Customer Experience Improvement Program ("CEIP") collects basic information from the Configuration Manager console about your hardware configuration and how you use our software and services in order to identify trends and usage patterns. CEIP also collects the type and number of errors you encounter, software and hardware performance, and the speed of services.  We will not collect your name, address, or other contact information. No CEIP data is collected from client computers.

We use this information to improve the quality, reliability, and performance of Microsoft software and services.

For more information about the information collected, processed, or transmitted by CEIP, see the CEIP privacy statement at [http://go.microsoft.com/fwlink/?LinkID=525211](http://go.microsoft.com/fwlink/?LinkID=525211).

## OMS Connector
The Microsoft Operations Management Suite Connector syncs data such as collections from System Center Configuration Manager to Microsoft Operations Management Suite. The Microsoft Azure subscription ID and secret key are stored in the Configuration Manager database when an administrator configures the feature. Both the Azure Active Directory client secret and the Microsoft Operations Management Suite workspace shared key are stored in the on-premise System Center Configuration Manager database. All communications between System Center Configuration Manager and Microsoft Operations Management Suite use HTTPS. No additional information about the collections are provided to Microsoft outside of randomized telemetry data. For details about what information is collected by Microsoft Operations Management Suite, see more about log analytics data security at [http://go.microsoft.com/fwlink/?LinkId=823545](http://go.microsoft.com/fwlink/?LinkId=823545).

## Asset Intelligence
Asset Intelligence lets IT administrators define, track, and proactively manage conformity with configuration standards. Metering and reporting on the deployment and use of both physical and virtual applications helps organizations make better business decisions about software licensing and maintain compliance with licensing agreements. After collecting usage data from Configuration Manager clients, administrators can use different features to view the data, including collections, queries, and reporting.

During each synchronization, a catalog of known software will be downloaded from Microsoft. The IT administrator can choose to send Microsoft information about uncategorized software titles discovered within their organization to be researched and added to the catalog. Prior to uploading this information, a dialog box shows exactly what data is going to be uploaded. Uploaded data cannot be recalled. Asset Intelligence does not send information about users and computers or license usage to Microsoft.

After a software title is uploaded, Microsoft researchers identify, categorize, and then make that knowledge available to all other customers that use this feature and other consumers of the catalog. Any software title uploaded becomes public, in the sense that the knowledge of that given application and its categorization become part of the catalog, and then can be downloaded to other consumers of the catalog. Before you configure Asset Intelligence data collection and decide whether to submit information to Microsoft, consider the privacy requirements of your organization.

Asset Intelligence is not enabled in System Center Configuration Manager by default. Uploading of uncategorized titles never occurs automatically, and the system is not designed for this task to be automated. You must manually select and approve the upload of each software title.

## Endpoint Protection
Microsoft Cloud Protection Service (formerly known as Microsoft Active Protection Service or MAPS)
Applicable products: System Center Endpoint Protection and the Endpoint Protection feature of System Center Configuration Manager (for managing System Center Endpoint Protection and Windows Defender for Windows 10). This feature is not implemented for System Center Endpoint Protection for Linux or System Center Endpoint Protection for Mac.

The Microsoft Cloud Protection Service antimalware community is a voluntary worldwide online community that includes System Center Endpoint Protection users. By joining Microsoft Cloud Protection Service, System Center Endpoint Protection will automatically send information to Microsoft to help Microsoft determine which software to investigate for potential threats and to help improve System Center Endpoint Protection's effectiveness. This community helps stop the spread of new malicious software infections. If a Microsoft Cloud Protection Service report includes details about malware or potentially unwanted software that the Endpoint Protection client may be able to remove, Microsoft Cloud Protection Service will download the latest signature to address it. Microsoft Cloud Protection Service can also find "false positives" (where something originally identified as malware turns out not to be) and fix them.

Microsoft Cloud Protection Service reports include information about potential malware files, such as file names, cryptographic hash, vendor, size, and date stamps. In addition, Microsoft Cloud Protection Service might collect full URLs to indicate the origin of the file. These URLs might occasionally contain personal information such as search terms or data entered in forms. Reports might also include the actions you took when Endpoint Protection notified you about unwanted software. Microsoft Cloud Protection Service reports include this information to help Microsoft gauge how effectively Endpoint Protection can detect and remove malware and potentially unwanted software and to attempt to identify new malware.

Microsoft Cloud Protection Service can be joined with a basic or an advanced membership. Basic member reports contain the information described above. Advanced member reports are more comprehensive and may include additional details about the software Endpoint Protection detects, including the location of such software, file names, how the software operates, and how it has impacted your computer. These reports, along with reports from other Endpoint Protection users who are participating in Microsoft Cloud Protection Service, help Microsoft researchers discover new threats more rapidly. Malware definitions are then created for programs that meet the analysis criteria, and the updated definitions are made available to all users through Microsoft Update.

To help detect and fix certain kinds of malware infections, the product regularly sends Microsoft Cloud Protection Service some information about the security state of your PC. This information includes information about your PC's security settings and log files describing the drivers and other software that load while your PC boots.
A number that uniquely identifies your PC is also sent. Also, Microsoft Cloud Protection Service may collect the IP addresses that the potential malware files connect to.

Microsoft Cloud Protection Service reports are used to improve Microsoft software and services. The reports might also be used for statistical or other testing or analytical purposes, and for generating definitions. Only Microsoft employees, contractors, partners, and vendors who have a business need to use the reports are provided access to them.

Microsoft Cloud Protection Service does not intentionally collect personal information. To the extent that Microsoft Cloud Protection Service collects any personal information, Microsoft does not use the information to identify you or contact you.

Additional details regarding data collected can be found in the product documentation at [http://go.microsoft.com/fwlink/?LinkId=823547](http://go.microsoft.com/fwlink/?LinkId=823547).

## Site Hierarchy – Geographical View with Bing Maps
Site Hierarchy - geographical view allows you to view your Configuration Manager physical server topology using maps provided by Microsoft Bing Maps. To enable this feature, location information you provide is sent from your server to the Bing Maps Web service.

Microsoft uses the information to operate and improve Microsoft Bing Maps and other Microsoft sites and services. For more information, see the Microsoft Privacy Statement at http://go.microsoft.com/fwlink/?LinkId=823548.
You can choose not to use the Geographical View for the Site Hierarchy. The Hierarchy Diagram view allows you to see the hierarchy and does not use the Bing Maps service.

## Microsoft Intune Subscription
Customers who have purchased a subscription to Microsoft Intune can use Configuration Manager to manage their mobile devices that connected through Microsoft Intune. [Microsoft Online Services Privacy Statement](http://go.microsoft.com/fwlink/?LinkId=262214) applies to the Microsoft online services, including Microsoft Intune. If customers also have a Microsoft Intune subscription, the [Microsoft Online Services Privacy Statement](http://go.microsoft.com/fwlink/?LinkId=262214) should be read in conjunction with this privacy statement.

All communications with Microsoft Intune use HTTPS. To configure the Microsoft Intune subscription and to download the Certificate Signing Request (CSR) needed for configuration of iOS support, an administrator must sign in to Microsoft Intune by using their organizational account and password. These credentials are not stored within Configuration Manager. All other communications with Microsoft Intune are authenticated by using PKI certificates that are automatically generated by Microsoft Intune.

In order to manage devices that are connected to Microsoft Intune, some information is sent to and received from Microsoft Intune. This information includes the User Principal Name (UPN) of all users that are assigned to the service and device inventory information for those devices that are managed by Microsoft Intune. Metadata, such as application name, publisher, and version, for content that is assigned to Manage.Microsoft.com distribution points is sent to Microsoft Intune. The actual binary content assigned to a Manage.Microsoft.com distribution point is encrypted before it is uploaded to Microsoft Intune.

This feature is not configured by default. Administrators have control over what content is transferred to the Manage.Microsoft.com distribution point and which users are assigned to the service. The feature can be removed at any time.
