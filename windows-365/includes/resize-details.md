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

When resizing starts, the user is automatically disconnected from their Cloud PC and any unsaved work might be lost.

Resizing can take from 15 to 20 minutes before the user can access their Cloud PC again. You can monitor the status in the Windows 365 provisioning blade. Users can see their Cloud PC status at https://windows365.microsoft.com.

If there are no licenses in your inventory, the resizing fails. To request more licenses, contact your procurement admin. After you purchase the license and added to the inventory in the Microsoft 365 admin center, you can retry the resize operation. Licenses can be purchased from various channels: EA, CSP, MCA, and Web Direct.

Devices with a state of **Resize not supported** aren't resized. The status message and details can help you identify the issue. You can still proceed with a bulk resize even if you have devices in the list that are marked as **Resize not supported**.
