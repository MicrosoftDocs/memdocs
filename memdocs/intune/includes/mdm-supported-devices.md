---
author: ErikjeMS
ms.author: erikje
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.topic: include
ms.date: 01/19/2022
ms.localizationpriority: high
---

### Apple

- Apple iOS 13.0 and later
- Apple iPadOS 13.0 and later
- macOS 10.15 and later

> [!NOTE]
> Intune requires iOS 13.x or higher for device enrollment scenarios and app configuration delivered through Managed devices app configuration policies.
> 
> For Intune app protection policies and app configuration delivered through Managed apps App configuration policies, Intune requires iOS 14.x or later.

### Google

- Android 8.0 and later (including Samsung KNOX Standard 2.4 and higher: [requirements](https://www.samsungknox.com/en/knox-platform/supported-devices/2.4+))
- Android enterprise: [requirements](https://support.google.com/work/android/topic/9428066)  

[!INCLUDE [android-supported-os](android-supported-os.md)]

### Microsoft

- Windows 11 (Home, S, Pro, Education, and Enterprise editions)

    > [!NOTE]
    > You can continue to use Microsoft Endpoint Manager to manage devices running Windows 11 the same as with Windows 10. If another article doesn't explicitly reference Windows 11, assume that feature support for Windows 10 also includes Windows 11.
    >
    > Some features may not be available on Windows 11. This article lists some [known issues](#windows-11-known-issues). As always, test your policies before broadly deploying them across your devices.

- Surface Hub
- Windows 10 (Home, S, Pro, Education, and Enterprise versions)
- Windows 10 and Windows 11 Cloud PCs on Windows 365
- Windows 10 Enterprise 2021 LTSC
- Windows 10 Enterprise 2019 LTSC

  For more information about managing devices running Windows 10 2019 LTSC, see [What's new in Windows 10 Enterprise 2019 LTSC](/windows/whats-new/ltsc/whats-new-windows-10-2019)

- Windows 10 IoT Enterprise (x86, x64)
- Windows Holographic for Business

  For more information about managing devices running Windows Holographic for Business, see [Window Holographic for Business support](../fundamentals/windows-holographic-for-business.md).

- Windows 10 Teams (Surface Hub)

  For more information about managing devices running Windows 10 Teams, see [Manage Surface Hub with MDM](/surface-hub/manage-settings-with-mdm-for-surface-hub)

- Windows 10 version 1709 (RS3) and later, Windows 8.1 RT, PCs running Windows 8.1 (Sustaining mode)

> [!NOTE]
> Not all Windows editions support all available operating system features being configured through MDM. For more information, see the [Windows configuration service provider reference docs](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers). Each CSP highlights which Windows editions are supported.

Customers with Enterprise Management + Security (EMS) can also use [Azure Active Directory (Azure AD) to register Windows 10 devices](../enrollment/windows-enroll.md).

For guidelines on using Windows 10 virtual machines with Intune, see [Using Windows 10 virtual machines](../fundamentals/windows-10-virtual-machines.md).

> [!NOTE]
> Intune does not currently support managing UWF enabled devices. For more information, see [Unified Write Filter (UWF) feature](/windows-hardware/customize/enterprise/unified-write-filter).

### Windows 11 known issues

- Multi-app kiosk mode isn't currently available. Windows 11 only supports the use of a single app in kiosk mode. For more information, see the following articles:
  - [Set up a multi-app kiosk on Windows devices](/windows/configuration/lock-down-windows-10-to-specific-apps)
  - [Windows device settings to run as a dedicated kiosk using Intune](../configuration/kiosk-settings.md)

- Management capabilities to deliver customized Start and Taskbar experiences are currently limited. For more information, see the following articles:

  - [Supported configuration service provider (CSP) policies for Windows 11 Start menu](/windows/configuration/supported-csp-start-menu-layout-windows)
  - [Supported configuration service provider (CSP) policies for Windows 11 taskbar](/windows/configuration/supported-csp-taskbar-windows)
  - [Windows device settings to allow or restrict features using Intune](../configuration/device-restrictions-windows-10.md)
