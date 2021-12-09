---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: include
ms.date: 12/01/2021
ms.localizationpriority: medium
---

> [!IMPORTANT]
> Starting in version 2103, the implementation of the recovery service changed. It's no longer using legacy MBAM components, but is still conceptually referred to as the _recovery service_. All version 2103 clients use the _message processing engine_ component of the management point as their recovery service. They escrow their recovery keys over the secure client notification channel. With this change, you can enable the Configuration Manager site for [enhanced HTTP](../../../../core/plan-design/hierarchy/enhanced-http.md). This configuration doesn't affect the functionality of BitLocker management in Configuration Manager.<!-- 11108795 -->
>
> When both the site and clients are running Configuration Manager version 2103 or later, clients send their recovery keys to the management point over the secure client notification channel. If any clients are on version 2010 or earlier, they need an HTTPS-enabled recovery service on the management point to escrow their keys.
