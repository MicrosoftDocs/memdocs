---
title: Overview of Apple Automated Device Enrollment for macOS in Intune
description: Learn about automated device enrollment (ADE) for Mac computers in Microsoft Intune, including supported scenarios, key features, and how to get started.
ms.date: 04/15/2026
ms.topic: concept-article
ms.reviewer: beflamm
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Overview of Apple Automated Device Enrollment for macOS  

Automated device enrollment (ADE) is an Apple enrollment method for corporate-owned Mac computers purchased through Apple Business Manager or Apple School Manager. With ADE, you configure and deploy enrollment profiles to devices over the air — without touching the devices. When someone turns on a device for the first time, Apple Setup Assistant guides them through setup and enrollment automatically.

> [!NOTE]
> The steps in ADE articles are the same whether you're using Apple Business Manager or Apple School Manager. For brevity, those articles refer to *Apple Business Manager* only, except where clarification is necessary.  

## Supported platforms

Intune supports automated device enrollment for macOS.  

| Platform | Setup article |
|----------|---------------|
| macOS | [Set up an enrollment profile for macOS](setup-automated-macos.md) |

For iOS/iPadOS, tvOS, and visionOS, see [Overview of Apple Automated Device Enrollment for Apple mobile](automated-device-enrollment-overview-apple.md).  

## Supported scenarios

| Scenario | Supported |
|----------|-----------|
| Supervised mode | ✅ ADE devices are supervised by default, giving you more management control. |
| Corporate-owned devices | ✅ Designed for devices purchased through Apple Business Manager or Apple School Manager. |
| Zero-touch deployment | ✅ Devices can ship directly to users. Enrollment starts when they turn on the device. |
| Bulk enrollment | ✅ Enroll a few devices or thousands using a single enrollment profile. |
| Devices with a single assigned user | ✅ Supported on macOS. |
| Userless devices (kiosk, shared-use) | ✅ Supported on macOS. |
| BYOD or personal devices | ❌ Not supported. |
| Device enrollment manager (DEM) accounts | ❌ Not supported. |
| Devices managed by another MDM provider | ❌ Users must unenroll from their current MDM provider before enrolling in Intune. For help migrating devices, see [Apple making device migration to Microsoft Intune easy with upcoming OS 26 release](https://techcommunity.microsoft.com/blog/IntuneCustomerSuccess/apple-making-device-migration-to-microsoft-intune-easy-with-upcoming-os-26-relea/4439895) on the Microsoft Community Hub. |

## How ADE works

Setting up ADE in Intune involves three main tasks:

1. **Get an enrollment program token**: Create a trust relationship between Intune and Apple Business Manager. This is typically a one-time setup task per token. For steps, see [Set up a macOS ADE token](token-setup-macos.md).

2. **Create and assign an enrollment profile**: Configure the enrollment experience for your Mac devices, including user affinity and Setup Assistant screens. Then assign the profile to device groups. For steps, see [Set up an enrollment profile for macOS](setup-automated-macos.md).

3. **Sync and distribute devices**: Sync device records from Apple Business Manager to Intune, then distribute devices to users. Enrollment starts automatically through Apple Setup Assistant when a device is turned on. For steps, see [Manage macOS ADE devices and tokens](manage-devices-tokens-macos.md).  

## Certificates

ADE supports the Automated Certificate Management Environment (ACME) protocol. When new devices enroll, the management profile from Intune receives an ACME certificate. ACME provides better protection than the SCEP protocol against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Devices that are already enrolled don't receive an ACME certificate unless they re-enroll into Microsoft Intune. ACME is supported on macOS 13.1 or later.   

## Before you begin  

Before setting up ADE for macOS, ensure the following are in place:

- Access to [Apple Business](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/).
- The [mobile device management authority](../../intune-service/fundamentals/mdm-authority-set.md) set to Intune in your tenant.
- An [Apple MDM push certificate](create-mdm-push-certificate.md) in Intune.  

## Next steps

- [Set up a macOS ADE token](token-setup-macos.md)
- [Set up an enrollment profile for macOS](setup-automated-macos.md)  
