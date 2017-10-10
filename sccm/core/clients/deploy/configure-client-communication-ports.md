---
title: "Configure client communication ports"
titleSuffix: "Configuration Manager"
description: "Set client communication ports in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to configure client communication ports in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can change the request port numbers that System Center Configuration Manager clients use to communicate with site systems that use HTTP and HTTPS for communication. Although HTTP or HTTPS is more likely to be already configured for firewalls, client notification that uses HTTP or HTTPS requires more CPU usage and memory on the management point computer than if you use a custom port number. You can also specify the site port number to use if you wake up clients by using traditional wake-up packets.  

 When you specify HTTP and HTTPS request ports, you can specify both a default port number and an alternative port number. Clients automatically try the alternative port after communication fails with the default port. You can specify settings for HTTP and HTTPS data communication.  

 The default values for client request ports are **80** for HTTP traffic and **443** for HTTPS traffic. Change them only if you do not want to use these default values. A typical scenario for using custom ports is when you use a custom website in IIS rather than the default website. If you change the default port numbers for the default website in IIS and other applications also use the default website, they are likely to fail.  

> [!IMPORTANT]  
>  Do not change the port numbers in Configuration Manager without understanding the consequences. Examples:  
>   
>  -   If you change the port numbers for the client request services as a site configuration and existing clients are not reconfigured to use the new port numbers, these clients will become unmanaged.  
> -   Before you configure a non-default port number, make sure that firewalls and all intervening network devices can support this configuration and reconfigure them as necessary. If you will manage clients on the Internet and change the default HTTPS port number of 443, routers and firewalls on the Internet might block this communication.  

 To make sure that clients do not become unmanaged after you change the request port numbers, clients must be configured to use the new request port numbers. When you change the request ports on a primary site, any attached secondary sites automatically inherit the same port configuration. Use the procedure in this topic to configure the request ports on the primary site.  

> [!NOTE]  
>  For information about how to configure the request ports for clients on computers that run Linux and UNIX, see [Configure Request Ports for the Client for Linux and UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 When the Configuration Manager site is published to Active Directory Domain Services, new and existing clients that can access this information will automatically be configured with their site port settings and you do not need to take further action. Clients that cannot access this information published to Active Directory Domain Services include workgroup clients, clients from another Active Directory forest, clients that are configured for Internet-only, and clients that are currently on the Internet. If you change the default port numbers after these clients have been installed, reinstall them and install any new clients by using one of the following methods:  

-   Reinstall the clients by using the Client Push Installation Wizard. Client push installation automatically configures clients with the current site port configuration. For more information about how to use the Client Push Installation Wizard, see [How to Install Configuration Manager Clients by Using Client Push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

-   Reinstall the clients by using CCMSetup.exe and the client.msi installation properties of CCMHTTPPORT and CCMHTTPSPORT. For more information about these properties, see  [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   Reinstall the clients by using a method that searches Active Directory Domain Services for Configuration Manager client installation properties. For more information, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 To reconfigure the port numbers for existing clients, you can also use the script PORTSWITCH.VBS that is provided with the installation media in the SMSSETUP\Tools\PortConfiguration folder.  

> [!IMPORTANT]  
>  For existing and new clients that are currently on the Internet, you must configure the non-default port numbers by using the CCMSetup.exe client.msi properties of CCMHTTPPORT and CCMHTTPSPORT.  

 After changing the request ports on the site, new clients that are installed by using the site-wide client push installation method will be automatically configured with the current port numbers for the site.  

#### To configure the client communication port numbers for a site  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, click **Sites**, and select the primary site to configure.  

3.  On the **Home** tab, click **Properties**, and then click the **Ports** tab.  

4.  Select any of the items and click the Properties icon to display the **Port Detail** dialog box.  

5.  In the **Port Detail** dialog box, specify the port number and description for the item, and then click **OK**.  

6.  Select **Use custom web site** if you will use the custom website name of **SMSWeb** for site systems that run IIS.  

7.  Click **OK** to close the properties dialog box for the site.  

 Repeat this procedure for all primary sites in the hierarchy.
