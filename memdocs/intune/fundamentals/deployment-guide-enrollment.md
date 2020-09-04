---
# required metadata

title: Device enrollment guide for Microsoft Intune - Azure | Microsoft Docs
description: Enroll Android, iOS, iPadOS, macOS, and Windows devices In Intune. Decide which enrollment method to use, and get an overview of the adminstrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/03/2020
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

# Deployment guide: Enroll devices in Microsoft Intune

> [!WARNING]
> THIS GUIDE IS STILL BEING WRITTEN, AND MAY CONTAIN INCORRECT INFORMATION.

Azure AD is the backbone of Intune and Endpoint Manager. Once users and devices are registered within your Azure AD (also called a tenant), then it's available. There are a few ways to get these devices registered in Azure AD. This is called "enrollment".

Enrolling devices in Intune allows them to receive the policies you create. This includes compliance policies that help users and devices meet your rules. And, it includes configuration profiles that configure features and settings on devices.

When users enroll, a record is created in Azure AD

Intune includes several "parts": app configuration, app protection, user and device compliance, and device configuration. You can use these parts individually, or together. When users and devices enroll, they can receive these policies during enrollment. Or, they can receive your policies after they enroll. The order depends on your organization's needs.

Many organizations create a baseline of what all users and devices must have. Typically, these policies get deployed during enrollment. For example, you might also create VPN connection, install an authentication certificate, and require Windows Hello PIN. For more information on enrollment, see [What is device enrollment?](../enrollment/device-enrollment.md).

When a device is enrolled, it's issued an MDM certificate. This certificate communicates with the Intune service.

Another "enrollment" method is configuring and protecting apps. This isn't a typical "enrollment" method, but it's commonly used on devices owned by your users.

This deployment guide includes details to enroll devices running different platforms, and separates the administrative tasks from the end user tasks.


Azure AD deployment guides: https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-deployment-plans

## Prerequisites

- Intune is set up, and ready to enroll users and devices. Be sure:

  - The [MDM Authority](../fundamentals/mdm-authority-set.md) is set to Intune, even when using [co-management](/configmgr/comanage/overview) with Intune + Configuration Manager.
  - [Intune licenses are assigned](../fundamentals/licenses-assign.md).

  For more information, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).

- Your devices [are supported](../fundamentals/supported-devices-browsers.md). This requirement includes devices that are co-managed, or hybrid Azure Active Directory (Azure AD) joined devices.

- Sign in as a member of the **Global Administrator** or **Intune Service Administrator** Azure AD roles. [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) has more information. If you created an Intune trial subscription, then the account that created the subscription is the **Global administrator**.

- Different platforms may have additional requirements. For example, iOS/iPadOS and macOS devices require an [MDM push certificate from Apple](../enrollment/apple-mdm-push-certificate-get.md). Any additional platform requirements are listed in this article.

  | Platform | Additional requirements |
  | --- | --- |
  | Android | none |
  | Android Enterprise | none |
  | iOS/iPadOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)<br/>Apple ID |
  | macOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) |
  | Windows | none |

- Have your users groups and device groups ready to receive your enrollment policies. If you haven't reviewed or created your group structure, and want some guidance, then see [Planning Guide: Task 4: Review existing policies and infrastructure](intune-planning-guide.md#task-4-review-existing-policies-and-infrastructure).

- If you're bulk enrolling devices, consider creating the **Device enrollment manager** (DEM) account. This account is an Intune permission that's applied to an Azure AD user account. The DEM account can enroll up to 1,000 mobile devices. Use this account to enroll and configure the devices before giving them to users.

  For more information, see [Enroll devices using a DEM account](../enrollment/device-enrollment-manager-enroll.md).

## Pilot groups

When assigning your profiles, start small, and use a staged approach. Assign the enrollment profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the enrollment profile to more pilot groups.

For more information and suggestions, see the [Planning guide: Task 5: Create a rollout plan](../fundamentals/intune-planning-guide.md#task-5-create-a-rollout-plan).

## Unenroll from existing MDM and factory reset

If devices are currently enrolled in another MDM provider, then unenroll the devices from the existing MDM provider. Typically, unenrolling doesn't remove existing features and settings you configured. Most MDM providers have remote actions that remove organization-specific data from devices. Before enrolling in Intune, you can remove organization-specific data from these devices. But, it's not required.

Depending on the platform, a factory reset may be required before enrolling in Intune.

-----
| Platform | Factory reset required? |
| --- | --- |
| Android device administrator | No |
| Android Enterprise dedicated devices (COSU) | Yes |
| Android Enterprise fully managed (COBO) | Yes |
| Android Enterprise work profile (profile owner) | No |
| iOS/iPadOS | Yes |
| macOS | Yes |
| Windows | No |

-----

On the platforms that don't require a factory reset, when these devices enroll in Intune, they'll start receiving your Intune policies. If you don't configure a setting in Intune, then Intune doesn't change or update that setting. So, it's possible that any previously configured settings remain configured on the device.

## Application management without enrollment (MAMWE)

MAM-WE isn't a traditional "enrollment" method, as it uses app protection policies to protect data within an app. Devices aren't enrolled. It's commonly used for personal or bring your own devices (BYOD), or for managed devices that need extra security. MAM-WE is also an option for users who don't enroll their personal devices, but still need access to organization email, Teams meetings, and more.

MAM-WE is available on the following platforms:

- Android
- iOS/iPadOS
- macOS
- Windows

This section provides recommendations on when to use MAM-WE. It also includes an overview of the administrator and user tasks. For more specific information on MAM-WE, see [Microsoft Intune app management](../apps/app-management.md).

---
| Feature | Use this enrollment option |
| --- | --- |
| You want to configure specifics apps, and control access to these apps, such as Outlook or Microsoft Teams. | ✔️ |
| Devices are personal or BYOD. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to manage a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are managed by another MDM provider. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ |
| Devices are owned by the organization or school. |  ❌ <br/><br/> Not recommended as the *only* enrollment method for organization-owned devices. Organization-owned devices should be enrolled and managed by Intune. If you want extra security for specific apps, then use enrollment and MAM-WE together. |
| Devices are user-less, such as kiosk, or dedicated device. | ❌ <br/><br/>Typically, user-less or shared devices are organization-owned. These devices should be enrolled and managed by Intune. |

---

#### MAM-WE administrator tasks

This task list provides an overview. For more specific information, see [Microsoft Intune app management](../apps/app-management.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), [add your apps](../apps/apps-supported-intune-apps.md). When they're added, they're considered "managed" by Intune. After you add the app, create an [app protection policy](../apps/app-protection-policy-settings-ios.md) that allows or blocks features within the app, such as copy and paste.
- Tell users how to get the app. For example, you can:

  - Direct users to the Company Portal web site at `portal.manage.microsoft.com`. When they sign in with their organization credentials, they see a list of apps, including required apps. They can download and install the apps from this site.
  - Have users download and install the Company Portal app from the app store. Once authenticated, users can install apps, including required apps.

#### MAM-WE end user tasks

The specific tasks depend on how you tell users to install the apps.

- To install the apps, users can:

  - Go to the app store, and download the app.
  - Go to the app store, and download the Company Portal app. The Company Portal app authenticates the user. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). They see a list of apps they can download and install, including required apps.
  - Go to the Company Portal web site at `portal.manage.microsoft.com`, and sign in with their organization credentials (`user@contoso.com`). Once signed in, they see a list of apps they can download and install, including required apps.

- After the app is installed, they open the app, and are prompted to sign in with their organization credentials (`user@contoso.com`). When users sign in, they may have to restart the app. After the restart, the app data is "managed" by Intune.

- Some platforms may require specific apps to install other apps, such as Outlook or Teams. For example, on iOS devices, users must install a broker app, such as the Microsoft Authenticator app. On Android devices, users must install the Company Portal app.

## Enroll Android devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling Android and Android Enterprise devices:

- [Android Enterprise work profile (profile owner)](#android-enterprise-work-profile)
- [Android Enterprise dedicated devices (COSU)](#android-enterprise-dedicated-devices)
- [Android Enterprise fully managed (COBO)](#android-enterprise-fully-managed)
- [Android device administrator](#android-device-administrator)

This section provides recommendations on the Android and Android Enterprise enrollment methods to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll Android devices](../enrollment/android-enroll.md).

### Android Enterprise work profile

These devices are personal or BYOD (bring your own device) Android devices that can access organization email, apps, and other data.

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

#### Android Enterprise work profile administrator tasks

This task list provides an overview. For more specific information, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an [enrollment restriction](../enrollment/enrollment-restrictions-set.md), and **allow** devices that support Android Enterprise work profiles. For the specific steps, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).

#### Android Enterprise work profile end user tasks

Your users must do the following. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Android Enterprise dedicated devices

These devices are organization-owned, with a sole purpose of being a kiosk-style. They can be shared devices, and aren't associated with a single or specific user. These devices are commonly used to scan items, print tickets, get digital signatures, manage inventory, and more. They're commonly referred to as COSU (corporate-owned, single-use) devices.

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

#### Android Enterprise dedicated devices administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your dedicated device group(s) ready. For the specific steps, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise dedicated devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

#### Android Enterprise dedicated devices end user tasks

It's not recommended for users to enroll Android Enterprise dedicated devices. This task should be completed by administrators.

### Android Enterprise fully managed

These devices are organization-owned, and have one user. They are used exclusively for organization work; not personal use. They're commonly referred to as COBO (corporate-owned, business only) devices.

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are owned by the organization or school. |  ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/>User-less devices should be enrolled using Android Enterprise dedicated devices. Also, an organization administrator can enroll. When the device is enrolled, create a [dedicated device](../configuration/device-restrictions-android-for-work.md#device-experience) profile, and assign this profile to this device. |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using Android Enterprise work profile.|
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

#### Android Enterprise fully managed administrator tasks

This task list provides an overview. For more specific information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable fully managed user devices. For the specific steps, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise fully managed devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

#### Android Enterprise fully managed end user tasks

It's not recommended for users to enroll Android Enterprise fully managed devices. This task should be completed by administrators.

### Android device administrator

> [!NOTE]
> Google is decreasing device administrator support in new Android releases. To avoid reduced functionality, Microsoft recommends:
>
> - Enroll new devices using [Android Enterprise work profiles](#android-enterprise-work-profile) (in this article). Do **not** enroll new devices using Android device administrator.
> - If devices will update to Android 10, then migrate devices off device administrator management.
> - Move existing Android device administrator devices to Android Enterprise work profiles. For more information, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md).

These Android devices are personal or BYOD (bring your own device) devices that can access organization email, apps, and other data.

#### Android device administrator administrator tasks

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable device administrator enrollment. For the specific steps, see [Android device administrator enrollment](../enrollment/android-enroll-device-administrator.md).

#### Android device administrator end user tasks

Your users must do the following. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Enroll iOS/iPadOS devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling iOS/iPadOS devices:

- [User and Device enrollment](#user-and-device-enrollment)
- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised)
- [Apple Configurator](#apple-configurator-enrollment)

This section provides recommendations on the iOS/iPadOS enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll macOS devices](../enrollment/ios-enroll.md).

### User and Device enrollment

These iOS/iPadOS devices are personal or BYOD (bring your own device) devices that can access organization email, apps, and other data. Starting with iOS 13 and newer, this enrollment option targets users or targets devices. It doesn't require resetting the devices.

When you create the enrollment profile, you're asked to to choose **User enrollment**, **Device enrollment** or **Determine based on user choice**.

For the specific enrollment steps, and its prerequisites, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).??Need to update the title of this article, is it applies to User enrollment and Device enrollment??

---
| Feature | Use this enrollment option |
| --- | --- |
| You want to help protect a specific feature on the device, such as per-app VPN. | ✔️ |
| Devices are personal or BYOD. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are managed by another MDM provider. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ |
| Devices are owned by the organization or school. |  ❌ <br/><br/> Not recommended. Organization-owned devices should be enrolled using Automated Device Enrollment or Apple Configurator. |
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/>Typically, user-less or shared devices are organization-owned. These devices should be enrolled using Automated Device Enrollment or Apple Configurator. |

---

#### User and Device enrollment administrator tasks

This task list provides an overview. For more specific information, see [Set up iOS/iPadOS and iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll iOS/iPadOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create the enrollment profile. When you create the enrollment profile, you have the following options:

  - **User enrollment**: Starting with iOS 13 and newer. This option configures a specific set of features and organization apps, such as password, per-app VPN, Wi-Fi, and Siri. If you use this enrollment method, to help secure apps and their data, it's strongly recommended to also use app protection policies. User enrollment is considered friendlier to end users, but may not provide the feature set and security Administrators need.

    For the complete list of what you can and can't do, see [Intune actions and options supported with Apple User Enrollment](../enrollment/ios-user-enrollment-supported-actions.md). For the specific user enrollment steps, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

    In some scenarios, user enrollment may not be the best option. Consider the following:

    - User enrollment creates a work partition on the devices. The features and security you configure in the user enrollment profile only exist in the work partition. They don't exist in the user partition. Users can't factory reset the work partition. Administrators can. Users can factory reset the personal partition. Administrators can't.

    - If users primarily use Microsoft apps, or use apps created with the [Intune App SDK](../developer/app-sdk.md), then users should download these apps from the Apple App Store. Then, use app protection policies to protect these apps. In this scenario, you don't need user enrollment.

    - For line of business (LOB) apps, user enrollment might be an option, as it'll deploy these apps to the work partition. MAM doesn't support LOB apps. So if you need LOB apps, then use User Enrollment.

    - When devices are enrolled using user enrollment, you can't switch to device enrollment. With user enrollment, you can't move an app from unmanaged to managed. Users must unenroll from user enrollment, and then re-enroll to device enrollment.

    - Apps installed before the user enrollment profile applies aren't protected or managed by the user enrollment profile.

      For example, a user downloads the Outlook app from the Apple App Store. The app automatically installs to the user partition on the device. The user configures Outlook for their personal email. When configuring their organization email, they're blocked by conditional access, and asked to enroll. They enroll, and a user enrollment profile deploys.

      Since the Outlook app was installed before the user enrollment profile, the user enrollment profile fails. The Outlook app can't be managed because it's installed and configured in the user partition, not the work partition. Users must manually uninstall the Outlook app.

      Once uninstalled, users can sync the device manually, and possibly re-apply the user enrollment profile. Or, you may have to create an app configuration policy to deploy Outlook, make it a required app, and then deploy an app protection policy to secure the app and its data.

  - **Device enrollment**: This option is a typical enrollment for personal devices. The device is managed, not just specifics apps or features. With this option, consider the following:

    - You can deploy certificates that apply to the whole device.
    - Users must install updates. Only devices enrolled using Automated Device Enrollment (ADE) can receive updates using MDM policies or profiles.
    - A user must be associated with the device. This user can be a device enrollment manager (DEM) account.

  - **Determine based on user choice**: Gives end users a choice when they enroll. Depending on their selection, **User enrollment** or **Device enrollment** is used.

- Assign the enrollment profile to user groups. Don't assign to device groups.

#### User and Device enrollment end user tasks

Your users must do the following. For the specific user experience, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md).

1. Go to the Apple App Store, and [install the Intune Company Portal app](../user-help/install-and-sign-in-to-the-intune-company-portal-app-ios.md).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md). 

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use on devices owned by your organization. This option configures settings using Apple Business Manager (ABM) or Apple School Manager (ASM). It enrolls a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your preconfigured settings, and can be shipped directly to users or schools. You create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and push this profile to the devices.

For more specific information on this enrollment type, see:

- [Apple Business Manager enrollment](../enrollment/device-enrollment-program-enroll-ios.md)
- [Apple School Manager enrollment](../enrollment/apple-school-manager-set-up-ios.md): For more information on Apple School Manager, see [Apple education](https://www.apple.com/education/k12/it/) (opens Apple's web site).

---
| Feature | Use this enrollment option |
| --- | --- |
| You want supervised mode, which includes deploying software updates, restricting features, allowing and blocking apps, and more. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using MAM-WE, or User and Device enrollment. |
| You have existing devices. | ❌ <br/><br/>Existing devices should be enrolled using Apple Configurator. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users must unenroll from the current MDM provider, and then enroll in Intune. Or, you can use MAM-WE to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

#### ADE administrator tasks

This task list provides an overview. For more specific information, see [Apple Business Manager enrollment](../enrollment/device-enrollment-program-enroll-ios.md) or [Apple School Manager enrollment](../enrollment/apple-school-manager-set-up-ios.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
- Be sure the Apple token (.p7m) is active. For more specific information, see [Get an Apple ADE token](../enrollment/device-enrollment-program-enroll-ios.md#get-an-apple-automated-device-enrollment-token).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll iOS/iPadOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- Decide how users will authenticate on their devices: the **Company Portal** app, or **Setup Assistant**. Make this decision before you create the enrollment profile.

  - Select the **Company Portal** app when:

    - You want to use multi-factor authentication (MFA).
    - You want to prompt users to update their expired password when they first sign in.
    - You want to prompt users to reset their expired passwords during enrollment.
    - You want devices registered in Azure AD. When they're registered, you can use features available with Azure AD, such as conditional access.
    - If your company uses the Volume Purchase Program (VPP), you can automatically install **Company Portal** app during enrollment without the users' Apple IDs.

  - Select the **Setup Assistant** when:

    - You don't want to use modern authentication features, such as MFA.
    - You want to wipe the device.
    - You want to import serial numbers.
    - You don't want to register the device in Azure AD. Setup Assistant authenticates the user with the Apple .p7m token. If you're fine with this, then you don't need to install the Company Portal app. Keep using the Setup Assistant. If you want the device registered in Azure AD, then install the **Company Portal** app. When you create the enrollment profile and select Setup Assistant, you have a choice to install or don't install the Company Portal app.

- If you use the Company Portal app, then decide how the Company Portal app will be installed on the devices. Make this decision before you create the enrollment profile.

  Devices enrolled using ADE aren't compatible with the Company Portal app version in the Apple App Store. Do not install this app store version. Instead, install the Company Portal app using the following options:

  - If you have the Volume Purchase Program (VPP), and you're enrolling new devices, then the Company Portal app is included. When you create the enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Install Company Portal with VPP**. No additional steps are needed. This option:

    - Includes the correct Company Portal app version.
    - You don't have to create another policy to deploy the Company Portal app to devices.
    - The Company Portal app must be updated manually by you, or your users.

  - If you have VPP, and devices are already enrolled, then:

    1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal app as a required app, and as a device licensed app.
    2. Create an app configuration policy that includes the Company Portal app as a device licensed app. For more specific information, see [Configure the Company Portal app to support iOS and iPadOS DEP devices](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices).
    3. Deploy the app configuration policy to the same device group as the enrollment profile.
    4. When devices check-in with the Intune service, it receives your profile, and the Company Portal app installs.

    This option:

    - Includes the correct Company Portal app version.
    - Requires you to create an enrollment profile, and create an app configuration policy. In your app configuration policy, make it a required app so you know it's deployed to all your devices.
    - The Company Portal app can be automatically updated by changing your existing app configuration policy.

  - ?? What happens if they don't have VPP? Is VPP required for ADE/DEP? If it's required, I'll add that to the requirements. If it's not required, how do they get the CP app? The following "option 1" and "option 1" paragraphs might no longer be needed. Will confirm once I confirm VPP requirement with PM. ??

  **Option 1**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), in your ADE enrollment profile, deploy the Company Portal app using the **Install Company Portal with VPP** (Volume Purchase Program) option. This option:

  - Includes the correct Company Portal app version.
  - You don't have to create another policy to deploy the Company Portal app to devices.
  - The Company Portal app must be updated manually by you, or your users.

  **Option 2**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an app configuration policy that deploys the Company Portal app to enrolled devices using the VPP. This option:

  - Includes the correct Company Portal app version.
  - Requires you to create an enrollment profile, and create an app configuration policy. In your app configuration policy, make it a required app so you know it's deployed to all your devices.
  - The Company Portal app can be automatically updated by changing your existing app configuration policy.

- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile:

  - Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).
  - Choose where users authenticate: the **Setup Assistant**, or the **Company Portal** app. Using the Company Portal app is considered modern authentication. It's recommended to select the Company Portal app.

  For more specific information and suggestions, see [Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

#### ADE end user tasks

When you create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you choose to associate a user to the device (with user affinity), or have shared devices (without user affinity). The specific steps depend on how you configured the enrollment profile.

- **Enroll with user affinity** + **Company Portal app**:

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. Once entered, the Company Portal app is automatically installed from your profile. It can take some time for the Company Portal app to auto-install.
  2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). When users sign-in, the enrollment starts. When enrollment completes, users can install and use apps used by your organization, including LOB apps.

  Users may have to enter more information. For more specific steps, see [Enroll your organization-provided iOS device](../user-help/enroll-your-device-dep-ios.md).

- **Enroll with user affinity** + **Setup Assistant**:

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`.
  2. The Setup Assistant prompts the user for information, and enrolls the device in Intune.

- **Enroll without user affinity**: No actions. Be sure they don't install the Company Portal app from the Apple App Store.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Apple Configurator enrollment

Use on devices owned by your organization, and includes [Direct Enrollment](../enrollment/device-enrollment-direct-enroll-macos.md). This option requires you to physically connect macOS devices to a Mac computer using the USB port.

For more specific information on this enrollment type, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

---
| Feature | Use this enrollment option |
| --- | --- |
| You need a wired connection, or are having a network issue. | ✔️ |
| Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements.  | ✔️ <br/><br/> The idea of *not* using the ABM or ASM portals is to give administrators less control.|
| A country doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM). | ✔️ <br/><br/> If your country supports ABS or ASM, then devices should be enrolled using Automatic Device Enrollment. |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> If you have a large number of devices, then this method will take some time. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using MAM-WE, or User and Device enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. Or, you can use MAM-WE to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

#### Apple Configurator administrator tasks

This task list provides an overview. For more specific information, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

- Requires access to a Mac computer with a USB port.
- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll iOS/iPadOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile.

  When you create an enrollment profile, you:

  - Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).

  - Choose where users authenticate: the Setup Assistant, or the Company Portal app. Using the **Company Portal** app is considered modern authentication.

    Select the **Company Portal** app when:

    - You want to use multi-factor authentication (MFA).
    - You want to prompt users to update their expired password when they first sign in.
    - You want to prompt users to reset their expired passwords during enrollment.
    - You want to automatically install **Company Portal** app during enrollment.

    Select the **Setup Assistant** when:

    - You don't want to use modern authentication features, such as MFA.
    - You want to wipe the device.
    - You want to import serial numbers.
    - You want to automatically install **Company Portal** app during enrollment, or you don't want to automatically install **Company Portal** app. It's recommended to install the **Company Portal** app during enrollment.

  - If you choose **Enroll without user affinity**, then you're automatically using **Direct enrollment**. Remember:

    - Users can't use apps that require a user, including the Company Portal app. Be sure users don't install the Company Portal app from the Apple App Store.
    - You use the settings from an existing macOS enrollment profile.

- When the enrollment profile is ready, USB connect the devices to the Mac, and open the **Apple Configurator** app. When the app opens, it detects the USB connected device, and deploys the Intune enrollment profile you created.

For more information on this enrollment option, and its prerequisites, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

#### Apple Configurator end user tasks

The tasks depend on the option you configured in the enrollment profile.

- If you select **Enroll with user affinity** and **Company Portal** app authentication, then users need to open the **Company Portal** app, and sign in with their organization account (`user@contoso.com`). When they sign-in, the enrollment starts. When enrollment completes, users can install and use apps used by your organization, including LOB apps.

- If you select **Enroll with user affinity** and **Setup Assistant** authentication, then users need to open the **Company Portal** app, and sign in with the organization account (`user@contoso.com`).

  If you chose to not install the **Company Portal** app when creating the enrollment profile, then users ust Setup Assistant. users go through all options.

  https://docs.microsoft.com/mem/intune/apps/app-configuration-policies-use-ios#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices

  If you don't install CP app, there's no CA, or Azure AD registrations. Recommended to install CP app. Admin should use app config, and push CP app to devices. Users should not install CP app from the Apple App Store. Then, users sign in, and are locked into CP app. They sign in with the organization account (`user@contoso.com`), and device is unlocked for users.

- If you select **Without user affinity (Direct enrollment)**, then there are no user actions. Be sure they don't install the Company Portal app from the Apple App Store.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Enroll macOS devices

Personal and organization-owned devices can be enrolled in Intune. On macOS devices, the Company Portal app or the Apple Setup Assistant authenticates users, and starts the enrollment. Once they're enrolled, they receive the policies and profiles you create.

You have the following options when enrolling macOS devices:

- [Device enrollment](#device-enrollment)
- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised-1)
- [Apple Configurator](#apple-configurator-enrollment-1)

This section:

- Describes your Company Portal app options for each enrollment method.
- Provides recommendations on the macOS enrollment method to use.
- Includes an overview of the administrator and user tasks for each enrollment type.

For more specific information, see [Enroll macOS devices](../enrollment/macos-enroll.md).

### Device enrollment

Use for personal or bring your own devices (BYOD). Not a traditional "enrollment" method, as it uses an app configuration profile. This option manages apps on the device. Devices aren't enrolled.

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are personal or BYOD. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| You have new or existing devices. | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are managed by another MDM provider. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ <br/><br/> Be aware of impact and any limitations using DEM account. |
| Devices are owned by the organization or school. | ❌ <br/><br/> Not recommended for organization-owned devices. Organization-owned devices should be enrolled using Automated Device Enrollment or Apple Configurator. |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/> These devices are organization-owned. User-less devices should be enrolled using Automated Device Enrollment or Apple Configurator. |

---

#### Device enrollment administrator tasks

This task list provides an overview.

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- There isn't a Company Portal app for macOS devices in the Apple App Store, or through VPP. Users must [manually download and run the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070). They sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the enrollment profile.

  When they approve, the device is added to your organization Azure AD. Then, it's available to Intune to receive your policies and profiles. Be sure to communicate this information with your users.

  For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### Device enrollment end user tasks

Your users must do the following. For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

1. Download and run [the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070).
2. Open the Company Portal app, and sign in with their organization account (`user@contoso.com`). Once they sign in, they must approve the enrollment profile. When users approve, the device is enrolled, and considered managed. If they don't approve, then they're not enrolled, and won't receive your policy and profiles.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

User: opens co portal app, goto system pref > profiles and approve profile --> Applies to macOS only for device enrollment.


### Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use on devices owned by your organization. This option configures settings using Apple Business Manager (ABM) or Apple School Manager (ASM). It enrolls a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your preconfigured settings, and can be shipped directly to users or schools. You create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and push this profile to the devices.

For more specific information on this enrollment type, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are owned by the organization or school. | ✔️ |
| You have new devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using Device enrollment. |
| You have existing devices. | ❌ <br/><br/>Existing devices should be enrolled using Apple Configurator. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users must unenroll from the current MDM provider, and then enroll in Intune. Or, you can use Device enrollment to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

#### ADE administrator tasks

This task list provides an overview. For more specific information, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
- Be sure the Apple token (.p7m) is active. For more specific information, see [Get an Apple ADE token](../enrollment/device-enrollment-program-enroll-macos.md#get-an-apple-ade-token).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile. Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices):

  - **Enroll with user affinity**: When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. The Setup Assistant authenticates the user, and enrolls the device. You can continue to use Setup Assistant for authentication. The device is enrolled, and ready to receive your policies and profiles. Setup Assistant uses the Apple token (.p7m) to know the user is a work account.  ??Are the accounts I listed for Setup Assistant correct? Does Setup Assistant add the user, the device, or both to Azure AD??

    ??Is the following correct??

    After the device is enrolled, you can also install the Company Portal app, and use it for authentication, instead of Setup Assistant. To install the Company Portal app on devices, add the Company Portal app [using one of the options](../apps/apps-company-portal-macos.md). Set the Company Portal app as a required app.

    Once installed, users open the Company Portal app, and sign in with their organization account (`user@contoso.com`). When they sign-in, they are authenticated, and ready to receive your policies and profiles.

  - **Enroll without user affinity**: Setup Assistant authenticates the user, and enrolls the user in Intune. The Company Portal app isn't used, needed, or supported on enrollments without user affinity.

  > [!NOTE]
  > For all organization-owned macOS devices, Setup Assistant is always and automatically used, even if you don't see "Setup Assistant" text in Endpoint Manager.

#### ADE end user tasks

These tasks depend on how administrators tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

- **Enroll with user affinity**:??

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. The Setup Assistant authenticates the user, and enrolls the device.

  2. If you're using the Company Portal app for authentication (instead of Setup Assistant), then the Company Portal app installs using [the option](../apps/apps-company-portal-macos.md) you configured.

      Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, users are authenticated, and can access organization resources.

- **Enroll without user affinity**: No actions. Be sure your users don't install the Company Portal app.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Apple Configurator enrollment

Use on devices owned by your organization, and includes [Direct Enrollment](../enrollment/device-enrollment-direct-enroll-macos.md). This option requires you to physically connect macOS devices to a Mac computer using the USB port.

For more specific information on this enrollment type, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md) and [Direct Enrollment for macOS devices](../enrollment/device-enrollment-direct-enroll-macos.md).

---
| Feature | Use this enrollment option |
| --- | --- |
| You need a wired connection, or are having a network issue. | ✔️ |
| Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements.  | ✔️ <br/><br/> The idea of *not* using the ABM or ASM portals is to give administrators less control.|
| A country doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM). | ✔️ <br/><br/> If your country supports ABS or ASM, then devices should be enrolled using Automatic Device Enrollment. |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> If you have a large number of devices, then this method will take some time. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated or shared. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using Device enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. Or, you can use Direct Enrollment to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

#### Apple Configurator administrator tasks

> [!NOTE]
> For all organization-owned macOS devices, Setup Assistant is always and automatically used, even if you don't see "Setup Assistant" text in Endpoint Manager.

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile. When you create an enrollment profile, you choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).

  **ENROLL WITH USER AFFINITY** ??Need to confirm this whole section. None of it makes sense since there's no CP app. Is it similar to macOS ADE user affinity??

  Choose where users authenticate: the **Setup Assistant**, or the **Company Portal** app. Using the **Company Portal** app is considered modern authentication.

  - Select the **Company Portal** app if you want to:

    - Use multi-factor authentication (MFA).
    - Prompt users to update their expired password when they first sign in.
    - Prompt users to reset their expired passwords during enrollment.

    <!-- Possible text??>

    Setup Assistant authenticates the user, and enrolls the user in Intune. After the device is enrolled, you can install the Company Portal app, and use it for authentication.

    To install the Company Portal app, in the Endpoint Manager admin center, add the Company Portal app using one of the options. Set the Company Portal app as a required app.

    Once installed, users open the Company Portal app, and sign in with their organization account (`user@contoso.com`). When they sign in, they're authenticated, and have access to your organization resources.

    <-->

    There isn't a Company Portal app for macOS devices in the Apple App Store, or through VPP. Your options:

    - **Option 1**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal app [using one of the options](../apps/apps-company-portal-macos.md). Set the Company Portal app as a required app.

      Once installed, users open the Company Portal app, and sign in with their organization account (`user@contoso.com`). When they sign in, they're authenticated, and have access to your organization resources.

      For more specific information, see [Add the macOS Company Portal app to Intune](../apps/apps-company-portal-macos.md).

    - **Option 2**: Users manually download and run the Company Portal app installer package. They sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the enrollment profile.

      When they approve, the device is enrolled, and ready to receive your policies and profiles.

      This option is more work for users, and less work for administrators. If your users aren't comfortable with downloading and running files, then consider deploying the Company Portal app using an app configuration policy (Option 1).

      For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

  - Select **Setup Assistant** if you:

    - You don't want to use modern authentication features, such as MFA.
    - You want to wipe the device.
    - You want to import serial numbers.
    - You want to automatically install Company Portal app during enrollment, or you don't want to automatically install Company Portal app. It's recommended to install the Company Portal app during enrollment.??

  **ENROLL WITHOUT USER AFFINITY**

  If you choose without user affinity, then you're automatically using **Direct enrollment**. Remember:

  - Users can't use apps that require a user, including the Company Portal app. The Company Portal app isn't used, needed, or supported on enrollments without user affinity.
  - You use the settings from an existing macOS enrollment profile.

  For more information, see [Direct enrollment](../enrollment/device-enrollment-direct-enroll-macos.md).

- When the enrollment profile is ready, USB connect the devices to the Mac, and open the **Apple Configurator** app. When the app opens, it detects the USB connected device, and deploys the Intune enrollment profile you created.

> [!NOTE]
> For all organization-owned macOS devices, Setup Assistant is always and automatically used, even if you don't see "Setup Assistant" text in Endpoint Manager.

#### Apple Configurator end user tasks

These tasks depend on how administrators tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

- If you select **Enroll with user affinity** and **Company Portal** app authentication, then users need to open the Company Portal app, and sign in with their organization account (`user@contoso.com`). When they sign-in, the enrollment starts. When enrollment completes, users can install and use apps used by your organization, including LOB apps.

- If you select Enroll with user affinity and Setup Assistant authentication, then users need to open the Company Portal app, and sign in with the organization account (user@contoso.com).

  If you chose to not install the Company Portal app when creating the enrollment profile, then admin can use one of the options to install CP app in article. Must use LOB app, as a required app.

  Users open the Company Portal app, and sign in with the organization account (user@contoso.com). ??

- **Without user affinity (Direct enrollment)**: No actions. Be sure they don't install the Company Portal app.

For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Enroll Windows devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling Windows devices:

- [Windows 10 Automatic enrollment](#windows-10-automatic-enrollment)
- [User enrollment](#user-enrollment)
- [Windows Autopilot](#windows-autopilot)
- [Group policy](#group-policy)
- [Co-management](#co-management-enrollment)
- [Windows IoT Core devices](#windows-iot-core-devices)

This section provides recommendations on the Windows enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll Windows devices](../enrollment/windows-enrollment-methods.md).

### Windows 10 Automatic enrollment

Use for personal/BYOD and organization-owned devices running Windows 10 and newer. This option requires Azure AD Premium. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile with your environment settings. When users sign in with their organization account, they're automatically enrolled.

You can also use this enrollment method to automatically bulk enroll devices with the Windows Configuration Designer app.

---
| Feature | Use this enrollment option |
| --- | --- |
| You have Azure AD Premium | ✔️ <br/><br/> This enrollment method requires Azure AD Premium. If you don't have Azure AD Premium, or aren't planning to get it, then use User enrollment. |
| You'll use Conditional Access (CA) on devices enrolled using [bulk enrollment](../enrollment/windows-bulk-enroll.md). | ✔️ On Windows 10 1803 and newer, CA is available for Windows devices enrolled using bulk enrollment. <br/><br/> ❌ On Windows 10 1709 and older, CA isn't available for Windows devices enrolled using bulk enrollment. |
| Devices are personal or BYOD. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> Bulk enrollment is available for organization-owned devices, not personal/BYOD.|
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated. or shared device. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization administrator can sign-in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also created a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Automatic enrollment. If the administrator will enroll and prepare devices before giving them to users, then you can use a DEM account. |

---

#### Automatic enrollment administrator tasks

- Be sure your devices are running Windows 10 and newer. For a complete list, see [supported device platforms](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and choose which users can automatically enroll. In the account settings on the device, users sign in with their organization account, and then are automatically enrolled.
- For bulk enrollment, go to the Microsoft Store, and download the Windows Configuration Designer (WCD) app. Configure the Windows Configuration Designer app, and choose to enroll devices in Azure AD. A package file is created. Put the package file on a USB drive, or on a network share.

  In the account settings on the device, users sign in with their organization account, and select this package file. Then, users are automatically enrolled.

  If your end users are familiar with running a file from these locations, they can complete the enrollment. For more information, see [automatic bulk enrollment](../enrollment/windows-bulk-enroll.md).

#### Automatic enrollment end user tasks

- Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**. Users sign in with organization email address and password. Once they sign in, the enrollment starts. The device is ready to receive the policies and profiles you create.

  For more information, see [Enroll Windows 10 devices](../user-help/enroll-windows-10-device.md).

- If using bulk enrollment, and your end users are familiar with running files from a network share or USB drive, they can complete the enrollment. If they're not comfortable with this step, then it's recommended that the administrator complete the enrollment.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### User enrollment

Use for personal/BYOD and organization-owned devices running all supported Windows versions, including Windows 10 and newer. This option doesn't require Azure AD Premium. Users open the account settings on the device, and sign in with their organization account. They're prompted for specific information that you must give them, including the Intune server name or CNAME record (`EnterpriseEnrollment.contoso.com`).

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are personal or BYOD. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared device. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization administrator can sign-in, and enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also created a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| You have Azure AD Premium. | ❌ <br/><br/> Not recommended. If you have Azure AD Premium, use Windows 10 Automatic enrollment. It's a better end user experience. |
| You require features only available in Azure AD Premium, such as Conditional Access. | ❌ <br/><br/> If you have Azure AD Premium, use Windows 10 Automatic enrollment. It's a better end user experience. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to User enrollment. If the administrator will enroll and prepare devices before giving them to users, then you can use a DEM account. |

---

#### User enrollment administrator tasks

Other than having Intune setup, there are minimal administrator tasks with this enrollment method. This is why it's called "user enrollment".

- Be sure your devices are [supported](supported-devices-browsers.md).
- Optional. Instead of users entering the Intune server name, you can create a CNAME record that's easier to enter, such as `EnterpriseEnrollment.contoso.com`. CNAME records associate a domain name with a specific server. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), test your CNAME record to make sure its configured correctly. For more information, see [create a CNAME record](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium).

#### User enrollment end user tasks

- Users open the **Settings** app > **Accounts** > **Access work or school** > **Connect**. They sign in with organization email address and password. They're asked for more information, including the Intune server name or CNAME record. Be sure to give them all the information they need to enter.

  Once they enter this information, the device is enrolled, and ready to receive the policies and profiles you create.

  For more information on the end user experience, see [enroll Windows 10 devices](../user-help/enroll-windows-10-device.md) or [enroll your Windows 8.1 devices](../user-help/enroll-your-w81-or-rt81-windows.md).

- On non-Windows 10 devices, users must install the Company Portal app from the Microsoft Store. Once installed, they open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). They'll be asked for more information, including the Intune server name. Be sure to give them all the information they need to enter.

  Once they enter this information, the device is enrolled, and ready to receive the policies and profiles you create.

  ??What is the Company Portal website referenced at https://docs.microsoft.com/mem/intune/enrollment/windows-enroll#tell-users-how-to-enroll-windows-devices??

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Windows Autopilot

Use on organization-owned devices running Windows 10 and newer. Windows Autopilot uses the Windows 10 OEM version preinstalled on the device. You don't have to wipe the devices or use custom OS images. It also requires Automatic Enrollment, and uses the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to create an enrollment profile. When users sign in with their organization account, they're automatically enrolled.

For more information on Windows Autopilot, see [Windows Autopilot overview](/mem/autopilot/windows-autopilot) or [Tutorial: Use Autopilot to enroll Windows devices](../enrollment/tutorial-use-autopilot-enroll-devices.md).

---
| Feature | Use this enrollment option |
| --- | --- |
| You purchase devices from an [OEM that supports the Windows Autopilot deployment service](https://aka.ms/windowsautopilot), or from resellers or distributors that are in the [Cloud Solution Partners (CSP)](https://partner.microsoft.com/membership/cloud-solution-provider) program. | ✔️ |
| Devices are hybrid Azure AD joined. | ✔️ <br/><br/> Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune. |
| You have remote workers, and want to send devices directly to these users. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ <br/><br/> You can update existing desktops running older Windows versions, such as Windows 7, to Windows 10. This option also uses Microsoft Endpoint Configuration Manager. |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| You have Azure AD Premium. | ✔️ <br/><br/> Windows Autopilot uses Automatic enrollment. Automatic enrollment requires Azure AD Premium. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization administrator can sign-in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also created a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are personal or BYOD. | ❌ <br/><br/> Windows Autopilot is only for organization-owned devices. For BYOD or personal devices, use Automatic enrollment or User enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Windows Autopilot. If the administrator will enroll and prepare devices before giving them to users, then you can use a DEM account. |

---

#### Windows Autopilot administrator tasks

- Be sure your devices are running Windows 10 and newer. For a complete list, see [supported device platforms](/mem/autopilot/windows-autopilot-requirements).
- For 100% cloud devices, you'll:
  - Work with the OEM, reseller, or distributor to register the devices with the [Windows Autopilot deployment service](https://aka.ms/windowsautopilot).
  - In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the devices, and create an enrollment profile that joins the devices to Azure AD. The enrollment profile also configures the out-of-box deployment user experience, including [user driven](/mem/autopilot/user-driven), [white glove](/mem/autopilot/white-glove), and more. For more specific information, see [Enroll Windows devices in Intune by using Windows Autopilot](/mem/autopilot/enrollment-autopilot).
  - In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a profile that configures startup behaviors, such as disabling the local administrator, and skipping the EULA. For more specific information, see [Configure Autopilot profiles](/mem/autopilot/profiles).

- For hybrid Azure AD joined devices, you'll register the devices, and create profiles in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). You'll also install the Intune Connector for Active Directory. This connector communicates between on-premises Active Directory and Azure AD.

  For more specific information, see [Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](/mem/autopilot/windows-autopilot-hybrid).

#### Windows Autopilot end user tasks

The end user experience depends on the Windows Autopilot deployment option you chose, such as [user driven](/mem/autopilot/user-driven) or [white glove](/mem/autopilot/white-glove).

- **Self-Deploying mode**: No actions. This option doesn't associate a user with the device. Users just turn on the device, and the enrollment automatically starts.

  For more specific information, see [self deployment](/mem/autopilot/self-deploying).

- **White glove**: Users turn on the device, and sign in with their organization or school account. The enrollment automatically starts.

  For more specific information, see [white glove deployment](/mem/autopilot/white-glove).

- **Existing devices**: Your users must do the following:

  1. Open the Software Center app, and select **Operating systems**.
  2. Select **Autopilot for existing devices** > **Install**. Content downloads, the drives are formatted, and Windows 10 installs.

      This can take some time, so users must wait.

  3. Autopilot runs, and users sign in with their organization or school account. The enrollment can automatically start. For more specific information, see [existing devices deployment](/mem/autopilot/existing-devices).

- **User driven**: Users turn on the device, and sign in with their organization or school account. The enrollment automatically starts. For more specific information, see [user-driven deployment](/mem/autopilot/user-driven).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Group policy

This enrollment option is available for domain-joined devices that you want to manage using Intune. Before enrolling, the devices must be hybrid Azure AD joined. Meaning, the devices are registered in on-premises Active Directory (AD), and registered in Azure AD. Once they're registered in Azure AD, they're available to enroll in Intune, and receive the settings and device features you configure.

You create a group policy on your local AD. When a group policy refresh occurs on the device, users are notified to complete the configuration. The configuration uses the user's Azure AD account to automatically enroll the device in Intune.

For more specific information, see [Enroll a Windows 10 device automatically using Group Policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are hybrid Azure AD joined. | ✔️ <br/><br/> Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune. |
| You have Azure AD Premium. | ✔️ <br/><br/> Group policy enrollment requires Azure AD Premium. |
| You have remote workers. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization administrator can sign-in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also created a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are personal or BYOD. | ❌ <br/><br/> For BYOD or personal devices, use Automatic enrollment or User enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. They shouldn't be enrolled using the Intune classic agents. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Group policy. |

---

#### Group policy administrator tasks

For more specific information on this enrollment method, see [Enroll a Windows 10 device automatically using Group Policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy#configure-the-auto-enrollment-group-policy-for-a-single-pc).

- Be sure your Windows 10 devices are [supported in Intune](supported-devices-browsers.md), and [supported for group policy enrollment](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).
- Register your AD into Azure AD. For more specific information, see [Azure AD integration with MDM](/windows/client-management/mdm/azure-active-directory-integration-with-mdm).
- Be sure your devices are hybrid Azure AD joined devices. The devices must be registered in local AD and in Azure AD.
- In local on-premises AD, create a **Enable automatic MDM enrollment using default Azure AD credentials** group policy. When group policy is refreshed, this policy is pushed to the devices, and users complete the configuration using their domain account (`user@contoso.com`).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

#### Group policy end user tasks

- Users are notified that there are configuration changes. The policy refresh may require users to sign in with their organization or school account (`user@contoso.com`). The enrollment automatically starts.

### Co-management enrollment

If you use Configuration Manager, and want to continue to use Configuration Manager, then co-management enrollment is for you. Co-management manages Windows 10 devices using Configuration Manager and Microsoft Intune together. You cloud-attach your existing Configuration Manager environment to Endpoint Manager. This enrollment option runs some workloads in Configuration Manager, and other workloads in Endpoint Manager.

For more specific information on co-management, see [What is co-management?](../../configmgr/comanage/overview.md).

---
| Feature | Use this enrollment option |
| --- | --- |
| You use Configuration Manager. | ✔️ |
| Devices are hybrid Azure AD joined. | ✔️ <br/><br/> Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune. |
| Devices are enrolled in Intune. | ✔️ <br/><br/> You have devices you want to bring to co-management. Devices may have been enrolled using Windows Autopilot, or are direct from your hardware OEM. |
| You have Azure AD Premium. | ✔️ <br/><br/>  Azure AD Premium may be required depending on your co-management configuration. For more specific information, see [Paths to co-management](../../configmgr/comanage/quickstart-paths.md). |
| You have remote workers. | ✔️ |
| Devices are owned by the organization or school. | ✔️ |
| Devices are personal or BYOD. | ✔️ |
| You have new or existing devices. | ✔️ <br/><br/> For devices that aren't running Windows 10 and newer, such as Windows 7, you'll need to upgrade. For more specific information, see [Upgrade Windows 10 for co-management](../../configmgr/comanage/quickstart-upgrade-win10.md). |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk, dedicated, or shared. | ✔️ <br/><br/> These devices are organization-owned. This enrollment method requires users to sign in with their organization account. An organization administrator can sign-in, and automatically enroll. When the device is enrolled, create a [kiosk](../configuration/kiosk-settings.md) profile, and assign this profile to this device. You can also created a profile for [devices shared with many users](../configuration/shared-user-device-settings.md). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be co-managed, users need to unenroll from the current MDM provider. They shouldn't be enrolled using the Intune classic agents. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to co-management. |

---

#### Co-management administrator tasks

The administrator tasks and requirements depend on the co-management option you choose. For more specific information, see [Paths to co-management](../../configmgr/comanage/quickstart-paths.md).

When setting up co-management, you choose to:

- Automatically enroll existing Configuration Manager-managed devices to Intune. This option requires hybrid Azure AD joined devices. For more specific information, see [Tutorial: Enable co-management for existing Configuration Manager clients](../../configmgr/comanage/tutorial-co-manage-clients.md).

- Bring existing Intune enrolled Windows 10 devices to also be managed by Configuration Manager. In this situation, these devices aren't hybrid Azure AD joined devices. Meaning, the devices are registered in Azure AD. They're not registered in on-premises local Active Directory.

  For more specific information, see [Tutorial: Enable co-management for new internet-based devices](../../configmgr/comanage/tutorial-co-manage-new-devices.md).

#### Co-management end user tasks

Both options use Automatic enrollment. With Automatic enrollment, users sign in with their organization account (`user@contoso.com`), and then are automatically enrolled. They can also open the **Settings** app > **Accounts** > **Access work or school** > **Connect**, and sign in with organization email address and password.

Configuration Manager may randomizes the enrollment, so it may not occur immediately. When enrollment completes, it's ready to receive the policies and profiles you create.

### Windows IoT Core devices

For more specific information, see [Managing Windows IoT Core Devices](/windows/iot-core/manage-your-device/devicemanagement)

## Common issues and resolutions

In this section, add extra information provided by CSS and PFE teams.

[Troubleshoot device enrollment](../enrollment/troubleshoot-device-enrollment-in-intune.md)

Add reporting Devices > enrollment status
Reports > workbooks > intune enrollment activity

- watch for trends

## Next steps

[Intune setup deployment guide](deployment-guide-intune-setup.md)  
