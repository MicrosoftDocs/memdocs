---
title: Prerequisites for software updates
titleSuffix: Configuration Manager
description: Learn about prerequisites for software updates in Configuration Manager.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 06/20/2024
ms.topic: conceptual
ms.service: configuration-manager
ms.subservice: software-updates
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz
ms.collection: tier3
---

# Prerequisites for software updates in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article lists the prerequisites for software updates in Configuration Manager. For each of the prerequisites, the external dependencies and internal dependencies are listed in separate tables.

## Software update dependencies that are external to Configuration Manager

The following sections list the external dependencies for software updates.

### Internet Information Services

Internet Information Services (IIS) must be installed on the site system servers to run the software update point, the management point, and the distribution point. For more information, see [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md).

### Windows Server Update Services

Windows Server Update Services (WSUS) is needed for software updates synchronization and for the software updates applicability scan on clients. The WSUS server must be installed before you create the software update point role. The following versions of WSUS are supported for a software update point:

- WSUS 10.0.14393 (role in Windows Server 2016) (2023-02 Cumulative Update, or a later cumulative update)
- WSUS 10.0.17763 (role in Windows Server 2019) (Requires Configuration Manager 1810 or later) (2023-02 Cumulative Update, or a later cumulative update)
- WSUS 10.0.20348 (role in Windows Server 2022) (2023-02 Cumulative Update, or a later cumulative update)

> [!NOTE]
>
> - On October 10th, 2023, Windows Server 2012 and Windows Server 2012 R2 entered the Extended Support Updates phase. Microsoft will no longer provide support for Configuration Manager site servers or roles installed to these Operating Systems. For more information, see **[Extended Security Updates and Configuration Manager](/mem/configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)**.
>
> - Starting March 28, 2023, on-premises Windows 11, version 22H2 devices will receive quality updates via the Unified Update Platform (UUP). The 2023-02 cumulative update is required for UUP to work. If you're unable to install these updates, you can [manually add the required MIME types for UUP](/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#manually-add-the-required-mime-types-for-uup) to the WSUS server. If you encounter a `Cannot add duplicate collection entry of type 'mimeMap'` error, see [Cannot add duplicate collection entry of type mimeMap](/windows-server/administration/windows-server-update-services/manage/wsus-messages-and-troubleshooting-tips#cannot-add-duplicate-collection-entry-of-type-mimemap).
>
> - When you have multiple software update points at a site, ensure that they're all running the same version of WSUS.

### WSUS Administration Console

The WSUS Administration Console is required on the Configuration Manager site server when the software update point is on a remote site system server and WSUS isn't already installed on the site server.

> [!IMPORTANT]
>
> - The WSUS version on the site server must be the same as the WSUS version that's running on the software update points.
> - Don't use WSUS Administration Console to configure WSUS settings. Configuration Manager connects to the instance of WSUS that is running on the software update point and configures the appropriate settings.

### Windows Update Agent

The Windows Update Agent (WUA) client is required on clients so that they can connect to the WSUS server. WUA retrieves the list of software updates that must be scanned for compliance.

When you install Configuration Manager, the latest version of WUA is downloaded. Then, when you install the Configuration Manager client, WUA is upgraded if necessary. If the installation fails, you must use a different method to upgrade WUA.

## Software update dependencies that are internal to Configuration Manager

The following sections list the internal dependencies for software updates in Configuration Manager.

### Management points

Management points transfer information between client computers and the Configuration Manager site. The management points are required for software updates.

### Software update points

You must install a software update point on the WSUS server to deploy software updates in Configuration Manager. For more information, see [Install and configure a software update point](../get-started/install-a-software-update-point.md).

### Distribution points

Distribution points are required to store the content for software updates. For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

### Client settings for software updates

Software updates are enabled for clients by default. There are other available settings that control how and when clients assess compliance for the software updates and control how the software updates are installed.

 For more information, see the following articles:

- [Client settings for software updates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)

- [Software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates)

> [!IMPORTANT]
>
> Beginning with the September 2020 cumulative update, HTTP-based WSUS servers will be secure by default. A client scanning for updates against an HTTP-based WSUS will no longer be allowed to leverage a user proxy by default. If you still require a user proxy despite the security trade-offs, a new [software updates client setting](../../core/clients/deploy/about-client-settings.md#software-updates) is available to allow these connections. For more information about the changes for scanning WSUS, see [September 2020 changes to improve security for Windows devices scanning WSUS](https://go.microsoft.com/fwlink/?linkid=2144403). To ensure that the best security protocols are in place, we highly recommend that you use the TLS/SSL protocol to help [secure your software update infrastructure](../get-started/software-update-point-ssl.md).

### Reporting services points

The reporting services point site system role can display reports for software updates. This role is optional but recommended. For more information about how to create a reporting services point, see [Configuring reporting](../../core/servers/manage/configuring-reporting.md).

## Next steps

[Prepare for software updates management](../get-started/prepare-for-software-updates-management.md)
