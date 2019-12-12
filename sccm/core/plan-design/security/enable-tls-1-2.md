---
title: Enable Transport Layer Security (TLS) 1.2 overview
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

*Applies to: Configuration Manager (Current Branch)*

Transport Layer Security (TLS), like Secure Sockets Layer (SSL), is an encryption protocol intended to keep data secure when being transferred over a network. These articles describe steps required to ensure that Configuration Manager secure communication uses the TLS 1.2 protocol. These articles also describe update requirements for commonly used components and troubleshooting common problems.

## Enabling TLS 1.2

Configuration Manager relies on a number of different components for secure communication. The protocol that's used for a given connection depends on the capabilities of  the relevant components on both the client and server side. If any component is out-of-date or not properly configured, the communication might use an older, less secure protocol. To correctly enable Configuration Manager to support TLS 1.2 for all secure communications, you must enable TLS 1.2 for all required components. The required components depend on your environment and the Configuration Manager features that you use.

> [!IMPORTANT]
> Start this process with the clients, especially previous versions of Windows. Before enabling TLS 1.2 and disabling the older protocols on the Configuration Manager servers, make sure that all clients support TLS 1.2. Otherwise, the clients can't communicate with the servers and can be orphaned.


## Tasks for Configuration Manager clients, site servers, and remote site systems

To enable TLS 1.2 for components that Configuration Manager depends on for secure communication, you'll need to do multiple tasks on both the clients and the site servers.

### Enable TLS 1.2 for Configuration Manager clients

- [Update Windows and WinHTTP on Windows 8.0, Windows Server 2012 (non-R2) and earlier](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_winhttp)
- [Ensure that TLS 1.2 is enabled as a protocol for SChannel at the Operating System level](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_protocol)
- [Update and configure the .NET Framework to support TLS 1.2](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net)


### Enable TLS 1.2 for Configuration Manager site servers and remote site systems

- [Ensure that TLS 1.2 is enabled as a protocol for SChannel at the Operating System level](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_protocol)
- [Update and configure the .NET Framework to support TLS 1.2](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_net)
- [Update SQL Server and the SQL Native Client](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql)
- [Update Windows Server Update Services (WSUS)](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_wsus)


## Features and scenario dependencies

This section describes the dependencies for specific Configuration Manager features and scenarios. To determine the next steps, locate the items that apply to your environment.

|Feature or scenario|Update tasks|
|--- |--- |
|Site servers (central, primary, or secondary)| - [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-server##bkmk_net)<br/> - Verify strong cryptography settings|
|Site database server|[Update SQL Server and its client components](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql)|
|Secondary site servers|[Update SQL Server and its client components](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql) to a compliant version of SQL Express|
|Site system roles| - [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_net) and verify strong cryptography settings <br/> - [Update SQL Server and its client components](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql) on roles that require it, including the [SQL Server Native Client](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_sql-client)|
|Reporting services point|- [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_net) on the site server, the SQL Reporting Services servers, and any computer with the console<br/> - Restart the SMS_Executive service as necessary|
|Software update point|[Update WSUS](/sccm/core/plan-design/security/enable-tls-1-2-server#bkmk_wsus)|
|Cloud management gateway|[Enforce TLS 1.2](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway#bkmk_tls)|
|Configuration Manager console| - [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net)<br/> - Verify strong cryptography settings|
|Configuration Manager client with HTTPS site system roles|[Update Windows to support TLS 1.2 for client-server communications by using WinHTTP](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_winhttp)|
|Software Center| - [Update .NET Framework](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_net)<br/> - Verify strong cryptography settings|
|Windows 7 clients| *Before* you enable TLS 1.2 on any server components, [update Windows to support TLS 1.2 for client-server communications by using WinHTTP](/sccm/core/plan-design/security/enable-tls-1-2-client#bkmk_winhttp). If you enable TLS 1.2 on server components first, you can orphan earlier versions of clients.|

## Frequently asked questions

### Why use TLS 1.2 with Configuration Manager?

TLS 1.2 is more secure than the previous cryptographic protocols such as SSL 2.0, SSL 3.0, TLS 1.0, and TLS 1.1. Essentially, TLS 1.2 keeps data being transferred across the network more secure.

### Where does Configuration Manager use encryption protocols like TLS 1.2?

There are basically five areas that Configuration Manager uses encryption protocols like TLS 1.2:

1. Client communications to IIS-based site server roles when the role is configured to use HTTPS. Examples of these roles include distribution points, software update points, and management points.
2. Management point, SMS Executive, and SMS Provider communications with SQL. Configuration Manager always encrypts SQL communications.
3. Site Server to WSUS communications if WSUS is configured to use HTTPS.
4. The Configuration Manager console to SQL Reporting Services (SSRS) if SSRS is configured to use HTTPS.
5. Any connections to internet-based services. Examples include the cloud management gateway (CMG), the service connection point sync, and sync of update metadata from Microsoft Update.

### What determines which encryption protocol is used?

HTTPS will always negotiate the highest protocol version that is supported by both the client and server in an encrypted conversation. On establishing a connection, the client sends a message to the server with its highest available protocol. If the server supports the same version, it sends a message using that version. This negotiated version is the one that is used for the connection. If the server doesn't support the version presented by the client, the server message will specify the highest version it can use. For more information about the TLS Handshake protocol, see [Establishing a Secure Session by using TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### What determines which protocol version the client and server can use?

Generally, the following items can determine which protocol version is used:

- The application can dictate which specific protocol versions to negotiate.
  - Best practice dictates to avoid hard coding specific protocol versions at the application level and to follow the configuration defined at the component and Operating System protocol level.
  - Configuration Manager follows this best practice.
- For applications written using the .NET Framework, the default protocol versions depend on the version of the framework they were compiled upon.  
  - .NET versions before 4.6.3 did not include TLS 1.1 and 1.2 in the list of protocols for negotiation, by default.
- Applications that use WinHTTP for HTTPS communications, like the Configuration Manager client, depend on the Operating System version, patch level and configuration for protocol version support.


## Additional resources

- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)
- [Transport layer security (TLS) best practices with the .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## Next steps

- [Enable TLS 1.2 on clients](/sccm/core/plan-design/security/enable-tls-1-2-client)
- [Enable TLS 1.2 on the site servers](/sccm/core/plan-design/security/enable-tls-1-2-server)
