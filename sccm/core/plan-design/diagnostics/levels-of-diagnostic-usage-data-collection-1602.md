---
title: "Diagnostic data for 1602"
titleSuffix: "Configuration Manager"
description: "Learn about the levels of diagnostics and usage data that System Center Configuration Manager version 1602 collects."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1210a1ca-78c7-4d17-81cf-ac1bc5c5cf3e
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
translation.priority.ht:
  - cs-cz
  - de-de
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
# Levels of diagnostic usage data collection for version 1602 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager version 1602 collects three levels of diagnostics and usage data: **Basic**, **Enhanced**, and **Full**. By default, this feature is set at the Enhanced level. The following sections provide additional detail about data that each level collects.

Changes from previous versions are noted with ***[New]*** or ***[Updated]***.

> [!IMPORTANT]
>  Configuration Manager does not collect site codes, sites names, IP addresses, user names, computer names, physical addresses, or email addresses on the Basic or Enhanced levels. Any collection of this information on the Full level is not purposeful, that is, potentially included in advanced diagnostic information like log files or memory snapshots. Microsoft will not use this information to identify you, contact you, or develop advertising.

##  <a name="bkmk_change"></a> How to change the level
 Administrators who have a role-based administrative scope that includes **Modify** permissions on the **Site** object class can change the level of data collected in the Diagnostics and Usage Data settings in the Configuration Manager console.


  To do so, in the console, go to the backstage tab (the upper left tab with the dropdown arrow), select **Usage Data**, and then select the data level that you want to use.  

##  <a name="bkmk_level1"></a> Level 1 - Basic
 The Basic level includes data about your hierarchy, data that's required to help improve your installation or upgrade experience, and data that helps determine the Configuration Manager updates that are applicable for your hierarchy.

 Beginning with System Center Configuration Manager version 1602, this level includes the following:


 -   Setup Information:
 	- Build, install type, language packs, features that you enabled  

 	- ***[Updated]***  Update pack deployment status and errors, download progress, and prerequisite errors 	

 	- ***[New]*** Version of post-upgrade script

 	- ***[New]*** Use of update fast ring

-   Database performance metrics (replication processing information, top SQL Server stored procedures by processor, and disk usage)

-   Basic database configuration (processors, cluster configuration, and configuration of distributed views)

-   Configuration Manager database schema (hash of all object definitions)

-   Count of Configuration Manager client versions and operating system versions

-   Count of operating systems for managed devices and policies set by the Exchange Connector

-   Count of client languages and locales

-   Count of Windows 10 devices by branch and build

-   Basic Configuration Manager site hierarchy data (site list, type, version, status, client count, and time zone)

-   Basic site system server information (site system roles used, Internet and SSL status, operating system, processors, and physical or virtual machine)

-   Basic user discovery statistics (user discovery count and minimum/maximum/average group sizes)

-   Basic Endpoint protection information (antimalware client versions)

-   Basic application and deployment type counts (total apps, total apps with multiple deployment types, total apps with dependencies, total superseded apps, and count of deployment technologies in use)

-   Basic operating system deployment (OSD) counts (images)

-   Distribution point and management point types and basic configuration information (protected, prestaged, PXE, multicast, SSL state, pull/peer distribution points, MDM-enabled, SSL-enabled, etc.)

-   Telemetry stats (when run, runtime, and errors)

- ***[New]*** Configured telemetry level, mode (online or offline), and fast update configuration

- ***[New]*** Use of Network Discovery (enabled or disabled)
- ***[New]*** Admin Console:

	-  Statistics about console connections (opeating system version, language, SKU and architecture, system memory, logical processor count, connect site ID, installed .NET versions, and console language packs)

##  <a name="bkmk_level2"></a> Level 2 - Enhanced
The Enhanced level is the default after setup finishes. This level includes data that's collected in the Basic level, feature-specific data (frequency and duration of use), Configuration Manager client settings (component name, state, and certain settings like polling intervals), and basic information about software updates.

This level is recommended because it provides Microsoft with the minimum data that's required to make useful improvements in future versions of products and services. This level does not collect object names (sites, users, computer, or objects), details about security-related objects, or vulnerabilities like counts of systems that require software updates.

Beginning with System Center Configuration Manager version 1602, this level includes the following:

-   **Application management:**

  -   ***[Updated]*** Basic usage/targeting information for deployment types that are used within the organization (user versus device targeted, required versus available, and universal apps)  

  -  ***[Updated]*** Application deployment information (install/uninstall, requires approval, user interaction enabled/disabled, dependency, and supersedence)  

  -   Available application request statistics  

  -   Count of packages by type  

  -   Count of application applicability by operating system  

  -   Count of package/program deployments  

  -   Count of App-V environments and deployment properties  

  -   Count of Windows 10 licensed application licenses  

  -   ***[Updated]*** Minimum/maximum/average number of application deployments per user/device per time period

  -   Maintenance window type and duration  

  -  ***[New]*** Application policy size and complexity statistics

-   **Client:**

    -   List/count of enabled client agents

    -   Count of client installations from each source location type

    -   Count of client installation failures

-   **Compliance settings:**

    -   Count of configuration items by type

    -   Basic configuration baseline information (count, number of deployments, and number of references)

    -   Count of deployments that reference built-in settings (value of setting is not captured)

    -   Count of rules and deployments that are created for custom settings

    -   ***[Updated]*** Count of deployed Simple Certificate Enrollment Protocol, VPN, Wi-Fi, certificate (.pfx), and Compliance Policy templates   

    -  ***[New]*** Count of Simple Certificate Enrollment Protocol (SCEP) certificate, VPN, Wi-Fi, certificate (.pfx) and Compliance Policy deployments by platform

-   **Content:**

    -   Count of boundaries by type

    -   Boundary group information (count of boundaries and site systems that are assigned to each boundary group)

    -   Distribution point group information (count of packages and distribution points that are assigned to each distribution point group)

    -   Distribution point configuration information (use of branch cache and distribution point monitoring)

    -   Distribution Manager configuration information (threads, retry delay, number of retries, and pull distribution point settings)

-   **Endpoint Protection:**

    -   Endpoint Protection antimalware and Windows Firewall policy usage (number of unique policies assigned to group)<br /><br />This does not include any information about settings that are included in the policy.

    -   Endpoint Protection deployment errors (count of Endpoint Protection policy deployment error codes)

    -   Count of collections that are selected to appear in endpoint protection dashboard

    -   Count of alerts that are configured for the Endpoint Protection feature

-   **Mobile application management (MAM):**

    -   Count of MAM-enabled Office applications, line-of-business applications, and policies by operating system

    -   Count of MAM application/policy deployments

    -   Count of rules that are created per MAM setting

-   **Mobile device management (MDM):**

    -   Count of issued mobile device actions: lock, pin rest, wipe, and retire commands

    -   Count of mobile devices that are managed by Configuration Manager and Microsoft Intune and how they were enrolled (bulk or user-based)

    -   Mobile device polling schedule and statistics for mobile device check-in duration

    -   Count of mobile device policies

    -   Count of users who have multiple enrolled mobile devices

-   **Microsoft Intune troubleshooting:**

    -   Count and size of state, status, inventory, RDR, DDR, UDX, Tenant state, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM, and compliance messages that are downloaded from Microsoft Intune

    -   Count and size of device actions (wipe, retire, lock), telemetry, and data messages that are replicated to Microsoft Intune

    -   Full and delta user synchronization statistics for Microsoft Intune

-   **On-premises mobile device management (MDM):**

    -   Deployment success/failure statistics for on-premises MDM application deployments

    -   Count of Windows 10 bulk enrollment packages and profiles

-   **Operating system deployment:**

    -   Count of boot images, drivers, driver packages, multicast-enabled distribution points, PXE-enabled distribution points, and task sequences

-   **Software updates:**

    -   Total/average number of collections that have software update deployments and the maximum/average number of deployed updates

    -   Number of automatic deployment rules that are tied to synchronization

    -   Number of automatic deployment rules that create new or add updates to an existing group

    -   Available and deadline deltas that are used in automatic deployment rules

    -   Average and maximum number of assignments per update

    -   Count of updates that are created and deployed with System Center Update Publisher

    -   Count of update groups and assignments

    -   Count of update packages and the maximum/minimum/average number of distribution points that are targeted with packages

    -   Number of update groups and minimum/maximum/average number of updates per group

    -   Number of updates and percentage of updates that are deployed, expired, superseded, downloaded, and contain EULAs

    -   Update scan error codes and machine count

    -   Client update evaluation and scan schedules

    -   Software update point synchronization schedule

    -   Number of automatic deployment rules that have multiple deployments

    -   Configurations that are used for active Windows 10 servicing plans

    -   Windows 10 dashboard content versions

    -   Count of Windows 10 clients that use Windows Update for Business

    -   Cluster patching statistics

    -   Count of deployed Office 365 updates

    -   ***[New]*** Classifications that are synced by Software Update Point

-   **SQL/performance data:**

    -   Count of largest database tables

    -   SQL Always-On replica information

    -   Count of collections by type

    -   ***[Updated]*** Collection evaluation statistics (query time, assigned versus unassigned counts, counts by type, ID rollover, and rule usage)

    - ***[New]***	SQL change tracking retention period

-   ***[New] Site updates:***

    - ***[New]*** Versions of installed Configuraton Manager hotfixes

##  <a name="bkmk_level3"></a> Level 3 - Full
The Full level includes all data in the Basic and Enhanced levels. It also includes additional information about Endpoint Protection, update compliance percentages, and software update information. This level can also include advanced diagnostic information like system files and memory snapshots, which might include personal information that existed in memory or log files at the time of capture.

Beginning with System Center Configuration Manager version 1602, this level includes the following:

-   Collection evaluation and refresh statistics

-   Endpoint Protection health summary (including count of protected, at risk, unknown, and unsupported clients)

-   Endpoint Protection policy configuration

-   Software update deployment information (percentage of deployments targeted with client versus UTC time, required versus optional versus silent, and reboot suppression)

-   Overall compliance of software update deployments

-   Automatic deployment rule evaluation schedule information

-   Number of clients that have network access protection policies

-   Software update deployment error codes and counts

-   Minimum/maximum/average number of inactive clients in software update deployment collections

-   Count of groups that have expired software updates

-   Minimum/maximum/average number of software updates per package

-   Software update scan success percentages

-   Minimum/maximum/average number of hours since last software update scan

-   ***[New]*** Software update products synced by Software Update Point
-   ***[New]*** Compliance Settings: SCEP, VPN, Wi-Fi and Compliance Policy template configuration details

-   ***[New]*** Type of EAS Conditional Access policies (block or quarantine) for Intune-managed devices
