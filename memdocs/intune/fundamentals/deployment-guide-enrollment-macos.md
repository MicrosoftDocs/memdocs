---
# required metadata

title: macOS device enrollment guide for  Microsoft Intune
description: Enroll macOS devices using device enrollment, automated device enrollment (DEP), and Apple Configurator enrollment options in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/24/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: auherrin, dregan, annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Deployment guide: Enroll macOS devices in Microsoft Intune

Personal and organization-owned devices can be enrolled in Intune. On macOS devices, the Company Portal app or the Apple Setup Assistant authenticates users, and starts the enrollment. Once they're enrolled, they receive the policies and profiles you create.

You have the following options when enrolling macOS devices:

- [BYOD: Device enrollment](#byod-device-enrollment)
- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised)
- [Direct enrollment](#direct-enrollment)

This article:

- Describes your Company Portal app options for each enrollment method.
- Provides recommendations on the macOS enrollment method to use.
- Includes an overview of the administrator and user tasks for each enrollment type.

For more specific information, see [Enroll macOS devices](../enrollment/macos-enroll.md).

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## BYOD: Device enrollment

Use for personal or bring your own devices (BYOD). 

---
| Feature | Use this enrollment option when |
| --- | --- |
| Devices are personal or BYOD. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| You have new or existing devices. | ✔️ |
| Devices are associated with a single user. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ <br/><br/> Be aware of impact and any limitations using DEM account. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> When a device enrolls, MDM providers install certificates and other files. These files must be removed. The quickest way may be to unenroll, or factory reset the devices. If you don't want to factory reset, then contact the MDM provider. |
| Devices are owned by the organization or school. | ❌ <br/><br/> Not recommended for organization-owned devices. Organization-owned devices should be enrolled using [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article) or Apple Configurator. <br/><br/> You can add the MacBook serial numbers to the corporate device identifiers to mark the devices as corporate. But, by default, devices are marked personal. |
| Devices are user-less, such as kiosk, dedicated, or shared. | ❌ <br/><br/> These devices are organization-owned. User-less devices should be enrolled using [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article) or Apple Configurator. |

---

### Device enrollment administrator tasks

This task list provides an overview.

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- There isn't a Company Portal app for macOS devices in the Apple App Store, or through VPP. Users must [manually download and run the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070). They sign in with their organization account (`user@contoso.com`), and then step through the enrollment. Once they enroll, they must approve the enrollment profile.

  When they approve, the device is added to your organization Azure AD. Then, it's available to Intune to receive your policies and profiles.

  Be sure to communicate this information with your users.

### Device enrollment end user tasks

Your users must do the following steps. For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

1. Download and run [the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070).
2. Open the Company Portal app, and sign in with their organization account (`user@contoso.com`). Once they sign in, they must approve the enrollment profile (System preferences). When users approve, the device is enrolled, and considered managed. If they don't approve, then they're not enrolled, and won't receive your policy and profiles.

For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use on devices owned by your organization. This option configures settings using Apple Business Manager (ABM) or Apple School Manager (ASM). It enrolls a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your preconfigured settings, and can be shipped directly to users or schools. You create an enrollment profile in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and push this profile to the devices.

For more specific information on this enrollment type, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| Devices are owned by the organization or school. | ✔️ |
| You have new devices. | ✔️ |
| You have existing devices. | ✔️ <br/><br/> To enroll existing devices, see [Enroll your macOS device registered in ABM/ASM with Automated Device Enrollment after Setup Assistant](../enrollment/device-enrollment-program-enroll-macos.md#enroll-your-macos-device-registered-in-abmasm-with-automated-device-enrollment-after-setup-assistant) (opens another Microsoft article). |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using [Device enrollment](#byod-device-enrollment) (in this article). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users must unenroll from the current MDM provider, and then enroll in Intune. Or, you can use Device enrollment to manage specifics apps on the device. Since these devices are organization-owned, it's recommended to enroll in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### ADE administrator tasks

This task list provides an overview. For more specific information, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
- Be sure the Apple token (.p7m) is active. For more specific information, see [Get an Apple ADE token](../enrollment/device-enrollment-program-enroll-macos.md#get-an-apple-ade-token).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- Decide how users will authenticate on their devices: **Setup Assistant (legacy)** or **Setup Assistant with modern authentication**. Make this decision before you create the enrollment profile. Using the **Setup Assistant with modern authentication** is considered modern authentication. Microsoft recommends using **Setup Assistant with modern authentication**.

  For all organization-owned macOS devices, **Setup Assistant (legacy)** is always and automatically used, even if you don't see "Setup Assistant" text in Endpoint Manager. Setup Assistant (legacy) authenticates the user, and enrolls the device.

  - Select the **Setup Assistant (legacy)** when:

    - You want to wipe the device.
    - You don't want to use modern authentication features, such as MFA.
    - You don't want to register devices in Azure AD. Setup Assistant (legacy) authenticates the user with the Apple `.p7m` token. If it's acceptable to not register devices in Azure AD, then you don't need to install the Company Portal app. Keep using the Setup Assistant (legacy).

      If you want to use the Company Portal app for authentication instead of using Setup Assistant, or want the devices registered in Azure AD, then install the **Company Portal** app. **After** the device is enrolled, you can install the Company Portal app.

      To install the Company Portal app on devices, see [add the Company Portal app](../apps/apps-company-portal-macos.md). Set the Company Portal app as a required app.

      Once installed, users open the Company Portal app, and sign in with their organization Azure AD account (`user@contoso.com`). When they sign in, they're authenticated, and ready to receive your policies and profiles.

  - Select the **Setup Assistant with modern authentication** when:

    - You want to wipe the device.
    - You want to use multi-factor authentication (MFA).
    - You want to prompt users to update their expired password when they first sign in.
    - You want to prompt users to reset their expired passwords during enrollment.
    - You want devices registered in Azure AD. When they're registered, you can use features available with Azure AD, such as conditional access.

    > [!NOTE]
    > During the Setup Assistant, users must enter their organization Azure AD credentials (`user@contoso.com`). When they enter their credentials, the enrollment starts. If you want, users can also enter their Apple ID to access Apple specific features, such as Apple Pay.
    > 
    > After the Setup Assistant completes, users can use the device. When the home screen shows, the enrollment is complete, and user affinity is established. The device isn't fully registered with Azure AD, and doesn't show in a user's device list in Azure AD.
    > 
    > If users need access to resources protected by conditional access or should be fully registered with Azure AD, then [install the Company Portal app](../apps/apps-company-portal-macos.md). After it's installed, users open the Company Portal app, and sign in with their organization Azure AD account (`user@contoso.com`). During this second login, any conditional access policies are evaluated, and Azure AD registration is complete. Users can install and use organizational resources, including LOB apps.

- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile. Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).

  - **Enroll with user affinity**: Setup Assistant authenticates the user, and enrolls the device in Intune. Also choose if users can delete the management profile, called **Locked enrollment**.

  - **Enroll without user affinity**: Setup Assistant authenticates the user, and enrolls the user in Intune. Also choose if users can delete the management profile, called **Locked enrollment**. The Company Portal app isn't used, needed, or supported on enrollments without user affinity.

### ADE end user tasks

These tasks depend on how administrators tell users to install the Company Portal app. Typically, the less end users must do to enroll, the higher chance they'll want to enroll.

For more specific information on the end user steps, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

- **Enroll with user affinity + Setup Assistant (legacy)**:

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`).
  2. The Setup Assistant prompts the user for information, and enrolls the device in Intune. The device isn't registered in Azure AD.

      If you're using Setup Assistant for authentication, then stop here.

  3. Optional. If you're using the Company Portal app for authentication (instead of Setup Assistant), then the Company Portal app [installs using the option](../apps/apps-company-portal-macos.md) you configured.

      Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, users are authenticated, and can access organization resources.

      Remember, installing the Company Portal app is optional. If you want your users to authenticate using Company Portal app, instead of using the Setup Assistant, then [add the Company Portal app](../apps/apps-company-portal-macos.md).

- **Enroll with user affinity + Setup Assistant with modern authentication**:

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`) and their organization Azure AD credentials (`user@contoso.com`).

      When users enter their Azure AD credentials, the enrollment starts.

  2. The Setup Assistant may prompt the user for additional information. When it completes, users can use the device. When the home screen shows, the enrollment is complete and user device affinity is established. Users will see your apps and policies on the device.

  3. Users open the Company Portal app [you installed](../apps/apps-company-portal-macos.md), and sign in with their organization credentials (`user@contoso.com`) again.

- **Enroll without user affinity**: No actions. Be sure your users don't install the Company Portal app.

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Direct enrollment

Use on devices owned by your organization that don't need user device affinity.

These devices are organization-owned, and use Apple Configurator. The only purpose is to be a kiosk-style device. They aren't associated with a single or specific user. These devices are commonly used to scan items, print tickets, get digital signatures, manage inventory, and more.

For more specific information on this enrollment type, see [Use Direct Enrollment for macOS devices](../enrollment/device-enrollment-direct-enroll-macos.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You need a wired connection, or are having a network issue. | ✔️ |
| Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements.  | ✔️ <br/><br/> The idea of *not* using the ABM or ASM portals is to give administrators less control.|
| A country doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM). | ✔️ <br/><br/> If your country supports ABS or ASM, then devices should be enrolled using [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article). |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> If you have a large number of devices, then this method will take some time. |
| Devices are associated with a single user. | ❌ <br/><br/> Not recommended. Devices that need user affinity should be enrolled using [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised). |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. BYOD or personal devices should be enrolled using [MAM-WE](deployment-guide-enrollment-mamwe.md) (opens another Microsoft article), or [BYOD: Device enrollment](#byod-device-enrollment) (in this article). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. Or, you can use MAM-WE to manage specifics apps on the device. Since these devices are organization-owned, we recommend enrolling in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### Direct enrollment administrator tasks

This task list provides an overview. For more specific information, see [macOS Direct Enrollment](../enrollment/device-enrollment-direct-enroll-macos.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Endpoint Manager, and is active. This certificate is required to enroll macOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile. Select **Enroll without user affinity** (user-less devices or shared devices). With user-less devices:

  - Users can't use apps that require a user, including the Company Portal app. The Company Portal app isn't used, needed, or supported on enrollments without user affinity. Be sure users don't install the Company Portal app from the Apple app store.
  - **Enroll with user affinity** is available in the UI, but it won't work. Don't select this option. If you need user affinity, then use [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article).

- When the enrollment profile is ready, export the policy, and copy the file to the macOS device. Double-click the file to install the enrollment policy.

For more information on this enrollment option, and its prerequisites, see [macOS Direct Enrollment](../enrollment/device-enrollment-direct-enroll-macos.md).

### Direct enrollment end user tasks

- **Enroll without user affinity**: No actions. Be sure they don't install the Company Portal app from the Apple app store.

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/configurator-enroll-without-user-affinity.png" alt-text="In the Endpoint Manager admin center and Microsoft Intune, enroll macOS devices using Direct enrollment. Select enroll without user affinity.":::

## Next steps

- [MAM](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)
