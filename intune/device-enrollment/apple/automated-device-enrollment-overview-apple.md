---
title: Overview of Apple Automated Device Enrollment for iOS/iPadOS in Intune
description: Learn about automated device enrollment (ADE) for Apple mobile devices in Microsoft Intune, including supported scenarios, key features, and how to get started.
ms.date: 04/15/2026
ms.topic: concept-article
ms.reviewer: annovich
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Overview of Apple Automated Device Enrollment for iOS/iPadOS

*Applies to iOS/iPadOS*

Automated device enrollment (ADE) is an Apple enrollment method for corporate-owned devices purchased through Apple Business Manager or Apple School Manager. With ADE, you configure and deploy enrollment profiles to devices over the air — without touching the devices. When someone turns on a device for the first time, Apple Setup Assistant guides them through setup and enrollment automatically.

> [!NOTE]
> The steps in ADE articles are the same whether you're using Apple Business Manager or Apple School Manager. For brevity, those articles refer to *Apple Business Manager* only, except where clarification is necessary.

## Supported platforms

Intune supports automated device enrollment for iOS/iPadOS. For macOS, see [Overview of Apple Automated Device Enrollment for macOS](automated-device-enrollment-overview-macos.md).

| Platform | Setup article |
|----------|---------------|
| iOS/iPadOS | [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md) |

## Supported scenarios

| Scenario | Supported |
|----------|-----------|
| Supervised mode | ✅ ADE devices are supervised by default, giving you more management control. |
| Corporate-owned devices | ✅ Designed for devices purchased through Apple Business Manager or Apple School Manager. |
| Zero-touch deployment | ✅ Devices can ship directly to users. Enrollment starts when they turn on the device. |
| Bulk enrollment | ✅ Enroll a few devices or thousands using a single enrollment profile. |
| Devices with a single assigned user | ✅ Supported on iOS/iPadOS. |
| Userless devices (kiosk, shared-use) | ✅ Supported on iOS/iPadOS. |
| Microsoft Entra shared device mode | ✅ Supported on iOS/iPadOS for frontline worker scenarios. |
| Apple Shared iPad | ✅ Supported on iPadOS. |
| BYOD or personal devices | ❌ Not supported. Use [MAM](../../intune-service/fundamentals/deployment-guide-enrollment-mamwe.md) or [user and device enrollment](setup-user-company-portal.md) instead. |
| Device enrollment manager (DEM) accounts | ❌ Not supported. |
| Devices managed by another MDM provider | ❌ Users must unenroll from their current MDM provider before enrolling in Intune. For help migrating devices, see [Apple making device migration to Microsoft Intune easy with upcoming OS 26 release](https://techcommunity.microsoft.com/blog/IntuneCustomerSuccess/apple-making-device-migration-to-microsoft-intune-easy-with-upcoming-os-26-relea/4439895) on the Microsoft Community Hub. |

## Certificates  
ADE supports the Automated Certificate Management Environment (ACME) protocol. When new devices enroll, the management profile from Intune receives an ACME certificate. ACME provides better protection than the SCEP protocol against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Devices that are already enrolled don't receive an ACME certificate unless they re-enroll into Microsoft Intune. ACME is supported on:

- iOS 16.0 or later
- iPadOS 16.1 or later

## How ADE works

Setting up ADE in Intune involves three main tasks:

1. **Get an enrollment program token**: Create a trust relationship between Intune and Apple Business Manager. This is typically a one-time setup task per token. For steps, see [Set up an iOS/iPadOS ADE token](token-setup-apple.md).

2. **Create and assign an enrollment profile**: Configure the enrollment experience for your devices, including user affinity, authentication method, and Setup Assistant screens. Then assign the profile to device groups. For steps, see [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md).

3. **Sync and distribute devices**: Sync device records from Apple Business Manager to Intune, then distribute devices to users. Enrollment starts automatically through Apple Setup Assistant when a device is turned on. For steps, see [Manage iOS/iPadOS ADE devices and tokens](manage-devices-tokens-apple.md).

## Prerequisites

Before setting up ADE for any Apple platform, ensure the following are in place:

- Access to [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/).
- The [mobile device management authority](../../intune-service/fundamentals/mdm-authority-set.md) set to Intune in your tenant.
- An [Apple MDM push certificate](create-mdm-push-certificate.md) in Intune.

## Next steps

- [Set up an iOS/iPadOS ADE token](token-setup-apple.md)
- [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md)
- [Manage iOS/iPadOS ADE devices and tokens](manage-devices-tokens-apple.md)