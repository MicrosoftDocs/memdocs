---
title: Site prerequisites
titleSuffix: Configuration Manager
description: Learn how to configure a Windows computer as a Configuration Manager site system server.
ms.date: 01/04/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Site and site system prerequisites for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Windows-based computers require specific configurations to support their use as Configuration Manager site system servers.

For some products, like Windows Server Update Services (WSUS) for the software update point, you need to refer to the product documentation to identify additional prerequisites and limitations for use. Only configurations that directly apply for use with Configuration Manager are included here.

## General requirements and limitations

The following requirements apply to all site system servers:

- Each site system server must use a 64-bit OS. The only exception is the distribution point site system role, which you can install on some 32-bit operating systems.

- Site systems aren't supported on Server Core installations of any OS. An exception is that Server Core installations are supported for the distribution point. For more information, see [Supported operating systems for Configuration Manager site system servers](supported-operating-systems-for-site-system-servers.md).

- After a site system server is installed, it's not supported to change:

  - The domain name of the domain where the site system computer is located (also called a **domain rename**).

  - The domain membership of the computer.

  - The name of the computer.

    If you must change any of these items, first remove the site system role from the computer. Then reinstall the role after the change is complete. For changes affecting the site server, first uninstall the site. Then reinstall the site after the change is complete.

- Site system roles aren't supported on an instance of a Windows Server cluster. The only exception is the site database server. For more information, see [Use a SQL Server Always On failover cluster instance for the site database](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

    The Configuration Manager setup process doesn't block installation of the site server role on a computer with the Windows role for Failover Clustering. SQL Server Always On availability groups require this role, so previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using an availability group and a site server in passive mode. For more information, see [High availability options](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->

- It's not supported to change the startup type or "Log on as" settings for any Configuration Manager service. If you do, you might prevent key services from running correctly.

## .NET version requirements

<!--10402814-->

Starting in version 2107, site servers and specific site systems require Microsoft .NET Framework version 4.6.2. Before you run setup to install or update the site, first update .NET and restart the system. If possible in your environment, install the latest version of .NET version 4.8.

> [!NOTE]
> .NET Framework version 4.6.2 is preinstalled with Windows Server 2016. Later versions of Windows are preinstalled with a later version of the .NET Framework.
>
> .NET Framework version 4.8 isn't supported on some OS versions.
>
> For more information, see [.NET Framework system requirements](/dotnet/framework/get-started/system-requirements).

### Site server

If the site server doesn't have any collocated roles that require .NET, it still requires .NET, but setup doesn't automatically install it. Make sure the site server itself has at least .NET version 4.6.2. If possible, install .NET 4.8.

### Site systems

During Configuration Manager setup, if site systems have a version earlier than 4.6.2, you'll see a prerequisite check warning. This check is a warning instead of an error, because setup will install version 4.6.2. When .NET updates, it usually requires Windows to restart. Site systems will send status message 4979 when a restart is required. Configuration Manager suppresses the restart; the system doesn't restart automatically.

The behavior will differ for different types of site roles that require .NET:

- The following site system roles support in-place upgrade of .NET. After upgrading .NET, if a restart is required, it sends status message 4979. The role keeps running with the earlier .NET version. After Windows restarts, the role starts using the new .NET version.
  - Asset Intelligence synchronization point
  - Management point
  - Service connection point
  - Data warehouse service point

- The following site systems roles uninstall and reinstall when .NET is upgraded. During site update, site component manager removes the role, and then updates .NET. If a restart is required, it sends status message 4979. After restart, site component manager reinstalls the role with the new .NET version. The role could be unavailable while it waits for you to restart the server.
  - SMS Provider for the administration service
  - Certificate registration point
  - Enrollment point
  - Enrollment proxy point
  - Reporting services point
  - Software update point

> [!NOTE]
> Currently, you still need to enable the Windows feature for .NET Framework 3.5 on site systems that require it.

If site systems have at least version 4.6.2 but earlier than version 4.8, you'll also see a prerequisite check warning. We recommend that you install the latest version of .NET version 4.8 to get the latest performance and security improvements. Configuration Manager setup doesn't automatically install .NET version 4.8. A later version of Configuration Manager will require .NET version 4.8.

There's also a new [management insight](../../servers/manage/management-insights.md) to recommend site systems that don't yet have .NET version 4.8 or later.

### Managing system restarts for .NET updates

Whether you update .NET before updating the site, or setup updates it, .NET may require a restart to complete its installation. After .NET Framework is installed, it may require other updates. These updates may also require the server to restart.

If you need to manage the device restarts before you update the site, use the following recommended process:

1. Install the latest baseline .NET version. For example, install .NET version 4.8.
1. Restart the server.
1. Scan for software updates and install the latest .NET cumulative update.
1. Restart the server.
1. Update the site to the latest current branch version.

## Central administration site and primary site servers

For more information on all prerequisites including permissions, see [Prerequisites for installing a primary site or a CAS](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri). The following sections detail the prerequisite components that you need to install or enable.

### Windows Server roles and features for the site server

- .NET Framework 3.5

- Remote Differential Compression

- When you use a software update point on a server other than the site server, install the WSUS Administration Console on the site server.

### .NET Framework for the site server

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### Windows ADK for the site server

- Before you install or upgrade a central administration site or primary site, install the version of the Windows Assessment and Deployment Kit (ADK) that's required by the version of Configuration Manager you're installing or upgrading to. For more information, see [Support for the Windows ADK](support-for-windows-adk.md).

- For more information about this requirement, see [Infrastructure requirements for OS deployment](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).

### Visual C++ Redistributable for the site server

- Starting in version 2107, Configuration Manager installs the Microsoft Visual C++ 2015-2019 redistributable package (14.28.29914.0) on each computer that installs a site server. In version 2103 and earlier, it installs the Visual C++ 2013 version (12.0.40660.0).<!--5170229-->

- The CAS and primary sites require both the x86 and x64 versions of the applicable redistributable file.

### SQL Server Native Client for the site server

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Secondary site server

### Windows Server roles and features for the secondary site server

- .NET Framework 3.5

- Remote Differential Compression

### .NET Framework for the secondary site server

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### Visual C++ Redistributable for the secondary site server

- Starting in version 2107, Configuration Manager installs the Microsoft Visual C++ 2015-2019 redistributable package (14.28.29914.0) on each computer that installs a secondary site server. In version 2103 and earlier, it installs the Visual C++ 2013 version (12.0.40660.0).<!--5170229-->

- Secondary sites require only the x64 version.

### Default site system roles for the secondary site server

By default, a secondary site installs a **management point** and a **distribution point**. Make sure that the secondary site server meets the prerequisites for these site system roles.

### SQL Server Native Client for the secondary site server

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Database server

### Remote Registry service for the site database server

During installation of the Configuration Manager site, enable the **Remote Registry** service on the computer that hosts the site database.

### SQL Server for the site database server

- Before you install a CAS or primary site, install a supported version of SQL Server to host the site database. For more information, see [Supported SQL Server versions](support-for-sql-server-versions.md).

- Before you install a secondary site:

  - You can install a supported version of SQL Server.

  - You can choose to have Configuration Manager install SQL Server Express. Make sure that the server meets the requirements to run SQL Server Express.

### SQL Server Native Client for the site database server

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## SMS Provider server

### Windows ADK for the SMS Provider

- The server where you install an instance of the SMS Provider must have a supported version of the Windows ADK. For more information, see [Support for the Windows ADK](support-for-windows-adk.md).

- For more information about this requirement, see [Infrastructure requirements for operating system deployment](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).

### Windows Server roles and features for the SMS Provider

Web Server (IIS): Every provider attempts to install the [administration service](../../../develop/adminservice/overview.md). This service has a dependency on IIS to bind a certificate to HTTPS port 443. Configuration Manager uses IIS APIs to check this certificate configuration. If you configure the site for [Enhanced HTTP](../hierarchy/enhanced-http.md), Configuration Manager uses IIS APIs to bind the site-generated certificate. Unless the server already has a PKI-based certificate, the site automatically uses the site's self-signed certificate.

### .NET Framework for the SMS Provider

If you're using the [administration service](../../../develop/adminservice/overview.md), the server that hosts the SMS Provider role requires .NET 4.5 or later. <!-- SCCMDocs issue #1203 --> Starting in version 2107, this role requires .NET version 4.6.2, and version 4.8 is recommended. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server Native Client for the SMS Provider

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Asset Intelligence synchronization point

> [!IMPORTANT]
> Starting in November 2021, this feature of Configuration Manager is deprecated.<!-- 12454890 --> For more information, see [Asset intelligence deprecation](../../clients/manage/asset-intelligence/deprecation.md).

### .NET Framework for the AISP

Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server Native Client for the AISP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Certificate registration point

### Windows Server roles and features for the CRP

- .NET Framework

  - HTTP Activation

#### IIS configuration for the CRP

- Application Development:

  - ASP.NET 3.5 (and automatically selected options)

  - ASP.NET 4.5 (and automatically selected options)

- IIS 6 Management Compatibility:

  - IIS 6 Metabase Compatibility

  - IIS 6 WMI Compatibility

### .NET Framework for the CRP

Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server Native Client for the CRP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Data warehouse service point

For more information on the prerequisites for this role, see [The data warehouse service point](../../servers/manage/data-warehouse.md#prerequisites).

### .NET Framework for the DWSP

Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server for the DWSP

The data warehouse database requires SQL Server 2012 or later. The edition can be Standard, Enterprise, or Datacenter. The SQL Server version for the data warehouse doesn't need to be the same as the site database server or the reporting services point.

## Distribution point

### Windows Server roles and features for the DP

- Remote Differential Compression

> [!NOTE]
> When the distribution point transfers content, it transfers using the **Background Intelligent Transfer Service** (BITS) built into Windows. The distribution point role doesn't require the optional BITS IIS Server Extension feature to be installed, because the client doesn't upload information to it.<!--sms.503672 -Clarified BITS use-->

#### IIS configuration for the DP

- Application Development:

  - ISAPI Extensions

- Security:

  - Windows Authentication

- IIS 6 Management Compatibility:

  - IIS 6 Metabase Compatibility

  - IIS 6 WMI Compatibility

By default, IIS uses request filtering to block several file name extensions and folder locations from access by HTTP or HTTPS communication. On a distribution point, this configuration prevents clients from downloading packages that have blocked extensions or folder locations. For more information, see [IIS request filtering for distribution points](../network/prepare-windows-servers.md#iis-request-filtering-for-distribution-points).

Distribution points require that IIS allows the following HTTP verbs:

- GET
- HEAD
- PROPFIND

### Visual C++ Redistributable for the DP

- Starting in version 2107, Configuration Manager installs the Microsoft Visual C++ 2015-2019 redistributable package (14.28.29914.0) on each computer that hosts a distribution point. In version 2103 and earlier, it installs the Visual C++ 2013 version (12.0.40660.0).<!--5170229-->

- The version that's installed depends on the computer's platform (x86 or x64).

### Add PXE support for the DP

There are two options to support PXE on a distribution point:

- Enable the Configuration Manager PXE responder without Windows Deployment Service.

- Install and configure the Windows Deployment Services (WDS) Windows Server role.

    > [!NOTE]
    > WDS installs and configures automatically when you enable a distribution point to support PXE.

For more information, see [Install and configure distribution points](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

### Add multicast support for the DP

- Install and configure the Windows Deployment Services (WDS) Windows Server role.

    > [!NOTE]
    > WDS installs and configures automatically when you enable a distribution point to support multicast.

- Make sure the SQL Server Native Client is installed and up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Endpoint Protection point

### Windows Server roles and features for the endpoint protection point

- .NET Framework 3.5

- Windows Defender features (Windows Server 2016 or later)

### SQL Server Native Client for the endpoint protection point

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Enrollment point

> [!IMPORTANT]
> With the deprecation of on-premises MDM and the Configuration Manager client for macOS, this site system role is also deprecated. For more information, see [Removed and deprecated features for Configuration Manager](../changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->

### Windows Server roles and features for the enrollment point

- .NET Framework 3.5

  - HTTP Activation (and automatically selected options)

  - ASP.NET 4.5

  - Windows Communication Foundation (WCF) Services<!-- SCCMDocs issue #1168 -->

#### IIS configuration for the enrollment point

- Common HTTP Features:

  - Default Document

- Application Development:

  - ASP.NET 3.5 (and automatically selected options)

  - .NET Extensibility 3.5

  - ASP.NET 4.5 (and automatically selected options)

  - .NET Extensibility 4.5

- IIS 6 Management Compatibility:

  - IIS 6 Metabase Compatibility

### .NET Framework for the enrollment point

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### Computer memory for the enrollment point

- The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.

- When this site system role is collocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.

### SQL Server Native Client

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Enrollment proxy point

> [!IMPORTANT]
> With the deprecation of on-premises MDM and the Configuration Manager client for macOS, this site system role is also deprecated. For more information, see [Removed and deprecated features for Configuration Manager](../changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->

### Windows Server roles and features for the enrollment proxy point

- .NET Framework 3.5

#### IIS configuration for the enrollment proxy point

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

### .NET Framework for the enrollment proxy point

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### Computer memory for the enrollment proxy point

- The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.

- When this site system role is colocated with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.

## Fallback status point

### Windows Server roles and features for the FSP

Depending upon the version of Windows Server, enable one of the following features:

- BITS Server Extensions and the automatically selected options
- Background Intelligent Transfer Services (BITS) and the automatically selected options

#### IIS configuration

The default IIS configuration is required with the following additions:

- IIS 6 Management Compatibility:

  - IIS 6 Metabase Compatibility

## Management point

### Windows Server roles and features for the MP

Depending upon the version of Windows Server, enable one of the following features:

- BITS Server Extensions and the automatically selected options
- Background Intelligent Transfer Services (BITS) and the automatically selected options

#### IIS configuration for the MP

- Application Development:

  - ISAPI Extensions

- Security:

  - Windows Authentication

- IIS 6 Management Compatibility:

  - IIS 6 Metabase Compatibility

  - IIS 6 WMI Compatibility

To make sure that clients can successfully communicate with a management point, make sure IIS allows the following HTTP verbs:

- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

### .NET Framework for the MP

Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server Native Client for the MP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Reporting services point

### .NET Framework for the RSP

Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server Reporting Services for the RSP

- Install and configure at least one instance of SQL Server to support SQL Server Reporting Services.

- The instance that you use for SQL Server Reporting Services can be the same instance you use for the site database.

- The instance that you use can be shared with System Center products. The System Center products can't have restrictions for sharing the instance of SQL Server.

### SQL Server Native Client for the RSP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Service connection point

### .NET Framework for the SCP

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### Visual C++ Redistributable for the SCP

- Starting in version 2107, Configuration Manager installs the Microsoft Visual C++ 2015-2019 redistributable package (14.28.29914.0) on the service connection point. In version 2103 and earlier, it installs the Visual C++ 2013 version (12.0.40660.0).<!--5170229-->

### SQL Server Native Client for the SCP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## Software update point

### Windows Server roles and features for the SUP

- .NET Framework 3.5

- The default IIS configuration is required.

### .NET Framework for the SUP

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### Windows Server Update Services (WSUS) for the SUP

Install the WSUS server role. For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md).

> [!NOTE]
> When you use a software update point on a remote site system, install the WSUS Administration Console on the site server.

### SQL Server Native Client for the SUP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

## State migration point

<!--SCCMDocs issue 645-->
### Windows Server roles and features for the SMP

- .NET Framework 3.5

  - HTTP Activation (and automatically selected options)

  - ASP.NET 4.5

#### IIS configuration for the SMP

- Common HTTP Features:

  - Default Document

- Application Development:

  - ASP.NET 3.5 (and automatically selected options)

  - .NET Extensibility 3.5

  - ASP.NET 4.5 (and automatically selected options)

  - .NET Extensibility 4.5

- IIS 6 Management Compatibility:

  - IIS 6 Metabase Compatibility

### .NET Framework for the SMP

- Enable the Windows feature for .NET Framework 3.5.

- Install a supported version of the .NET Framework. For more information, [.NET version requirements](#net-version-requirements).

### SQL Server Native Client for the SMP

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Make sure this component is up to date. For more information, see [Prerequisite checks - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).
