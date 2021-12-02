---
title: Communications between endpoints
titleSuffix: Configuration Manager
description: Learn how Configuration Manager site systems and components communicate across a network.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Communications between endpoints in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article describes how Configuration Manager site systems and clients communicate across your network. It includes the following sections:  

- [Communications between site systems in a site](#Planning_Intra-site_Com)  
  - [Site server to distribution point](#bkmk_site2dp)  

- [Communications from clients to site systems and services](#Planning_Client_to_Site_System)  
  - [Client to management point communication](#bkmk_client2mp)  
  - [Client to distribution point communication](#bkmk_client2dp)  
  - [Considerations for client communications from the internet or an untrusted forest](#BKMK_clientspan)  

- [Communications across Active Directory forests](#Plan_Com_X-Forest)  
  - [Support domain computers in a forest that's not trusted by your site server's forest](#bkmk_noforesttrust)  
  - [Support computers in a workgroup](#bkmk_workgroup)  
  - [Scenarios to support a site or hierarchy that spans multiple domains and forests](#bkmk_span)  

## <a name="Planning_Intra-site_Com"></a> Communications between site systems in a site  

When Configuration Manager site systems or components communicate across the network to other site systems or components in the site, they use one of the following protocols, depending on how you configure the site:  

- Server message block (SMB)  

- HTTP  

- HTTPS  

With the exception of communication from the site server to a distribution point, server-to-server communications in a site can occur at any time. These communications don't use mechanisms to control the network bandwidth. Because you can't control the communication between site systems, make sure that you install site system servers in locations that have fast and well-connected networks.  

### <a name="bkmk_site2dp"></a> Site server to distribution point

To help you manage the transfer of content from the site server to distribution points, use the following strategies:  

- Configure the distribution point for network bandwidth control and scheduling. These controls resemble the configurations that are used by intersite addresses. Use this configuration instead of installing another Configuration Manager site when the transfer of content to remote network locations is your main bandwidth consideration.  

- You can install a distribution point as a prestaged distribution point. A prestaged distribution point lets you use content that is manually put on the distribution point server and removes the requirement to transfer content files across the network.  

For more information, see [Manage network bandwidth for content management](manage-network-bandwidth.md).

## <a name="Planning_Client_to_Site_System"></a> Communications from clients to site systems and services

Clients initiate communication to site system roles, Active Directory Domain Services, and online services. To enable these communications, firewalls must allow the network traffic between clients and the endpoint of their communications. For more information about ports and protocols used by clients when they communicate to these endpoints, see [Ports used in Configuration Manager](ports.md).  

Before a client can communicate with a site system role, the client uses service location to find a role that supports the client's protocol (HTTP or HTTPS). By default, clients use the most secure method that's available to them. For more information, see  [Understand how clients find site resources and services](understand-how-clients-find-site-resources-and-services.md).  

To help secure the communication between Configuration Manager clients and site servers, configure one of the following options:

- Use a public key infrastructure (PKI) and install PKI certificates on clients and servers. Enable site systems to communicate with clients over HTTPS. For information about how to use certificates, see [PKI certificate requirements](../network/pki-certificate-requirements.md).

- Configure the site to **Use Configuration Manager-generated certificates for HTTP site systems**. For more information, see [Enhanced HTTP](enhanced-http.md).

When you deploy a site system role that uses Internet Information Services (IIS) and supports communication from clients, you must specify whether clients connect to the site system by using HTTP or HTTPS. If you use HTTP, you must also consider signing and encryption choices. For more information, see [Planning for signing and encryption](../security/plan-for-security.md#signing-and-encryption).

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

### <a name="bkmk_client2mp"></a> Client to management point communication

There are two stages when a client communicates with a management point: authentication (transport) and authorization (message). This process varies depending upon the following factors:

- Site configuration: HTTPS only, allows HTTP or HTTPS, or allows HTTP or HTTPS with enhanced HTTP enabled
- Management point configuration: HTTPS or HTTP
- Device identity for device-centric scenarios
- User identity for user-centric scenarios

Use the following table to understand how this process works:  

| MP type  | Client authentication  | Client authorization<br>Device identity  | Client authorization<br>User identity  |
|----------|---------|---------|---------|
| HTTP     | Anonymous<br>With Enhanced HTTP, the site verifies the Azure AD *user* or *device* token. | Location request: Anonymous<br>Client package: Anonymous<br>Registration, using one of the following methods to prove device identity:<br> - Anonymous (manual approval)<br> - Windows-integrated authentication<br> - Azure AD *device* token (Enhanced HTTP)<br>After registration, the client uses message signing to prove device identity | For user-centric scenarios, using one of the following methods to prove user identity:<br> - Windows-integrated authentication<br> - Azure AD *user* token (Enhanced HTTP) |
| HTTPS    | Using one of the following methods:<br> - PKI certificate<br> - Windows-integrated authentication<br> - Azure AD *user* or *device* token | Location request: Anonymous<br>Client package: Anonymous<br>Registration, using one of the following methods to prove device identity:<br> - Anonymous (manual approval)<br> - Windows-integrated authentication<br> - PKI certificate<br> - Azure AD *user* or *device* token<br>After registration, the client uses message signing to prove device identity | For user-centric scenarios, using one of the following methods to prove user identity:<br> - Windows-integrated authentication<br> - Azure AD *user* token |

> [!Tip]  
> For more information on the configuration of the management point for different device identity types and with the cloud management gateway, see [Enable management point for HTTPS](../../clients/manage/cmg/configure-authentication.md#enable-management-point-for-https).  

### <a name="bkmk_client2dp"></a> Client to distribution point communication

When a client communicates with a distribution point, it only needs to authenticate before downloading the content. Use the following table to understand how this process works:

| DP type  | Client authentication  |
|----------|---------|
| HTTP     | - Anonymous, if allowed<br>- Windows-integrated authentication with computer account or network access account<br> - Content access token (Enhanced HTTP) |
| HTTPS    | - PKI certificate<br> - Windows-integrated authentication with computer account or network access account<br> - Content access token |

### <a name="BKMK_clientspan"></a> Considerations for client communications from the internet or an untrusted forest

For more information, see the following articles:

- [Overview of cloud management gateway](../..//clients/manage/cmg/overview.md)

- [Plan for internet-based client management](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="Plan_Com_X-Forest"></a> Communications across Active Directory forests  

Configuration Manager supports sites and hierarchies that span Active Directory forests. It also supports domain computers that aren't in the same Active Directory forest as the site server, and computers that are in workgroups.  

### <a name="bkmk_noforesttrust"></a> Support domain computers in a forest that's not trusted by your site server's forest

- Install site system roles in that untrusted forest, with the option to publish site information to that Active Directory forest  

- Manage these computers as if they're workgroup computers  

When you install site system servers in an untrusted Active Directory forest, the client-to-server communication from clients in that forest is kept within that forest, and Configuration Manager can authenticate the computer by using Kerberos. When you publish site information to the client's forest, clients benefit from retrieving site information, such as a list of available management points, from their Active Directory forest, rather than downloading this information from their assigned management point.  

> [!NOTE]  
> If you want to manage devices that are on the internet, you can install internet-based site system roles in your perimeter network when the site system servers are in an Active Directory forest. This scenario doesn't require two-way trust between the perimeter network and the site server's forest.  

### <a name="bkmk_workgroup"></a> Support computers in a workgroup  

- Manually approve workgroup computers when they use HTTP client connections to site system roles. Configuration Manager can't authenticate these computers by using Kerberos.  

- Configure workgroup clients to use the Network Access Account so that these computers can retrieve content from distribution points.  

- Provide an alternative mechanism for workgroup clients to find management points. Use DNS publishing or directly assign a management point. These clients can't retrieve site information from Active Directory Domain Services.  

For more information, see the following articles:  

- [Manage conflicting records](../../clients/manage/manage-clients.md#manage-conflicting-records)  

- [Network access account](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [How to install Configuration Manager clients on workgroup computers](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="bkmk_span"></a> Scenarios to support a site or hierarchy that spans multiple domains and forests  

#### Scenario 1: Communication between sites in a hierarchy that spans forests

This scenario requires a two-way forest trust that supports Kerberos authentication.  If you don't have a two-way forest trust that supports Kerberos authentication, then Configuration Manager doesn't support a child site in the remote forest.  

Configuration Manager supports installing a child site in a remote forest that has the required two-way trust with the forest of the parent site. For example, you can place a secondary site in a different forest from its primary parent site as long as the required trust exists.  

> [!NOTE]  
> A child site can be a primary site (where the central administration site is the parent site) or a secondary site.  

Intersite communication in Configuration Manager uses database replication and file-based transfers. When you install a site, you must specify an account with which to install the site on the designated server. This account also establishes and maintains communication between sites. After the site successfully installs and initiates file-based transfers and database replication, you don't have to configure anything else for communication to the site.  

When a two-way forest trust exists, Configuration Manager doesn't require any additional configuration steps.  

By default, when you install a new child site, Configuration Manager configures the following components:  

- An intersite file-based replication route at each site that uses the site server computer account. Configuration Manager adds the computer account of each computer to the **SMS_SiteToSiteConnection_&lt;sitecode\>** group on the destination computer.  

- Database replication between the SQL Servers at each site.  

Also set the following configurations:  

- Intervening firewalls and network devices must allow the network packets that Configuration Manager requires.  

- Name resolution must work between the forests.  

- To install a site or site system role, you must specify an account that has local administrator permissions on the specified computer.  

#### Scenario 2: Communication in a site that spans forests

This scenario doesn't require a two-way forest trust.  

Primary sites support the installation of site system roles on computers in remote forests.  

- When a site system role accepts connections from the internet, as a security best practice, install the site system roles in a location where the forest boundary provides protection for the site server (for example, in a perimeter network).  

To install a site system role on a computer in an untrusted forest:  

- Specify a **Site System Installation Account**, which the site uses to install the site system role. (This account must have local administrative credentials to connect to.) Then install site system roles on the specified computer.  

- Select the site system option **Require the site server to initiate connections to this site system**. This setting requires the site server to establish connections to the site system server to transfer data. This configuration prevents the computer in the untrusted location from initiating contact with the site server that's inside your trusted network. These connections use the **Site System Installation Account**.  

To use a site system role that was installed in an untrusted forest, firewalls must allow the network traffic even when the site server initiates the transfer of data.  

Additionally, the following site system roles require direct access to the site database. Therefore, firewalls must allow applicable traffic from the untrusted forest to the site's SQL Server:  

- Asset Intelligence synchronization point  

- Endpoint Protection point  

- Enrollment point  

- Management point  

- Reporting service point  

- State migration point  

For more information, see [Ports used in Configuration Manager](ports.md).  

You might need to configure the management point and enrollment point access to the site database.

- By default, when you install these roles, Configuration Manager configures the computer account of the new site system server as the connection account for the site system role. It then adds the account to the appropriate SQL Server database role.  

- When you install these site system roles in an untrusted domain, configure the site system role connection account to enable the site system role to obtain information from the database.  

If you configure a domain user account to be the connection account for these site system roles, make sure that the domain user account  has appropriate access to the SQL Server database at that site:  

- Management point: **Management Point Database Connection Account**  

- Enrollment point: **Enrollment Point Connection Account**  

Consider the following additional information when you plan for site system roles in other forests:  

- If you run Windows Firewall, configure the applicable firewall profiles to pass communications between the site database server and computers that are installed with remote site system roles.

- When the internet-based management point trusts the forest that contains the user accounts, user policies are supported. When no trust exists, only computer policies are supported.  

#### Scenario 3: Communication between clients and site system roles when the clients aren't in the same Active Directory forest as their site server

Configuration Manager supports the following scenarios for clients that aren't in the same forest as their site's site server:  

- There's a two-way forest trust between the forest of the client and the forest of the site server.  

- The site system role server is located in the same forest as the client.  

- The client is on a domain computer that doesn't have a two-way forest trust with the site server, and site system roles aren't installed in the client's forest.  

- The client is on a workgroup computer.  

Clients on a domain-joined computer can use Active Directory Domain Services for service location when their site is published to their Active Directory forest.  

To publish site information to another Active Directory forest:  

- Specify the forest and then enable publishing to that forest in the **Active Directory Forests** node of the **Administration** workspace.  

- Configure each site to publish its data to Active Directory Domain Services. This configuration enables clients in that forest to retrieve site information and find management points. For clients that can't use Active Directory Domain Services for service location, you can use DNS or the client's assigned management point.

#### <a name="bkmk_xchange"></a> Scenario 4: Put the Exchange Server connector in a remote forest  

To support this scenario, make sure that name resolution works between the forests. For example, configure DNS forwards. When you configure the Exchange Server connector, specify the intranet FQDN of the Exchange Server. For more information, see [Manage mobile devices with Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## See also

- [Plan for security](../security/plan-for-security.md)  

- [Security and privacy for Configuration Manager clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
