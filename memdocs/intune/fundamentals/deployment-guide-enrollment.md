---
# required metadata

title: Device enrollment guide for Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/19/2020
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

Azure AD is the backbone of Intune and Endpoint Manager. Once users and devices are registered within Azure AD, then it's available. There are a few ways to get these devices registered in Azure AD. This is called "enrollment".

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

When assigning your profiles, start small, and use a staged approach. Assign the profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the profile to more pilot groups.

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

## Enroll Android devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling Android and Android Enterprise devices:

- [Android Enterprise work profile (profile owner)](#android-enterprise-work-profile)
- [Android Enterprise dedicated devices (COSU)](#android-enterprise-dedicated-devices)
- [Android Enterprise fully managed (COBO)](#android-enterprise-fully-managed)
- [Android device administrator](#android-device-administrator)

This section provides recommendations on the Android and Android Enterprise enrollment methods to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll Android devices](../enrollment/android-enroll.md).

### Android Enterprise work profile

These devices are personal or BYOD (bring your own device) Android devices that can access work or school email, apps, and other data.

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
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/> User-less devices should be enrolled using Android Enterprise dedicated devices. |

---

#### Administrator tasks: Android Enterprise work profile

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an [enrollment restriction](../enrollment/enrollment-restrictions-set.md), and **allow** devices that support Android Enterprise work profiles. For the specific steps, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).

#### End user tasks: Android Enterprise work profile

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
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using Android Enterprise work profile.|
| Devices are associated with a single user. | ❌ <br/><br/> Not recommended. These devices should be enrolled using Android Enterprise fully managed. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |

---

#### Administrator tasks: Android Enterprise dedicated devices

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your dedicated device group(s) ready. For the specific steps, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise dedicated devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

#### End user tasks: Android Enterprise dedicated devices

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
| Devices are personal or BYOD. | ❌ <br/><br/>BYOD or personal devices should be enrolled using Android Enterprise work profile.|
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/>User-less devices should be enrolled using Android Enterprise dedicated devices. |
|Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

#### Administrator tasks: Android Enterprise fully managed

- Be sure your devices are [supported](supported-devices-browsers.md).
- Factory reset the devices. This step is required.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable fully managed user devices. For the specific steps, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).
- Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise fully managed devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

  On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

#### End user task: Android Enterprise fully managed

It's not recommended for users to enroll Android Enterprise fully managed devices. This task should be completed by administrators.

### Android device administrator

> [!NOTE]
> Google is decreasing device administrator support in new Android releases. To avoid reduced functionality, Microsoft recommends:
>
> - Enroll new devices using [Android Enterprise work profiles](#android-enterprise-work-profile) (in this article). Do **not** enroll new devices using Android device administrator.
> - If devices will update to Android 10, then migrate devices off device administrator management.
> - Move existing Android device administrator devices to Android Enterprise work profiles. For more information, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md).

These Android devices are personal or BYOD (bring your own device) devices that can access work or school email, apps, and other data.

#### Administrator tasks: Android device administrator

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable device administrator enrollment. For the specific steps, see [Android device administrator enrollment](../enrollment/android-enroll-device-administrator.md).

#### End user tasks: Android device administrator

Your users must do the following. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Enroll iOS/iPadOS devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling iOS/iPadOS devices:

- [Application management without enrollment (MAMWE)](#application-management-without-enrollment-mamwe)
- [User and Device enrollment](#user-and-device-enrollment)
- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised)
- [Apple Configurator](#apple-configurator-enrollment)

This section provides recommendations on the iOS/iPadOS enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll macOS devices](../enrollment/ios-enroll.md).

### Application management without enrollment (MAMWE)

Commonly used for personal or bring your own devices (BYOD). Not a traditional "enrollment" method, as it uses an app configuration profile. This option manages apps on the device. Devices aren't enrolled. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you create app configuration policies and app protection policies, and push these policies to the devices.

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
| Devices are owned by the organization or school. |  ❌ <br/><br/> Not recommended as the *only* enrollment method for organization-owned devices. Organization-owned devices should be enrolled using Automated Device Enrollment or Apple Configurator. If you want extra security for specific apps, then use enrollment and MAM-WE together. |
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/>User-less devices should be enrolled using Automated Device Enrollment or Apple Configurator. |

---

For more information on MAM-WE, see [Microsoft Intune app management](../apps/app-management.md).

#### Administrator tasks: MAM-WE

- Be sure your iOS/iPadOS devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), [add your apps](../apps/apps-supported-intune-apps.md), optionally create [app configuration policies](../apps/app-configuration-policies-use-ios.md), and create [app protection policies](../apps/app-protection-policy-settings-ios.md). Deploy these policies to the devices.

#### End user tasks: MAM-WE

??Is Company Portal app required???
??How do they get work apps, Outlook???

- Users may have to download the app from the Apple App Store

### User and Device enrollment

These iOS/iPadOS devices are personal or BYOD (bring your own device) devices that can access work or school email, apps, and other data. Starting with iOS 13 and newer, this enrollment option targets users or targets devices. It doesn't require resetting the devices.

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
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/>User-less devices should be enrolled using Automated Device Enrollment or Apple Configurator. |

---

When you create the enrollment profile, you're asked to to choose **User enrollment**, **Device enrollment** or **Determine based on user choice**.

For the specific enrollment steps, and its prerequisites, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).??Need to update the title of this article, is it applies to user enrollment and Device enrollment??

#### Administrator tasks: User and Device enrollment

- Be sure you have an [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md). This certificate is required to enroll iOS/iPadOS devices.
- Be sure your iOS/iPadOS devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you create the enrollment profile. When you create the profile, you have the following options:

  - **Apple user enrollment**: Starting with iOS 13 and newer. This option configures a specific set of features and organization apps, such as password, per-app VPN, Wi-Fi, and Siri. If you use this enrollment method, to help secure apps and their data, it's strongly recommended to also use app protection policies. User enrollment is considered friendlier to end users, but may not provide the feature set and security Administrators need.

    For the complete list of what you can and can't do, see [Intune actions and options supported with Apple User Enrollment](../enrollment/ios-user-enrollment-supported-actions.md). For the specific user enrollment steps, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

    In some scenarios, user enrollment may not be the best option. Consider the following:

    - User enrollment creates a work partition on the devices. The features and security you configure in the user enrollment profile only exist in the work partition. They don't exist in the user partition. Users can't factory reset the work partition. Administrators can. Users can factory reset the personal partition. Administrators can't.

    - If users primarily use Microsoft apps, or use apps created with the [Intune App SDK](../developer/app-sdk.md), then users should download these apps from the Apple App Store. Then, use app protection policies to protect these apps. In this scenario, you don't need user enrollment.

    - For line of business (LOB) apps, user enrollment might be an option, as it'll deploy these apps to the work partition. That is a key feature that app protect policies don't have.??

    - When devices are enrolled using user enrollment, you can't switch to device enrollment. With user enrollment, you can't move an app from unmanaged to managed. Users must unenroll from user enrollment, and then re-enroll to device enrollment.

    - Apps installed before the user enrollment profile applies aren't protected or managed by the user enrollment profile.

      For example, a user downloads the Outlook app from the Apple App Store. The app automatically installs to the user partition on the device. The user configures Outlook for their personal email. When configuring their organization email, they're blocked by conditional access, and asked to enroll. They enroll, and a user enrollment profile deploys.

      Since the Outlook app was installed before the user enrollment profile, the user enrollment profile fails. The Outlook app can't be managed because it's installed and configured in the user partition, not the work partition. Users must manually uninstall the Outlook app.

      Once uninstalled, users can sync the device manually, and possibly re-apply the user enrollment profile. Or, you may have to create an app configuration policy to deploy Outlook, make it a required app, and then deploy an app protection policy to secure the app and its data.

  - **Apple device enrollment**: This option is a typical enrollment for personal devices. The device is managed, not just specifics apps or features. With this option, consider the following:

    - You can deploy certificates that apply to the whole device.
    - Users must install updates. Only devices enrolled using Automated Device Enrollment can receive updates using MDM policies or profiles.
    - A user must be associated with the device. This user can be a device enrollment manager (DEM) account.

  - **Determine based on user choice**: Gives end users a choice when they enroll. Depending on their selection, **User enrollment** or **Device enrollment** is used.

- Assign the enrollment profile to user groups. Don't assign to device groups.

#### End user tasks: User and Device enrollment

Your users must do the following. For the specific user experience, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md).

1. Go to the Apple App Store, and [install the Intune Company Portal app](../user-help/install-and-sign-in-to-the-intune-company-portal-app-ios.md).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md). 

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use Apple Business Manager (ABM) or Apple School Manager (ASM) to enroll a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your preconfigured settings, and can be shipped directly to users or schools.

Use on devices owned by your organization. This option configures settings using Apple Business Manager (ABM) or Apple School Manager (ASM). You create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and push this profile to the devices.

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

For more specific information on this enrollment type, see:

- [Apple Business Manager enrollment](../enrollment/device-enrollment-program-enroll-ios.md)
- [Apple School Manager enrollment](../enrollment/apple-school-manager-set-up-ios.md)

  For more information on Apple School Manager, see [Apple education](https://www.apple.com/education/k12/it/) (opens Apple's web site).

#### Administrator tasks: ADE

- Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
- Have the Apple token (.p7m) ready.
- Have the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) ready. This certificate is required to enroll iOS/iPadOS and macOS devices.
- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile. When users connect their devices to the internet, and sign in to the Company Portal app with their organization credentials (`user@contoso.com`), they receive the profile and your settings.

  When you create an enrollment profile, you:

  - Choose to assign a user with the device (**with user affinity**), or have shared devices (**without user affinity**).
  - Choose how users authenticate: the Setup Assistant, or the Company Portal app

    If you want to use MFA, prompt users to update their expired password when they first sign in, or prompt users to reset their expired passwords during enrollment, then select the Company Portal app.

  Devices enrolled using ADE aren't compatible with the Company Portal app version in the Apple App Store. Do not install this app store version. Instead, install the Company Portal app using the following options:

  **Option 1**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), in your ADE enrollment profile, deploy the Company Portal app using the **Install Company Portal with VPP** (Volume Purchase Program) option. This option:

  - Already includes the correct Company Portal app version.
  - You don't have to create another policy to deploy the Company Portal app to devices.
  - The Company Portal app must be updated manually by you, or your users.

  **Option 2**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an app configuration policy that deploys the Company Portal app to enrolled devices using the VPP. This option:

  - Already includes the correct Company Portal app version.
  - Requires you to create an enrollment profile and an app configuration policy.
  - In your app configuration policy, make it a required app so you know it's deployed to all your devices.
  - The Company Portal app can be automatically updated by changing your existing app configuration policy.

  For more information on this enrollment option, see [Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

#### End user tasks: ADE

When you create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you choose to associate a user to the device (with user affinity), or have shared devices (without user affinity).

- **With user affinity**:

  1. When the device is turned on, the Apple Setup Assistant runs.
  2. When setup completes, they enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. Once entered, the Company Portal app is automatically installed from your profile. It can take some time for the Company Portal app to auto-install.
  3. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, the device is checked for compliance, and may be Azure AD registered.

  Users may have to enter more information. For more specific steps, see [Enroll your organization-provided iOS device](../user-help/enroll-your-device-dep-ios.md).

- **Without user affinity**: No actions. Be sure they don't install the Company Portal app from the Apple App Store.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Apple Configurator enrollment

Use on devices owned by your organization, and includes [Direct Enrollment](../enrollment/device-enrollment-direct-enroll-macos.md). This option requires you to physically connect macOS devices to a Mac computer using the USB port.

---
| Feature | Use this enrollment option |
| --- | --- |
| You need a wired connection, or are having a network issue. | ✔️ |
| Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements.  | ✔️ <br/><br/> The idea of *not* using the ABM or ASM portals is to give administrators less control.|
| A country doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM). | ✔️ <br/><br/> If your country supports ABS or ASM, then devices should be enrolled using Automatic Device Enrollment. |
| Devices are owned by the organization or school. | ✔️ |
| You have new and existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> If you have a large number of devices, then this method will take some time. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using MAM-WE, or User and Device enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. Or, you can use MAM-WE to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

For more specific information on this enrollment type, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

#### Administrator tasks: Apple Configurator

- Requires access to a Mac computer with a USB port.
- Have the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) ready. This certificate is required to enroll iOS/iPadOS devices.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you create an enrollment profile. When you create an enrollment profile, you choose to associate a user to the device (with user affinity), or have shared devices (without user affinity).

  If you choose with user affinity, then also choose if users will authenticate using **Setup Assistant** or the **Company Portal app**. Remember:

  - **Company Portal app**: Select this option to use MFA, prompt users to update their expired password when they first sign in, or prompt users to reset their expired passwords during enrollment.

  - **Setup Assistant**: Select this option to wipe the device, and import serial numbers.

  If you choose without user affinity, then you're automatically using **Direct enrollment**. Remember:

  - Users can't use apps that require a user, including the Company Portal app. Be sure they don't install the Company Portal app from the Apple App Store.
  - You use the settings from an existing macOS enrollment profile, without serial numbers.

- When the profile is ready, USB connect the devices to the Mac, and open the **Apple Configurator** app. When the app opens, it detects the USB connected device, and deploys the Intune enrollment profile you created.

For more information on this enrollment option, and its prerequisites, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

#### End user tasks: Apple Configurator

- **Setup Assistant enrollment**: Go to the Apple App Store, and [install the Intune Company Portal app](../user-help/install-and-sign-in-to-the-intune-company-portal-app-ios.md). Once installed, they'll can install apps, including LOB apps, used by your organization.
  - Admins should push comp port app from VPP
- **Without user affinity (Direct enrollment)**: No actions. Be sure they don't install the Company Portal app from the Apple App Store.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Enroll macOS devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling macOS devices:

- [Device enrollment](#device-enrollment)
- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised-1)
- [Apple Configurator](#apple-configurator-enrollment-1)

This section provides recommendations on the macOS enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll macOS devices](../enrollment/macos-enroll.md).

### Device enrollment

Use for personal or bring your own devices (BYOD). Not a traditional "enrollment" method, as it uses an app configuration profile. This option manages apps on the device. Devices aren't enrolled. ??This option uses the Company Portal app version in VPP.?? Create an application configuration profile to configure the Company Portal app, and then push the app and its configuration to macOS devices.

---
| Feature | Use this enrollment option |
| --- | --- |
| Devices are personal or BYOD. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ |
| You have new and existing devices. | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are managed by another MDM provider. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ ?? If Co Portal app is from VPP, can't use DEM account. Need to confirm if VPP version is used. https://docs.microsoft.com/en-us/mem/intune/apps/apps-company-portal-macos, doesn't mention VPP. ??|
| Devices are owned by the organization or school. | ❌ <br/><br/> Not recommended for organization-owned devices. Organization-owned devices should be enrolled using Automated Device Enrollment or Apple Configurator. |
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/> User-less devices should be enrolled using Automated Device Enrollment or Apple Configurator. |

---

#### Administrator tasks: Device enrollment

- Have the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) ready. This certificate is required to enroll macOS devices.
- Be sure your devices are [supported](supported-devices-browsers.md).
- There isn't a Company Portal app for macOS devices in the Apple App Store. Your options:

  - **Option 1**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), [add the Company Portal app using one of the options](../apps/apps-company-portal-macos.md). Create an app configuration policy, set the Company Portal app as a required app, and then deploy this policy to the macOS devices.

    Users open the Company Portal app, sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the profile. When they approve, the device is added to Azure AD, and is available to Intune to receive your policies and profiles.

    This option is more work for administrators, and less work for end users.

    For more specific information, see [Add the macOS Company Portal app to Intune](../apps/apps-company-portal-macos.md).

  - **Option 2**: Users manually download and run the Company Portal app installer package. They sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the profile.

    When they approve, the device is added to Azure AD in your organization (also called a tenant). Then, it's available to Intune to receive your policies and profiles.

    This option is more work for users, and less work for administrators. If your users aren't comfortable with downloading and running files, then consider deploying the Company Portal app using an app configuration policy (Option 1).

    For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### End user tasks: Device enrollment

These tasks depend on how you, the administrator, tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

- Users open the Company Portal app, sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the profile. When users approve, the device is enrolled and considered managed. If they don't approve, then they're not enrolled, and won't receive your policy and profile updates.

  For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use Apple Business Manager (ABM) or Apple School Manager (ASM) to enroll a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your preconfigured settings, and can be shipped directly to users or schools.

Use on devices owned by your organization. This option configures settings using Apple Business Manager (ABM) or Apple School Manager (ASM). You create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and push this profile to the devices.

On macOS devices, ADE is the same as iOS/iPadOS devices. Rather than duplicate the content here, see the [iOS/iPad section](#automated-device-enrollment-ade-supervised) in this article.

For more specific information on this enrollment type, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

### Apple Configurator enrollment

Enrolls macOS devices by physically connecting these devices to the USB port on a Mac computer.

Use on devices owned by your organization, and includes [Direct Enrollment](../enrollment/device-enrollment-direct-enroll-macos.md). This option requires you to physically connect macOS devices to a Mac computer using the USB port.

---
| Feature | Use this enrollment option |
| --- | --- |
| You need a wired connection, or are having a network issue. | ✔️ |
| Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements.  | ✔️ <br/><br/> The idea of *not* using the ABM or ASM portals is to give administrators less control.|
| A country doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM). | ✔️ <br/><br/> If your country supports ABS or ASM, then devices should be enrolled using Automatic Device Enrollment. |
| Devices are owned by the organization or school. | ✔️ |
| You have new and existing devices. | ✔️ |
| Need to enroll a small number of devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> If you have a large number of devices, then this method will take some time. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using Device enrollment. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. Or, you can use Direct Enrollment to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

For more specific information on this enrollment type, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md) and [Direct Enrollment for macOS devices](../enrollment/device-enrollment-direct-enroll-macos.md).

#### Administrator tasks: Apple Configurator macOS

- Have the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) ready. This certificate is required to enroll macOS devices.
- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you create an enrollment profile. When you create an enrollment profile, you choose to have shared devices (without user affinity), or to associate a user to the device (with user affinity).

  **WITHOUT USER AFFINITY**:

  If you choose without user affinity, then you're automatically using **Direct enrollment**. Remember:

  - Users can't use apps that require a user, including the Company Portal app.
  - You use the settings from an existing macOS enrollment profile, without serial numbers.??

  For more information, see [Direct enrollment](../enrollment/device-enrollment-direct-enroll-macos.md).

  **WITH USER AFFINITY**:

  If you choose with user affinity, then also choose if users will authenticate using the **Setup Assistant** or the **Company Portal app**:

  - **Setup Assistant**: Select this option to wipe the device, and import serial numbers.??

  - **Company Portal app**: Select this option to use MFA, prompt users to update their expired password when they first sign in, or prompt users to reset their expired passwords during enrollment.

    There isn't a Company Portal app for macOS devices in the Apple App Store. Your options:

    - **Option 1**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal app [using one of the options](../apps/apps-company-portal-macos.md). Create an app configuration policy, set the Company Portal app as a required app, and then deploy this policy to the macOS devices.

      Users open the Company Portal app, sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the profile. When they approve, the device is added to Azure AD, and is available to Intune to receive your policies and profiles.

      This option is more work for administrators, and less work for end users.

      For more specific information, see [Add the macOS Company Portal app to Intune](../apps/apps-company-portal-macos.md).

    - **Option 2**: Users manually download and run the Company Portal app installer package. They sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the profile.

      When they approve, the device is added to Azure AD in your organization (also called a tenant). Then, it's available to Intune to receive your policies and profiles.

      This option is more work for users, and less work for administrators. If your users aren't comfortable with downloading and running files, then consider deploying the Company Portal app using an app configuration policy (Option 1).

      For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

- When the profile is ready, USB connect the devices to the Mac, and open the **Apple Configurator** app. When the app opens, it detects the USB connected device, and deploys the Intune enrollment profile you created.

#### End user tasks: Apple Configurator macOS

These tasks depend on how you, the administrator, tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

- **Setup Assistant enrollment**: Users open the Company Portal app, sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the profile. When users approve, the device is enrolled and considered managed. If they don't approve, then they're not enrolled, and won't receive your policy and profile updates.

  For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

  - Admins should push comp port app from VPP

- **Without user affinity (Direct enrollment)**: No actions. Be sure they don't install the Company Portal app.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]


-----------
Admin creates:
app config policy to configure co portal app, set as required app > VPP app
push down the pkg
Co portal app isn't on Apple App Store

User:
opens co portal app, goto system pref > profiles and approve profile

Arnab

Administrators get the Company Portal app from their VPP. 

-----------

## Enroll Windows devices

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling Windows devices:

- [Windows 10 Automatic enrollment](#windows-10-automatic-enrollment)
- [User enrollment](#user-enrollment)
- [Windows Autopilot](#windows-autopilot)
- **Group policy**: https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy
- **Co-management**: 

This section provides recommendations on the Windows enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. For more specific information, see [Enroll Windows devices](../enrollment/windows-enrollment-methods.md).

### Windows 10 Automatic enrollment

Use for personal/BYOD and organization-owned devices running Windows 10 and newer. This option requires Azure AD Premium. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile with your environment settings. When users sign in with their work or school account, they're automatically enrolled.

You can also use this enrollment method to automatically bulk enroll devices with the Windows Configuration Designer app.

Use this enrollment option when:

- Your devices are personal/BYOD or organization-owned devices.
- You have existing or new devices.
- You need to enroll a small number of devices, or a large number of devices (bulk enrollment). Bulk enrollment is available for organization-owned devices, not personal/BYOD.
- Your users know their domain username and password.

Don't use this option when:

- You don't have Azure AD Premium, or aren't planning to get it.
- You'll use Conditional Access on devices bulk-enrolled. Bulk-enrolled devices don't support conditional access.

#### Administrator tasks: Automatic enrollment

- Be sure your devices are running Windows 10 and newer. For a complete list, see [supported device platforms](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and choose which users can automatically enroll. In the account settings on the device, users sign in with their work or school account, and then are automatically enrolled.
- For bulk enrollment, go to the Microsoft Store, and download the Windows Configuration Designer (WCD) app. Configure the Windows Configuration Designer app, and choose to enroll devices in Azure AD. A package file is created. Put the package file on a USB drive, or on a network share.

  In the account settings on the device, users sign in with their work or school account, and select this package file. Then, users are automatically enrolled.

  If your end users are familiar with running a file from these locations, they can complete the enrollment. For more information, see [automatic bulk enrollment](../enrollment/windows-bulk-enroll.md).

#### End user tasks: Automatic enrollment

- Open the **Settings** app > **Accounts** > **Access work or school** > **Connect**. Users sign in with work or school email address and password. Once they sign in, they're enrolled. The device is registered in Azure AD, and is ready to receive the policies and profiles you create.

  For more information, see [Enroll Windows 10 devices](../user-help/enroll-windows-10-device.md).

- If using bulk enrollment, and your end users are familiar with running files from a network share or USB drive, they can complete the enrollment. If they're not comfortable with this step, then it's recommended that the administrator complete the enrollment.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### User enrollment

Use for personal/BYOD and organization-owned devices running all supported Windows versions, including Windows 10 and newer. This option doesn't require Azure AD Premium. Users open the account settings on the device, and sign in with their work or school account. They're prompted for specific information that you must give them, including the Intune server name or CNAME record (`EnterpriseEnrollment.contoso.com`).

Use this enrollment option when:

- Your devices are personal/BYOD or organization-owned devices.
- You have existing or new devices.
- You need to enroll a small number of devices, or a large number of devices.
- Your users know their domain username and password.
- You're not using Azure AD Premium, or aren't planning to get it.

Don't use this option when:

- You have Azure AD Premium. If you have Azure AD Premium, use Windows 10 Automatic enrollment. It's a better end user experience.
- You require features only available in Azure AD Premium, such as Conditional Access.

#### Administrator tasks: User enrollment

Other than having Intune setup, there are minimal administrator tasks with this enrollment method. This is why it's called "user enrollment".

- Be sure your devices are [supported](supported-devices-browsers.md).
- Optional. Instead of users entering the Intune server name, you can create a CNAME record that's easier to enter, such as `EnterpriseEnrollment.contoso.com`. CNAME records associate a domain name with a specific server. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), test your CNAME record to make sure its configured correctly. For more information, see [create a CNAME record](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium).

#### End user tasks: User enrollment

- Users open the **Settings** app > **Accounts** > **Access work or school** > **Connect**. They sign in with work or school email address and password. They're asked for more information, including the Intune server name or CNAME record. Be sure to give them all the information they need to enter.

  Once they enter this information, the device is registered in Azure AD, and is ready to receive the policies and profiles you create.

  For more information on the end user experience, see [enroll Windows 10 devices](../user-help/enroll-windows-10-device.md) or [enroll your Windows 8.1 devices](../user-help/enroll-your-w81-or-rt81-windows.md).

- On non-Windows 10 devices, users must install the Company Portal app from the Microsoft Store. Once installed, they open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). They'll be asked for more information, including the Intune server name. Be sure to give them all the information they need to enter.

  Once they enter this information, the device is registered in Azure AD, and is ready to receive the policies and profiles you create.

  ??What is the Company Portal website referenced at https://docs.microsoft.com/mem/intune/enrollment/windows-enroll#tell-users-how-to-enroll-windows-devices??

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

### Windows Autopilot

Use on organization-owned devices running Windows 10 and newer. Windows Autopilot uses the Windows 10 OEM version preinstalled on the device. You don't have to wipe the devices or use custom OS images. It also requires Automatic Enrollment, and uses the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to create an enrollment profile that joins the device to Azure AD. When users sign in with their work or school account, they're automatically enrolled.

Use this enrollment option when:

- You have new or existing devices.
- Your devices are owned by the organization or school.
- You need to enroll a small number of devices, or a large number of devices.
- Devices are hybrid Azure AD joined. Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune.
- You purchase devices from an [OEM that supports the Windows Autopilot deployment service](https://aka.ms/windowsautopilot), or from resellers or distributors that are in the [Cloud Solution Partners (CSP)](https://partner.microsoft.com/membership/cloud-solution-provider) program.
- You have remote workers, and want to send devices directly to these users.

Don't use this option when:

- Your devices are personal or BYOD. Windows Autopilot is only for organization-owned devices.
- You don't have Azure AD Premium, or aren't planning to get it. Azure AD Premium is required by Automatic enrollment. Windows Autopilot uses Automatic enrollment.

For more information on Windows Autopilot, see:  

- [Windows Autopilot overview](/mem/autopilot/windows-autopilot)
- [Tutorial: Use Autopilot to enroll Windows devices](../enrollment/tutorial-use-autopilot-enroll-devices.md)

#### Administrator tasks: Windows Autopilot

- Be sure your devices are running Windows 10 and newer. For a complete list, see [supported device platforms](/mem/autopilot/windows-autopilot-requirements).
- For 100% cloud devices, you'll:
  - Work with the OEM, reseller, or distributor to register the devices with the [Windows Autopilot deployment service](https://aka.ms/windowsautopilot).
  - In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the devices, and create an enrollment profile that joins the devices to Azure AD. The profile also configures the out-of-box deployment user experience, including [user driven](/mem/autopilot/user-driven), [white glove](/mem/autopilot/white-glove), and more. For more specific information, see [Enroll Windows devices in Intune by using Windows Autopilot](/mem/autopilot/enrollment-autopilot).
  - In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a profile that configures startup behaviors, such as disabling the local administrator, and skipping the EULA. For more specific information, see [Configure Autopilot profiles](/mem/autopilot/profiles).

- For hybrid Azure AD joined devices, you'll register the devices, and create profiles in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). You'll also install the Intune Connector for Active Directory. This connector communicates between on-premises Active Directory and Azure AD.

  For more specific information, see [Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](/mem/autopilot/windows-autopilot-hybrid).

#### End user tasks: Windows Autopilot



## Common issues and resolutions

In this section, add extra information provided by CSS and PFE teams.

[Troubleshoot device enrollment](../enrollment/troubleshoot-device-enrollment-in-intune.md)

## Next steps

[Intune setup deployment guide](deployment-guide-intune-setup.md)  
