---
title: include file
description: include file
author: brenduns  
ms.service: microsoft-intune
ms.topic: include
ms.date: 09/20/2021
ms.author: brenduns
ms.custom: include file
---

#### Attack surface reduction

*Support for devices managed by Configuration Manager is in Preview.*

Manage [attack surface reduction settings for Configuration Manager devices](../protect/endpoint-security-asr-profile-settings.md#-attack-surface-reduction-configmgr), when you use tenant attach.

**Policy path**:

- Endpoint security > Attach surface reduction > Windows 10 and later (ConfigMgr)  

**Profiles**:

- Exploit Protection(ConfigMgr)(preview)
- Web Protection (ConfigMgr)(preview)

**Required version of Configuration Manager**:

- Configuration Manager current branch version 2006 or later

**Supported Configuration Manager device platforms**:

- Windows 10 and later (x86, x64, ARM64)
- Windows Server 2019 and later (x64)
- Windows Server 2016 (x64)
- Windows 8.1 (x86, x64), starting in Configuration Manager version 2010 <!--8763780, 8740844-->
- Windows Server 2012 R2 (x64), starting in Configuration Manager version 2010 <!--8763780, 8740844-->
