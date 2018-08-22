---
title: Support for Windows 10
titleSuffix: Configuration Manager
description: Learn about the Windows 10 versions that are supported as clients or for OSD with System Center Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Support for Windows 10 in Configuration Manager  

*Applies to: System Center Configuration Manager (Current Branch)*


Learn about the Windows 10 versions that Configuration Manager supports, including:
 -  [Windows 10 as a Configuration Manager client](#windows-10-as-a-client)
 -  [The Windows Assessment and Deployment Kit (ADK) for Windows 10](#windows-10-adk)



## Windows 10 as a client
Configuration Manager attempts to provide support as a client for each new Windows 10 version as soon as possible after it becomes available. Because the products have separate development and release schedules, the support that Configuration Manager provides depends on when each becomes available.

For example, a Configuration Manager version drops from the matrix after [support for that version](/sccm/core/servers/manage/current-branch-versions-supported) ends. Similarly, support for Windows 10 versions like the Enterprise 2015 LTSB or 1511 drops from the matrix when they are removed from support. For more information, see [Deprecated operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).

-   This information supplements [Supported operating systems for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   If you use the long-term servicing branch of Configuration Manager, see [Supported configurations for the long-term servicing branch](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
The following table lists the versions of Windows 10 that you can use as a client with different versions of Configuration Manager.

| Windows 10 version | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|---------------------|-----|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| 1607   <br />(*see editions*)   <!--04+6/10/2018-->   | ![Supported](media/green_check.png) <sup>1</sup> | ![Supported](media/green_check.png) <sup>1</sup> | ![Supported](media/green_check.png) <sup>1</sup> | ![Supported](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*see editions*)   <!--10+6/09/2018-->   | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| 1709   <br />(*see editions*)   <!--04+6/09/2019-->   | ![Backwards compatible](media/blue_compat.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |
| 1803   <br />(*see editions*)   <!--11/12/2019-->   | ![Not supported](media/Red_X.png) | ![Not supported](media/Red_X.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Editions**: Enterprise, Pro, Education, Pro Education   

<sup>1</sup> For more information, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) and the section on "Servicing extension for Enterprise and Education editions".

| Key |
|--|
| ![Supported](media/green_check.png) = **Supported**  |
| ![Backwards compatible](media/blue_compat.png)  = **Backwards compatible** <br/> Existing client management features should work with the new Windows 10 version. For example, hardware inventory, software inventory, and software updates. We will document any known issues or caveats. <br><br>This approach gives you the ability to deploy and manage new Windows versions right away with application compatibility support, and without requiring a new Configuration Manager update version. |
| ![Not supported](media/Red_X.png) = **Not supported** |

 > [!NOTE]  
 > Starting in version 1802, Configuration Manager supports the client on Windows 10 ARM64 devices. Existing client management features should work with these new devices. For example, hardware and software inventory, software updates, and application management. OS deployment is currently not supported. <!-- 1353704 --> 



## Windows 10 ADK
When you deploy operating systems with Configuration Manager, the [Windows ADK is an external dependency](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) that is required.

The following table lists the versions of the Windows 10 ADK that you can use with different versions of Configuration Manager.

| Windows 10 ADK version  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|--------------------|-----|-----|-----|-----|
| 1703  | ![Supported](media/green_check.png) | ![Backwards compatible](media/blue_compat.png) | ![Backwards compatible](media/blue_compat.png) | ![Not supported](media/Red_X.png)   |
| 1709  | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | ![Backwards compatible](media/blue_compat.png) |
| 1803  | ![Not supported](media/Red_X.png)   | ![Not supported](media/Red_X.png) | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) |

|Key|
|--|
| ![Supported](media/green_check.png) = **Supported** <br/> Microsoft recommends using the Windows ADK that matches the version of Windows you're deploying. For example, use the Windows ADK for Windows 10 version 1703 when deploying Windows 10 version 1703. For more information on Windows ADK component supportability, see [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) and [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Backwards compatible](media/blue_compat.png)  = **Backward compatible** <br/> This combination isn't tested but should work. We will document any known issues or caveats. |
| ![Not supported](media/Red_X.png) = **Not supported** |

 > [!Note]  
 > Configuration Manager only supports x86 and amd64 components of the Windows 10 ADK. It doesn't currently support ARM or ARM64 components. 

> [!Tip]
> ADK version support for Server OS deployment: 
Windows Server builds have the same ADK requirement as the associated Windows 10 version. For example, Windows Server 2016 is the same build version as Windows 10 LTSB 2016.
