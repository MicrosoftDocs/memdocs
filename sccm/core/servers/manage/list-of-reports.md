---
title: "List of reports"
titleSuffix: "Configuration Manager"
description: "Review a list of reports that are supplied with Configuration Manager. The reports appear in various categories."
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
caps.latest.revision: 10
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# List of reports in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager supplies many built-in reports covering many of the reporting tasks that you might want to perform. You can also use the SQL statements in these reports to help you to write your own reports.   

The following reports are included with Configuration Manager. The reports appear in various categories.  



## Administrative Security  
 The following reports are listed under the **Administrative Security** category.  

|Report name|Description|  
|-----------------|-----------------|  
|**Administration activity log**|Displays a record of administrative changes made for administrative users, security roles, security scopes, and collections.|  
|**Administrative users security assignments**|Displays administrative users, their associated security roles, and the security scopes associated with each security role for each user.|  
|**Objects secured by a single security scope**|Displays objects that an administrator assigned to only the specified security scope. This report does not display objects that an administrator associates with more than one security scope.|  
|**Security for a specific or multiple Configuration Manager objects**|Displays securable objects, the security scopes associated with the objects, and which administrative users have rights to the objects.|  
|**Security roles summary**|Displays security roles and the Configuration Manager administrators associated with each role.|  
|**Security scopes summary**|Displays security scopes and the Configuration Manager administrative users and security groups associated with each scope.|  



## Alerts  

|Report name|Description|  
|-----------------|-----------------|  
|**Alert scorecard**|Displays a summary of all postponed alerts that were generated between the specified start and finish date.|  
|**Alerts Generated Most Often**|Displays a summary of the alerts that were generated most often from today back to the specified date for the specified feature area.|  



## Asset Intelligence  

|Report name|Description|  
|-----------------|-----------------|  
|**Hardware 01A - Summary of computers in a specific collection**|Displays an Asset Intelligence summary view of computers in a collection you specify.|  
|**Hardware 03A - Primary computer users**|Displays users and the count of computers on which they are the primary user.|  
|**Hardware 03B - Computers for a specific primary console user**|Displays all computers for which a specified user is the primary console user.|  
|**Hardware 04A - Computers with multiple users (shared)**|Displays computers that do not have a primary user because no one user has a % console login time greater than 66%.|  
|**Hardware 05A - Console users on a specific computer**|Displays all of the console users on a specified computer.|  
|**Hardware 06A - Computers for which console users could not be determined**|Helps administrative users identify computers that need to have security logging turned on.|  
|**Hardware 07A - USB devices by manufacturer**|Displays USB devices, grouped by manufacturer.|  
|**Hardware 07B - USB devices by manufacturer and description**|Displays USB devices, grouped by manufacturer and description.|  
|**Hardware 07C - Computers with a specific USB device**|Displays all the computers with a specified USB device.|  
|**Hardware 07D - USB devices on a specific computer**|Displays all USB devices on a specified computer.|  
|**Hardware 08A - Hardware that is not ready for a software upgrade**|Displays hardware that does not meet the minimum hardware requirements.|  
|**Hardware 09A - Search for computers**|Displays a summary of computers matching keyword filters. These filters are computer name, Configuration Manager site, domain, top console user, operating system, manufacturer, or model.|  
|**Hardware 10A - Computers in a specified collection that have changed during a specified timeframe**|Displays a list of computers in a specified collection where a hardware class has changed during a specified time period.|  
|**Hardware 10B - Changes on a specified computer within a specified timeframe**|Displays the classes that have changed on a specified computer within a specified time period.|  
|**License 01A - Microsoft Volume License ledger for Microsoft license statements**|Displays an inventory of all Microsoft software titles that are available from the Microsoft Volume Licensing program.|  
|**License 01B - Microsoft Volume License ledger item by sales channel**|Identifies and displays sales channel for inventoried Microsoft Volume License software.|  
|**License 01C - Computers with a specific Microsoft Volume License ledger item and sales channel**|Identifies and displays computers that have a specified item from the Microsoft Volume license ledger.|  
|**License 01D - Microsoft Volume License ledger products on a specific computer**|Identifies and displays all Microsoft Volume license ledger items on a specified computer.|  
|**License 02A - Count of licenses nearing expiration by time ranges**|Displays a count of licenses nearing expiration by a specified time range. The displayed products have their licenses managed by the Software Licensing Service.|  
|**License 02B - Computers with licenses nearing expiration**|Displays the specified computers with licenses that are nearing expiration.|  
|**License 02C - License information on a specific computer**|Displays products on a specified computer that have their licenses managed by the Software Licensing Service.|  
|**License 03A - Count of licenses by license status**|Displays products, by license status, which have their licenses managed by the Software Licensing Service.|  
|**License 03B - Computers with a specific license status**|Displays products, with a specified license status, whose licenses are managed by the Software Licensing Service.|  
|**License 04A - Count of products managed by software licensing**|Displays a count of products that have their licenses managed by the Software Licensing Service.|  
|**License 04B - Computers with a specific product managed by Software Licensing Service**|Displays computers, managed by the Software Licensing Service, that contain a specified product.|  
|**License 05A - Computers providing Key Management Service**|Displays computers that act as Key Management Servers.|  
|**License 06A - Processor counts for per-processor licensed products**|Displays the number of processors on computers using Microsoft products that support per-processor licensing.|  
|**License 06B - Computers with a specific product that supports per-processor licensing**|Displays a list of computers where a specified Microsoft product that supports per-processor licensing is installed.|  
|**License 14A - Microsoft Volume Licensing reconciliation report**|Displays reconciliation on software licenses purchased through Microsoft Volume License Agreement and the actual inventory count.|  
|**License 14B - List of Microsoft software inventory not found in MVLS**|This report displays Microsoft software titles in use that are not found in the Microsoft Volume License Agreement.|  
|**License 15A - General license reconciliation report**|Displays reconciliation on general software licenses purchased and the actual inventory count.|  
|**License 15B - General license reconciliation report by computer**|Displays computers that installed the licensed product with a specified version.|  
|**Software 01A - Summary of installed software in a specific collection**|Displays a summary of installed software ordered by the number of instances found from inventory.|  
|**Software 02A - Product families for a specific collection**|Displays the product families and the count of software in the family for a specified collection.|  
|**Software 02B - Product categories for a specific product family**|Displays the product categories in a specified product family and the count of software within the category.|  
|**Software 02C - Software in a specific product family and category**|Displays all software that is in the specified product family and category.|  
|**Software 02D - Computers with specific software installed**|Displays all computers with specified software installed.|  
|**Software 02E - Installed software on a specific computer**|Displays all software installed on a specified computer.|  
|**Software 03A - Uncategorized software**|Displays the software that is either categorized as unknown or has no categorization.|  
|**Software 04A - Software configured to automatically run on computers**|Displays a list of software configured to automatically run on computers.|  
|**Software 04B - Computers with specific software configured to automatically run**|Displays all computers with specified software configured to automatically run.|  
|**Software 04C - Software configured to automatically run on a specific computer**|Displays installed software configured to automatically run on a specified computer.|  
|**Software 05A - Browser Helper Objects**|Displays the browser helper objects installed on computers in a specified collection.|  
|**Software 05B - Computers with a specific Browser Helper Object**|Displays all of the computers with a specified browser helper object.|  
|**Software 05C - Browser Helper Objects on a specific computer**|Displays all browser helper objects on the specified computer.|  
|**Software 06A - Search for installed software**|This report provides a summary of installed software. It searches based on the following criteria: product name, publisher, or version.|  
|**Software 06B - Software by product name**|Displays a summary of installed software based on a specified product name.|  
|**Software 07A - Recently used executable programs by the count of computers**|Displays executable programs that users recently used. It also includes the count of computers on which users used the program. Software metering must be enabled for this site to view this report.|  
|**Software 07B - Computers that recently used a specified executable program**|Displays the computers on which users recently used a specified executable program. This report requires that you enable the software metering client setting.|  
|**Software 07C - Recently used executable programs on a specified computer**|Displays executable files that users recently used on a specified computer. This report requires that you enable the software metering client setting.|  
|**Software 08A - Recently used executable programs by the count of users**|Displays executable programs that users recently used. It also includes a count of users that most recently used the program. This report requires that you enable the software metering client setting.|  
|**Software 08B - Users that recently used a specified executable program**|Displays the users that most recently used a specified executable program. This report requires that you enable the software metering client setting.|  
|**Software 08C - Recently used executable programs by a specified user**|Displays executable programs that the specified user used recently. This report requires that you enable the software metering client setting.|  
|**Software 09A - Infrequently used software**|Displays software titles that users have not used during a specified period of time.|  
|**Software 09B - Computers with infrequently used software installed**|Displays computers with installed software that users have not used for a specified period of time. The specified period of time is based on the value specified in the 'Software 09A - Infrequently used software' report.|  
|**Software 10A - Software titles with specific multiple custom labels defined**|Displays software titles based on matching of all specified custom label criteria. Up to three custom labels can be selected to refine a software title search.|  
|**Software 10B - Computers with a specific custom-labeled software title installed**|Displays all computers in this collection that have the specified custom-labeled software title installed.|  
|**Software 11A - Software titles with a specific custom label defined**|Displays software titles based on matching of at least one of the specified custom label criteria.|  
|**Software 12A - Software titles without a custom label**|Displays all software titles that do not have a custom label defined.|  
|**Software 14A - Search for software identification tag enabled software**|Displays a count of installed software with a software identification tag enabled.|  
|**Software 14B - Computers with specific software identification tag enabled software installed**|Displays all computers that have installed software with a specified software identification tag enabled.|  
|**Software 14C - Installed software identification tag enabled software on a specific computer**|Displays all installed software with a specified software identification tag enabled on a specified computer.|  



## Client Push  

|Report name|Description|  
|-----------------|-----------------|  
|**Client push installation status details**|Displays information about the client push installation process for all sites.|  
|**Client push installation status details for a specified site**|Displays information about the client push installation process for a specified site.|  
|**Client push installation status summary**|Displays a summary view of the client push installation status for all sites.|  
|**Client push installation status summary for a specified site**|Displays a summary view of the client push installation status for a specified site.|  



## Client Status  

|Report name|Description|  
|-----------------|-----------------|  
|**Client remediation details**|Displays details of client remediation actions for a collection you specify.|  
|**Client remediation summary**|Displays a summary of client remediation actions for a specified collection.|  
|**Client status history**|Displays a historical view of overall client status in the site.|  
|**Client status summary**|Displays the client check results of active clients for a given collection.|  
|**Client time to request policy**|Displays the percentage of clients that requested policy at least once in the last 30 days. Each day represents a percentage of total clients that requested policy since the first day in the cycle.|  
|**Clients with failed client check details**|Displays details about clients that client check failed for a specified collection.|  
|**Inactive clients details**|Displays a detailed list of inactive clients for a given collection.|  



## Company Resource Access  

|Report name|Description|  
|-----------------|-----------------|  
|**Certificate issuance history**|Displays the history of certificates issued by the certificate registration point to users and devices for the specified date range.|  
|**List of assets by certificate issuance status**|Displays the devices or users in a specified certificate issuance state following the evaluation of a specified certificate profile.|  
|**List of assets with certificates nearing expiry**|Displays the devices or users with certificates that expire on or before the specified date.|  



## Compliance and Settings Management  

|Report name|Description|  
|-----------------|-----------------|  
|**Compliance history of a configuration baseline**|Displays the history of the changes in compliance of a configuration baseline for the specified date range.|  
|**Compliance history of a configuration item**|Displays the history of the changes in compliance of a configuration item for the specified date range.|  
|**Conditional Access Compliance for User**|Displays detailed conditional access compliance for a specific user.|
|**Conditional Access Compliance Report**|A conditional access compliance report for each targeted compliance policy.|
|**Details of compliant rules of configuration items in a configuration baseline for an asset**|Displays information about the rules evaluated as compliant for a specified configuration item for a specified device or user.|  
|**Details of conflicting rules of configuration items in a configuration baseline for an asset**|Displays information about rules in a deployed configuration item that conflict with other rules. The other rules can be contained in the same or another deployed configuration item.|  
|**Details of errors of configuration items in a configuration baseline for an asset**|Displays information about errors generated by a specified configuration item for a specified device or user.|  
|**Details of non-compliant rules of configuration items in a configuration baseline for an asset**|Displays information about rules that were evaluated as noncompliant for a specified configuration item, for a specified device or user.|  
|**Details of remediated rules of configuration items in a configuration baseline for an asset**|Displays information about rules that were remediated by a specified configuration item for a specified device or user.|  
|**List of assets by compliance state for a configuration baseline**|Displays the devices or users in a specified compliance state following the evaluation of a specified configuration baseline.|  
|**List of assets by compliance state for a configuration item in a configuration baseline**|Displays the devices or users in a specified compliance state following the evaluation of a specified configuration item.|  
|**List of noncompliant Apps and Devices for a specified user**|Displays information about users and devices that have apps installed that are not compliant with a policy you specified.|  
|**List of rules conflicting with a specified rule for an asset**|Displays a list of rules that conflict with a specified rule for a deployed configuration item.|  
|**List of unknown assets for a configuration baseline**|Displays a list of devices or users that have not yet reported any compliance data for a specified configuration baseline.|  
|**List of unknown assets for a configuration item**|Displays a list of devices or users that have not yet reported any compliance data for a specified configuration item.|  
|**Rules and errors summary of configuration items in a configuration baseline for an asset**|Displays a summary of the compliance state of the rules and any setting errors for a specified configuration item. The configuration item must be deployed to a device or user.|  
|**Summary compliance by configuration baseline**|Displays a summary of the overall compliance of deployed configuration baselines in the hierarchy.|  
|**Summary compliance by configuration items for a configuration baseline**|Displays a summary of the compliance of configuration items in a specified configuration baseline.|  
|**Summary compliance by configuration policies**|Displays a summary of the compliance of configuration policies.|  
|**Summary compliance of a configuration baseline for a collection**|Displays a summary of the overall compliance of a specified configuration baseline. The configuration item must be deployed to the specified collection.|  
|**Summary of Users who have Noncompliant Apps**|Displays information about users that have apps installed that are not compliant with a policy you specified.|  
|**Terms and Conditions acceptance**|Displays Terms and Conditions items and which version each user has accepted.|  



## Device Management  

|Report name|Description|  
|-----------------|-----------------|  
|**All corporate-owned mobile devices**|Displays all corporate owned mobile devices.|
|**All mobile device clients**|Displays information about all mobile device clients. Devices that are managed by the Exchange Server connector are not included.|  
|**Certificate issues on mobile devices that are managed by the Configuration Manager client for Windows CE and that are not healthy**|Displays detailed information about certificate issues on mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Client deployment failure for mobile devices that are managed by the Configuration Manager client for Windows CE**|Displays detailed information about deployment failure for mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Client deployment status details for mobile devices that are managed by the Configuration Manager client for Windows CE**|Displays information about the status of mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Client deployment success for mobile devices that are managed by the Configuration Manager client for Windows CE**|Displays detailed information about deployment success for mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Communication issues on mobile devices that are managed by the Configuration Manager client for Windows CE and that are not healthy**|This report contains detailed information about communication issues on mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Compliance status of default ActiveSync mailbox policy for the mobile devices that are managed by the Exchange Server connector**|Displays a summary of the compliance status with the Default Exchange ActiveSync mailbox policy for the mobile devices managed by the Exchange Server connector.|  
|**Count of mobile devices by display configurations**|This report displays the number of mobile devices by display settings.|  
|**Count of mobile devices by operating system**|Displays the number of mobile devices by operating system.|  
|**Count of mobile devices by program memory**|Displays the number of mobile devices by program memory.|  
|**Count of mobile devices by storage memory configurations**|Count of mobile devices by storage memory configurations|  
|**Health information for mobile devices that are managed by the Configuration Manager client for Windows CE**|Displays detailed health information for mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Health summary for mobile devices that are managed by the Configuration Manager client for Windows CE**|Displays health summary information for mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Inactive mobile devices that are managed by the Exchange Server connector**|Displays the mobile devices managed by the Exchange Server connector that have not connected to an Exchange Server in a specified number of days.|  
|**List of devices by Conditional Access State**|Displays information about the current compliance and conditional access state of devices. You can use this report with conditional access policies. This report is available beginning in version 1602 of Configuration Manager.|  
|**List of devices by Health Attestation state**|Displays a list of devices with attributes reported by Health Attestation Service|
|**List of Devices enrolled per user in Microsoft Intune**|Displays all devices a user has enrolled with Microsoft Intune.|  
|**List of devices in a specific device category**|Displays information for all devices within a specific device category.|
|**Local client issues on mobile devices that are managed by the Configuration Manager client for Windows CE and that are not healthy**|This report contains detailed information about local client issues on mobile devices that are managed by the Configuration Manager client for Windows CE.|  
|**Mobile device client information**|Displays information about the mobile devices that have the Configuration Manager client installed. You can use this report to verify which mobile devices can successfully communicate with a management point.|  
|**Mobile device compliance details for the Exchange Server connector**|Displays the mobile device compliance details for a default Exchange ActiveSync mailbox policy that is configured by using the Exchange Server connector.|  
|**Mobile devices by operating system**|Displays the mobile devices by operating system.|  
|**Mobile devices that are jailbroken or a rooted device**|Displays the mobile devices that are jailbroken or a rooted device.|  
|**Mobile devices that are unmanaged because they enrolled but failed to assign to a site**|Displays the mobile devices that completed enrollment with Configuration Manager, have a certificate, but failed to complete site assignment.|  
|**Mobile devices with a specific amount of free program memory**|Displays all mobile devices with their specified amount of free program memory.|  
|**Mobile devices with a specific amount of free removable storage memory**|Displays all mobile devices with the specified amount of free removable memory.|  
|**Mobile devices with certificate renewal issues**|Displays the enrolled mobile devices that failed to renew their certificate. If you do not renew the certificate before the expiry period, the mobile devices become unmanaged.|  
|**Mobile devices with low free program memory (less than specified KB free)**|Displays the mobile devices for which the program memory is lower than a specified size in KB.|  
|**Mobile devices with low free removable storage memory (less than specified KB free)**|Displays the mobile devices for which the removable storage memory is lower than a specified size in KB.|  
|**Number of devices enrolled per user in Microsoft Intune**|Displays the users enabled for the Microsoft Intune subscription. It also shows the total number of devices enrolled for each user.|  
|**Pending retire and wipe request for mobile devices**|Displays the wipe requests that are pending for mobile devices.|  
|**Recently enrolled and assigned mobile devices**|Displays mobile devices that recently enrolled with Configuration Manager and successfully assigned to a site.|  
|**Recently wiped mobile devices**|Displays the list of mobile devices that were recently successfully wiped.|  
|**Settings summary for mobile devices that are managed by the Exchange Server connector**|Displays the number of mobile devices that apply the settings for each Default Exchange ActiveSync mailbox policy managed by the Exchange Server connector.|  
|**Windows RT Sideloading Keys Detailed Status**|Displays detailed status information for a specified Windows RT sideloading key.|  
|**Windows RT Sideloading Keys Summary**|Displays the status of Windows RT sideloading keys.|  



## Driver Management  

|Report name|Description|  
|-----------------|-----------------|  
|**All drivers**|Displays a list of all drivers.|  
|**All drivers for a specific platform**|Displays all drivers for a specified platform.|  
|**All drivers in a specific boot image**|Displays all drivers in a specified boot image.|  
|**All drivers in a specific category**|Displays all drivers in a specified category.|  
|**All drivers in a specific package**|Displays all drivers in a specified package.|  
|**Categories for a specific driver**|Displays categories for a specified driver.|  
|**Computers that failed to install drivers for a specific collection**|Displays computers that failed to install drivers for a specified collection.|  
|**Driver catalog matching report for a specific collection**|Displays the driver catalog matching report for a specified collection.|  
|**Driver catalog matching report for a specific computer**|Displays the driver catalog matching report for a specified computer.|  
|**Driver catalog matching report for a specific device on a specific computer**|Displays the driver catalog matching report for a specified device on a specified computer.|  
|**Driver catalog matching report for computers in a specific collection with a specific device**|Displays driver catalog matching report for computers in a specified collection with a specified device.|  
|**Drivers that failed to install on a specific computer**|Displays drivers that failed to install on a specified computer.|  
|**Supported platforms for a specific Driver**|Displays supported platforms for a specified driver.|  



## Endpoint Protection  

|Report name|Description|  
|-----------------|-----------------|  
|**Antimalware activity report**|Displays an overview of antimalware activity.|  
|**Antimalware overall status and history**|Displays the antimalware overall status and history.|  
|**Computer malware details**|Displays details about a specified computer and the list of malware found on it.|  
|**Infected computers**|Displays a list of computers with a specified threat detected.|  
|**Top users by threats**|Displays the list of users with the most number of detected threats.|  
|**User threat list**|Displays the list of threats found for a specified user account.|  



## Hardware - CD-ROM  

|Report name|Description|  
|-----------------|-----------------|  
|**CD-ROM information for a specific computer**|Displays information about the CD-ROM drives on a specified computer.|  
|**Computers for a specific CD-ROM manufacturer**|Displays a list of computers that contain a CD-ROM drive made by a manufacturer you specify.|  
|**Count CD-ROM drives per manufacturer**|Displays the number of CD-ROM drives inventoried per manufacturer.|  
|**History - CD-ROM history for a specific computer**|Displays the inventory history for CD-ROM drives on a specified computer.|  



## Hardware - Disk  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers with a specific hard disk size**|Displays a list of computers that have hard disks of a specified size.|  
|**Computers with low free disk space (less than specified % free)**|Displays a list of computers in a specified collection that have less that the specified free disk space.|  
|**Computers with low free disk space (less that specified MB free)**|Displays a list of computers and disks where the disks are low on space. The amount of free space to check for is specified in MB.|  
|**Count physical disk configurations**|Displays the number of hard disks inventoried by disk capacity.|  
|**Disk information for a specific computer - Logical disks**|Displays summary information about the logical disks on a specified computer.|  
|**Disk information for a specific computer - Partitions**|Displays summary information about the disk partitions on a specified computer.|  
|**Disk information for a specific computer - Physical disks**|Displays summary information about the physical disks on a specified computer.|  
|**History - Logical disk space history for a specific computer**|Displays the inventory history for logical disk drives on a specified computer.|  



## Hardware - General  

|Report name|Description|  
|-----------------|-----------------|  
|**Computer information for a specific computer**|Displays summary information for a specified computer.|  
|**Computers in a specific workgroup or domain**|Displays a list of computers in a specified Workgroup or domain.|  
|**Inventory classes assigned to a specific collection**|Displays the inventory classes that are assigned to a specified collection.|  
|**Inventory classes enabled on a specific computer**|Displays the inventory classes that are enabled on a specified computer.|  
|**Windows AutoPilot Device Information**|Displays client device information that is needed for Windows AutoPilot registration.|



## Hardware - Memory  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers where physical memory has changed**|Displays a list of computers where the amount of RAM has changed since the last inventory cycle.|  
|**Computers with a specific amount of memory**|Displays a list of computers that have a specified amount of RAM (Total Physical Memory rounded to the nearest MB).|  
|**Computers with low memory (less than or equal to specified MB)**|Displays a list of computers that are low on memory. The amount of memory to check for is specified in MB.|  
|**Count memory configurations**|Displays the number of computers inventoried by amount of RAM.|  
|**Memory information for a specific computer**|Displays summary information about the memory on a specified computer.|  



## Hardware - Modem  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers for a specific modem manufacturer**|Displays a list of computers that have a modem made by a specified manufacturer.|  
|**Count modems by manufacturer**|Displays the number of modems inventoried for each modem manufacturer.|  
|**Modem information for a specific computer**|Displays summary information about the modem on a specified computer.|  



## Hardware - Network Adapter  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers with a specific network adapter**|Displays a list of computers that have a specified network adapter.|  
|**Count network adapters by type**|Displays the number of inventoried network adapters cards of each type.|  
|**Network adapter information for a specific computer**|Displays information about the network adapters installed on a specified computer.|  



## Hardware - Processor  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers for a specific processor speed**|Displays a list of computers that have a processor of a specified speed.|  
|**Computers with fast processors (greater than or equal to a specified clock speed)**|Displays a list of computers that have processors with a speed that is faster than the specified speed.|  
|**Computers with slow processors (less than or equal to a specified clock speed)**|Displays a list of computers that have processors that run at or slower than a specified clock speed.|  
|**Count processor speeds**|Displays the number of computers inventoried by processor speed.|  
|**Processor information for a specific computer**|Displays information about the processors installed on a specified computer.|  



## Hardware - SCSI  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers with a specific SCSI card type**|Displays a list of computers that have a specified SCSI card installed.|  
|**Count SCSI card types**|Displays the number of inventoried SCSI cards by card type.|  
|**SCSI card information for a specific computer**|Displays information about the SCSI cards installed on a specified computer.|  



## Hardware - Security

|Report name|Description|  
|-----------------|-----------------|  
|**Details of firmware states on devices**|Displays the details of the states of UEFI, SecureBoot, and TPM|  



## Hardware - Sound Card  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers with a specific sound card**|Displays a list of computers that have a specified sound card.|  
|**Count sound cards**|Displays the number of computers inventoried by each sound card type.|  
|**Sound card information for a specific computer**|Displays summary information about the sound cards on a specified computer.|  



## Hardware - Video Card  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers with a specific video card**|Displays a list of computers that have a specified video card.|  
|**Count video cards by type**|Displays a list of all of the video cards installed on computers. It also shows the number of each type of video card.|  
|**Video card information for a specific computer**|Displays summary information about the video cards installed on a specified computer.|  



## Migration  

|Report name|Description|  
|-----------------|-----------------|  
|**Clients in exclusion list**|Displays clients that are excluded from migration.|  
|**Dependency on a Configuration manager collection**|Displays the objects that depend on a collection of the source hierarchy.|  
|**Migration job properties**|This report shows the contents of the specified migration job.|  
|**Migration jobs**|This report shows the list of migration jobs.|  
|**Objects that failed to migrate**|Displays a list of objects that failed to migrate during the last attempt.|  



## Network  

|Report name|Description|  
|-----------------|-----------------|  
|**Count IP addresses by subnet**|Displays the number of IP addresses inventoried for each IP subnet.|  
|**IP - All subnets by subnet mask**|Displays a list of IP subnets and subnet masks.|  
|**IP - Computers in a specific subnet**|Displays a list of computers and IP information for a specified IP subnet.|  
|**IP - Information for a specific computer**|Displays summary information about IP on a specified computer.|  
|**IP - Information for a specific IP address**|Displays summary information about a specified IP address.|  
|**MAC - Computers for a specific MAC address**|Displays the computer name and IP address of computers that have the specified MAC address.|  



## Operating System  

|Report name|Description|  
|-----------------|-----------------|  
|**Computer operating system version history**|Displays the inventory history for the operating system on a specified computer.|  
|**Computers with a specific operating system**|Displays computers with a specified operating system.|  
|**Computers with a specific operating system and service pack**|Displays computers with a specified operating system and service pack.|  
|**Count operating system versions**|Displays the number of computers inventoried by operating system.|  
|**Count operating systems and service packs**|Displays the number of computers inventoried by operating system and service pack combinations.|  
|**Services - Computers running a specific service**|Displays a list of computers running a specified service.|  
|**Services - Computers running Remote Access Server**|Displays a list of computers running Remote Access Server.|  
|**Services - Services information for a specific computer**|Displays summary information about the services on a specified computer.|  
|**Windows 10 Servicing details for a specific collection**|Displays general information about Windows 10 servicing for a specific collection.|
|**Windows Server computers**|Displays a list of computers that run Windows Server operating systems.|  



## Power Management  

|Report name|Description|  
|-----------------|-----------------|  
|**Power Management - Computer activity**|Displays a graph showing monitor, computer, and user activity for a specified collection over a specified time period.|  
|**Power Management - Computer activity by computer**|Displays a graph showing monitor, computer, and user activity for a specified computer on a specified date.|  
|**Power Management - Computer activity details**|Displays a list of the sleep and wake capabilities of computers in the specified collection for a specified date and time.|  
|**Power Management - Computer details**|Displays detailed information about the power capabilities, power settings, and power plans applied to a specified computer.|  
|**Power Management - Computer not reporting details**|Displays a list of computers not reporting any power activity for a specified date and time.|  
|**Power Management - Computers excluded**|Displays a list of computers excluded from the power plan.|  
|**Power Management - Computers with multiple power plans**|Displays a list of computers that have multiple, conflicting power settings applied.|  
|**Power Management - Energy consumption**|Displays the total monthly energy consumption (in kWh) for a specified collection over a specified time period.|  
|**Power Management - Energy consumption by day**|Displays the total energy consumption (in kWh) for a specified collection in the last 31 days.|  
|**Power Management - Energy cost**|Displays the total monthly energy consumption cost for a specified collection over a specified time period.|  
|**Power Management - Energy cost by day**|Displays the total energy consumption cost for a specified collection over the past 31 days.|  
|**Power Management - Environmental impact**|Displays a graph showing carbon dioxide (CO2) emissions generated by a specified collection over a specified time period.|  
|**Power Management - Environmental impact by day**|Displays a graph showing CO2 emissions generated by a specified collection over the past 31 days.|  
|**Power Management - Insomnia computer details**|Displays detailed information about computers that did not sleep or hibernate within a specified time period.|  
|**Power Management - Insomnia report**|Displays a list of common causes that prevented computers from sleeping or hibernating. It also shows the number of computers affected by each cause over a specified time period.|  
|**Power Management - Power capabilities**|Displays the power management capabilities of computers in the specified collection.|  
|**Power Management - Power settings**|Displays an aggregated list of power settings used by computers in a specified collection.|  
|**Power Management - Power settings details**|Used to display further information about computers that were specified in the **Power Management - Power settings** report.|  



## Replication Traffic  

|Report name|Description|  
|-----------------|-----------------|  
|**Global Data Replication Traffic Per Link (line chart)**|Displays total global data replication traffic on a specified link for a specified number of days.|  
|**Global Data Replication Traffic Per Link (pie chart)**|Displays total global data replication traffic on a specified link for a specified number of days.|  
|**Hierarchy Replication Traffic By Link**|Displays total replication traffic for each link in the hierarchy for a specified number of days.|  
|**Hierarchy Top Ten Replication Groups Traffic Per Link (pie chart)**|Displays the replication traffic for the top 10 replication groups across the entire hierarchy identified by link.|  
|**Link Replication Traffic**|Displays total replication traffic for all data for a specified number of days.|  
|**Replication group traffic per link**|Displays the replication group network traffic over a specified database replication link for a specified number of days.|  
|**Site Data Replication Traffic Per Link (line chart)**|Displays total site data replication traffic on a specified link for a specified number of days.|  
|**Site Data Replication Traffic Per Link (pie chart)**|Displays total site data replication traffic on a specified link for a specified number of days.|  
|**Total Hierarchy Replication Traffic (line chart)**|Displays hierarchy aggregate global and site data replication for each direction of every link for a specified number of days.|  
|**Total Hierarchy Replication Traffic (pie chart)**|Displays hierarchy aggregate global and site data replication for each direction of every link for a specified number of days.|  



## Site - Client Information  

|Report name|Description|  
|-----------------|-----------------|  
|**Client assignment detailed status report**|Displays detailed information about client assignment status.|  
|**Client assignment failure details**|Displays detailed information about client assignment failures.|  
|**Client assignment status details**|Displays overview information about client assignment status.|  
|**Client assignment success details**|Displays detailed information about successfully assigned clients.|  
|**Client deployment failure report**|Displays detailed information for clients that have failed to deploy.|  
|**Client deployment status details**|Displays summary information for the status of client installations.|  
|**Client deployment success report**|Displays detailed information for clients that have successfully deployed.|  
|**Clients incapable of HTTPS communication**|Displays detailed information about each client that runs the HTTPS Communication Readiness Tool, and reports to be incapable of communicating over HTTPS.|  
|**Computers assigned but not installed for a particular site**|Displays a list of computers assigned to a specified site, but are not reporting to that site.|  
|**Computers with a specific Configuration Manager client version**|Displays a list of computers running a specified version of the Configuration Manager client software.|  
|**Count of clients and protocol used for communication**|Displays a summary of the communication methods used by clients (HTTP or HTTPS).|  
|**Count of clients assigned and installed for each site**|Displays the number of computers assigned and installed for each site. Clients with a network location associated to multiple sites are only counted as installed if they are reporting to that site.|  
|**Count of clients capable of HTTPS communication**|Displays detailed information about each client that runs the HTTPS Communication Readiness Tool, and reports to be either capable or incapable of communicating over HTTPS.|  
|**Count of clients for each site**|Displays the number of Configuration Manager clients installed by site code.|  
|**Count of Configuration Manager clients by client versions**|Displays the number of computers discovered by Configuration Manager client version.|  
|**Problem details reported to the fallback status point for a specified collection**|Displays detailed information for issues reported by clients in a specified collection. These clients must have an assigned fallback status point.|  
|**Problem details reported to the fallback status point for a specified site**|Displays detailed information about issues reported by clients in a specified site. These clients must have an assigned fallback status point.|  
|**Summary of problems reported to the fallback status point**|Displays information about all the issues reported by clients. These clients must have an assigned fallback status point.|  
|**Summary of problems reported to the fallback status point for a specific collection**|Displays summary information for issues reported by clients in a specified collection. These clients must have an assigned fallback status point.|  



## Site - Discovery and Inventory Information  

|Report name|Description|  
|-----------------|-----------------|  
|**Clients that have not reported recently (in a specified number of days)**|Displays a list of clients that have not reported discovery data, hardware inventory, or software inventory in a specified number of days.|  
|**Computers discovered by a specific site**|Displays a list of all computers that the specified site discovered. It also shows the date of the most recent discovery.|  
|**Computers discovered recently by discovery method**|Displays a list of computers that the site discovered within the specified number of days. It also lists the agents that discovered them. If multiple agents discovered a computer, it may appear more than once in the list.|  
|**Computers not discovered recently (in a specified number of days)**|Displays a list of computers that the site has not recently discovered. It also shows the number of days since the site discovered the computer.|  
|**Computers not inventoried recently (in a specified number of days)**|Displays a list of computers that the site has not recently inventoried. It also shows the last times the client inventoried the computer.|  
|**Computers that might share the same Configuration Manager unique identifier**|Displays a list of computers that have changed their names. A change in name is a possible symptom that a computer shares a Configuration Manager Unique Identifier with another computer.|  
|**Computers with duplicate MAC addresses**|Displays computers that share MAC address.|  
|**Count computers in resource domains or workgroups**|Displays the number of computers in each resource domain or workgroup.|  
|**Discovery information for a specific computer**|Displays a list of the agents and sites that discovered a specified computer.|  
|**Inventory dates for a specific computer**|Displays the date and time inventory was last run on a specified computer.|  



## Site - General  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers in a specific site**|Displays a list of client computers in a specified site.|  
|**Site status for the hierarchy**|Displays the list of sites in the hierarchy with site version and site status information.|  
|**Status of Configuration Manager update within hierarchy**|Displays information about Configuration Manager site updates for the  hierarchy.|  



## Site - Server Information  

|Report name|Description|  
|-----------------|-----------------|  
|**Site system roles and site system servers for a specific site**|Displays a list of site system server and their site system roles for a specified site.|  



## Software - Companies and Products  

|Report name|Description|  
|-----------------|-----------------|  
|**All inventoried products for a specific software company**|Displays a list of the inventoried software products and versions from a specified software company.|  
|**All software companies**|Displays a list of all companies manufacturing inventoried software.|  
|**All Windows apps**|Displays a summary of installed Windows apps. It searches using the following criteria: application name, architecture, or publisher.|  
|**Computers with a specific product**|Displays a list of the computers that a specified product is inventoried on, as well as the versions of that product.|  
|**Computers with a specific product name and version**|Displays a list of the computers that a specified version of a product is inventoried on.|  
|**Computers with specific software registered in Add Remove Programs**|Displays a summary of all computers with specified software registered in Add Remove Programs or Programs and Features.|  
|**Count all inventoried products and versions**|Displays a list of the inventoried software products and versions, and the number of computers each is installed on.|  
|**Count inventoried products and versions for a specific product**|Displays a list of the inventoried versions of a specified product, and the number of computers each is installed on.|  
|**Count of all instances of software registered with Add or Remove Programs**|Displays a summary of all instances of software installed and registered with Add or Remove Programs or Programs and Features on computers within the specified collection.|  
|**Count of instances of specific software registered with Add or Remove Programs**|Displays a count of instances for specified software packages installed and registered in Add or Remove Programs or Programs and Features.|  
|**Default Browser counts**|Shows the count of clients with a specific web browser as the Windows default. </br>Use the following reference for common BrowserProgIDs:</br> - AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge</br> - IE.HTTP: Microsoft Internet Explorer</br> - ChromeHTML: Google Chrome</br> - OperaStable: Opera Software</br> - FirefoxURL-308046B0AF4A39CB: Mozilla Firefox|
|**Installations of specified Windows apps**|This report lists all computers with a specified Windows app.|  
|**Products on a specific computer**|Displays a summary of the inventoried software products and their manufacturers on a specified computer.|  
|**Software registered in Add Remove Programs on a specific computer**|Displays a summary of the software installed on a specified computer that is registered in Add Remove Programs or Programs and Features.|  
|**Windows apps installed to the specified user**|Displays all Windows apps installed to the specified user|  



## Software - Files  

|Report name|Description|  
|-----------------|-----------------|  
|**All inventoried files for a specific product**|Display a summary of the files inventoried that are associated with a specified software product.|  
|**All inventoried files on a specific computer**|Display a summary of all the files inventoried on a specified computer.|  
|**Compare software inventory on two computers**|Displays the differences between the software inventories reported for two specified computers.|  
|**Computers with a specific file**|Displays a list of computers that have collected software inventory for a specified file name. If a computer contains multiple copies of the file, it might appear more than once in the list.|  
|**Count computers with a specific file name**|Displays the number of computers that have collected software inventory for a specified file.|  



## Software Distribution - Application Monitoring  

|Report name|Description|  
|-----------------|-----------------|  
|**All application deployments (advanced)**|Displays detailed summary information for all application deployments.|  
|**All application deployments (basic)**|Displays summary information for all application deployments.|  
|**Application compliance**|Displays compliance information for the specified application within the specified collection.|  
|**Application deployments per asset**|Displays applications deployed to a specified device or user.|  
|**Application infrastructure errors**|Displays application infrastructure errors. These errors include internal infrastructure issues, or errors resulting from invalid requirement rules.|  
|**Application Usage Detailed Status**|Displays usage details for installed applications.|  
|**Application Usage Summary Status**|Displays a usage summary for installed applications.|  
|**iOS apps with failed deployments (app already installed)**|Displays compliance information for the selected iOS app. You deployed this app as an 'App package for iOS from App Store', which you also associated with a mobile application management policy. This report is used to display users and devices for which the app failed to install because it had already been manually installed by the user.|  
|**Task sequence deployments containing application**|Displays task sequence deployments that install a specified application.|  
|**User Requests for Android Application**|Displays users that requested to install an Android application.|  



## Software Distribution - Collections  

|Report name|Description|  
|-----------------|-----------------|  
|**All collections**|Displays all the collections in the hierarchy.|  
|**All resources in a specific collection**|Displays all the resources in a specified collection.|  
|**Maintenance windows available to a specified client**|Displays all maintenance windows that are applicable to the specified client.|  



## Software Distribution - Content  

|Report name|Description|  
|-----------------|-----------------|  
|**All active content distributions**|Displays all distributions points on which content is currently being installed or removed.|  
|**All content**|Displays all applications and packages at a site.|  
|**All content on a specific distribution point**|Displays all content currently installed on a specified distribution point.|  
|**All distribution points**|Displays information about the distribution points for each site.|  
|**All status messages for a specific package on a specific distribution point**|Displays all status messages for a specified package on a specified distribution point.|  
|**Application content distribution status**|Displays information about the distribution status for application content.|  
|**Applications targeted to distribution point group**|Displays information about application content that was deployed to a specified distribution point group.|  
|**Applications that are out of synchronization on a specified distribution point group**|Displays the applications for which associated content files have not been updated with the latest version on a specified distribution point group.|  
|**Distribution point group**|Displays information about a specified distribution point group.|  
|**Distribution point usage summary**|Displays the distribution point usage summary for each distribution point.|  
|**Distribution status of specified package**|Displays the distribution status for specified package content on each distribution point.|  
|**Packages targeted to distribution point group**|Displays information about packages that target a specified distribution point group.|  
|**Packages that are out of synchronization on a specified distribution point group**|Displays packages for which associated content files have not been updated with the latest version on a specified distribution point group.|  
|**Peer cache source content rejection**|Displays the number of peer cache source rejections per boundary group.|
|**Peer cache source content rejection by condition**|Displays the peer cache sources that rejected to serve content based on a condition.|
|**Peer cache source content rejection details**|Displays the name of the content that was rejected by a peer source.|



## Software Distribution - Package and Program Deployment  

|Report name|Description|  
|-----------------|-----------------|  
|**All deployments for a specified package and program**|Displays information about all deployments of a specified package and program.|  
|**All package and program deployments**|Displays all of the package and program deployments at this site.|  
|**All package and program deployments to a specified collection**|Displays all of the package and program deployments to a specified collection.|  
|**All package and program deployments to a specified computer**|Displays all of the package and program deployments that apply to a specified computer.|  
|**All package and program deployments to a specified user**|Displays all of the package and program deployments to a specified user.|  



## Software Distribution - Package and Program Deployment Status  

|Report name|Description|  
|-----------------|-----------------|  
|**All system resource package and program deployments with status**|Displays all package and program deployments for the site with a summary status of each deployment.|  
|**All system resources for a specified package and program deployment in a specified state**|Displays a list of resources that are in a specified state for a specified package and program deployment.|  
|**Chart - Hourly package and program deployment completion status**|Displays the percentage of computers that successfully installed the package. The list organizes for every hour since an administrator creates the package and program deployment. It can be used to track the average time for a package and program deployment.|  
|**Package and program deployment status for a specified client and deployment**|Displays the status messages reported for a specified computer and package and program deployment.|  
|**Status of a specified package and program deployment**|Displays the status summary for a specified package and program deployment.|  



## Software Metering  

|Report name|Description|  
|-----------------|-----------------|  
|**All software metering rules applied to this site**|Displays a list of all software metering rules at the site.|  
|**Computers that have a metered program installed but have not run the program since a specified date**|Displays all computers with the specified metered application, but no user has run the program since the specified date.|  
|**Computers that have run a specific metered software program**|Displays a list of computers that have run programs matching the specified software metering rule within the specified month and year.|  
|**Concurrent usage for all metered software programs**|Displays the maximum number of users who concurrently ran each metered software program during the specified month and year.|  
|**Concurrent usage trend analysis of a specific metered software program**|Displays the maximum number of users who concurrently ran the specified metered software program during each month for the past year.|  
|**Install base for all metered software programs**|Displays the number of computers that have metered software programs installed as reported by software inventory. This report requires that the computer collects software inventory.|  
|**Software metering summarization progress**|Displays the time at which the most recently summarized metering data was processed on the site server. The software metering reports only reflect metering data processed before these dates.|  
|**Time of day usage summary for a specific metered software program**|Displays the average number of usages of a particular program for the past 90 days, broken down by hour and day.|  
|**Total usage for all metered software programs**|Displays the number of users who ran programs within the specified month and year, and that match each software metering rule. These rules are for locally-installed software, or using Terminal Services.|  
|**Total usage for all metered software programs on Windows Terminal Servers**|Displays the number of users who ran programs matching each software metering rule using Terminal Services within the specified month and year.|  
|**Total usage trend analysis for a specific metered software program**|Displays the number of users who ran programs during each month for the past year, and that match the specified software metering rule. These rules are for locally-installed software, or using Terminal Services.|  
|**Total usage trend analysis for a specific metered software program on Windows Terminal Servers**|Displays the number of users who ran programs during each month for the past year, and that match the specified software metering rule. These rules are for using Terminal Services.|  
|**Users that have run a specific metered software program**|Displays a list of users who have run programs within the specified month and year, and that match the specified software metering rule.|  



## Software Updates - A Compliance  

|Report name|Description|  
|-----------------|-----------------|  
|**Compliance 1 - Overall compliance**|Displays the overall compliance data for a software update group.|  
|**Compliance 2 - Specific software update**|Displays the compliance data for a specified software update.|  
|**Compliance 3 - Update group (per update)**|Displays the compliance data for software updates defined in a software update group.|  
|**Compliance 4 - Updates by vendor month year**|Displays the compliance data for software updates released by a vendor during a specified month and year.|  
|**Compliance 5 - Specific computer**|This report returns the software update compliance data for a specified computer. To limit the amount of information returned, you can specify the vendor and software update classification.|  
|**Compliance 6 - Specific software update states (secondary)**|Displays the count and percentage of computers in each compliance state for the specified software update.|  
|**Compliance 7 - Computers in a specific compliance state for an update group (secondary)**|Displays all computers in a collection that have a specified overall compliance state against a software update group.|  
|**Compliance 8 - Computers in a specific compliance state for an update (secondary)**|Displays all computers in a collection that have a specified compliance state for a software update.|  



## Software Updates - B Deployment Management  

|Report name|Description|  
|-----------------|-----------------|  
|**Management 1 - Deployments of an update group**|Displays all deployments that contain all of the software updates defined in a specified software update group.|  
|**Management 2 - Updates required but not deployed**|Displays all vendor-specific software updates that clients detect as required, but an administrator has not deployed to a specified collection.|  
|**Management 3 - Updates in a deployment**|Displays the software updates that are contained in a specified deployment.|  
|**Management 4 - Deployments that target a collection**|Displays all software update deployments that target a specified collection.|  
|**Management 5 - Deployments that target a computer**|Displays all software update deployments that are deployed to a specified computer.|  
|**Management 6 - Deployments that contain a specific update**|Displays all deployments that contain a specified software update and the associated target collection for the deployment.|  
|**Management 7 - Updates in a deployment missing content**|Displays the software updates in a specified deployment that do not have all of the associated content retrieved. This state prevents clients from installing the update, which prevents the deployment from achieving 100% compliance.|  
|**Management 8 - Computers missing content (secondary)**|Displays all computers requiring the specified software update, but the associated content is not yet distributed to a distribution point.|  



## Software Updates - C Deployment States  

|Report name|Description|  
|-----------------|-----------------|  
|**States 1 - Enforcement states for a deployment**|Displays the enforcement states for a specified software update deployment, which is typically the second phase of a deployment assessment.|  
|**States 2 - Evaluation states for a deployment**|Displays the evaluation state for a specified software update deployment, which is typically the first phase of a deployment assessment.|  
|**States 3 - States for a deployment and computer**|Displays the states for all software updates in the specified deployment for a specified computer.|  
|**States 4 - Computers in a specific state for a deployment (secondary)**|Displays all computers in a specified state for a software update deployment.|  
|**States 5 - States for an update in a deployment (secondary)**|Displays a summary of states for a specified software update targeted by a specified deployment.|  
|**States 6 - Computers in a specific enforcement state for an update (secondary)**|Displays all computers in a specified enforcement state for a specified software update.|  



## Software Updates - D Scan  

|Report name|Description|  
|-----------------|-----------------|  
|**Scan 1 - Last scan states by collection**|Specify a collection to display the count of computers in each compliance scan state. The clients return the state during the last compliance scan.|  
|**Scan 2 - Last scan states by site**|Specify a site to display the count of computers in each compliance scan state. The clients return the state during the last compliance scan.|  
|**Scan 3 - Clients of a collection reporting a specific state (secondary)**|Displays all computers for a specified collection and a specified compliance scan state during their last compliance scan.|  
|**Scan 4 - Clients of a site reporting a specific state (secondary)**|Specify a site to display all computers with a specified compliance scan state. The clients return the state during their last compliance scan.|  



## Software Updates - E Troubleshooting  

|Report name|Description|  
|-----------------|-----------------|  
|**Troubleshooting 1 - Scan errors**|Displays scan errors at the site and a count of computers that are experiencing each error.|  
|**Troubleshooting 2 - Deployment errors**|Displays the deployment errors at the site and a count of computers that are experiencing each error.|  
|**Troubleshooting 3 - Computers failing with a specific scan error (secondary)**|Displays a list of the computers that failed a scan because of a specified error.|  
|**Troubleshooting 4 - Computers failing with a specific deployment error (secondary)**|Displays a list of the computers on which the deployment of update is failing because of a specified error.|  



## State Migration  

|Report name|Description|  
|-----------------|-----------------|  
|**State migration information for a specific source computer**|Displays state migration information for a specified computer.|  
|**State migration information for a specific state migration point**|Displays state migration information for a specified state migration point.|  
|**State migration points for a specific site**|Displays the state migration points for a specified site.|  



## Status Messages  

|Report name|Description|  
|-----------------|-----------------|  
|**All messages for a specific message ID**|Displays a list of status messages that have a specified message ID.|  
|**Clients reporting errors in the last 12 hours for a specific site**|Displays a list of computers and components reporting errors in the last 12 hours, and the number of errors reported.|  
|**Component messages for the last 12 hours**|Displays a list of component messages for the last 12 hours for a specified site code, computer, and component.|  
|**Component messages for the last hour**|Displays a list of the status messages created in the last hour by a specified component on a specified computer at a specified site.|  
|**Count component messages for the last hour for a specific site**|Displays the number of status messages by component and severity reported in the last hour at a specified site.|  
|**Count errors in the last 12 hours**|Displays the number of server component error status messages in the last 12 hours.|  
|**Fatal errors (by component)**|Displays a list of computers reporting fatal errors by component.|  
|**Fatal errors (by computer name)**|Displays a list of computers reporting fatal errors by computer name.|  
|**Last 1000 messages for a specific computer (Errors and Warnings)**|Displays a summary of the last 1000 error and warning component status messages for a specified computer.|  
|**Last 1000 messages for a specific computer (Errors Warnings and Information)**|Displays a summary of the last 1000 error, warning, and informational component status messages for a specified computer.|  
|**Last 1000 messages for a specific computer (Errors)**|Displays a summary of the last 1000 error server component status messages for a specified computer.|  
|**Last 1000 messages for a specific server component**|Displays a summary of the most recent 1000 status messages for a specified server component.|  



## Status Messages - Audit  

|Report name|Description|  
|-----------------|-----------------|  
|**All audit messages for a specific user**|Displays a summary of all audit status messages for a specified user. Audit messages describe actions taken in the Configuration Manager console that add, modify, or delete objects in Configuration Manager.|  
|**Remote Control - All computers remote controlled by a specific user**|Displays a summary of status messages indicating remote control of client computers by a specified user.|  
|**Remote Control - All remote control information**|Displays a summary of status messages related to the remote control of client computers.|  



## Task Sequence - Deployment Status  

|Report name|Description|  
|-----------------|-----------------|  
|**All system resources for a task sequence deployment in a specific state**|Displays a list of the destination computers for the specified task sequence deployment in a specified deployment state.|  
|**All system resources for a task sequence deployment that is in a specific state and that is available to unknown computers**|Displays a list of the destination computers for the specified task sequence deployment that is in the specified deployment state.|  
|**Count of system resources that have task sequence deployments assigned but not yet run**|Displays the number of computers that have accepted task sequences, but have not run the task sequence.|  
|**History of a task sequence deployment on a computer**|Displays the status of each step of the specified task sequence deployment on the specified destination computer. If no record is returned, the task sequence has not started on the computer.|  
|**List of computers that exceeded a specific length of time to run a task sequence deployment**|Displays the list of destination computers that exceeded the specified length of time to run a task sequence.|  
|**Run time for a specific task sequence deployment on a specific destination computer**|Displays the total time that it took to successfully complete a specified task sequence on a specified computer.|  
|**Run time for each step of a task sequence deployment on a specific destination computer**|Displays the time that it took to complete each step of the specified task sequence deployment on the specified destination computer.|  
|**Status of a specific task sequence deployment for a specific computer**|Displays the status summary of a specified task sequence deployment on a specified computer.|  
|**Status of a task sequence deployment on an unknown destination computer**|Displays the status of the specified task sequence deployment on the specified unknown destination computer.|  
|**Status summary of a specific task sequence deployment**|Displays a status summary of all resources that have been targeted by a deployment.|  
|**Status summary of a specific task sequence deployment available to unknown computers**|Displays the status summary of all resources targeted by the specified deployment that is available to a collection containing unknown computers.|  



## Task Sequence - Deployments  

|Report name|Description|  
|-----------------|-----------------|  
|**All system resources currently in a specific group or phase of a specific task sequence deployment**|Displays a list of computers that are currently running in a specified group or phase of a specified task sequence deployment.|  
|**All system resources where a task sequence deployment failed within a specific group or phase**|Displays a list of computers that failed within a specified group/phase of the specified task sequence deployment.|  
|**All task sequence deployments**|Displays details of all task sequence deployments initiated from the current site.|  
|**All task sequence deployments available to unknown computers**|Displays details of all the task sequence deployments initiated from the site, and deployed to collections that contain unknown computers.|  
|**Count of failures in each phase or group of a specific task sequence**|Displays the number of failures in each phase or group of the specified task sequence.|  
|**Count of failures in each phase or group of a specific task sequence deployment**|Displays the number of failures in each phase or group of the specified task sequence deployment.|  
|**Deployment status of all task sequence deployments**|Displays the overall progress of all task sequence deployments.|  
|**Progress of a running task sequence**|Displays the progress of the specified task sequence.|  
|**Progress of a running task sequence deployment**|Displays the summary information for the specified task sequence deployment.|  
|**Progress of all deployments for a specific task sequence**|Displays the progress of all deployments for the specified task sequence.|  
|**Summary report for a task sequence deployment**|Displays the summary information for the specified task sequence deployment.|  



## Task Sequence - Progress  

|Report name|Description|  
|-----------------|-----------------|  
|**Chart - Weekly progress of a task sequence**|Displays the weekly progress of a task sequence, starting from the deployment date.|  
|**Progress of a task sequence**|Displays the progress of the specified task sequence.|  
|**Progress of all task sequences**|Displays a summary of the progress of all task sequences.|  
|**Progress of task sequences for operating system deployments**|Displays the progress of all task sequences that deploy operating systems.|  
|**Status of all unknown computers**|Displays a list of computers that were unknown at the time they ran a task sequence deployment, and whether they are now known computers.|  



## Task Sequences - References  

|Report name|Description|  
|-----------------|-----------------|  
|**Content referenced by a specific task sequence**|Displays content that is referenced by a specified task sequence.|  



<!--
## Upgrade Assessment  

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## User - Device Affinity  

|Report name|Description|  
|-----------------|-----------------|  
|**Pending user device affinity associations by collection**|This report shows all pending user device affinity assignments based on usage data, for members of a collection.|  
|**User device affinity associations per collection**|Displays all user device associations for the specified collection, and groups the results by collection type (for example, user or device).|  



## User Data and Profiles Health  

|Report name|Description|  
|-----------------|-----------------|  
|**Folder Redirection Health Report - Details**|Displays the health state details of folder redirection for each of the redirected folders for a given user.|  
|**Roaming User Profiles Health Report - Details**|Displays the health state details of the roaming user profile for a specified user.|  
|**User Data and Profiles Health Report - Details**|Displays the error or warning details of folder redirection or roaming user profiles. This report is the details target from the summary report.|  
|**User Data and Profiles Health Report - Summary**|Displays the summary of health states for folder redirection and roaming user profiles.|  



## Users  

|Report name|Description|  
|-----------------|-----------------|  
|**Computers for a specific user name**|Displays a list of the computers that were used by a specified user.|  
|**Count users by domain**|Displays the number of users in each domain.|  
|**Users in a specific domain**|Displays a list of users and their computers in a specified domain.|  



## Virtual Applications  

|Report name|Description|  
|-----------------|-----------------|  
|**App-V Virtual Environment Results**|Displays information about a specified virtual environment that is in a specified state for a specified collection.|  
|**App-V Virtual Environment Results For Asset**|Displays information about a specified virtual environment for a specified asset. It also shows any deployment types for the specified virtual environment.|  
|**App-V Virtual Environment Status**|Displays compliance information for a specified virtual environment for a specified collection.|  
|**Computers with a specific virtual application**|Displays a summary of computers that have the specified App-V application shortcut as created using the Application Virtualization Management Sequencer.|  
|**Computers with a specific virtual application package**|Displays a summary of computers that have the specified App-V application package.|  
|**Count of all instances of virtual application packages**|Display a count of detected App-V application packages.|  
|**Count of all instances of virtual applications**|Display a count of detected App-V applications.|  



## Volume Purchase Programs - Apple

|Report name|Description|  
|-----------------|-----------------|  
|**Apple Volume Purchase Program apps for iOS with license counts**|Displays all iPhone, iPad, and iPod Touch applications licensed through Apple's Volume Purchase Program. This report also includes the total licenses purchased, and licenses consumed per application.|  



## Vulnerability Assessment

|Report name|Description|  
|-----------------|-----------------|  
|**Vulnerability Assessment Overall Report**|Identifies security, administrative, and compliance vulnerabilities for a specific computer|  



## Wake On LAN  

|Report name|Description|  
|-----------------|-----------------|  
|**All computers targeted for Wake On LAN activity**|Specify the type of deployment to display a list of computers targeted for Wake on LAN activity.|  
|**All objects pending wake-up activity**|Displays objects that are scheduled for wakeup.|  
|**All sites that are enabled for Wake On LAN**|Displays a list of all sites in the hierarchy that are enabled for Wake On LAN.|  
|**Errors received while sending wake-up packets for a defined period**|Displays errors received while sending wake-up packets to computers for a defined period.|  
|**History of Wake On LAN activity**|Displays a history of the wakeup activity that has occurred since a certain period.|  
|**Wake-Up Proxy Deployment State Details**|Displays information about the deployment status of Wake-Up Proxy for each device in a specified collection.|  
|**Wake-Up Proxy Deployment State Summary**|Displays a summary of the deployment status of wake-up proxy for a specified collection.|  
