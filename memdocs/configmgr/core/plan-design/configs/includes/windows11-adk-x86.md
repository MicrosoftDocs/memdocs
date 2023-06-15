---
author: banreet
ms.author: banreetkaur
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 12/01/2021
ms.localizationpriority: medium
# the same text of this include is also used in customize-boot-images.md
---

- The 32-bit versions of Windows PE (WinPE) in the WinPE add-ons for Windows 11 and Windows Server 2022 aren't supported. The last supported version of 32-bit WinPE is available in the **WinPE add-on for Windows 10, version 2004**. For more information, see [Download and install the Windows ADK](/windows-hardware/get-started/adk-install).<!--12440724-->

    Configuration Manager supports the use of older versions of Windows PE as boot images, but you can't customize them in the Configuration Manager console. For more information, see [Customize boot images with Configuration Manager](../../../../osd/get-started/customize-boot-images.md).
