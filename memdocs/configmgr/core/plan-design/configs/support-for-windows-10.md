---
title: Support for Windows 10
titleSuffix: Configuration Manager
description: Learn about the Windows 10 versions that are supported as clients or for OSD with Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
---

# Support for Windows 10 in Configuration Manager  

*Applies to: Configuration Manager (current branch)*

Learn about the Windows 10 versions that Configuration Manager supports, including:

- [Windows 10 as a Configuration Manager client](#windows-10-as-a-client)
- [The Windows Assessment and Deployment Kit (ADK) for Windows 10](#windows-10-adk)

> [!Tip]
> Windows Server builds as a client are supported the same as the associated Windows 10 version. For example, Windows Server 2016 is the same build version as Windows 10 LTSB 2016, and Windows Server version 1803 is the same build version as Windows 10 version 1803.
>
> For more information on Windows Server as a site system, see [Supported operating systems for Configuration Manager site system servers](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## Windows 10 as a client

Configuration Manager attempts to provide support as a client for each new Windows 10 version as soon as possible after it becomes available. Because the products have separate development and release schedules, the support that Configuration Manager provides depends on when each becomes available.

A Configuration Manager version drops from the matrix after [support for that version](../../servers/manage/current-branch-versions-supported.md) ends. Similarly, support for Windows 10 versions like the Enterprise 2015 LTSB or 1511 drops from the matrix when they're removed from support.

- The latest version of Configuration Manager current branch receives both security and critical updates, which can include fixes for issues with Windows 10 versions. When Microsoft releases a new version of Configuration Manager current branch, prior versions only receive security updates. For more information, see [Support for Configuration Manager current branch versions](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > The best way to stay current with Windows 10 is to stay current with Configuration Manager. For more information, see [Configuration Manager and Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md).  

- This information supplements [Supported operating systems for clients and devices](supported-operating-systems-for-clients-and-devices.md).  

- If you use the long-term servicing branch of Configuration Manager, see [Supported configurations for the long-term servicing branch](../../understand/supported-configurations-for-ltsb.md).  

The following table lists the versions of Windows 10 that you can use as a client with different versions of Configuration Manager.

| Windows 10 version | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Not supported](media/Red_X.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

For more information on Windows lifecycle, see the [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

| Key |
|--|
| ![Supported](media/green_check.png) = **Supported**  |
| ![Not supported](media/Red_X.png) = **Not supported** |

### <a name="bkmk_win10-notes"></a> Windows 10 client support notes

- Support for Windows 10 semi-annual channel versions includes the following editions: Enterprise, Pro, Education, and Pro Education.  

- Starting in version 1906, Configuration Manager supports Windows 10 Pro for Workstation.

- For Windows 10, version 1909, OS deployment media shows the version as 10.0.18362.418.

### <a name="bkmk_arm64"></a> Windows 10 on ARM64

Configuration Manager supports the client on Windows 10 ARM64 devices. OS deployment is not supported.<!-- 1353704 -->

Starting in version 2002,<!--5954175--> the **All Windows 10 (ARM64)** platform is available in the list of supported OS versions on objects with requirement rules or applicability lists.

> [!NOTE]
> If you previously selected the top-level **Windows 10** platform, this action automatically selected both **All Windows 10 (64-bit)** and **All Windows 10 (32-bit)**. This new platform isn't automatically selected. If you want to add **All Windows 10 (ARM64)**, manually select it in the list.

### <a name="bkmk_WIfB-support"></a> Support for Windows Insider

Starting in Configuration Manager version 1906, you can [update and service Windows Insider](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) builds. This ability is provided as a convenience to our customers. While this functionality should work, the support for it is best effort. Configuration Manager might not issue a hotfix for this functionality if it ceases to function.  

To provide feedback on Windows Insider, use the [Feedback Hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## Windows 10 ADK

When you deploy operating systems with Configuration Manager, the Windows ADK is a required external dependency. For more information, see the following articles:

- [Infrastructure requirements for OS deployment](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Download the Windows ADK for Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Starting with Windows 10 version 1809, Windows PE is a separate installer. Otherwise there's no functional difference.
    >
    > Make sure to download both the **Windows ADK for Windows 10** and the **Windows PE add-on for the ADK**.

The following table lists the versions of the Windows 10 ADK that you can use with different versions of Configuration Manager.

| Windows 10 ADK version  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Not supported](media/Red_X.png)   | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Backwards compatible](media/blue_compat.png) | ![Backwards compatible](media/blue_compat.png) | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Backwards compatible](media/blue_compat.png) | ![Backwards compatible](media/blue_compat.png) | ![Not supported](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Not supported](media/Red_X.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |

|Key|
|--|
| ![Supported](media/green_check.png) = **Supported** <br/> This table only shows Windows ADK supportability in relation to the version of Configuration Manager. Microsoft recommends using the Windows ADK that matches the version of Windows you're deploying. Use the latest Windows ADK version when deploying the latest Windows 10 version. The latest Windows ADK version may support deployment of older OS versions, such as Windows 8.1.<!-- SCCMDocs issue 1229 --> For more information on Windows ADK component supportability, see [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) and [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Backwards compatible](media/blue_compat.png)  = **Backward compatible** <br/> This combination isn't tested but should work. We'll document any known issues or caveats. |
| ![Not supported](media/Red_X.png) = **Not supported** |

### <a name="bkmk_adk-notes"></a> Windows 10 ADK support notes

- Configuration Manager only supports x86 and amd64 components of the Windows 10 ADK. It doesn't currently support ARM or ARM64 components.

- Windows Server builds have the same Windows ADK requirement as the associated Windows 10 version. For example, Windows Server 2016 is the same build version as Windows 10 LTSB 2016.
