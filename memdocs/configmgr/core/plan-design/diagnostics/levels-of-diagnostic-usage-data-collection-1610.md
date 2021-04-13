---
title: "Diagnostic data for 1610"
titleSuffix: "Configuration Manager"
description: "Learn about the levels of diagnostics and usage data that Configuration Manager version 1610 collects."
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# Levels of diagnostic usage data collection for version 1610 of Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager version 1610 collects three levels of diagnostics and usage data: **Basic**, **Enhanced**, and **Full**. By default, this feature is set at the Enhanced level. The following sections provide additional detail about data that each level collects.

Changes from previous versions are noted with ***[New]***, ***[Updated]***, ***[Removed]***, or ***[Moved]***.


> [!IMPORTANT]
>  Configuration Manager does not collect site codes, sites names, IP addresses, user names, computer names, physical addresses, or email addresses on the Basic or Enhanced levels. Any collection of this information on the Full level is not purposeful, that is, potentially included in advanced diagnostic information like log files or memory snapshots. Microsoft will not use this information to identify you, contact you, or develop advertising.

##  <a name="bkmk_change"></a> How to change the level
 Administrators who have a role-based administrative scope that includes **Modify** permissions on the **Site** object class can change the level of data collected in the Diagnostics and Usage Data settings in the Configuration Manager console.

Beginning with version 1610, you change the data collection level from within the console by navigating to **Administration** > **Overview** > **Site Configuration** > **Sites**. Open **Hierarchy Settings**, and then select the data level you want to use.  

##  <a name="bkmk_level1"></a> Level 1 - Basic
 The Basic level includes data about your hierarchy, data that's required to help improve your installation or upgrade experience, and data that helps determine the Configuration Manager updates that are applicable for your hierarchy.

 for Configuration Manager version 1610, this level includes the following:


- Setup Information:
  - Build, install type, language packs, features that you enabled  

  - Update pack deployment status and errors, download progress, and prerequisite errors    

  - Version of post-upgrade script

  - Use of update fast ring

  - ***[New]*** Pre-release use, setup media type, branch type

  - ***[New]*** Software Assurance expiration date

- Database performance metrics (replication processing information, top SQL Server stored procedures by processor and disk usage)

- Basic database configuration (processors, cluster configuration, and configuration of distributed views)

- Configuration Manager database schema (hash of all object definitions)

- Count of Configuration Manager client versions and operating system versions

- Count of operating systems for managed devices and policies set by the Exchange Connector

- Count of client languages and locales

- Count of Windows 10 devices by branch and build

- Basic Configuration Manager site hierarchy data (site list, type, version, status, client count, and time zone)

- Basic site system server information (site system roles used, Internet and SSL status, operating system, processors, and physical or virtual machine)

- Basic user discovery statistics (user discovery count and minimum/maximum/average group sizes)

- Basic Endpoint Protection information (antimalware client versions)

- Basic application and deployment type counts (total apps, total apps with multiple deployment types, total apps with dependencies, total superseded apps, and count of deployment technologies in use)

- Basic operating system deployment (OSD) counts (images)

- Distribution point and management point types and basic configuration information (protected, prestaged, PXE, multicast, SSL state, pull/peer distribution points, MDM-enabled, SSL-enabled, etc.)

- Telemetry stats (when run, runtime, errors)

- Configured telemetry level, mode (online or offline), and fast update configuration

- Use of Network Discovery (enabled or disabled)
- Admin Console:

  - Statistics about console connections (operating system version, language, SKU and architecture, system memory, logical processor count, connect site ID, installed .NET versions, and console language packs)

- SQL Server version, service pack level, edition, collation ID, and character set


##  <a name="bkmk_level2"></a> Level 2 - Enhanced
The Enhanced level is the default after setup finishes. This level includes data that's collected in the Basic level and feature-specific data (frequency and duration of use), Configuration Manager client settings (component name, state, and certain settings like polling intervals), and basic information about software updates.

This level is recommended because it provides Microsoft with the minimum data that's required to make useful improvements in future versions of products and services. This level does not collect object names (sites, users, computer, or objects), details of security-related objects, or vulnerabilities like counts of systems that require software updates.

For Configuration Manager version 1610, this level includes the following:

-   **Application management:**  

    -    Basic usage/targeting information for deployment types that are used within the organization (user versus device targeted, required versus available, and universal apps)  

    -   Application deployment information (install/uninstall, requires approval, user interaction enabled/disabled, dependency, and supersedence)  

    -   Available application request statistics  

    -   Count of packages by type  

    -   Count of application applicability by operating system  

    -   Count of package/program deployments  

    -   Count of App-V environments and deployment properties  

    -   Count of Windows 10 licensed application licenses  

    -   Minimum/maximum/average number of application deployments per user/device per time period

    -   Maintenance window type and duration  

    -  Application policy size and complexity statistics

    - ***[Updated]*** Count of Windows Store for Business apps and sync statistics (including summarized types of apps, licensed app status, and number of online and offline licensed apps)  

    - Boundary group statistics (how many fast, how many slow, and count per group)

    - MSI configuration options and counts

    - App requirements (count of built-in conditions is referenced by deployment technology)

    - App supersedence, maximum depth of chain

    - Universal Data Access (UDA) usage, how created

    - ***[New]*** Application approval statistics and usage frequency



-   **Client:**  

    -   List/count of enabled client agents  

    -   Count of client installations from each source location type  

    -   Count of client installation failures  

    -  ***[Updated]*** Client auto-upgrade: deployment configuration including client piloting and exclusion usage (extended interoperability client)

    -  Client health statistics and top issue summary

    - BIOS age in years

    - Operating system age in months

    - Count of Software Center actions

    - Active Management Technology (AMT) client version

    - Client deployment download errors

    - Client notification operation action status (how many times each is run, max number of targeted clients, and average success rate)

    - Deployment methods used for client and count of clients per deployment method

    - Client cache size configuration

    - ***[New]***  Number of hardware inventory classes, software inventory rules, and file collection rules




- **Cloud Services:**

  - Count of collections synced to Operations Management Suite

  -  Whether the Operations Management Suite cloud connector is enabled

  - ***[New]*** Configuration and usage statistics of Cloud Management Gateway

  - ***[New]*** Count of Upgrade Analytics Connectors




- **Collections:**

    -  Collection evaluation statistics (query time, assigned versus unassigned counts, counts by type, ID rollover, and rule usage)

    - Collections without a deployment

    - Collection ID usage (not running out of IDs)



-   **Compliance settings:**  

    -   Count of configuration items by type  

    -   Basic configuration baseline information (count, number of deployments, and number of references)  

    -   Count of deployments that reference built-in settings (now capturing remediate setting)  

    -   Count of rules and deployments created for custom settings (now capturing remediate setting)  
    -   Count of deployed Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certificate (.pfx), and Compliance Policy templates

    -  Count of SCEP certificate, VPN, Wi-Fi, certificate (.pfx) and Compliance Policy deployments by platform

    - Passport for Work policy (created, deployed)



-   **Content:**  

    -   Count of boundaries by type  

    -   Boundary group information (count of boundaries and site systems that are assigned to each boundary group)  

    - ***[New]*** Boundary group relationships and fallback configuration

    -   Distribution point group information (count of packages and distribution points that are assigned to each distribution point group)  

    -   Distribution point configuration information (use of branch cache and distribution point monitoring)  

    -   Distribution Manager configuration information (threads, retry delay, number of retries, and pull distribution point settings)  

    - ***[New]*** Count of peer cache clients and usage statistics

    - ***[New]*** Client content download statistics


-   **Endpoint Protection:**  

    -   Endpoint Protection antimalware and Windows Firewall policy usage (number of unique policies assigned to group)<br /><br /> This does not include any information about the settings included in the policy.  

    -   Endpoint Protection deployment errors (count of Endpoint Protection policy deployment error codes)  

    -   Count of collections that are selected to appear in Endpoint Protection dashboard  

    -   Count of alerts that are configured for Endpoint Protection feature  

    -   Endpoint Policies (count of policies and whether policies are deployed)


- **Migration:**

  -   Count of migrated objects (use of migration wizard)



-   **Mobile device management (MDM):**  

    -   ***[Updated]*** Count of issued mobile device actions: lock, pin rest, wipe, retire, and Sync now commands  

    -   Count of mobile devices that are managed by Configuration Manager and Microsoft Intune and how they were enrolled (bulk, user-based)  

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

    -   Counts of task sequence step usage

    - ***[New]*** Count of edition upgrade policies



-   **Site updates:**

    - Versions of installed Configuration Manager hotfixes




-   **Software Updates:**  

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

    -   Count of deployed Microsoft 365 updates  

    -   Classifications that are synced by Software Update Point

    -   Software update point load balancing statistics

    -  ***[New]*** Configuration of Windows 10 express updates




-   **SQL/performance data:**  

    -   Count of largest database tables  

    -   ***[Updated]*** SQL Server Always On availability group replica information, usage, and health status

    -  SQL Server change tracking retention period

    - Discovery types, enabled and schedule (full, incremental)

    - Discovery operational statistics (count of objects found)

    - SQL Server change tracking performance issues, retention period, and auto-cleanup state



- **Miscellaneous**

    - Count of sites with Wake on LAN (WOL)

    - ***[New]*** Reporting usage and performance statistics  



##  <a name="bkmk_level3"></a> Level 3 - Full
The Full level includes all data in the Basic and Enhanced levels. It also includes additional information about Endpoint Protection, update compliance percentages, and software update information.  This level can also include advanced diagnostic information like system files and memory snapshots which might include personal information that existed in memory or log files at the time of capture.

For Configuration Manager version 1610, this level includes the following:

-   Collection evaluation and refresh statistics

-   Endpoint Protection health summary (including count of protected, at risk, unknown, and unsupported clients)

-   Endpoint Protection policy configuration

-   Software update deployment information (percentage of deployments that are targeted with client versus UTC time, required versus optional versus silent, and reboot suppression)

-   Overall compliance of software update deployments

-   Automatic deployment rule evaluation schedule information

-   Software update deployment error codes and counts

-   Minimum/maximum/average number of inactive clients in software update deployment collections

-   Count of groups that have expired software updates

-   Minimum/maximum/average number of software updates per package

-   Software update scan success percentages

-   Minimum/maximum/average number of hours since last software update scan

-    Software update products synced by Software Update Point
-    Compliance Settings: SCEP, VPN, Wi-Fi and Compliance Policy template configuration details

-    Type of EAS Conditional Access policies (block or quarantine) for devices that Intune manages

-   Top 50 CPUs in the environment

-   DCM config pack for Configuration Manager usage

-   MSI product code (common apps that customers deploy)

-   ATP Health Summary

-   Detailed client deployment installation errors

- ***[New]*** Windows Store for Business application details (non-aggregate list of synced applications including AppID, online state or offline state, and total purchased license counts)
