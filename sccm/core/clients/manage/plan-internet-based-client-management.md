---
title: "Internet-based client management | Microsoft Docs"
description: "Create a plan to manage Internet-based clients in System Center Configuration Manager."
ms.custom: na
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe

---
# Plan for Internet-based client management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Internet-based client management (sometimes referred to as IBCM) lets you manage System Center Configuration Manager clients when they are not connected to your company network but have a standard Internet connection. This arrangement has several advantages that include the reduced costs of not having to run virtual private networks (VPNs) and being able to deploy software updates in a timelier manner.  

 Because of the higher security requirements of managing client computers on a public network, Internet-based client management requires that clients and the site system servers that the clients connect to use PKI certificates. This ensures that connections are authenticated by an independent authority, and that data to and from these site systems are encrypted by using Secure Sockets Layer (SSL).  

 Use the following sections to help you plan for Internet-based client management.  

##  Features that Are Not Supported on the Internet  
 Not all client management functionality is appropriate for the Internet; therefore they are not supported when clients are managed on the Internet. The features that are not supported for Internet management typically rely on Active Directory Domain Services or are not appropriate for a public network, such as network discovery and Wake-on-LAN (WOL).  

 The following features are not supported when clients are managed on the Internet:  

-   Client deployment over the Internet, such as client push and software update-based client deployment. Instead, use manual client installation.  

-   Automatic site assignment.  

-   Wake-on-LAN.  

-   Operating system deployment. However, you can deploy task sequences that do not deploy an operating system; for example, task sequences that run scripts and maintenance tasks on clients.  

-   Remote control.  

-   Software deployment to users unless the Internet-based management point can authenticate the user in Active Directory Domain Services by using Windows authentication (Kerberos or NTLM). This is possible when the Internet-based management point trusts the forest where the user account resides.  

 Additionally, Internet-based client management does not support roaming. Roaming enables clients to always find the closest distribution points to download content. Clients that are managed on the Internet communicate with site systems from their assigned site when these site systems are configured to use an Internet FQDN and the site system roles allow client connections from the Internet. Clients non-deterministically select one of the Internet-based site systems, regardless of bandwidth or physical location.  

 When you have a software update point that is configured to accept connections from the Internet, Configuration Manager Internet-based clients on the Internet always scan against this software update point, to determine which software updates are required. However, when these clients are on the Internet, they first try to download the software updates from Microsoft Update, rather than from an Internet-based distribution point. Only if this fails, will they then try to download the required software updates from an Internet-based distribution point. Clients that are not configured for Internet-based client management never try to download the software updates from Microsoft Update, but always use Configuration Manager distribution points.  

##  Considerations for client communications from the Internet or untrusted forest  
 The following site system roles installed at primary sites support connections from clients that are in untrusted locations, like the Internet or an untrusted forest (secondary sites do not support client connections from untrusted locations):  

-   Application Catalog website point  

-   Configuration Manager Policy Module  

-   Distribution point (HTTPS is required by cloud-based distribution points)  

-   Enrollment proxy point  

-   Fallback status point  

-   Management point  

-   Software update point  

 **About internet facing site systems:**   
Although there is no requirement to have a trust between a client's forest and that of the site system server, when the forest that contains an Internet facing site system trusts the forest that contains the user accounts, this configuration supports user-based policies for devices on the Internet when you enable the **Client Policy** client setting **Enable user policy requests from Internet clients**.  

 For example, the following configurations illustrate when Internet-based client management supports user policies for devices on the Internet:  

-   The Internet-based management point is in the perimeter network where a read-only domain controller resides to authenticate the user and an intervening firewall allows Active Directory packets.  

-   The user account is in Forest A (the intranet) and the Internet-based management point is in Forest B (the perimeter network). Forest B trusts Forest A, and an intervening firewall allows the authentication packets.  

-   The user account and the Internet-based management point are in Forest A (the intranet). The management point is published to the Internet by using a web proxy server (like Forefront Threat Management Gateway).  

> [!NOTE]  
>  If Kerberos authentication fails, NTLM authentication is then automatically tried.  

 As the previous example shows, you can place Internet-based site systems in the intranet when they are published to the Internet by using a web proxy server, such as ISA Server and Forefront Threat Management Gateway. These site systems can be configured for client connection from the Internet only, or client connections from the Internet and intranet. When you use a web proxy server, you can configure it for Secure Sockets Layer (SSL) bridging to SSL (more secure) or SSL tunneling:  

-   **SSL bridging to SSL:**   
    The recommended configuration when you use proxy web servers for Internet-based client management is SSL bridging to SSL, which uses SSL termination with authentication. Client computers must be authenticated by using computer authentication, and mobile device legacy clients are authenticated by using user authentication. Mobile devices that are enrolled by Configuration Manager do not support SSL bridging.  

     The benefit of SSL termination at the proxy web server is that packets from the Internet are subject to inspection before they are forwarded to the internal network. The proxy web server authenticates the connection from the client, terminates it, and then opens a new authenticated connection to the Internet-based site systems. When Configuration Manager clients use a proxy web server, the client identity (client GUID) is securely contained in the packet payload so that the management point does not consider the proxy web server to be the client. Bridging is not supported in Configuration Manager with HTTP to HTTPS, or from HTTPS to HTTP.  

-   **Tunneling**:   
    If your proxy web server cannot support the requirements for SSL bridging, or you want to configure Internet support for mobile devices that are enrolled by Configuration Manager, SSL tunneling is also supported. It is a less secure option because the SSL packets from the Internet are forwarded to the site systems without SSL termination, so they cannot be inspected for malicious content. When you use SSL tunneling, there are no certificate requirements for the proxy web server.  

##  Planning for Internet-Based Clients  
 You must decide whether the client computers that will be managed over the Internet will be configured for management on the intranet and the Internet, or for Internet-only client management. You can only configure the client management option during the installation of a client computer. If you change your mind later, you must reinstall the client.  

> [!NOTE]  
>  If you configure an Internet capable management point, clients that connect to the management point will become Internet-capable when they next refresh their list of available management points.  

> [!TIP]  
>  You do not have to restrict the configuration of Internet-only client management to the Internet and you can also use it on the intranet.  

 Clients that are configured for Internet-only client management only communicate with the site systems that are configured for client connections from the Internet. This configuration would be appropriate for computers that you know never connect to your company intranet, for example, point of sale computers in remote locations. It might also be appropriate when you want to restrict client communication to HTTPS only (for example, to support firewall and restricted security policies), and when you install Internet-based site systems in a perimeter network and you want to manage these servers by using the Configuration Manager client.  

 When you want to manage workgroup clients on the Internet, you must install them as Internet-only.  

> [!NOTE]  
>  Mobile device clients are automatically configured as Internet-only when they are configured to use an Internet-based management point.  

 Other client computers can be configured for Internet and intranet client management. They can automatically switch between Internet-based client management and intranet client management when they detect a change of network. If these clients can find and connect to a management point that is configured for client connections on the intranet, these clients are managed as intranet clients that have full Configuration Manager management functionality. If the clients cannot find or connect to a management point that is configured for client connections on the intranet, they attempt to connect to an Internet-based management point, and if this is successful, these clients are then managed by the Internet-based site systems in their assigned site.  

 The benefit in automatic switching between Internet-based client management and intranet client management is that client computers can automatically use all Configuration Manager features whenever they are connected to the intranet and continue to be managed for essential management functions when they are on the Internet. Additionally, a download that began on the Internet can seamlessly resume on the intranet, and vice versa.  

##  Prerequisites for Internet-Based Client Management  
 Internet-based client management in Configuration Manager has the following external dependencies:  

-   Clients that will be managed on the Internet must have an Internet connection.  

     Configuration Manager uses existing Internet Service Provider (ISP) connections to the Internet, which can be either permanent or temporary connections. Client mobile devices must have a direct Internet connection, but client computers can have either a direct Internet connection or connect by using a proxy web server.  

-   Site systems that support Internet-based client management must have connectivity to the Internet and must be in an Active Directory domain.  

     The Internet-based site systems do not require a trust relationship with the Active Directory forest of the site server. However, when the Internet-based management point can authenticate the user by using Windows authentication, user policies are supported. If Windows authentication fails, only computer policies are supported.  

    > [!NOTE]  
    >  To support user policies, you also must set to **True** the two **Client Policy** client settings:  
    >   
    >  -   **Enable user policy polling on clients**  
    > -   **Enable user policy requests from Internet clients**  

     An Internet-based Application Catalog website point also requires Windows authentication to authenticate users when their computer is on the Internet. This requirement is independent from user policies.  

-   You must have a supporting public key infrastructure (PKI) that can deploy and manage the certificates that the clients require and that are managed on the Internet and the Internet-based site system servers.  

     For more information about the PKI certificates, see [PKI certificate requirements for System Center Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

-   The Internet fully qualified domain name (FQDN) of site systems that support Internet-based client management must be registered as host entries on public DNS servers.  

-   Intervening firewalls or proxy servers must allow the client communication that is associated with Internet-based site systems.  

     Client communication requirements:  

    -   Support HTTP 1.1  

    -   Allow HTTP content type of multipart MIME attachment (multipart/mixed and application/octet-stream)  

    -   Allow the following verbs for the Internet-based management point:  

        -   HEAD  

        -   CCM_POST  

        -   BITS_POST  

        -   GET  

        -   PROPFIND  

    -   Allow the following verbs for the Internet-based distribution point:  

        -   HEAD  

        -   GET  

        -   PROPFIND  

    -   Allow the following verbs for the Internet-based fallback status point:  

        -   POST  

    -   Allow the following verbs for the Internet-based Application Catalog website point:  

        -   POST  

        -   GET  

    -   Allow the following HTTP headers for the Internet-based management point:  

        -   Range:  

        -   CCMClientID:  

        -   CCMClientIDSignature:  

        -   CCMClientTimestamp:  

        -   CCMClientTimestampsSignature:  

    -   Allow the following HTTP header for the Internet-based distribution point:  

        -   Range:  

     For configuration information to support these requirements, refer to your firewall or proxy server documentation.  

     For similar communication requirements when you use the software update point for client connections from the Internet, see the documentation for Windows Server Update Services (WSUS). For example, for WSUS on Windows Server 2003, see [Appendix D: Security Settings](http://go.microsoft.com/fwlink/p/?LinkId=143368), the deployment appendix for security settings.
