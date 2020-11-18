---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 11/16/2020
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
The following profiles are supported for devices you manage with Configuration Manager current branch 2006 or later, through the tenant attach scenario:
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- Platform: **Windows 10 and Windows Server (ConfigMgr)**

  - Profile: **Microsoft Defender Antivirus Policy (preview)** - Manage [Antivirus policy settings for Configuration Manager devices](../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json), when you use tenant attach.

    This profile is supported with devices that are tenant attached and run the following platforms:
    - Windows 10 and later (x86, x64, ARM64)
    - Windows Server 2019 and later (x64)
    - Windows Server 2016 (x64)

  - Profile: **Windows Security experience (preview)** - Manage [Windows Security app settings for Configuration Manager devices](../../../intune/protect/antivirus-windows-security-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json), when you use tenant attach.

    This profile is supported with devices that are tenant attached and run the following platforms:
    - Windows 10 and later (x86, x64, ARM64)
    - Windows Server 2019 and later (x64)

- Platform: **Windows 10 and later**

  - Profile: **Microsoft Defender Firewall (ConfigMgr) (preview)** - Manage [firewall policy settings for Configuration Manager devices](../../../intune/protect/endpoint-security-firewall-profile-settings-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json), when you use tenant attach.

    This profile is supported with devices that are tenant attached and run the following platforms:
    - Windows 10 and later (x86, x64, ARM64)
