---

title: Plan for software updates
titleSuffix: "Configuration Manager"
description: "A plan for the software update point infrastructure is essential before you use software updates in a System Center Configuration Manager production environment."
keywords:
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 06/27/2017
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f

---

# Plan for software updates in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you use software updates in a System Center Configuration Manager production environment, it's important that you go through the planning process. Having a good plan for the software update point infrastructure is key to a successful software updates implementation.

## Capacity planning recommendations for software updates  
 You can use the following recommendations as a baseline that can help you determine the information for the software updates capacity planning that is appropriate to your organization. The actual capacity requirements might vary from the recommendations that are listed in this article depending on the following criteria: your specific networking environment, the hardware that you use to host the software update point site system, the number of clients that are installed, and the site system roles that are installed on the server.  

###  <a name="BKMK_SUMCapacity"></a> Capacity planning for the software update point  
 The number of supported clients depends on the version of Windows Server Update Services (WSUS) that runs on the software update point, and it also depends on whether the software update point site system role co-exists with another site system role:  

-   The software update point can support up to 25,000 clients when WSUS runs on the software update point computer and the software update point co-exists with another site system role.  

-   The software update point can support up to 150,000 clients when the remote computer meets WSUS requirements, WSUS is used with Configuration Manager, and you configure the following:

    IIS Application Pools:
    - Increase the WsusPool Queue Length to 2000
    - Increase the WsusPool Private Memory limit x4 times, or set to 0 (unlimited)      

    For details about hardware requirements for the software update point, see [Recommended hardware for site systems](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).

-   By default, Configuration Manager does not support configuring software update points as NLB clusters. Prior to Configuration Manager version 1702, you could use the Configuration Manager SDK to configure up to four software update points on an NLB cluster. However, starting in Configuration Manager version 1702, software update points are not supported as NLB clusters and upgrades to Configuration Manager version 1702 will be blocked if this configuration is detected.

### Capacity planning for software updates objects  
 Use the following capacity information to plan for software updates objects.  

-   **Limit of 1000 software updates in a deployment**  

     You must limit the number of software updates to 1000 for each software update deployment. When you create an automatic deployment rule, specify a criteria that limits the number of software updates that are returned. The automatic deployment rule fails when the criteria that you specify returns more than 1000 software updates. You can check the status of the automatic deployment rule from the **Automatic Deployment Rules** node in the Configuration Manager console. When you manually deploy software updates, do not select more than 1000 updates to deploy.  

     You must also limit the number of software updates to 1000 in a configuration baseline. For more information, see [Create configuration baselines](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="BKMK_SUPInfrastructure"></a> Determine the software update point infrastructure  
 The central administration site and all child primary sites must have a software update point where you deploy software updates. As you plan for the software update point infrastructure, you need to determine the following dependencies:
 - where to install the software update point for the site
 - which sites require a software update point that accepts communication from Internet-based clients
 - whether you need a software update point at a secondary site.

Use the following sections to determine the software update point infrastructure.  

> [!IMPORTANT]  
>  For information about the internal and external dependencies that are required for software updates, see [Prerequisites for software updates](prerequisites-for-software-updates.md).  

 You can add multiple software update points at a Configuration Manager primary site. The ability to have multiple software update points at a site provides fault tolerance without requiring the complexity of NLB. However, the failover that you receive with multiple software update points is not as robust as NLB for pure load balancing, but it is rather designed for fault-tolerance. Also, the failover design of the software update point is different than the pure randomization model that is used in the design for management points. Unlike in the design of management points, in the software update points there are client and network performance costs that are associated with switching to a new software update point. When the client switches to a new WSUS server to scan for software updates, the result is an increase in the catalog size and associated client-side and network performance demands. Therefore, the client preserves affinity with the last software update point for which it successfully scanned.  

 The first software update point that you install on a primary site is the synchronization source for all additional software update points that you add at the primary site. After you added your software update points and initiated software updates synchronization, you can view the status of the software update points and the synchronization source from the **Software Update Point Synchronization Status** node in the **Monitoring** workspace.  

 When a software update point fails, and that software update point is configured as the synchronization source for the other software update points at the site, you must manually remove the failed software update point and select a new software update point to use as the synchronization source. For more information about how to remove a software update point, see [Remove the software update point site system role](../get-started/remove-a-software-update-point.md).  

###  <a name="BKMK_SUPList"></a> Software update point list  
 Configuration Manager provides the client with a software update point list in the following scenarios: when a new client receives the policy to enable software updates, or when a client cannot contact its software update point and needs to switch to another software update point. The client randomly selects a software update point from the list, and it prioritizes the software update points that are in the same forest. Configuration Manager provides clients with a different list depending on the type of client.  

-   **Intranet-based clients**: Receive a list of software update points that you can configure to allow connections only from the intranet, or a list of software update points that allow Internet and intranet client connections.  

-   **Internet-based clients**: Receive a list of software update points that you configure to allow connections only from the Internet, or a list of software update points that allow Internet and intranet client connections.  

###  <a name="BKMK_SUPSwitching"></a> Software update point switching  
> [!NOTE]
> Beginning with version 1702, clients use boundary groups to find a new software update point, and to fallback and find a new software update point if their current one is no longer accessible. You can add individual software update points to different boundary groups to control which servers a client can find. For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the [configuring boundary groups](/sccm/core/servers/deploy/configure/boundary-groups) article.

If you have multiple software update points at a site, and then one fails or becomes unavailable, clients will connect to a different software update point and continue to scan for the latest software updates. When a client is first assigned a software update point, it stays assigned to that software update point unless it fails to scan for software updates on that software update point.  

The scan for software updates can fail with a number of different retry and non-retry error codes. When the scan fails with a retry error code, the client starts a retry process to scan for the software updates on the software update point. The high-level conditions that result in a retry error code are typically because the WSUS server is unavailable or because it is temporarily overloaded. The client uses the following process when it fails to scan for software updates:  

1.  The client scans for software updates at its scheduled time, or when it is initiated through the control panel on the client, or by using the SDK. If the scan fails, the client waits 30 minutes to retry the scan, and it uses the same software update point.  

2.  The client retries a minimum of four times at 30-minute intervals. After the fourth failure, and after it waits an additional two minutes, the client will move to the next software update point in the software update point list.  

3.  The client goes through the same process on the new software update point. After a successful scan, the client will continue to connect to the new software update point.

 The following list provides additional information that you can consider for software update point retry and switching scenarios:  

-   If a client is disconnected from the corporate intranet and fails to scan for software updates, it will not switch to another software update point. This is an expected failure, because the client cannot reach the corporate network or the software update point that allows connection from the intranet. The Configuration Manager client determines the availability of the intranet software update point.  

-   If Internet-based client management is enabled, and there are multiple software update points that are configured to accept communication from clients on the Internet, the switching process follows the standard retry process that is described in the previous scenario.  

-   If the scan process started, but the client was powered down before the scan completed, it is not considered a scan failure and it does not count as one of the four retries.  

When Configuration Manager receives any of the following Windows Update Agent error codes, it has the client retry the connection:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

To look up the meaning of an error code, you must convert the decimal error code to hexadecimal, and then search for the hexadecimal value on a site such as the [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx).


###  <a name="BKMK_ManuallySwitchSUPs"></a>Manually switch clients to a new software update point
Beginning in Configuration Manager version 1606, you can enable the option for Configuration Manager clients to switch to a new software update point when there are issues with the active software update point. This option results in changes only when a client receives multiple software update points from a management point.

> [!IMPORTANT]    
> When you switch devices to use a new server, the devices use fallback to find that new server. Therefore, review your boundary group configurations, and ensure that your software update points are in the correct boundary groups before you start this change. For details, see [Software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).
>
> The switch to a new software update point generates additional network traffic. The amount of traffic depends on your WSUS configuration settings (update classifications, products, whether the software update points share a WSUS database, etc.). If you plan to switch multiple devices, consider doing so during maintenance windows to reduce the impact to your network during the synchronization to the new software update point server.

#### To enable the option to switch software update points  
Enable this option on a device collection or on a set of selected devices. Once enabled, the clients will look for another software update point at the next scan.

1.  In the Configuration Manager console, go to **Assets and Compliance > Overview > Device collections**.  

2.  On the **Home** tab, in the **Collection** group, click **Client Notification**, and then click **Switch to Next Software Update Point**.  


###  <a name="BKMK_SUP_CrossForest"></a> Software update points in an untrusted forest  
 You can create one or more software update points at a site to support clients in an untrusted forest. To add a software update point in another forest, you must first install and configure a WSUS server in the forest. Then start the wizard to add a Configuration Manager site server with the software update point site system role. In the wizard, configure the following settings to successfully connect to WSUS in the untrusted forest:  

-   Specify a Site System Installation account that can access the WSUS server in the forest.  

-   Specify the WSUS Server Connection account to use to connect to the WSUS server.  

 For example, you have a primary site in forest A with two software update points (SUP01 and SUP02). Also, for the same primary site you have two software update points (SUP03 and SUP04) in forest B. When the switching occurs in this example, the software update points from the same forest as the client are prioritized first.  

###  <a name="BKMK_WSUSSyncSource"></a> Use an existing WSUS server as the synchronization source at the Top-level site  
 Typically, the top-level site in your hierarchy is configured to synchronize software updates metadata with Microsoft Update. When your corporate security policy does not allow access to the Internet from the top-level site, you can configure the synchronization source for the top-level site to use an existing WSUS server that is not in your Configuration Manager hierarchy. For example, you might have a WSUS server installed in your DMZ that has Internet access, but your top-level site does not. You can configure the WSUS server in the DMZ as your synchronization source for software updates metadata. You must ensure that the WSUS server in the DMZ synchronizes software updates that meet the criteria that you need in your Configuration Manager hierarchy. Otherwise, the top-level site might not synchronize the software updates that you expect. When you install the software update point, configure a WSUS connection account that has access to the WSUS server in the DMZ and confirm that the firewall permits traffic for the appropriate ports. For more information, review the [ports used by the software update point to the synchronization source](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="BKMK_NLBSUPSP1"></a> Software update point configured to use an NLB  
 Software update point switching likely addresses the fault tolerance needs that you have. By default, Configuration Manager does not support configuring software update points as NLB clusters. Prior to Configuration Manager version 1702, you could use the Configuration Manager SDK to configure up to four software update points on a NLB cluster. However, starting in Configuration Manager version 1702, software update points are not supported as NLB clusters and upgrades to Configuration Manager version 1702 will be blocked if this configuration is detected. For more information about the Set-CMSoftwareUpdatePoint PowerShell cmdlet, see the [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="BKMK_SUPSecSite"></a> Software update point on a secondary site  
 The software update point is optional on a secondary site. When you install a software update point on a secondary site, the WSUS database is configured as a replica of the default software update point at the parent primary site. You can install only one software update point at a secondary site. The devices that are assigned to a secondary site are configured to use a software update point at the parent site when a software update point is not installed at the secondary site. Typically, you install a software update point at a secondary site when there is limited network bandwidth between the devices that are assigned to the secondary site and the software update points at the parent primary site, or when the software update point approaches the capacity limit. After a software update point is successfully installed and configured at the secondary site, a site-wide policy is updated for client computers that are assigned to the site, and they will start to use the new software update point.  

##  <a name="BKMK_SUPInstallation"></a> Plan for Software Update Point Installation  
 Before you create a software update point site system role in Configuration Manager, there are several requirements that you must consider depending on your Configuration Manager infrastructure. When you configure the software update point to communicate by using SSL, this section is especially important to review because you must take additional steps for the software update points in your hierarchy will work properly. This section provides information about the steps that you must take to successfully plan and prepare for the software update point installation.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requirements for the software update point  
 The software update point site system role must be installed on a site system that meets the minimum requirements for WSUS and the supported configurations for Configuration Manager site systems.  

-   For more information about the minimum requirements for the WSUS server role in Windows Server 2012, see [Review considerations and system requirements](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) in the Windows Server 2012 documentation library.  

-   For more information about the supported configurations for Configuration Manager site systems, see [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="BKMK_PlanningForWSUS"></a> Plan for WSUS installation  

Software updates requires that a supported version of WSUS is installed on all site system servers that you configure for the software update point site system role. Additionally, when you do not install the software update point on the site server, you must install the WSUS Administration Console on the site server computer, if it is not already installed. This allows the site server to communicate with WSUS that runs on the software update point.  

 When you use WSUS on Windows Server 2012, you must configure additional permissions to allow **WSUS Configuration Manager** in Configuration Manager to connect to the WSUS in order to perform periodic health checks. Choose one of the following options to configure the permissions:  

-   Add the **SYSTEM** account to the **WSUS Administrators** group  

-   Add the **NT AUTHORITY\SYSTEM** account as a user for the WSUS database (SUSDB) and configure a minimum of the webService database role membership  

 For more information about how to install WSUS on Windows Server 2012, see [Install the WSUS Server Role](http://go.microsoft.com/fwlink/p/?LinkId=272355) in the Windows Server 2012 documentation library.  

 When you install more than one software update point at a primary site, use the same WSUS database for each software update point in the same Active Directory forest. If you share the same database, it significantly mitigates, but does not completely eliminate the client and the network performance impact that you might experience when clients switch to a new software update point. A delta scan still occurs when a client switches to a new software update point that shares a database with the old software update point, but the scan is much smaller than it would be if the WSUS server had its own database.  

####  <a name="BKMK_CustomWebSite"></a> Configure WSUS to use a custom web site  
 When you install WSUS, you have the option to use the existing IIS Default website, or to create a custom WSUS website. Create a custom website for WSUS so that IIS hosts the WSUS services in a dedicated virtual website, instead of sharing the same web site that is used by the other Configuration Manager site systems or other applications. This is especially true when you install the software update point site system role on the site server. When you run WSUS in Windows Server 2012 or Windows Server 2016, WSUS is configured by default to use port 8530 for HTTP and port 8531 for HTTPS. You must specify these port settings when you create the software update point at a site.  

####  <a name="BKMK_WSUSInfrastructure"></a> Use an existing WSUS infrastructure  
 You can select a WSUS server that was active in your environment before you installed Configuration Manager as a software update point. When the software update point is configured, you must specify the synchronization settings. Configuration Manager connects to the WSUS server that runs on the software update point server and configures WSUS with the same settings. If you synchronized WSUS before it was configured as a software update point with products or classifications that you did not configure as part of the software update point synchronization settings, the software updates metadata for the products and classifications are synchronized for all of the software updates metadata in the WSUS database regardless of the synchronization settings that you configured for the software update point. This might result in unexpected software updates metadata in the site database. You experience the same behavior when you add products or classifications directly in the WSUS Administration console, and then immediately initiate a synchronization. Every hour, by default, Configuration Manager connects to WSUS on the software update point and resets any settings that were modified outside of Configuration Manager. The software updates that do not meet the products and classifications that you specify in synchronization settings are set to expired, and then they are removed from the site database.

 When a WSUS server is configured as a software update point, you are no longer able to use it as a stand-alone WSUS server. If you need a separate stand-alone WSUS server that is not managed by Configuration Manager, you must configure it on a different server.

####  <a name="BKMK_WSUSAsReplica"></a> Configure WSUS as a replica server  
 When you create a software update point site system role on a primary site server, you cannot use a WSUS server that is configured as a replica. When the WSUS server is configured as a replica, Configuration Manager fails to configure the WSUS server, and the WSUS synchronization fails as well. When a software update point is created on a secondary site, Configuration Manager configures WSUS to be a replica server of the WSUS that runs on the software update point at the parent primary site. The first software update point that you install at a primary site is the default software update point. Additional software update points at the site are configured as replicas of the default software update point.  

####  <a name="BKMK_WSUSandSSL"></a> Decide whether to configure WSUS to use SSL  
 You can use the SSL protocol to help secure the WSUS that runs on the software update point. WSUS uses SSL to authenticate client computers and downstream WSUS servers to the WSUS server. WSUS also uses SSL to encrypt software update metadata. When you choose to secure WSUS with SSL, you must prepare the WSUS server before you install the software update point.  

 When you install and configure the software update point, you must select the **Enable SSL communications for the WSUS Server** setting. Otherwise, Configuration Manager configures WSUS not to use SSL. When you enable SSL for WSUS that runs on a software update point, WSUS that runs on the software update point at any child sites must also be configured to use SSL.  

###  <a name="BKMK_ConfigureFirewalls"></a> Configure firewalls  
 Software updates on a Configuration Manager central administration site communicate with the WSUS that runs on the software update point, which in turn communicates with the synchronization source to synchronize software updates metadata. Software update points on a child site communicate with the software update point at the parent site. When there is more than one software update point at a primary site, the additional software update points must communicate with the first software update point that is installed at the site, which is the default software update point.  

 The firewall might need to be configured to accept the HTTP or HTTPS ports that are used by WSUS in following scenarios: when you have a corporate firewall between the Configuration Manager software update point and the Internet; when you have a software update point and its upstream synchronization source; or when you have the additional software update points. The connection to Microsoft Update is always configured to use port 80 for HTTP and port 443 for HTTPS. You can use a custom port for the connection from WSUS that runs on the software update point at a child site to WSUS that runs on the software update point at the parent site. When your security policy does not allow the  connection, you must use the export and import synchronization method. For more information, see the [Synchronization source](#BKMK_SyncSource) section in this article. For more information about the ports that are used by WSUS, see [How to determine the port settings used by WSUS in System Center Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  

#### Restrict Access to Specific Domains  
 If your organization does not allow the ports and protocols to be open to all addresses on the firewall between the active software update point and the Internet, you can restrict access to the following domains, so that WSUS and Automatic Updates can communicate with Microsoft Update:  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 You might need to add the following addresses to the firewall that is located between the two site systems in the following cases: if child sites have a software update point or if there is a remote active Internet-based software update point at a site:  

 **Software update point on the child site**  

-   http://<*FQDN for software update point on child site*>  

-   https://<*FQDN for software update point on child site*>  

-   http://<*FQDN for software update point on parent site*>  

-   https://<*FQDN for software update point on parent site*>  

##  <a name="BKMK_SyncSettings"></a> Plan for synchronization settings  
 Software updates synchronization in Configuration Manager is the process of retrieving the software updates metadata based on criteria that you configure. The top-level site in your hierarchy, the central administration site, or stand-alone primary site synchronizes software updates from Microsoft Update. You have the option to configure the software update point on the top-level site to synchronize with an existing WSUS server, not in the Configuration Manager hierarchy. The child primary sites synchronize software updates metadata from the software update point on the central administration site. Before you install and configure a software update point, use this section to plan for the synchronization settings.  

###  <a name="BKMK_SyncSource"></a> Synchronization source  
 The synchronization source settings for the software update point specify the location for where the software update point retrieves software updates metadata, and whether the WSUS reporting events are created during the synchronization process.  

-   **Synchronization source:** The software update point at the top-level site configures the synchronization source for Microsoft Update by default. You have the option to synchronize the top-level site with an existing WSUS server. The software update point on a child primary site configures the synchronization source as the software update point at the central administration site by default.  

    > [!NOTE]  
    >  The first software update point that you install at a primary site, which is the default software update point, synchronizes with the central administration site. Additional software update points at the primary site synchronize with the default software update point at the primary site.  

     When a software update point is disconnected from Microsoft Update or from the upstream update server, you can configure the synchronization source not to synchronize with a configured synchronization source, but instead to use the export and import function of the WSUSUtil tool to synchronize software updates. For more information, see [Synchronize software updates from a disconnected software update point](../get-started/synchronize-software-updates-disconnected.md).  

-   **WSUS reporting events:** The Windows Update Agent on client computers can create event messages that are used for WSUS reporting. These events are not used by software update in Configuration Manager, and therefore, the **Do not create WSUS reporting events** option is selected by default. When these events are not created, the only time that the client computer should connect to the WSUS server is during software update evaluation and compliance scans. If these events are needed for reporting outside of software updates in Configuration Manager, you need to modify this setting to create WSUS reporting events.  

###  <a name="BKMK_SyncSchedule"></a> Synchronization schedule  
 You can configure the synchronization schedule only at the software update point on the top-level site in the Configuration Manager hierarchy. When you configure the synchronization schedule, the software update point synchronizes with the synchronization source at the date and time that you specified. The custom schedule allows you to synchronize software updates on a date and time when the demands from the WSUS server, site server, and network are low, such as 2:00 AM once a week. Alternatively, you can initiate synchronization on the top-level site by using the **Synchronization Software Updates** action from the **All Software Updates** or **Software Update Groups** node in the Configuration Manager console.  

> [!TIP]  
>  Schedule the software updates synchronization to run by using a time frame that is appropriate for your environment. One common scenario is to set the software updates synchronization schedule to run shortly after the Microsoft regular security update release on the second Tuesday of each month, which is typically referred to as Patch Tuesday. Another common scenario is to set the software updates synchronization schedule to run daily when you use software updates to deliver the Endpoint Protection definition and engine updates.  

 After the software update point successfully completes synchronization, a synchronization request is sent to child sites. If you have additional software update points at a primary site, a synchronization request is sent to each software update point. The process is repeated on every site in the hierarchy.  

###  <a name="BKMK_UpdateClassifications"></a> Update classifications  
 Every software update is defined with an update classification that helps to organize the different types of updates. During the synchronization process, the software updates metadata for the specified classifications will be synchronized. Configuration Manager allows you to synchronize software updates with the following update classifications:  

-   **Critical Updates:** Specifies a broadly released update for a specific problem that addresses a critical, non-security-related bug.  

-   **Definition Updates:** Specifies an update to virus or other definition files.  

-   **Feature Packs:** Specifies new product features that are distributed outside of a product release and feature that are typically included in the next full product release.  

-   **Security Updates:** Specifies a broadly released update for a product-specific, security-related issue.  

-   **Service Packs:** Specifies a cumulative set of hotfixes that are applied to an application. These hotfixes can include security updates, critical updates, software updates, and so on.  

-   **Tools:** Specifies a utility or feature that helps to complete one or more tasks.  

-   **Update Rollups:** Specifies a cumulative set of hotfixes that are packaged together for easy deployment. These hotfixes can include security updates, critical updates, updates, and so on. An update rollup generally addresses a specific area, such as security or a product component.  

-   **Updates:** Specifies an update to an application or file that is currently installed.  

 The update classification settings are configured only on the top-level site. The update classification settings are not configured on the software update point on child sites, because the software updates metadata is replicated from the top-level site to child primary sites. When you select the update classifications, be aware the more classifications that you select, the longer it takes to synchronize the software updates metadata.  

> [!WARNING]  
>  As a best practice, clear all classifications before you synchronize software updates for the first time. After the initial synchronization, select the classifications from Software Update Point Component properties, and then reinitiate synchronization.  

###  <a name="BKMK_UpdateProducts"></a> Products  
 The metadata for each software update defines  one or more products for which the update is applicable. A product is a specific edition of an operating system or application. An example of a product is Microsoft Windows Server 2008. A product family is the base operating system or application from which the individual products are derived. An example of a product family is Microsoft Windows, of which Microsoft Windows Server 2008 is a member. You can specify a product family or individual products within a product family.  

 When software updates are applicable to multiple products, and at least one of the products is selected for synchronization, all of the products will appear in the Configuration Manager console even if some products were not selected. For example, if Windows Server 2012 is the only operating system that you subscribed to, and if a software update applies to Windows Server 2012 and Windows Server 2012 Datacenter Edition, both products will be in the site database.  

 The product settings are configured only on the top-level site. The product settings are not configured on the software update point for child sites because the software updates metadata is replicated from the top-level site to child primary sites. When you select products, be aware that the more products that you select, the longer it takes to synchronize the software updates metadata.  

> [!IMPORTANT]  
>  Configuration Manager stores a list of products and product families that you can choose from when you first install the software update point. Products and product families that are released after Configuration Manager is released might not be available to select until you complete software updates synchronization, which updates the list of available products and product families from which you can choose. As a best practice, clear all products before you synchronize software updates for the first time. After the initial synchronization, select the products from Software Update Point Component properties, and then reinitiate synchronization.  

###  <a name="BKMK_SupersedenceRules"></a>Supersedence rules  
 Typically, a software update that supersedes another software update does one or more of the following actions:  

-   Enhances, improves, or updates the fix that was provided by one or more previously released updates.  

-   Improves the efficiency of the superseded update file package, which is installed on client computers if the update is approved for installation. For example, the superseded update might contain files that are no longer relevant to the fix or to the operating systems that are supported by the new update, so those files are not included in the superseding  file package of the update.  

-   Updates newer versions of a product. In other words, it updates versions that are no longer applicable to older versions or configurations of a product. Updates can also supersede other updates if modifications were made to expand language support. For example, a later revision of a product update for Microsoft Office might remove the support for an older operating system, but it might add additional support for new languages in the initial update release.  

 In the properties for the software update point, you can specify that the superseded software updates are immediately expired, which prevents them from being included in new deployments and flags the existing deployments to indicate that they contain one or more expired software updates. Or, you can specify a period of time before the superseded software updates are expired, which allows you to continue to deploy them. Consider the following scenarios in which you might need to deploy a superseded software update:  

-   If a superseding software update supports only newer versions of an operating system, and some of your client computers run earlier versions of the operating system.  

-   If a superseding software update has more restricted applicability than the software update it supersedes. This would make it inappropriate for some client computers.  

-   If a superseding software update was not approved for deployment in your production environment.  

    > [!NOTE]  
    > When Configuration Manager sets a superseded software update to **Expired**, it does not set the update to **Declined** in WSUS. However, when the WSUS cleanup task runs, the updates set to **Expired** in Configuration Manager are set to a status of **Declined** on the WSUS server and the Windows Update Agent on computers will no longer scan for these updates. This means that clients continue to scan for an expired update until the cleanup task runs. For information about the WSUS cleanup task, see [Software updates maintenance](/sccm/sum/deploy-use/software-updates-maintenance).

###  <a name="BKMK_UpdateLanguages"></a> Languages  
 The language settings for the software update point allow you to configure the languages for which the summary details (software updates metadata) are synchronized for software updates, and the software update file languages that are downloaded for software updates.  

#### Software update file  
 The languages that you configure for the **Software update file** setting in the properties for the software update point provide the default set of languages that are available when you download software updates at a site. You can modify the languages that are selected by default each time that the software updates are downloaded or deployed. During the download process, the software update files for the configured languages are downloaded to the deployment package source location, if the software update files are available in the selected language. Then they are  copied to the content library on the site server, and then they are copied to the distribution points that are configured for the package.  

 The software update file language settings should be configured with the languages that are most often used in your environment. For example, if client computers that are assigned to the site use mostly English and Japanese languages for the operating system or applications, and there are very few other languages that are used at the site, then select English and Japanese in the **Software Update File** column when you download or deploy the software update and clear the other languages. This allows you to use the default settings on the **Language Selection** page of the deployment and to download wizards. This also prevents unneeded update files from being downloaded. This setting is configured at each software update point in the Configuration Manager hierarchy.  

#### Summary details  
 During the synchronization process, the summary details information (software updates metadata) is updated for software updates in the languages that you specify. The metadata provides the information about the software update, such as name, description, products that the update supports, update classification, article ID, download URL, applicability rules, and so on.  

 The summary details settings are configured only on the top-level site. The summary details are not configured on the software update point on child sites because the software updates metadata is replicated from the central administration site down to these sites by using file-based replication. When you select the summary details languages, select only the languages that you need in your environment. The more languages that you select, the longer it takes to synchronize the software updates metadata. Configuration Manager displays the software updates metadata in the locale of the operating system in which the Configuration Manager console runs. If the localized properties for the software updates are not available in the locale of the operating system, the software updates information displays in English.  

> [!IMPORTANT]  
>  It is important that you select all of the summary details languages that you need in your Configuration Manager hierarchy. When the software update point on top-level site synchronizes with the synchronization source, the selected summary details languages determine the software updates metadata that is retrieved. If you modify the summary details languages after synchronization ran at least one time, the software updates metadata is retrieved for the modified summary details languages only for new or updated software updates. The software updates that have already been synchronized are not updated with new metadata for the modified languages unless there is a change to the software update on the synchronization source.  

##  <a name="BKMK_MaintenanceWindow"></a> Plan for a Software Updates Maintenance Window  
 You can add a maintenance window dedicated for software updates installation. This lets you configure a general maintenance window and a different maintenance window for software updates. When a general maintenance window and software updates maintenance window are both configured, clients install software updates only during the software updates maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="BKMK_RestartOptions"></a> Restart options for Windows 10 clients after software update installation
When a software update that requires a restart is deployed using Configuration Manager and installed on a computer, a pending restart is scheduled and a restart dialog box is displayed.

Beginning in Configuration Manager version 1606, the option to **Update and Restart**, and **Update and Shutdown** is available on Windows 10 computers in the Windows Power options whenever there is a pending restart for a Configuration Manager software update. After using one of these options, the restart dialog will not display after the computer restarts.

In previous versions of Configuration Manager, when a restart is pending for Windows 8 and later computers, and when you shut down or restart the computer using the Windows Power options (instead of from the restart dialog), the restart dialog remains after the computer restarts and the computer will still need to restart at the configured deadline.


## Next steps
Once you plan for software updates, see [Prepare for software updates management](../get-started/prepare-for-software-updates-management.md).

**For more information:** <br/>
[Fundamentals of Configuration Manager as a service and Windows as a service](sccm/core/understand/configuration-manager-and-windows-as-service.md)