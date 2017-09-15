---
title: "Client deployment best practices | Microsoft Docs"
description: "Get best practices for client deployment in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: arob98
ms.author: angrobe
manager: angrobe

---
# Best practices for client deployment in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


## Use software update-based client installation for Active Directory computers  
 This client deployment method uses existing Windows technologies, integrates with your Active Directory infrastructure, requires the least configuration in Configuration Manager, is the easiest to configure for firewalls, and is the most secure. By using security groups and WMI filtering for the Group Policy configuration, you also have a lot of flexibility to control which computers install the Configuration Manager client.  

 For more information, see [How to Install Configuration Manager Clients by Using Software Update-Based Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## Extend the Active Directory schema and publish the site so that you can run CCMSetup without command-line options  
 When you extend the Active Directory schema for Configuration Manager and the site is published to Active Directory Domain Services, many client installation properties are published to Active Directory Domain Services. If a computer can locate these client installation properties, it can use them during Configuration Manager client deployment. Because this information is automatically generated, the risk of human error associated with manually entering installation properties is eliminated.  

 For more information, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## Use a phased rollout to manage CPU usage  
 Minimize the effect of the CPU processing requirements on the site server by using a phased rollout of clients. Deploy clients outside business hours so that other services have more available bandwidth during the day and users are not disrupted if their computer slows down or requires a restart.  

## Enable automatic upgrade after your main client deployment has finished  
 [Automatic client upgrades](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) are useful when you want to upgrade a small number of client computers that might have been missed by your main client installation method, perhaps because they were offline. 

> [!NOTE]  
>  Performance improvements in Configuration Manager can allow you to use automatic upgrades as a primary client upgrade method. However, performance will depend on your hierarchy infrastructure, such as the number of clients.  


## Use SMSMP and FSP if you install the client with client.msi properties  
 The SMSMP property specifies the initial management point for the client to communicate with and removes the dependency on service location solutions such as Active Directory Domain Services, DNS, and WINS.  

 Use the FSP property and install a fallback status point so that you can monitor client installation and assignment, and identify any communication problems.  

 For more information about these options, see [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## Install client language packs before you install the clients  
We recommend that you install client language packs before deploying the client. If you install [client language packs](../../../../core/servers/deploy/install/language-packs.md) (to enable additional languages) on a site after you install clients, you must reinstall the clients before they can use those languages. For mobile device clients, you must wipe the mobile device and enroll it again.  

## Prepare required PKI certificates in advance  
 To manage devices on the Internet, enrolled mobile devices, and Mac computers, you must have PKI certificates on site systems (management points and distribution points) and the client devices. On production networks, you might require change management approval to use new certificates, restart site system servers, or users might have to logoff and logon for new group membership. In addition, you might have to allow sufficient time for replication of security permissions and for any new certificate templates.  

 For more information about required PKI certificates, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## Before you install clients, configure any required client settings and maintenance windows  
 Although you can [configure client settings](../../../../core/clients/deploy/configure-client-settings.md) and maintenance windows before or after clients are installed, it's better to configure required settings before you install clients so that they are used as soon as the client is installed. 

 Configure maintenance windows for servers and for Windows Embedded devices to ensure business continuity for critical devices. Maintenance windows will ensure that required software updates and antimalware software do not restart the computer during business hours.  

> [!IMPORTANT]  
>  For Windows 10 computers that you plan to protect with Unified Write Filter (UWF), you must configure the device  for UWF before you install the client. This enables Configuration Manager to install the client with a custom credential provider that locks out low-rights users from logging in to the device during maintenance mode.  

## Plan your user enrollment experience for Mac computers and mobile devices   
 If users will enroll their own Mac computers and mobile devices with Configuration Manager, plan the user experience. For example, you might script the installation and enrollment process by using a web page so users enter the minimum amount of information necessary, and send  instructions with a link by email.  

## Use File-Based Write Filters for Windows Embedded devices 
 Embedded devices that use Enhanced Write Filters (EWF) are likely to experience state message resynchronizations. If you have just a few embedded devices that use Enhanced Write Filters, you might not notice this. However, when you have a lot of embedded devices that resynchronize their information, such as sending full inventory rather than delta inventory, this can generate a noticeable increase in network packets and higher CPU processing on the site server.  

 When you have a choice of which type of write filter to enable, choose File-Based Write Filters and configure exceptions to persist client state and inventory data between device restarts for network and CPU efficiency on the Configuration Manager client. For more information about write filters, see   [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 For more information about the maximum number of Windows Embedded clients that a primary site can support, see [Supported operating sysetms for clients and devices](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
