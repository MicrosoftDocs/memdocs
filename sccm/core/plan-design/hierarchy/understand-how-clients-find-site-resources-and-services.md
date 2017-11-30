---
title: "Find site resources"
titleSuffix: "Configuration Manager"
description: "Learn how and when System Center Configuration Manager clients use service location to find site resources."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Learn how clients find site resources and services for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager clients use a process called *service location* to locate site system servers that they can communicate with, and that  provide  services that clients are directed to use. Understanding how and when clients use service location to find site resources can help you configure your sites to successfully support client tasks. These configurations can require the site to interact with domain and network configurations like Active Directory Domain Services (AD DS) and DNS. Or they can require you to configure more complex alternatives.  

 Examples of site system roles that provide services include:

 - The core site system server for clients.
 - The management point.
 - Additional site system servers that the client can communicate with, like distribution points and software update points.  



##  <a name="bkmk_fund"></a> Fundamentals of service location  
 A client evaluates its current network location, communication protocol preference, and assigned site when it is using service location to find a management point that it can communicate with.  

 **A client communicates with a management point to:**  
-   Download information about other management points for the site, so it can build a list of known management points (known as the *MP list*) for future service location cycles.  
-   Upload configuration details, like inventory and status.  
-   Download a policy that sets configurations on the client and can inform the client of software that it can or must install, and other related tasks.  
-   Request information about additional site system roles that provide services that the client has been configured to use. Examples include distribution points for software that the client can install, or a software update point from which to get updates.  

**A Configuration Manager client makes a service location request:**  
-   Every 25 hours of continuous operation.  
-   When the client detects a change in its network configuration or location.  
-   When the **ccmexec.exe** service on the computer (the core client service) starts.  
-   When the client must locate a site system role that provides a required service.  

**When a client is attempting to find servers that host site system roles**, it uses service location to find a site system role that supports the client's protocol (HTTP or HTTPS). By default, clients use the most secure method available to them. Consider the following:  

-   To use HTTPS, you must have a public key infrastructure (PKI) and install PKI certificates on clients and servers. For information about how to use certificates, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   When you deploy a site system role that uses Internet Information Services (IIS) and supports communication from clients, you must specify whether clients connect to the site system by using HTTP or HTTPS. If you use HTTP, you must also consider signing and encryption choices. For more information, see  [Planning for Signing and Encryption](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in the [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="BKMK_Plan_Service_Location"></a> Service location and how clients determine their assigned management point  
When a client is first assigned to a primary site, it selects a default management point for that site. Primary sites support multiple management points, and each client independently identifies a management point as its default management point. This default management point then becomes that client's assigned management point. (You can also use client installation commands to set the assigned management point for a client when it's installed.)  

A client selects a management point to communicate with based on the client's  current network location and boundary group configurations. Even though it has an assigned management point, this might not be the management point that the client uses.  

    > [!NOTE]  
    >  A client always uses the assigned management point for registration messages and certain policy messages, even when other communications are sent to a proxy or local management point.  

You can use preferred management points. Preferred management points are management points from a client's assigned site that are associated with a boundary group that the client is using to find site system servers. A preferred management point's association with a boundary group as a site system server is similar to how distribution points or state migration points are associated with a boundary group. If you enable preferred management points for the hierarchy, when a client uses a management point from its assigned site, it will try to use a preferred management point before using other management points from its assigned site.  

You can also use the information in the [management point affinity](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx) blog on TechNet.com to configure management point affinity. Management point affinity overrides the default behavior for assigned management points and lets the client use one or more specific management points.  

Each time a client needs to contact a management point, it checks the MP list, which it stores locally in Windows Management Instrumentation (WMI). The client creates an initial MP list when it's installed. The client then periodically updates the list with details about each management point in the hierarchy.  

When the client cannot find a valid management point in its MP list, it searches the following service location sources, in order, until it finds a management point that it can use:  

1.  Management point  
2.  AD DS  
3.  DNS  
4.  WINS  

After a client successfully locates and contacts a management point, it downloads the current list of management points that are available in the hierarchy, and it updates the local MP list. This applies equally to clients that are domain joined and those that are not.  

For example, when a Configuration Manager client that is on the Internet connects to an Internet-based management point, the management point sends that client a list of available Internet-based management points in the site. Similarly, clients that are domain joined or in workgroups also receive the list of management points that they might use.  

A client that is not configured for the Internet is not provided Internet-facing-only management points. Workgroup clients configured for the Internet communicate only with Internet-facing management points.  

##  <a name="BKMK_MPList"></a> The MP list  
The MP list is the preferred service location source for a client, because it is a prioritized list of management points that the client previously identified. This list is sorted by each client based on its network location when the client updates the list, and then stored locally on the client in WMI.  

### Building the initial MP list  
During installation of the client, the following rules are used to build the client's initial MP list:  

-   The initial list includes management points specified during client installation (when you use the **SMSMP**= or **/MP** option).  
-   The client queries AD DS for published management points. To be identified from AD DS, the management point must be from the client's assigned site, and it must be of the same product version as the client.  
-   If no management point was specified during client installation, and the Active Directory schema is not extended, the client checks DNS and WINS for published management points.  
-   When the client builds the initial list, information about some management points in the hierarchy might not be known.  

### Organizing the MP list  
Clients organize their list of management points by using the following classifications:  

-   **Proxy**: A management point at a secondary site.  
-   **Local**: Any management point that is associated with the client's current network location, as defined by site boundaries. Note the following information about boundaries:
    -   When a client belongs to more than one boundary group, the list of local management points is determined from the union of all boundaries that include the current network location of the client.  
    -   Local management points are typically a subset of a client's assigned management points, unless the client is in a network location that is associated with another site with management points servicing its boundary groups.   


-   **Assigned**: Any management point that is a site system for the client's assigned site.  

You can use preferred management points. Management points at a site that are not associated with a boundary group, or that are not in a boundary group associated with a client's current network location, are not considered preferred. They will be used when the client cannot identify an available preferred management point.  

### Selecting a management point to use  
For typical communications, a client attempts to use a use a management point from the classifications in the following order, based on the client's network location:  

1.  Proxy  
2.  Local  
3.  Assigned  

However, the client always uses the assigned management point for registration messages and certain policy messages, even when other communications are sent to a proxy or local management point.  

Within each classification (proxy, local, or assigned), the client attempts to use a management point based on preferences, in the following order:  

1.  HTTPS capable in a trusted or local forest (when the client is configured for HTTPS communication)  
2.  HTTPS capable not in a trusted or local forest (when the client is configured for HTTPS communication)  
3.  HTTP capable in a trusted or local forest  
4.  HTTP capable not in a trusted or local forest  

From the set of management points sorted by preferences, the client attempts to use the first management point on the list. This sorted list of management points is random and cannot be ordered. The order of the list can change each time the client updates its MP list.  

When a client cannot establish contact with the first management point, it tries each successive management point on its list. It tries each preferred management point in the classification before trying the non-preferred management points. If a client cannot successfully communicate with any management point in the classification, it attempts to contact a preferred management point from the next classification, and so on, until it finds a management point to use.  

After a client establishes communication with a management point, it continues to use that same management point until:  

-   25 hours have passed.  
-   The client is unable to communicate with the management point for five attempts over a period of 10 minutes.

The client then randomly selects a new management point to use.  

##  <a name="bkmk_ad"></a> Active Directory  
Clients that are domain joined can use AD DS for service location. This requires sites to [publish data to Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

A client can use AD DS for service location when all the following conditions are true:  

-   The Active Directory [schema has been extended](https://technet.microsoft.com/library/mt345589.aspx) or was extended for System Center 2012 Configuration Manager.  
-   The [Active Directory forest is configured for publishing](http://technet.microsoft.com/library/hh696542.aspx), and Configuration Manager sites are configured to publish.  
-   The client computer is a member of an Active Directory domain and can access a global catalog server.  

If a client cannot find a management point to use for service location from AD DS, it attempts to use DNS.  

##  <a name="bkmk_dns"></a> DNS  
Clients on the intranet can use DNS for service location. This requires at least one site in a hierarchy to publish information about management points to DNS.  

Consider using DNS for service location when any of the following conditions are true:
-   The AD DS schema is not extended to support Configuration Manager.
-   Clients on the intranet are located in a forest that is not enabled for Configuration Manager publishing.  
-   You have clients on workgroup computers, and those clients are not configured for Internet-only client management. (A workgroup client configured for the Internet will communicate only with Internet-facing management points and will not use DNS for service location.)  
-   You can [configure clients to find management points from DNS](http://technet.microsoft.com/library/gg682055).  

When a site publishes service location records for management points to DNS:  

-   Publishing is applicable only to management points that accept client connections from the intranet.  
-   Publishing adds a service location resource record (SRV RR) in the DNS zone of the management point computer. There must be a corresponding host entry in DNS for that computer.  

By default, domain-joined clients search DNS for management point records from the client's local domain. You can configure a client property that specifies a domain suffix for a domain that has management point information published to DNS.  

For more information about how to configure the DNS suffix client property, see [How to configure client computers to find management points by using DNS publishing in System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

If a client cannot find a management point to use for service location from DNS, it attempts to use WINS.  

### Publish management points to DNS  
To publish management points to DNS, the following two conditions must be true:  

-   Your DNS servers support service location resource records, by using a version of BIND that is at least 8.1.2.  
-   The specified intranet FQDNs for the management points in Configuration Manager have host entries (for example, A records) in DNS.  

> [!IMPORTANT]  
>  Configuration Manager DNS publishing does not support a disjoint namespace. If you have a disjoint namespace, you can manually publish management points to DNS or use one of the other service location methods that are documented in this section.  

**When your DNS servers support automatic updates**, you can configure Configuration Manager to automatically publish management points on the intranet to DNS, or you can manually publish these records to DNS. When management points are published to DNS, their intranet FQDN and port number are published in the service location (SRV) record. You configure DNS publishing at a site in the site's Management Point Component Properties. For more information, see  [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**When your DNS zone is set to “Secure only” for dynamic updates**, only the first management point to publish to DNS can do so successfully with default permissions.

If only one management point can successfully publish and change its DNS record, and the management point server is healthy, clients can get the full MP list from that management point and then find their preferred management point.


**When your DNS servers do not support automatic updates but do support service location records**, you can manually publish management points to DNS. To accomplish this, you must manually specify the service location resource record (SRV RR) in DNS.  

Configuration Manager supports RFC 2782 for service location records. These records have the following format:   *_Service._Proto.Name TTL Class SRV Priority Weight Port Target*  

To publish a management point to Configuration Manager, specify the following values:  

-   **_Service**: Enter **_mssms_mp**_&lt;sitecode\>, where &lt;sitecode\> is the management point's site code.  
-   **._Proto**: Specify **._tcp**.  
-   **.Name**: Enter the DNS suffix of the management point, for example **contoso.com**.  
-   **TTL**: Enter **14400**, which is four hours.  
-   **Class**: Specify **IN** (in compliance with RFC 1035).  
-   **Priority**: Configuration Manager does not use this field.
-   **Weight**: Configuration Manager does not use this field.  
-   **Port**: Enter the port number that the management point uses, for example **80** for HTTP and **443** for HTTPS.  

    > [!NOTE]  
    >  The SRV record port should match the communication port that the management point uses. By default, this is **80** for HTTP communication and **443** for HTTPS communication.  

-   **Target**: Enter the intranet FQDN that is specified for the site system that is configured with the management point site role.  

If you use Windows Server DNS, you can use the following procedure to enter this DNS record for intranet management points. If you use a different implementation for DNS, use the information in this section about the field values and consult that DNS documentation to adapt this procedure.  

##### To configure automatic publishing:  

1.  In the Configuration Manager console, expand **Administration** > **Site Configuration** > **Sites**.  

2.  Select your site and then choose **Configure Site Components**.  

3.  Choose **Management Point**.  

4.  Select the management points that you want to publish. (This selection applies to publishing to AD DS and DNS.)  

5.  Check the box to publish to DNS. This box:  

    -   Lets you select which management points to publish to DNS.  

    -   Does not configure publishing to AD DS.  

##### To manually publish management points to DNS on Windows Server  

1.  In the Configuration Manager console, specify the intranet FQDNs of site systems.  

2.  In the DNS management console, select the DNS zone for the management point computer.  

3.  Verify that there is a host record (A or AAAA) for the intranet FQDN of the site system. If this record does not exist, create it.  

4.  By using the **New Other Records** option, choose **Service Location (SRV)** in the **Resource Record Type** dialog box, choose **Create Record**, enter the following information, and then choose **Done**:  

    -   **Domain**: If necessary, enter the DNS suffix of the management point, for example **contoso.com**.  
    -   **Service**: Type **_mssms_mp**_&lt;sitecode\>, where &lt;sitecode\> is the management point's site code.  
    -   **Protocol**: Type **_tcp**.  
    -   **Priority**: Configuration Manager does not use this field.  
    -   **Weight**: Configuration Manager does not use this field.  
    -   **Port**: Enter the port number that the management point uses, for example **80** for HTTP and **443** for HTTPS.  

        > [!NOTE]  
        >  The SRV record port should match the communication port that the management point uses. By default, this is **80** for HTTP communication and **443** for HTTPS communication.  

    -   **Host offering this service**: Enter the intranet FQDN that is specified for the site system that is configured with the management point site role.  

Repeat these steps for each management point on the intranet that you want to publish to DNS.  

##  <a name="bkmk_wins"></a> WINS  
When other service location mechanisms fail, clients can find an initial management point by checking WINS.  

By default, a primary site publishes to WINS the first management point at the site that is configured for HTTP and the first management point that is configured for HTTPS.  

If you do not want clients to find an HTTP management point in WINS, configure clients with the CCMSetup.exe Client.msi property **SMSDIRECTORYLOOKUP=NOWINS**.  
