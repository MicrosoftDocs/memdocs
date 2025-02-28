---
title: Prepare Windows Servers
titleSuffix: Configuration Manager
description: Make sure that a computer meets prerequisites for use as a site server or a site system server for Configuration Manager.
ms.date: 08/02/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Prepare Windows Servers to support Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before you can use a Windows computer as a site system server for Configuration Manager, it must meet the prerequisites for its intended use. These prerequisites often include one or more Windows features or roles. Because the method to enable Windows features and roles differs among OS versions, refer to the documentation for your OS version for detailed information.

The information in this article provides an overview of the types of Windows configurations that are required to support Configuration Manager site systems. For configuration details for specific site system roles, see [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md).

## Windows features and roles

When you set up Windows features and roles on a computer, you might be required to reboot the computer to complete that configuration. So before you install a Configuration Manager site or site system server, identify computers that will host specific site system roles.

### Features

The following Windows features are required on certain site system servers. Set them up before you install a site system role on that computer.

- **.NET Framework**: Different site system roles require different versions of .NET Framework.

- **Background Intelligent Transfer Services (BITS)**: Management points require BITS to support communication with managed devices. This feature includes all automatically selected options.

- **BranchCache**: Distribution points can be set up with BranchCache to support clients.

- **Data Deduplication**: Distribution points can be set up with and benefit from data deduplication.

- **Remote Differential Compression (RDC)**: Each computer that hosts a site server or a distribution point requires RDC. RDC is used to generate package signatures and compare digital signatures.

### Roles

The following Windows roles are required to support specific functionality, like software updates and OS deployments. IIS is required by the most common site system roles.

- **Network Device Enrollment Service** (under Active Directory Certificate Services): This Windows role is a prerequisite to use certificate profiles in Configuration Manager.

- **Web server (IIS)**: The following site system roles use IIS:

  - Distribution point
  - Enrollment point
  - Enrollment proxy point
  - Fallback status point
  - Management point
  - Software update point
  - State migration point

  The minimum version of IIS that's required is the version that's supplied with the OS of the site server.

- **Windows Deployment Services**: This role is used with OS deployment.

- **Windows Server Update Services**: This role is required for software updates.

## IIS request filtering for distribution points

By default, IIS uses request filtering to block several file name extensions and folder locations from access by HTTP or HTTPS communication. On a distribution point, this configuration prevents clients from downloading packages that have blocked extensions or folder locations.

When your package source files have extensions that are blocked in IIS by your request filtering configuration, set up request filtering to allow them. Use the IIS Manager to [edit the request filtering feature](/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)) on your distribution point computers.

Additionally, the following file name extensions are used by Configuration Manager for packages and applications. Make sure that your request filtering configurations don't block these file extensions:

- .PCK
- .PKG
- .STA
- .TAR

For example, source files for a software deployment might include a folder named **bin** or have a file that has the **.mdb** file name extension.

- By default, IIS request filtering blocks access to these elements. **Bin** is blocked as a Hidden Segment and **.mdb** is blocked as a file name extension.

- When you use the default IIS configuration on a distribution point, clients that use BITS fail to download this software deployment from the distribution point and indicate that they're waiting for content.

- To let the clients download this content, on each applicable distribution point, edit **Request Filtering** in IIS Manager. Allow access to the file extensions and folders that are in the packages and applications that you deploy.

> [!IMPORTANT]
> Edits to the request filter can increase the attack surface of the computer.
>
> - Edits that you make at the server level apply to all websites on the server.
> - Edits that you make to individual websites apply to only that website.
>
> For best security, run Configuration Manager on a dedicated web server. If you need to run other applications on the web server, use a custom website for Configuration Manager. For information, see [Websites for site system servers](websites-for-site-system-servers.md).

## HTTP verbs

For more information, see [Configure request filtering in IIS](/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)#http-verbs).

### Management points

To make sure that clients can successfully communicate with a management point, on the management point server make sure IIS allows the following HTTP verbs:

- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

### Distribution points

Distribution points require that IIS allows the following HTTP verbs:

- GET
- HEAD
- PROPFIND
