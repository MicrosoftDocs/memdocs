---
title: Enable Transport Layer Security (TLS) 1.2 overview
titleSuffix: Configuration Manager
description: Overview of how to enable TLS 1.2 for Configuration Manager.
ms.date: 10/18/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: concept-article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to enable TLS 1.2

*Applies to: Configuration Manager (Current Branch)*

Transport Layer Security (TLS), like Secure Sockets Layer (SSL), is an encryption protocol intended to keep data secure when being transferred over a network. These articles describe steps required to ensure that Configuration Manager secure communication uses the TLS 1.2 protocol. These articles also describe update requirements for commonly used components and troubleshooting common problems.

## Enabling TLS 1.2

Configuration Manager relies on many different components for secure communication. The protocol that's used for a given connection depends on the capabilities of  the relevant components on both the client and server side. If any component is out-of-date or not properly configured, the communication might use an older, less secure protocol. To correctly enable Configuration Manager to support TLS 1.2 for all secure communications, you must enable TLS 1.2 for all required components. The required components depend on your environment and the Configuration Manager features that you use.

> [!IMPORTANT]
> Start this process with the clients, especially previous versions of Windows. Before enabling TLS 1.2 and disabling the older protocols on the Configuration Manager servers, make sure that all clients support TLS 1.2. Otherwise, the clients can't communicate with the servers and can be orphaned.


## Tasks for Configuration Manager clients, site servers, and remote site systems

To enable TLS 1.2 for components that Configuration Manager depends on for secure communication, you'll need to do multiple tasks on both the clients and the site servers.

### Enable TLS 1.2 for Configuration Manager clients

- [Update Windows and WinHTTP on Windows 8.0, Windows Server 2012 (non-R2) and earlier](enable-tls-1-2-client.md#bkmk_winhttp)
- [Ensure that TLS 1.2 is enabled as a protocol for SChannel at the OS level](enable-tls-1-2-client.md#bkmk_protocol)
- [Update and configure the .NET Framework to support TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### Enable TLS 1.2 for Configuration Manager site servers and remote site systems

- [Ensure that TLS 1.2 is enabled as a protocol for SChannel at the OS level](enable-tls-1-2-server.md#bkmk_protocol)
- [Update and configure the .NET Framework to support TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [Update SQL Server and the SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Update Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## Features and scenario dependencies

This section describes the dependencies for specific Configuration Manager features and scenarios. To determine the next steps, locate the items that apply to your environment.

|Feature or scenario|Update tasks|
|--- |--- |
|Site servers (central, primary, or secondary)| - [Update .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - Verify strong cryptography settings|
|Site database server|[Update SQL Server and its client components](enable-tls-1-2-server.md#bkmk_sql)|
|Secondary site servers|[Update SQL Server and its client components](enable-tls-1-2-server.md#bkmk_sql) to a compliant version of SQL Server Express|
|Site system roles| - [Update .NET Framework](enable-tls-1-2-server.md#bkmk_net) and verify strong cryptography settings <br/> - [Update SQL Server and its client components](enable-tls-1-2-server.md#bkmk_sql) on roles that require it, including the [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Reporting services point|- [Update .NET Framework](enable-tls-1-2-server.md#bkmk_net) on the site server, the SQL Server Reporting Services servers, and any computer with the console<br/> - Restart the SMS_Executive service as necessary|
|Software update point|[Update WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|Cloud management gateway|[Enforce TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#enforce-tls-12)|
|Configuration Manager console| - [Update .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - Verify strong cryptography settings|
|Configuration Manager client with HTTPS site system roles|[Update Windows to support TLS 1.2 for client-server communications by using WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Software Center| - [Update .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - Verify strong cryptography settings|
|Windows 7 clients| *Before* you enable TLS 1.2 on any server components, [update Windows to support TLS 1.2 for client-server communications by using WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). If you enable TLS 1.2 on server components first, you can orphan earlier versions of clients.|

## Frequently asked questions

### Why use TLS 1.2 with Configuration Manager?

TLS 1.2 is more secure than the previous cryptographic protocols such as SSL 2.0, SSL 3.0, TLS 1.0, and TLS 1.1. Essentially, TLS 1.2 keeps data being transferred across the network more secure.

### Where does Configuration Manager use encryption protocols like TLS 1.2?

There are basically five areas that Configuration Manager uses encryption protocols like TLS 1.2:

- Client communications to IIS-based site server roles when the role is configured to use HTTPS. Examples of these roles include distribution points, software update points, and management points.
- Management point, SMS Executive, and SMS Provider communications with SQL. Configuration Manager always encrypts SQL Server communications.
- Site Server to WSUS communications if WSUS is configured to use HTTPS.
- The Configuration Manager console to SQL Server Reporting Services (SSRS) if SSRS is configured to use HTTPS.
- Any connections to internet-based services. Examples include the cloud management gateway (CMG), the service connection point sync, and sync of update metadata from Microsoft Update.

### What determines which encryption protocol is used?

HTTPS will always negotiate the highest protocol version that is supported by both the client and server in an encrypted conversation. On establishing a connection, the client sends a message to the server with its highest available protocol. If the server supports the same version, it sends a message using that version. This negotiated version is the one that is used for the connection. If the server doesn't support the version presented by the client, the server message will specify the highest version it can use. For more information about the TLS Handshake protocol, see [Establishing a Secure Session by using TLS](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### What determines which protocol version the client and server can use?

Generally, the following items can determine which protocol version is used:

- The application can dictate which specific protocol versions to negotiate.
  - Best practice dictates to avoid hard coding specific protocol versions at the application level and to follow the configuration defined at the component and OS protocol level.
  - Configuration Manager follows this best practice.
- For applications written using the .NET Framework, the default protocol versions depend on the version of the framework they were compiled upon.  
  - .NET versions before 4.6.3 did not include TLS 1.1 and 1.2 in the list of protocols for negotiation, by default.
- Applications that use WinHTTP for HTTPS communications, like the Configuration Manager client, depend on the OS version, patch level, and configuration for protocol version support.


## Additional resources

- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)
- [Transport layer security (TLS) best practices with the .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/topic/kb3135244-tls-1-2-support-for-microsoft-sql-server-e4472ef8-90a9-13c1-e4d8-44aad198cdbe)

## Next steps

- [Enable TLS 1.2 on clients](enable-tls-1-2-client.md)
- [Enable TLS 1.2 on the site servers](enable-tls-1-2-server.md)
