---
# required metadata

title: Operating systems and browsers supported by Microsoft Intune
titleSuffix: 
description: Lists supported device platforms and browsers for Intune device management
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 01/19/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started; seodec18
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Supported operating systems and browsers in Intune

Before setting up Microsoft Intune, review the supported operating systems and browsers.

For more information on configuration service provider support, visit the [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference).  


## Intune supported operating systems

Intune supports devices running the following operating systems (OS):

* iOS
* Android 
* Windows
* macOS 

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

Supported platforms for MDE Integration: https://docs.microsoft.com/en-us/mem/intune/protect/mde-security-integration

### Supported Samsung Knox Standard devices  

Microsoft Intune only attempts Samsung Knox activation during enrollment on supported Knox devices. Devices that don't support Samsung Knox enroll as standard Android devices. For a list of devices that support Samsung Knox, see [Devices secured by Knox](https://www.samsungknox.com/knox-supported-devices/knox-workspace) on the Samsung Knox website. It's important to look for your device model number when verifying support, because some device models support Knox while others do not. Always verify Knox compatibility with your device reseller before you buy and deploy Samsung devices.  

> [!NOTE]
> You may need to enable access to Samsung servers to enroll Samsung Knox devices. For more information about enrollment, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).  

The Samsung device models in the following table do not support Knox solutions and features. Intune enrolls them as native Android devices. 

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

Device management and administrative tasks are done in the Microsoft Endpoint Manager admin center. Use these portals to access the admin center:  

- [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Azure portal](https://portal.azure.com/)

Microsoft Endpoint Manager is supported with the following web browsers: 

- Microsoft Edge (latest version)
- Safari (latest version, Mac only)
- Chrome (latest version)
- Firefox (latest version)  

## Next steps  
For network configuration requirements, or to learn more about setting up devices using the configuration service provider (CSP), see:

* [Intune network configuration requirements and bandwidth](network-bandwidth-use.md)   
* [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference)  
