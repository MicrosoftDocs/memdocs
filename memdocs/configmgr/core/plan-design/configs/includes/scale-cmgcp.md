---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: include
ms.date: 09/17/2020
---

- You can install multiple instances of the CMG connection point at primary sites.

- One CMG connection point can support a CMG with up to four VM instances. If the CMG has more than four VM instances, add a second CMG connection point for load balancing. A CMG with 16 VM instances should be linked with four CMG connection points.

> [!NOTE]
> When considering hardware requirements for the CMG connection point, see [Recommended hardware for remote site system servers](../recommended-hardware.md#remote-site-system-servers).<!-- SCCMDocs#2276 -->
