---
title: How to enable TLS 1.2
titleSuffix: Configuration Manager
description: Information about how to enable TLS 1.2 for Configuration Manager.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to enable TLS 1.2

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes how to enable TLS 1.2 for Configuration Manager, including for individual components. Update requirements for commonly used features, and troubleshooting of some common problems, are also described in this article.

Configuration Manager relies on many different components for secure communication. The protocol that's used for a given connection depends on the capabilities of all the required components. If one component is out-of-date, the communication might use an older, less secure protocol.

To correctly enable Configuration Manager to support TLS 1.2, first enable TLS 1.2 for all required components. The required components depends on your environment and the Configuration Manager features that you use.


## Enable TLS 1.2

To enable TLS 1.2, first enable TLS 1.2 as a security provider for each computer that's running or interacting with Configuration Manager. Then, enable TLS 1.2 for components that Configuration Manager depends on for secure communication.

### Enable the TLS 1.2 protocol as a security provider

Verify the `\SecurityProviders\SCHANNEL\Protocols` registry subkey setting, as shown in [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

> [!NOTE]
> TLS 1.2 is enabled by default. Therefore, no change to these keys is required to enable it. You can make changes under Protocols to disable TLS 1.0 and TLS 1.1 after you have followed the rest of the guidance in this article, and you have verified that the environment works by having only TLS 1.2 enabled.

### Enable TLS 1.2 for dependent components

To enable TLS 1.2 for dependent components that Configuration Manager depends on for secure communication, you must:

- [Update .NET Framework to support TLS 1.2](#update-net-framework-to-support-tls-12)
- [Update SQL Server and client components](#update-sql-server-and-client-components)
- [Update Windows and WinHTTP on Windows 8.0, Windows Server 2012 R2 and earlier](#update-windows-and-winhttp)
- [Update Windows Server Update Services (WSUS)](#update-windows-server-update-services-wsus)

#### Update .NET Framework to support TLS 1.2

##### Determine .NET version

First, determine your .NET version number. For more information, see [How to determine which versions and service pack levels of the Microsoft .NET Framework are installed](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

##### Install .NET updates

Some versions of .NET Framework might require updates to enable strong cryptography. Use these guidelines:

- NET Framework 4.6.2 and later supports TLS 1.1 and TLS 1.2. Confirm the registry settings, but no additional changes are required.

- Update NET Framework 4.6 and earlier versions to support TLS 1.1 and TLS 1.2. For more information, see [.NET Framework versions and dependencies](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- If you're using .NET Framework 4.5.1 or 4.5.2 on Windows 8.1 or Windows Server 2012, the relevant updates and details are also available from the [Download Center](https://www.microsoft.com/download/details.aspx?id=42883).

##### Configure for strong cryptography

Configure .NET Framework to support strong cryptography. Set the `SchUseStrongCrypto` registry setting to `DWORD:00000001`. This value disables the RC4 stream cipher and requires a restart. For more information about this setting, see [Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Make sure to set the following registry keys on any computer that communicates across the network with a TLS 1.2-enabled system. For example, Configuration Manager clients, or any remote site system role that's not installed on the site server.

For 32-bit applications that are running on 32-bit systems or 64-bit applications that are running on 64-bit systems, update the following subkey value:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

For 32-bit applications that are running on 64-bit systems, update the following subkey value:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> The `SchUseStrongCrypto` setting allows .NET to use TLS 1.1 and TLS 1.2. The `SystemDefaultTlsVersions` setting allows .NET to use the OS configuration. For more information, see [TLS best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).


#### Update SQL Server and client components

Microsoft SQL Server 2016 and later support TLS 1.1 and TLS 1.2. Earlier versions and dependent libraries might require updates. For more information, see [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

> [!NOTE]
> KB 3135244 also describes requirements for SQL Server client components. Update each component that's used in your environment.

##### SQL Server Native Client

Make sure to also update the SQL Server Native Client. Starting in version 1810, this requirement is a [prerequisite check (warning)](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-server-native-client).

Configuration Manager uses SQL Server Native Client on the following site system roles:

- Site database server
- Site server: central administration site, primary site, or secondary site
- Management point
- Device management point
- State migration point
- SMS Provider
- Software update point
- Multicast-enabled distribution point
- Asset Intelligence update service point
- Reporting services point
- Application catalog web service
- Enrollment point
- Endpoint Protection point
- Service connection point
- Certificate registration point
- Data warehouse service point

#### Update Windows and WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016, and later versions of Windows natively support TLS 1.2 for client-server communications over WinHTTP.

Earlier versions of Windows, such as Windows 7 or Windows Server 2012, don't enable TLS 1.1 or 1.2 by default for client-server communications through HTTPS. For these earlier versions of Windows, install [Update 3140245](https://support.microsoft.com/help/3140245) to enable TLS 1.1 and TLS 1.2 as the default secure protocols for WinHTTP in Windows. Then set the following registry values:

> [!IMPORTANT]
> Enable these settings on all clients *before* enabling TLS 1.2 on the Configuration Manager servers. Otherwise, you can inadvertently orphan them.

Verify that the `DefaultSecureProtocols` registry setting is `0xAA0`, as follows:

```Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

> [!NOTE]
> This change requires a restart.

#### Update Windows Server Update Services (WSUS)

To support TLS 1.2 for client-server communications in WSUS on Windows Server 2012 and Windows Server 2012 R2, install the following update on the WSUS server:

- For WSUS server that's running Windows Server 2012, install [update 4022721](https://support.microsoft.com/help/4022721) or a later update.
- For WSUS server that's running Windows Server 2012 R2, install [update 4022720](https://support.microsoft.com/help/4022720) or a later update.


## Tasks for features and scenarios

This section describes the dependencies for specific Configuration Manager features and scenarios. To determine the next steps, locate the items that apply to your environment. Then verify the dependencies by using the steps provided earlier in [Enable TLS 1.2 for dependent components](#enable-tls-12-for-dependent-components).

|Feature or scenario|Update tasks|
|--- |--- |
|Site servers (central, primary, or secondary)| - [Update .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verify strong cryptography settings|
|Site database server|[Update SQL Server and its client components](#update-sql-server-and-client-components)|
|Secondary site servers|[Update SQL Server and its client components](#update-sql-server-and-client-components) to a compliant version of SQL Express|
|Site system roles| - [Update .NET Framework](#update-net-framework-to-support-tls-12) and verify strong cryptography settings <br/> - [Update SQL Server and its client components](#update-sql-server-and-client-components) on roles that require it, including the [SQL Server Native Client](#sql-server-native-client)|
|Reporting services point|- [Update .NET Framework](#update-net-framework-to-support-tls-12) on the site server, the SQL Reporting Services servers, and any computer with the console<br/> - Restart the SMS_Executive service as necessary|
|Software update point|[Update WSUS](#update-windows-server-update-services-wsus)|
|Configuration Manager console| - [Update .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verify strong cryptography settings|
|Configuration Manager client with HTTPS site system roles|[Update Windows to support TLS 1.2 for client-server communications by using WinHTTP](#update-windows-and-winhttp)|
|Software Center| - [Update .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verify strong cryptography settings|
|Windows 7 clients| *Before* you enable TLS 1.2 on any server components, [update Windows to support TLS 1.2 for client-server communications by using WinHTTP](#update-windows-and-winhttp). If you enable TLS 1.2 on server components first, you can orphan earlier versions of clients.|


## Known issues

This section provides advice for common issues that occur when you enable TLS 1.2 support.

### Unsupported platforms

The following client platforms are supported by Configuration Manager but aren't supported in a TLS 1.2 environment:

- Windows Server 2008
- Windows CE
- Apple OS X
- Windows 10 devices managed with on-premises MDM

### Reports don't show in the console

If reports don't show in the Configuration Manager console, make sure to update the computer on which you're running the console. You need to [update the .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography.

### FIPS security policy enabled

If you enable the FIPS security policy setting for either the client or a server, Secure Channel (Schannel) negotiation can cause them to use TLS 1.0. This behavior happens even if you disable the protocol in the registry.

To investigate, enable Secure Channel event logging, and then review Schannel events in the system log. For more information, see [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### SQL Server communication failure

If SQL Server communication fails and returns an **SslSecurityError** error, verify the following settings:

- [Update .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography on each machine
- [Update SQL Server](#update-sql-server-and-client-components) on the host server
- [Update SQL client components](#update-sql-server-and-client-components) on all systems that communicate with SQL. For example, the site servers, SMS provider, and site role servers.

### Configuration Manager client communication failures

If the Configuration Manager client doesn't communicate with site roles, verify that you [updated Windows](#update-windows-and-winhttp) to support TLS 1.2 for client-server communication by using WinHTTP. Common site roles include distribution points, management points, and state migration points.

### Reporting services point fails and returns an expected error

If the reporting services point doesn't configure reports, check the **SRSRP.log** for the following error entry:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

To resolve this issue, follow these steps:

1. [Update .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography on all relevant computers.

1. After you install any updates, restart the SMS_Executive service.

### Application catalog doesn't initialize

> [!Important]  
> The application catalog is deprecated. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

If the application catalog doesn't initialize, check the **ServicePortalWebSite.svclog** file for the following error entry:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

To resolve this issue, follow these steps:

1. [Update .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography on all relevant computers.

1. In the `%WinDir%\System32\InetSrv` folder of the application catalog server, create a **W2SP.exe.config** file with the following contents:

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > This file is the default file that's created if the application was built by using .NET Framework 4.6.3.

1. Use HTTPS transport security for application catalog roles.

    > [!Important]
    > When you use HTTP message security for application catalog roles, WCF is hard-coded to use SSL 3.0 and TLS 1.0 only. This prevents the use of TLS 1.2.

1. If you made any changes, restart the computer.

### Software Center or browser doesn't communicate with the application catalog

> [!Important]  
> The application catalog is deprecated. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

The best method to make Software Center work with for user-available apps in a TLS 1.2-enabled site, remove the application catalog role. Then let Software Center communicate directly with a management point. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

If you need to resolve communication failures between the application catalog and Software Center, verify the following conditions:

- [Update .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography on each computer.

- After you make the changes, restart all affected computers.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

### Service connection point upload failures

If the service connection point doesn't upload data to SCCMConnectedService, [update the .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography on each computer. After you make the changes, remember to restart the computers.

### Configuration Manager console displays Intune onboarding dialog box

If the Intune onboarding dialog box appears when the console tries to connect to the Intune portal, [update the .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography on each computer. After you make the changes, remember to restart the computers.

### Configuration Manager console displays failure to sign in to Azure

When you try to create applications in Azure Active Directory (Azure AD), if the Azure Services onboarding dialog box immediately fails after you select **Sign in**, [update the .NET Framework](#update-net-framework-to-support-tls-12), and enable strong cryptography. After you make the changes, remember to restart the computers.

## See also

[Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)
