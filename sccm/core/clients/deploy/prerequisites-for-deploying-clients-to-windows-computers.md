---
title: Windows client deployment prerequisites
titleSuffix: Configuration Manager
description: Learn about the prerequisites for deploying the Configuration Manager client to Windows computers.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Prerequisites for deploying clients to Windows computers in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Deploying Configuration Manager clients in your environment has the following external dependencies and dependencies within the product. Additionally, each client deployment method has its own dependencies that must be met for client installations to be successful.  

For more information on the minimum hardware and OS requirements for the Configuration Manager client, see [Supported configurations](/sccm/core/plan-design/configs/supported-configurations).  

> [!NOTE]  
>  The software version numbers shown in this article only list the minimum version numbers required.  



##  <a name="BKMK_prereqs_computers"></a> Prerequisites for Windows clients  

Use the following information to determine the prerequisites for when you install the Configuration Manager client on Windows devices.  

### Dependencies external to Configuration Manager  

|Component|Description|  
|---|---|  
|Windows Installer version 3.1.4000.2435|Required to support the use of Windows Installer update (.msp) files for packages and software updates.|  
|Microsoft Background Intelligent Transfer Service (BITS) version 2.5|Required to allow throttled data transfers between the client computer and Configuration Manager site systems. BITS isn't automatically downloaded during client installation. When BITS is installed on computers, it typically requires a restart to complete the installation.<br /><br /> Most operating systems include BITS. If they don't, install BITS before you install the Configuration Manager client.|  
|Microsoft Task Scheduler|Enable this service on the client for the client installation to complete.|  


### <a name="bkmk_ExternalDependencies"></a> Dependencies external to Configuration Manager and automatically downloaded during installation  

The Configuration Manager client has external dependencies. These dependencies depend on the OS version and the installed software on the client computer.  

If the client requires these dependencies to complete the installation, it automatically installs them.  

|Component|Description|  
|---|---|  
|Windows Update Agent version 7.0.6000.363|Required by Windows to support update detection and deployment.|  
|Microsoft Core XML Services (MSXML) version 6.20.5002 or later|Required to support the processing of XML documents in Windows.|  
|Microsoft Remote Differential Compression (RDC)|Required to optimize data transmission over the network.|  
|Microsoft Visual C++ 2013 Redistributable version 12.0.21005.1|Required to support client operations. When you install this update on client computers, it might require a restart to complete the installation.|  
|Microsoft Visual C++ 2005 Redistributable version 8.0.50727.42|For version 1606 and earlier, required to support Microsoft SQL Server Compact operations.|  
|Windows Imaging APIs 6.0.6001.18000|Required to allow Configuration Manager to manage Windows image (.wim) files.|  
|Microsoft Policy Platform 1.2.3514.0|Required to allow clients to evaluate compliance settings.|  
|Microsoft Silverlight 5.1.41212.0|Required to support the Application Catalog website user experience. Starting in Configuration Manager 1802, the client doesn't automatically install Silverlight. The primary functionality of the Application Catalog is now included in Software Center. Support for the Application Catalog website ends in version 1806.<!--1356195-->|  
|Microsoft .NET Framework version 4.5.2|Required to support client operations. Automatically installed on the client computer if it doesn't have Microsoft .NET Framework version 4.5 or later installed. For more information, see [Additional details about Microsoft .NET Framework version 4.5.2](#dotNet).|  
|Microsoft SQL Server Compact 4.0 components|Required to store information related to client operations.|  


####  <a name="dotNet"></a> Additional details about Microsoft .NET Framework version 4.5.2  

> [!NOTE]  
>  .NET 4.0, 4.5, and 4.5.1 are no longer supported. For more information, see [Microsoft .NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Microsoft .NET Framework version 4.5.2 may require a restart to complete the installation. The user sees a **Restart required** notification in the system tray. The following common scenarios require client computers to restart:  

-   .NET applications or services are running on the computer.  

-   One or more software updates required for .NET installation are missing.  

-   The computer is pending a restart from prior installation of .NET framework software updates.  


After .NET Framework 4.5.2 is installed, it may require additional updates. These later updates may require additional computer restarts.  


### Configuration Manager dependencies  

For more information, see [Determine the site system roles for clients](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

|Component|Description|  
|---|---|  
|Management point|To deploy the Configuration Manager client, you don't require a management point. Clients require a management point to transfer information with the site. Without a management point, you can't manage client computers.|  
|Distribution point|The distribution point is an optional, but recommended site system role for client deployment and management. All distribution points host the client source files. Clients find the nearest distribution point from which to download the source files during client deployment or update. If the site doesn't have a distribution point, computers download the client source files from their management point.|  
|Fallback status point|The fallback status point is an optional, but recommended site system role for client deployment. The fallback status point tracks client deployment and enables computers in the Configuration Manager site to send state messages when they can't communicate with a management point.|  
|Reporting services point|The reporting services point is an optional, but recommended site system role. It displays reports related to client deployment and management. For more information, see [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).|  


### Installation method dependencies  

The following prerequisites are specific to the various methods of client installation.  

#### Client push installation  

   -   The site uses client push installation accounts to connect to computers to install the client. Specify these accounts on the **Accounts** tab of the Client Push Installation Properties. The account must be a member of the local administrators group on the destination computer.  

         If you don't specify a client push installation account, the site server uses its computer account.  

   -   The site needs to discover the computer on which you're installing the client. At least one Configuration Manager discovery method is needed.  

   -   The computer has an ADMIN$ share.  

   -   To automatically push the Configuration Manager client to discovered resources, select the option to **Enable client push installation to assigned resources** in the Client Push Installation Properties.  

   -   The client computer needs to communicate with a distribution point or a management point to download the source files.  

   -   Starting in version 1806, when you require Kerberos mutual authentication, clients must be in a trusted Active Directory forest. Kerberos in Windows relies upon Active Directory for mutual authentication.<!--1358204-->  


To use client push, you need the following security permissions:  

   -   To configure the client push installation account: **Modify** and **Read** permission for the **Site** object.  

   -   To use client push to install the client to collections, devices and queries: **Modify Resource** and **Read** permission for the **Collection** object.  


The **Infrastructure Administrator** default security role includes the required permissions to manage client push installations.  


#### Software update point-based installation  

   -   If you haven't extended the Active Directory schema, or you're installing clients from another forest, use group policy to provision installation parameters for CCMSetup.exe. For more information, see [How to provision client installation properties](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Publish the Configuration Manager client to the software update point.  

   -   To download the source files, the client computer needs to communicate with a distribution point or a management point.  


For the security permissions required to manage Configuration Manager software updates, see [Prerequisites for software updates](/sccm/sum/plan-design/prerequisites-for-software-updates).  


#### Group policy-based installation  

   -   If you haven't extended the Active Directory schema, or you're installing clients from another forest, use group policy to provision installation parameters for CCMSetup.exe. For more information, see [How to provision client installation properties](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   To download the source files, the client computer needs to communicate with a distribution point or a management point.  


#### Logon script-based installation  

To download the source files, the client computer needs to communicate with a distribution point or a management point. Unless you specified CCMSetup.exe with the following command-line parameter: `ccmsetup /source`  


#### Manual installation  

To download the source files, the client computer needs to communicate with a distribution point or a management point. Unless you specified CCMSetup.exe with the following command-line parameter: `ccmsetup /source`  


#### Microsoft Intune MDM installation

 - Requires a Microsoft Intune subscription and appropriate licenses.  

 - Requires the device has internet access, even if it isn't internet-based.  

 - Depending upon the use case, you may also require one or both of the following technologies:  

     - Azure Active Directory  

     - Cloud management gateway  


#### Workgroup computer installation  

To access resources in the Configuration Manager site server's domain, configure a network access account for the site.  

For more information about how to configure the network access account, see the [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  


#### Software distribution-based installation (for upgrades only)  

   -   If you haven't extended the Active Directory schema, or you're installing clients from another forest, use group policy to provision installation parameters for CCMSetup.exe. For more information, see [How to provision client installation properties](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).   

   -   To download the source files, the client computer needs to communicate with a distribution point or a management point.  


For the security permissions required to upgrade the Configuration Manager client using application management, see [Security and privacy for application management](/sccm/apps/plan-design/security-and-privacy-for-application-management).  


#### Automatic client upgrades  

You must be a member of the **Full Administrator** security role to configure automatic client upgrades.  


### Firewall requirements  

If there's a firewall between the site system servers and the computers onto which you want to install the Configuration Manager client, see [Windows Firewall and port settings for clients](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Prerequisites for mobile device clients  

When you install the Configuration Manager client on mobile devices and enroll them, use this information to determine the prerequisites.  

### Dependencies external to Configuration Manager  

-   A Microsoft enterprise certification authority (CA) with certificate templates to deploy and manage the certificates required for mobile devices.  

     The issuing CA must automatically approve certificate requests from the mobile device users during the enrollment process.  

     For more information about the certificate requirements, see [Security and privacy for certificate profiles](/sccm/protect/plan-design/security-and-privacy-for-certificate-profiles).  

-   A security group that contains the users that can enroll their mobile devices.  

     This security group is used to configure the certificate template that is used during mobile device enrollment.  

-   Optional but recommended: a DNS alias (CNAME record) named **ConfigMgrEnroll**. Configure this alias for the server name of the enrollment proxy point.  

     This DNS alias is required to support automatic discovery for the enrollment service. If you don't configure this DNS record, users must manually specify the name of the enrollment proxy point as part of the enrollment process.  

-   Site system role dependencies for the computers that run the enrollment point and the enrollment proxy point site system roles.  

     For more information, see [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  


### Configuration Manager dependencies  

For more information, see [Determine the site system roles for clients](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

-   Management point that's configured for HTTPS client connections and enabled for mobile devices  

     A management point is always required to install the Configuration Manager client on mobile devices. In addition to the configuration requirements of HTTPS and enabled for mobile devices, the management point must be configured with an internet FQDN and accept client connections from the internet.  

-   Enrollment point and enrollment proxy point  

     An enrollment proxy point manages enrollment requests from mobile devices and the enrollment point completes the enrollment process. The enrollment point must be in the same Active Directory forest as the site server, but the enrollment proxy point can be in another forest.  

-   Client settings for mobile device enrollment  

     Configure client settings to allow users to enroll mobile devices and configure at least one enrollment profile.  

-   Reporting services point  

     The reporting services point is an optional, but recommended site system role that can display reports related to mobile device enrollment and client management.  

     For more information, see [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).  

-   To configure enrollment for mobile devices, you must have the following security permissions:  

    -   To add, modify, and delete the enrollment site system roles: **Modify** permission for the **Site** object.  

    -   To configure client settings for enrollment: Default client settings require **Modify** permission for the **Site** object, and custom client settings require **Client agent**  permissions.  

     The **Full Administrator** default security role includes the required permissions to configure the enrollment site system roles.  

     To manage enrolled mobile devices, you must have the following security permissions:  

    -   To wipe or retire a mobile device: **Delete resource** for the **Collection** object.  

    -   To cancel a wipe or retire command: **Delete resource** for the **Collection** object.  

    -   To allow and block mobile devices: **Modify resource** for the **Collection** object.  

    -   To remote lock, or reset the passcode on a mobile device: **Modify** resource for the **Collection** object.  

     The **Operations Administrator** default security role includes the required permissions to manage mobile devices.  

     For more information about how to configure security permissions, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration) and [Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### Firewall requirements  

Intervening network devices such as routers and firewalls, and Windows Firewall if applicable, must allow the traffic associated with mobile device enrollment:  

-   Between mobile devices and the enrollment proxy point: HTTPS (by default, TCP 443)  

-   Between the enrollment proxy point and the enrollment point: HTTPS (by default, TCP 443)  


If you use a proxy web server, it must be configured for SSL tunneling. SSL bridging isn't supported for mobile devices.  
