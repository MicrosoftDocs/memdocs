---
title: Enable TLS 1.2 overview
titleSuffix: Configuration Manager
description: Overview of how to enable TLS 1.2 for Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
---

# How to enable TLS 1.2

*Applies to: System Center Configuration Manager (Current Branch)*

These articles describe how to enable TLS 1.2 for Configuration Manager, including for individual components. Update requirements for commonly used features, and troubleshooting of some common problems are also described in these articles.

Configuration Manager relies on many different components for secure communication. The protocol that's used for a given connection depends on the capabilities of all the required components. If one component is out-of-date, the communication might use an older, less secure protocol. To correctly enable Configuration Manager to support TLS 1.2, first enable TLS 1.2 for all required components. The required components depend on your environment and the Configuration Manager features that you use.

Start this process with the clients, especially previous versions of Windows. Before enabling TLS 1.2 on the Configuration Manager servers, make sure that all clients support TLS 1.2. Otherwise, the clients won't be able to communicate with the servers and can be orphaned.


## Tasks for features and scenarios

To enable TLS 1.2 for components that Configuration Manager depends on for secure communication, you must:

- [Enable TLS 1.2 protocol as a security provider](#enable-tls-12-protocol-as-a-security-provider)
- [Update .NET Framework to support TLS 1.2](#update-net-framework-to-support-tls-12)
- [Update SQL Server and client components](#update-sql-server-and-client-components)
- [Update Windows and WinHTTP on Windows 8.0, Windows Server 2012 R2 and earlier](#update-windows-and-winhttp)
- [Update Windows Server Update Services (WSUS)](#update-windows-server-update-services-wsus)

This section describes the dependencies for specific Configuration Manager features and scenarios. To determine the next steps, locate the items that apply to your environment.

|Feature or scenario|Update tasks|
|--- |--- |
|Site servers (central, primary, or secondary)| - [Update .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verify strong cryptography settings|
|Site database server|[Update SQL Server and its client components](#update-sql-server-and-client-components)|
|Secondary site servers|[Update SQL Server and its client components](#update-sql-server-and-client-components) to a compliant version of SQL Express|
|Site system roles| - [Update .NET Framework](#update-net-framework-to-support-tls-12) and verify strong cryptography settings <br/> - [Update SQL Server and its client components](#update-sql-server-and-client-components) on roles that require it, including the [SQL Server Native Client](#sql-server-native-client)|
|Reporting services point|- [Update .NET Framework](#update-net-framework-to-support-tls-12) on the site server, the SQL Reporting Services servers, and any computer with the console<br/> - Restart the SMS_Executive service as necessary|
|Software update point|[Update WSUS](#update-windows-server-update-services-wsus)|
|Cloud management gateway|[Enforce TLS 1.2](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway#bkmk_tls)|
|Configuration Manager console| - [Update .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verify strong cryptography settings|
|Configuration Manager client with HTTPS site system roles|[Update Windows to support TLS 1.2 for client-server communications by using WinHTTP](#update-windows-and-winhttp)|
|Software Center| - [Update .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verify strong cryptography settings|
|Windows 7 clients| *Before* you enable TLS 1.2 on any server components, [update Windows to support TLS 1.2 for client-server communications by using WinHTTP](#update-windows-and-winhttp). If you enable TLS 1.2 on server components first, you can orphan earlier versions of clients.|








## Additional resources

- [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)

## Next steps

- [Enable TLS 1.2 on clients](./enable-tls-1-2-client)
- [Enable TLS 1.2 on the site servers](./enable-tls-1-2-server)
