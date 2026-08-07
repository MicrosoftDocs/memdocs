---
title: Device association lifecycle management
description: Manage the Windows Autopilot device association lifecycle, including resetting devices, uploading updated device information, working with registered Windows Autopilot devices, stale records, and decommissioning.
ms.date: 08/07/2026
ms.topic: concept-article
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Device association lifecycle management

This article describes how to manage common events throughout the device association lifecycle.

## Resetting an associated device

The tenant affinity created by device association is stored in the device's UEFI firmware, so it persists across a device reset, a Windows reinstall, and enrollment removal. Resetting the device alone doesn't remove the association.

> [!NOTE]
>
> After a device is reset and re-enrolled, its Microsoft Entra ID and Intune device records aren't reused—new records are created for the device. We recommend that you clean up the stale Microsoft Entra ID and Intune device records.

To fully remove the association, clear the tenant affinity on the device itself by clearing the association information—for example, by running the RemoveAssociation PowerShell script. This requires physical access to the device. For instructions, see [Remove association from a device](remove-association.md).

> [!IMPORTANT]
>
> Physical access to the device is required to clear the device's tenant affinity. The person with physical access to a device is treated as its owner from an association security perspective.

## Removing association locally on a device

If the association information is cleared locally on the device—for example, by running the RemoveAssociation PowerShell script—the behavior depends on whether the device is still enrolled in Intune:

- **The device is still enrolled in Intune.** Intune attempts to re-associate the device on its next check-in.
- **The device is no longer enrolled in Intune.** Intune doesn't know that the association information was removed, so the device's record in the **Device association** list remains stale.

## Uploading a new CSV file for an already pre-associated device

If a device already has a pre-association record in your tenant and you upload a new CSV for the same device:

- **If the device's hardware identity hasn't changed**, the existing pre-association record is updated. For example, if you're assigning a different device preparation policy, the record is updated in place.
- **If the device's hardware identity has changed**—which happens when someone clears UEFI via PowerShell script, resets the BIOS/UEFI settings, or toggles Secure Boot—the service can no longer match the new submission to the original device. In this case, a new pre-association record is created and the original record becomes stale. The new record is associated during OOBE as normal.

## Pre-associating a device that is registered for Windows Autopilot

If a device is already registered for Windows Autopilot, you can still pre-associate it. When the device goes through OOBE, the device association takes precedence. The device is enrolled using the device preparation policy. For guidance on exporting device information from an existing device, see [How do I get the DeviceLink CSV for a device that's already set up?](faq.md#how-do-i-get-the-devicelink-csv-for-a-device-thats-already-set-up).

## Managing stale records

A pre-association record becomes stale when:

- A new pre-association record is created for the same device because the hardware identity changed.
- The device was pre-associated and then associated with a different tenant.

> [!NOTE]
>
> Stale pre-associated device records are automatically deleted after 360 days. No manual cleanup is required.

## Decommissioning a device

You only need to remove association when the device is permanently leaving your tenant. To do so, follow the steps in [Remove association from a device](remove-association.md).

## Next steps

- [Overview of Windows Autopilot device association](overview.md)
- [Requirements for Windows Autopilot device association](requirements.md)
- [Remove association from a device](remove-association.md)
