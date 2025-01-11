---
title: Diagnostic and usage data for 1802
titleSuffix: Configuration Manager
description: Learn about the levels of diagnostics and usage data collected in version 1802.
ms.date: 05/13/2018
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Levels of diagnostic usage data collection for version 1802 of Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager version 1802 collects three levels of diagnostics and usage data: **Basic**, **Enhanced**, and **Full**. By default, this feature is set at the Enhanced level. The following sections provide additional detail about data collected at each level.

Changes from previous versions are noted with ***[New]***, ***[Updated]***, ***[Removed]***, or ***[Moved]***.


> [!IMPORTANT]
>  Configuration Manager doesn't collect site codes, sites names, IP addresses, user names, computer names, physical addresses, or email addresses on the Basic or Enhanced levels. Any collection of this information on the Full level is not purposeful. It is potentially included in advanced diagnostic information like log files or memory snapshots. Microsoft doesn't use this information to identify you, contact you, or develop advertising.



##  <a name="bkmk_change"></a> How to change the level
 Administrators who have a role-based administrative scope that includes **Modify** permissions on the **Site** object class can change the level of data collected in the Diagnostics and Usage Data settings in the Configuration Manager console.

You change the data collection level from within the console by navigating to **Administration** > **Overview** > **Site Configuration** > **Sites**. Open **Hierarchy Settings**, and then select the data level you want to use.  



##  <a name="bkmk_level1"></a> Level 1 - Basic
The Basic level includes data about your hierarchy, data that's required to help improve your installation or upgrade experience, and data that helps determine the Configuration Manager updates that are applicable for your hierarchy.

For Configuration Manager version 1802, this level includes the following data:

- Statistics about Configuration Manager console connections: OS version, language, SKU and architecture, system memory, logical processor count, connect site ID, installed .NET versions, and console language packs

- Basic application and deployment type counts: total apps, total apps with multiple deployment types, total apps with dependencies, total superseded apps, and count of deployment technologies in use

- Basic Configuration Manager site hierarchy data: site list, type, version, status, client count, and time zone

- Basic database configuration: processors, cluster configuration, and configuration of distributed views

- Basic discovery statistics: discovery count, minimum/maximum/average group sizes, and when the site is running entirely with Microsoft Entra services

- Basic Endpoint Protection information about antimalware client versions

- Basic OS deployment counts of images

- Basic site system server information: site system roles used, internet and SSL status, OS, processors, physical or virtual machine, and usage of site server high availability

- Configuration Manager database schema (hash of all object definitions)

- Configured telemetry level, online or offline mode, and fast update configuration

- Count of client languages and locales

- Count of Configuration Manager client versions, OS versions, and Office versions

- Count of operating systems for managed devices and policies set by the Exchange Connector

- Count of Windows 10 devices by branch and build

- ***[Moved]*** Count of Windows 10 clients that use Windows Update for Business  

- Database performance metrics: replication processing information, top SQL Server stored procedures by processor, and disk usage

- Distribution point and management point types and basic configuration information: protected, prestaged, PXE, multicast, SSL state, pull/peer distribution points, MDM-enabled, and SSL-enabled

- Hashed list of extensions to admin console property pages and wizards

- Setup Information:
     - Build, install type, language packs, features that you enabled   

     - Pre-release use, setup media type, branch type

     - Software Assurance expiration date      

     - Update pack deployment status and errors, download progress, and prerequisite errors 

     - Use of update fast ring

     - Version of post-upgrade script

- SQL Server version, service pack level, edition, collation ID, and character set

- Telemetry statistics: when run, runtime, errors

- Whether network discovery is enabled or disabled

- ***[Moved]*** Count of clients joined to Microsoft Entra ID

- ***[New]*** Count of phased deployments created by type

- ***[New]*** Count of extended interoperability clients

- ***[New]*** Hashed list of hardware inventory properties longer than 255 characters



##  <a name="bkmk_level2"></a> Level 2 - Enhanced
The Enhanced level is the default after setup finishes. This level includes data that's collected in the Basic level and feature-specific data (frequency and duration of use), Configuration Manager client settings (component name, state, and certain settings like polling intervals), and basic information about software updates.

This level is recommended because it provides Microsoft with the minimum data that's required to make useful improvements in future versions of products and services. This level does not collect object names (sites, users, computer, or objects), details of security-related objects, or vulnerabilities like counts of systems that require software updates.

For Configuration Manager version 1802, this level includes the following data:

### Application management  

- App requirements: count of built-in conditions referenced by deployment technology

- App supersedence, maximum depth of chain

- Application approval statistics and usage frequency

- Application content size statistics

- Application deployment information: use of install versus uninstall, requires approval, user interaction enabled/disabled, dependency, supersedence, and usage count of install behavior feature  

- Application policy size and complexity statistics

- Available application request statistics

- Basic configuration information for packages and programs: deployment options and program flags

- Basic usage/targeting information for deployment types: user versus device targeted, required versus available, and universal apps

- Count of App-V environments and deployment properties

- Count of application applicability by OS  

- Count of applications that are referenced by a task sequence

- Count of distinct branding for application catalog

- Count of Microsoft 365 applications created using dashboard

- Count of packages by type  

- Count of package/program deployments  

- Count of Windows 10 licensed application licenses  

- Count of Windows Installer deployment types by uninstall content settings

- Count of Microsoft Store for Business apps and sync statistics: summarized types of apps, licensed app status, and number of online and offline licensed apps  

- Maintenance window type and duration  

- Minimum/maximum/average number of application deployments per user/device per time period

- Most common application installation error codes by deployment technology

- MSI configuration options and counts

- Statistics on end-user interaction with notification for required software deployments   

- Universal Data Access usage, how created

- ***[New]*** Aggregated User Device Affinity statistics 

- ***[New]*** Max and average primary users per device


### Client  

- Active Management Technology (AMT) client version

- BIOS age in years

- Count of devices with Secure Boot enabled

- Count of devices by TPM state

- Client auto-upgrade: deployment configuration including client piloting and exclusion usage (extended interoperability client)

- Client cache size configuration

- Client deployment download errors

- Client health statistics and top issue summary

- Client notification operation action status: how many times each is run, max number of targeted clients, and average success rate

- Count of client installations from each source location type  

- Count of client installation failures  

- Count of devices virtualized by Hyper-V or Azure  

- Count of Software Center actions   

- Count of UEFI-enabled devices

- Deployment methods used for client and count of clients per deployment method

- List/count of enabled client agents  

- OS age in months

- Number of hardware inventory classes, software inventory rules, and file collection rules

- Statistics for device health attestation: most common error codes, number of on-premises servers, and counts of devices in various states

- ***[New]*** Count of devices by default browser


### Cloud services  

- Microsoft Entra discovery statistics

- Configuration and usage statistics of Cloud Management Gateway: counts of regions and environments, and authentication/authorization statistics

- Count of Microsoft Entra applications and services connected to Configuration Manager

- Count of collections synced to Azure Log Analytics

- Count of Upgrade Analytics Connectors

- Whether the Azure Log Analytics cloud connector is enabled


### Co-management  
- Aggregated usage statistics of co-management: number of enrolled clients, clients receiving policy, workload states, pilot/exclusion collection sizes, and enrollment errors  

- Count of clients by co-management enrollment method  

- Error statistics for co-management enrollment  

- Enrollment schedule and historical statistics  

- Count of clients eligible for co-management  

- Associated Microsoft Intune tenant


### Collections  

- Collection ID usage (not running out of IDs)

- Collection evaluation statistics: query time, assigned versus unassigned counts, counts by type, ID rollover, and rule usage

- Collections without a deployment


### Compliance settings  

- Basic configuration baseline information: count, number of deployments, and number of references

- Compliance policy error statistics

- Count of configuration items by type  

- Count of deployments that reference built-in settings, including remediate setting  

- Count of rules and deployments created for custom settings, including remediate setting  

- Count of deployed Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certificate (.pfx), and compliance policy templates

- Count of SCEP certificate, VPN, Wi-Fi, certificate (.pfx) and compliance policy deployments by platform

- Windows Hello for Business policy (created, deployed)


### Content  

- ***[Updated]*** Boundary group statistics: how many fast, how many slow, count per group, and fallback relationships

- Boundary group information: count of boundaries and site systems that are assigned to each boundary group  

- Boundary group relationships and fallback configuration

- Client content download statistics

- Count of boundaries by type  

- Count of peer cache clients, usage statistic, and partial download statistics

- Distribution Manager configuration information: threads, retry delay, number of retries, and pull distribution point settings  

- Distribution point configuration information: use of branch cache and distribution point monitoring

- Distribution point group information: count of packages and distribution points that are assigned to each distribution point group  


### Endpoint Protection  

- Microsoft Defender for Endpoint policies (formerly known as Windows Defender for Endpoint): count of policies, and whether policies are deployed.

- Count of alerts that are configured for Endpoint Protection feature  

- Count of collections that are selected to appear in Endpoint Protection dashboard  

- Count of Windows Defender Exploit Guard policies, deployments, and targeted clients

- Endpoint Protection deployment errors, count of Endpoint Protection policy deployment error codes  

- Endpoint Protection antimalware and Windows Firewall policy usage (number of unique policies assigned to group)<br /><br /> This data doesn't include any information about the settings included in the policy.  


### Migration  

- Count of migrated objects (use of migration wizard)


### Mobile device management (MDM)  

- Count of issued mobile device actions: lock, pin rest, wipe, retire, and sync now commands

- Count of mobile device policies  

- Count of mobile devices that are managed by Configuration Manager and Microsoft Intune and how they were enrolled (bulk, user-based)  

- Count of users who have multiple enrolled mobile devices  

- Mobile device polling schedule and statistics for mobile device check-in duration  


### Microsoft Intune troubleshooting  

- Count and size of device actions (wipe, retire, lock), telemetry, and data messages that are replicated to Microsoft Intune

- Count and size of state, status, inventory, RDR, DDR, UDX, Tenant state, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM, and compliance messages that are downloaded from Microsoft Intune

- Full and delta user synchronization statistics for Microsoft Intune


### On-premises mobile device management (MDM)  

- Count of Windows 10 bulk enrollment packages and profiles  

- Deployment success/failure statistics for on-premises MDM application deployments  


### OS deployment  

- Count of boot images, drivers, driver packages, multicast-enabled distribution points, PXE-enabled distribution points, and task sequences  

- Count of boot images by Configuration Manager client version

- Count of boot images by Windows PE version

- Count of edition upgrade policies

- Count of hardware identifiers excluded from PXE

- Count of OS deployment by OS version

- Count of OS upgrades over time

- Count of task sequence deployments using option to pre-download content

- Counts of task sequence step usage

- Version of Windows ADK installed


### Site updates  

- Versions of installed Configuration Manager hotfixes


### Software updates  

- Available and deadline deltas that are used in automatic deployment rules  

- Average and maximum number of assignments per update  

- Client update evaluation and scan schedules  

- Classifications that are synced by software update point

- Cluster patching statistics  

- Configuration of Windows 10 express updates

- Configurations that are used for active Windows 10 servicing plans  

- Count of deployed Microsoft 365 updates  

- Count of Microsoft Surface drivers synced

- Count of update groups and assignments  

- Count of update packages and the maximum/minimum/average number of distribution points that are targeted with packages  

- Count of updates that are created and deployed with System Center Update Publisher  

- Count of Windows Update for Business policies created and deployed

- ***[New]*** Aggregated statistics of Windows Update for Business configurations

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


### SQL/performance data  

- Configuration and duration of site summarization

- Count of largest database tables  

- Discovery operational statistics (count of objects found)

- Discovery types, enabled, and schedule (full, incremental)

- SQL Server Always On availability group replica information, usage, and health status

- SQL Server change tracking performance issues, retention period, and auto-cleanup state

- SQL Server change tracking retention period

- State and status message performance statistics including most common and most expensive message types


### Miscellaneous  

- Configuration of data warehouse service point including synchronization schedule and average time

- Count of scripts and run statistics

- Count of sites with Wake On LAN (WOL)

- Reporting usage and performance statistics

- ***[New]*** Phased deployment usage statistics



##  <a name="bkmk_level3"></a> Level 3 - Full
The Full level includes all data in the Basic and Enhanced levels. It also includes additional information about Endpoint Protection, update compliance percentages, and software update information. This level can also include advanced diagnostic information like system files and memory snapshots, which might include personal information that existed in memory or log files at the time of capture.

For Configuration Manager version 1802, this level includes the following data:

- Automatic deployment rule evaluation schedule information

- ATP Health Summary

- Collection evaluation and refresh statistics

- Compliance policy statistics on compliance and errors

- Compliance Settings: SCEP, VPN, Wi-Fi, and compliance policy template configuration details

- DCM config pack for Configuration Manager usage

- Detailed client deployment installation errors

- Endpoint Protection health summary: including count of protected, at risk, unknown, and unsupported clients

- Endpoint Protection policy configuration

- List of processes configured with installation behavior for applications

- Minimum/maximum/average number of hours since last software update scan

- Minimum/maximum/average number of inactive clients in software update deployment collections

- Minimum/maximum/average number of software updates per package

- ***[Updated]*** MSI product code deployment statistics 

- Overall compliance of software update deployments

- Count of groups that have expired software updates

- Software update deployment error codes and counts

- Software update deployment information: percentage of deployments that are targeted with client versus UTC time, required versus optional versus silent, and reboot suppression

- Software update products synced by software update point

- Software update scan success percentages

- Top 50 CPUs in the environment

- Type of Exchange Active Sync (EAS) Conditional Access policies (block or quarantine) for devices that Microsoft Intune manages

- Microsoft Store for Business application details: non-aggregate list of synced applications including AppID, online state or offline state, and total purchased license counts
