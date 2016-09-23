---
title: "Understand how clients find site resources and services for System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: Brenduns

---
# Understand how clients find site resources and services for System Center Configuration Manager
System Center Configuration Manager clients us a process called **service location** to locate site system servers that they can communicate with, and that  provide  services that clients are directed to use.   Understanding how and when clients use service location to find site resources can help you configure your sites to successfully support client operations.   These configurations can require the site to interact with domain and network configurations like Active Directory Domain Services (AD DS) and DNS, or for you to configure more complex alternatives.  

 Examples of site system roles that provide services include the core site system server for clients, the management point, and additional site system servers the client can communicate with, like distribution points and software update points.  

 This topic is divided into the following sections:  

-   [Fundamentals of service location](#bkmk_fund)  

-   [Service Location and how clients determine their assigned management point](#BKMK_Plan_Service_Location)  

-   [The MP list](#BKMK_MPList)  

-   [Active Directory](#bkmk_ad)  

-   [DNS](#bkmk_dns)  

-   [WINS](#bkmk_wins)  

##  <a name="bkmk_fund"></a> Fundamentals of service location  
 A client evaluates its current network location, communication protocol preference,  and assigned site, when using service location to find a management point they can communicate with.  

 **A client communicates  with a management point to:**  

-   Download information about other management points for the site, so they can build a MP List for future service location cycles  

-   Upload configuration details, like inventory and status  

-   Download policy that sets configurations on the client and can inform the client of software it can or must install, and other related tasks.  

-   Request information about additional sites system roles that provide services the client has been configured to use, like distribution points for software it can install, or a software update point from which to obtain updates.  

**A  Configuration Manager client makes a service location request:**  

-   Every 25 hours of continuous operation  

-   When the client detects a change of its network configuration or location  

-   When the **ccmexec.exe** service on the computer (the core client service) starts  

-   When the client must locate a site system role that provides a required service  

**When attempting to find servers that host site system roles**, the client uses service location to find a site system role that supports the client's protocol (HTTP or HTTPS). By default, clients use the most secure method available to them:  

-   To use HTTPS, you must have a public key infrastructure (PKI) and install PKI certificates on clients and servers. For information about how to use certificates, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   When you deploy a site system role that uses Internet Information Services (IIS) and supports communication from clients, you must specify whether clients connect to the site system by using HTTP or HTTPS. If you use HTTP, you must also consider signing and encryption choices. For more information, see  [Planning for Signing and Encryption](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in the [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md) topic.  

##  <a name="BKMK_Plan_Service_Location"></a> Service Location and how clients determine their assigned management point  
When a client first assigns to a primary site, it selects a default management point for that site. (Primary sites support multiple management points, and each client independently identifies a management point as its default management point.)  This default management point then becomes that clients assigned management point. (You can also use client installation commands to set the assigned management point for a client at the time it installs.)  

-   Clients select a  management point to communicate with based on the clients  current network location and boundary group configurations. Even though it has an assigned management point, this might not be the management point the client uses.  

    > [!NOTE]  
    >  A client always uses the assigned management point for registration messages and certain policy messages, even when other communications are sent to a proxy or local management point.  

  -   You can use preferred management points. A preferred management point is a management point that is associated to a boundary group as site system server, similar to how distribution points or state migration points are associated with a boundary group. If you enable preferred management points for the hierarchy, when a client uses a management point from its assigned site, it will try to use a preferred management point before using other management points from its assigned site.  

-   You can also use the information in the following blog on TechNet.com to configure management point affinity. Management point affinity overrides the default behavior for assigned management points and enables the client to use one or more specific management points: [management point affinity](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx)  

Each time a client needs to contact a management point it checks a list of known management points (known as the **MP list**) which it stores locally in WMI. The client creates an initial MP list when it installs, and then periodically updates the list with details about each management point in the hierarchy.  

When the client cannot find a valid management point on its MP list, it then searches the following service location sources, in order, until it finds a management point it can use:  

1.  Management point  

2.  Active Directory Domain Services  

3.  DNS  

4.  WINS  

After a client successfully locates and contacts a management point from one of these sources, it downloads the current list of management points that are available in the hierarchy, and updates its local MP list. This applies equally to clients that are domain joined and those that are not.  

For example, when a Configuration Manager client that is on the Internet connects to an Internet-based management point, the management point sends that client a list of available Internet-based management points in the site. Similarly, clients that are domain joined or in workgroups also receive the list of management points that they might use.  

-   A client that is not configured for the Internet would not be provided Internet-only facing management points.  

-   Workgroup clients configured for the Internet only communicate with Internet facing management points.  

##  <a name="BKMK_MPList"></a> The MP list  
The MP list is the preferred source for service location source for a client, as it is a prioritized list of management points that the client previously identified. This list is sorted by each client based on its network location when the client updates the list, and then stored locally on the client in WMI.  

### Building the Initial MP list  
During installation of the client, the following rules are used to build the clients initial **MP list**:  

-   The initial list includes management points specified during client installation (when you use the **SMSMP**= or the **/MP** options).  

-   The client queries Active Directory Domain Services (AD DS) for published management points. In order to be identified from AD DS, the management point must be from the client's assigned site, and be of the same product version as the client.  

-   If no management point was specified during client installation, and when the Active Directory schema is not extended, the client checks DNS and WINS for published management points.  

-   When building the initial list, information about some management points in the hierarchy might not be known.  

### Organizing the management point list  
Clients organize their list of management points using the following classifications:  

-   **Proxy**: A proxy management point is a management point at a secondary site.  

-   **Local**: Any management point that is associated with the client's current network location as defined by site boundaries.  

    -   When a client belongs to more than one boundary group, the list of local management points is determined from the union of all boundaries that include the current network location of the client.  

    -   Typically, **Local** management points are a subset of a clients **Assigned** management points unless the client is on a network location associated with another site with management points servicing its boundary groups.  

-   **Assigned**: Any management point that is a site system for the client's assigned site.  

     You can use preferred management points. Preferred management points are management points from a client's assigned site that are associated to a boundary group that the client is using to find site system servers.  

     Management points at a site that are not associated with a boundary group, or that are not in a boundary group associated with a client's current network location, are not considered preferred, and will be used when the client cannot identify an available preferred management point.  

### Selecting a management point to use  
For typical communications, a client attempts to use a use a management point from the classifications in the following order, based on the client's network location:  

1.  Proxy  

2.  Local  

3.  Assigned  

However, the client always uses the assigned management point for registration messages and certain policy messages, even when other communications are sent to a proxy or local management point.  

Within each classification (proxy, local, or assigned), clients attempt to use a management point based on preferences, in the following order:  

1.  HTTPS capable in a trusted or local forest (when the client is configured for HTTPS communication)  

2.  HTTPS capable not in trusted or local forest (when the client is configured for HTTPS communication)  

3.  HTTP capable in trusted or local forest  

4.  HTTP capable not in trusted or local forest  

From the set of management points sorted by preferences, clients attempt to use the first management point on the list:  

-   This sorted list of management points is random, and cannot be ordered.  

-   The order of the list can change each time the client updates its management point list.  

When a client cannot establish contact with the first management point, it tries each successive management point on its list, trying each preferred management point in the classification before trying the non-preferred management points. If a client cannot successfully communicate with any management point in the classification, it will then attempt to contact a preferred management point from the next classification, and so on until the client finds a management point to use.  

After establishing communication with a management point, clients continue to use that same management point until:  

-   After 25 hours the client randomly selects a new management point to use.  

-   The client is unable to communicate with the management point for 5 attempts over a period of 10 minutes, at which time the client selects a new management point to use.  

##  <a name="bkmk_ad"></a> Active Directory  
Clients that are domain joined can use Active Directory Domain Services (AD DS) for service location. This requires sites to [publish data to Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

Clients can use Active Directory Domain Services for service location when all the following conditions are true:  

-   The Active Directory [schema is has been extended](https://technet.microsoft.com/library/mt345589.aspx) or was extended for System Center 2012 Configuration Manager.  

-   The [Active Directory forest is configured for publishing](http://technet.microsoft.com/library/hh696542.aspx), and Configuration Manager sites are configured to publish.  

-   The client computer is a member of an Active Directory domain and can access a global catalog server.  

If a client cannot find a management point to use for service location from AD DS, it then attempts to use DNS. Clients that are domain joined can use AD DS for service location. This requires sites to [publish data to Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

##  <a name="bkmk_dns"></a> DNS  
Clients on the intranet can use DNS for service location. This requires at least one site in a hierarchy to publish information about management points to DNS.  

Consider using DNS for service location when any of the following conditions are true:  

-   The Active Directory Domain Services schema is not extended to support Configuration Manager.  

-   Clients on the intranet are located in a forest that is not enabled for Configuration Manager publishing.  

-   You have clients on workgroup computers, and those clients are not configured for Internet-only client management. (A workgroup client configured for the Internet will only communicate with Internet facing management points and will not use DNS for service location.)  

-   You can [configure clients to find management points from DNS](http://technet.microsoft.com/library/gg682055).  

When a site publishes service location records for management points to DNS:  

-   Publishing is applicable only to management points that accept client connections from the intranet.  

-   Publishing adds a service location resource record (SRV RR) in the DNS zone of the management point computer. There must be a corresponding host entry in DNS for that computer.  

By default, domain joined clients search DNS for management point records from the client's local domain. You can configure a client property that specifies a domain suffix for a domain that does have management point information published to DNS.  

For more information about how to configure the DNS suffix client property, see [How to configure client computers to find management points by using DNS publishing in System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

If a client cannot find a management point to use for service location from DNS, it then attempts to use WINS.  

### Publish management points to DNS  
To publish management points to DNS, the following two conditions must be true:  

-   Your DNS servers support service location resource records, by using a version of BIND that is at least 8.1.2.  

-   The specified intranet FQDNs for the management points in Configuration Manager have host entries (for example, A records) in DNS.  

> [!IMPORTANT]  
>  Configuration Manager DNS publishing does not support a disjoint namespace. If you have a disjoint namespace, you can manually publish management points to DNS or use one of the other alternative service location methods that are documented in this section.  

**When your DNS servers support automatic updates**, you can configure Configuration Manager to automatically publish management points on the intranet to DNS, or you can manually publish these records to DNS. When management points are published to DNS, their intranet FQDN and port number are published in the service location (SRV) record. You configure DNS publishing at a site in the sites Management Point Component Properties. For more information, see  [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**When your DNS servers do not support automatic updates but do support service location records**, you can manually publish management points to DNS. To accomplish this, you must manually specify the service location resource record (SRV RR) in DNS.  

Configuration Manager supports RFC 2782 for service location records, which have the following format:  

*_Service._Proto.Name TTL Class SRV Priority Weight Port Target*  

To publish a management point to Configuration Manager, specify the following values:  

-   **_Service**: Enter **_mssms_mp***_&lt;sitecode\>*, where *&lt;sitecode\>* is the management point's site code.  

-   **._Proto**: Specify **._tcp**.  

-   **.Name**: Enter the DNS suffix of the management point, for example **contoso.com**.  

-   **TTL**: Enter **14400**, which is four hours.  

-   **Class**: Specify **IN** (in compliance with RFC 1035).  

-   **Priority**: This field is not used by Configuration Manager.  

-   **Weight**: This field is not used by Configuration Manager.  

-   **Port**: Enter the port number that the management point uses, for example **80** for HTTP and **443** for HTTPS.  

    > [!NOTE]  
    >  The SRV record port should match the communication port used by the management point. By default, this is **80** for HTTP communication, and **443** for HTTPS communications.  

-   **Target**: Enter the intranet FQDN that is specified for the site system that is configured with the management point site role.  

If you use Windows Server DNS, you can use the following procedure to enter this DNS record for intranet management points. If you use a different implementation for DNS, use the information in this section about the field values and consult that DNS documentation to adapt this procedure.  

##### To configure automatic publishing:  

1.  In the Configuration Manager console, expand **Administration** > **Site Configuration** > **Sites**.  

2.  Select your site and then click **Configure Site Components**.  

3.  Select **Management Point**.  

4.  Select the management points you want to publish. (This selection applies to publishing to AD DS, and DNS).  

5.  Select the checkbox to publish to DNS:  

    -   This dialog allows you to select which management points to publish, and to publish to DNS.  

    -   This dialog does not configure publishing to AD DS.  

##### To manually publish management points to DNS on Windows Server  

1.  In the Configuration Manager console, specify the intranet FQDNs of site systems.  

2.  In the DNS management console, select the DNS zone for the management point computer.  

3.  Verify that there is a host record (A or AAAA) for the intranet FQDN of the site system. If this record does not exist, create it.  

4.  By using the **New Other Records** option, click **Service Location (SRV)** in the **Resource Record Type** dialog box, click **Create Record**, enter the following information, and then click **Done**:  

    -   **Domain**: If necessary, enter the DNS suffix of the management point, for example **contoso.com**.  

    -   **Service**: Type **_mssms_mp***_&lt;sitecode\>*, where *&lt;sitecode\>* is the management point's site code.  

    -   **Protocol**: Type **_tcp**.  

    -   **Priority**: This field is not used by Configuration Manager.  

    -   **Weight**: This field is not used by Configuration Manager.  

    -   **Port**: Enter the port number that the management point uses, for example **80** for HTTP and **443** for HTTPS.  

        > [!NOTE]  
        >  The SRV record port should match the communication port used by the management point. By default, this is **80** for HTTP communication, and **443** for HTTPS communications.  

    -   **Host offering this service**: Enter the intranet fully qualified domain name that is specified for the site system that is configured with the management point site role.  

Repeat these steps for each management point on the intranet that you want to publish to DNS.  

##  <a name="bkmk_wins"></a> WINS  
When other service location mechanisms fail, clients can find an initial management point by checking WINS.  

By default, a primary site publishes to WINS the first management point at the site that is configured for HTTP and the first management point configured for HTTPS.  

If you do not want clients to find an HTTP management point in WINS, configure clients with the CCMSetup.exe Client.msi property **SMSDIRECTORYLOOKUP=NOWINS**.  

