---
author: MandiOhlinger
ms.author: mandia
ms.topic: include
ms.date: 10/14/2025
---

### Apple

- **Devices with user affinity** - devices enrolled with user affinity using ADE (automated device enrollment) or personally enrolled devices.
- Supported:
  - iOS/iPadOS 17.x and later
  - macOS 14.x and later
- **Devices without user affinity** - devices enrolled without user affinity using ADE (automated device enrollment) or Apple Configurator.
  - Supported:
    - iOS/iPadOS 17.x and later
    - macOS 14.x and later
  - Allowed to enroll:
    - iOS/iPadOS 15.x and later
    - macOS 12.x and later

> [!NOTE]
> **Supported** versions include devices running the three most recent operating system versions. These devices can enroll and take advantage of all Intune functionality that's applicable, and all new eligible features work on these devices.
>
> **Allowed** versions include devices running a non-supported version (within three versions of the supported versions). These devices can enroll and take advantage of Intune's eligible features but there's no guarantee that they'll work as expected.
>
> Intune requires iOS/iPadOS 17.x or later for app protection policies and app configuration.

### Android

**Android 10.0 and later for user-based management methods**. These methods are:

- Android Enterprise personally owned with a work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator ([Intune ended support for Android device administrator on devices with GMS in December 2024](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443))

**Android 8.0 and later for userless management methods**. These methods are:

- Android Enterprise dedicated
- AOSP userless

**Additional**

- Samsung KNOX Standard 3.0 and higher: [requirements](https://www.samsungknox.com/en/knox-platform/supported-devices/2.4+)
- Android open source project devices: [See here for the list of supported devices](../fundamentals/android-os-project-supported-devices.md)

[!INCLUDE [android-supported-os](android-supported-os.md)]

### Linux

- Ubuntu Desktop 22.04 LTS with a GNOME graphical desktop environment
- Ubuntu LTS, version 24.04
- RedHat Enterprise Linux 8
- RedHat Enterprise Linux 9

> [!NOTE]
> Ubuntu Desktop already has a GNOME graphical desktop environment installed.

### Microsoft

- Windows 11 Home, S, Pro, Pro Education, Education, Enterprise, and IoT Enterprise editions
- Windows 10/11 Cloud PCs on Windows 365

  You can continue to use Microsoft Intune to manage devices running Windows 11 the same as with Windows 10. If another article doesn't explicitly reference Windows 11, assume that feature support for Windows 10 also includes Windows 11.

  Some features might not be available on Windows 11. This article lists some [known issues](#windows-11-known-issues). As always, test your policies before broadly deploying them across your devices.

- Windows 10 LTSC 2019/2021 and Windows 11 LTSC 2024 (Enterprise and IoT Enterprise editions)

- Windows Holographic for Business

  For more information about managing devices running Windows Holographic for Business, see [Windows Holographic for Business support](../fundamentals/windows-holographic-for-business.md).

> [!NOTE]
> Not all Windows editions support all available operating system features being configured through MDM. For more information, see the [Windows configuration service provider reference docs](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers). Each CSP highlights which Windows editions are supported.

Customers with Enterprise Management + Security (EMS) can also use [Microsoft Entra ID to register Windows devices](../enrollment/windows-enroll.md).

For guidelines on using Windows virtual machines with Intune, see [Using Windows virtual machines](../fundamentals/windows-10-virtual-machines.md).

> [!IMPORTANT]
>
> - [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]
> - Intune doesn't currently support managing UWF enabled devices. For more information, see [Unified Write Filter (UWF) feature](/windows-hardware/customize/enterprise/unified-write-filter).

### Windows 11 known issues

- Currently, you can use Intune to configure a single-app kiosk on Windows 11 devices. For more information about Windows 11 multi-app kiosk support, go to [Set up a multi-app kiosk on Windows 11 devices](/windows/configuration/lock-down-windows-11-to-specific-apps).

  For more information on dedicated kiosk devices in Intune, go to [Windows and Windows Holographic for Business device settings to run as a dedicated kiosk using Intune](../configuration/kiosk-settings.md).

- Management capabilities to deliver customized Start and Taskbar experiences are currently limited. For more information, see the following articles:

  - [Supported configuration service provider (CSP) policies for Windows 11 Start menu](/windows/configuration/supported-csp-start-menu-layout-windows)
  - [Supported configuration service provider (CSP) policies for Windows 11 taskbar](/windows/configuration/supported-csp-taskbar-windows)
  - [Windows device settings to allow or restrict features using Intune](../configuration/device-restrictions-windows-10.md)
