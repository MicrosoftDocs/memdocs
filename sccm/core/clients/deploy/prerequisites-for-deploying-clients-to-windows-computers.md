---
title: "Windows client deployment prerequisites"
description: "Learn the prerequisites for deploying clients to Windows computers in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: 16
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# Prerequisites for deploying clients to Windows computers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Deploying Configuration Manager clients in your environment has the following external dependencies and dependencies within the product. Additionally, each client deployment method has its own dependencies that must be met for client installations to be successful.  

  Make sure that you also review [Supported configurations for System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md) to confirm that devices meet the minimum hardware and operating system requirements for the Configuration Manager client.  

 For information about the prerequisites for the Configuration Manager client for Linux and UNIX, see  [Planning for client deployment to Linux and UNIX computers in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

> [!NOTE]  
>  The software version numbers shown in this article only list the minimum version numbers required.  

##  <a name="BKMK_prereqs_computers"></a> Prerequisites for Computer Clients  
 Use the following information to determine the prerequisites for when you install the Configuration Manager client on computers.  

### Dependencies External to Configuration Manager  

|||  
|-|-|  
|Windows Installer version 3.1.4000.2435|Required to support the use of Windows Installer update (.msp) files for packages and software updates.|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|Install this hotfix on site servers that run Windows Server 2008 R2 when client push installation is enabled.|  
|Microsoft Background Intelligent Transfer Service (BITS) version 2.5|Required to allow throttled data transfers between the client computer and Configuration Manager site systems. BITS is not automatically downloaded during client installation. When BITS is installed on computers, a restart is typically required to complete the installation.<br /><br /> Most operating systems include BITS, but if they do not (for example, Windows Server 2003 R2 SP2), you must install BITS before you install the Configuration Manager client.|  
|Microsoft Task Scheduler|Enable this  service on the client for the client installation to complete.|  

### Dependencies External to Configuration Manager and Automatically Downloaded During Installation  
 The Configuration Manager client has some potential external dependencies. These dependencies depend on the operating system and the installed software on the client computer.  

 If these dependencies are required to complete the installation of the client, they are automatically installed with the client software.  

|||  
|-|-|  
|Windows Update Agent version 7.0.6000.363|Required by Windows to support update detection and deployment.|  
|Microsoft Core XML Services (MSXML) version 6.20.5002 or later|Required to support the processing of XML documents in Windows.|  
|Microsoft Remote Differential Compression (RDC)|Required to optimize data transmission over the network.|  
|Microsoft Visual C++ 2013 Redistributable version 12.0.21005.1|Required to support client operations. When this update is installed on client computers, a restart might be required to complete the installation.|  
|Microsoft Visual C++ 2005 Redistributable version 8.0.50727.42|For version 1606 and earlier, required to support Microsoft SQL Server Compact operations.|  
|Windows Imaging APIs 6.0.6001.18000|Required to allow Configuration Manager to manage Windows image (.wim) files.|  
|Microsoft Policy Platform 1.2.3514.0|Required to allow clients to evaluate compliance settings.|  
|Microsoft Silverlight 5.1.41212.0 (beginning in Configuration Manager version 1602)|Required to support the Application Catalog website user experience.|  
|Microsoft .NET Framework version 4.5.2|Required to support client operations. Automatically installed on the client computer if it does not have Microsoft .NET Framework version 4.5 or later installed. For more information, see [Additional details about Microsoft .NET Framework version 4.5.2](#dotNet).|  
|Microsoft SQL Server Compact 3.5 SP2 components|Required to store information related to client operations.|  
|Microsoft Windows Imaging Components|Required by Microsoft .NET Framework 4.0 for Windows Server 2003 or Windows XP SP2 for 64-bit computers.|
|Microsoft Intune PC software client|You cannot run the Intune PC software client and the Configuration Manager client on the same PC. Ensure the Intune client is removed before you install the Configuration Manager client.|

####  <a name="dotNet"></a> Additional details about Microsoft .NET Framework version 4.5.2  

> [!NOTE]  
>  On January 12th of 2016, support for .NET 4.0, 4.5, and 4.5.1 expired. For more information, see [Microsoft .NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) at support.microsoft.com.  

 A restart may be required to complete the installation of Microsoft .NET Framework version 4.5.2. The user will see **Restart required** notification in the system tray.  Common scenarios that require client computers to be restarted:  

-   .NET applications or services are running on the computer.  

-   One or more software updates required for .NET installation are missing.  

-   The computer is pending a restart from prior installation of .NET framework software updates.  

 After  .NET Framework 4.5.2 is installed, additional updates to it might be installed subsequently, which may require addition computer restarts.  

### Configuration Manager Dependencies  
 For more information about the following site system roles, see [Determine the site system roles for System Center Configuration Manager clients](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)  

|||  
|-|-|  
|Management point|Although a management point is not required to deploy the Configuration Manager client, you must have a management point to transfer information between client computers and Configuration Manager servers. Without a management point, you cannot manage client computers.|  
|Distribution point|The distribution point is an optional, but recommended site system role for client deployment. All distribution points host the client source files, which lets computers find the nearest distribution point from which to download the client source files during client deployment. If the site does not have a distribution point, computers download the client source files from their management point.|  
|Fallback status point|The fallback status point is an optional, but recommended site system role for client deployment. The fallback status point tracks client deployment and enables computers in the Configuration Manager site to send state messages when they cannot communicate with a management point.|  
|Reporting services point|The reporting services point is an optional, but recommended site system role that can display reports related to client deployment and management. For more information, see [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### Installation Method Dependencies  
 The following prerequisites are specific to the various methods of client installation.  

-   Client push installation  

    -   Client push installation accounts are used to connect to computers to install the client and are specified on the **Accounts** tab of the **Client Push Installation Properties** dialog box. The account must be a member of the local administrators group on the destination computer.  

         If you do not specify a client push installation account, the site server computer account will be used.  

    -   The computer on which you are installing the client must have been discovered by at least one Configuration Manager discovery method.  

    -   The computer has an ADMIN$ share.  

    -   **Enable client push installation to assigned resources** must be selected in the **Client Push Installation Properties** dialog box if you want to automatically push the Configuration Manager client to discovered resources.  

    -   The client computer must be able to contact a distribution point or a management point to download the supporting files.  

     You must have the following security permissions to install the Configuration Manager client by using client push:  

    -   To configure the Client Push Installation account: **Modify** and Read permission for the **Site** object.  

    -   To use client push to install the client to collections, devices and queries: **Modify Resource** and **Read** permission for the Collection object.  

     The **Infrastructure Administrator** security role includes the required permissions to manage client push installation.  

-   Software update point-based installation  

    -   If the Active Directory schema has not been extended, or you are installing clients from another forest, installation properties for CCMSetup.exe must be provisioned in the registry of the computer by using Group Policy. For more information, see  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   The Configuration Manager client must be published to the software update point.  

    -   The client computer must be able to contact a distribution point or a management point in order to download supporting files.  

     For the security permissions required to manage Configuration Manager software updates, see [Prerequisites for software updates in System Center Configuration Manager](../../../sum/plan-design/prerequisites-for-software-updates.md).  

-   Group Policy-based installation  

    -   If the Active Directory schema has not been extended, or you are installing clients from another forest, installation properties for CCMSetup.exe must be provisioned in the registry of the computer by using Group Policy. For more information, see  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   The client computer must be able to contact a management point in order to download supporting files.  

-   Logon script-based installation  

     The client computer must be able to contact a distribution point or a management point in order to download supporting files unless, at the command prompt, you specified CCMSetup.exe with the command-line property **ccmsetup /source**.  

-   Manual installation  

     The client computer must be able to contact a distribution point or a management point in order to download supporting files unless, at the command prompt, you specified CCMSetup.exe with the command-line property **ccmsetup /source**.  

-   Workgroup computer installation  

     In order to access resources in the Configuration Manager site server domain, the Network Access Account must be configured for the site.  

     For more information about how to configure the Network Access Account, see the [Fundamental concepts for content management in System Center Configuration Manager](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Software distribution-based installation (for upgrades only)  

    -   If the Active Directory schema has not been extended, or you are installing clients from another forest, installation properties for CCMSetup.exe must be provisioned in the registry of the computer by using Group Policy. For more information, see [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   The client computer must be able to contact a distribution point or a management point to download the supporting files.  

     For the security permissions required to upgrade the Configuration Manager client using application management, see [Security and privacy for application management](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   Automatic client upgrades  

     You must be a member of the **Full Administrator** security role to configure automatic client upgrades.  

### Firewall Requirements  
 If there is a firewall between the site system servers and the computers onto which you want to install the Configuration Manager client, see [Windows Firewall and port settings for clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

##  <a name="BKMK_prereqs_mobiledevices"></a> Prerequisites for Mobile Device Clients  
 Use the following information to determine the prerequisites for when you install the Configuration Manager client on mobile devices and use Configuration Manager to enroll them.  

### Dependencies External to Configuration Manager  

-   A Microsoft enterprise certification authority (CA) with certificate templates to deploy and manage the certificates required for mobile devices.  

     The issuing CA must automatically approve certificate requests from the mobile device users during the enrollment process.  

     For more information about the certificate requirements, see [Security and privacy for certificate profiles in System Center Configuration Manager](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

-   A security group that contains the users that can enroll their mobile devices.  

     This security group is used to configure the certificate template that is used during mobile device enrollment.  

-   Optional but recommended: a DNS alias (CNAME record) named **ConfigMgrEnroll** that is configured for the site system server name on which you will install the enrollment proxy point.  

     This DNS alias is required to support automatic discovery for the enrollment service: If you do not configure this DNS record, users must manually specify the site system server name of the enrollment proxy point as part of the enrollment process.  

-   Site system role dependencies for the computers that will run the enrollment point and the enrollment proxy point site system roles.  

     See  [Supported operating systems for site system servers](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### Configuration Manager Dependencies  
 For more information about the following site system roles, see [Determine the site system roles for System Center Configuration Manager clients](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

-   Management point that is configured for HTTPS client connections and enabled for mobile devices  

     A management point is always required to install the Configuration Manager client on mobile devices. In addition to the configuration requirements of HTTPS and enabled for mobile devices, the management point must be configured with an Internet FQDN and accept client connections from the Internet.  

-   Enrollment point and enrollment proxy point  

     An enrollment proxy point manages enrollment requests from mobile devices and the enrollment point completes the enrollment process. The enrollment point must be in the same Active Directory forest as the site server, but the enrollment proxy point can be in another forest.  

-   Client settings for mobile device enrollment  

     Configure client settings to allow users to enroll mobile devices and configure at least one enrollment profile.  

-   Reporting services point  

     The reporting services point is an optional, but recommended site system role that can display reports related to mobile device enrollment and client management.  

     For more information, see [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   To configure enrollment for mobile devices, you must have the following security permissions:  

    -   To add, modify, and delete the enrollment site system roles: **Modify** permission for the **Site** object.  

    -   To configure client settings for enrollment: Default client settings require **Modify** permission for the **Site** object, and custom client settings require **Client agent**  permissions.  

     The **Full Administrator** security role includes the required permissions to configure the enrollment site system roles.  

     To manage enrolled mobile devices, you must have the following security permissions:  

    -   To wipe or retire a mobile device: **Delete resource** for the **Collection** object.  

    -   To cancel a wipe or retire command: **Delete resource** for the **Collection** object.  

    -   To allow and block mobile devices: **Modify resource** for the **Collection** object.  

    -   To remote lock, or reset the passcode on a mobile device: **Modify** resource for the **Collection** object.  

     The **Operations Administrator** security role includes the required permissions to manage mobile devices.  

     For more information about how to configure security permissions, see [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) and  [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### Firewall Requirements  
 Intervening network devices such as routers and firewalls, and Windows Firewall if applicable, must allow the traffic associated with mobile device enrollment:  

-   Between mobile devices and the enrollment proxy point: HTTPS (by default, TCP 443)  

-   Between the enrollment proxy point and the enrollment point: HTTPS (by default, TCP 443)  

 If you use a proxy web server, it must be configured for SSL tunneling; SSL bridging is not supported for mobile devices.  
