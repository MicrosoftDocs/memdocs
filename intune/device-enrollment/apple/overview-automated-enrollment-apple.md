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

# Overview of Apple Automated Device Enrollment for Apple mobile   

Automated device enrollment (ADE) is an Apple enrollment method for corporate-owned devices purchased through Apple Business or Apple School Manager. With ADE, you configure and deploy enrollment profiles to devices over the air — without touching the devices. When someone turns on a device for the first time, Apple Setup Assistant guides them through setup and enrollment automatically.

> [!NOTE]
> The steps in ADE articles are the same whether you're using Apple Business or Apple School Manager. For brevity, those articles refer to *Apple Business* only, except where clarification is necessary.  

## Supported platforms

Microsoft Intunee supports automated device enrollment for Apple mobile devices, which include iOS/iPadOS, tvOS, and visionOS. 

| Platform | Setup article |What it's for|
|----------|---------------|-------------|
| iOS/iPadOS | [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md) | User affinity, no user affinity|
| tvOS| [Set up an enrollment profile for tvOS](setup-tvos.md)| No user affinity|
| visionOS| [Set up an enrollment profile for visionOS](setup-visionos.md)| No user affinity|

Intune supports ADE for visionOS and tvOS devices using enrollment without user affinity. These devices are enrolled as corporate‑owned and receive device‑targeted policies. Configuration is delivered using custom configuration profiles.  

For macOS, see [Overview of Apple Automated Device Enrollment for macOS](automated-device-enrollment-overview-macos.md).  

## Supported scenarios

| Scenario | Supported |
|----------|-----------|
| Supervised mode | ✅ ADE devices are supervised by default, giving you more management control. |
| Corporate-owned devices | ✅ Designed for devices purchased through Apple Business or Apple School Manager. |
| Zero-touch deployment | ✅ Devices can ship directly to users. Enrollment starts when they turn on the device. |
| Bulk enrollment | ✅ Enroll a few devices or thousands using a single enrollment profile. |
| Devices with a single assigned user | ✅ Supported on iOS/iPadOS, not tvOS or visionOS.|
| Userless devices (kiosk, shared-use) | ✅ Supported on all Apple mobile platforms. |
| Microsoft Entra shared device mode | ✅ Supported on iOS/iPadOS for frontline worker scenarios. |
| Apple Shared iPad | ✅ Supported on iPadOS. |
| BYOD or personal devices | ❌ Not supported. Use [MAM](../../intune-service/fundamentals/deployment-guide-enrollment-mamwe.md) or [user and device enrollment](setup-user-company-portal.md) instead. |
| Device enrollment manager (DEM) accounts | ❌ Not supported. |
| Devices managed by another MDM provider | ❌ Users must unenroll from their current MDM provider before enrolling in Intune. For help migrating devices, see [Apple making device migration to Microsoft Intune easy with upcoming OS 26 release](https://techcommunity.microsoft.com/blog/IntuneCustomerSuccess/apple-making-device-migration-to-microsoft-intune-easy-with-upcoming-os-26-relea/4439895) on the Microsoft Community Hub. |


## How ADE works

Setting up ADE in Intune involves three main tasks:

1. **Get an enrollment program token**: Create a trust relationship between Intune and Apple Business. This is typically a one-time setup task per token. For steps, see [Set up an iOS/iPadOS ADE token](token-setup-apple.md).

2. **Create and assign an enrollment profile**: Configure the enrollment experience for your devices, including user affinity, authentication method, and Setup Assistant screens. Then assign the profile to device groups. For steps, see [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md).

3. **Sync and distribute devices**: Sync device records from Apple Business to Intune, then distribute devices to users. Enrollment starts automatically through Apple Setup Assistant when a device is turned on. For steps, see [Manage iOS/iPadOS ADE devices and tokens](manage-devices-tokens-apple.md).

## What is supervised mode?

Supervised mode provides more management control over corporate-owned devices, so you can do things like block screen captures and restrict AirDrop.

Corporate-owned devices running iOS/iPadOS 11 and later and enrolled through automated device enrollment should always be in supervised mode, which you can turn on in the enrollment profile. For more information about supervised mode, see [Turn on iOS/iPadOS supervised mode](enable-supervised-mode.md). Microsoft Intune ignores the *is_supervised* flag for devices running iOS/iPadOS 13.0 and later because these devices are automatically put in supervised mode at the time of enrollment.  

## Certificates

This enrollment type supports the Automated Certificate Management Environment (ACME) protocol. ACME is supported on iOS 16.0 and iPadOS 16.1 or later. Already-enrolled devices don't receive an ACME certificate unless they re-enroll. For details, see [Certificates](automated-device-enrollment-overview-apple.md#certificates) in the ADE overview. 

## Enrolling devices in shared device mode

You can set up automated device enrollment for devices in [shared device mode](/azure/active-directory/develop/msal-ios-shared-devices). *Shared device mode* is a feature of Microsoft Entra ID that enables frontline workers to share a single device throughout the day, signing in and out as needed. For more information about how to enable enrollment for devices in Microsoft Entra shared device mode, see [Automated device enrollment for shared device mode](setup-automated-shared-device-mode.md).  

## Before you begin

Before setting up ADE in Intune, make sure you have the following in place across all platforms:

* Access to [Apple Business](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/).
* An [Apple MDM push certificate in Intune](create-mdm-push-certificate.md).
* An active ADE token (.p7m file) linking your Apple Business or Apple School Manager account to Intune. For steps, see [Set up an ADE token](token-setup-apple.md).
* New or wiped corporate-owned devices purchased through Apple Business or Apple School Manager.

Additionally, decide how you want users to authenticate:

- **Setup Assistant with modern authentication** (recommended):
  - Supported on iOS/iPadOS 13.0 and later.  
  - Supports multifactor authentication and just-in-time (JIT) registration, eliminating the need for the Company Portal app if configured with a device configuration policy.  

- **Intune Company Portal app**:
  - Also supports modern authentication and multifactor authentication.  
  - Still requires users to complete Microsoft Entra registration through the app.  

- **Setup Assistant (Legacy)**:
  - Supports devices running iOS/iPadOS earlier than 13.0.  
  - Not recommended or supported.  

> [!IMPORTANT]
> We recommend using **Setup Assistant with modern authentication** for all Automated Device Enrollment (ADE) scenarios with user device affinity. Avoid using legacy authentication.

tvOS and visionOS enrollment happens without user affinity. Authentication selection isn't required for these types of devices. For more information about authentication options, see [Authentication methods for automated device enrollment](ref-automated-authentication-methods.md).  

## Next steps

- [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md) 
- [Set up an enrollment profile for tvOS](setup-tvos.md)  
- [Set up an enrollment profile for visionOS](setup-visionos.md)  