---
title: High availability
titleSuffix: Configuration Manager
description: Learn how to deploy Configuration Manager by using options that maintain a high level of available service.
ms.date: 12/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# High availability options for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article describes how to deploy Configuration Manager using options that maintain a high level of available service.

The following Configuration Manager options support high availability:

- Configure any central administration or primary site with an additional site server in passive mode.  

- Configure a SQL Server Always On availability group for the site database at primary sites and the central administration site.

- Sites support multiple instances of site system roles that provide important services to clients. For example, management points and distribution points.  

- Central administration sites and primary sites support the backup of the site database. The site database stores all the configurations for sites and clients. The sites in a hierarchy share this configuration data.  

- Built-in site recovery options can reduce server downtime. These advanced options simplify recovery when you have a hierarchy with a central administration site.  

- Clients can automatically remediate typical issues without administrative intervention.  

- Sites generate alerts about clients that fail to submit recent data, which alerts administrators to potential problems.  

- Configuration Manager provides several built-in reports and dashboards. Use these to identify problems and trends before they become problems for server or client operations.  

Configuration Manager includes several features that provide near real-time service. If these features are critical to meet your business requirements, plan and configure your sites and hierarchies for high availability. For example:  

- [Client notification actions](../../../clients/manage/manage-clients.md), such as restart, start Windows Defender scans, or remote desktop.  

- State-based messages for monitoring features such as software updates and endpoint protection.

- [Scripts](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Other features of Configuration Manager don't provide real-time service. These features include, but aren't limited to, client settings, hardware and software inventory, software deployments, and compliance settings. Expect them to operate with some data latency. It's unusual for most scenarios that involve a temporary interruption of service to become a critical problem. To minimize downtime, maintain autonomy of operations, and provide a high level of service, configure your sites and hierarchies with high availability in mind.  

For example, Configuration Manager clients typically operate autonomously by using known schedules and configurations for operations, and schedules to submit data to the site for processing.  

- When clients can't contact the site, they cache data to be submitted until they can contact the site.  

- Clients that can't contact the site continue to operate. They use the last known schedules and cached information, until they can contact the site and receive new policies. For example, a client may keep a previously downloaded application that they must run or install.

- The site monitors its site systems and clients for periodic status updates. It can generate alerts when these components fail to register.  

- Built-in reports provide insight to ongoing operations, historical operations, and current trends. Configuration Manager also supports state-based messages that provide near real-time information for ongoing operations.  


## <a name="bkmk_snh"></a> High availability for sites and hierarchies  

### Use a site server in passive mode

Install an additional site server in *passive* mode for a central administration or primary site. The site server in passive mode is in addition to your existing site server in *active* mode. A site server in passive mode is available for immediate use, when needed. For more information, see [Site server high availability](site-server-high-availability.md).  

### Use a remote content library

Move the site's content library to a remote location that provides highly available storage. This feature is a requirement for site server high availability. For more information, see [Configure a remote content library for the site server](../../../plan-design/hierarchy/remote-content-library.md).

### Centralize content sources

All software content in Configuration Manager requires a package source location on the network. Use centralized, highly available storage to host a common package source location for all content.

### Use a SQL Server Always On solution for the site database

Configuration Manager supports the following SQL Server Always On solutions for the site database:

- Host the site database at primary sites and the central administration site in an availability group. For more information, see [Prepare to use a SQL Server Always On availability group](sql-server-alwayson-for-a-highly-available-site-database.md).

- Use a failover cluster instance for the database at a central administration site or primary site. For more information, see [Use a SQL Server Always On failover cluster instance](use-a-sql-server-cluster-for-the-site-database.md).

Secondary sites can't use SQL Server Always On, and don't support backup or restoration of their site database. Recover a secondary site by reinstalling the secondary site from its parent primary site.

### Deploy a hierarchy of sites with a central administration site, and one or more child primary sites

This configuration can provide fault tolerance when your sites manage overlapping segments of your network. It also offers an additional recovery option to use the information in the shared database available at another site, to rebuild the site database at the recovered site. Use this option to replace a failed or unavailable backup of the failed site's database.  

### Create regular backups at central administration sites and primary sites

When you create and test a regular site backup, this makes sure that you have the data necessary to recover a site. You also practice recovering a site in the minimal amount of time.  

### Install multiple instances of site system roles

When you install multiple instances of critical site system roles, you provide redundant points of contact for clients. For example, multiple management points and distribution points provide redundant service in the event that a specific server is offline.  

### Install multiple instances of the SMS Provider at a site

The SMS Provider provides the point of administrative contact for one or more Configuration Manager consoles. To provide redundancy for contact points to administer your site and hierarchy, install multiple SMS Providers.  


## <a name="bkmk_ssr"></a> High availability for site system roles

At each site, you deploy site system roles to provide the services that you want clients to use at that site. The site database contains the configuration information for the site and for all clients. Use one or more of the available options to provide for high availability of the site database, and the recovery of the site and site database if needed.  

### Redundancy for important site system roles

- Distribution point  

- Management point  

- Software update point  

- State migration point  

To provide redundancy for reporting on sites and clients, install multiple instances of the reporting services point.

Failover support for a software update point in a network load balancing (NLB) cluster was deprecated in version 1702. For more information, see [Removed and deprecated features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#unsupported-and-removed-features). To provide redundancy for software update points, use software update point switching. This allows clients to connect to a new software update point server if one fails or becomes unavailable. For more information, see [Software update point switching](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)  

### Built-in site backup

Configuration Manager includes a built-in backup task to help you back up your site and critical information on a regular schedule. Additionally, the Configuration Manager setup wizard supports site restoration actions to help you restore a site to operations.  

### Publishing to Active Directory Domain Services and DNS

Configure each site to publish data about the site to Active Directory Domain Services and DNS. This publishing enables clients to identify the most accessible server on the network. Clients also use it to identify when new site system servers are available to provide important services, such as management points.  

### SMS Provider and Configuration Manager console

Configuration Manager supports installing multiple SMS Providers on separate servers as multiple access points for the console. If one SMS Provider server is offline, you can still view and manage sites and clients.  

When a Configuration Manager console connects to a site, it connects to an instance of the SMS Provider at that site. The instance of the SMS Provider is randomly selected. If the selected SMS Provider isn't available, you have the following options:  

- Reconnect the console to the site. Each new connection request is randomly assigned an instance of the SMS Provider. It's possible that the new connection is assigned an available instance.  

- Connect the console to a different Configuration Manager site and manage the configuration from that connection. This option introduces a slight delay of configuration changes of no more than a few minutes. After the SMS Provider for the site is online, reconnect your Configuration Manager console directly to the site that you want to manage.  

Install the Configuration Manager console on multiple computers for use by administrators. Each SMS Provider supports connections from more than one console.  

### Management point

Install multiple management points at each primary site, and enable the sites to publish site data to your Active Directory infrastructure, and to DNS.  

Multiple management points help to load-balance the use of any single management point by multiple clients. Also consider installing one or more database replicas for management points. This configuration decreases the processor-intensive operations of the management point. It also increases the availability of this critical site system role.  

Secondary sites only support installation of one management point, which must be located on the secondary site server. Management points at secondary sites aren't considered to have a highly available configuration.  

> [!NOTE]  
> Devices managed by on-premises mobile device management connect to only one management point at a primary site. The management point is assigned by Configuration Manager to the mobile device during enrollment and then doesn't change. When you install multiple management points and enable more than one for mobile devices, the management point that's assigned to a mobile device client is non-deterministic.  
>
> If the management point that a mobile device client uses becomes unavailable, you must resolve the problem with that management point or wipe the mobile device and re-enroll the mobile device so that it can be assigned to an operational management point that is enabled for mobile devices.  

### Distribution point

Install multiple distribution points, and deploy content to multiple distribution points. Add more than one distribution point per boundary group to make sure clients get several options in their content request. Configure boundary group relationships so that they have a predicable fallback behavior to another boundary group or content-enabled cloud management gateway. For more information, see [Configure boundary groups](boundary-groups.md).

## <a name="bkmk_client"></a> High availability for clients  

### Client operations are autonomous

Configuration Manager client autonomy includes the following behaviors:  

- Clients don't require continuous contact with any specific site system servers. They use known configurations to perform preconfigured actions on a schedule.  

- Clients can use any available instance of a site system role that provides services to clients. They attempt to contact known servers until they locate an available server.  

- Clients can run inventory, software deployments, and similar scheduled actions independent of direct contact with site system servers.  

- Clients that are configured to use a fallback status point can submit details to the fallback status point when they can't communicate with a management point.  

### Clients can repair themselves

Clients automatically remediate most typical issues without direct administrative intervention.  

- Periodically, clients self-evaluate their status. They take action to remediate typical problems by using a local cache of remediation steps and source files for repairs.  

- When a client fails to submit status information to its site, the site can generate an alert. Administrative users that receive these alerts can take immediate action to restore the normal operation of the client.  

### Clients cache information to use in the future

When a client communicates with a management point, the client can obtain and cache the following information:  

- Client settings  

- Client schedules  

- Information about software deployments and a download of the software the client is scheduled to install, when the deployment is configured for this action.  

When a client can't contact a management point, the clients locally cache the status, state, and client information they report to the site. The client transfers this data after it establishes contact with a management point.  

### Client can submit status to a fallback status point

When you configure a client to use a fallback status point, you provide an additional point of contact for the client to submit important details about its operation. Clients that are configured to use a fallback status point continue to send status about their operations to that site system role even when the client can't communicate with a management point.  

### Central management of client data and client identity

The site database, rather than the individual client, retains important information about each client's identity, and associates that data to a specific computer, or user.  

- The client source files on a computer can be uninstalled and reinstalled without affecting the historical records for the computer where the client is installed.  

- Failure of a client computer doesn't affect the integrity of the information that's stored in the database. This information can remain available for reporting.  


## <a name="bkmk_nonHAoptions"></a> Options for sites and site system roles that aren't highly available

Several site systems don't support multiple instances at a site or in the hierarchy. This information can help you prepare for these site systems going offline.  

### Asset intelligence synchronization point (hierarchy)

> [!IMPORTANT]
> Starting in November 2021, this feature of Configuration Manager is deprecated.<!-- 12454890 --> For more information, see [Asset intelligence deprecation](../../../clients/manage/asset-intelligence/deprecation.md).

This site system role isn't considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

- Resolve the reason for the site system to be offline.  

- Uninstall the role from the current server, and install the role on a new server.  

### Endpoint protection point (hierarchy)

This site system role isn't considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

- Resolve the reason for the site system to be offline.  

- Uninstall the role from the current server, and install the role on a new server.  

### Enrollment point (site)

This site system role isn't considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

- Resolve the reason for the site system to be offline.  

- Uninstall the role from the current server, and install the role on a new server.  

### Enrollment proxy point (site)

This site system role isn't considered mission critical and provides optional functionality in Configuration Manager. However, you can install multiple instances of this site system role at a site, and at multiple sites in the hierarchy. If this site system goes offline, use one of the following options:  

- Resolve the reason for the site system to be offline.  

- Uninstall the role from the current server, and install the role on a new server.  

When you have more than one enrollment proxy server in a site, use a DNS alias for the server name. When you use this configuration, DNS round robin provides some fault tolerance and load balancing for when users enroll their mobile devices.  

### Fallback status point (site or hierarchy)

This site system role isn't considered mission critical and provides optional functionality in Configuration Manager. If this site system goes offline, use one of the following options:  

- Resolve the reason for the site system to be offline.  

- Uninstall the role from the current server, and install the role on a new server. Because clients are assigned the fallback status point during client installation, you need to modify existing clients to use the new site system server.  

### Service connection point (hierarchy)

While this site system role is critical for keeping Configuration Manager current branch up to date, it's generally not used frequently. If this system goes offline, use one of the following options:

- Resolve the reason for the site system to be offline.  

- Uninstall the role from the current server, and install the role on a new server.  


## See also

- [Supported configurations](../../../plan-design/configs/supported-configurations.md)  

- [Recommended hardware](../../../plan-design/configs/recommended-hardware.md)  

- [Supported operating systems for site system servers](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Site failure impacts](../../manage/site-failure-impacts.md)
