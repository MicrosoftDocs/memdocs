---
author: banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 05/29/2024
ms.localizationpriority: medium
# the same text of this include is also used in customize-boot-images.md
---

- The last supported version of 32-bit WinPE is available in the **WinPE add-on for Windows 10, version 2004** (10.1.19041). Versions of the WinPE add-on for the ADK after the **ADK for Windows 10, version 2004**
(10.1.19041) no longer support 32-bit versions of Windows PE (WinPE). For more information, see [Download and install the Windows ADK](/windows-hardware/get-started/adk-install).<!--12440724-->

    Configuration Manager supports the use of older versions of Windows PE as boot images, but you can't customize them in the Configuration Manager console. For more information, see [Customize boot images with Configuration Manager](../../../../osd/get-started/customize-boot-images.md).
