---
title: Common issues when enabling Transport Layer Security (TLS) 1.2
titleSuffix: Configuration Manager
description: Describes common issues when enabling Transport Layer Security (TLS) 1.2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual


ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
---

# Common issues when enabling TLS 1.2

This article provides advice for common issues that occur when you enable TLS 1.2 support in Configuration Manager.

## Unsupported platforms

The following client platforms are supported by Configuration Manager but aren't supported in a TLS 1.2 environment:

- Windows Server 2008
- Windows CE
- Apple OS X
- Windows 10 devices managed with on-premises MDM

## Reports don't show in the console

If reports don't show in the Configuration Manager console, make sure to update the computer on which you're running the console. [Update the .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net), and enable strong cryptography.

## FIPS security policy enabled

If you enable the FIPS security policy setting for either the client or a server, Secure Channel (Schannel) negotiation can cause them to use TLS 1.0. This behavior happens even if you disable the protocol in the registry.

To investigate, enable Secure Channel event logging, and then review Schannel events in the system log. For more information, see [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## SQL Server communication failure

If SQL Server communication fails and returns an **SslSecurityError** error, verify the following settings:

- [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_net), and enable strong cryptography on each machine
- [Update SQL Server](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql) on the host server
- [Update SQL client components](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql-client) on all systems that communicate with SQL. For example, the site servers, SMS provider, and site role servers.

## Configuration Manager client communication failures

If the Configuration Manager client doesn't communicate with site roles, verify that you [updated Windows](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_winhttp) to support TLS 1.2 for client-server communication by using WinHTTP. Common site roles include distribution points, management points, and state migration points.

## Reporting services point fails and returns an expected error

If the reporting services point doesn't configure reports, check the **SRSRP.log** for the following error entry:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

To resolve this issue, follow these steps:

1. [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net), and enable strong cryptography on all relevant computers.

1. After you install any updates, restart the SMS_Executive service.

## Application catalog doesn't initialize

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

If the application catalog doesn't initialize, check the **ServicePortalWebSite.svclog** file for the following error entry:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

To resolve this issue, follow these steps:

1. [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net), and enable strong cryptography on all relevant computers.

1. In the `%WinDir%\System32\InetSrv` folder of the application catalog server, create a **W2SP.exe.config** file with the following contents:

    ``` XML
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

## Software Center or browser doesn't communicate with the application catalog

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

The best method to make Software Center work with for user-available apps in a TLS 1.2-enabled site, remove the application catalog role. Then let Software Center communicate directly with a management point. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

If you need to resolve communication failures between the application catalog and Software Center, verify the following conditions:

- [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net), and enable strong cryptography on each computer.

- After you make the changes, restart all affected computers.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## Service connection point upload failures

If the service connection point doesn't upload data to SCCMConnectedService, [update the .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_net), and enable strong cryptography on each computer. After you make the changes, remember to restart the computers.

## Configuration Manager console displays Intune onboarding dialog box

If the Intune onboarding dialog box appears when the console tries to connect to the Intune portal, [update the .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net), and enable strong cryptography on each computer. After you make the changes, remember to restart the computers.

## Configuration Manager console displays failure to sign in to Azure

When you try to create applications in Azure Active Directory (Azure AD), if the Azure Services onboarding dialog box immediately fails after you select **Sign in**, [update the .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_net), and enable strong cryptography. After you make the changes, remember to restart the computers.

## Configuration Manager cloud services and TLS 1.2

The Azure virtual machines used by the cloud management gateway and cloud distribution points support TLS 1.2. Supported client versions automatically use TLS 1.2.

The **SMSAdminui.log** may contain an error similar to the following example:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

In the System EventLog, SChannel EventID 36874 may be logged with the following description: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## Additional resources

- [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)

## Next steps

- [Enable TLS 1.2 on clients](/sccm/core/plan-design/security/enable-tls-1-2-client)
- [Enable TLS 1.2 on the site servers and remote site systems](/sccm/core/plan-design/security/enable-tls-1-2-server)

