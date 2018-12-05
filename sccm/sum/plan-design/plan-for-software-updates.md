---
title: Plan for software updates
titleSuffix: Configuration Manager
description: A plan for the software update point infrastructure is essential before you use software updates in a Configuration Manager production environment.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
---

# Plan for software updates in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you use software updates in a Configuration Manager production environment, it's important that you go through the planning process. Having a good plan for the software update point infrastructure is key to a successful software updates implementation.



## Capacity planning recommendations for software updates  

This section includes the following subtopics:  
- [Capacity planning for the software update point](#BKMK_SUMCapacity)
- [Capacity planning for software updates objects](#bkmk_sum-capacity-obj)  


Use the following recommendations as a baseline. This baseline helps you determine the information for the software updates capacity planning that is appropriate to your organization. The actual capacity requirements might vary from the recommendations listed in this article depending on the following criteria: 
- Your specific networking environment
- The hardware that you use to host the software update point site system
- The number of managed clients
- The other site system roles installed on the server  


###  <a name="BKMK_SUMCapacity"></a> Capacity planning for the software update point  

The number of supported clients depends on the version of Windows Server Update Services (WSUS) that runs on the software update point. It also depends on whether the software update point site system role co-exists with another site system role:  

-   The software update point can support up to 25,000 clients when WSUS runs on the software update point server, and the software update point co-exists with another site system role.  

-   The software update point can support up to 150,000 clients when a remote server meets WSUS requirements, WSUS is used with Configuration Manager, and you configure the following settings:

    IIS Application Pools:
    - Increase the WsusPool Queue Length to 2000
    - Increase the WsusPool Private Memory limit x4 times, or set to 0 (unlimited). For example, if the default limit is 1,843,200 KB, increase it to 7,372,800. For more information, see this [Configuration Manager support team blog post](https://blogs.technet.microsoft.com/configurationmgr/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    For more information about hardware requirements for the software update point, see [Recommended hardware for site systems](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).  


### <a name="bkmk_sum-capacity-obj"></a> Capacity planning for software updates objects  

Use the following capacity information to plan for software updates objects:  

#### Limit of 1000 software updates in a deployment  
Limit the number of software updates to 1000 for each software update deployment. When you create an automatic deployment rule (ADR), specify criteria that limits the number of software updates. The ADR fails when the specified criteria returns more than 1000 software updates. Check the status of the ADR from the **Automatic Deployment Rules** node in the Configuration Manager console. When you manually deploy software updates, don't select more than 1000 updates to deploy.  

Also limit the number of software updates to 1000 in a configuration baseline. For more information, see [Create configuration baselines](/sccm/compliance/deploy-use/create-configuration-baselines).



##  <a name="BKMK_SUPInfrastructure"></a> Determine the software update point infrastructure  

This section includes the following subtopics:    
- [Software update point list](#BKMK_SUPList)
- [Software update point switching](#BKMK_SUPSwitching)
- [Manually switch clients to a new software update point](#BKMK_ManuallySwitchSUPs)
- [Software update points in an untrusted forest](#BKMK_SUP_CrossForest)
- [Use an existing WSUS server as the synchronization source at the top-level site](#BKMK_WSUSSyncSource)
- [Software update point on a secondary site](#BKMK_SUPSecSite)  
- [Plan for internet-based clients](#bkmk_internet-clients)  
- [Plan software update content](#bkmk_content)  
- [Plan for third-party updates](#bkmk_thirdparty)  


The central administration site and all child primary sites must have a software update point. As you plan for the software update point infrastructure, determine the following dependencies:
 - Where to install the software update point for the site  
 - Which sites require a software update point that accepts communication from internet-based clients
 - Whether you need a software update point at secondary sites  

> [!IMPORTANT]  
>  For more information about the internal and external dependencies that are required for software updates, see [Prerequisites for software updates](prerequisites-for-software-updates.md).  

Add multiple software update points at a Configuration Manager primary site to provide fault tolerance. The failover design of the software update point is different than the pure randomization model that's used in the design for management points. Unlike in the design of management points, there are client and network performance costs in the software update point design when clients switch to a new software update point. When the client switches to a new WSUS server to scan for software updates, the result is an increase in the catalog size and associated client-side and network performance demands. Therefore, the client preserves affinity with the last software update point from which it successfully scanned.  

The first software update point that you install on a primary site is the synchronization source for all additional software update points that you add at the primary site. After you add software update points and start synchronization, view the status of the software update points and the synchronization source from the **Software Update Point Synchronization Status** node in the **Monitoring** workspace.  

When there is a failure of the software update point configured as the synchronization source for the site, manually remove the failed role. Then select a new software update point to use as the synchronization source. For more information, see [Remove the software update point site system role](../get-started/remove-a-software-update-point.md).  


###  <a name="BKMK_SUPList"></a> Software update point list  

Configuration Manager provides the client with a software update point list in the following scenarios:  

- A new client receives the policy to enable software updates  

- A client can't contact its assigned software update point and needs to switch to another  

The client randomly selects a software update point from the list. It prioritizes the software update points in the same forest. Configuration Manager provides clients with a different list depending on the type of client:  

-   **Intranet-based clients**: Receive a list of software update points that you can configure to allow connections only from the intranet, or a list of software update points that allow internet and intranet client connections.  

-   **Internet-based clients**: Receive a list of software update points that you configure to allow connections only from the internet, or a list of software update points that allow internet and intranet client connections.  


###  <a name="BKMK_SUPSwitching"></a> Software update point switching  

> [!NOTE]  
> Clients use boundary groups to find a new software update point. If their current software update point is no longer accessible, they also use boundary groups to fallback and find a new one. Add individual software update points to different boundary groups to control which servers a client can find. For more information, see [Software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  

If you have multiple software update points at a site, and one fails or becomes unavailable, clients will connect to a different software update point. With this new server, clients continue to scan for the latest software updates. When a client is first assigned a software update point, it stays assigned to that software update point unless it fails to scan.  

The scan for software updates can fail with a number of different retry and non-retry error codes. When the scan fails with a retry error code, the client starts a retry process to scan for the software updates on the software update point. The high-level conditions that result in a retry error code are typically because the WSUS server is unavailable or because it is temporarily overloaded. When the client fails to scan for software updates, it uses the following process:  

1.  The client scans for software updates:  
    - At its scheduled time
    - When it's manually run from the control panel on the client
    - When it's manually run from the Configuration Manager console via a client notification action
    - When it's run from a Configuration Manager SDK method  

2.  If the scan fails, the client waits 30 minutes to retry the scan. It uses the same software update point.  

3.  The client retries a minimum of four times every 30 minutes. After the fourth failure, and after it waits an additional two minutes, the client moves to the next software update point in its list.  

4.  The client repeats this process with the new software update point. After a successful scan, the client continues to connect to the new software update point.  

The following list provides additional information to consider for software update point retry and switching scenarios:  

-   If a client is disconnected from the intranet and fails to scan for software updates, it doesn't switch to another software update point. This failure is expected, because the client can't reach the internal network or a software update point that allows connections from the intranet. The Configuration Manager client determines the availability of the intranet software update point.  

-   If you're managing clients on the internet, and have configured multiple software update points to accept communication from clients on the internet, the switching process follows the standard retry process previously described.  

-   If the scan process starts, but the client is turned off before the scan completes, it isn't considered a scan failure and it doesn't count as one of the four retries.  

When Configuration Manager receives any of the following Windows Update Agent error codes, the client retries the connection:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

To look up the meaning of an error code, convert the decimal error code to hexadecimal, and then search for the hexadecimal value on a site such as the [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx).‭ For example, the decimal error code 2149842970 is hexadecimal 8024001A‬, which means WU_E_POLICY_NOT_SET A policy value was not set.  


###  <a name="BKMK_ManuallySwitchSUPs"></a> Manually switch clients to a new software update point

Switch Configuration Manager clients to a new software update point when there are issues with the active software update point. This change only happens when a client receives multiple software update points from a management point.

> [!IMPORTANT]    
> When you switch devices to use a new server, the devices use fallback to find that new server. Before you start this change, review your boundary group configurations to make sure that your software update points are in the correct boundary groups. For more information, see [Software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  
>
> Switching to a new software update point generates additional network traffic. The amount of traffic depends on your WSUS configuration settings, for example, the synchronized classifications and products, or use of a shared WSUS database. If you plan to switch multiple devices, consider doing so during maintenance windows. This timing reduces the impact to your network when clients scan with the new software update point.  

#### Process to switch software update points  
Start this change on a device collection. Once triggered, the clients look for another software update point at the next scan.  

1.  In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.  

2.  Select the target collection. On the **Home** tab of the ribbon, in the **Collection** group, click **Client Notification**, and then click **Switch to next Software Update Point**.  


###  <a name="BKMK_SUP_CrossForest"></a> Software update points in an untrusted forest  

Create one or more software update points at a site to support clients in an untrusted forest. To add a software update point in another forest, first install and configure a WSUS server in that forest. Then start the wizard to add a Configuration Manager site server with the software update point site system role. In the wizard, configure the following settings to successfully connect to WSUS in the untrusted forest:  

-   Specify a **Site System Installation account** that can access the WSUS server in the untrusted forest.  

-   Specify a **WSUS Server Connection account** to connect to the WSUS server.  

For example, you have a primary site in forest A with two software update points (SUP01 and SUP02). For the same primary site, you also have two software update points (SUP03 and SUP04) in forest B. When switching to the next software update point, the clients prioritize the servers from the same forest.  


###  <a name="BKMK_WSUSSyncSource"></a> Use an existing WSUS server as the synchronization source at the top-level site  

Typically, the top-level site in your hierarchy is configured to synchronize software updates metadata with Microsoft Update. When your organizational security policy doesn't allow the top-level site to access to the internet, configure the synchronization source for the top-level site to use an existing WSUS server. This WSUS server isn't in your Configuration Manager hierarchy. For example, you have a WSUS server in an internet-connected network (DMZ), but your top-level site is in an internal network without internet access. Configure the WSUS server in the DMZ as your synchronization source for software updates metadata. Configure the WSUS server in the DMZ to synchronize software updates with the same criteria that you need in Configuration Manager. Otherwise, the top-level site might not synchronize the software updates that you expect. When you install the software update point, configure a WSUS server connection account. This account needs access to the WSUS server in the DMZ. Also confirm that the firewall permits traffic for the appropriate ports. For more information, see the [ports used by the software update point to the synchronization source](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsSUP-WSUS).  


###  <a name="BKMK_SUPSecSite"></a> Software update point on a secondary site  

The software update point is optional on a secondary site. Install only one software update point at a secondary site. When a software update point isn't installed at the secondary site, devices within the boundaries of a secondary site use a software update point at their assigned primary site. You typically install a software update point at a secondary site when there's limited network bandwidth between the devices in the secondary site and the software update points at the parent primary site. You may also use this configuration when the software update point at the primary site approaches the capacity limit. After you successfully install and configure a software update point at the secondary site, a site-wide policy is updated for clients, and they start to use the new software update point.  


### <a name="bkmk_internet-clients"></a> Plan for internet-based clients

When you need to manage devices that roam off your network onto the internet, develop a plan for how to manage software updates on these devices. Configuration Manager supports several technologies for this scenario. Use one or a combination as necessary to meet the requirements of your organization.

#### Cloud management gateway
Create a cloud management gateway in Microsoft Azure and enable at least one on-premises software update point to allow traffic from internet-based clients. As clients roam onto the internet, they continue to scan against your software update points. All internet-based clients always get content from the Microsoft Update cloud service. 

For more information, see [Plan for the cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### Internet-based client management
Place a software update point in an internet-facing network and enable it to allow traffic from internet-based clients. As clients roam onto the internet, they switch to this software update point for scanning. All internet-based clients always get content from the Microsoft Update cloud service.

For more information on the advantages and disadvantages of internet-based client management, see [Manage clients on the internet](/sccm/core/clients/manage/manage-clients-internet).

#### Windows Update for Business
Windows Update for Business allows you to keep Windows 10 devices always up-to-date with the latest quality and feature updates. These devices connect directly to the Windows Update cloud service. Configuration Manager can differentiate between Windows 10 computers that use WUfB and WSUS for getting software updates.

For more information, see [Integration with Windows Update for Business](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).


### <a name="bkmk_content"></a> Plan software update content

Clients need to download the content files for software updates in order to install them. Configuration Manager provides several technologies to support management and delivery of this content. Or configure software update deployments to allow or require clients to get content directly from the Microsoft Update cloud service.

#### Download and distribute content 
By default, the software update management process in Configuration Manager uses the built-in content management features. These features include the centralized, single-instance store content library, and the distributed design of the distribution point site system role. You use these features when you download and distribute software update deployment packages. 

For more information, see [Download software updates](/sccm/sum/deploy-use/download-software-updates).

#### Manage express installation files for Windows 10
Configuration Manager supports the use of express installation files for Windows 10 updates. Express update files and supporting technologies such as Delivery Optimization can help reduce the network impact of large content files downloading to clients. 

For more information, see [Optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).

#### Clients download content from the internet
When you deploy software updates to clients, configure the deployment for clients to download content from the Microsoft Update cloud service. When clients aren't able to download content from another content source, they can still download the content from the internet. 

Starting in version 1806, you don't have to create a deployment package when deploying software updates. When you select the **No deployment package** option, clients can still download content from local sources if available, but typically download from the Microsoft Update service.<!--1357933-->

Internet-based clients always download content from the Microsoft Update cloud service. Don't distribute software update deployment packages to a cloud distribution point. You're charged for storage with the cloud distribution point, but clients won't download these packages. 


### <a name="bkmk_thirdparty"></a> Plan for third-party updates
Configuration Manager integrates with WSUS, which natively supports software updates published by Microsoft. Most customers use other third-party applications that also need updates. There are several options to consider for keeping third-party applications up to date.

#### Supersede applications to update
Use a supersedence relationship with the application management feature in Configuration Manager to upgrade or replace existing applications. When you supersede an application, specify a new deployment type to replace the deployment type of the superseded application. Also decide whether to upgrade or uninstall the superseded application before the superseding application is installed.

For more information, see [Revise and supersede applications](/sccm/apps/deploy-use/revise-and-supersede-applications).

#### Third-party software updates
Starting in version 1806, use the **Third-Party Software Update Catalogs** node in the Configuration Manager console to subscribe to third-party catalogs, publish their updates to your software update point, and then deploy them to clients.<!--1352101-->

For more information, see [Third-party software updates](/sccm/sum/deploy-use/third-party-software-updates).

#### System Center Updates Publisher
System Center Updates Publisher (SCUP) is a stand-alone tool that enables independent software vendors or line-of-business application developers to manage custom updates. These updates include those with dependencies, like drivers and update bundles.

For more information, see [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).



##  <a name="BKMK_SUPInstallation"></a> Plan for software update point installation  

This section includes the following subtopics:  
- [Requirements for the software update point](#BKMK_SUPSystemRequirements)
- [Plan for WSUS installation](#BKMK_PlanningForWSUS)
- [Configure firewalls](#BKMK_ConfigureFirewalls)  


This section provides information about the steps to take to successfully plan and prepare for the software update point installation. Before you create a site system role for the software update point in Configuration Manager, there are several requirements to consider. The specific requirements depend on your Configuration Manager infrastructure. When you configure the software update point to communicate by using HTTPS, this section is especially important to review. HTTPS-enabled servers require additional steps to work properly.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requirements for the software update point  

Install the software update point role on a site system that meets the minimum requirements for WSUS and the supported configurations for Configuration Manager site systems.  

-   For more information about the minimum requirements for the WSUS server role in Windows Server, see [Review considerations and system requirements](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#BKMK_1.1).  

-   For more information about the supported configurations for Configuration Manager site systems, see [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


###  <a name="BKMK_PlanningForWSUS"></a> Plan for WSUS installation  

Install a supported version of WSUS on all site system servers that you configure for the software update point role. When you don't install the software update point on the site server, install the WSUS Administration Console on the site server. This component allows the site server to communicate with WSUS that runs on the software update point.  

When you use WSUS on Windows Server 2012 or later, configure additional permissions to allow the **WSUS Configuration Manager** component in Configuration Manager to connect to WSUS. This component performs periodic health checks. Choose one of the following options to configure the required permission:  

-   Add the **SYSTEM** account to the **WSUS Administrators** group  

-   Add the **NT AUTHORITY\SYSTEM** account as a user for the WSUS database (SUSDB). Configure a minimum of the webService database role membership.  
  
For more information about how to install WSUS on Windows Server, see [Install the WSUS Server Role](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

When you install more than one software update point at a primary site, use the same WSUS database for each software update point in the same Active Directory forest. Sharing the same database improves performance when clients switch to a new software update point. For more information, see [Use a shared WSUS database for software update points](/sccm/sum/plan-design/software-updates-best-practices#bkmk_shared-susdb).  


####  <a name="BKMK_CustomWebSite"></a> Configure WSUS to use a custom website  
When you install WSUS, you have the option to use the existing IIS Default website, or to create a custom WSUS website. Create a custom website for WSUS so that IIS hosts the WSUS services in a dedicated virtual website. Otherwise it shares the same website that's used by the other Configuration Manager site systems or applications. This configuration is especially necessary when you install the software update point role on the site server. When you run WSUS in Windows Server 2012 or later, WSUS is configured by default to use port 8530 for HTTP and port 8531 for HTTPS. Specify these ports when you create the software update point at a site.  


####  <a name="BKMK_WSUSInfrastructure"></a> Use an existing WSUS infrastructure  
Select a WSUS server that was active in your environment before you installed Configuration Manager as a software update point. When the software update point is configured, specify the synchronization settings. Configuration Manager connects to the WSUS server that runs on the software update point server and configures WSUS with the same settings. 

Before you configure the server as a software update point, compare its configuration for products and classifications with your Configuration Manager settings. If you synchronized the existing WSUS server before configuring it as a software update point, and the lists of products and classifications are different, it syncs all of the software updates metadata regardless of the configured settings. This behavior results in unexpected software updates metadata in the site database. 

You experience the same behavior when you add products or classifications directly in the WSUS Administration console, and then immediately initiate a synchronization. By default, every hour Configuration Manager connects to WSUS and resets any settings that were modified outside of Configuration Manager. The software updates that don't meet the products and classifications that you specify in synchronization settings are set to expired. Then they are removed from the site database.  

When a WSUS server is configured as a software update point, you're no longer able to use it as a standalone WSUS server. If you need a separate standalone WSUS server that isn't managed by Configuration Manager, configure it on a different server.  

####  <a name="BKMK_WSUSAsReplica"></a> Configure WSUS as a replica server  
When you add the software update point role on a primary site server, you can't use a WSUS server that's configured as a replica. When the WSUS server is configured as a replica, Configuration Manager fails to configure the WSUS server, and the WSUS synchronization fails. The first software update point that you install at a primary site is the default software update point. Additional software update points at the site are configured as replicas of the default software update point.  

####  <a name="BKMK_WSUSandSSL"></a> Decide whether to configure WSUS to use SSL  
Use the SSL protocol to help secure the software update point. WSUS uses SSL to authenticate client computers and downstream WSUS servers to the WSUS server. WSUS also uses SSL to encrypt software update metadata. When you choose to secure WSUS with SSL, prepare the WSUS server before you install the software update point. For more information, see the [Configure SSL on the WSUS server](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) article in the documentation for WSUS. 

When you install and configure the software update point, select the option to **Enable SSL communications for the WSUS Server**. Otherwise, Configuration Manager configures WSUS not to use SSL. When you enable SSL on a software update point, also configure any software update points at child sites to use SSL.  


###  <a name="BKMK_ConfigureFirewalls"></a> Configure firewalls  

The software update point at a Configuration Manager central administration site communicates with WSUS on the software update point. WSUS communicates with the synchronization source to synchronize software updates metadata. Software update points at a child site communicate with the software update point at the parent site. When there's more than one software update point at a primary site, the additional software update points communicate with the default software update point. The default role is the first software update point that's installed at the site.  

You might need to configure the firewall to allow the HTTP or HTTPS traffic that WSUS uses in following scenarios: 
- Between the software update point and the internet
- Between a software update point and its upstream synchronization source
- Between additional software update points  

The connection to Microsoft Update is always configured to use port 80 for HTTP and port 443 for HTTPS. Use a custom port for the connection from WSUS on the software update point at a child site to WSUS on the software update point at the parent site. When your security policy doesn't allow the connection, use the export and import synchronization method. For more information, see the [Synchronization source](#BKMK_SyncSource) section in this article. For more information about the ports that WSUS uses, see [How to determine the port settings used by WSUS in Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### Restrict access to specific domains  
If your organization doesn't allow the ports and protocols to be open to all addresses on the firewall between the active software update point and the internet, restrict access to the following domains so that WSUS and Automatic Updates can communicate with Microsoft Update:  

-   `http://windowsupdate.microsoft.com`  

-   `http://*.windowsupdate.microsoft.com`  

-   `https://*.windowsupdate.microsoft.com`  

-   `http://*.update.microsoft.com`  

-   `https://*.update.microsoft.com`  

-   `http://*.windowsupdate.com`  

-   `http://download.windowsupdate.com`  

-   `http://download.microsoft.com`  

-   `http://*.download.windowsupdate.com`  

-   `http://test.stats.update.microsoft.com`  

-   `http://ntservicepack.microsoft.com`  

You might need to add the addresses below to the firewall that's located between the two site systems in the following cases: 
- If child sites have a software update point 
- If there is a remote active internet-based software update point at a site

 **Software update point on the child site**  

-   `http://<FQDN for software update point on child site>`  

-   `https://<FQDN for software update point on child site>`  

-   `http://<FQDN for software update point on parent site>`  

-   `https://<FQDN for software update point on parent site>`  



##  <a name="BKMK_SyncSettings"></a> Plan for synchronization settings  

This section includes the following subtopics:  
- [Synchronization source](#BKMK_SyncSource)
- [Synchronization schedule](#BKMK_SyncSchedule)
- [Update classifications](#BKMK_UpdateClassifications)
- [Products](#BKMK_UpdateProducts)
- [Supersedence rules](#BKMK_SupersedenceRules)
- [Languages](#BKMK_UpdateLanguages)  


Software updates synchronization in Configuration Manager downloads the software updates metadata based on criteria that you configure. The top-level site in your hierarchy synchronizes software updates from Microsoft Update. You have the option to configure the software update point on the top-level site to synchronize with an existing WSUS server, not in the Configuration Manager hierarchy. The child primary sites synchronize software updates metadata from the software update point on the central administration site. Before you install and configure a software update point, use this section to plan for the synchronization settings.  


###  <a name="BKMK_SyncSource"></a> Synchronization source  

The synchronization source settings for the software update point specify the location for where the software update point retrieves software updates metadata. It also specifies whether the synchronization process creates WSUS reporting events.  

-   **Synchronization source**: By default, the software update point at the top-level site configures the synchronization source for Microsoft Update. You have the option to synchronize the top-level site with an existing WSUS server. The software update point on a child primary site configures the synchronization source as the software update point at the central administration site.  

    -  The first software update point that you install at a primary site, which is the default software update point, synchronizes with the central administration site. Additional software update points at the primary site synchronize with the default software update point at the primary site.  

    - When a software update point is disconnected from Microsoft Update or from the upstream update server, configure the synchronization source not to synchronize with a configured synchronization source. Instead configure it to use the export and import function of the **WSUSUtil** tool to synchronize software updates. For more information, see [Synchronize software updates from a disconnected software update point](../get-started/synchronize-software-updates-disconnected.md).  

-   **WSUS reporting events:** The Windows Update Agent on client computers can create event messages for WSUS reporting. These events aren't used by Configuration Manager. Thus, the option, **Do not create WSUS reporting events**, is selected by default. When these events aren't created, the only time that the client should connect to the WSUS server is during software update evaluation and compliance scans. If these events are needed for reporting outside of Configuration Manager, modify this setting to create WSUS reporting events.  


###  <a name="BKMK_SyncSchedule"></a> Synchronization schedule  

Configure the synchronization schedule only at the software update point on the top-level site in the Configuration Manager hierarchy. When you configure the synchronization schedule, the software update point synchronizes with the synchronization source at the date and time that you specified. The custom schedule allows you to synchronize software updates to optimize for your environment. Consider the performance demands of the WSUS server, site server, and network. For example, 2:00 AM once a week. Alternatively, manually start synchronization on the top-level site by using the **Synchronization Software Updates** action from the **All Software Updates** or **Software Update Groups** nodes in the Configuration Manager console.  

> [!TIP]  
>  Schedule the software updates synchronization to run by using a time that's appropriate for your environment. One common scenario is to set the synchronization schedule to run shortly after Microsoft's regular software update release on the second Tuesday of each month. This day is typically referred to as *Patch Tuesday*. If you use Configuration Manager to deliver Endpoint Protection and Windows Defender definition and engine updates, consider setting the synchronization schedule to run daily.  

After the software update point successfully synchronizes, it sends a synchronization request to child sites. If you have additional software update points at a primary site, it sends a synchronization request to each software update point. This process is repeated on every site in the hierarchy.  


###  <a name="BKMK_UpdateClassifications"></a> Update classifications  

Every software update is defined with an update classification that helps to organize the different types of updates. During the synchronization process, the site synchronizes the metadata for the specified classifications. 

Configuration Manager supports synchronization of the following update classifications:  

-   **Critical Updates**: A broadly released update for a specific problem that addresses a critical, non-security-related bug.  

-   **Definition Updates**: An update to virus or other definition files.  

-   **Feature Packs**: New product features that are distributed outside of a product release and are typically included in the next full product release.  

-   **Security Updates**: A broadly released update for a product-specific, security-related issue.  

-   **Service Packs**: A cumulative set of hotfixes that is applied to an OS or application. These hotfixes include security updates, critical updates, and software updates.  

-   **Tools**: A utility or feature that helps to complete one or more tasks.  

-   **Update Rollups**: A cumulative set of hotfixes that is packaged together for easy deployment. These hotfixes include security updates, critical updates, and software updates. An update rollup generally addresses a specific area, such as security or a product component.  

-   **Updates**: An update to an application or file that's currently installed.  

-   **Upgrades**: A feature update to a new version of Windows 10.  

Configure the update classification settings only on the top-level site. The update classification settings aren't configured on the software update point on child sites, because the software updates metadata is replicated from the top-level site. When you select the update classifications, be aware the more classifications that you select, the longer it takes to synchronize the software updates metadata.  

> [!WARNING]  
>  As a best practice, clear all classifications before you synchronize for the first time. After the initial synchronization, select the desired classifications, and then rerun synchronization.  


###  <a name="BKMK_UpdateProducts"></a> Products  

The metadata for each software update defines one or more products for which the update is applicable. A product is a specific edition of an OS or application. An example of a product is Microsoft Windows 10. A product family is the base OS or application from which the individual products are derived. An example of a product family is Microsoft Windows, of which Windows 10 and Windows Server 2016 are members. Select a product family or individual products within a product family.  

When software updates are applicable to multiple products, and at least one of the products is selected for synchronization, all of the products appear in the Configuration Manager console even if some products weren't selected. For example, you only select the Windows Server 2012 product. If a software update applies to Windows Server 2012 and Windows Server 2012 Datacenter Edition, both products are in the site database.  

Configure the product settings only on the top-level site. The product settings aren't configured on the software update point for child sites because the software updates metadata is replicated from the top-level site. The more products that you select, the longer it takes to synchronize the software updates metadata.  

> [!IMPORTANT]  
>  Configuration Manager stores a list of products and product families that you choose from when you first install the software update point. Products and product families that are released after Configuration Manager is released might not be available to select until you complete synchronization. The synchronization process updates the list of available products and product families from which you can choose. Clear all products before you synchronize software updates for the first time. After the initial synchronization, select the desired products, and then rerun synchronization.  


###  <a name="BKMK_SupersedenceRules"></a> Supersedence rules  

Typically, a software update that supersedes another software update does one or more of the following actions:  

-   Enhances, improves, or updates the fix that was provided by one or more previously released updates.  

-   Improves the efficiency of the superseded update file package, which is installed on clients if the update is approved for installation. For example, the superseded update might contain files that are no longer relevant to the fix or to the operating systems that are supported by the new update. Those files aren't included in the superseding  file package of the update.  

-   Updates newer versions of a product. In other words, it updates versions that are no longer applicable to older versions or configurations of a product. Updates can also supersede other updates if modifications were made to expand language support. For example, a later revision of a product update for Microsoft Office might remove the support for an older OS, but it might add additional support for new languages in the initial update release.  

In the properties for the software update point, specify that the superseded software updates are immediately expired. This setting prevents them from being included in new deployments. It also flags the existing deployments to indicate that they contain one or more expired software updates. Or specify a period of time before the superseded software updates are expired. This action allows you to continue to deploy them. 

Consider the following scenarios in which you might need to deploy a superseded software update:  

-   A superseding software update supports only newer versions of an OS. Some of your client computers run earlier versions of the OS.  

-   A superseding software update has more restricted applicability than the software update it supersedes. This behavior would make it inappropriate for some clients.  

-   If a superseding software update wasn't approved for deployment in your production environment.  

    > [!NOTE]  
    > Before Configuration Manager version 1806, when Configuration Manager sets a superseded software update to **Expired**, it doesn't set the update to **Declined** in WSUS. Clients continue to scan for an expired update until the update is declined manually or via a custom script.  After Configuration Manager version 1806, Configuration Manager  For more information about the WSUS cleanup task, see [Software updates maintenance](/sccm/sum/deploy-use/software-updates-maintenance).  


###  <a name="BKMK_UpdateLanguages"></a> Languages  

The language settings for the software update point allow you to configure: 
- The languages for which the summary details (software updates metadata) are synchronized for software updates  
- The software update file languages that are downloaded for software updates  

#### Software update file  
Configure languages for the **Software update file** setting in the properties for the software update point. This setting provides the default languages that are available when you download software updates at a site. Modify the languages that are selected by default each time that the software updates are downloaded or deployed. During the download process, the software update files for the configured languages are downloaded to the deployment package source location, if the software update files are available in the selected language. Next, they're copied to the content library on the site server. Then they're distributed to the distribution points that are configured for the package.  

Configure the software update file language settings with the languages that are most often used in your environment. For example, clients in your site use mostly English and Japanese for Windows or applications. There are few other languages that are used at the site. Select only English and Japanese in the **Software Update File** column when you download or deploy the software update. This action allows you to use the default settings on the **Language Selection** page of the deployment and download wizards. This action also prevents unneeded update files from being downloaded. Configure this setting at each software update point in the Configuration Manager hierarchy.  

#### Summary details  
During the synchronization process, the summary details information (software updates metadata) is updated for software updates in the languages that you specify. The metadata provides information about the software update, for example:
- Name
- Description
- Products that the update supports
- Update classification
- Article ID
- Download URL
- Applicability rules

Configure the summary details settings only on the top-level site. The summary details aren't configured on the software update point on child sites because the software updates metadata is replicated from the central administration site by using file-based replication. When you select the summary details languages, select only the languages that you need in your environment. The more languages that you select, the longer it takes to synchronize the software updates metadata. Configuration Manager displays the software updates metadata in the locale of the OS in which the Configuration Manager console runs. If the localized properties for the software updates aren't available in the locale of this OS, the software updates information displays in English.  

> [!IMPORTANT]  
>  Select all of the summary details languages that you need. When the software update point at the top-level site synchronizes with the synchronization source, the selected summary details languages determine the software updates metadata that it retrieves. If you modify the summary details languages after synchronization ran at least one time, it retrieves the software updates metadata for the modified summary details languages only for new or updated software updates. The software updates that have already been synchronized aren't updated with new metadata for the modified languages unless there's a change to the software update on the synchronization source.  



##  <a name="BKMK_MaintenanceWindow"></a> Plan for a software updates maintenance window  

Add a maintenance window dedicated for software updates installation. This action lets you configure a general maintenance window and a different maintenance window for software updates. When you configure both a general maintenance window and software updates maintenance window, clients install software updates only during the software updates maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  



##  <a name="BKMK_RestartOptions"></a> Restart options for Windows 10 clients after software update installation

When a software update that requires a restart is deployed and installed using Configuration Manager, the client schedules a pending restart and displays a restart dialog box.

When there's a pending restart for a Configuration Manager software update, the option to **Update and Restart** and **Update and Shutdown** is available on Windows 10 computers in the Windows power options. After using one of these options, the restart dialog doesn't display after the computer restarts.



## Next steps
Once you plan for software updates, see [Prepare for software updates management](../get-started/prepare-for-software-updates-management.md).  

For more information about managing Windows as a service, see [Fundamentals of Configuration Manager as a service and Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service).
