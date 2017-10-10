---
title: "Communications between endpoints"
titleSuffix: "Configuration Manager"
description: "Learn about how System Center Configuration Manager site systems and components communicate across a network."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
caps.latest.revision: 10
author: Brendunsms.author: brendunsmanager: angrobe

---
# Communications between endpoints in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

##  <a name="Planning_Intra-site_Com"></a> Communications between site systems in a site  
 When Configuration Manager site systems or components communicate across the network to other site systems or Configuration Manager components in the site, they use one of the following protocols, depending on how you configure the site:  

-   Server message block (SMB)  

-   HTTP  

-   HTTPS  

With the exception of communication from the site server to a distribution point,  server-to-server communications in a site can occur at any time and do not use mechanisms to control the network bandwidth. Because you cannot control the communication between site systems, ensure that you install site system servers in locations that have fast and well-connected networks.  

To help you manage the transfer of content from the site server to distribution points:  

-   Configure the distribution point for network bandwidth control and scheduling. These controls resemble the configurations that are used by intersite addresses, and you can often use this configuration instead of installing another Configuration Manager site when the transfer of content to remote network locations is your main bandwidth consideration.  

-   You can install a distribution point as a prestaged distribution point. A prestaged distribution point lets you use content that is manually put on the distribution point server and removes the requirement to transfer content files across the network.  

For more information, see [Manage network bandwidth for content management](manage-network-bandwidth.md).


##  <a name="Planning_Client_to_Site_System"></a> Communications from clients to site systems and services  
Clients initiate communication to site system roles, Active Directory Domain Services, and online services. To enable these communications, firewalls must allow the network traffic between clients and the endpoint of their communications. Endpoints include:  

-   **Application Catalog website point**: Supports HTTP and HTTPS communication

-   **Cloud-based resources**: Includes Microsoft Azure and Microsoft Intune  

-   **Configuration Manager Policy Module (NDES)**: Supports HTTP and HTTPS communication

-   **Distribution points**: Supports HTTP and HTTPS communication, and HTTPS is required by cloud-based distribution points  

-   **Fallback status point**: Supports HTTP communication  

-   **Management point**: Supports HTTP and HTTPS communication  

-   **Microsoft Update**  

-   **Software update points** : Supports HTTP and HTTPS communication  

-   **State Migration point**: Supports HTTP and HTTPS communication  

-   **Various domain services**  

Before a client can communicate with a site system role, the client uses service location to find a site system role that supports the client's protocol (HTTP or HTTPS). By default, clients use the most secure method that's available to them:  

-   To use HTTPS, you must have a public key infrastructure (PKI) and install PKI certificates on clients and servers. For information about how to use certificates, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   When you deploy a site system role that uses Internet Information Services (IIS) and supports communication from clients, you must specify whether clients connect to the site system by using HTTP or HTTPS. If you use HTTP, you must also consider signing and encryption choices. For more information, see [Planning for signing and encryption](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

For information about service location by clients, see  [Understand how clients find site resources and services for System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

For details about ports and protocols used by clients when they communicate to these endpoints, see [Ports used in System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Considerations for client communications from the Internet or an untrusted forest  
The following site system roles installed at primary sites support connections from clients that are in untrusted locations, such as the Internet or an untrusted forest. (Secondary sites do not support client connections from untrusted locations):  

-   Application Catalog website point  

-   Configuration Manager Policy Module  

-   Distribution point (HTTPS is required by cloud-based distribution points)  

-   Enrollment proxy point  

-   Fallback status point  

-   Management point  

-   Software update point  

**About Internet-facing site systems:**   
There is no requirement to have a trust between a client's forest and that of the site system server. However, when the forest that contains an Internet-facing site system trusts the forest that contains the user accounts, this configuration supports user-based policies for devices on the Internet when you enable the **Client Policy** client setting **Enable user policy requests from Internet clients**.  

For example, the following configurations illustrate when Internet-based client management supports user policies for devices on the Internet:  

-   The Internet-based management point is in the perimeter network where a read-only domain controller resides to authenticate the user and an intervening firewall allows Active Directory packets.  

-   The user account is in Forest A (the intranet) and the Internet-based management point is in Forest B (the perimeter network). Forest B trusts Forest A, and an intervening firewall allows the authentication packets.  

-   The user account and the Internet-based management point are in Forest A (the intranet). The management point is published to the Internet by using a web proxy server (like Forefront Threat Management Gateway).  

> [!NOTE]  
>  If Kerberos authentication fails, NTLM authentication is then automatically tried.  

As the previous example shows, you can place Internet-based site systems in the intranet when they are published to the Internet by using a web proxy server, such as ISA Server and Forefront Threat Management Gateway. These site systems can be configured for client connection from the Internet only, or for client connections from the Internet and intranet. When you use a web proxy server, you can configure it for Secure Sockets Layer (SSL) bridging to SSL (more secure) or SSL tunneling as follows:  

-   **SSL bridging to SSL:**   
    The recommended configuration when you use proxy web servers for Internet-based client management is SSL bridging to SSL, which uses SSL termination with authentication. Client computers must be authenticated by using computer authentication, and mobile device legacy clients are authenticated by using user authentication. Mobile devices that are enrolled by Configuration Manager do not support SSL bridging.  

     The benefit of SSL termination at the proxy web server is that packets from the Internet are subject to inspection before they are forwarded to the internal network. The proxy web server authenticates the connection from the client, terminates it, and then opens a new authenticated connection to the Internet-based site systems. When Configuration Manager clients use a proxy web server, the client identity (client GUID) is securely contained in the packet payload so that the management point does not consider the proxy web server to be the client. Bridging is not supported in Configuration Manager with HTTP to HTTPS, or from HTTPS to HTTP.  

-   **Tunneling**:   
    If your proxy web server cannot support the requirements for SSL bridging, or you want to configure Internet support for mobile devices that are enrolled by Configuration Manager, SSL tunneling is also supported. It is a less secure option because the SSL packets from the Internet are forwarded to the site systems without SSL termination, so they cannot be inspected for malicious content. When you use SSL tunneling, there are no certificate requirements for the proxy web server.  

##  <a name="Plan_Com_X-Forest"></a> Communications across Active Directory forests  
System Center Configuration Manager supports sites and hierarchies that span Active Directory forests.  

Configuration Manager also supports domain computers that are not in the same Active Directory forest as the site server, and computers that are in workgroups:  

-   **To support domain computers in a forest that is not trusted by your site server's forest**, you can:  

    -   Install site system roles in that untrusted forest, with the option to publish site information to that Active Directory forest  

    -   Manage these computers as if they were workgroup computers.  

  When you install site system servers in an untrusted Active Directory forest, the client-to-server communication from clients in that forest is kept within that forest, and Configuration Manager can authenticate the computer by using Kerberos. When you publish site information to the client's forest, clients benefit from retrieving site information, such as a list of available management points, from their Active Directory forest, rather than downloading this information from their assigned management point.  

  > [!NOTE]  
  >  If you want to manage devices that are on the Internet, you can install Internet-based site system roles in your perimeter network when the site system servers are in an Active Directory forest. This scenario does not require two-way trust between the perimeter network and the site server's forest.  

-   **To support computers in a workgroup**, you must:  

    -   Manually approve workgroup computers when they use HTTP client connections to site system roles. This is because Configuration Manager cannot authenticate these computers by using Kerberos.  

    -   Configure workgroup clients to use the Network Access Account so that these computers can retrieve content from distribution points.  

    -   Provide an alternative mechanism for workgroup clients to find management points. You can use DNS publishing, WINS, or you can directly assign a management point. This is because these clients cannot retrieve site information from Active Directory Domain Services.  

    Related resources in this content library:  

    -   [Manage conflicting records for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Network access account](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [How to Install Configuration Manager Clients on Workgroup Computers](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Scenarios to support a site or hierarchy that spans multiple domains and forests  

#### Communication between sites in a hierarchy that spans forests  
This scenario requires a two-way forest trust that supports Kerberos authentication.  If you do not have a two-way forest trust that supports Kerberos authentication, then Configuration Manager does not support a child site in the remote forest.  

 **Configuration Manager supports installing a child site in a remote forest that has the required two-way trust with the forest of the parent site**  

-   For example, you can place a secondary site in a different forest from its primary parent site as long as the required trust exists.  

> [!NOTE]  
>  A child site can be primary site (where the central administration site is the parent site) or a secondary site.  

Intersite communication in Configuration Manager uses database replication and file-based transfers. When you install a site, you must specify an account with which to install the site on the designated server. This account also establishes and maintains communication between sites.  

After the site successfully installs and initiates file-based transfers and database replication, you do not have to configure anything else for communication to the site.  

**When a two-way forest trust exists, Configuration Manager does not require any additional configuration steps.**  

By default, when you install a new site as a child of another site, Configuration Manager configures the following:  

-   An intersite file-based replication route at each site that uses the site server computer account. Configuration Manager adds the computer account of each computer to the **SMS_SiteToSiteConnection_&lt;sitecode\>** group on the destination computer.  

-   Database replication between the SQL Server at each site.  

The following configurations must also be set:  

-   Intervening firewalls and network devices must allow the network packets that Configuration Manager requires.  

-   Name resolution must work between the forests.  

-   To install a site or site system role, you must specify an account that has local administrator permissions on the specified computer.  

#### Communication in a site that spans forests  
This scenario does not require a two-way forest trust.  

**Primary sites support the installation of site system roles on computers in remote forests**.  

-   The Application Catalog web service point is the only exception.  It  is only supported  in the same forest as the site server.  

-   When a site system role accepts connections from the Internet, as a security best practice, install the site system roles in a location where the forest boundary provides protection for the site server (for example, in a perimeter network).  

**To install a site system role on a computer in an untrusted forest:**  

-   You must specify a **Site System Installation Account**, which is used to install the site system role. (This account must have local administrative credentials to connect to.) Then install site system roles on the specified computer.  

-   You must select the site system option **Require the site server to initiate connections to this site system**. This requires the site server to establish connections to the site system server to transfer data. This prevents the computer in the untrusted location from initiating contact with the site server that's inside your trusted network. These connections use the **Site System Installation Account**.  

**To use a site system role that was installed in an untrusted forest,** firewalls must allow the network traffic even when the site server initiates the transfer of data.  

Additionally, the following site system roles require direct access to the site database. Therefore, firewalls must allow applicable traffic from the untrusted forest to the site's SQL Server:  

-   Asset Intelligence synchronization point  

-   Endpoint Protection point  

-   Enrollment point  

-   Management point  

-   Reporting service point  

-   State migration point  

For more information, see [Ports used in System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

**You might need to  configure site system role access to the site database:**  

Both the management point and enrollment point site system roles connect to the site database.  

-   By default, when these site system roles are installed, Configuration Manager configures the computer account of the new site system server as the connection account for the site system role, and then adds the account to the appropriate SQL Server database role.  

-   When you install these site system roles in an untrusted domain, you must configure the site system role connection account to enable the site system role to obtain information from the database.  

If you configure a domain user account to be the  connection account for these site system roles, ensure that the domain user account  has appropriate access to the SQL Server database at that site:  

-   Management point: **Management Point Database Connection Account**  

-   Enrollment point: **Enrollment Point Connection Account**  

Consider the following additional information when you plan for site system roles in other forests:  

-   If you run Windows Firewall, configure the applicable firewall profiles to pass communications between the site database server and computers that are installed with remote site system roles. For information about firewall profiles, see [Understanding firewall profiles](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   When the Internet-based management point trusts the forest that contains the user accounts, user policies are supported. When no trust exists, only computer policies are supported.  

#### Communication between clients and site system roles when the clients are not in the same Active Directory forest as their site server  
Configuration Manager supports the following scenarios for clients that are not in the same forest as their site's site server:  

-   There is a two-way forest trust between the forest of the client and the forest of the site server.  

-   The site system role server is located in the same forest as the client.  

-   The client is on a domain computer that does not have a two-way forest trust with the site server, and site system roles are not installed in the client's forest.  

-   The client is on a workgroup computer.  

Clients on a domain-joined computer can use Active Directory Domain Services for service location when their site is published to their Active Directory forest.  

To publish site information to another Active Directory forest, you must:  

-   Specify the forest and then enable publishing to that forest in the **Active Directory Forests** node of the **Administration** workspace.  

-   Configure each site to publish its data to Active Directory Domain Services. This configuration enables clients in that forest to retrieve site information and find management points. For clients that cannot use Active Directory Domain Services for service location, you can use DNS, WINS, or the client's assigned management point.  

###  <a name="bkmk_xchange"></a> Put the Exchange Server connector in a remote forest  
To support this scenario, ensure that name resolution works between the forests (for example, configure DNS forwards), and when you configure the Exchange Server connector, specify the intranet FQDN of the Exchange Server. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  
