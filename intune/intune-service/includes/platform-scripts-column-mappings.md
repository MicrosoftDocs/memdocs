---
author: nicholasswhite
ms.author: nwhite
manager: laurawi
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.topic: include
description: Platform scripts Device status export column mappings
ms.date: 09/08/2025
---
<!--This file contains the column mapping table for Platform scripts Device status exports.-->

> [!NOTE]
> Device status exports from the Intune admin center for Platform scripts now use the Intune Export API, and CSV column names align with the API schema.
> Column mappings are as follows:
> 
> | Admin center column | Export API column |
> |---------------------|-------------------|
> | Device name         | DeviceName        |
> | User name           | UserName          |
> | OS Version          | OSVersion         |
> | Status              | RunState          |
> | Last Updated        | ModifiedTime      |
> | Result              | PolicyResultDetail (macOS only) |