---
title: Site prerequisites
titleSuffix: Configuration Manager
description: Learn how to configure a Windows computer as a Configuration Manager site system server.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Site and site system prerequisites for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Windows-based computers require specific configurations to support their use as Configuration Manager site system servers. 

This article primarily focuses on [Windows Server 2012 and later](#bkmk_2012Prereq). [Windows Server 2008 R2 and Windows Server 2008](#bkmk_2008) are supported for the distribution point site system role. For more information, see [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers). 

For some products, like Windows Server Update Services (WSUS) for the software update point, you need to refer to the product documentation to identify additional prerequisites and limitations for use. Only configurations that directly apply for use with Configuration Manager are included here.   

> [!NOTE]  
>  In January 2016, support expired for the .NET Framework 4.0, 4.5, and 4.5.1. For more information, see [Microsoft .NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  



## <a name="bkmk_generalprerewq"></a> General requirements and limitations

The following requirements apply to all site system servers:

- Each site system server must use a 64-bit OS. The only exception is the distribution point site system role, which you can install on some 32-bit operating systems.  

- Site systems aren't supported on Server Core installations of any operating system. An exception is that Server Core installations are supported for the distribution point site system role. For more information, see [Supported operating systems for Configuration Manager site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

- After a site system server is installed, it's not supported to change:  

    - The domain name of the domain where the site system computer is located (also called a **domain rename**).  

    - The domain membership of the computer.  

    - The name of the computer.  

  If you must change any of these items, first remove the site system role from the computer. Then reinstall the role after the change is complete. For changes affecting the site server, first uninstall the site. Then reinstall the site after the change is complete.  

- Site system roles aren't supported on an instance of a Windows Server cluster. The only exception is the site database server. For more information, see [Use a SQL Server cluster for the Configuration Manager site database](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).  

- It's not supported to change the startup type or "Log on as" settings for any Configuration Manager service. If you do, you might prevent key services from running correctly.  


###  <a name="bkmk_2012Prereq"></a> Prerequisites for Windows Server 2012 and later operating systems  

See the main sections of this article for the specific prerequisites for site system servers and roles on Windows Server 2012 and later:

- [Central administration site and primary site servers](#bkmk_2012sspreq)
- [Secondary site server](#bkmk_2012secpreq)
- [Database server](#bkmk_2012dbpreq)
- [SMS Provider server](#bkmk_2012smsprovpreq)
- [Application Catalog website point](#bkmk_2012acwspreq)
- [Application Catalog web service point](#bkmk_2012ACwsitepreq)
- [Asset Intelligence synchronization point](#bkmk_2012AIpreq)
- [Certificate registration point](#bkmk_2012crppreq)
- [Distribution point](#bkmk_2012dppreq)
- [Endpoint Protection point](#bkmk_2012EPPpreq)
- [Enrollment point](#bkmk_2012Enrollpreq)
- [Enrollment proxy point](#bkmk_2012EnrollProxpreq)
- [Fallback status point](#bkmk_2012FSPpreq)
- [Management point](#bkmk_2012MPpreq)
- [Reporting point](#bkmk_2012RSpoint)
- [Service connection point](#bkmk_SCPpreq)
- [Software update point](#bkmk_2012SUPpreq)
- [State migration point](#bkmk_2012SMPpreq)

##  <a name="bkmk_2012sspreq"></a> Central administration site and primary site servers 

#### Windows Server roles and features  

- .NET Framework 3.5 SP1 (or later)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2  

    - For more information about .NET Framework versions, see [.NET Framework Versions and Dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Remote Differential Compression  

#### Windows ADK  

- Before you install or upgrade a central administration site or primary site, install the version of the Windows Assessment and Deployment Kit (ADK) that's required by the version of Configuration Manager you're installing or upgrading to. For more information, see [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- For more information about this requirement, see [Infrastructure requirements for operating system deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### Visual C++ Redistributable  

- Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

- Central administration sites and primary sites require both the x86 and x64 versions of the applicable redistributable file.  



##  <a name="bkmk_2012secpreq"></a> Secondary site server   

#### Windows Server roles and features  

- .NET Framework 3.5 SP1 (or later)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2  

    - For more information about .NET Framework versions, see [.NET Framework Versions and Dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  

- Remote Differential Compression  

#### Visual C++ Redistributable  

- Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

- Secondary sites require only the x64 version.  

#### Default site system roles  

- By default, a secondary site installs a **management point** and a **distribution point**.  

- Ensure that the secondary site server meets the prerequisites for these site system roles.  



##  <a name="bkmk_2012dbpreq"></a> Database server  

#### Remote Registry service  

- During installation of the Configuration Manager site, enable the **Remote Registry** service on the computer that hosts the site database.  

#### SQL Server  

- Before you install a central administration site or primary site, install a supported version of SQL Server to host the site database. For more information, see [Supported SQL Server versions](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

- Before you install a secondary site, you can install a supported version of SQL Server.  

- If you choose to have Configuration Manager install SQL Server Express as part of the secondary site installation, ensure that the computer meets the requirements to run SQL Server Express.  



##  <a name="bkmk_2012smsprovpreq"></a> SMS Provider server  

#### Windows ADK  

- The computer where you install an instance of the SMS Provider must have the required version of the Windows ADK that the version of Configuration Manager you're installing or upgrading to requires. For more information, see [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- For more information about this requirement, see [Infrastructure requirements for operating system deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  



##  <a name="bkmk_2012acwspreq"></a> Application Catalog website point  

#### Windows Server roles and features  

- .NET Framework 3.5 SP1 (or later)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2  

    - ASP.NET 4.5  

    - For more information about .NET Framework versions, see [.NET Framework Versions and Dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  


#### IIS configuration  

-   Common HTTP Features:  

    -   Default Document  

    -   Static Content  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   .NET Extensibility 4.5  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  



##  <a name="bkmk_2012ACwsitepreq"></a> Application Catalog web service point  

#### Windows Server roles and features  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2:  

    -   ASP.NET 4.5:  

        -   HTTP Activation (and automatically selected options)  

#### IIS configuration  

-   Common HTTP Features:  

    -   Default Document  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 4.5  

#### Computer memory  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  



##  <a name="bkmk_2012AIpreq"></a> Asset Intelligence synchronization point  

#### Windows Server roles and features  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2 



##  <a name="bkmk_2012crppreq"></a> Certificate registration point  

#### Windows Server roles and features  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2:  

    -   HTTP Activation  

#### IIS configuration  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   ASP.NET 4.5 (and automatically selected options)  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  



##  <a name="bkmk_2012dppreq"></a> Distribution point  

#### Windows Server roles and features  

-   Remote Differential Compression  

#### IIS configuration  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

#### PowerShell  

-   On Windows Server 2012 or later, PowerShell 3.0 or 4.0 is required before you install the distribution point.  

#### Visual C++ Redistributable  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The version that's installed depends on the computer's platform (x86 or x64).  

#### Microsoft Azure  

-   You can use a cloud service in Microsoft Azure to host a distribution point.  

#### To support PXE or multicast  

-   Install and configure the Windows Deployment Services (WDS) Windows Server role.  

    > [!NOTE]  
    >  WDS installs and configures automatically when you configure a distribution point to support PXE or multicast on a server that runs Windows Server 2012 or later.  

-   Starting in version 1806, enable a PXE responder on a distribution point without Windows Deployment Service.  

For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> When the distribution point transfers content, it transfers using the **Background Intelligent Transfer Service** (BITS) built into Windows. The distribution point role doesn't require the optional BITS IIS Server Extension feature to be installed, because the client doesn't upload information to it.  



##  <a name="bkmk_2012EPPpreq"></a> Endpoint Protection point  

#### Windows Server roles and features  

-   .NET Framework 3.5 SP1 (or later)  



##  <a name="bkmk_2012Enrollpreq"></a> Enrollment point  

#### Windows Server roles and features  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2:  

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

    -   HTTP Activation (and automatically selected options)  

    -   ASP.NET 4.5  

#### IIS configuration  

-   Common HTTP Features:  

    -   Default Document  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 4.5  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

#### Computer memory  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  



##  <a name="bkmk_2012EnrollProxpreq"></a> Enrollment proxy point  

#### Windows Server roles and features  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2 

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation completes.  

#### IIS configuration  

-   Common HTTP Features:  

    -   Default Document  

    -   Static Content  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   .NET Extensibility 4.5  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

#### Computer memory  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  



##  <a name="bkmk_2012FSPpreq"></a> Fallback status point  

The default IIS configuration is required with the following additions:  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  



##  <a name="bkmk_2012MPpreq"></a> Management point  

#### Windows Server roles and features  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2 

-   BITS Server Extensions (and automatically selected options) or Background Intelligent Transfer Services (BITS) (and automatically selected options)  

#### IIS configuration  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  



##  <a name="bkmk_2012RSpoint"></a> Reporting point  

#### Windows Server roles and features  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2 

#### SQL Server Reporting Services  

-   Install and configure at least one instance of SQL Server to support SQL Server Reporting Services before installing the reporting point.  

-   The instance that you use for SQL Server Reporting Services can be the same instance you use for the site database.  

-   Additionally, the instance that you use can be shared with other System Center products, as long as the other System Center products don't have restrictions for sharing the instance of SQL Server.  



##  <a name="bkmk_SCPpreq"></a> Service connection point  

#### Windows Server roles and features  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2 

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

#### Visual C++ Redistributable  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The site system role requires the x64 version.  



##  <a name="bkmk_2012SUPpreq"></a> Software update point  

#### Windows Server roles and features  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2 

The default IIS configuration is required.

#### Windows Server Update Services  

-   Install the Windows server role Windows Server Update Services on a computer before installing a software update point.  

-   For more information, see [Plan for software updates](/sccm/sum/plan-design/plan-for-software-updates).  



##  <a name="bkmk_2012SMPpreq"></a> State migration point  
<!--SCCMDocs issue 645-->
#### Windows Server roles and features  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1, or 4.7.2:  

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

    -   HTTP Activation (and automatically selected options)  

    -   ASP.NET 4.5  

#### IIS configuration  

-   Common HTTP Features:  

    -   Default Document  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 4.5  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  



##  <a name="bkmk_2008"></a> Prerequisites for Windows Server 2008 R2 and Windows Server 2008  

Windows Server 2008 and Windows Server 2008 R2 are now in extended support and are no longer in mainstream support, as detailed by the [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Removed and deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

These OS versions aren't supported for site servers or most site system roles. They're still supported for the distribution point site system role, including pull-distribution points and for PXE and multicast.


###  <a name="bkmk_2008dppreq"></a> Distribution point  

#### IIS configuration

You can use the default IIS configuration or a custom configuration. To use a custom IIS configuration, you must enable the following options for IIS:  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

When you use a custom IIS configuration, you can remove options that aren't required, such as the following items:  

-   Common HTTP Features:  

    -   HTTP Redirection  

-   IIS Management Scripts and Tools  

#### Windows feature  

-   Remote Differential Compression  

#### Visual C++ Redistributable  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The version that is installed depends on the computer's platform (x86 or x64).  

#### Microsoft Azure  

-   You can use a cloud service in Azure to host a distribution point.  

#### To support PXE or multicast  

-   Install and configure the Windows Deployment Services (WDS) Windows Server role.  

    > [!NOTE]  
    >  WDS installs and configures automatically when you configure a distribution point to support PXE or multicast on a server that runs Windows Server 2012 or later.  

-   Starting in version 1806, enable a PXE responder on a distribution point without Windows Deployment Service.  

For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> When the distribution point transfers content, it transfers using the **Background Intelligent Transfer Service** (BITS) built into the Windows operating system. The distribution point role doesn't require the optional BITS IIS Server Extension feature to be installed because the client does not  upload information to it.   

