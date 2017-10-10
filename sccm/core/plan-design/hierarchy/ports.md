---
title: "Ports used by Configuration Manager"
description: "Learn about the required and customizable ports that System Center Configuration Manager uses for connections."
ms.custom: na
ms.date: 09/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Ports used in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager is a distributed client/server system. The distributed nature of Configuration Manager means that connections can be established between site servers, site systems, and clients. Some connections use ports that are not configurable, and some support custom ports that you specify. You must verify that the required ports are available if you use any port filtering technology such as firewalls, routers, proxy servers, or IPsec.  
    
> [!NOTE]  
>  If you support Internet-based clients by using SSL bridging, in addition to port requirements, you might also have to allow some HTTP verbs and headers to traverse your firewall.   

 The port listings that follow are used by Configuration Manager and do not include information for standard Windows services, such as Group Policy settings for Active Directory Domain Services or Kerberos authentication. For information about Windows Server services and ports, see [Service overview and network port requirements for the Windows Server system](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="BKMK_ConfigurablePorts"></a> Ports you can configure  
 Configuration Manager enables you to configure the ports for the following types of communication:  

-   Application Catalog website point to Application Catalog web service point  

-   Enrollment proxy point to enrollment point  

-   Client-to-site systems that run IIS  

-   Client to Internet (as proxy server settings)  

-   Software update point to Internet (as proxy server settings)  

-   Software update point to WSUS server  

-   Site server to site database server  

-   Reporting services points  

    > [!NOTE]  
    >  The ports that are in use for the reporting services point site system role are configured in SQL Server Reporting Services. These ports are then used by Configuration Manager during communications to the reporting services point. Be sure to review these ports that define the IP filter information for IPsec policies or for configuring firewalls.  

By default, the HTTP port that's used for client-to-site system communication is port 80, and the default HTTPS port is 443. Ports for client-to-site system communication over HTTP or HTTPS can be changed during setup or in the site properties for your Configuration Manager site.  

The ports that are in use for the reporting services point site system role are configured in SQL Server Reporting Services. These ports are then used by Configuration Manager during communications to the reporting services point. Be sure to review these ports when you're defining the IP filter information for IPsec policies or for configuring firewalls.  

##  <a name="BKMK_NonConfigurablePorts"></a> Non-configurable ports  
Configuration Manager does not allow you to configure ports for the following types of communication:  

-   Site to site  

-   Site server to site system  

-   Configuration Manager console to SMS Provider  

-   Configuration Manager console to the Internet  

-   Connections to cloud services, such as Microsoft Intune and cloud-based distribution points  

##  <a name="BKMK_CommunicationPorts"></a> Ports used by Configuration Manager clients and site systems  
The following sections detail the ports that are used for communication in Configuration Manager. The arrows in the section title represent the direction of the communication:  

-   -- > Indicates that one computer initiates communication and the other computer always responds  

-   &lt; -- > Indicates that either computer can initiate communication  

###  <a name="BKMK_PortsAI"></a> Asset Intelligence synchronization point -- > Microsoft  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a> Asset Intelligence synchronization point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a> Application Catalog web service point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Application Catalog website point -- > Application Catalog web service point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client -- > Application Catalog website point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Client -- > Client  
 In addition to the ports that are listed in the following table, wake-up proxy also uses Internet Control Message Protocol (ICMP) echo request messages from one client to another client when they are configured for wake-up proxy.

This communication is used to confirm whether the other client computer is awake on the network. ICMP is sometimes referred to as TCP/IP ping commands. ICMP does not have a UDP or TCP protocol number, and so it is not listed in the following table. However, any host-based firewalls on these client computers or intervening network devices within the subnet must permit ICMP traffic for wake-up proxy communication to succeed.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 (See note 2, **Alternate port available**)|--|  
|Wake-up proxy|25536 (See note 2, **Alternate port available**)|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> Client -- > Configuration Manager Policy Module (Network Device Enrollment Service)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)||80|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a> Client -- > Cloud-based distribution point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a> Client -- > Distribution point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsClient-DP2"></a> Client -- > Distribution point configured for multicast  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Multicast protocol|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> Client -- > Distribution point configured for PXE  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Dynamic Host Configuration Protocol (DHCP)|67 and 68|--|  
|Trivial File Transfer Protocol (TFTP)|69 (See note 4, **Trivial FTP (TFTP) Daemon**)|--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a> Client -- > Fallback status point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsClient-GCDC"></a> Client -- > Global catalog domain controller  
 A Configuration Manager client does not contact a global catalog server when it is a workgroup computer or when it is configured for Internet-only communication.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Global catalog LDAP|--|3268|  


###  <a name="BKMK_PortsClient-MP"></a> Client -- > Management point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Client notification (default communication before falling back to HTTP or HTTPS)|--|10123 (See note 2, **Alternate port available**)|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsClient-SUP"></a> Client -- > Software update point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 or 8530 (See note 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 or 8531 (See note 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsClient-SMP"></a> Client -- > State migration point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a> Configuration Manager console -- > Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Remote Control (control)|--|2701|  
|Remote Assistance (RDP and RTC)|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a> Configuration Manager console -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a> Configuration Manager console -- > Reporting Services point  


|Description|UDP|TCP|
|-----------------|---------|---------|   
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsConsole-Site"></a> Configuration Manager console -- > Site server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (initial connection to WMI to locate provider system)|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a> Configuration Manager console -- > SMS Provider  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager Policy Module (Network Device Enrollment Service) -- > Certificate registration point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsDist_MP"></a> Distribution point -- > Management point  
 A distribution point communicates to the management point in the following scenarios:  

-   To report the status of prestaged content  

-   To report usage summary data  

-   To report content validation  

-   To report the status of package downloads (pull-distribution point)

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate port available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection point -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Enrollment proxy point -- > Enrollment point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Enrollment point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server Connector -- > Exchange Online  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management over HTTPS|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server Connector -- > On-Premises Exchange Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management over HTTP|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac computer -- > Enrollment proxy point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a> Management point -- > Domain controller  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|--|389|  
|Global catalog LDAP|--|3268|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsMP-Site"></a> Management point &lt; -- > Site server  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Endpoint mapper|--|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a> Management point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobile device -- > Enrollment proxy point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Mobile device -- > Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a> Reporting Services point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Service connection point -- > Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|
For more information see [Internet access requirements](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) for the service connection point.

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Site server &lt; -- > Application Catalog web service point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Site server &lt; -- > Application Catalog website point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-AISP"></a> Site server &lt; -- > Asset Intelligence synchronization point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-Client"></a> Site server -- > Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 (See note 2, **Alternate port available**)|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a> Site server -- > Cloud-based distribution point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a> Site server -- > Distribution point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-DC"></a> Site server -- > Domain controller  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|--|389|  
|Global catalog LDAP|--|3268|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Site server &lt; -- > Certificate registration point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> Site server &lt; -- > Endpoint Protection point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> Site server &lt; -- > Enrollment point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Site server &lt; -- > Enrollment proxy point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-FSP"></a> Site server &lt; -- > Fallback status point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortSite-Internet"></a> Site server -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 1, **Proxy server port**)|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> Site server &lt; -- > Issuing certification authority (CA)  
 This communication is used when you deploy certificate profiles by using the certificate registration point. The communication is not used for every site server in the hierarchy. Instead, it's used only for the site server at the top of the hierarchy.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Endpoint Mapper|135|135|  
|RPC (DCOM)|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-RSP"></a> Site server &lt; -- > Reporting services point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-Site"></a> Site server &lt; -- > Site server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a> Site server -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

 During the installation of a site that uses a remote SQL Server to host the site database, you must open the following ports between the site server and the SQL Server:  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-Provider"></a> Site server -- > SMS Provider  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-SUP"></a> Site server &lt; -- > Software update point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Hypertext Transfer Protocol (HTTP)|--|80 or 8530 (See note 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 or 8531 (See note 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSite-SMP"></a> Site server &lt; -- > State migration point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> SMS Provider -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  

###  <a name="BKMK_PortsSUP-Internet"></a> Software update point -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 1, **Proxy server port**)|  

###  <a name="BKMK_PortsSUP-WSUS"></a> Software update point -- > Upstream WSUS server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 or 8530 (See note 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 or 8531 (See note 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --> SQL Server  
 Intersite database replication requires the SQL Server at one site to communicate directly with the SQL Server at its parent or child site.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server service|--|1433 (See note 2, **Alternate port available**)|  
|SQL Server Service Broker|--|4022 (See note 2, **Alternate port available**)|  

> [!TIP]  
>  Configuration Manager does not require the SQL Server Browser, which uses port UDP 1434.  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> State migration point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate port available**)|  



###  <a name="BKMY_PortNotes"></a> Notes for ports used by Configuration Manager clients and site systems  

1.  **Proxy server port**: This port cannot be configured but can be routed through a configured proxy server.  

2.  **Alternate port available**: An alternate port can be defined within Configuration Manager for this value. If a custom port has been defined, substitute that custom port when defining the IP filter information for IPsec policies or for configuring firewalls.  

3.  **Windows Server Update Services (WSUS)**: WSUS can be installed to use either ports 80/443 or ports 8530/8531 for client communication. When you run WSUS in Windows Server 2012 or Windows Server 2016, WSUS is configured by default to use port 8530 for HTTP and port 8531 for HTTPS.  

     After installation, the port can be changed. You do not have to use the same port number throughout the site hierarchy.  

    -   If the HTTP port is 80, the HTTPS port must be 443.  

    -   If the HTTP port is anything else, the HTTPS port must be 1 or higher, for example, 8530 and 8531.   

    > [!NOTE]  
    >  When you configure the software update point to use HTTPS, the HTTP port must also be open. Unencrypted data, such as the EULA for specific updates, uses the HTTP port.  

4.  **Trivial FTP (TFTP) Daemon**: The Trivial FTP (TFTP) Daemon system service does not require a user name or password and is an integral part of Windows Deployment Services (WDS). The Trivial FTP Daemon service implements support for the TFTP protocol that's defined by the following RFCs:  

    -   RFC 350: TFTP  

    -   RFC 2347: Option extension  

    -   RFC 2348: Block size option  

    -   RFC 2349: Time-out interval and transfer size options  

     Trivial File Transfer Protocol is designed to support diskless boot environments. TFTP Daemons listen on UDP port 69 but respond from a dynamically allocated high port. Therefore, enabling this port allows the TFTP service to receive incoming TFTP requests but doesn't allow the selected server to respond to those requests. You can't enable the selected server to respond to inbound TFTP requests unless the TFTP server is configured to respond from port 69.  

5.  **Communication between the site server and site systems**: By default, communication between the site server and site systems is bi-directional. The site server initiates communication to configure the site system, and then most site systems connect back to the site server to send status information. Reporting service points and distribution points do not send status information. If you select **Require the site server to initiate connections to this site system** on the site system properties after the site system has been installed, the site system won't initiate communication with the site server. Instead, the site server initiates the communication and uses the site system installation account for authentication to the site system server.  

6.  **Dynamic ports**: Dynamic ports (also known as ephemeral ports) use a range of port numbers that's defined by the operating system version. For more information about the default port ranges, see [Service overview and network port requirements for Windows](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="BKMK_AdditionalPorts"></a> Additional lists of ports  
 The following sections provide additional information about ports that are used by Configuration Manager.  

###  <a name="BKMK_ClientShares"></a> Client to server shares  
 Clients use Server Message Block (SMB) whenever they connect to UNC shares. For example:  

-   Manual client installation that specifies the CCMSetup.exe **/source:** command-line property  

-   Endpoint Protection clients that download definition files from a UNC path

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> Connections to Microsoft SQL Server  
 For communication to the SQL Server database engine and for intersite replication, you can use the default SQL Server port or specify custom ports:  

-   Intersite communications use:  

    -   SQL Server Service Broker, which defaults to port TCP 4022.  

    -   SQL Server service, which defaults to port TCP 1433.  

-   Intrasite communication between the SQL Server database engine and various Configuration Manager site system roles defaults to port TCP 1433.  

- Configuration Manager uses the same ports and protocols to communicate with each SQL Availability Group replica that hosts the site database as if the replica was a standalone SQL Server instance.

When you use Azure and the site database is behind an Internal or External Load Balancer, configure the following firewall exceptions on each replica and add load balancing rules for the following ports:
 - SQL over TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - Server Message Block (SMB): TCP 445
 - RPC Endpoint Mapper: TCP 135

> [!WARNING]  
>  Configuration Manager does not support dynamic ports. Because SQL Server named instances by default use dynamic ports for connections to the database engine, when you use a named instance, you must manually configure the static port that you want to use for intrasite communication.  

 The following site system roles communicate directly with the SQL Server database:  

-   Application Catalog web service point  

-   Certificate registration point role  

-   Enrollment point role  

-   Management point  

-   Site server  

-   Reporting Services point  

-   SMS Provider  

-   SQL Server --> SQL Server  

When a SQL Server hosts a database from more than one site, each database must use a separate instance of SQL Server, and each instance must be configured with a unique set of ports.  

If you have a firewall enabled on the SQL Server computer, ensure that it is configured to allow the ports in use by your deployment. Also configure firewalls that are at additional locations on the network between computers that communicate with the SQL Server to allow these same ports.  

For an example of how to configure SQL Server to use a specific port, see [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) in the SQL Server TechNet library.  


### <a name="bkmk_discovery"> </a> Discovery and publishing
The following ports are used for the discovery and publishing of site information:
 - Lightweight Directory Access Protocol (LDAP): 389
 - Global catalog LDAP: 3268
 - RPC Endpoint Mapper: 135
 - RPC: Dynamically allocated high TCP ports
 - TCP: 1024: 5000
 - TCP:  49152: 65535


###  <a name="BKMK_External"></a> External connections made by Configuration Manager  
 Configuration Manager clients or site systems can make the following external connections:  

-   [Asset Intelligence synchronization point -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Endpoint Protection point -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Client -- &gt; Global catalog domain controller](#BKMK_PortsClient-GCDC)  

-   [Configuration Manager console -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Management point -- &gt; Domain controller](#BKMK_PortsMP-DC)  

-   [Site server -- &gt; Domain controller](#BKMK_PortsSite-DC)  

-   [Site server &lt; -- &gt; Issuing Certification Authority (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Software update point -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Software update point -- &gt; Upstream WSUS Server](#BKMK_PortsSUP-WSUS)  

-   [Service connection point -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> Installation requirements for site systems that support Internet-based clients  
 Management points and distribution points that support Internet-based clients, the software update point, and the fallback status point use the following ports for installation and repair:  

-   Site server --> Site system: RPC endpoint mapper using UDP and TCP port 135.  

-   Site server --> Site system: RPC dynamic TCP ports  

-   Site server &lt; --> Site system: Server message blocks (SMB) using TCP port 445

Application and package installations on distribution points require the following RPC ports:  

-   Site server --> Distribution point: RPC endpoint mapper using UDP and TCP port 135

-   Site server --> Distribution point: RPC dynamic TCP ports  

Use IPsec to help secure the traffic between the site server and site systems. If you must restrict the dynamic ports that are used with RPC, you can use the Microsoft RPC configuration tool (rpccfg.exe) to configure a limited range of ports for these RPC packets. For more information about the RPC configuration tool, see [How to configure RPC to use certain ports and how to help secure those ports by using IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Before you install these site systems, ensure that the remote registry service is running on the site system server and that you have specified a site system installation account if the site system is in a different Active Directory forest without a trust relationship.  

###  <a name="BKMK_PortsClientInstall"></a> Ports used by Configuration Manager client installation  
The ports that are using during client installation depend on the client deployment method. For a list of ports for each client deployment method, see **Ports used during Configuration Manager client deployment** in the [Windows Firewall and port settings for clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) topic. For information about how to configure Windows Firewall on the client for client installation and post-installation communication, see [Windows Firewall and port settings for clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="BKMK_MigrationPorts"></a> Ports used by migration  
The site server that runs migration uses several ports to connect to applicable sites in the source hierarchy to gather data from the source sites' SQL Server databases, and to share distribution points.  

 For information about these ports, see the [Required configurations for migration](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) section in the  [Prerequisites for migration in System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md) topic.  

###  <a name="BKMK_ServerPorts"></a> Ports used by Windows Server  
 The following table lists some of the key ports used by Windows Server along with their respective functions. For a more complete list of Windows Server services and network ports requirements, see [Service overview and network port requirements for the Windows Server system](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Domain Name System (DNS)|53|53|  
|Dynamic Host Configuration Protocol (DHCP)|67 and 68|--|  
|NetBIOS Name Resolution|137|--|  
|NetBIOS Datagram Service|138|--|  
|NetBIOS Session Service|--|139|  
