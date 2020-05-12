---
title: Site prerequisites
titleSuffix: Configuration Manager
description: Learn how to configure a Windows computer as a Configuration Manager site system server.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
---

# Site and site system prerequisites for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Windows-based computers require specific configurations to support their use as Configuration Manager site system servers.

For some products, like Windows Server Update Services (WSUS) for the software update point, you need to refer to the product documentation to identify additional prerequisites and limitations for use. Only configurations that directly apply for use with Configuration Manager are included here.

For more information on .NET Framework, see [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="bkmk_generalprerewq"></a> General requirements and limitations

The following requirements apply to all site system servers:

- Each site system server must use a 64-bit OS. The only exception is the distribution point site system role, which you can install on some 32-bit operating systems.  

- Site systems aren't supported on Server Core installations of any operating system. An exception is that Server Core installations are supported for the distribution point site system role. For more information, see [Supported operating systems for Configuration Manager site system servers](supported-operating-systems-for-site-system-servers.md).  

- After a site system server is installed, it's not supported to change:  

    - The domain name of the domain where the site system computer is located (also called a **domain rename**).  

    - The domain membership of the computer.  

    - The name of the computer.  

    If you must change any of these items, first remove the site system role from the computer. Then reinstall the role after the change is complete. For changes affecting the site server, first uninstall the site. Then reinstall the site after the change is complete.  

- Site system roles aren't supported on an instance of a Windows Server cluster. The only exception is the site database server. For more information, see [Use a SQL Server cluster for the Configuration Manager site database](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    Starting in version 1810, the Configuration Manager setup process no longer blocks installation of the site server role on a computer with the Windows role for Failover Clustering. SQL Always On requires this role, so previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using SQL Always On and a site server in passive mode. For more information, see [High availability options](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- It's not supported to change the startup type or "Log on as" settings for any Configuration Manager service. If you do, you might prevent key services from running correctly.  

### <a name="bkmk_2012Prereq"></a> Prerequisites for Windows Server 2012 and later operating systems  

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
- [Reporting services point](#bkmk_2012RSpoint)
- [Service connection point](#bkmk_SCPpreq)
- [Software update point](#bkmk_2012SUPpreq)
- [State migration point](#bkmk_2012SMPpreq)

## <a name="bkmk_2012sspreq"></a> Central administration site and primary site servers

### Windows Server roles and features

- .NET Framework 3.5

- Remote Differential Compression  

- When you use a software update point on a server other than the site server, install the WSUS Administration Console on the site server.

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### Windows ADK  

- Before you install or upgrade a central administration site or primary site, install the version of the Windows Assessment and Deployment Kit (ADK) that's required by the version of Configuration Manager you're installing or upgrading to. For more information, see [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- For more information about this requirement, see [Infrastructure requirements for OS deployment](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### Visual C++ Redistributable  

- Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

- Central administration sites and primary sites require both the x86 and x64 versions of the applicable redistributable file.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012secpreq"></a> Secondary site server

### Windows Server roles and features

- .NET Framework 3.5

- Remote Differential Compression  

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### Visual C++ Redistributable

- Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

- Secondary sites require only the x64 version.  

### Default site system roles  

- By default, a secondary site installs a **management point** and a **distribution point**.  

- Ensure that the secondary site server meets the prerequisites for these site system roles.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012dbpreq"></a> Database server  

### Remote Registry service  

- During installation of the Configuration Manager site, enable the **Remote Registry** service on the computer that hosts the site database.  

### SQL Server  

- Before you install a central administration site or primary site, install a supported version of SQL Server to host the site database. For more information, see [Supported SQL Server versions](support-for-sql-server-versions.md).  

- Before you install a secondary site, you can install a supported version of SQL Server.  

- If you choose to have Configuration Manager install SQL Server Express as part of the secondary site installation, ensure that the computer meets the requirements to run SQL Server Express.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012smsprovpreq"></a> SMS Provider server  

### Windows ADK

- The computer where you install an instance of the SMS Provider must have the required version of the Windows ADK that the version of Configuration Manager you're installing or upgrading to requires. For more information, see [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- For more information about this requirement, see [Infrastructure requirements for operating system deployment](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### Windows Server roles and features

- If you're using the [administration service](../../../develop/adminservice/overview.md), the server that hosts the SMS Provider role requires .NET 4.5 or later  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager version 1810 requires .NET 4.5.2 or later.

- Web Server (IIS): Every provider attempts to install the [administration service](../../../develop/adminservice/overview.md). This service has a dependency on IIS to bind a certificate to HTTPS port 443. Configuration Manager uses IIS APIs to check this certificate configuration. If you configure the site for [Enhanced HTTP](../hierarchy/enhanced-http.md), Configuration Manager uses IIS APIs to bind the site-generated certificate. Starting in version 2002, the site automatically uses the site's self-signed certificate.

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012acwspreq"></a> Application catalog website point  

> [!Important]  
> The application catalog's Silverlight user experience isn't supported as of current branch version 1806. Starting in version 1906, updated clients automatically use the management point for user-available application deployments. You also can't install new application catalog roles. Support ends for the application catalog roles with version 1910.  
>
> For more information, see the following articles:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Removed and deprecated features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### Windows Server roles and features

- .NET Framework 3.5

- ASP.NET 4.5  

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration  

- Common HTTP Features:  

    - Default Document  

    - Static Content  

- Application Development:  

    - ASP.NET 3.5 (and automatically selected options)  

    - ASP.NET 4.5 (and automatically selected options)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Security:  

    - Windows Authentication  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  


## <a name="bkmk_2012ACwsitepreq"></a> Application catalog web service point  

> [!Important]  
> The application catalog's Silverlight user experience isn't supported as of current branch version 1806. Starting in version 1906, updated clients automatically use the management point for user-available application deployments. You also can't install new application catalog roles. Support ends for the application catalog roles with version 1910.  
>
> For more information, see the following articles:
>
> - [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Removed and deprecated features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### Windows Server roles and features

- .NET Framework 3.5

- ASP.NET 4.5:  

    - HTTP Activation (and automatically selected options)  

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration

- Common HTTP Features:  

    - Default Document  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

- Application Development:  

    - ASP.NET 3.5 (and automatically selected options)  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5 (and automatically selected options)  

    - .NET Extensibility 4.5  

### Computer memory  

- The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

- When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012AIpreq"></a> Asset Intelligence synchronization point  

### .NET Framework

Install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012crppreq"></a> Certificate registration point  

### Windows Server roles and features

- .NET Framework

    - HTTP Activation  

### .NET Framework

Install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration

- Application Development:  

    - ASP.NET 3.5 (and automatically selected options)  

    - ASP.NET 4.5 (and automatically selected options)  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

    - IIS 6 WMI Compatibility  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012dppreq"></a> Distribution point  

### Windows Server roles and features

- Remote Differential Compression  

#### IIS configuration

- Application Development:  

    - ISAPI Extensions  

- Security:  

    - Windows Authentication  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

    - IIS 6 WMI Compatibility  

### PowerShell  

- On Windows Server 2012 or later, PowerShell 3.0 or 4.0 is required before you install the distribution point.  

### Visual C++ Redistributable

- Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

- The version that's installed depends on the computer's platform (x86 or x64).  

### Microsoft Azure  

- You can use a cloud service in Microsoft Azure to host a distribution point.  

### To support PXE or multicast  

- Enable a PXE responder on a distribution point without Windows Deployment Service.  

- Install and configure the Windows Deployment Services (WDS) Windows Server role.  

    > [!NOTE]  
    > WDS installs and configures automatically when you configure a distribution point to support PXE or multicast on a server that runs Windows Server 2012 or later.  

- For a multicast-enabled distribution point, make sure the SQL Server Native Client is installed and up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

For more information, see [Install and configure distribution points](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> When the distribution point transfers content, it transfers using the **Background Intelligent Transfer Service** (BITS) built into Windows. The distribution point role doesn't require the optional BITS IIS Server Extension feature to be installed, because the client doesn't upload information to it.  


## <a name="bkmk_2012EPPpreq"></a> Endpoint Protection point  

### Windows Server roles and features  

- .NET Framework 3.5

- Windows Defender features (Windows Server 2016 or later)  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012Enrollpreq"></a> Enrollment point  

### Windows Server roles and features

- .NET Framework 3.5

    - HTTP Activation (and automatically selected options)  

    - ASP.NET 4.5  

    - Windows Communication Foundation (WCF) Services<!-- SCCMDocs issue #1168 -->  

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

> [!Note]
> When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration

- Common HTTP Features:  

    - Default Document  

- Application Development:  

    - ASP.NET 3.5 (and automatically selected options)  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5 (and automatically selected options)  

    - .NET Extensibility 4.5  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

### Computer memory

- The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

- When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012EnrollProxpreq"></a> Enrollment proxy point  

### Windows Server roles and features

- .NET Framework 3.5

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

> [!Note]
> When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration

- Common HTTP Features:  

    - Default Document  

    - Static Content  

- Application Development:  

    - ASP.NET 3.5 (and automatically selected options)  

    - ASP.NET 4.5 (and automatically selected options)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Security:  

    - Windows Authentication  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

### Computer memory

- The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

- When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  


## <a name="bkmk_2012FSPpreq"></a> Fallback status point

### Windows Server roles and features

- BITS Server Extensions (and automatically selected options) or Background Intelligent Transfer Services (BITS) (and automatically selected options)

#### IIS configuration

The default IIS configuration is required with the following additions:  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  


## <a name="bkmk_2012MPpreq"></a> Management point  

### Windows Server roles and features

- BITS Server Extensions (and automatically selected options) or Background Intelligent Transfer Services (BITS) (and automatically selected options)  

### .NET Framework

Install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration

- Application Development:  

    - ISAPI Extensions  

- Security:  

    - Windows Authentication  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

    - IIS 6 WMI Compatibility  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012RSpoint"></a> Reporting services point  

### .NET Framework

Install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### SQL Server Reporting Services  

- Install and configure at least one instance of SQL Server to support SQL Server Reporting Services before installing the reporting point.  

- The instance that you use for SQL Server Reporting Services can be the same instance you use for the site database.  

- Additionally, the instance that you use can be shared with other System Center products, as long as the other System Center products don't have restrictions for sharing the instance of SQL Server.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_SCPpreq"></a> Service connection point  

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

> [!Note]
> When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### Visual C++ Redistributable

- Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

- The site system role requires the x64 version.  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012SUPpreq"></a> Software update point  

### Windows Server roles and features

- .NET Framework 3.5

The default IIS configuration is required.

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### Windows Server Update Services  

- Install the Windows server role Windows Server Update Services on a computer before installing a software update point.  

- For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> When you use a Software Update Point on a server other than the site server, you must install the WSUS Administration Console on the site server.

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="bkmk_2012SMPpreq"></a> State migration point

<!--SCCMDocs issue 645-->
### Windows Server roles and features

- .NET Framework 3.5

    - HTTP Activation (and automatically selected options)  

    - ASP.NET 4.5  

### .NET Framework

Enable the Windows feature for .NET Framework 3.5.

Also install a supported version of the .NET Framework version 4.5 or later. Starting in version 1906, Configuration Manager supports .NET Framework 4.8.

> [!Note]
> When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. If a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

For more information about .NET Framework versions, see the following articles:

- [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Lifecycle FAQ - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### IIS configuration

- Common HTTP Features:  

    - Default Document  

- Application Development:  

    - ASP.NET 3.5 (and automatically selected options)  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5 (and automatically selected options)  

    - .NET Extensibility 4.5  

- IIS 6 Management Compatibility:  

    - IIS 6 Metabase Compatibility  

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

