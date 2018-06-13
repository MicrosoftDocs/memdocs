---
title: High availability
titleSuffix: Configuration Manager
description: Learn how to deploy Configuration Manager by using options that maintain a high level of available service.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# High availability options for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*



You can deploy System Center Configuration Manager using options that maintain a high level of available service.   

Options that support high availability:   

-   Sites support multiple instances of site system servers that provide important services to clients.  

-   Central administration sites and primary sites support the backup of the site database. The site database contains all the configurations for sites and clients, and it is shared between sites in a hierarchy that contain a central administration site.  

-   Built-in site recovery options can reduce server downtime and include advanced options that simplify recovery when you have a hierarchy with a central administration site.  

-   Clients can automatically remediate typical issues without administrative intervention.  

-   Sites generate alerts about clients that fail to submit recent data, which alerts administrators to potential problems.  

-   Configuration Manager provides several built-in reports that enable you to identify problems and trends before they become problems for server or client operations.  

 Configuration Manager does not provide a real-time service and you must expect it to operate with some data latency. Therefore, it is unusual for most scenarios that involve a temporary interruption of service to become a critical problem. When you have configured your sites and hierarchies with high availability in mind, downtime can be minimized, autonomy of operations maintained, and a high level of service provided.  

 For example, Configuration Manager clients typically operate autonomously by using known schedules and configurations for operations, and schedules to submit data to the site for processing.  

-   When clients cannot contact the site, they cache data to be submitted until they can contact the site.  

-   Clients that cannot contact the site continue to operate by using the last known schedules and cached information, such as a previously downloaded application that they must run or install, until they can contact the site and receive new policies.  

-   The site monitors its site systems and clients for periodic status updates, and can generate alerts when these fail to register.  

-   Built-in reports provide insight to ongoing operations as well as historical operations and trends. Configuration Manager also supports state-based messages that provide near real-time information for ongoing operations.  

  Use the information in this topic with the information in the following articles:
-   [Recommended hardware](../../core/plan-design/configs/recommended-hardware.md)
-   [Supported operating systems for site system serveres](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="bkmk_snh"></a> High availability for sites and hierarchies  
 **Use a SQL Server cluster to host the site database:**  

 When you use a SQL Server cluster for the database at a central administration site or primary site, you use the fail-over support built into SQL Server.  

 Secondary sites cannot use a SQL Server cluster, and do not support backup or restoration of their site database. Recover a secondary site by reinstalling the secondary site from its parent primary site.  

 **Use a SQL Server AlwaysOn availability group to host the site database:**  

 Beginning with version 1602, you can use SQL Server AlwaysOn availability groups to host the site database at primary sites and the central administration site as a high-availability and disaster-recovery solution. For more information, see [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

 **Deploy a hierarchy of sites with a central administration site, and one or more child primary sites:**  

 This configuration can provide fault tolerance when your sites manage overlapping segments of your network. In addition, this configuration offers an additional recovery option to use the information in the shared database available at another site, to rebuild the site database at the recovered site. You can use this option to replace a failed or unavailable backup of the failed site's database.  

 **Create regular backups at central administration sites and primary sites:**  

 When you create and test a regular site backup, you can ensure that you have the data necessary to recover a site, and the experience to recover a site in the minimal amount of time.  

 **Install multiple instances of site system roles:**  

 When you install multiple instances of critical site system roles such as the management point and distribution point, you provide redundant points of contact for clients in the event that a specific site system server is off-line.  

 **Install multiple instances of the SMS Provider at a site:** The SMS Provider provides the point of administrative contact for one or more Configuration Manager consoles. When you install multiple SMS Providers, you can provide redundancy for contact points to administer your site and hierarchy.  

##  <a name="bkmk_ssr"></a> High availability for site system roles  
 At each site, you deploy site system roles to provide the services that you want clients to use at that site. The site database contains the configuration information for the site and for all clients. Use one or more of the available options to provide for high availability of the site database, and the recovery of the site and site database if needed.  

 **Redundancy for important site system roles:**  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Distribution point  

-   Management point  

-   Software update point  

-   State migration point  

 You can install multiple instance of the Reporting services point role to provide redundancy for reporting on sites and clients.

 You can use PowerShell to install the Software update point site system role on a Windows Network Load Balancing (NLB) cluster to provide failover support  


 **Built-in site backup:**  

 Configuration Manager includes a built-in backup task to help you back up your site and critical information on a regular schedule. Additionally, the Configuration Manager Setup wizard supports site restoration actions to help you restore a site to operations.  

 **Publishing to Active Directory Domain Services and DNS:**  

 You can configure each site to publish data about site system servers and services to Active Directory Domain Services and to DNS. This enables clients to identify the most accessible server on the network, and to identify when new site system servers that can provide important services, such as management points, are available.  

 **SMS Provider and Configuration Manager console:**  

 Configuration Manager supports installing multiple SMS Providers, each on a separate computer, to ensure multiple access points for the Configuration Manager console. This ensures that if one SMS Provider computer is offline, you maintain the ability to view and reconfigure Configuration Manager sites and clients.  

 When a Configuration Manager console connects to a site, it connects to an instance of the SMS Provider at that site. The instance of the SMS Provider is selected nondeterministically. If the selected SMS Provider is not available, you have the following options:  

-   Reconnect the console to the site. Each new connection request is nondeterministically assigned an instance of the SMS Provider and it is possible that the new connection will be assigned an available instance.  

-   Connect the console to a different Configuration Manager site and manage the configuration from that connection. This introduces a slight delay of configuration changes of no more than a few minutes. After the SMS Provider for the site is on-line, you can reconnect your Configuration Manager console directly to the site that you want to manage.  

 You can install the Configuration Manager console on multiple computers for use by administrative users. Each SMS Provider supports connections from multiple Configuration Manager consoles.  

 **Management point:**  

 Install multiple management points at each primary site, and enable the sites to publish site data to your Active Directory infrastructure, and to DNS.  

 Multiple management points help to load-balance the use of any single management point by multiple clients. In addition, you can install one or more database replicas for management points to decrease the CPU-intensive operations of the management point, and to increase the availability of this critical site system role.  

 Because you can install only one management point in a secondary site, which must be located on the secondary site server, management points at secondary sites are not considered to have a highly available configuration.  

> [!NOTE]  
>  Devices managed by on-premises mobile device management connect to only one management point at a primary site. The management point is assigned by Configuration Manager to the mobile device during enrollment and then does not change. When you install multiple management points and enable more than one for mobile devices, the management point that is assigned to a mobile device client is non-deterministic.  
>   
>  If the management point that a mobile device client uses becomes unavailable, you must resolve the problem with that management point or wipe the mobile device and re-enroll the mobile device so that it can be assigned to an operational management point that is enabled for mobile devices.  

 **Distribution point:**  

 Install multiple distribution points, and deploy content to multiple distribution points. You can configure overlapping boundary groups for content location to ensure that clients on each subnet can access a deployment from two or more distribution points. Finally, consider configuring one or more distribution points as fallback locations for content.  

 For more information about fallback locations for content, see  [Manage content and content infrastructure for System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 **Application Catalog web service point and Application Catalog website point:**  

 You can install multiple instances of each site system role, and for best performance, deploy one of each on the same site system computer.  

 Each Application Catalog site system role provides the same information as other instances of that site system role regardless of the location of this site server role in the hierarchy. Therefore, when a client makes a request for the Application Catalog and you have configured the Default Application Catalog website point device client setting for Automatically detect, the client can be directed to an available instance. Preference is given to local Application Catalog site system servers, based on the current network location of the client.  

 For more information about this client setting and how automatic detection works, see the [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent) section in the [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md) topic.  

##  <a name="bkmk_client"></a> High availability for clients  
 **Client operations are autonomous:**  

 Configuration Manager client autonomy includes the following:  

-   Clients do not require continuous contact with any specific site system servers. They use known configurations to perform preconfigured actions on a schedule.  

-   Clients can use any available instance of a site system role that provides services to clients, and they will attempt to contact known servers until an available server is located.  

-   Clients can run inventory, software deployments, and similar scheduled actions independent of direct contact with site system servers.  

-   Clients that are configured to use a fallback status point can submit details to the fallback status point when they cannot communicate with a management point.  

 **Clients can repair themselves:**  

 Clients automatically remediate most typical issues without direct administrative intervention:  

-   Periodically, clients self-evaluate their status and take action to remediate typical problems by using a local cache of remediation steps and source files for repairs.  

-   When a client fails to submit status information to its site, the site can generate an alert. Administrative users that receive these alerts can take immediate action to restore the normal operation of the client.  

 **Clients cache information to use in the future:**  

 When a client communicates with a management point, the client can obtain and cache the following information:  

-   Client settings.  

-   Client schedules.  

-   Information about software deployments and a download of the software the client is scheduled to install, when the deployment is configured for this action.  

 When a client cannot contact a management point the clients locally cache the status, state, and client information they report to the site, and transfer this data after they establish contact with a management point.  

 **Client can submit status to a fallback status point:**  

 When you configure a client to use a fallback status point, you provide an additional point of contact for the client to submit important details about its operation. Clients that are configured to use a fallback status point continue to send status about their operations to that site system role even when the client cannot communicate with a management point.  

 **Central management of client data and client identity:**  

 The site database, rather than the individual client, retains important information about each client’s identity, and associates that data to a specific computer, or user. This means:  

-   The client source files on a computer can be uninstalled and reinstalled without affecting the historical records for the computer where the client is installed.  

-   Failure of a client computer does not affect the integrity of the information that is stored in the database. This information can remain available for reporting.  

##  <a name="bkmk_nonHAoptions"></a> Options for sites and site system roles that are not highly available  
 Several site systems do not support multiple instances at a site or in the hierarchy. This information can help you prepare for these site systems going off-line.  

 **Site server (site):**  

 Configuration Manager does not support the installation of the site server for each site on a Windows Server cluster or NLB cluster.  

 The following information can help you prepare for when a site server fails or is not operational:  

-   Use the built-in backup task to regularly create a backup of the site. In a test environment, regularly practice restoring sites from a backup.  

-   Deploy multiple Configuration Manager primary sites in a hierarchy with a central administration site to create redundancy. If you experience a site failure, consider using Windows group policy or logon scripts to reassign clients to a functional site.  

-   If you have a hierarchy with a central administration site, you can recover the central administration site or a child primary site by using the option to recover a site database from another site in your hierarchy.  

-   Secondary sites cannot be restored, and must be reinstalled.  

 **Asset Intelligence synchronization point (hierarchy):**  

 This site system role is not considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

-   Resolve the reason for the site system to be off-line.  

-   Uninstall the role from the current server, and install the role on a new server.  

 **Endpoint Protection point (hierarchy):**  

 This site system role is not considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

-   Resolve the reason for the site system to be off-line.  

-   Uninstall the role from the current server, and install the role on a new server.  

 **Enrollment point (site):**  

 This site system role is not considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

-   Resolve the reason for the site system to be off-line.  

-   Uninstall the role from the current server, and install the role on a new server.  

 **Enrollment proxy point (site):**  

 This site system role is not considered mission critical and provides optional functionality in Configuration Manager. However, you can install multiple instances of this site system role at a site, and at multiple sites in the hierarchy. If this site system goes offline, use one of the following options:  

-   Resolve the reason for the site system to be off-line.  

-   Uninstall the role from the current server, and install the role on a new server.  

 When you have more than one enrollment proxy server in a site, use a DNS alias for the server name. When you use this configuration, DNS round robin provides some fault tolerance and load balancing for when users enroll their mobile devices.  

 **Fallback status point (site or hierarchy) :**  

 This site system role is not considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

-   Resolve the reason for the site system to be off-line.  

-   Uninstall the role from the current server, and install the role on a new server. Because clients are assigned the fallback status point during client installation, you will need to modify existing clients to use the new site system server.  

### See also  
 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)
