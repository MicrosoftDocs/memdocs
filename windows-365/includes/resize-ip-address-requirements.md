---
title: include file
description: include file
author: ErikjeMS  
ms.service: windows-365
ms.topic: include
ms.date: 09/25/2024
ms.author: erikje
ms.custom: include file
---

## IP address requirements

When resizing a Microsoft Entra hybrid join bring-your-own-network Cloud PC, a second IP address must be available in the subnet for the Cloud PC to be resized.

During the resizing operation, a second IP address is used when moving to the new size. This precaution makes sure that the Cloud PC can be rolled back to the original should an issue occur.

To account for this precaution, you can:

- Make sure that adequate IP addresses are available in the vNET for all Cloud PCs to be resized, or
- Stagger your resize operations to make sure that the address scope is maintained.

If inadequate addresses are available, resize failures can occur.