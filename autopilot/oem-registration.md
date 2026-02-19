---
title: Windows Autopilot OEM registration process
description: How OEMs add devices to Windows Autopilot.
ms.date: 06/13/2025
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---


# OEM registration

## Device registration process

When devices are purchased from an OEM, the OEM can automatically register the devices with the Windows Autopilot. For the list of OEMs that support registration, see the **Participant device manufacturers and resellers** section of the [Windows Autopilot page](https://aka.ms/windowsautopilot).

> [!NOTE]
>
> While the hardware hashes, also known as hardware IDs, are generated as part of the OEM device manufacturing process, the hardware hashes aren't normally provided directly to customers or Cloud Solution Partners (CSPs). Instead, the OEM should register devices on the customer's behalf. In cases where CSPs register devices, OEMs might provide PKID information to those partners to support the device registration process.

OEMs must follow [device guidelines](autopilot-device-guidelines.md) for Windows Autopilot devices.

### Service data

Microsoft manages and maintains Windows Autopilot. This service provides the backend database that associates hardware hashes with customer tenants. When an OEM registers devices for a customer, they're writing that data to this database and not directly to the customer's tenant. No permissions to the customer's tenant are granted or required for OEMs to register devices on the customer's behalf.

### Customer consent

Before an OEM can register devices for an organization, the organization's Microsoft Entra Global Administrator must approve the OEM. For more information, see [OEM authorization](registration-auth.md#oem-authorization).

<!-- MAXADO-9048730 -->

> [!IMPORTANT]
> [!INCLUDE [global-administrator](../autopilot/includes/global-administrator.md)]

## Microsoft Surface registration

For Surface devices, see [Surface registration support for Windows Autopilot](/surface/surface-autopilot-registration-support).

## Related content

- [Registration overview](registration-overview.md).
