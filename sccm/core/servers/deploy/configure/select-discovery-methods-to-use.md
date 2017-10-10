---
title: "Select discovery methods"
titleSuffix: "Configuration Manager"
description: "Review considerations for which methods to use and at which sites to run them."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brendunsms.author: brendunsmanager: angrobe
---
# Select discovery methods to use for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
To successfully and efficiently use discovery for System Center Configuration Manager, you must consider which methods to use and at which sites to run them.  

 Because discovery can generate a large volume of network traffic, and the resultant discovery data records (DDRs) can use significant CPU resources during processing, use only those discovery methods that you require to meet your goals. You might start by using only one or two discovery methods, and then later enable additional methods in a controlled manner to extend the level of discovery in your environment. The information in this topic can help you make informed decisions.  

 For information about the different discovery methods, see [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## Select methods to discover different things  
 To discover potential Configuration Manager client computers or user resources, you must enable the appropriate discovery methods. You can use different combinations of discovery methods to locate different resources, and to discover additional information about those resources. The discovery methods that you use determine the type of resources that are discovered, and which Configuration Manager services and agents are used in the discovery process. They also determine the type of information about resources that you can discover.  

### Discover computers   
When you want to discover computers, you can use **Active Directory System Discovery** or **Network Discovery**.  

 For example, if you want to discover resources that can install the Configuration Manager client before you use client push installation, you might run Active Directory System Discovery. Using this method, you not only discover the resource, but also discover basic information even extended information about it from Active Directory Domain Services. This information might be useful in building complex queries and collections to use for the assignment of client settings or content deployment.

Alternatively, you could run Network Discovery, and use its options to discover the operating system of resources (required to later use client push installation). Network Discovery provides you with information about your network topology that you are not able to acquire with other discovery methods. This method does not, however, provide you any information about your Active Directory environment.

 There is also a method called **Heartbeat Discovery**. It is possible to use only Heartbeat Discovery to force the discovery of clients that you installed by methods other than client push installation. However, unlike other discovery methods, Heartbeat Discovery cannot discover computers that do not have an active Configuration Manager client. It returns a limited set of information, intended to maintain an existing database record rather than be the basis of that record. Information submitted by Heartbeat Discovery might not be sufficient to build complex queries or collections.  

 If you use **Active Directory Group Discovery** to discover the membership of a specified group, you can discover limited system or computer information. This does not replace a full discovery of computers, but can provide basic information. This information is insufficient for client push installation.  

### Discover users   
When you want to discover information about users, use **Active Directory User Discovery**. Similar to Active Directory System Discovery, this method discovers users from Active Directory. It includes basic information, in addition to extended Active Directory information. You can use this information to build complex queries and collections similar to those for computers.  

### Discover group information   
When you want to discover information about groups and group memberships, use **Active Directory Group Discovery**. This discovery method creates resource records for security groups.  

 You can use this method to search a specific Active Directory group to identify the members of that group, in addition to any nested groups within that group. You can also use this method to search an Active Directory location for groups, and recursively search each child container of that location in Active Directory Domain Services.  

 This discovery method can also search the membership of distribution groups. This can identify the group relationships of both users and computers.  

 When you discover a group, you can also discover limited information about its members. This does not replace the Active Directory system or user discovery methods, though. It is usually insufficient to build complex queries and collections, or serve as the basis of a client push installation.  

### Discover infrastructure   
There are two methods you can use to discover network infrastructure, **Active Directory Forest Discovery** and **Network Discovery**.  

 Use Active Directory Forest Discovery to search an Active Directory forest for information about subnets and Active Directory site configurations. These configurations can then be automatically entered into Configuration Manager as boundary locations.  

 When you want to discover your network topology, use Network Discovery. While other discovery methods return information related to Active Directory Domain Services, and can identify the current network location of a client, they do not provide infrastructure information based on the subnets and router topology of your network.  

##  <a name="bkmk_shared"></a> Discovery data is shared among sites  
 After Configuration Manager adds discovery data to a database, it is quickly shared among all sites in the hierarchy. Because there is typically no benefit to discovering the same information at multiple sites in your hierarchy, consider setting up a single instance of each discovery method that you use to run at a single site. It's a good idea to do this instead of running multiple instances of a single method at different sites.  

 However, for some environments it might be useful to assign the same discovery method to run at multiple sites, each with a separate configuration and schedule. For example, when using Network Discovery, you might want to direct each site to discover its local network, instead of attempting to discover all network locations across a WAN.

If you do configure multiple instances of the same discovery methods to run at different sites, plan the configuration of each site carefully. You want to avoid having two or more sites discover the same resources from your network or Active Directory. This can consume additional network bandwidth and create duplicate DDRs.

The following table identifies at which sites you can set up the different discovery methods.  

|Discovery method|Supported locations|  
|----------------------|-------------------------|  
|Active Directory Forest Discovery|Central administration site<br /><br /> Primary site|  
|Active Directory Group Discovery|Primary site|  
|Active Directory System Discovery|Primary site|  
|Active Directory User Discovery|Primary site|  
|Heartbeat Discovery<sup>1</sup>|Primary site|  
|Network Discovery|Primary site<br /><br /> Secondary site|  

 <sup>1</sup> Secondary sites cannot configure Heartbeat Discovery, but can receive the Heartbeat DDR from a client.  

 When secondary sites run Network Discovery, or receive Heartbeat Discovery DDRs, they transfer the DDR by file-based replication to their parent primary site. This is because only primary sites and central administration sites can process DDRs. For more information about how DDRs are processed, see [About discovery data records](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## Considerations for different discovery methods  
 Because each site server and network environment is different, it's a good idea to limit your initial configurations for discovery. Then closely monitor each site server for its ability to process the discovery data that is generated.  

When you use an **Active Directory** discovery method for systems, users, or groups:  

-   Run discovery at a site that has a fast network connection to your domain controllers.  

-   Consider the Active Directory replication topology to ensure discovery can access the latest information.  

-   Consider the scope of the discovery configuration, and limit discovery to only those Active Directory locations and groups that you have to discover.  

If you use **Network Discovery**:  

-   Use a limited initial configuration to identify your network topography.  

-   After you identify your network topography, set up Network Discovery to run at specific sites that are central to the network areas that you want to more fully discover.  

Because **Heartbeat Discovery** does not run at a specific site, you do not have to consider it in general planning for where to run discovery.  

##  <a name="bkmk_best"></a> Best practices for discovery  
For best results with discovery, we recommend the following:

 - **Run Active Directory System Discovery and Active Directory User Discovery before you run Active Directory Group Discovery.**  

 When Active Directory Group Discovery identifies a previously undiscovered user or computer as a member of a group, it attempts to discover basic details for the user or computer. Because Active Directory Group Discovery is not optimized for this type of discovery, this process can cause it to run slowly. Additionally, Active Directory Group Discovery identifies only the basic details about the users and computers it discovers, and does not create a complete user or computer discovery record. When you run Active Directory System Discovery and Active Directory User Discovery, the additional Active Directory attributes for each object type are available. As a result, Active Directory Group Discovery runs more efficiently.  

- **When you set up Active Directory Group Discovery, only specify groups that you use with Configuration Manager.**  

 To help control the use of resources by Active Directory Group Discovery, specify only those groups that you use with Configuration Manager. This is because Active Directory Group Discovery recursively searches each group it discovers for users, computers, and nested groups. The search of each nested group can expand the scope of Active Directory Group Discovery, and reduce performance. Additionally, when you set up delta discovery for Active Directory Group Discovery, the discovery method monitors each group for changes. This further reduces performance when the method must search unnecessary groups.  

- **Set up discovery methods with a longer interval between full discovery, and a more frequent period of delta discovery.**  

 Because delta discovery uses fewer resources than a full discovery cycle, and can identify new or modified resources in Active Directory, you can reduce the frequency of full discovery cycles to run weekly (or less). Delta discovery for Active Directory System Discovery, Active Directory User Discovery and Active Directory Group Discovery identifies almost all the changes of Active Directory objects, and can maintain accurate discovery data for resources.  

- **Run Active Directory discovery methods at a primary site that has a network location that is closest to your Active Directory domain controller.**  

 To improve the performance of Active Directory discovery, it's a good idea to run discover at a primary site that has a fast network connection to your domain controllers. If you run the same Active Directory discovery method at multiple sites, set up each discovery method to avoid overlap. Unlike past versions of Configuration Manager, discovery data is shared among sites. Therefore, it is not necessary to discover the same information at multiple sites. For more information, see [Discovery data is shared between sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Run Active Directory Forest Discovery at only one site when you plan to automatically create boundaries from the discovery data.**  

 If you run Active Directory Forest Discovery at more than one site in a hierarchy, it's a good idea to only enable options to automatically create boundaries at a single site. This is because when Active Directory Forest Discovery runs at each site and creates boundaries, Configuration Manager cannot merge those boundaries into a single boundary object. When you configure Active Directory Forest Discovery to automatically create boundaries at multiple sites, the result can be duplicated boundary objects in the Configuration Manager console.  
