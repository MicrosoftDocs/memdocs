---
title: Capabilities in Technical Preview 1511
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview for Configuration Manager, version 1511.
ms.date: 01/23/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ROBOTS: NOINDEX
manager: apoorvseth
ms.author: banreetkaur
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1511 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1511. This version  is a baseline installation for the  technical preview that you can use install a new technical preview site or to upgrade from an earlier version of the technical preview.   Before installing this version of the technical preview, review the introductory topic, [Technical Preview for Configuration Manager](technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.  

The following are new features you can try out with this version.  

##  <a name="BKMK_WUfB"></a> Integration with Windows Update for Business in Windows 10  
 Configuration Manager now has the ability to differentiate a Windows 10 computer that is directly connected via Windows Update for Business versus the ones connected to WSUS for getting Windows 10 updates and upgrades.  For computers connected via Windows Update for Business, the updates and upgrades can be managed at the cadence set by an administrative user via Group Policies or MDM policies and these updates/upgrades can be installed directly from Windows Update for Business.    
For computers connected via Windows Update for Business, Configuration Manager will not be able to report on compliance status (including Windows Updates or Definition Updates). Also Configuration Manager will not be able to deploy Microsoft Updates or 3rd party updates to these computers.  

 **Prerequisites for this scenario:**  

-   Windows 10 Desktop Pro or Windows 10 Enterprise Edition version 1511 or later  

-   Computers to be managed via [Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb).  

### Try it out!  
 Try to complete the following task and then use the feedback information near the top of this topic to let us know how it worked:  

1.  Disable the Windows Update Agent so it doesn't scan against WSUS,  if it was previously enabled.   
    The registry key **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** can be set to indicate whether the computer is scanning against WSUS or Windows Update.  When the value is  2, it's not scanning against WSUS.  

2.  Take note of  the new attribute **UseWUServer**, under the **Windows Update** node in Configuration Manager Resource Explorer.  

3.  Create a collection based on the **UseWUServer** attribute for all the computers that are connected via Windows Update for Business for updates and upgrades.  

4.  Create a  client agent setting to disable the software update workflow and deploy the setting to the collection of computers that are connected directly to Windows Update for Business.  

5.  The computers that are managed via Windows Update for Business will display **Unknown** in the compliance status and won't be counted as part of the overall compliance percentage.  

##  <a name="BKMK_Office365ProPlus"></a> Managing Microsoft 365 Apps for enterprise Client Update through Configuration Manager  
Configuration Manager now has the ability to manage Microsoft 365 desktop client updates using the Configuration Manager Software Update Management workflow.
When Microsoft publishes a new Microsoft 365 desktop client update to Windows Server Updates Services (WSUS), Configuration Manager will be able to synchronize the update to its catalog if the Microsoft 365 update is configured to be part of the catalog synchronization.  The Configuration Manager site server will download the Microsoft 365 client updates and distribute the package to Configuration Manager distribution points.  The Configuration Manager client will then inform Microsoft 365 desktop clients where to get the updates and when to start the update installation process.  

**Prerequisites for this scenario:**  

### Try it out!  
 Try to complete the following task and then use the feedback information near the top of this topic to let us know how it worked:  

1. You can synchronize Microsoft 365 updates to the Configuration Manager site server and view them from the Configuration Manager console.  

2. You can approve and successfully deploy Microsoft 365 updates.  

3. You can download and successfully Microsoft 365 updates to clients.  

4. You can verify compliance for Microsoft 365 updates by using in-console monitoring or reports.  

   For detailed steps, see [Manage Microsoft 365 client updates with Configuration Manager Technical Preview](/deployoffice/manage-microsoft-365-apps-updates-configuration-manager).  

##  <a name="BKMK_AlwasyOn"></a> Support for SQL Server AlwaysOn for highly available databases  
 Configuration Manager now supports using a SQL Server AlwaysOn availability groups to host the site database.  When you install a new site, you can direct setup to use the availability group instead of a normal instance of SQL Server.  

> [!NOTE]  
>  Successful configuration and use of availability groups requires you to be comfortable with configuring SQL Server availability groups, and relies on documentation and procedures provided in the SQL Server documentation library.  

The high level process to configure and use availability groups includes:  

1.  Configure the availability group in SQL Server.  

2.  Install a new Configuration Manager site and during Setup direct the site to use the availability group by specifying the groups Endpoint.  

**Prerequisites for this scenario:**  

-   Requires a version of SQL Server supported by the Configuration Manager Technical Preview  

-   You must create and configure the SQL Server Availability Group before installing Configuration Manager  

-   The availability group must have one primary replica, and can have up to two synchronous secondary replicas  

-   The availability group must have at least one Endpoint  

-   You must have a network location that each SQL Server in the Availability Group can access. This location is used by Setup when configuring the Availability Group, and can be removed after Setup completes.  

**Known issues for this release:**  

-   You cannot successfully add a new replica member to an Availability Group that is already in use as a site database. Instead, you must reinstall the site after the new replica member is added.  

-   For this scenario  you might need to install the **SQL Server 2012 native client** ([from the SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041)) on the management point server. This prevents SQL Server connection errors (which are logged in the **mp_getauth.log** on the management point server).  

### Try it out!  
Try to complete the following tasks and then use the feedback information near the top of this topic to let us know how they worked:  

-   I can install a primary site that uses a database server configured for SQL Server Always On availability groups  

-   I was able to failover my SQL Server Always On availability group to a new replica in the group and the primary site is still operational  

### Configuring availability groups for Configuration Manager  
 Use the following procedures to first create and configure the availability group, and then install a new Configuration Manager site that uses the availability group.  

#### To create an availability group  
The process to [create an availability group](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server) is documented in the SQL Server documentation library.  When you create the availability group, ensure the following requirements for use with Configuration Manager are met:  

-   A maximum of three members:  

    -   One primary replica and up to two secondary replicas  

    -   Secondary replicas must be synchronous.  

        > [!TIP]  
        >  We recommend that secondary replicas be configured to be read only. This enables you to use a secondary replica for functions like reporting while maintaining the performance of the primary replica for site operations.  

-   At least one endpoint. The virtual name of this endpoint will be used when you install the Configuration Manager site.  

    > [!TIP]  
    >  Although the group can contain multiple Endpoints, Configuration Manager can only make use of one.  

#### To install a Configuration Manager site that uses the availability group  
To install a site that uses a SQL Server availability group:  

1.  Substitute the following when prompted by Configuration Manager Setup:  

    -   **SQL Server name**: Enter the virtual name for the Endpoint that you configured when creating the availability group. The virtual name should be a full DNS name, like **&lt;endpointServer\>.fabrikam.com**.  

    -   **Instance**:  This value should remain blank. There is no instance in this configuration.  

    -   **Database**: Enter the name of the database you created on the primary replica of the availability group.  

2.  Next, you must provide a network location that each SQL Server in the group can access:  

    -   The computer account and service account from each SQL Server require full control access to this location.  

    -   This location is only used during setup, and can be unshared or deleted after Setup completes and the site is installed.  

3.  After you provide this information, complete setup with your normal process and configurations.  

##  <a name="BKMK_ClusterServerUpdates"></a> Service a  server cluster  
You can now create a collection that contains servers in a cluster,  and then configure the cluster settings to use when you deploy updates to the cluster. You can control the percentage of servers that are online at any given time, as well as to configure pre-deployment and post-deployment PowerShell scripts to run custom actions.  

**Known issues for this release:**  

-   Reporting is not available to check the status of software updates deployment for cluster servers.  

-   The maintenance sequence option on the **Cluster Settings** page is disabled and not available in this release.  

### Try it out!  
Try to complete the following task and then use the feedback information near the top of this topic to let us know how it worked:  

-   I can create a collection that represents a cluster of servers. For this test, you can configure your collect membership rules to have 2 machines in this collection.  

-   I can specify that only 50% of servers in the cluster can be offline at any point in cluster servicing. Use the sample scripts in the procedure to specify the pre-deployment and post-deployment scripts.  

-   Deploy an update to this collection. Review the start.txt and end.txt files in C:\temp and verify start and end times for the deployment on the servers in the cluster. Review the UpdatesDeployment.log file for more information.  

#### To create a collection for a server cluster  

1.  [Create a device collection](../clients/manage/collections/create-collections.md) that contains the servers in the cluster.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**, right-click the collection that contains the servers in the cluster, and then click **Properties**.  

3.  On the **General** tab, select **All devices are part of the same server cluster**, and then click **Settings**.  

4.  On the **Cluster Settings** page, select the percentage of servers that can be taken offline at the same time  to have software updates installed. One cluster server might be taken offline at a time regardless of the percentage that you provide. Configuration Manager will round down when selecting how many servers to service at one time. For example, if you choose 51% and there are 4 servers in the cluster, 2 servers will be taken offline at the same time.  

5.  Specify whether to use a pre-deployment (node drain) script or post-deployment (node resume) script.  

    > [!TIP]  
    >  The following are examples that you can use in testing for pre-deployment and post-deployment scripts that write the current time to a text file:  
    >   
    >  **Pre-deployment**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Post-deployment**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### To deploy software updates to the server cluster  

1.  [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) to the server cluster collection.  

2.  [Monitor the software update deployment](../../sum/deploy-use/monitor-software-updates.md).
