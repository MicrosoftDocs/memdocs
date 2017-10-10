---
title: "Discovery methods"
titleSuffix: "Configuration Manager"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# About discovery methods for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager discovery methods can find different devices on your network or devices and users from Active Directory. To efficiently use a discovery method, you should understand its available configurations and limitations.  

##  <a name="bkmk_aboutForest"></a> Active Directory Forest Discovery  
 **Configurable:** Yes  

 **Enabled by default:** No  

 **Accounts** you can use to run this method:  

-   **Active Directory Forest Discovery Account** (user defined)  

-   **Computer account** of the site server  

Unlike other Active Directory discovery methods, Active Directory Forest Discovery does not discover resources that you can manage. Instead, this method discovers network locations that are configured in Active Directory and can convert those locations into boundaries for use throughout your hierarchy.  

When this method runs, it searches the local Active Directory forest, each trusted forest, and each additional forest that you configure in the **Active Directory Forests** node of the Configuration Manager console.  

Use Active Directory Forest Discovery to:  

-   Discover Active Directory sites and subnets, and then create Configuration Manager boundaries based on those network locations.  

-   Identify supernets that are assigned to an Active Directory site and convert each supernet into an IP address range boundary.  

-   Publish to Active Directory Domain Services (AD DS) in a forest when publishing to that forest is enabled and the specified Active Directory Forest Account has permissions to that forest.  

You can manage Active Directory Forest Discovery in the Configuration Manager console from the following nodes under **Hierarchy Configuration** in the **Administration** workspace:  

-   **Discovery Methods**: Here you can enable Active Directory Forest Discovery to run at the top-level site of your hierarchy. You can also specify a simple schedule to run discovery, and configure it to automatically create boundaries from the IP subnets and Active Directory sites that it discovers. Active Directory Forest Discovery cannot be run at a child primary site or at a secondary site.  

-   **Active Directory Forests**: Here you configure the additional Active Directory forests that you want to discover, specify the account to use as the Active Directory Forest Account for each forest, and configure publishing to each forest. Additionally, you can monitor the discovery process and add IP subnets and Active Directory sites to Configuration Manager as boundaries and members of boundary groups.  

To configure publishing for Active Directory forests for each site in your hierarchy, connect your Configuration Manager console to the top-level site of your hierarchy. The **Publishing** tab in an Active Directory site's **Properties** dialog box can show only the current site and its child sites. When publishing is enabled for a forest and that forest's schema is extended for Configuration Manager, the following information is published for each site that is enabled to publish to that Active Directory forest:  

-    **SMS-Site-&lt;site code>**

-   **SMS-MP-&lt;site code>-&lt;site system server name>**  

-   **SMS-SLP-&lt;site code>-&lt;site system server name>**  

-   **SMS-&lt;site code>-&lt;Active Directory site name or subnet>**  

> [!NOTE]  
>  Secondary sites always use the secondary site server computer account to publish to Active Directory. If you want secondary sites to publish to Active Directory, ensure that the secondary site server computer account has permissions to publish to Active Directory. A secondary site cannot publish data to an untrusted forest.  

> [!CAUTION]  
>  When you uncheck the option to publish a site to an Active Directory forest, all previously published information for that site, including available site system roles, is removed from Active Directory.  

Actions for Active Directory Forest Discovery are recorded in the following logs:  

-   All actions, except actions related to publishing, are recorded in the **ADForestDisc.Log** file in the **&lt;InstallationPath>\Logs** folder on the site server.  

-   Active Directory Forest Discovery publishing actions are recorded in the **hman.log** and **sitecomp.log** files in the **&lt;InstallationPath>\Logs** folder on the site server.  

For more information about how to configure this discovery method, see [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutGroup"></a> Active Directory Group Discovery  
**Configurable:** Yes  

**Enabled by default:** No  

**Accounts** you can use to run this method:  

-   **Active Directory Group Discovery Account**  (user defined)  

-   **Computer account** of the site server  

> [!TIP]  
>  In addition to the information in this section, see [Common features of Active Directory Group, System, and User Discovery](#bkmk_shared).  

Use this method to search Active Directory Domain Services to identify:  

-   Local, global, and universal security groups.  

-   The membership of groups.  

-   Limited information about a group's member computers and users, even when another discovery method has not previously discovered those computers and users.  

This discovery method is intended to identify groups and the group relationships of members of groups. By default, only security groups are discovered. If you want to also find the membership of distribution groups, you must check the box for the option **Discover the membership of distribution groups** on the **Option** tab in the **Active Directory Group Discovery Properties** dialog box.  

Active Directory Group Discovery does not support the extended Active Directory attributes that can be identified by using Active Directory System Discovery or Active Directory User Discovery. Because this discovery method is not optimized to discover computer and user resources, consider running this discovery method after you have run Active Directory System Discovery and Active Directory User Discovery. This is because this method creates a full discovery data record (DDR) for groups, but only a limited DDR for computers and users that are members of groups.  

You can configure the following discovery scopes that control how this method searches for information:  

-   **Location**: Use a location if you want to search one or more Active Directory containers. This scope option supports a recursive search of the specified Active Directory containers that also searches each child container under the container that you specify. This process continues until no more child containers are found.  

-   **Groups**: Use groups if you want to search one or more specific Active Directory groups. You can configure **Active Directory Domain** to use the default domain and forest, or limit the search to an individual domain controller. Additionally, you can specify one or more groups to search. If you do not specify at least one group, all groups found in the specified **Active Directory Domain** location are searched.  

> [!CAUTION]  
>  When you configure a discovery scope, choose only the groups that you must discover. This is because Active Directory Group Discovery tries to discover each member of each group in the discovery scope. Discovery of large groups can require extensive use of bandwidth and Active Directory resources.  

> [!NOTE]  
>  Before you can create collections that are based on extended Active Directory attributes (and to ensure accurate discovery results for computers and users), run Active Directory System Discovery or Active Directory User Discovery, depending on what you want to discover.  

Actions for Active Directory Group Discovery are recorded in the file **adsgdis.log** in the **&lt;InstallationPath\>\LOGS** folder on the site server.  

For more information about how to configure this discovery method, see [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutSystem"></a> Active Directory System Discovery  
**Configurable:** Yes  

**Enabled by default:** No  

**Accounts** you can use to run this method:  

-   **Active Directory System Discovery Account**  (user defined)  

-   **Computer account** of the site server  

> [!TIP]  
>  In addition to the information in this section, see [Common features of Active Directory Group, System, and User Discovery](#bkmk_shared).  

Use this discovery method to search the specified Active Directory Domain Services locations for computer resources that can be used to create collections and queries. You can also install the Configuration Manager client on a discovered device by using client push installation.  

By default, this method discovers basic information about the computer, including the following:  

-   Computer name  

-   Operating system and version  

-   Active Directory container name  

-   IP address  

-   Active Directory site  

-   Time stamp of last logon  

To successfully create a DDR for a computer, Active Directory System Discovery must be able to identify the computer account and then successfully resolve the computer name to an IP address.  

In the **Active Directory System Discovery Properties** dialog box, on the **Active Directory Attributes** tab, you can view the full list of default object attributes that Active Directory System Discovery has returned. You can also configure the method to discover additional (extended) attributes.  

Actions for Active Directory System Discovery are recorded in the file **adsysdis.log** in the **&lt;InstallationPath\>\LOGS** folder on the site server.  

For more information about how to configure this discovery method, see [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutUser"></a> Active Directory User Discovery  
**Configurable:** Yes  

**Enabled by default:** No  

**Accounts** you can use to run this method:  

-   **Active Directory User Discovery Account**  (user defined)  

-   **Computer account** of the site server  

> [!TIP]  
>  In addition to the information in this section, see [Common features of Active Directory Group, System, and User Discovery](#bkmk_shared).  

Use this discovery method to search Active Directory Domain Services to identify user accounts and associated attributes. By default, this method discovers basic information about the user account, including the following:  

-   User name  

-   Unique user name (includes domain name)  

-   Domain  

-   Active Directory container names  

In the **Active Directory User Discovery Properties** dialog box, on the **Active Directory Attributes** tab, you can view the full default list of object attributes that Active Directory User Discovery has returned. You can also configure the method to discover additional (extended) attributes.

Actions for Active Directory User Discovery are recorded in the file **adusrdis.log** in the **&lt;InstallationPath\>\LOGS** folder on the site server.  

For more information about how to configure this discovery method, see [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

## <a name="azureaddisc"></a> Azure Active Directory User Discovery
Beginning with version 1706, you can use Azure Active Directory (Azure AD) User Discovery, when you configure your environment to use Azure services.
Use this discovery method to search your Azure AD for users who authenticate to your instance of Azure AD, to find the following attributes:  
-   objectId
-   displayName
-   mail
-   mailNickname
-   onPremisesSecurityIdentifier
-   userPrincipalName
-   AAD tenantID

This method supports a full synchronization and delta synchronization of User data from Azure AD. This information can then be used along-side discovery data you collect from the other discovery methods.

Actions for Azure AD User Discovery are recorded in the SMS_AZUREAD_DISCOVERY_AGENT.log file on the top-tier site server of the hierarchy.

To configure Azure AD User Discovery, you use the Azure Services Wizard.  For information about how to configure this discovery method, see [Configure Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods).





##  <a name="bkmk_aboutHeartbeat"></a> Heartbeat Discovery  
**Configurable:** Yes  

**Enabled by default:** Yes  

**Accounts** you can use to run this method:  

-   **Computer account** of the site server  

Heartbeat Discovery differs from other Configuration Manager discovery methods. It is enabled by default and runs on each computer client (instead of on a site server) to create a DDR. For mobile device clients, this DDR is created by the management point that the mobile device client is using. To help maintain the database record of Configuration Manager clients, do not disable Heartbeat Discovery. In addition to maintaining the database record, this method can force discovery of a computer as a new resource record or can repopulate the database record of a computer that was deleted from the database.  

Heartbeat Discovery runs either on a schedule configured for all clients in the hierarchy, or if manually invoked, on a specific client by running the **Discovery Data Collection Cycle** on the **Action** tab in a client’s Configuration Manager program. The default schedule for Heartbeat Discovery is set to every 7 days. If you change the heartbeat discovery interval, ensure that it runs more frequently than the site maintenance task **Delete Aged Discovery Data**, which deletes inactive client records from the site database. You can configure the **Delete Aged Discovery Data** task only for primary sites.  

When Heartbeat Discovery runs, it creates a DDR that has the client’s current information. The client then copies this small file (about 1 KB in size) to a management point so that a primary site can process it. The file has the following information:  

-   Network location  

-   NetBIOS name  

-   Version of the client agent  

-   Operational status details  

Heartbeat Discovery is the only discovery method that provides details about the client installation status. It does so by updating the system resource client attribute to set a value equal to **Yes**.  

> [!NOTE]  
>  Even when Heartbeat Discovery is disabled, DDRs are still created and submitted for active mobile device clients. This ensures that the **Delete Aged Discovery Data** task does not affect active mobile devices. This is done because when the **Delete Aged Discovery Data** task deletes a database record for a mobile device, it also revokes the device certificate and blocks the mobile device from connecting to management points.  

Actions for Heartbeat Discovery are logged in the following locations:  

-   For computer clients, Heartbeat Discovery actions are recorded on the client in the **InventoryAgent.log** file in the *%Windir%\CCM\Logs* folder.  

-   For mobile device clients, Heartbeat Discovery actions are recorded in the **DMPRP.log** file in the *%Program Files%\CCM\Logs* folder of the management point that the mobile device client uses.  

For more information about how to configure this discovery method, see [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutNetwork"></a> Network Discovery  
**Configurable:** Yes  

**Enabled by default:** No  

**Accounts** you can use to run this method:  

-   **Computer account** of the site server  

Use this method to discover the topology of your network and to discover devices on your network that have an IP address. Network Discovery searches your network for IP-enabled resources by querying servers that run a Microsoft implementation of DHCP, Address Resolution Protocol (ARP) caches in routers, SNMP-enabled devices, and Active Directory domains.  

Before you can use Network Discovery, you must specify the *level* of discovery to run. You also configure one or more discovery mechanisms that enable Network Discovery to query for network segments or devices. You can also configure settings that help control discovery actions on the network. Finally, you define one or more schedules for when Network Discovery runs.  

For this method to successfully discover a resource, Network Discovery must identify the IP address and the subnet mask of the resource. The following methods are used to identify the subnet mask of an object:  

-   **Router ARP cache:** Network Discovery queries the ARP cache of a router to find subnet information. Typically, data in a router ARP cache has a short time-to-live. Therefore, when Network Discovery queries the ARP cache, the ARP cache might no longer have information about the requested object.  

-   **DHCP:** Network Discovery queries each DHCP server that you specify to discover the devices for which the DHCP server has provided a lease. Network Discovery supports only DHCP servers that run the Microsoft implementation of DHCP.  

-   **SNMP device:** Network Discovery can directly query a SNMP device. For Network Discovery to query a device, the device must have a local SNMP agent installed. You must also configure Network Discovery to use the community name that the SNMP agent is using.  

When discovery identifies an IP-addressable object and can determine the object's subnet mask, it creates a DDR for that object. Because different types of devices can connect to the network, Network Discovery can discover resources that cannot support the Configuration Manager client software. For example, devices that can be discovered but not managed include printers and routers.  

Network Discovery can return several attributes as part of the discovery record that it creates. These include:  

-   NetBIOS name  

-   IP addresses  

-   Resource domain  

-   System roles  

-   SNMP community name  

-   MAC addresses  

Network Discovery activity is recorded in the **Netdisc.log** file in *&lt;InstallationPath\>\Logs* on the site server that runs discovery.  

 For more information about how to configure this discovery method, see [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

> [!NOTE]  
>  Complex networks and low-bandwidth connections can cause Network Discovery to run slowly and generate significant network traffic. As a best practice, run Network Discovery only when the other discovery methods cannot find the resources that you have to discover. For example, use Network Discovery if you must discover workgroup computers. Other discovery methods do not discover workgroup computers.  

###  <a name="BKMK_NetDiscLevels"></a> Levels of Network Discovery  
When you configure Network Discovery, you specify one of three levels of discovery:  

|Level of discovery|Details|  
|------------------------|-------------|  
|Topology|This level discovers routers and subnets but does not identify a subnet mask for objects.|  
|Topology and client|In addition to topology, this level discovers potential clients like computers, and resources like printers and routers. This level of discovery tries to identify the subnet mask of objects that it finds.|  
|Topology, client, and client operating system|In addition to topology and potential clients, this level tries to discover the computer operating system name and version. This level uses Windows Browser and Windows Networking calls.|  

 With each incremental level, Network Discovery increases its activity and network bandwidth usage. Consider the network traffic that can be generated before you enable all aspects of Network Discovery.  

 For example, when you first use Network Discovery, you might start with only the topology level to identify your network infrastructure. Then, you can reconfigure Network Discovery to discover objects and their device operating systems. You can also configure settings that limit Network Discovery to a specific range of network segments. That way, you can discover objects in network locations that you require and avoid unnecessary network traffic, and you can discover objects from edge routers or from outside your network.  

###  <a name="BKMK_NetDiscOptions"></a> Network Discovery options  
To enable Network Discovery to search for IP-addressable devices, you must configure one or more of the following options that specify how to query for devices.  

> [!NOTE]  
>  Network Discovery runs in the context of the computer account of the site server that runs discovery. If the computer account does not have permissions to an untrusted domain, the domain and DHCP server configurations can fail to discover resources.  

**DHCP:**  

Specify each DHCP server that you want Network Discovery to query. (Network Discovery supports only DHCP servers that run the Microsoft implementation of DHCP.)  

-   Network Discovery retrieves information by using remote procedure calls to the database on the DHCP server.  

-   Network Discovery can query both 32-bit and 64-bit DHCP servers for a list of devices that are registered with each server.  

-   For Network Discovery to successfully query a DHCP server, the computer account of the server that runs discovery must be a member of the DHCP Users group on the DHCP server. For example, this level of access exists when one of the following is true:  

    -   The specified DHCP server is the DHCP server of the server that runs discovery.  

    -   The computer that runs discovery and the DHCP server are in the same domain.  

    -   A two-way trust exists between the computer that runs discovery and the DHCP server.  

    -   The site server is a member of the DHCP Users group.  

-   When Network Discovery enumerates a DHCP server, it does not always discover static IP addresses. Network Discovery does not find IP addresses that are part of an excluded range of IP addresses on the DHCP server. It also does not discover IP addresses that are reserved for manual assignment.  

**Domains:**  

Specify each domain that you want Network Discovery to query.  

-   The computer account of the site server that runs discovery must have permissions to read the domain controllers in each specified domain.  

-   To discover computers from the local domain, you must enable the Computer Browser service on at least one computer that is on the same subnet as the site server that runs Network Discovery.  

-   Network Discovery can discover any computer that you can view from your site server when you browse the network.  

-   Network Discovery retrieves the IP address and then uses an Internet Control Message Protocol echo request to ping each device that it finds. The **ping** command helps determine which computers are currently active.  

**SNMP Devices:**  

Specify each SNMP device that you want Network Discovery to query.  

-   Network Discovery retrieves the ipNetToMediaTable value from any SNMP device that responds to the query. This value returns arrays of IP addresses that are client computers or other resources like printers, routers, or other IP-addressable devices.  

-   To query a device, you must specify the IP address or NetBIOS name of the device.  

-   You must configure Network Discovery to use the community name of the device, or the device rejects the SNMP-based query.  

###  <a name="BKMK_LimitNetDisc"></a> Limiting Network Discovery  
When Network Discovery queries an SNMP device on the edge of you network, it can identify information about subnets and SNMP devices that are outside your immediate network. Use the following information to limit Network Discovery by configuring the SNMP devices that discovery can communicate with, and by specifying the network segments to query.  

**Subnets:**  

Configure the subnets that Network Discovery queries when it uses the SNMP and DHCP options. These two options search only the enabled subnets.  

For example, a DHCP request can return devices from locations across your whole network. If you want to discover only devices on a specific subnet, specify and enable that specific subnet on the **Subnets** tab in the **Network Discovery Properties** dialog box. When you specify and enable subnets, you limit future DHCP and SNMP discovery tasks to those subnets.  

> [!NOTE]  
>  Subnet configurations do not limit the objects that the **Domains** discovery option discovers.  

**SNMP community names:**  

To enable Network Discovery to successfully query a SNMP device, configure Network Discovery with the community name of the device. If Network Discovery is not configured by using the community name of the SNMP device, the device rejects the query.  

**Maximum hops:**  

When you configure the maximum number of router hops, you limit the number of network segments and routers that Network Discovery can query by using SNMP.  

The number of hops that you configure limits the number of additional devices and network segments that Network Discovery can query.  

For example, a topology-only discovery with **0** (zero) router hops discovers the subnet on which the originating server resides. It includes any routers on that subnet.  

The following diagram shows what a topology-only Network Discovery query finds when it runs on Server 1 with 0 router hops specified: subnet D and Router 1.  

 ![Image of discovery with zero router jump](media/Disc-0.gif)  

 The following diagram shows what a topology and client Network Discovery query finds when it runs on Server 1 with 0 router hops specified: subnet D and Router 1, and all potential clients on subnet D.  

 ![Image of discovery with one router jump](media/Disc-1.gif)  

 To get a better idea of how additional router hops can increase the amount of network resources that are discovered, consider the following network:  

 ![Image of discovery with two router jumps](media/Disc-2.gif)  

 Running a topology-only Network Discovery from Server 1 with one router hop discovers the following:  

-   Router 1 and subnet 10.1.10.0 (found with zero hops)  

-   Subnets 10.1.20.0 and 10.1.30.0, subnet A, and Router 2 (found on the first hop)  

> [!WARNING]  
>  Each increase to the number of router hops can significantly increase the number of discoverable resources and increase the network bandwidth that Network Discovery uses.  

##  <a name="bkmk_aboutServer"></a> Server Discovery  
**Configurable:** No  

In addition to the user-configurable discovery methods, Configuration Manager uses a process named **Server Discovery** (SMS_WINNT_SERVER_DISCOVERY_AGENT). This discovery method creates resource records for computers that are site systems, like a computer that is configured as a management point.  

##  <a name="bkmk_shared"></a> Common features of Active Directory Group Discovery, System Discovery, and User Discovery  
This section provides information about features that are common to the following discovery methods:  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

-   Active Directory User Discovery  

> [!NOTE]  
>  The information in this section does not apply to Active Directory Forest Discovery.  

These three discovery methods are similar in configuration and operation. They can discover computers, users, and information about group memberships of resources that are stored in Active Directory Domain Services. The discovery process is managed by a discovery agent that runs on the site server at each site where discovery is configured to run. You can configure each of these discovery methods to search one or more Active Directory locations as location instances in the local forest or remote forests.  

When discovery searches an untrusted forest for resources, the discovery agent must be able to resolve the following to be successful:  

-   To discover a computer resource by using Active Directory System Discovery, the discovery agent must be able to resolve the FQDN of the resource. If it cannot resolve the FQDN, it will then try to resolve the resource by its NetBIOS name.  

-   To discover a user or group resource by using Active Directory User Discovery or Active Directory Group Discovery, the discovery agent must be able to resolve the FQDN of the domain controller name that you specify for the Active Directory location.  

For each location that you specify, you can configure individual search options, like enabling a recursive search of the location's Active Directory child containers. You can also configure a unique account to use when it searches that location. This provides flexibility in configuring a discovery method at one site to search multiple Active Directory locations across multiple forests, without having to configure a single account that has permissions to all locations.  

When each of these three discovery methods runs at a specific site, the Configuration Manager site server at that site contacts the nearest domain controller in the specified Active Directory forest to locate Active Directory resources. The domain and forest can be in any supported Active Directory mode. The account that you assign to each location instance must have **Read** access permission to the specified Active Directory locations.

Discovery searches the specified locations for objects and then tries to collect information about those objects. A DDR is created when sufficient information about a resource can be identified. The required information varies depending on the discovery method that is being used.  

If you configure the same discovery method to run at different Configuration Manager sites to take advantage of querying local Active Directory servers, you can configure each site with a unique set of discovery options. Because discovery data is shared with each site in the hierarchy, avoid overlap between these configurations to efficiently discover each resource a single time.

For smaller environments, you might consider running each discovery method at only one site in your hierarchy to reduce administrative overhead and the potential for multiple discovery actions to rediscover the same resources. When you minimize the number of sites that run discovery, you can reduce the overall network bandwidth that discovery is using. You can also reduce the overall number of DDRs that are created and must be processed by your site servers.  

Many of the discovery method configurations are self-explanatory. Use the following sections for more information about the discovery options that might require additional information before you configure them.  

The following options are available for use with multiple Active Directory discovery methods:  

-   [Delta Discovery](#bkmk_delta)  

-   [Filter stale computer records by domain logon](#bkmk_stalelogon)  

-   [Filter stale records by computer password](#bkmk_stalepassword)  

-   [Search customized Active Directory attributes](#bkmk_customAD)  

###  <a name="bkmk_delta"></a> Delta Discovery  
Available for:  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

-   Active Directory User Discovery  

Delta Discovery is not an independent discovery method but an option available for the applicable discovery methods. Delta Discovery searches specific Active Directory attributes for changes that were made since the last full discovery cycle of the applicable discovery method. The attribute changes are submitted to the Configuration Manager database to update the discovery record of the resource.  

By default, Delta Discovery runs on a five-minute cycle. This is much more frequent than the typical schedule for a full discovery cycle.  This frequent cycle is possible because Delta Discovery uses fewer site server and network resources than a full discovery cycle does. When you use Delta Discovery, you can reduce the frequency of the full discovery cycle for that discovery method.  

The following are the most common changes that Delta Discovery detects:  

-   New computers or users added to Active Directory  

-   Changes to basic computer and user information  

-   New computers or users that are added to a group  

-   Computers or users that are removed from a group  

-   Changes to system group objects  

Although Delta Discovery can detect new resources and changes to group membership, it cannot detect when a resource has been deleted from Active Directory. DDRs created by Delta Discovery are processed similarly to the DDRs that are created by a full discovery cycle.  

You configure Delta Discovery on the **Polling Schedule** tab in the properties for each discovery method.  

###  <a name="bkmk_stalelogon"></a> Filter stale computer records by domain logon  
Available for:  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

You can configure discovery to exclude computers with a stale computer record based on the last domain logon of the computer. When this option is enabled, Active Directory System Discovery evaluates each computer that it identifies. Active Directory Group Discovery evaluates each computer that is a member of a group that is discovered.  

To use this option:  

-   Computers must be configured to update the **lastLogonTimeStamp** attribute in Active Directory Domain Services.  

-   The Active Directory domain functional level must be set to Windows Server 2003 or later.  

When you're configuring the time after the last logon that you want to use for this setting, consider the interval for replication between domain controllers.  

You configure filtering on the **Option** tab in the **Active Directory System Discovery Properties** and **Active Directory Group Discovery Properties** dialog boxes. Choose the option **Only discover computers that have logged on to a domain in a given period of time**.  

> [!WARNING]  
>  When you configure this filter and **Filter stale records by computer password**, computers that meet the criteria of either filter are excluded from discovery.  

###  <a name="bkmk_stalepassword"></a> Filter stale records by computer password  
Available for:  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

You can configure discovery to exclude computers with a stale computer record based on the last computer account password update by the computer. When this option is enabled, Active Directory System Discovery evaluates each computer that it identifies. Active Directory Group Discovery evaluates each computer that is a member of a group that is discovered.  

To use this option:  

-   Computers must be configured to update the **pwdLastSet** attribute in Active Directory Domain Services.  

When you're configuring this option, consider the interval for updates to this attribute in addition to the replication interval between domain controllers.  

You configure filtering on the **Option** tab in the **Active Directory System Discovery Properties** and **Active Directory Group Discovery Properties** dialog boxes. Choose the option **Only discover computers that have updated their computer account password in a given period of time**.  

> [!WARNING]  
>  When you configure this filter and **Filter stale records by domain logon**, computers that meet the criteria of either filter are excluded from discovery.  

###  <a name="bkmk_customAD"></a> Search customized Active Directory attributes  
 Available for:  

-   Active Directory System Discovery  

-   Active Directory User Discovery  

Each discovery method supports a unique list of Active Directory attributes that can be discovered.  

You can view and configure the list of customized attributes on the **Active Directory Attributes** tab in the **Active Directory System Discovery Properties** and **Active Directory User Discovery Properties** dialog boxes.  
