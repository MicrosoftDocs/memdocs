---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 10/20/2020
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
The following profiles are supported for devices you manage with Configuration Manager current branch 2006 or later, through the tenant attach scenario:
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- Platform: **Windows 10 and Windows Server (ConfigMgr)**

  - Profile: **Microsoft Defender Antivirus Policy (preview)** - Manage [Antivirus policy settings for Configuration Manager devices](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md), when you use tenant attach.

    This profile is supported with devices that are tenant attached and run the following platforms:
    - Windows 10 and later (x86, x64, ARM64)
    - Windows Server 2019 and later (x64)
    - Windows Server 2016 (x64)

  - Profile: **Windows Security experience (preview)** - Manage [Windows Security app settings for Configuration Manager devices](../../protect/antivirus-windows-security-settings-windows-tenant-attach.md), when you use tenant attach.

    This profile is supported with devices that are tenant attached and run the following platforms:
    - Windows 10 and later (x86, x64, ARM64)
    - Windows Server 2019 and later (x64)
