---
title: Enable Transport Layer Security (TLS) 1.2 on the site servers and remote site systems
titleSuffix: Configuration Manager
description: Information about how to enable TLS 1.2 for Configuration Manager site servers.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual


ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
---

# How to enable TLS 1.2 on the site servers and remote site systems

*Applies to: Configuration Manager (Current Branch)*

When enabling TLS 1.2 for your Configuration Manager environment, start with [enabling TLS 1.2 for the clients](enable-tls-1-2-client.md) first. Then, enable TLS 1.2 on the site servers and remote site systems second. Finally, test client to site system communications before potentially disabling the older protocols on the server side. The following tasks are needed for enabling TLS 1.2 on the site servers and remote site systems:

- Ensure that TLS 1.2 is enabled as a protocol for SChannel at the operating system level
- Update and configure the .NET Framework to support TLS 1.2
- Update SQL Server and client components
- Update Windows Server Update Services (WSUS)

For more information about dependencies for specific Configuration Manager features and scenarios, see [About enabling TLS 1.2](enable-tls-1-2.md). 

## <a name="bkmk_protocol"></a> Ensure that TLS 1.2 is enabled as a protocol for SChannel at the operating system level

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="bkmk_net"></a> Update and configure the .NET Framework to support TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="bkmk_sql"></a> Update SQL Server and client components

Microsoft SQL Server 2016 and later support TLS 1.1 and TLS 1.2. Earlier versions and dependent libraries might require updates. For more information, see [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Secondary site servers need to use at least SQL Server 2016 Express with Service Pack 2 (13.2.50.26) or later.

### <a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) also describes requirements for SQL Server client components.

Make sure to also update the SQL Server Native Client to at least version SQL 2012 SP4 (11.*.7001.0). Starting in version 1810, this requirement is a [prerequisite check (warning)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

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


## <a name="bkmk_wsus"></a> Update Windows Server Update Services (WSUS)

To support TLS 1.2 in earlier versions of WSUS, install the following update on the WSUS server:

- For WSUS server that's running Windows Server 2012, install [update 4022721](https://support.microsoft.com/help/4022721) or a later rollup update.
- For WSUS server that's running Windows Server 2012 R2, install [update 4022720](https://support.microsoft.com/help/4022720) or a later rollup update.

Starting in Windows Server 2016, TLS 1.2 is supported by default for WSUS.  TLS 1.2 updates are only needed on Windows Server 2012 and Windows Server 2012 R2 WSUS servers.

## Next steps

- [Common issues when enabling TLS 1.2](enable-tls-1-2-troubleshoot.md)
