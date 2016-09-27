---
title: "Ports used in System Center Configuration Manager"
ms.custom: na
ms.date: 02/10/2016
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

---
# Ports used in System Center Configuration Manager
System Center Configuration Manager is a distributed client/server system. The distributed nature of Configuration Manager means that connections can be established between site servers, site systems, and clients. Some connections use ports that are not configurable, and some support custom ports you specify. You must verify that the required ports are available if you use any port filtering technology such as firewalls, routers, proxy servers, and IPsec.  

> [!NOTE]  
>  If you support Internet-based clients by using SSL bridging, in addition to port requirements, you might have to also allow some HTTP verbs and headers to traverse your firewall. .  

 The port listings that follow are used by Configuration Manager and do not include information for standard Windows services, such as Group Policy settings for Active Directory Domain Services and Kerberos authentication. For information about Windows Server services and ports, see [Service overview and network port requirements for the Windows Server system](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="BKMK_ConfigurablePorts"></a> Ports you can configure  
 Configuration Manager allows you to configure the ports for the following types of communication:  

-   Application Catalog Website point to Application Catalog web service point  

-   Enrollment proxy point to enrollment point  

-   Client to site systems that run IIS  

-   Client to Internet (as proxy server settings)  

-   Software update point to Internet (as proxy server settings)  

-   Software update point to WSUS server  

-   Site server to site database server  

-   Reporting services points  

    > [!NOTE]  
    >  The ports in use for the reporting services point site system role are configured in SQL Server Reporting Services. These ports are then used by Configuration Manager during communications to the reporting services point. Be sure to review these ports defining the IP filter information for IPsec policies or for configuring firewalls.  

By default, the HTTP port used for client to site system communication is port 80, and the default HTTPS port is 443. Ports for client-to-site system communication over HTTP or HTTPS can be changed during Setup or in the Site Properties for your Configuration Manager site.  

The ports in use for the reporting services point site system role are configured in SQL Server Reporting Services. These ports are then used by Configuration Manager during communications to the reporting services point. Be sure to review these ports defining the IP filter information for IPsec policies or for configuring firewalls.  

##  <a name="BKMK_NonConfigurablePorts"></a> Non-configurable ports  
Configuration Manager does not allow you to configure ports for the following types of communication:  

-   Site to site  

-   Site server to site system  

-   Configuration Manager console to SMS Provider  

-   Configuration Manager console to the Internet  

-   Connections to cloud services, such as Microsoft Intune and cloud-based distribution points  

##  <a name="BKMK_CommunicationPorts"></a> Ports used by Configuration Manager clients and site systems  
The following sections detail the ports used for communication in Configuration Manager. The arrows in the section title, between the computers, represent the direction of the communication:  

-   -- > indicates one computer initiates communication and the other computer always responds  

-   &lt; -- > indicates that either computer can initiate communication  

###  <a name="BKMK_PortsAI"></a> Asset Intelligence Synchronization Point -- > Microsoft  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a> Asset Intelligence Synchronization Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a> Application Catalog Web Service Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Application Catalog Website Point -- > Application Catalog Web Service Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client -- > Application Catalog Website Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Client -- > Client  
 In addition to the ports listed in the following table, wake-up proxy also uses Internet Control Message Protocol (ICMP) echo request messages from one client to another client when they are configured for wake-up proxy. This communication is used to confirm whether the other client computer is awake on the network. ICMP is sometimes referred to as TCP/IP ping commands. ICMP does not have a UDP or TCP protocol number, and so it is not listed in the following table. However, any host-based firewalls on these client computers or intervening network devices within the subnet must permit ICMP traffic for wake-up proxy communication to succeed.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 (See note 2, **Alternate Port Available**)|--|  
|Wake-up proxy|25536 (See note 2, **Alternate Port Available**)|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> Client -- > Configuration Manager Policy Module (Network Device Enrollment Service)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)||80|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a> Client -- > Cloud-Based Distribution Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a> Client -- > Distribution Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsClient-DP2"></a> Client -- > Distribution Point Configured for Multicast  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Multicast Protocol|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> Client -- > Distribution Point Configured for PXE  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Dynamic Host Configuration Protocol (DHCP)|67 and 68|--|  
|Trivial File Transfer Protocol (TFTP)|69 (See note 4 **Trivial FTP (TFTP) Daemon**)|--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a> Client -- > Fallback Status Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsClient-GCDC"></a> Client -- > Global Catalog Domain Controller  
 A Configuration Manager client does not contact a global catalog server when it is a workgroup computer or when it is configured for Internet-only communication.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Global Catalog LDAP|--|3268|  
|Global Catalog LDAP SSL|--|3269|  

###  <a name="BKMK_PortsClient-MP"></a> Client -- > Management Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Client notification (default communication before falling back to HTTP or HTTPS)|--|10123 (See note 2, **Alternate Port Available**)|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsClient-SUP"></a> Client -- > Software Update Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 or 8530 (See note 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 or 8531 (See note 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsClient-SMP"></a> Client -- > State Migration Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a> Configuration Manager Console -- > Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Remote Control (control)|--|2701|  
|Remote Assistance (RDP and RTC)|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a> Configuration Manager Console -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a> Configuration Manager Console -- > Reporting Services Point  

||||  
|-|-|-|  
|Description|UDP|TCP|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsConsole-Site"></a> Configuration Manager Console -- > Site Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (initial connection to WMI to locate provider system)|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a> Configuration Manager Console -- > SMS Provider  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager Policy Module (Network Device Enrollment Service) -- > Certificate Registration Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsDist_MP"></a> Distribution Point -- > Management Point  
 A distribution point communicates to the management point in the following scenarios:  

-   To report status of prestaged content  

-   To report usage summary data  

-   To report content validation  

-   A pull distribution point reports package download status  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 2, **Alternate Port Available**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection Point -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Enrollment Proxy Point -- > Enrollment Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Enrollment Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server Connector -- > Exchange Online  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management over HTTPS|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server Connector -- > On Premises Exchange Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management over HTTP|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac Computer -- > Enrollment Proxy Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a> Management Point -- > Domain Controller  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|--|389|  
|LDAP (Secure Sockets Layer [SSL] connection)|636|636|  
|Global Catalog LDAP|--|3268|  
|Global Catalog LDAP SSL|--|3269|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsMP-Site"></a> Management Point &lt; -- > Site Server  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Endpoint mapper|--|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a> Management Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobile Device -- > Enrollment Proxy Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Mobile Device -- > Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a> Reporting Services Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, Alternate Port Available)|  

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Site Server &lt; -- > Application Catalog Web Service Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Site Server &lt; -- > Application Catalog Website Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-AISP"></a> Site Server &lt; -- > Asset Intelligence Synchronization Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-Client"></a> Site Server -- > Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 (See note 2, **Alternate Port Available**)|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a> Site Server -- > Cloud-Based Distribution Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a> Site Server -- > Distribution Point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-DC"></a> Site Server -- > Domain Controller  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|--|389|  
|LDAP (Secure Sockets Layer [SSL] connection)|636|636|  
|Global Catalog LDAP|--|3268|  
|Global Catalog LDAP SSL|--|3269|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Site Server &lt; -- > Certificate Registration Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> Site Server &lt; -- > Endpoint Protection Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> Site Server &lt; -- > Enrollment Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Site Server &lt; -- > Enrollment Proxy Point  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-FSP"></a> Site Server &lt; -- > Fallback Status Point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortSite-Internet"></a> Site Server -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 1, **Proxy Server port**)|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> Site Server &lt; -- > Issuing Certification Authority (CA)  
 This communication is used when you deploy certificate profiles by using the certificate registration point. The communication is not used for every site server in the hierarchy; it is used only for the site server at the top of the hierarchy.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Endpoint Mapper|135|135|  
|RPC (DCOM)|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-RSP"></a> Site Server &lt; -- > Reporting Services Point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-Site"></a> Site Server &lt; -- > Site Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a> Site Server -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

 During the installation of a site that will use a remote SQL Server to host the site database, you must open the following ports between the site server and the SQL Server:  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-Provider"></a> Site Server -- > SMS Provider  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  
|RPC|--|DYNAMIC (See note 6, **Dynamic ports**)|  

###  <a name="BKMK_PortsSite-SUP"></a> Site Server &lt; -- > Software Update Point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Hypertext Transfer Protocol (HTTP)|--|80 or 8530 (See note 3, Windows Server Update Services)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 or 8531 (See note 3, Windows Server Update Services)|  

###  <a name="BKMK_PortsSite-SMP"></a> Site Server &lt; -- > State Migration Point  
 (See note 5, **Communication between the site server and site systems**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC Endpoint Mapper|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> SMS Provider -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, Alternate Port Available)|  

###  <a name="BKMK_PortsSUP-Internet"></a> Software Update Point -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (See note 1, **Proxy Server port**)|  

###  <a name="BKMK_PortsSUP-WSUS"></a> Software Update Point -- > Upstream WSUS Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 or 8530 (See note 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 or 8531 (See note 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --> SQL Server  
 Intersite database replication requires the SQL Server at one site to communicate directly with the SQL Server of its parent or child site.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server Service|--|1433 (See note 2, Alternate Port Available)|  
|SQL Server Service Broker|--|4022 (See note 2, Alternate Port Available)|  

> [!TIP]  
>  Configuration Manager does not require the SQL Server Browser, which uses port UDP 1434.  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> State Migration Point -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (See note 2, **Alternate Port Available**)|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Service Connection Point -- > Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="BKMY_PortNotes"></a> Notes for ports used by Configuration Manager clients and site systems  

1.  **Proxy Server port**: This port cannot be configured but can be routed through a configured proxy server.  

2.  **Alternate Port Available**: An alternate port can be defined within Configuration Manager for this value. If a custom port has been defined, substitute that custom port when defining the IP filter information for IPsec policies or for configuring firewalls.  

3.  **Windows Server Update Services**: WSUS can be installed either on the default Web site (port 80) or a custom Web site (port 8530).  

     After installation, the port can be changed. You do not have to use the same port number throughout the site hierarchy.  

    -   If the HTTP port is 80, the HTTPS port must be 443.  

    -   If the HTTP port is anything else, the HTTPS port must be 1 higher. For example, 8530 and 8531.  

    > [!NOTE]  
    >  When you configure the software update point to use HTTPS, the HTTP port must also be open. Unencrypted data, such as the EULA for specific updates, uses the HTTP port.  

4.  **Trivial FTP (TFTP) Daemon**: The Trivial FTP (TFTP) Daemon system service does not require a user name or password and is an integral part of the Windows Deployment Services (WDS). The Trivial FTP Daemon service implements support for the TFTP protocol defined by the following RFCs:  

    -   RFC 350 - TFTP  

    -   RFC 2347 - Option extension  

    -   RFC 2348 - Block size option  

    -   RFC 2349 - Time-out interval, and transfer size options  

     Trivial File Transfer Protocol is designed to support diskless boot environments. TFTP Daemons listen on UDP port 69 but respond from a dynamically allocated high port. Therefore, enabling this port will allow the TFTP service to receive incoming TFTP requests but will not allow the selected server to respond to those requests. Allowing the selected server to respond to inbound TFTP requests cannot be accomplished unless the TFTP server is configured to respond from port 69.  

5.  **Communication between the site server and site systems**: By default, communication between the site server and site systems is bi-directional. The site server initiates communication to configure the site system, and then most site systems connect back to the site server to send status information. Reporting service points and distribution points do not send status information. If you select **Require the site server to initiate connections to this site system** on the site system properties, after the site system is installed, it will not initiate communication to the site server. Instead, the site server initiates the connections and uses the Site System Installation Account for authentication to the site system server.  

6.  **Dynamic ports**: Dynamic ports (also known as ephemeral ports) use a range of port numbers, which is defined by the operating system version. For more information about the default port ranges, see [Service overview and network port requirements for Windows](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="BKMK_AdditionalPorts"></a> Additional lists of ports  
 The following sections provide additional information about ports used by Configuration Manager.  

###  <a name="BKMK_ClientShares"></a> Client to server shares  
 Clients use Server Message Block (SMB) whenever they connect to UNC shares. For example:  

-   Manual client installation that specifies the CCMSetup.exe **/source:** command line property.  

-   Endpoint Protection clients that download definition files from a UNC path.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> Connections to Microsoft SQL Server  
 For communication to the SQL Server database engine and for intersite replication, you can use the default SQL Server port or specify custom ports:  

-   Intersite communications use:  

    -   SQL Server Service Broker, which defaults to port TCP 4022.  

    -   SQL Server Service, which defaults to port TCP 1433  

-   Intrasite communication between the SQL Server database engine and various Configuration Manager site system roles default to port TCP 1433.  

> [!WARNING]  
>  Configuration Manager does not support dynamic ports. Because SQL Server named instances by default use dynamic ports for connections to the database engine, when you use a named instance, you must manually configure the static port that you want to use for intrasite communication.  

 The following site system roles communicate directly with the SQL Server database:  

-   Application Catalog web service point  

-   Certificate registration point role  

-   Enrollment point role  

-   Management point  

-   Site server  

-   Reporting services point  

-   SMS Provider  

-   SQL Server --> SQL Server  

When a SQL Server hosts a database from more than one site, each database must use a separate instance of SQL Server, and each instance must be configured with a unique set of ports.  

If you have a firewall enabled on the SQL Server computer, ensure that it is configured to allow the ports in use by your deployment, and at any locations on the network between computers that communicate with the SQL Server.  

For an example of how to configure SQL Server to use a specific port, see [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) in the SQL Server TechNet library.  

###  <a name="BKMK_External"></a> External connections made by Configuration Manager  
 Configuration Manager clients or site systems can make the following external connections:  

-   [Asset Intelligence Synchronization Point -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Endpoint Protection Point -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Client -- &gt; Global Catalog Domain Controller](#BKMK_PortsClient-GCDC)  

-   [Configuration Manager Console -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Management Point -- &gt; Domain Controller](#BKMK_PortsMP-DC)  

-   [Site Server -- &gt; Domain Controller](#BKMK_PortsSite-DC)  

-   [Site Server &lt; -- &gt; Issuing Certification Authority (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Software Update Point -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Software Update Point -- &gt; Upstream WSUS Server](#BKMK_PortsSUP-WSUS)  

-   [Service Connection Point -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> Installation requirements for site systems that support Internet-based clients  
 Management points and distribution points that support internet-based clients, the software update point, and the fallback status point use the following ports for installation and repair:  

-   Site server --> site system: RPC endpoint mapper using UDP and TCP port 135.  

-   Site server --> site system: RPC dynamic TCP ports.  

-   Site server &lt; --> site system: Server message blocks (SMB) using TCP port 445.  

Application and package installations on distribution points require the following RPC ports:  

-   Site server --> distribution point: RPC endpoint mapper using UDP and TCP port 135.  

-   Site server --> distribution point: RPC dynamic TCP ports  

Use IPsec to help secure the traffic between the site server and site systems. If you must restrict the dynamic ports that are used with RPC, you can use the Microsoft RPC configuration tool (rpccfg.exe) to configure a limited range of ports for these RPC packets. For more information about the RPC configuration tool, see [How to configure RPC to use certain ports and how to help secure those ports by using IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Before you install these site systems, ensure that the remote registry service is running on the site system server and that you have specified a Site System Installation Account if the site system is in a different Active Directory forest without a trust relationship.  

###  <a name="BKMK_PortsClientInstall"></a> Ports used by Configuration Manager client installation  
The ports that are using during client installation depend on the client deployment method. See **Ports Used During Configuration Manager Client Deployment** in the [Windows Firewall and port settings for clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) topic for a list of ports for each client deployment method. For information about how to configure Windows Firewall on the client for client installation and post-installation communication, see [Windows Firewall and port settings for clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="BKMK_MigrationPorts"></a> Ports used by migration  
The site server that runs Migration uses several ports to connect to applicable sites in the source hierarchy to gather data from the source sites SQL Server database, and to share distribution points.  

 For information these ports, see the [Required configurations for migration](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) section in the Prerequisites for [Prerequisites for migration in System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md) topic.  

###  <a name="BKMK_ServerPorts"></a> Ports used by Windows Server  
 The following table lists some of the key ports that Windows Server uses and their respective functions. For a more complete list of Windows Server services and network ports requirements, see [Service overview and network port requirements for the Windows Server system](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Domain Name System (DNS)|53|53|  
|Dynamic Host Configuration Protocol (DHCP)|67 and 68|--|  
|NetBIOS Name Resolution|137|--|  
|NetBIOS Datagram Service|138|--|  
|NetBIOS Session Service|--|139|  
