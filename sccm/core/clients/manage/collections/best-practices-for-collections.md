---
title: Collections best practices
titleSuffix: Configuration Manager
description: Get best practices for collections in Configuration Manager.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Best practices for collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the following best practices for collections in Configuration Manager.  

## <a name="bkmk_incremental"></a> Don't use incremental updates with many collections

When you enable the **Use incremental updates for this collection** option, this configuration might cause evaluation delays when you enable it for many collections. The threshold is about 200 collections in your hierarchy. The exact number depends on the following factors:  

- The total number of collections  

- The frequency of new resources being added and changed in the hierarchy  

- The number of clients in your hierarchy  

- The complexity of collection membership rules in your hierarchy  

## Maintenance window size for software updates

You can configure maintenance windows for device collections to restrict the times that Configuration Manager can install software on these devices. If you configure the maintenance window to be too small, the client might not be able to install critical software updates, which leaves the client vulnerable to the attack mitigated by the software update.

> [!Tip]
> Important considerations to keep in mind when planning your maintenance windows:
>
> - The default software update maximum run time is 60 minutes.
> - When Configuration Manager calculates whether an update can install, it adds five minutes to the maximum run time to account for a restart.
> - The remaining duration of a maintenance window must be longer than the maximum run time of the software update plus five minutes.
