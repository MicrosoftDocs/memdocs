---
title: Remote Windows Autopilot reset in Intune
description: Remote Windows Autopilot reset in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/14/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

## Reset devices with remote Windows Autopilot Reset

You can use an MDM service such a Microsoft Intune to start the remote Windows Autopilot reset process. Resetting in this way avoids the need for IT staff to visit each machine to start the process.

To enable a device for a remote Windows Autopilot Reset, the device must be MDM managed and joined to Azure AD.

### Triggering a remote Windows Autopilot Reset

To trigger a remote Windows Autopilot Reset via Intune, follow these steps:

1. Navigate to **Devices** tab in the Intune admin center.
2. In the **All devices** view, select the targeted reset devices and then click **More** to view device actions.
3. Select **Autopilot Reset** to start the reset task.

> [!NOTE]
> The Autopilot Reset option will not be enabled in Microsoft Intune for devices not running Windows 10 build 17672 or higher.

Once the reset is complete, the device is again ready for use.