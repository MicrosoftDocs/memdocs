---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/03/2020
ms.localizationpriority: medium
---
<!--Don't apply H2 in this include file since they are context driven by article. Used in the adoption-score.md and startup-performance.md files -->
The **Startup performance score** helps IT get users from power-on to productivity quickly, without lengthy boot and sign-in delays. The **Startup score** is a number between 0 and 100. This score is a weighted average of **Boot score** and the **Sign-in** score, which are computed as follows:

- **Boot score**: Based on the time from power-on to sign in. We look at the last boot time from each device, excluding the update phase, then score it from 0 (poor) to 100 (exceptional). These scores are averaged to provide an overall tenant boot score.
- **Sign-in score**: Based on the time from when credentials have been entered until the user can access a responsive desktop (meaning the desktop has rendered and the CPU usage has fallen below 50% for at least 2 seconds). We look at the last sign-in time to each device, excluding first sign-ins or sign-ins immediately after a feature update, then score it from 0 (poor) to 100 (exceptional). These scores are averaged to provide an overall tenant boot score.
