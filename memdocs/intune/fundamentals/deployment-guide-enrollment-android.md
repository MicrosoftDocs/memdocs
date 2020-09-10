---
# required metadata

title: Android device enrollment guide for  Microsoft Intune - Azure | Microsoft Docs
description: Enroll Android and Android Enterprise work profile, fully managed, and dedicated devices in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Deployment guide: Enroll Android devices in Microsoft Intune

> [!WARNING]
> THIS GUIDE IS STILL BEING WRITTEN, AND MAY CONTAIN INCORRECT INFORMATION.

Personal and organization-owned devices can be enrolled in Intune. Once enrolled, they receive the policies and profiles you create. You have the following options when enrolling Android and Android Enterprise devices:

- [Android Enterprise personal with work profile (profile owner)](#android-enterprise-personal-with-work-profile)
- [Android Enterprise corporate-owned dedicated devices (COSU)](#android-enterprise-dedicated-devices)
- [Android Enterprise corporate-owned fully managed (COBO)](#android-enterprise-fully-managed)
- [Android Enterprise corporate-owned with personal profile (COPE)](#android-enterprise-corporate-with-personal-profile)
- [Android device administrator](#android-device-administrator)

This article provides recommendations on the Android and Android Enterprise enrollment methods to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll Android devices](../enrollment/android-enroll.md).

## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## Android Enterprise personal with work profile

These devices are personal or BYOD (bring your own device) Android devices that access organization email, apps, and other data.

---
| Feature | Use this enrollment option |
| --- | --- | 
| Devices are personal or BYOD. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
|Devices are managed by another MDM provider. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ |
| Devices are owned by the organization or school. | ❌ <br/><br/>Not recommended for organization-owned devices. Organization-owned devices should be enrolled using Android Enterprise fully managed. |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/> User-less or shared devices should be organization-owned. These devices should be enrolled using Android Enterprise dedicated devices. |

---

### Android Enterprise personal with work profile administrator tasks

This task list provides an overview. For more specific information, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an [enrollment restriction](../enrollment/enrollment-restrictions-set.md), and **allow** devices that support Android Enterprise work profiles. For the specific steps, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).

### Android Enterprise personal with work profile end user tasks

Your users must do the following steps. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
2. Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android Enterprise dedicated devices

These devices are organization-owned, with the only purpose of being a kiosk-style device. They're commonly referred to as COSU (corporate-owned, single-use) devices.

They're often shared devices, and aren't associated with a single or specific user. These devices are commonly used to scan items, print tickets, get digital signatures, manage inventory, and more. 

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using Android Enterprise work profile.|
| Devices are associated with a single user. | ❌ <br/><br/> Not recommended. These devices should be enrolled using Android Enterprise fully managed. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |

---

### Android Enterprise dedicated devices administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your dedicated device group(s) ready. For the specific steps, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

### Android Enterprise dedicated devices end user tasks

It's not recommended for users to enroll Android Enterprise dedicated devices. This task should be completed by administrators.

## Android Enterprise fully managed

These devices are organization-owned, and have one user. They're commonly referred to as COBO (corporate-owned, business only) devices.

They're used exclusively for organization work; not personal use.

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/>User-less devices should be enrolled using Android Enterprise dedicated devices. Also, an organization administrator can enroll. When the device is enrolled, create a [dedicated device](../configuration/device-restrictions-android-for-work.md#device-experience) profile, and assign this profile to this device. |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using Android Enterprise personal with work profile.|
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### Android Enterprise fully managed administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable fully managed user devices. For the specific steps, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

- Communicate to your users how they should enroll: Near Field Communication (NFC), Token, QR Code, or Google Zero Touch.

### Android Enterprise fully managed end user tasks

The specific steps depend on how you configured the enrollment profile. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

1. Users turn on the device, and are prompted for information, including the enrollment method: NFC, Token, QR Code, or Google Zero Touch. They may be asked to sign in with their organization credentials (`user@contoso.com`).
2. After they enter the required information, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android Enterprise corporate with personal profile

These devices are organization-owned, and have one user. They're commonly referred to as COPE (corporate-owned, personally enabled) devices.

They're used for organization work, and allow personal use.

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/>User-less devices should be enrolled using Android Enterprise dedicated devices. Also, an organization administrator can enroll. When the device is enrolled, create a [dedicated device](../configuration/device-restrictions-android-for-work.md#device-experience) profile, and assign this profile to this device. |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using Android Enterprise work profile.|
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### Android Enterprise corporate with personal profile administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise corporate-owned devices with personal profile](../enrollment/android-corporate-owned-work-profile-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable corporate-owned personal profile devices. For the specific steps, see [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md)..
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

### Android Enterprise corporate with personal profile end user tasks

The specific steps depend on how you configured the enrollment profile. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

1. Users turn on the device, and are prompted for information, including the enrollment method: NFC, Token, QR Code, or Google Zero Touch. They may be asked to sign in with their organization credentials (`user@contoso.com`).
2. After they enter the required information, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android device administrator

These Android devices are personal or BYOD (bring your own device) devices that can access organization email, apps, and other data.

Google is reducing device administrator support in new Android releases. To avoid reduced functionality, Microsoft recommends:

- Enroll new devices using [Android Enterprise work profiles](#android-enterprise-personal-with-work-profile) (in this article). Don't enroll new devices using Android device administrator.
- Create a device enrollment restriction to block device administrator enrollment. Android devices may try to enroll using device administrator before trying other enrollment methods. So, create the restriction to prevent this behavior. For more information, see [Set enrollment restrictions](../enrollment/enrollment-restrictions-set.md).
- If devices will update to Android 10, then migrate devices off device administrator management.
- Move existing Android device administrator devices to Android Enterprise work profiles. For more information, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md).

<!-- MandiA 9.10.2020: Commenting out this section.

### Android device administrator tasks

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable device administrator enrollment. For the specific steps, see [Android device administrator enrollment](../enrollment/android-enroll-device-administrator.md).

### Android device administrator end user tasks

Your users must do the following steps. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

-->

## Next steps

- [MAM-WE](deployment-guide-enrollment-mamwe.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)
