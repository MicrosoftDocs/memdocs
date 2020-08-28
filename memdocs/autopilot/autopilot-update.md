---
title: Windows Autopilot update
ms.reviewer: 
manager: laurawi
description: Windows Autopilot update 
keywords: Autopilot, update, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
---


# Windows Autopilot update

**Applies to**

- Windows 10, version 1903

Windows Autopilot update installs the lastest Autopilot features and fixes to your organization's Autopilot devices. The devices aren't moved to latest Windows OS version. With Autopilot update, you can keep the devices' current OS version and still benefit from new Autopilot features and bug fixes.
 
During the Autopilot deployment process, Windows Autopilot update has been added as a new node after the critical [Windows Zero Day Patch (ZDP) update](/windows-hardware/customize/desktop/windows-updates-during-oobe) check. During the update process, Windows Autopilot devices contact Windows Update to check for a new Autopilot update. If there's an Autopilot update available, the device will download and install the update, then restart automatically. See the following example.

 ![Autopilot update 1](images/update1.png)<br>
 ![Autopilot update 2](images/update2.png)<br>
 ![Autopilot update 3](images/update3.png)

The following diagram illustrates a typical Windows Autopilot deployment orchestration during the Out of Box Experience (OOBE) with the new Windows Autopilot update node.

 ![Autopilot update flow](images/update-flow.png)

## Release cadence

- When an Autopilot update is available, it's typically released on the fourth Tuesday of the month. The update could be released on a different week if there's an exception.
- A knowledge base (KB) article will also be published to document the changes that are included in the update.

For a list of released updates, see [Autopilot update history](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## See also

[Windows Update during OOBE](/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[What's new in Windows Autopilot](windows-autopilot-whats-new.md)<br>