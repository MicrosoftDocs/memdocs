---
title: Communications between endpoints
titleSuffix: Configuration Manager
description: Learn how Configuration Manager site systems and components communicate across a network.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Communications between endpoints in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


##  <a name="Planning_Intra-site_Com"></a> Communications between site systems in a site  

 When Configuration Manager site systems or components communicate across the network to other site systems or components in the site, they use one of the following protocols, depending on how you configure the site:  

-   Server message block (SMB)  

-   HTTP  

-   HTTPS  

With the exception of communication from the site server to a distribution point, server-to-server communications in a site can occur at any time. These communications don't use mechanisms to control the network bandwidth. Because you can't control the communication between site systems, make sure that you install site system servers in locations that have fast and well-connected networks.  


### Site server to distribution point 

To help you manage the transfer of content from the site server to distribution points, use the following strategies:  

-   Configure the distribution point for network bandwidth control and scheduling. These controls resemble the configurations that are used by intersite addresses. Use this configuration instead of installing another Configuration Manager site when the transfer of content to remote network locations is your main bandwidth consideration.  

-   You can install a distribution point as a prestaged distribution point. A prestaged distribution point lets you use content that is manually put on the distribution point server and removes the requirement to transfer content files across the network.  

For more information, see [Manage network bandwidth for content management](manage-network-bandwidth.md).



##  <a name="Planning_Client_to_Site_System"></a> Communications from clients to site systems and services  

Clients initiate communication to site system roles, Active Directory Domain Services, and online services. To enable these communications, firewalls must allow the network traffic between clients and the endpoint of their communications. For more information about ports and protocols used by clients when they communicate to these endpoints, see [Ports used in Configuration Manager](/sccm/core/plan-design/hierarchy/ports).  

Before a client can communicate with a site system role, the client uses service location to find a role that supports the client's protocol (HTTP or HTTPS). By default, clients use the most secure method that's available to them. For more information, see  [Understand how clients find site resources and services](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  

To use HTTPS, configure one of the following options:  

- Use a public key infrastructure (PKI) and install PKI certificates on clients and servers. For information about how to use certificates, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  

- Starting in version 1806, configure the site to **Use Configuration Manager-generated certificates for HTTP site systems**. For more information, see [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).  

When you deploy a site system role that uses Internet Information Services (IIS) and supports communication from clients, you must specify whether clients connect to the site system by using HTTP or HTTPS. If you use HTTP, you must also consider signing and encryption choices. For more information, see [Planning for signing and encryption](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForSigningEncryption).  


###  <a name="BKMK_clientspan"></a> Considerations for client communications from the internet or an untrusted forest  

The following site system roles installed at primary sites support connections from clients that are in untrusted locations, such as the internet or an untrusted forest. (Secondary sites don't support client connections from untrusted locations.) 

-   Application catalog website point  

-   Configuration Manager policy module (NDES) 

-   Distribution point   

-   Cloud-based distribution point (requires HTTPS)

-   Enrollment proxy point  

-   Fallback status point  

-   Management point  

-   Software update point  

-   Cloud management gateway (requires HTTPS)


#### About internet-facing site systems

> [!Note]  
> The following section is about internet-based client management scenarios. It doesn't apply to cloud management gateway scenarios. For more information, see [Manage clients on the internet](/sccm/core/clients/manage/manage-clients-internet).  

There's no requirement to have a trust between a client's forest and that of the site system server. However, when the forest that contains an internet-facing site system trusts the forest that contains the user accounts, this configuration supports user-based policies for devices on the internet when you enable the **Client Policy** client setting **Enable user policy requests from internet clients**.  

For example, the following configurations illustrate when internet-based client management supports user policies for devices on the internet:  

-   The internet-based management point is in the perimeter network where a read-only domain controller resides to authenticate the user and an intervening firewall allows Active Directory packets.  

-   The user account is in Forest A (the intranet) and the internet-based management point is in Forest B (the perimeter network). Forest B trusts Forest A, and an intervening firewall allows the authentication packets.  

-   The user account and the internet-based management point are in Forest A (the intranet). The management point is published to the internet by using a web proxy server (like Forefront Threat Management Gateway).  

> [!NOTE]  
>  If Kerberos authentication fails, NTLM authentication is then automatically tried.  

As the previous example shows, you can place internet-based site systems in the intranet when they're published to the internet by using a web proxy server. These site systems can be configured for client connection from the internet only, or for client connections from the internet and intranet. When you use a web proxy server, you can configure it for Secure Sockets Layer (SSL) bridging to SSL (more secure) or SSL tunneling as follows:  

-   **SSL bridging to SSL:**   
    The recommended configuration when you use proxy web servers for internet-based client management is SSL bridging to SSL, which uses SSL termination with authentication. Client computers must be authenticated by using computer authentication, and mobile device legacy clients are authenticated by using user authentication. Mobile devices that are enrolled by Configuration Manager don't support SSL bridging.  

     The benefit of SSL termination at the proxy web server is that packets from the internet are subject to inspection before they're forwarded to the internal network. The proxy web server authenticates the connection from the client, terminates it, and then opens a new authenticated connection to the internet-based site systems. When Configuration Manager clients use a proxy web server, the client identity (client GUID) is securely contained in the packet payload so that the management point doesn't consider the proxy web server to be the client. Bridging isn't supported in Configuration Manager with HTTP to HTTPS, or from HTTPS to HTTP.  

-   **Tunneling**:   
    If your proxy web server can't support the requirements for SSL bridging, or you want to configure internet support for mobile devices that are enrolled by Configuration Manager, SSL tunneling is also supported. It's a less secure option because the SSL packets from the internet are forwarded to the site systems without SSL termination, so they can't be inspected for malicious content. When you use SSL tunneling, there are no certificate requirements for the proxy web server.  



##  <a name="Plan_Com_X-Forest"></a> Communications across Active Directory forests  

Configuration Manager supports sites and hierarchies that span Active Directory forests.  

Configuration Manager also supports domain computers that aren't in the same Active Directory forest as the site server, and computers that are in workgroups:  

#### Support domain computers in a forest that's not trusted by your site server's forest 

-   Install site system roles in that untrusted forest, with the option to publish site information to that Active Directory forest  

-   Manage these computers as if they're workgroup computers  

When you install site system servers in an untrusted Active Directory forest, the client-to-server communication from clients in that forest is kept within that forest, and Configuration Manager can authenticate the computer by using Kerberos. When you publish site information to the client's forest, clients benefit from retrieving site information, such as a list of available management points, from their Active Directory forest, rather than downloading this information from their assigned management point.  

> [!NOTE]  
>  If you want to manage devices that are on the internet, you can install internet-based site system roles in your perimeter network when the site system servers are in an Active Directory forest. This scenario doesn't require two-way trust between the perimeter network and the site server's forest.  

#### Support computers in a workgroup  

-   Manually approve workgroup computers when they use HTTP client connections to site system roles. Configuration Manager can't authenticate these computers by using Kerberos.  

-   Configure workgroup clients to use the Network Access Account so that these computers can retrieve content from distribution points.  

-   Provide an alternative mechanism for workgroup clients to find management points. Use DNS publishing, WINS, or directly assign a management point. These clients can't retrieve site information from Active Directory Domain Services.  

For more information, see the following articles:  

-   [Manage conflicting records](/sccm/core/clients/manage/manage-clients#BKMK_ConflictingRecords)  

-   [Network access account](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#accounts-used-for-content-management)  

-   [How to install Configuration Manager clients on workgroup computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup)  


###  <a name="bkmk_span"></a> Scenarios to support a site or hierarchy that spans multiple domains and forests  

#### Scenario 1: Communication between sites in a hierarchy that spans forests  
This scenario requires a two-way forest trust that supports Kerberos authentication.  If you don't have a two-way forest trust that supports Kerberos authentication, then Configuration Manager doesn't support a child site in the remote forest.  

Configuration Manager supports installing a child site in a remote forest that has the required two-way trust with the forest of the parent site. For example, you can place a secondary site in a different forest from its primary parent site as long as the required trust exists.  

> [!NOTE]  
>  A child site can be a primary site (where the central administration site is the parent site) or a secondary site.  

Intersite communication in Configuration Manager uses database replication and file-based transfers. When you install a site, you must specify an account with which to install the site on the designated server. This account also establishes and maintains communication between sites. After the site successfully installs and initiates file-based transfers and database replication, you don't have to configure anything else for communication to the site.  

When a two-way forest trust exists, Configuration Manager doesn't require any additional configuration steps.  

By default, when you install a new child site, Configuration Manager configures the following components:  

-   An intersite file-based replication route at each site that uses the site server computer account. Configuration Manager adds the computer account of each computer to the **SMS_SiteToSiteConnection_&lt;sitecode\>** group on the destination computer.  

-   Database replication between the SQL Servers at each site.  

Also set the following configurations:  

-   Intervening firewalls and network devices must allow the network packets that Configuration Manager requires.  

-   Name resolution must work between the forests.  

-   To install a site or site system role, you must specify an account that has local administrator permissions on the specified computer.  

#### Scenario 2: Communication in a site that spans forests  
This scenario doesn't require a two-way forest trust.  

Primary sites support the installation of site system roles on computers in remote forests.  

-   The Application Catalog web service point is the only exception.  It's only supported in the same forest as the site server.  

-   When a site system role accepts connections from the internet, as a security best practice, install the site system roles in a location where the forest boundary provides protection for the site server (for example, in a perimeter network).  

To install a site system role on a computer in an untrusted forest:  

- Specify a **Site System Installation Account**, which the site uses to install the site system role. (This account must have local administrative credentials to connect to.) Then install site system roles on the specified computer.  

- Select the site system option **Require the site server to initiate connections to this site system**. This setting requires the site server to establish connections to the site system server to transfer data. This configuration prevents the computer in the untrusted location from initiating contact with the site server that's inside your trusted network. These connections use the **Site System Installation Account**.  

To use a site system role that was installed in an untrusted forest, firewalls must allow the network traffic even when the site server initiates the transfer of data.  

Additionally, the following site system roles require direct access to the site database. Therefore, firewalls must allow applicable traffic from the untrusted forest to the site's SQL Server:  

-   Asset Intelligence synchronization point  

-   Endpoint Protection point  

-   Enrollment point  

-   Management point  

-   Reporting service point  

-   State migration point  

For more information, see [Ports used in Configuration Manager](/sccm/core/plan-design/hierarchy/ports).  

You might need to configure the management point and enrollment point access to the site database.

-   By default, when you install these roles, Configuration Manager configures the computer account of the new site system server as the connection account for the site system role. It then adds the account to the appropriate SQL Server database role.  

-   When you install these site system roles in an untrusted domain, configure the site system role connection account to enable the site system role to obtain information from the database.  

If you configure a domain user account to be the connection account for these site system roles, make sure that the domain user account  has appropriate access to the SQL Server database at that site:  

-   Management point: **Management Point Database Connection Account**  

-   Enrollment point: **Enrollment Point Connection Account**  

Consider the following additional information when you plan for site system roles in other forests:  

-   If you run Windows Firewall, configure the applicable firewall profiles to pass communications between the site database server and computers that are installed with remote site system roles.   

-   When the internet-based management point trusts the forest that contains the user accounts, user policies are supported. When no trust exists, only computer policies are supported.  

#### Scenario 3: Communication between clients and site system roles when the clients aren't in the same Active Directory forest as their site server  
Configuration Manager supports the following scenarios for clients that aren't in the same forest as their site's site server:  

-   There's a two-way forest trust between the forest of the client and the forest of the site server.  

-   The site system role server is located in the same forest as the client.  

-   The client is on a domain computer that doesn't have a two-way forest trust with the site server, and site system roles aren't installed in the client's forest.  

-   The client is on a workgroup computer.  

Clients on a domain-joined computer can use Active Directory Domain Services for service location when their site is published to their Active Directory forest.  

To publish site information to another Active Directory forest:  

-   Specify the forest and then enable publishing to that forest in the **Active Directory Forests** node of the **Administration** workspace.  

-   Configure each site to publish its data to Active Directory Domain Services. This configuration enables clients in that forest to retrieve site information and find management points. For clients that can't use Active Directory Domain Services for service location, you can use DNS, WINS, or the client's assigned management point.  


####  <a name="bkmk_xchange"></a> Scenario 4: Put the Exchange Server connector in a remote forest  

To support this scenario, make sure that name resolution works between the forests. For example, configure DNS forwards. When you configure the Exchange Server connector, specify the intranet FQDN of the Exchange Server. For more information, see [Manage mobile devices with Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  
