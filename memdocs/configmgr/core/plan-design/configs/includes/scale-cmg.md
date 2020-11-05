---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: include
ms.date: 09/17/2020
---

- You can install multiple instances of the cloud management gateway (CMG) at primary sites, or the central administration site.

    > [!TIP]
    > In a hierarchy, create the CMG at the central administration site.

- One CMG supports one to 16 virtual machine (VM) instances in the Azure cloud service.

- Each CMG VM instance supports 6,000 simultaneous client connections. When the CMG is under high load with more than the supported number of clients, it still handles requests but there may be delay.
