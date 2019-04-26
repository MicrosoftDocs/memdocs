---
title: Third-party MDM co-existence
titleSuffix: Configuration Manager
description: Learn about using a third-party MDM service with Configuration Manager 
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Third-party MDM co-existence with Configuration Manager

When you concurrently manage Windows 10 devices with both Configuration Manager and Microsoft Intune, this functionality is called [co-management](/sccm/comanage/overview). When you manage devices with Configuration Manager and enroll with a third-party MDM service, this functionality is called *coexistence*. Having two management authorities for a single device can be challenging if not properly orchestrated between the two. With co-management, Configuration Manager and Intune balance the [workloads] to make sure there are no conflicts. This interaction doesn't exist with third-party services, so there are limitations with the management capabilities of coexistence.