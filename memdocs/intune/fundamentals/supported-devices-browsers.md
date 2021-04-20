---
# required metadata

title: Operating systems and browsers supported by Microsoft Intune
titleSuffix: 
description: Lists supported device platforms and browsers for Intune device management
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/14/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 5d1ac59c-a885-4276-8576-f3cf81c2d268

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started; seodec18
ms.collection: M365-identity-device-management
---

# Supported operating systems and browsers in Intune

Before setting up Microsoft Intune, review the supported operating systems and browsers.

For help installing Intune on your device, see [using managed devices to get work done](../user-help/use-managed-devices-to-get-work-done.md) and [Intune network bandwidth usage](network-bandwidth-use.md).

For more information on configuration service provider support, visit the [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference).

> [!NOTE]
> Intune requires Android 6.x or higher for applications and devices to access company resources via the Company Portal app for Android and the Intune App SDK for Android. This requirement does NOT apply to Polycom Android-based Teams devices running 4.4. These devices will continue to be supported.

## Intune supported operating systems

You can manage devices running the following operating systems:

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

> [!NOTE]
> Intune does not currently support managing UWF enabled devices. See [Unified Write Filter (UWF) feature](/windows-hardware/customize/enterprise/unified-write-filter) for more information.

### Supported Samsung Knox Standard devices

To avoid Knox activation errors that prevent MDM enrollment, the Company Portal app only attempts Samsung Knox activation during MDM enrollment if the device appears in the [list of supported Knox devices](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Devices that don't support Samsung Knox activation enroll as standard Android devices. A Samsung device might have some model numbers that support Knox, while others don't. Verify Knox compatibility with your device reseller before you buy and deploy Samsung devices.

> [!NOTE]
> Enrolling Samsung Knox devices may require you to [enable access to Samsung servers](https://support.samsungknox.com/hc/articles/115013833108-Our-corporate-devices-are-behind-a-firewall-How-do-I-enable-Knox-Workspace-devices-to-contact-Samsung-servers).

The following list of Samsung device models do not support Knox. They are enrolled as native Android devices by the Company Portal app for Android:

| **Device Name** | **Device Model Numbers** |
| --- | --- |
| Galaxy Avant | SM-G386T |
| Galaxy Core 2/Core 2 Duos | SM-G355H<br>SM-G355M |
| Galaxy Core Lite | SM-G3588V |
| Galaxy Core Prime | SM-G360H |
| Galaxy Core LTE | SM-G386F<br>SM-G386W |
| Galaxy Grand | GT-I9082L<br>GT-I9082<br>GT-I9080L |
| Galaxy Grand 3 | SM-G7200 |
| Galaxy Grand Neo | GT-I9060I |
| Galaxy Grand Prime Value Edition | SM-G531H |
| Galaxy J Max | SM-T285YD |
| Galaxy J1 | SM-J100H<br>SM-J100M<br>SM-J100ML |
| Galaxy J1 Ace | SM-J110F<br>SM-J110H |
| Galaxy J1 Mini | SM-J105M |
| Galaxy J2/J2 Pro | SM-J200H<br>SM-J210F |
| Galaxy J3 | SM-J320F<br>SM-J320FN<br>SM-J320H<br>SM-J320M |
| Galaxy K Zoom | SM-C115 |
| Galaxy Light | SGH-T399N |
| Galaxy Note 3 | SM-N9002<br>SM-N9009 |
| Galaxy Note 7/Note 7 Duos | SM-N930S<br>SM-N9300<br>SM-N930F<br>SM-N930T<br>SM-N9300<br>SM-N930F<br>SM-N930S<br>SM-N930T |
| Galaxy Note 10.1 3G | SM-P602 |
| Galaxy S2 Plus | GT-I9105P |
| Galaxy S3 Mini | SM-G730A<br>SM-G730V |
| Galaxy S3 Neo | GT-I9300<br>GT-I9300I |
| Galaxy S4 | SM-S975L |
| Galaxy S4 Neo | SM-G318ML |
| Galaxy S5 | SM-G9006W |
| Galaxy S6 Edge | 404SC |
| Galaxy Tab A 7.0&quot; | SM-T280<br>SM-T285 |
| Galaxy Tab 3 7&quot;/Tab 3 Lite 7&quot; | SM-T116<br>SM-T210<br>SM-T211 |
| Galaxy Tab 3 8.0&quot; | SM-T311 |
| Galaxy Tab 3 10.1&quot; | GT-P5200<br>GT-P5210<br>GT-P5220 |
| Galaxy Trend 2 Lite | SM-G318H |
| Galaxy V Plus | SM-G318HZ |
| Galaxy Young 2 Duos | SM-G130BU |

## Intune supported web browsers

Different administrative tasks require that you use one of the following administrative websites.

- [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Azure portal](https://portal.azure.com/)

The following browsers are supported for these portals:

- Microsoft Edge (latest version)
- Safari (latest version, Mac only)
- Chrome (latest version)
- Firefox (latest version)