---
title: How to enable transport layer security 1.2
titleSuffix: Configuration Manager
description: Information about how to enable TLS 1.2 for Microsoft Configuration Manager.
ms.date: 05/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to enable transport layer security 1.2 for Configuration Manager

This article describes how to enable transport layer security (TLS) 1.2 for Configuration Manager, including for individual components. Update requirements for commonly used features, and troubleshooting of some common problems, are also described in this article.

Configuration Manager relies on many different components for secure communication. The protocol that's used for a given connection depends on the capabilities of all the required components. If one component is out-of-date, the communication might use an older, less secure protocol.

To correctly enable Configuration Manager to support TLS 1.2, you must enable TLS 1.2 for all required components. The required components depends on your environment and the Configuration Manager features that you use.


## To enable TLS 1.2

To enable TLS 1.2, you must first enable TLS 1.2 as a security provider for each computer that's running or interacting with Configuration Manager. Then, enable TLS 1.2 for components that Configuration Manager depends on for secure communication.

### Enable the TLS 1.2 protocol as a security provider

Verify the "\SecurityProviders\SCHANNEL\Protocols" registry subkey setting, as shown in [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry?).

> [!NOTE]
> TLS 1.2 is enabled by default. Therefore, no change to these keys is required to enable it. You can make changes under Protocols to disable TLS 1.0 and TLS 1.1 after you have followed the rest of the guidance in this article, and you have verified that the environment works by having only TLS 1.2 enabled.

### Enable TLS 1.2 for dependent components
To enable TLS 1.2 for dependent components that Configuration Manager depends on for secure communication, you must:

- [Update .NET Framework to support TLS 1.2](#update-net-framework-to-support-tls-12)
- [Update SQL Server and client components](#update-sql-server-and-client-components)
- [Update Windows and WinHTTP on Windows 8.0, Windows Server 2012 R2 and earlier](#update-windows-and-winhttp)
- [Update Windows Server Update Services (WSUS)](#update-windows-server-update-services)

#### Update .NET Framework to support TLS 1.2
To update .NET Framework to support TLS 1.2, first determine your .NET version number. For help, see [How to determine which versions and service pack levels of the Microsoft .NET Framework are installed](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

Earlier versions of .NET Framework might require updates or registry changes to enable strong cryptography. Use these guidelines:

- NET Framework 4.6.2 supports TLS 1.1 and TLS 1.2.  No additional changes are required.
- NET Framework 4.6 and earlier versions [must be updated](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies) to support TLS 1.1 and TLS 1.2.

If you're using .NET Framework 4.5.1 or 4.5.2 on Windows 8.1, Windows RT 8.1, or Windows Server 2012, the relevant updates and details are also available from the [Download Center](https://www.microsoft.com/download/details.aspx?id=42883).
-  .NET Framework must be configured to support strong cryptography. Set the `SchUseStrongCrypto` registry setting to `DWORD:00000001`. This disables the RC4 stream cipher and requires a restart. To learn more about this setting, see [Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

For 32-bit applications that are running on 32-bit systems or 64-bit applications that are running on 64-bit systems, update the following subkey value:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
For 32-bit applications that are running on 64-bit systems, update the following subkey value:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\.NETFramework\\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
#### Update SQL Server and client components

Microsoft SQL Server 2016 supports TLS 1.1 and TLS 1.2.
Earlier versions and dependent libraries might require updates. For more information, see [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

> [!NOTE]
> KB 3135244 also describes requirements for SQL Server client components. Update each component that's used in your environment.

#### Update Windows and WinHTTP

Windows 10, Windows 8.1, Windows Server 2016, and Windows Server 2012 R2 support TLS 1.2 for client-server communications over WinHTTP out of the box.

Windows 8.0, Windows Server 2012, and earlier versions of Windows don't enable TLS 1.1 or 1.2 by default for client-server communications through HTTPS. For these earlier versions of Windows, you should install [Update 3140245](https://support.microsoft.com/help/3140245) to enable TLS 1.1 and TLS 1.2 as the default secure protocols in WinHTTP in Windows, and set the following registry values.

Verify that the `DefaultSecureProtocols` registry setting is `0xAA0`, as follows:

```
HKEY_LOCAL_MACHINE\SOFTWARE\
   \Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```
> [!NOTE]
> This change requires a restart.

#### Update Windows Server Update Services

To support TLS 1.2 for client-server communications in WSUS on Windows Server 2012 and Windows Server 2012 R2, you must apply the following update on the WSUS server:
- For WSUS server that's running Windows Server 2012, apply [update 4022721](https://support.microsoft.com/help/4022721) or a later update.
- For WSUS server that's running Windows Server 2012 R2, apply [update 4022720](https://support.microsoft.com/help/4022720) or a later update.

## Tasks required for Configuration Manager features and scenarios
This section describes the dependencies for specific Configuration Manager features and scenarios. To determine the next steps, locate the items that apply to your environment, and then verify the dependencies by using the steps provided earlier in [Enable TLS 1.2 for dependent components](#enable-tls-12-for-dependent-components).

|Feature or scenario|Update tasks|
|--- |--- |
|Site servers (central, primary, or secondary)|[Update .NET Framework](#update-net-framework-to-support-tls-12), and verify strong cryptography settings.|
|SMS Provider|[Update SQL Server and its client components](#update-sql-server-and-client-components) as appropriate for each SMS provider.|
|Site system roles|[Update .NET Framework](#update-net-framework-to-support-tls-12), and verify strong cryptography settings. [Update SQL Server and its client components](#update-sql-server-and-client-components).|
|Service connection point application catalog|[Update .NET Framework](#update-net-framework-to-support-tls-12), and verify strong cryptography settings.|
|SRS reporting point|[Update .NET Framework](#update-net-framework-to-support-tls-12) on the site server and the SRS servers. Restart the SMS_Executive service as necessary.|
|Admin console|[Update .NET Framework](#update-net-framework-to-support-tls-12), and verify strong cryptography settings.|
|SCCM client with HTTPS site system roles|[Update Windows to support TLS 1.2 for client-server communications by using WinHTTP](#update-windows-and-winhttp).|
|Software Center|[Update .NET Framework](#update-net-framework-to-support-tls-12), and verify strong cryptography settings.|
|Software Update Point|[Update WSUS](#update-windows-server-update-services).|
|Management Points|Update to the latest SQL Server native client to enable Configuration Manager to talk to the latest TLS 1.2-enabled SQL Server components. See the "Client component downloads" table in [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244).|

## Known issues

This section provides advice for common issues that occur when you enable TLS 1.2 support.

### FIPS security policy enabled

If the FIPS security policy setting is enabled for either the client or a server, Secure Channel (Schannel) negotiation can cause TLS 1.0 to be used even if the protocol is disabled using the registry.

To investigate, enable Secure Channel event logging, and then review Schannel events in the system log. For related information, see [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### SQL Server communication failure

If SQL Server communication fails and returns an **SslSecurityError** error, verify the following:
- .NET Framework is updated and has strong cryptography enabled on each machine.
- SQL Server is updated on the host server.
- SQL client components are updated on the site servers, SMS provider, site role servers, and all other systems that communicate with SQL server.

### Configuration Manager client communication failures

If Configuration Manager client doesn't communicate with site role endpoints, such as distribution points, management points, and state migration points, verify that Windows has been updated to support TLS 1.2 for client-server communication by using WinHTTP.

### SRS Reporting Point fails and returns an expected error

If the SRS Reporting Point doesn't configure reports, check *SRSRP.log* for the following error entry:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

To resolve this issue, follow these steps:

1. Verify that .NET Framework is updated and has strong cryptography enabled on all relevant computers.
1. Verify that the SMS_Executive service has been restarted after any updates are installed.

### Application catalog doesn't initialize

If the application catalog doesn't initialize, check the *ServicePortalWebSite.svclog* file for the following error entry:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

To resolve this issue, follow these steps:
1. Verify that .NET Framework is updated and has strong cryptography enabled on all relevant computers.
1. In the C:\Windows\System32\InetSrv folder of the application catalog server, create a *W2SP.exe.config* file by running the following script: 

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <configuration>
     <runtime>
     <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
     </runtime>
   </configuration>
   ```
   > [!NOTE]
   > This is the default file that would be created if the application was built by using .NET Framework 4.6.3.
1. Use HTTPS transport security for Application Catalog roles.

   > [!NOTE]
   > When you use HTTP message security for Application Catalog roles, WCF is hard-coded to use SSL 3.0 and TLS 1.0 only. This prevents the use of TLS 1.2.
1. If any changes were made, restart the computer.


### Software Center or browser doesn't communicate with Application Catalog

To resolve communication failures between Application Catalog and Software Center or the browser, verify the following conditions:

- .NET Framework is updated and has strong cryptography enabled on each computer.
- The browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default.
- All computers were restarted after the changes were made.

   > [!NOTE]
   > To make Software Center work with TLS 1.2-enforced server for user-available apps, we recommend you remove app catalog roles and let Software Center communicate with management point.

### Service Connection Point upload failures

If the Service Connection Point doesn't upload data to SCCMConnectedService, verify that .NET Framework is updated and has strong cryptography enabled on each computer. Remember to restart the computers after the changes are made.

### Admin Console displays Intune onboarding dialog box

If the Intune onboarding dialog box appears when the Admin Console tries to connect to the Intune portal, verify that .NET Framework is updated and has strong cryptography enabled on each computer.  Remember to restart the computers after the changes are made.

### Admin Console displays failure to sign in to Azure

If the Azure Services onboarding dialog box immediately fails after you select **Sign in** when you try to create Azure AD applications, verify that .NET Framework is updated and that strong cryptography is enabled. A restart is required for these changes to take effect.

### WSUS communication failures

To resolve WSUS communication failures in Windows Server 2012 and Windows Server 2012 R2, apply the following update on the WSUS server:
- For WSUS server that's running Windows Server 2012, apply [update 4022721](https://support.microsoft.com/help/4022721) or a later update.
- For WSUS server that's running Windows Server 2012 R2, apply [update 4022720](https://support.microsoft.com/help/4022720) or a later update.
## See Also

[Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)