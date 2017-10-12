---
title: Remotely synchronize policy on devices enrolled with Intune
titleSuffix: "Configuration Manager"
description: Learn how to synchronize policy on Intune-enrolled devices from the Configuration Manager console
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: 18
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
---
# Remotely synchronize policy on Intune-enrolled devices from the Configuration Manager console

*Applies to: System Center Configuration Manager (Current Branch)*


You can request a policy sync for a device that is enrolled with Intune from the Configuration Manager console instead of having to request a sync from the Company Portal app on the device itself. 

To do this:

1.	Select a device under **Assets and Compliance** > **Overview** > **Devices**.
2.	Click **Send Sync Request** in the **Remote Device Actions** menu.


After five to ten minutes, any changes in policy will be synced to the device. You can view sync request state information in a new column in device views, called **Remote Sync State**, as well as in the discovery data section of the **Properties** dialog box for each device.
