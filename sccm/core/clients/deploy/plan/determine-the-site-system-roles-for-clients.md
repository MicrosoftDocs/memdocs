---
title: "Site system roles for clients | Microsoft Docs"
description: "Determine site system roles for clients in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: 9
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# Determine the site system roles for System Center Configuration Manager clients

*Applies to: System Center Configuration Manager (Current Branch)*

This topic can help you determine the site system roles that you need to deploy Configuration Manager clients:  

 For more information about where to install required site system roles in the hierarchy, see [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 For more information about how to install and configure the site system roles that you require, see [Install site system roles](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  Determine if you need a management point  
 By default, all Windows client computers use a distribution point to install the Configuration Manager client and can fall back to a management point when a distribution point is unavailable. However, you can install Windows clients on computers from an alternative source when you use the CCMSetup command-line property **/source:<Path\>**. For example, you might do this if you install clients on the Internet. Another scenario is when you want to avoid sending network packets between the computer and the management point during client installation, perhaps because a firewall blocks the required ports or because you have a low-bandwidth connection. However, all clients must communicate with a management point to assign to a site and to be managed by Configuration Manager.  

 For more information about the CCMSetup command-line property **/source:<Path\>**, see [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 When you install more than one management point in the hierarchy, clients automatically connect to one point based on their forest membership and network location. You cannot install more than one management point in a secondary site.  

 Mac computer clients and mobile device clients that you enroll with Configuration Manager always require a management point for client installation. This management point must be in a primary site, must be configured to support mobile devices, and must accept client connections from the Internet. These clients cannot use management points in secondary sites or connect to management points in other primary sites.  

##  Determine if you need a fallback status point  
 You can use a fallback status point to monitor client deployment for Windows computers. You can also identify the Windows computer clients that are unmanaged because they cannot communicate with a management point. Mac computers, mobile devices that are enrolled by Configuration Manager, and mobile devices that are managed by using the Exchange Server connector do not use a fallback status point.  

 A fallback status point is not required to monitor client activity and client health.  

 The fallback status point always communicates with clients over HTTP, which uses unauthenticated connections and sends data in clear text. This makes the fallback status point vulnerable to attack, particularly when it is used with Internet-based client management. To help reduce the attack surface, always dedicate a server to running the fallback status point and do not install other site system roles on the same server in a production environment.  

 Install a fallback status point if all the following apply:  

-   You want client communication errors from Windows computers to be sent to the site, even if these client computers cannot communicate with a management point.  

-   You want to use the Configuration Manager client deployment reports, which display the data that is sent by the fallback status point.  

-   You have a dedicated server for this site system role and have additional security measures to help protect the server from attack.  

-   The benefits of using a fallback status point outweigh any security risks associated with unauthenticated connections and clear text transfers over HTTP traffic.  

 Do not install a fallback status point if the security risks of running a website with unauthenticated connections and clear text transfers outweigh the benefits of identifying client communication problems.  

##  Determine whether you need a reporting services point  
 Configuration Manager provides many reports to help you monitor the installation, assignment, and management of clients in the Configuration Manager console. Some of the client deployment reports require that clients are assigned to a fallback status point.  

 Although the reports are not needed to deploy clients and you can see some deployment information in the Configuration Manager console or use the client log files for detailed information, the client reports provide valuable information to help monitor and troubleshoot client deployment.  

##  Determine if you need an enrollment point and an enrollment proxy point  
 Configuration Manager requires the enrollment point and the enrollment proxy point to enroll mobile devices and to enroll certificates for Mac computers. These site system roles are not needed if you will manage mobile devices by using the Exchange Server connector, or if you install the mobile device legacy client (for example, for Windows CE), or if you request and install the client certificate on Mac computers independently from Configuration Manager.  

##  Determine if you need a distribution point  
 You don't need a distribution point to install Configuration Manager clients on Windows computers. However, by default, Configuration Manager uses a distribution point to install the client source files on Windows computers but can fall back to downloading these files from a management point. Distribution points are not used to install mobile device clients that are enrolled by Configuration Manager but are used if you install the mobile device legacy client. If you install the Configuration Manager client as part of an operating system deployment, the operating system image is stored and retrieved from a distribution point.  

 Although you might not need distribution points to install most Configuration Manager clients, you will need them to install software such as applications and software updates on the clients.  

##  Determine if you need an application catalog website point and an application catalog Web services point  
 The application catalog website point and the application catalog Web service point are not needed for client deployment. However, you might want to install them as part of your client deployment process, so that users can perform the following actions as soon as the Configuration Manager client is installed on Windows computers:  

-   Wipe their mobile devices.  

-   Search for and install applications from the Application Catalog.  

-   Deploy applications to users and devices with a deployment purpose of **Available**.  

##  Determine Whether You Require a Cloud Management Gateway Connector point 

You need a cloud management gateway connector point if you are setting up a [cloud management gateway](/sccm/core/clients/manage/setup-cloud-management-gateway) to [manage clients on the Internet](/sccm/core/clients/manage/manage-clients-internet).


 