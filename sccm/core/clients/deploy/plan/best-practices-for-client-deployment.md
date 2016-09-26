---
title: "Client deployment best practices | System Center Configuration Manager"
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: Mtillman

---
# Best practices for client deployment in System Center Configuration Manager
Use the following best practices information to help you deploy clients on computers in System Center Configuration Manager.  

## Use software update-based client installation for Active Directory computers  
 This client deployment method has the benefit of using existing Windows technologies, integrates with your Active Directory infrastructure, requires the least configuration in Configuration Manager, is the easiest to configure for firewalls, and is the most secure. By using security groups and WMI filtering for the Group Policy configuration, you also have a lot of flexibility to control which computers install the Configuration Manager client.  

 For more information, see [How to Install Configuration Manager Clients by Using Software Update-Based Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## Extend the Active Directory schema and publish the site so that you can run CCMSetup without command-line options  
 When you extend the Active Directory schema for Configuration Manager and the site is published to Active Directory Domain Services, many client installation properties are published to Active Directory Domain Services. If a computer can locate these client installation properties, it can use them during Configuration Manager client deployment. Because this information is automatically generated, the risk of human error associated with manually entering installation properties is eliminated.  

 For more information, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## When you have many clients to deploy, plan a phased rollout outside business hours  
 Minimize the effect of the CPU processing requirements on the site server by planning a phased rollout of clients over a period of time. Deploy clients outside business hours so that critical business services have more available bandwidth during the day and users are not disrupted if their computer slows down or requires a restart to complete the installation.  

## Enable automatic upgrade after your main client deployment has finished  
 Automatic client upgrades are useful when you want to upgrade a small number of client computers that might have been missed by your main client installation method. For example, you have completed an initial client upgrade, but some clients were offline during the upgrade deployment. You then use this method to upgrade the client on these computers when they are next active.  

> [!NOTE]  
>  Performance improvements in Configuration Manager can allow you to use automatic upgrades as a primary client upgrade method. However, performance will depend on your hierarchy infrastructure, such as the number of clients.  

 For more information about automatic client upgrade method, see [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## Use SMSMP and FSP if you install the client with client.msi properties  
 The SMSMP property specifies the initial management point for the client to communicate with and removes the dependency on service location solutions such as Active Directory Domain Services, DNS, and WINS.  

 Use the FSP property and install a fallback status point so that you can monitor client installation and assignment, and identify any communication problems.  

 For more information about these options, see [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## If you want to use client languages other than English, install the client language packs before you install the clients  
 If you install client language packs on a site after you install clients, you must reinstall the clients before they can use the additional languages. For mobile device clients, this means you must wipe the mobile device and enroll it again.  

 For more information about how to add support for additional client languages, see [Language Packs in System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

## Plan and prepare any required PKI certificates in advance  
 To manage devices on the Internet, enrolled mobile devices, and Mac computers, you must have PKI certificates on site systems (management points and distribution points) and the client devices. For many customers, this requires advanced planning and preparation, especially if you have a separate team who manages your PKI. On production networks, you might require change management approval to use new certificates, restart site system servers, or users might have to logoff and logon for new group membership. In addition, you might have to allow sufficient time for replication of security permissions and for any new certificate templates.  

 For more information about the PKI certificates that are required, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## Before you install clients, configure any required client settings and maintenance windows  
 Although you can configure client settings and maintenance windows before or after clients are installed, configure any required settings before you install clients so that these settings are used as soon as the client is installed. For more information, see [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)  

 Configure maintenance windows for servers and for Windows Embedded devices to ensure business continuity for these often business-critical computers. For example, maintenance windows will ensure that required software updates and antimalware software do not restart the computer during business hours.  

> [!IMPORTANT]  
>  For Windows 10 computers that you plan to protect with Unified Write Filter (UWF), you must configure the device  for UWF before you install the client. This enables Configuration Manager to install the client with a custom credential provider that locks out low rights users from logging in to the device during maintenance mode.  

## For Mac computers and mobile devices that are enrolled by Configuration Manager, plan your user enrollment experience  
 If users will enroll their own Mac computers and mobile devices by using Configuration Manager, plan and prepare the user experience. For example, you might script the installation and enrollment process by using a web page so users enter the minimum amount of information necessary, and you send them instructions with a link by email.  

## When you manage Windows Embedded devices, use File-Based Write Filters (FBWF) rather than Enhanced Write Filters (EWF) for higher scalability  
 Embedded devices that use Enhanced Write Filters (EWF) are likely to experience state message resynchronizations. If you have just a few embedded devices that use Enhanced Write Filters, you might not notice this. However, when you have a lot of embedded devices that resynchronize their information, such as sending full inventory rather than delta inventory, this can generate a noticeable increase in network packets and higher CPU processing on the site server.  

 When you have a choice of which type of write filter to enable, choose File-Based Write Filters and configure exceptions to persist client state and inventory data between device restarts for network and CPU efficiency on the Configuration Manager client. For more information about write filters, see   [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 For more information about the maximum number of Windows Embedded clients that a primary site can support, see [Supported operating sysetms for clients and devices](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  

