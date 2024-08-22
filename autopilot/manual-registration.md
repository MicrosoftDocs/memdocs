---
title: Manual registration of devices for Windows Autopilot
description: Manual registration overview.
ms.service: windows-client
ms.subservice: itpro-autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Manual registration overview

Ideally, the OEM, reseller, or distributor from which the device was purchased performs the registration of a device with Windows Autopilot. However it's also possible to register devices manually. A device might need to be registered manually if:

- The device was obtained from a non-participant device manufacturer or reseller.
- The device is a virtual machine (VM).
- The device doesn't otherwise qualify for automatic registration, such as an existing legacy device.

The following diagram shows how manual registration and OEM registration might be used to deploy both new and existing devices with Windows Autopilot.

:::image type="content" source="images/image2.png" alt-text="Screenshot that shows Windows Autopilot device registration process.":::

For a list of participant device manufacturers and device resellers, see [Autopilot device manufacturers and resellers](https://www.microsoft.com/microsoft-365/windows/windows-autopilot).

To [manually register a device](add-devices.md), a device's hardware hash first has to be captured. Once this process is completed, the resulting hardware hash can be uploaded to the Windows Autopilot service. Because this process requires booting the device into Windows to obtain the hardware hash, manual registration is intended primarily for testing and evaluation scenarios.

> [!NOTE]
>
> Customers can only register devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners as described in the previous sections.

## Platforms for device registration

After the hardware hashes are captured from existing devices, they can be uploaded in any of the following ways:

- [Microsoft Intune](add-devices.md) - Intune is the preferred mechanism for all customers.

  - The [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) is used for Intune device enrollment.

- Partner Center - Partner Center is used by CSP partners to register devices on behalf of customers.

- Microsoft 365 Business & Office 365 Admin - Microsoft 365 Business & Office 365 Admin is typically used by small and medium businesses (SMBs) who manage their devices using Microsoft 365 Business.

- Microsoft Store for Business - Since Microsoft Store for Business is deprecated, use another method instead.

> [!IMPORTANT]
>
> Microsoft Store for Business and Microsoft Store for Education is deprecated. The current capabilities of free apps can be used while they're still available. For more information about this change, see [Evolving the Microsoft Store for Business and Education](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/evolving-the-microsoft-store-for-business-and-education/ba-p/2569423) and [Microsoft Store for Business and Education](/microsoft-store/).

A summary of each platform's capabilities is provided in the following table:

| Platform/Portal | Register devices? | Create/Assign profile | Acceptable Device ID |
|---|---|--|--|
| OEM Direct API | YES - 1000 at a time max | NO | Tuple or PKID |
| [Partner Center](/partner-center/autopilot) | YES - 1000 at a time max | YES<sup>3</sup> | Tuple or PKID or 4K HH |
| [Intune](add-devices.md) | YES - 500 at a time max | YES<sup>12</sup> | 4K HH |
| [Microsoft Store for Business](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles) | YES - 1000 at a time max | YES<sup>4</sup> | 4K HH |
| [Microsoft 365 Business Premium](/microsoft-365/business/create-and-edit-autopilot-profiles) | YES - 1000 at a time max | YES<sup>3</sup> | 4K HH |

- **<sup>1</sup>** Microsoft recommended platform to use.
- **<sup>2</sup>** Intune license required.
- **<sup>3</sup>** Feature capabilities are limited.
- **<sup>4</sup>** Device profile assignment will be retired from Microsoft Store for Business in the coming months.

For more information about device IDs, see the following articles:

- [Device identification](registration-overview.md#device-identification).
- [Windows Autopilot device guidelines](autopilot-device-guidelines.md).
- [Add devices to a customer account](/partner-center/autopilot).

## Related content

- [Registration overview](registration-overview.md).
- [Manually register devices with Windows Autopilot](add-devices.md).
