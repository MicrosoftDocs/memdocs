---
title: Windows Autopilot device association FAQ
description: Frequently asked questions about Windows Autopilot device association, including exported CSV content, corporate identifiers, OEM support, and virtual machines.
ms.date: 08/07/2026
ms.topic: faq
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device association frequently asked questions

This article answers common questions about Windows Autopilot device association.

## General

### Why did the CSV content for association change?

If you export the device information CSV multiple times, the exported information may look different because the DeviceLink contains metadata timestamps. This behavior is expected, and the device's hardware identity doesn't change.

A changed CSV doesn't invalidate an existing pre-association on its own. A pre-association is only invalidated when the device's hardware identity is changed by running a RemoveAssociation PowerShell script, BIOS reset, or changing the Secure Boot configuration. After the identity is cleared on the device, you can export a new DeviceLink CSV and upload it to pre-associate the device again.

### How do I get the DeviceLink CSV for a device that's already set up?

For existing devices that are past the out-of-box experience (OOBE), you can export the device information from the device's Autopilot diagnostic logs instead of using the OOBE Autopilot menu. On the device, go to **Settings** > **Accounts** > **Access work or school**, select **Export your management logs** under **Related settings**, and then retrieve the DeviceLink CSV from the exported diagnostics. You can also run `MdmDiagnosticsTool.exe -area Autopilot -cab <path>` from an elevated command prompt, or collect the diagnostics remotely from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Devices** > select the device > **Collect diagnostics**). Upload the exported CSV in Intune to pre-associate the device. For more information, see [Associate devices](../tutorial/user-driven/entra-join-device-association.md).

### Do I need to upload corporate identifiers if my devices are pre-associated?

No. Pre-associated and associated devices are automatically marked as corporate-owned, so you don't need to upload corporate identifiers for them—even if you use enrollment restrictions to block personal device enrollments. Corporate identifiers and device association are two alternative ways to make sure only trusted devices are onboarded; you don't need both.

### Can an OEM, reseller, or partner associate devices before shipment?

At this time, device uploads are only supported through Intune. In the future, OEMs and partners will also be able to pre-associate devices.

### Are virtual machines supported for testing?

No. Device association requires a physical Windows 11 device with TPM 2.0 in a good state. This is the only way to guarantee that the device identity can be securely verified.

## Related content

- [Overview of Windows Autopilot device association](overview.md)
- [Device association lifecycle management](lifecycle-management.md)
