---
# required metadata

title: Android device enrollment guide for  Microsoft Intune
description: Enroll Android and Android Enterprise corporate-owned work profile, personally owned devices with a work profile, fully managed, AOSP, and dedicated devices in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chmaguir, priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Deployment guide: Enroll Android devices in Microsoft Intune

Personal and organization-owned devices can be enrolled in Intune. Once enrolled, they receive the policies and profiles you create. You have the following options when enrolling Android devices:

- [BYOD: Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile)
- [Android Enterprise corporate owned dedicated devices](#android-enterprise-dedicated-devices) (COSU)
- [Android Enterprise corporate owned fully managed](#android-enterprise-fully-managed) (COBO)
- [Android Enterprise corporate owned work profile](#android-enterprise-corporate-owned-work-profile) (COPE)
- [Android Open Source Project (preview)](#android-open-source-project) (AOSP)
- [Android device administrator](#android-device-administrator) (DA)

This article provides recommendations on the Android enrollment methods. It also includes an overview of the administrator and user tasks for each enrollment type.

For more specific information, see [Enroll Android devices](../enrollment/android-enroll.md). There's also a visual guide of the different enrollment options for each platform:

[![A visual representation of Intune enrollment options by platform](./media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## BYOD: Android Enterprise personally owned devices with a work profile

These devices are personal or BYOD (bring your own device) Android devices that access organization email, apps, and other data.

---
| Feature | Use this enrollment option when |
| --- | --- | 
| Use Google Mobile Services (GMS). | ✔️ |
| Devices are personal or BYOD. | ✔️ <br/><br/> You can mark these devices as corporate or personal. |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| You use the optional device enrollment manager (DEM) account. | ✔️ |
| Devices are managed by another MDM provider. | ❌ <br/><br/> When a device enrolls, MDM providers install certificates and other files. These files must be removed. The quickest way may be to unenroll, or factory reset the devices. If you don't want to factory reset, then contact the MDM provider. |
| Devices are owned by the organization or school. | ❌ <br/><br/>Not recommended for organization-owned devices. Organization-owned devices should be enrolled using [Android Enterprise fully managed](#android-enterprise-fully-managed) (in this article), or using [Android Enterprise corporate owned work profile](#android-enterprise-corporate-owned-work-profile) (in this article). |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/> User-less or shared devices should be organization-owned. These devices should be enrolled using Android Enterprise dedicated devices. |

---

### Android Enterprise personally owned devices with a work profile administrator tasks

This task list provides an overview. For more specific information, see [Set up enrollment of Android Enterprise personally owned work profile devices](../enrollment/android-work-profile-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).

### Android Enterprise personally owned devices with a work profile end user tasks

Your users must do the following steps. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal).
2. Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

> [!TIP]
> There is a short, step-by-step video to help your users in enroll their devices in Intune:
>
> [Enroll your Android device](https://www.youtube.com/watch?v=9Dl8HsGk4tI&t=3s)

## Android Enterprise dedicated devices

Previously referred to as COSU. These devices are organization-owned, and supported by Google’s Zero Touch. The only purpose is to be a kiosk-style device. They aren't associated with a single or specific user. These devices are commonly used to scan items, print tickets, get digital signatures, manage inventory, and more.

---
| Feature | Use this enrollment option when |
| --- | --- |
| Use Google Mobile Services (GMS). | ✔️ |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using [Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile) (in this article).|
| Devices are associated with a single user. | ❌ <br/><br/> Not recommended. These devices should be enrolled using Android Enterprise fully managed. |
| You use the optional device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |

---

### Android Enterprise dedicated devices administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Intune app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your dedicated device group(s) ready. For the specific steps, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

### Android Enterprise dedicated devices end user tasks

Admins can complete the enrollment themselves, and then give the devices to the users. Or, users can enroll the devices using the following steps:

1. Users turn on the device, and are prompted for information, including the enrollment method: NFC, Token, QR Code, or Google Zero Touch.
2. After they enter the required information, your enrollment profile applies to the device. When the enrollment wizard completes, the device is ready to use.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android Enterprise fully managed

Previously referred to as COBO. These devices are organization-owned, and have one user. They're used exclusively for organization work; not personal use.

---
| Feature | Use this enrollment option when |
| --- | --- |
| Use Google Mobile Services (GMS). | ✔️ |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/> User-less devices should be enrolled using Android Enterprise dedicated devices.|
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using [Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile) (in this article).|
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the optional device enrollment manager (DEM) account | ❌ <br/><br/> The DEM account isn't supported. |

---

### Android Enterprise fully managed administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable fully managed user devices. For the specific steps, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

- Communicate to your users how they should enroll: Near Field Communication (NFC), Token, QR Code, Google Zero Touch, or Samsung Knox Mobile Enrollment (KME).

  Using Samsung Knox Mobile Enrollment (KME), you can automatically enroll a large number of Android Enterprise Samsung Knox devices. For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

### Android Enterprise fully managed end user tasks

The specific steps depend on how you configured the enrollment profile. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

1. Users turn on the device, and are prompted for information, including the enrollment method: NFC, Token, QR Code, or Google Zero Touch. They may be asked to sign in with their organization credentials (`user@contoso.com`).
2. After they enter the required information, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android Enterprise corporate owned work profile

Previously referred to as COPE. These devices are organization-owned, and have one user. They're used for organization work, and allow personal use.

---
| Feature | Use this enrollment option when |
| --- | --- |
| Use Google Mobile Services (GMS). | ✔️ |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/>User-less devices should be enrolled using Android Enterprise dedicated devices. Also, an organization administrator can enroll. When the device is enrolled, create a [dedicated device](../configuration/device-restrictions-android-for-work.md#device-experience) profile, and assign this profile to this device. |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using [Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile) (in this article).|
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the optional device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### Android Enterprise corporate owned work profile administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise corporate owned work profile](../enrollment/android-corporate-owned-work-profile-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable corporate-owned personal profile devices. For the specific steps, see [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).
- Communicate to your users how they should enroll: Near Field Communication (NFC), Token, QR Code, Google Zero Touch, or Samsung Knox Mobile Enrollment (KME).

  Using Samsung Knox Mobile Enrollment (KME), you can automatically enroll a large number of Android Enterprise Samsung's Knox devices. For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

### Android Enterprise corporate owned work profile end user tasks

The specific steps depend on how you configured the enrollment profile. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

1. Users turn on the device, and are prompted for information, including the enrollment method: NFC, Token, QR Code, or Google Zero Touch. They may be asked to sign in with their organization credentials (`user@contoso.com`).
2. After they enter the required information, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android Open Source Project

> [!NOTE]
> Currently, there's limited OEM support for this enrollment method.

Also referred to as AOSP. Currently in [public preview](public-preview.md). These devices are organization-owned, and don't use Google Mobile Services (GMS). They can be kiosk-style devices that aren't associated with a single or specific user, or can have one user. They're used exclusively for organization work; not personal use.

When you create the Intune enrollment profile, you decide if the devices are userless, or are associated with a single user. For more information on these options, including supported OEMs, see:

- [Set up Intune enrollment for Android (AOSP) corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md)
- [Set up Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)

---
| Feature | Use this enrollment option when |
| --- | --- |
| Use Google Mobile Services (GMS). | ❌ <br/><br/> Device doesn't support [GMS](https://www.android.com/gms/) (opens Android's web site). Some countries don't support GMS. <br/><br/> If your devices will use GMS, then use [dedicated devices](#android-enterprise-dedicated-devices) (in this article) or [fully managed](#android-enterprise-fully-managed) (in this article) enrollment. |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ❌ <br/><br/> Can only enroll one device at a time. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> [Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile) (in this article) support [GMS](https://www.android.com/gms/) (opens Android's web site).|
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the optional device enrollment manager (DEM) account | ❌ <br/><br/> The DEM account isn't supported. |

---

### Android Open Source Project administrator tasks

This task list provides an overview. For more specific information, see enrollment for [AOSP corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md) and [AOSP corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required. New devices might not require a factory reset.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your device group(s) ready. For the specific steps, see:
  - [AOSP corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md) 
  - [AOSP corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)
- Enroll the devices in Intune. For the specific steps, see:
  - [AOSP corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md) 
  - [AOSP corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)

  During enrollment, the Microsoft Intune app and Microsoft Authenticator app automatically install and open on the device, which allows the device to enroll. The device is locked in the enrollment process until enrollment completes.

### Android Open Source Project end user tasks

The specific steps depend on how you configured the enrollment profile.

Admins can complete the enrollment themselves, and then give the devices to the users. Or, users can enroll the devices using the following steps:

1. Users turn on the device, and are prompted for information, including the enrollment method: QR Code. If you created a user-associated devices enrollment profile, then they may be asked to sign in with their organization credentials (`user@contoso.com`).
2. If you created a userless devices enrollment profile, then wait for the enrollment wizard to complete. When it does, the device is ready to use.

    If you created a user-associated devices enrollment profile, then users enter the required information. Then, wait for the enrollment wizard to complete. For more specific steps, see [enroll the device](../user-help/enroll-device-android-microsoft-intune-app.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Android device administrator

These Android devices are corporate, or personal/BYOD (bring your own device) devices that can access organization email, apps, and other data.

Google is reducing device administrator support in new Android releases. To avoid reduced functionality, Microsoft recommends:

- Enroll new devices using [Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile) (in this article). Don't enroll new devices using Android device administrator.
- Create a device enrollment restriction to block device administrator enrollment. Android devices may try to enroll using device administrator before trying other enrollment methods. So, create the restriction to prevent this behavior. For more information, see [Set enrollment restrictions](../enrollment/enrollment-restrictions-set.md).
- If devices will update to Android 10, then migrate devices off device administrator management.
- Move existing Android device administrator devices to [Android Enterprise personally owned devices with a work profile](#byod-android-enterprise-personally-owned-devices-with-a-work-profile) (in this article) or [corporate-owned work profiles](#android-enterprise-corporate-owned-work-profile) (in this article). For more information, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md).
- By default, device administrator enrollment is blocked on new tenants.

There are some situations when you must use Device Administrator enrollment:

- Android Enterprise requires access to Google services. Google services may not be available because of geography, or because of the device manufacturer. For example:

  - There are places where Google services aren’t available, like China. In this situation, use Android device administrator enrollment.  
  - Some devices are based on Android, but don't have access to Google Services, such as Amazon Fire tablets. In this situation, use Android device administrator enrollment.

- Android OS versions older than 5.0 must use Android device administrator enrollment. Android Enterprise enrollment isn't an option.

<!-- MandiA 9.10.2020: Commenting out this section.

### Android device administrator tasks

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable device administrator enrollment. For the specific steps, see [Android device administrator enrollment](../enrollment/android-enroll-device-administrator.md).

### Android device administrator end user tasks

Your users must do the following steps. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

-->

## Next steps

- [MAM](deployment-guide-enrollment-mamwe.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)
