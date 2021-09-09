---
title: Support for Windows 11
titleSuffix: Configuration Manager
description: Learn about the Windows 11 versions that are supported as clients with Configuration Manager.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Support for Windows 11 in Configuration Manager  

*Applies to: Configuration Manager (current branch)*

Learn about the Windows 11 versions that Configuration Manager supports as a client.

For more information about support for the Windows Assessment and Deployment Kit (ADK) for Windows 11, see [Support for the Windows ADK](support-for-windows-adk.md).

> [!TIP]
> Windows Server builds as a client are supported the same as the associated Windows 11 version.<!--  For example, Windows Server 2022 is the same build version as Windows 11 ..., and Windows Server version ... is the same build version as Windows 11, version .... -->
>
> For more information on Windows Server as a site system, see [Supported operating systems for Configuration Manager site system servers](supported-operating-systems-for-site-system-servers.md).

## Windows 11 versions

Configuration Manager attempts to provide support as a client for each new Windows 11 version soon after it becomes available. Because the products have separate development and release schedules, the support that Configuration Manager provides depends on when each becomes available.

A Configuration Manager version drops from the matrix after [support for that version](../../servers/manage/current-branch-versions-supported.md) ends. Similarly, Configuration Manager doesn't support Windows 11 versions when their support lifecycle ends.

- The latest version of Configuration Manager current branch receives both security and critical updates, which can include fixes for Windows 11-specific features. When Microsoft releases a new version of Configuration Manager current branch, prior versions only receive security updates. For more information, see [Support for Configuration Manager current branch versions](../../servers/manage/current-branch-versions-supported.md).

    > [!NOTE]
    > The best way to stay current with Windows 11 is to stay current with Configuration Manager. For more information, see [Configuration Manager and Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md).

- This information supplements [Supported operating systems for clients and devices](supported-operating-systems-for-clients-and-devices.md).

The following table lists the versions of Windows 11 that you can use as a client with different versions of Configuration Manager.

| Windows 11 version                         | ConfigMgr 2006 | ConfigMgr 2010 | ConfigMgr 2103 | ConfigMgr 2107 |
|--------------------------------------------|----------------|----------------|----------------|----------------|
| **21H2**<br>(10.1.222xx) <!--mm/dd/yyyy--> | ![Not supported](media/red-x.png) | ![Not supported](media/red-x.png) | ![Not supported](media/red-x.png) | ![Supported](media/green-check.png) |

<!--
All currently supported versions of Configuration Manager current branch support the following Windows 11 LTSC editions:

- **Enterprise LTSC xxxx** <!--mm/dd/yyyy
-->

For more information on Windows lifecycle, see the [Windows lifecycle fact sheet](/lifecycle/faq/windows) and [Windows release information](/windows/release-health/release-information)<!-- need to revise this link? -->.

| Key |
|--|
| ![Supported](media/green-check.png) = **Supported** |
| ![Not supported](media/red-x.png) = **Not supported** |

## Support notes

- Support for Windows 11 semi-annual channel versions includes the following editions: Enterprise, Pro, Education, Pro Education, and Pro for Workstation.

<!-- - For Windows 11, version 21H2, OS deployment media shows the version as 10.1.222xx.xxx. --><!-- 9504158 -->

## Support for Windows Insider

You can [update and service Windows Insider](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) builds. This ability is provided as a convenience to our customers. While this functionality should work, its support is best effort. Configuration Manager might not issue a hotfix for this functionality if it doesn't work.

To provide feedback on Windows Insider, use the Windows [Feedback Hub](/windows-insider/business/feedback).

## Known issues

### Desktop Analytics

<!-- 10797955 -->

### Support for ARM64 devices

<!-- 10589908 -->

### Windows servicing dashboard

<!-- 10732387 -->

### Microsoft Store for Business and Education

<!-- TBD -->

## Next steps

[Support for the Windows ADK](support-for-windows-adk.md)
