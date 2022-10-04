---
title: Supported configurations
titleSuffix: Configuration Manager
description: Identify key configurations and requirements so you can plan, deploy, and maintain a functional Configuration Manager deployment.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Supported configurations for Configuration Manager

*Applies to: Configuration Manager (current branch)*

As an on-premises solution, Configuration Manager makes use of your servers, clients, network configurations, and other products like Microsoft Intune, SQL Server, and Azure.

This information can help you identify key configurations, requirements, and limitations. Use it to plan, deploy, and maintain a functional Configuration Manager deployment. This information is specific to the infrastructure for Configuration Manager sites, hierarchies, and managed devices.

When a Configuration Manager feature or capability requires more specific configurations, see the feature-specific documentation. It's supplemental to the more general configuration details.

The products and technologies described in these articles are supported by Configuration Manager. However, their inclusion in this content doesn't imply an extension of support for any product beyond that product's individual support lifecycle. Products that are beyond their support lifecycle aren't supported for use with Configuration Manager. This statement includes any products that are covered under the [Extended Security Updates (ESU)](/lifecycle/faq/extended-security-updates) program. For more information about Extended Security Updates in Configuration Manager, see [Supported OS versions for clients and devices for Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]
> For more general information, see the [Microsoft Support Lifecycle](/lifecycle).

Products and product versions that aren't listed in these articles aren't supported with Configuration Manager unless they're announced on the [Configuration Manager blog](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog). The content on this blog may precede an update to this documentation.

- [Site and site system prerequisites](site-and-site-system-prerequisites.md): Learn about required configurations on a Windows Server to support different site types and site system roles.

- [Supported operating systems for site system servers](supported-operating-systems-for-site-system-servers.md): Learn about which operating systems you can use as a site server or site system server.

- [Supported operating systems for clients and devices](supported-operating-systems-for-clients-and-devices.md): Learn about which operating systems you can manage with Configuration Manager. These include Windows, Windows Embedded, macOS, and mobile devices.

- [Support for Windows 11](support-for-windows-11.md) and [Support for Windows 10](support-for-windows-10.md): Learn about the Windows 11 and Windows 10 versions that are supported as clients.

- [Support for the Windows ADK](support-for-windows-adk.md): Learn about the Windows Assessment and Deployment Kit (Windows ADK) version that are supported with Configuration Manager current branch for OS deployment.

- [Supported operating systems for the console](supported-operating-systems-consoles.md): Learn about which operating systems can host the Configuration Manager console.

- [Support for SQL Server versions](support-for-sql-server-versions.md): Learn about which versions of SQL Server can host the site database and reporting database. It also includes required and optional configurations that you can use with SQL Server.

- [High-availability options](../../servers/deploy/configure/high-availability-options.md): Learn about the options you can implement when designing your environment to help maintain a high level of available service for Configuration Manager.

- [Support for Active Directory domains](support-for-active-directory-domains.md): Learn about the supported Active Directory domain configurations that Configuration Manager requires and supports.

- [Support for Windows features and networks](support-for-windows-features-and-networks.md): Learn about supported Windows technologies and limitations for use with Configuration Manager. For example, Windows BranchCache and data deduplication.

- [Support for virtualization environments](support-for-virtualization-environments.md): Learn more about how to use supported virtual machine technologies.

- [FAQ for Configuration Manager on Azure](../../understand/configuration-manager-on-azure.yml): Answers to common questions about using Configuration Manager on an Azure environment.

Use the following articles to understand Configuration Manager size, scale, and performance:

- [Size and scale numbers](size-and-scale-numbers.md): Learn about how many sites, roles per site, and clients are supported in different hierarchy designs.

- [Recommended hardware](recommended-hardware.md): Learn about guidelines that can help you identify the right hardware and configurations to host your Configuration Manager sites and key services.

- [Site size and performance guidelines](site-size-performance-guidelines.md): Site size-related performance test results, methodology, and guidance.

- [Site size and performance FAQ](../../understand/site-size-performance-faq.yml): Answers to common Configuration Manager questions about site sizing and performance.
