---
title: "New version 1706 | Microsoft Docs"
description: "Get details about changes and new capabilities introduced in version 1706 of System Center Configuration Manager."
ms.custom: na
ms.date:  07/31/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# What&#39;s new in version 1706 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1706 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1606, 1610, or 1702.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>   - [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1706 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1706 drops support for the following products:
-->


## Site infrastructure

### Client Peer Cache support for express installation files for Windows 10 and Office 365  
<!-- 1352486 -->
Beginning with this release, Peer Cache supports distribution of content express installation files for Windows 10, and of update files for Office 365. No additional configurations are required to support this change.

### Updates for the data warehouse
<!-- 1277922 -->
The data warehouse is no longer a pre-release feature. We have also updated the prerequisites to include support for the database on SQL Server Always on availability groups, and failover clusters. For more information, see [The Data Warehouse service point](/sccm/core/servers/manage/data-warehouse).

### Accessibility improvements
<!-- 1253000 -->
We have added additional improvements to accessibility for the Configuration Manager console. For details, see [Accessibility features](/sccm/core/understand/accessibility-features).

### Improvements  for SQL Server Always On Availability Groups
<!-- 1352094 -->
With this release, you can now use asynchronous commit replicas in the SQL Server Always On availability groups you use with Configuration Manager. This means you can add additional replicas to your availability groups to use as off-site (remote) backups, and then use them in a disaster recovery scenario.  
  -	  Configuration Manager supports using the asynchronous commit replica to recover your synchronous replica. See [site database recovery options](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) in the Backup and Recovery topic for information on how to accomplish this.
  -	  This release does not support failover to use the asynchronous commit replica as your site database.
For more information, see [Prepare to use Always On Availability Groups](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### Update reset tool
<!-- 1324589 -->
Beginning with version 1706, Configuration Manager primary sites, and central administration sites include the Configuration Manager Update Reset Tool, **CMUpdateReset.exe**. Use this tool with any version of the current branch that remains in support, to fix issues when in-console updates have problems downloading or replicating. For more information, see [Update reset tool](/sccm/core/servers/manage/update-reset-tool).

### High DPI console support  
<!-- 1353476 -->
With this release, issues with how the Configuration Manager console scales and displays different parts of the UI when viewed on high DPI devices (like a Surface book) should be fixed.

### Improved boundary groups for software update points
<!-- 1324591 -->
This release includes improvements for how software update points work with boundary groups. The following summarizes the new fallback behavior:
-   Fallback for software update points now uses a configurable time for fallback to neighbor boundary groups.
-   Independent of the fallback configuration, a client attempts to reach the last software update point it used for 120 minutes. After failing to reach that server for 120 minutes, the client then checks its pool of available software update points, so it can find a new one.
-   After failing to reach its original server for two hours, the client switches to a shorter cycle for contacting a new software update point. This means if a client fails to connect with a new server, it quickly selects the next server from its pool of available servers and attempts to contact that one.

For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the Boundary Groups topic for the Current Branch.

### Azure AD integration with Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
With this release, we have improved the integration of Configuration Manager and Azure Active Directory (Azure AD).  These improvements streamline how you configure the Azure services you use with Configuration Manager, and help you to manage clients and users who authenticate though Azure AD.

The improved integration makes the following possible:  
  -   Azure Services Wizard – This Wizard provides a common configuration experience that replaces the individual workflows to set up the following Azure services you use with Configuration Manager.
      - **Cloud Management**
        Enable clients to authenticate by using Azure Active Directory (Azure AD). You can also configure Azure AD User Discovery.
      - **OMS Connector**
        Connect to Operations Manager Suite (OMS) and sync data like collections to OMS Log Analytics.
      - **Upgrade Readiness**
        Connect to Upgrade Readiness and view client upgrade-compatibility data.
      - **Windows Store for Business**
        Connect to the on-line store for Windows Store for Business and get apps for your organization that you can deploy with Configuration Manager.


  This is done by using an [Azure server web app](/azure/azure/app-service/app-service-authentication-overview#service-to-service-authentication) to provide the subscription and configuration details that you otherwise enter each time you set up a new Configuration Manager component or service with Azure. For more information, see [Azure Services Wizard](/sccm/core/servers/deploy/configure/azure-services-wizard).

-   Use Azure AD to authenticate clients on the Internet to access your Configuration Manager sites. Azure AD replaces the need to configure and use client authentication certificates. <!-- This requires the cloud management gateway site system role. For more information, see []().  -->

-   Install and manage the Configuration Manager client on computers that are located on the Internet. This requires the use of the cloud management gateway site system role. <!-- For more information, see [](). -->

-   Configure Azure AD User Discovery.  Use the Azure Services Wizard to configure this new discovery method. This new method queries your Azure AD for user data you can then use along-side traditional discovery data.  Both full and delta synchronization are supported.  For more information see [Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### Peer cache improvements
<!-- 1252345 -->
Peer cache no longer uses the Network Access Account to authenticate download requests from peers. There is one caveat to this when the account remains required by clients. This remains a requirement for clients that boot in to WinPE and then access content from a peer cache source. For more information, see [requirements and considerations for peer cache](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache).


<!-- ## Migration  -->


<!-- ## Client management  -->


<!-- ## Compliance settings -->

### New compliance settings for Windows 10 devices that are not managed with the Configuration Manager client
<!-- 1354715 -->
In this release, we've added new configuration item settings for Windows 10 devices that are enrolled with Intune, or managed on premises by Configuration Manager. The settings are:

- **Password**
	- Device Encryption
- **Device**
	- Region settings modification (desktop only)
	- Power and sleep settings modification
	- Language settings modification
	- System time modification
	- Device name modification
- **Store**
	- Auto-update apps from store
	- Use private store only
	- Store originated app launch
- **Microsoft Edge**
	- Block access to about:flags
	- SmartScreen prompt override
	- SmartScreen prompt override for files
	- WebRTC localhost IP address
	- Default search engine
	- OpenSearch XML URL
	- Homepages (desktop only)

For details of all Windows 10 settings, see [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

<!-- ## Application Management  -->

### Run PowerShell scripts from the Configuration Manager console
<!-- 1236459 -->

In Configuration Manager, you can deploy scripts to client devices using packages and programs. In this release, we've added new functionality that lets you take the following actions:

- Import PowerShell Scripts to Configuration Manager
- Edit the scripts from the Configuration Manager console (for unsigned scripts only)
- Mark scripts as Approved or Denied, to improve security
- Run scripts on collections of Windows client PCs, and on-premises managed Windows PCs. You don't deploy scripts, instead, they are run in near real time on client devices.
- Examine the results returned by the script in the Configuration Manager console.

For more information, see [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts).


<!--  ## Operating system deployment  -->

<!-- ## Software updates -->


<!-- ## Reporting  -->

<!-- ## Inventory  -->

<!--  ## Mobile device management  -->

<!--  ## Protect devices  -->
