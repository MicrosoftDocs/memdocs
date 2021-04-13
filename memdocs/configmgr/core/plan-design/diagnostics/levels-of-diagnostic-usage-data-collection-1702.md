---
title: "Diagnostic data for 1702"
titleSuffix: "Configuration Manager"
description: "Learn about the levels of diagnostics and usage data that Configuration Manager version 1702 collects."
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: d43ab033-2902-4681-8716-b4b17a6df372
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# Levels of diagnostic usage data collection for version 1702 of Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager version 1702 collects three levels of diagnostics and usage data: **Basic**, **Enhanced**, and **Full**. By default, this feature is set at the Enhanced level. The following sections provide additional detail about data that each level collects.

Changes from previous versions are noted with ***[New]***, ***[Updated]***, ***[Removed]***, or ***[Moved]***.


> [!IMPORTANT]
>  Configuration Manager does not collect site codes, sites names, IP addresses, user names, computer names, physical addresses, or email addresses on the Basic or Enhanced levels. Any collection of this information on the Full level is not purposeful, that is, potentially included in advanced diagnostic information like log files or memory snapshots. Microsoft will not use this information to identify you, contact you, or develop advertising.



##  <a name="bkmk_change"></a> How to change the level
 Administrators who have a role-based administrative scope that includes **Modify** permissions on the **Site** object class can change the level of data collected in the Diagnostics and Usage Data settings in the Configuration Manager console.

You change the data collection level from within the console by navigating to **Administration** > **Overview** > **Site Configuration** > **Sites**. Open **Hierarchy Settings**, and then select the data level you want to use.  



##  <a name="bkmk_level1"></a> Level 1 - Basic
The Basic level includes data about your hierarchy, data that's required to help improve your installation or upgrade experience, and data that helps determine the Configuration Manager updates that are applicable for your hierarchy.

For Configuration Manager version 1702, this level includes the following:

- Admin Console:
   - Statistics about console connections (operating system version, language, SKU and architecture, system memory, logical processor count, connect site ID, installed .NET versions, and console language packs)

- Basic application and deployment type counts (total apps, total apps with multiple deployment types, total apps with dependencies, total superseded apps, and count of deployment technologies in use)

- Basic Configuration Manager site hierarchy data (site list, type, version, status, client count, and time zone)

- Basic database configuration (processors, cluster configuration, and configuration of distributed views)

- ***[Updated]*** Basic discovery statistics (discovery count and minimum/maximum/average group sizes) including when the site is running entirely with Azure Active Directory Services.

- Basic Endpoint Protection information (antimalware client versions)

- Basic operating system deployment (OSD) counts (images)

- Basic site system server information (site system roles used, Internet and SSL status, operating system, processors, and physical or virtual machine)

- Configuration Manager database schema (hash of all object definitions)

- Configured telemetry level, mode (online or offline), and fast update configuration

- Count of client languages and locales

- Count of Configuration Manager client versions and operating system versions

- Count of operating systems for managed devices and policies set by the Exchange Connector

- Count of Windows 10 devices by branch and build

- Database performance metrics (replication processing information, top SQL Server stored procedures by processor and disk usage)

- Distribution point and management point types and basic configuration information (protected, prestaged, PXE, multicast, SSL state, pull/peer distribution points, MDM-enabled, SSL-enabled, etc.)

- Setup Information:
     - Build, install type, language packs, features that you enabled   

     - Pre-release use, setup media type, branch type

     - Software Assurance expiration date      

     - Update pack deployment status and errors, download progress, and prerequisite errors 

     - Use of update fast ring

     - Version of post-upgrade script

- SQL Server version, service pack level, edition, collation ID, and character set

- Telemetry stats (when run, runtime, errors)

- Use of Network Discovery (enabled or disabled)




##  <a name="bkmk_level2"></a> Level 2 - Enhanced
The Enhanced level is the default after setup finishes. This level includes data that's collected in the Basic level and feature-specific data (frequency and duration of use), Configuration Manager client settings (component name, state, and certain settings like polling intervals), and basic information about software updates.

This level is recommended because it provides Microsoft with the minimum data that's required to make useful improvements in future versions of products and services. This level does not collect object names (sites, users, computer, or objects), details of security-related objects, or vulnerabilities like counts of systems that require software updates.

For Configuration Manager version 1702, this level includes the following:

- **Application management:**  

   - App requirements (count of built-in conditions is referenced by deployment technology)

   - App supersedence, maximum depth of chain

   - Application approval statistics and usage frequency

   - ***[Updated]*** Application deployment information (use of install versus uninstall, requires approval, user interaction enabled/disabled, dependency, supersedence, and usage count of install behavior feature)  

   - Application policy size and complexity statistics

   - Available application request statistics

   - ***[New]*** Basic configuration information for packages and programs (deployment options and program flags)

   - Basic usage/targeting information for deployment types that are used within the organization (user versus device targeted, required versus available, and universal apps)

   - Boundary group statistics (how many fast, how many slow, and count per group)

   - Count of App-V environments and deployment properties

   - Count of application applicability by operating system  

   - ***[New]*** Count of applications that are referenced by a task sequence

   - Count of packages by type  

   - Count of package/program deployments  

   - Count of Windows 10 licensed application licenses  

   - Count of Windows Store for Business apps and sync statistics (including summarized types of apps, licensed app status, and number of online and offline licensed apps)  

   - Maintenance window type and duration  

   - Minimum/maximum/average number of application deployments per user/device per time period

   - ***[New]*** Most common application installation error codes by
   deployment technology

   - MSI configuration options and counts

   - ***[New]*** Statistics on end-user interaction with notification for required software deployments   

   - Universal Data Access (UDA) usage, how created




- **Client:**  

   - Active Management Technology (AMT) client version

   - BIOS age in years

   - Client auto-upgrade: deployment configuration including client piloting and exclusion usage (extended interoperability client)

   - Client cache size configuration

   - Client deployment download errors

   - Client health statistics and top issue summary

   - Client notification operation action status (how many times each is run, max number of targeted clients, and average success rate)
   - Count of client installations from each source location type  

   - Count of client installation failures  

   - ***[New]*** Count of devices virtualized by Hyper-V or Azure  

   - Count of Software Center actions   

   - ***[New]*** Count of UEFI-enabled devices

   - Deployment methods used for client and count of clients per deployment method

   - List/count of enabled client agents  

   - Operating system age in months

   - Number of hardware inventory classes, software inventory rules, and file collection rules

   - ***[New]*** Statistics for device health attestation including most common error codes, number of on-premises servers, and counts of devices in various states.



- **Cloud Services:**

  - Configuration and usage statistics of Cloud Management Gateway

  - ***[New]*** Count of clients joined to Azure Active Directory Services

  - Count of collections synced to Operations Management Suite

  - Count of Upgrade Analytics Connectors

  - Whether the Operations Management Suite cloud connector is enabled




- **Collections:**

    - Collection ID usage (not running out of IDs)

    - Collection evaluation statistics (query time, assigned versus unassigned counts, counts by type, ID rollover, and rule usage)

    - Collections without a deployment




- **Compliance settings:**  

    - Basic configuration baseline information (count, number of deployments, and number of references)  

    - Count of configuration items by type  

    - Count of deployments that reference built-in settings (now capturing remediate setting)  

    - Count of rules and deployments created for custom settings (now capturing remediate setting)  
    -  Count of deployed Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certificate (.pfx), and Compliance Policy templates

    - Count of SCEP certificate, VPN, Wi-Fi, certificate (.pfx) and Compliance Policy deployments by platform

    - Passport for Work policy (created, deployed)



- **Content:**  

    - Boundary group information (count of boundaries and site systems that are assigned to each boundary group)  

    - Boundary group relationships and fallback configuration

    - Client content download statistics

    - Count of boundaries by type  

    - Count of peer cache clients and usage statistics

    - Distribution Manager configuration information (threads, retry delay, number of retries, and pull distribution point settings)  

    - Distribution point configuration information (use of branch cache and distribution point monitoring)

    - Distribution point group information (count of packages and distribution points that are assigned to each distribution point group)  



- **Endpoint Protection:**  

   - Endpoint Policies (count of policies and whether policies are deployed)

   - Count of alerts that are configured for Endpoint Protection feature  

   - Count of collections that are selected to appear in Endpoint Protection dashboard  

   - Endpoint Protection deployment errors (count of Endpoint Protection policy deployment error codes)  

   - Endpoint Protection antimalware and Windows Firewall policy usage (number of unique policies assigned to group)<br /><br /> This does not include any information about the settings included in the policy.  



- **Migration:**

  - Count of migrated objects (use of migration wizard)



- **Mobile device management (MDM):**  

    - Count of issued mobile device actions: lock, pin rest, wipe, retire, and Sync now commands

    - Count of mobile device policies  

    - Count of mobile devices that are managed by Configuration Manager and Microsoft Intune and how they were enrolled (bulk, user-based)  

    - Count of users who have multiple enrolled mobile devices  

    - Mobile device polling schedule and statistics for mobile device check-in duration  




- **Microsoft Intune troubleshooting:**

    - Count and size of device actions (wipe, retire, lock), telemetry, and data messages that are replicated to Microsoft Intune

    - Count and size of state, status, inventory, RDR, DDR, UDX, Tenant state, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM, and compliance messages that are downloaded from Microsoft Intune

    - Full and delta user synchronization statistics for Microsoft Intune



- **On-premises mobile device management (MDM):**  

    - Count of Windows 10 bulk enrollment packages and profiles  

    - Deployment success/failure statistics for on-premises MDM application deployments  




- **Operating system deployment:**  

    - Count of boot images, drivers, driver packages, multicast-enabled distribution points, PXE-enabled distribution points, and task sequences  

    - Count of edition upgrade policies

    - Counts of task sequence step usage



- **Site updates:**

    - Versions of installed Configuration Manager hotfixes



- **Software Updates:**  

    - Available and deadline deltas that are used in automatic deployment rules  

    - Average and maximum number of assignments per update  

    - Client update evaluation and scan schedules  

    - Classifications that are synced by Software Update Point

    - Cluster patching statistics  

    - Configuration of Windows 10 express updates

    - Configurations that are used for active Windows 10 servicing plans  

    - Count of deployed Microsoft 365 updates  

    - Count of update groups and assignments  

    - Count of update packages and the maximum/minimum/average number of distribution points that are targeted with packages  

    - Count of updates that are created and deployed with System Center Update Publisher  

    - Count of Windows 10 clients that use Windows Update for Business  

    - Number of automatic deployment rules that are tied to synchronization  

    - Number of automatic deployment rules that create new or add updates to an existing group  

    - Number of automatic deployment rules that have multiple deployments  
    - Number of update groups and minimum/maximum/average number of updates per group  

    - Number of updates and percentage of updates that are deployed, expired, superseded, downloaded, and contain EULAs  

    - Software update point load balancing statistics

    - Software update point synchronization schedule  

    - Total/average number of collections that have software update deployments and the maximum/average number of deployed updates  

    - Update scan error codes and machine count  

    - Windows 10 dashboard content versions  



- **SQL/performance data:**  

    - ***[New]*** Configuration and duration of site summarization

    - Count of largest database tables  

    - Discovery operational statistics (count of objects found)

    - Discovery types, enabled and schedule (full, incremental)

    - SQL Server Always On availability group replica information, usage, and health status

    - SQL Server change tracking performance issues, retention period, and auto-cleanup state

    - SQL Server change tracking retention period

    - ***[New]*** State and status message performance statistics including most common and most expensive message types



- **Miscellaneous**

    - ***[New]*** Configuration of Data Warehouse Service Point including synchronization schedule and average time

    - Count of sites with Wake on LAN (WOL)

    - Reporting usage and performance statistics  



##  <a name="bkmk_level3"></a> Level 3 - Full
The Full level includes all data in the Basic and Enhanced levels. It also includes additional information about Endpoint Protection, update compliance percentages, and software update information.  This level can also include advanced diagnostic information like system files and memory snapshots which might include personal information that existed in memory or log files at the time of capture.

For Configuration Manager version 1702, this level includes the following:

- Automatic deployment rule evaluation schedule information

- ATP Health Summary

- Collection evaluation and refresh statistics

- Compliance Settings: SCEP, VPN, Wi-Fi and Compliance Policy template configuration details
Count of groups that have expired software updates

- DCM config pack for Configuration Manager usage

- Detailed client deployment installation errors
- Endpoint Protection health summary (including count of protected, at risk, unknown, and unsupported clients)

- Endpoint Protection policy configuration

- ***[New]*** List of processes configured with installation behavior for applications

- Minimum/maximum/average number of hours since last software update scan

- Minimum/maximum/average number of inactive clients in software update deployment collections

- Minimum/maximum/average number of software updates per package

- MSI product code (common apps that customers deploy)

- Overall compliance of software update deployments

- Software update deployment error codes and counts

- Software update deployment information (percentage of deployments that are targeted with client versus UTC time, required versus optional versus silent, and reboot suppression)

- Software update products synced by Software Update Point

- Software update scan success percentages

- Top 50 CPUs in the environment

- Type of EAS Conditional Access policies (block or quarantine) for devices that Intune manages

- Windows Store for Business application details (non-aggregate list of synced applications including AppID, online state or offline state, and total purchased license counts)
