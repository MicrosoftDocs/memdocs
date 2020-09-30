---
# required metadata

title: macOS device enrollment guide for  Microsoft Intune - Azure | Microsoft Docs
description: Enroll macOS devices using device enrollment, automated device enrollment (DEP), and Apple Configurator enrollment options in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/08/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: auherrin, dregan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Deployment guide: Enroll macOS devices in Microsoft Intune

> [!WARNING]
> THIS GUIDE IS STILL BEING WRITTEN, AND MAY CONTAIN INCORRECT INFORMATION.

Personal and organization-owned devices can be enrolled in Intune. On macOS devices, the Company Portal app or the Apple Setup Assistant authenticates users, and starts the enrollment. Once they're enrolled, they receive the policies and profiles you create.

You have the following options when enrolling macOS devices:

- [Device enrollment](#device-enrollment)
- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised)
- [Apple Configurator](#apple-configurator-enrollment)

This article:

- Describes your Company Portal app options for each enrollment method.
- Provides recommendations on the macOS enrollment method to use.
- Includes an overview of the administrator and user tasks for each enrollment type.

For more specific information, see [Enroll macOS devices](../enrollment/macos-enroll.md).

## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## Device enrollment

Use for personal or bring your own devices (BYOD). Not a traditional "enrollment" method, as it uses an app configuration profile. This option manages apps on the device. Devices aren't enrolled.

https://msit.microsoftstream.com/video/eddfa3ff-0400-a521-3ef3-f1eac74a25be?referrer=https:%2F%2Fstatics.teams.cdn.office.net%2Fevergreen-assets%2Fsafelinks%2F1%2Fatp-safelinks.html


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

### Device enrollment administrator tasks

This task list provides an overview.

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- There isn't a Company Portal app for macOS devices in the Apple App Store, or through VPP. Users must [manually download and run the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070). They sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the enrollment profile.

  When they approve, the device is added to your organization Azure AD. Then, it's available to Intune to receive your policies and profiles. Be sure to communicate this information with your users.

  For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

### Device enrollment end user tasks

Your users must do the following steps. For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

1. Download and run [the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070).
2. Open the Company Portal app, and sign in with their organization account (`user@contoso.com`). Once they sign in, they must approve the enrollment profile (System preferences). When users approve, the device is enrolled, and considered managed. If they don't approve, then they're not enrolled, and won't receive your policy and profiles.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Automated Device Enrollment (ADE) (supervised)

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

### ADE administrator tasks

This task list provides an overview. For more specific information, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
- Be sure the Apple token (.p7m) is active. For more specific information, see [Get an Apple ADE token](../enrollment/device-enrollment-program-enroll-macos.md#get-an-apple-ade-token).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile. Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).

  CONTINUE HERE

  - **Enroll with user affinity**: This option uses Setup Assistant to authenticate the user, and enroll the device. When you create the profile, also choose if users can delete the management profile, called **Locked enrollment**.

    Once enrolled, it's ready to receive your policies and profiles.

    You can continue to use Setup Assistant for authentication. Or, after the device is enrolled, you can also install the Company Portal app, and use it for authentication, instead of Setup Assistant. To install the Company Portal app on devices, [add the Company Portal app](../apps/apps-company-portal-macos.md). Set the Company Portal app as a required app.

    Once installed, users open the Company Portal app, and sign in with their organization account (`user@contoso.com`). When they sign-in, they are authenticated, and ready to receive your policies and profiles.

    When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. The Setup Assistant authenticates the user, and enrolls the device. You can continue to use Setup Assistant for authentication. The device is enrolled, and ready to receive your policies and profiles. Setup Assistant uses the Apple token (.p7m) to know the user is a work account.  ??Are the accounts I listed for Setup Assistant correct? Does Setup Assistant add the user, the device, or both to Azure AD??

  - **Enroll without user affinity**: Setup Assistant authenticates the user, and enrolls the user in Intune. Also choose if users can delete the management profile, called **Locked enrollment**. The Company Portal app isn't used, needed, or supported on enrollments without user affinity.

  > [!NOTE]
  > For all organization-owned macOS devices, Setup Assistant is always and automatically used, even if you don't see "Setup Assistant" text in Endpoint Manager.

### ADE end user tasks

These tasks depend on how administrators tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

- **Enroll with user affinity**:??

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. The Setup Assistant authenticates the user, and enrolls the device.

  2. If you're using the Company Portal app for authentication (instead of Setup Assistant), then the Company Portal app installs using [the option](../apps/apps-company-portal-macos.md) you configured.

      Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, users are authenticated, and can access organization resources.

- **Enroll without user affinity**: No actions. Be sure your users don't install the Company Portal app.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Apple Configurator enrollment

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

### Apple Configurator administrator tasks

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

### Apple Configurator end user tasks

These tasks depend on how administrators tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

- If you select **Enroll with user affinity** and **Company Portal** app authentication, then users need to open the Company Portal app, and sign in with their organization account (`user@contoso.com`). When they sign-in, the enrollment starts. When enrollment completes, users can install and use apps used by your organization, including LOB apps.

- If you select Enroll with user affinity and Setup Assistant authentication, then users need to open the Company Portal app, and sign in with the organization account (user@contoso.com).

  If you chose to not install the Company Portal app when creating the enrollment profile, then admin can use one of the options to install CP app in article. Must use LOB app, as a required app.

  Users open the Company Portal app, and sign in with the organization account (user@contoso.com). ??

- **Without user affinity (Direct enrollment)**: No actions. Be sure they don't install the Company Portal app.

For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Next steps

- [MAM-WE](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)
