---
title: Support for the Windows ADK
titleSuffix: Configuration Manager
description: Learn about the Windows Assessment and Deployment Kit (ADK) versions that are supported for OS deployment with Configuration Manager.
ms.date: 05/09/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz,frankroj
---

# Support for the Windows ADK in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you deploy operating systems with Configuration Manager, the Windows Assessment and Deployment Kit (ADK) is a required external dependency. For more information, see the following articles:

- [Infrastructure requirements for OS deployment](/mem/configmgr/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk)

- [Download the Windows ADK](/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    >
    > - Windows PE is a separate installer. Make sure to download both the **Windows ADK** and the **Windows PE add-on for the ADK**.
    > - **ADK 10.1.25398.1 (updated September 2023)** (10.1.25398.1) or newer is required to deploy Windows 10/11 ARM64 operating systems. However, **ADK 10.1.25398.1 (updated September 2023)** (10.1.25398.1) Windows PE boot images have some known issues and need to be updated with the latest cumulative update to work with Configuration Manager. For more information, see [Support notes](#support-notes).

    > [!NOTE]
    >
    > **ADK 10.1.25398.1 (updated September 2023)** isn't currently supported for use with Configuration Manager due to [known issues](#support-notes) unless the Windows PE boot images are updated with the latest cumulative update (LCU). Previous supported ADK versions can be found at [Other ADK downloads](/windows-hardware/get-started/adk-install#other-adk-downloads). For more information, see [Support notes](#support-notes).

## Windows ADK versions

The following table lists the versions of the Windows ADK that you can use with different versions of Configuration Manager.

| Windows ADK version            | ConfigMgr 2211| ConfigMgr 2303 | ConfigMgr 2309 | ConfigMgr 2403  |
|--------------------------------|----------------|----------------|----------------|----------------|
| **ADK 10.1.25398.1 (updated September 2023)** <br>(10.1.25398.1)| ❌ | ❌ | ❌ | Only with LCU |
| **ADK for Windows 11, version 22H2**<br>(10.1.22621.1)| ✅ | ✅ | ✅ | ✅ |
| **ADK for Windows 11, version 21H1**<br>(10.1.22000) | ✅ | ✅ | ✅ | ✅ |
| **ADK for Windows Server 2022**<br>(10.1.20348)  | ✅ | ✅ | ✅ | ✅ |
| **ADK for Windows 10, version 2004**<br>(10.1.19041)| ✅ | ✅ | ✅ | ✅ |

|Key|
|--|
| ✅ = **Supported** <br/> This table only shows Windows ADK supportability in relation to the version of Configuration Manager. Microsoft recommends using the Windows ADK that matches the version of Windows you're deploying. Use the latest Windows ADK version when deploying the latest Windows version. The latest Windows ADK version might support deployment of older OS versions, such as Windows 10.<!-- SCCMDocs issue 1229 --> For more information on Windows ADK component supportability, see [DISM supported platforms](/windows-hardware/manufacture/desktop/dism-supported-platforms), [USMT requirements](/windows/deployment/usmt/usmt-requirements#bkmk-1), and [Choose the right ADK for your scenario](/windows-hardware/get-started/adk-install#choose-the-right-adk-for-your-scenario). |
| ![Backwards compatible](media/blue-compat.png)  = **Backward compatible** <br/> This combination isn't tested but should work. We'll document any known issues or caveats. |
| ❌ = **Not supported** |

## Support notes

- **ADK 10.1.25398.1 (updated September 2023)** Windows PE AMD64 boot images aren't currently supported for use with Configuration Manager due to known issues:

  - VBScript doesn't work in WinPE.
  - The **Pre-provision BitLocker** task doesn't work in WinPE.
  - Devices with UFS storage, such as the Surface Go 4, don't work in WinPE.

    These issues can be fixed by applying the latest **Windows Server 23H2** cumulative update (**Cumulative Update for Microsoft server operating system version 23H2 for x64-based Systems**) to the Windows PE AMD64 boot image found in the **ADK 10.1.25398.1 (updated September 2023)**. Once the latest cumulative update is applied to the Windows PE AMD64 boot image, it can be used with Configuration Manager. Information regarding applying cumulative updates to Windows PE boot images can be found in the article [Customize Windows PE boot images](/windows/deployment/customize-boot-image).

    > [!NOTE]
    >
    > To enable VBScript support in the **ADK 10.1.25398.1 (updated September 2023)** Windows PE AMD64 boot image, make sure to add the [Scripting/WinPE-Scripting](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference) optional component before applying the latest **Windows Server 23H2** cumulative update to the Windows PE AMD64 boot image.

    The Windows PE ARM64 boot image in the **ADK 10.1.25398.1 (updated September 2023)** doesn't support either VBScript or BitLocker while in Windows PE, even when the ([Scripting/WinPE-Scripting](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference)) and ([Startup/WinPE-SecureStartup](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference)) optional components are added and the latest **Windows Server 23H2** cumulative update is applied to the Windows PE ARM64 boot image.

- For information on applying the [BlackLotus UEFI bootkit vulnerability](https://prod.support.services.microsoft.com/topic/kb5025885-how-to-manage-the-windows-boot-manager-revocations-for-secure-boot-changes-associated-with-cve-2023-24932-41a975df-beb2-40c1-99a3-b3ff139f832d) security updates to boot images from the ADKs before the **ADK 10.1.25398.1 (updated September 2023)** (10.1.25398.1), see [Customize Windows PE boot images](/windows/deployment/customize-boot-image). Boot images from the **ADK 10.1.25398.1 (updated September 2023)** (10.1.25398.1) and newer already have the BlackLotus UEFI bootkit vulnerability security update applied to them.

- Windows Server builds have the same Windows ADK requirement as the associated Windows client version. For example, Windows Server 2016 is the same build version as Windows 10 LTSB 2016.

- If you're deploying both Windows 11 and Windows Server 2022, use the Windows ADK for Windows 11, which is the latest version. If you're deploying Windows Server 2022 and not Windows 11, you can use either Windows ADK for Windows Server 2022 or Windows 11.

<!--12440724-->
[!INCLUDE [windows11-adk-x86](includes/windows11-adk-x86.md)]

## Known issues

<!-- 11307733 -->
[!INCLUDE [windows-adk-11-preprovision-bitlocker](includes/windows-adk-11-preprovision-bitlocker.md)]

## Next steps

[Support for Windows 11](support-for-windows-11.md)

[Support for Windows 10](support-for-windows-10.md)

[Supported OS versions for clients](supported-operating-systems-for-clients-and-devices.md)
