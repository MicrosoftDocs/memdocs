---
title: Include file
description: Include file
author: brenduns  
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/19/2024
ms.author: brenduns
ms.custom: include file
---

#### Attack surface reduction

*Support for devices managed by Configuration Manager is in Preview.*

Manage [attack surface reduction settings for Configuration Manager devices](../protect/endpoint-security-asr-profile-settings.md#attack-surface-reduction-configmgr), when you use tenant attach.

**Policy path**:

- Endpoint security > Attach surface reduction > Windows (ConfigMgr)

**Profiles**:

- App and Browser Isolation(ConfigMgr)
- Attack Surface Reduction Rules(ConfigMgr)
- Exploit Protection(ConfigMgr)(preview)
- Web Protection (ConfigMgr)(preview)

**Required version of Configuration Manager**:

- Configuration Manager current branch version 2006 or later

**Supported Configuration Manager device platforms**:

- Windows 10 and later (x86, x64, ARM64)
- Windows 11 and later (x86, x64, ARM64)