---
title: Get started with frontline worker (FLW) device management
description: Learn how to manage frontline worker devices using Android, iOS/iPadOS, and Windows devices in Microsoft Intune. Get guidance on device use and Intune features built for FLW, like Remote Help. Also, learn about Microsoft Entra shared device mode (SDM) for FLW. 
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 08/19/2024
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: cbernier
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Frontline worker device management overview in Microsoft Intune

A frontline worker (FLW) is a person that works in an essential or critical role to your business. They're typically in direct contact with the public and customers. During a crisis or emergency, like a pandemic or natural disaster, frontline workers are often at the forefront of the response effort, providing critical services and support.

Some popular examples of frontline workers include healthcare, emergency responders, law enforcement, retail & food service, and transportation.

The articles in this section apply to:

- [FLW Android devices owned by the organization and enrolled in Intune](frontline-worker-overview-android.md)
- [FLW iOS and iPadOS devices owned by the organization and enrolled in Intune](frontline-worker-overview-ios-ipados.md)
- [FLW Windows devices owned by the organization and enrolled in Intune](frontline-worker-overview-windows.md)

> [!NOTE]
> FLW devices are typically owned by the organization. End user personal devices can be used as FLW devices, but personal devices aren't covered in these articles. This set of articles focus on corporate-owned devices.

Frontline workers rely on devices to enable their productivity, like devices used to scan barcodes or devices utilized for field operations. If these devices fail, worker productivity and business operation can stop. Often, these types of devices can be categorized as mission critical.

The articles in this section provide guidance on managing and configuring frontline worker (FLW) devices using Intune. These devices play a key role in running business operations. And, they're an extension of the operator who uses and relies on the device to be productive for day-to-day business operations.

## Before you begin

When you're planning for FLW devices (including rugged devices) and how you manage them, there are questions you need to answer. These questions help you determine the best device management experience for you, your end user frontline workers, and the needs of your organization.

- Determine how the **devices will be used**.

  For example, you can provide a device wide experience where frontline workers access all the apps and settings on the device. Or, provide a locked screen experience where frontline workers only access specific apps. You can configure the device for a single purpose, like scanning inventory. Or, configure the device for multiple purposes, like using an app to check in customers and using another app to check email.

  Intune has built-in kiosk features that can run one app or run many apps for Android, iPadOS, and Windows. This article provides more details about these device management scenarios.

- Determine if the **devices will be shared** with other users, or if the devices are assigned to specific users.

  For example, if the devices are part of a shared pool, then your device management strategy should focus on shared device management. If the devices are assigned to specific users, then your device management strategy should focus on user associated device management.

  Intune has built-in features that offer shared device management for Android, iPadOS, and Windows devices. This article provides more details about shared devices, and the decisions you need to make.

- Determine the **sign-in/sign-out experience** and how user switching happens, including device hand-off. For example, before cradling the device for charging, you might want users to sign out of apps.

  Intune has built-in features that allow users to sign in as a guest, sign in with their Microsoft Entra organization credentials, or only sign into apps. There are also features that use single sign-on and single sign-out for your apps. This article provides more details about these features.

- Determine the **starting app experience**. For example, users can sign in to the device and then launch an app, or users can get the device and have an app automatically start.

  Intune has built-in features that allow you to configure the starting app experience. This article provides more details about these features.

When you have this information, the next step is to identify the platforms you use and the devices scenarios.

## Intune features designed for FLW

Intune has built-in features that can be used for frontline worker devices, including:

- **[Windows cloud configuration](../../intune/fundamentals/cloud-configuration.md)**

  This feature is a guided scenario and can turn a Windows client device into a cloud-optimized device. It simplifies the devices, and secures them with Microsoft-recommended security features.

  For more information on this guided scenario and the other guided scenarios available, go to:

  - [Guided scenario - Windows 10/11 in cloud configuration](../../intune/fundamentals/cloud-configuration.md)
  - [Step-by-step guide - Windows 10/11 in cloud configuration](../../intune/fundamentals/cloud-configuration-setup-guide.md)
  - [Intune guided scenarios overview](../../intune/fundamentals/guided-scenarios-overview.md)

- **[Remote Help](../../intune/fundamentals/remote-help.md)**

  This feature is cloud-based solution that secures help desk connections. With these connections, your support staff can remote connect to FLW devices on:

  - [Android](../../intune/fundamentals/remote-help-android.md)
  - [macOS](../../intune/fundamentals/remote-help-macos.md)
  - [Windows](../../intune/fundamentals/remote-help-windows.md)

- **[Specialty devices](../../intune/fundamentals/specialty-devices-with-intune.md)**

  These devices include augmented reality (AR) & virtual reality (VR) headsets, large smart-screen devices, and some conference room meeting devices, like Microsoft Teams Rooms devices. They can be managed using Intune policies.

> [!NOTE]
> Some features may require additional licenses. For more information, go to [Intune Suite add-on capabilities](../../intune/fundamentals/intune-add-ons.md) or [Microsoft Intune licensing](../../intune/fundamentals/licenses.md).

## Microsoft Entra shared device mode for FLW

Microsoft Entra shared device mode (SDM) is designed for frontline workers (FLW). It's an Entra feature that focuses on building apps so many users can use the apps on the same device. Users sign in/sign out of apps, have all their data removed, and have the device ready for the next user.

Some of the benefits of Entra SDM include:

- Entra SDM supports multiple users on devices designed for one user. Some mobile devices running Android and iOS are designed for single users. Most apps optimize their experience for a single user. Apps built with Entra SDM support multiple users on one device.

- Entra SDM does automatic single sign-in and single sign-out. Employees can sign in once and get single sign-on (SSO) to all apps that support Entra SDM, giving them faster access to information.

  This feature is good for organizations with a set of apps in a device pool that employees share. Devices can be immediately ready for use by the next employee with no access to the previous user's data.

- Apps built for Entra SDM use the Microsoft Authentication Library (MSAL) and the Microsoft Authenticator app. When a device is in shared device mode, and with (MSAL) and the Microsoft Authenticator app, Microsoft provides information to your app. This information allows the app to modify its behavior based on the state of the user on the device, which helps protect user data.

Shared device mode (SDM) is a feature of Microsoft Entra. It's not an Intune feature. On Android, Entra SDM and Intune can work together. On iOS/iPadOS, you must use Entra SDM or use Intune. For more information, go to the following articles:

- [Frontline worker for Android devices in Microsoft Intune](frontline-worker-overview-android.md)
- [Frontline worker for iOS/iPadOS devices in Microsoft Intune](frontline-worker-overview-ios-ipados.md)

For more information on Entra SDM, go to [Overview of shared device mode](/azure/active-directory/develop/msal-shared-devices).

## More Microsoft services for FLW

**Microsoft 365 for frontline workers** is a licensing option designed for frontline worker scenarios. It's ideal for a mobile workforce that primarily interacts with customers and needs to stay connected to the rest of the organization. It interacts with other apps and services, including Microsoft Teams, Outlook, SharePoint, and more.

For more information and to get started, go to:

- [Get started with Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-overview)
- [Choose your scenarios for Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-choose-scenarios)

**Windows 365 Frontline** is a version of Windows 365 that provides a single license to provision some Cloud PC virtual machines. It can help organizations save costs. It's ideal for workers who share computing resources and don't require 24/7 devices, including users who:

- Are on a rotation schedule
- Work across time zones and regions
- Are part-time workers
- Are contingent staff

For more information and to get started, go to:

- [Windows 365 Frontline](https://www.microsoft.com/windows-365/frontline)
- [What is Windows 365 Frontline?](/windows-365/enterprise/introduction-windows-365-frontline)

## Related articles

- [FLW for Android devices](frontline-worker-overview-android.md)
- [FLW for iOS/iPadOS devices](frontline-worker-overview-ios-ipados.md)
- [FLW for Windows devices](frontline-worker-overview-windows.md)
- [Microsoft Intune securely manages identities, manages apps, and manages devices](../../intune/fundamentals/what-is-intune.md)
- [Microsoft Intune planning guide](../../intune/fundamentals/intune-planning-guide.md)
- [Migration guide: Set up or move to Microsoft Intune](../../intune/fundamentals/deployment-guide-intune-setup.md)
