---
# required metadata

title: Learn about using Windows Update for Business in Microsoft Intune - Azure | Microsoft Docs
description: Manage Windows 10 software updates by using Intune policy for Windows 10 update rings and Windows 10 feature updates for Windows Update for Business settings in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/25/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dudeso
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Manage Windows 10 software updates in Intune

Use Intune to manage the install of Windows 10 software updates from Windows Update for Business.

By using Windows Update for Business, you simplify the update management experience. You don't need to approve individual updates for groups of devices and can manage risk in your environments by configuring an update rollout strategy. Intune provides the ability to [configure update settings](windows-update-settings.md) on devices and gives you the ability to defer update installation. You can also prevent devices from installing features from new Windows versions to help keep them stable, while allowing those devices to continue installing updates for quality and security.

Intune stores only the update policy assignments, not the updates themselves. Devices access Windows Update directly for the updates.

Learn more about Windows 10 [*feature* and *quality* updates](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) in the Windows documentation.

> [!NOTE]
> If the Microsoft Account Sign-In Assistant (wlidsvc) service is disabled, Windows Update will no longer offer feature updates to devices running Windows 10 1709 or higher. See [Feature updates are not being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are) in the Windows documentation.

## Policy types to manage updates

Intune provides the following policy types to manage updates:

- **Windows 10 update ring**: This policy is a collection of settings that configures when Windows 10 updates get installed.

  Update ring policies are supported for devices that run Windows 10 version 1607 or later.

- **Windows 10 feature updates** *(public preview)*: This policy updates devices to the Windows version you specify, and then freezes the feature set version on those devices. This version freeze remains in place until you choose to update them to a later Windows version. While the feature version remains static, devices can continue to install quality and security updates that are available for their feature version.

  Feature updates policies are supported for devices that run Windows 10 version 1709 or later.

You assign policies for Windows 10 update rings and Windows 10 feature updates to groups of devices. Use both policy types in the same Intune environment to manage updates for your Windows 10 devices.

## Reporting on updates

To learn about report options for Windows 10 update ring policy and Windows 10 feature updates policy, see [Intune compliance reports for updates](windows-update-compliance-reports.md).

## Next steps

- [Use Windows 10 update rings in Intune](../protect/windows-10-update-rings.md)
- [Use Windows 10 feature updates in Intune](../protect/windows-10-feature-updates.md)
- For more information, see [Manage updates using Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb) in the Windows documentation.
