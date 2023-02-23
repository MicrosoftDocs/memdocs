---
# required metadata

title: iOS/iPadOS device enrollment guide for  Microsoft Intune
description: Enroll iOS and iPadOS devices using user and device enrollment, automated device enrollment (DEP), and Apple Configurator in Microsoft Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/10/2022
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
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune

Personal and organization-owned devices can be enrolled in Intune. Once they're enrolled, they receive the policies and profiles you create. You have the following options when enrolling iOS/iPadOS devices:

- [Automated device enrollment (ADE)](#automated-device-enrollment-ade-supervised)
- [Apple Configurator](#apple-configurator-enrollment)
- [BYOD: User and Device enrollment](#byod-user-and-device-enrollment)

This article provides recommendations on the iOS/iPadOS enrollment method to use. It also includes an overview of the administrator and user tasks for each enrollment type. 

For more specific information, see [Enroll iOS/iPadOS devices](../enrollment/ios-enroll.md). There's also a visual guide of the different enrollment options for each platform:

[![A visual representation of Intune enrollment options by platform](./media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use on devices owned by your organization. This option configures settings using Apple Business Manager (ABM) or Apple School Manager (ASM). It enrolls a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your preconfigured settings, and can be shipped directly to users or schools. You create an enrollment profile in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and push this profile to the devices.

For more specific information on this enrollment type, see:

- [Apple Business Manager enrollment](../enrollment/device-enrollment-program-enroll-ios.md)
- [Apple School Manager enrollment](../enrollment/apple-school-manager-set-up-ios.md): For more information on Apple School Manager, see [Apple education](https://www.apple.com/education/k12/it/) (opens Apple's web site).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You want supervised mode. | ✔️ <br/><br/> Supervised mode deploys software updates, restricts features, allows and blocks apps, and more.|
| Devices are owned by the organization or school. | ✔️ |
| You have new devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. Applications on BYOD or personal devices can be managed using [MAM](deployment-guide-enrollment-mamwe.md) (opens another Microsoft article), or [User and Device enrollment](#byod-user-and-device-enrollment) (in this article). |
| You have existing devices. | ❌ <br/><br/>Existing devices should be enrolled using [Apple Configurator](#apple-configurator-enrollment) (in this article). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users must unenroll from the current MDM provider, and then enroll in Intune. Or, you can use MAM to manage specifics apps on the device. Since these devices are organization-owned, we recommend enrolling in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### ADE administrator tasks

This task list provides an overview. For more specific information, see [Apple Business Manager enrollment](../enrollment/device-enrollment-program-enroll-ios.md) or [Apple School Manager enrollment](../enrollment/apple-school-manager-set-up-ios.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
- Be sure the Apple token (.p7m) is active. For more specific information, see [Get an Apple ADE token](../enrollment/device-enrollment-program-enroll-ios.md#get-an-apple-automated-device-enrollment-token).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Intune, and is active. This certificate is required to enroll iOS/iPadOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- Decide how users will authenticate on their devices: the **Company Portal** app, **Setup Assistant (legacy)**, or **Setup Assistant with modern authentication**. Make this decision before you create the enrollment profile. Using the **Company Portal** app or **Setup Assistant with modern authentication** is considered modern authentication.

  - Select the **Company Portal** app when:

    - You want to wipe the device.
    - You want to use multi-factor authentication (MFA).
    - You want to prompt users to update their expired password when they first sign in.
    - You want to prompt users to reset their expired passwords during enrollment.
    - You want devices registered in Azure AD. When they're registered, you can use features available with Azure AD, such as conditional access.
    - You want to automatically install the **Company Portal** app during enrollment. If your company uses the Volume Purchase Program (VPP), you can automatically install **Company Portal** app during enrollment without user Apple IDs.
    - You want to lock the device until the **Company Portal** app installs. After it installs, users sign in to the Company Portal app with their organization Azure AD account. Then, the device is unlocked, and users can use it.

  - Select the **Setup Assistant (legacy)** when:

    - You want to wipe the device.
    - You don't want to use modern authentication features, such as MFA.
    - You don't want to register devices in Azure AD. Setup Assistant (legacy) authenticates the user with the Apple `.p7m` token. If it's acceptable to not register devices in Azure AD, then you don't need to install the Company Portal app. Keep using the Setup Assistant (legacy).

      If you want devices registered in Azure AD, then install the **Company Portal** app. When you create the enrollment profile and select Setup Assistant (legacy), you can install the Company Portal app. We recommend installing the **Company Portal** app during enrollment.

  - Select the **Setup Assistant with modern authentication** when:

    - You want to wipe the device.
    - You want to use multi-factor authentication (MFA).
    - You want to prompt users to update their expired password when they first sign in.
    - You want to prompt users to reset their expired passwords during enrollment.
    - You want devices registered in Azure AD. When they're registered, you can use features available with Azure AD, such as conditional access.
    - You want to automatically install the **Company Portal** app during enrollment. If your company uses the Volume Purchase Program (VPP), you can automatically install the **Company Portal** app during enrollment without user Apple IDs.
    - You want users to use the device, even when the Company Portal app isn't installed.

  > [!NOTE]
  > To authenticate users, Microsoft recommends using the **Company Portal** app or the **Setup Assistant with modern authentication**.
  >
  > Which option should you use? It depends:
  >
  > - If you want to use the device before the Company Portal app installs, then use the **Setup Assistant with modern authentication**.
  > 
  >   During the Setup Assistant, users must enter their organization Azure AD credentials (`user@contoso.com`). When they enter their credentials, the enrollment starts, and the Company Portal app installs. If you want, users can also enter their Apple ID to access Apple specific features, such as Apple Pay.
  > 
  >   After the Setup Assistant completes, users can use the device. When the home screen shows, the enrollment is complete, and user affinity is established. The device isn't fully registered with Azure AD, and shows as non-compliant in a user's device list in Azure AD. The device shows as compliant in the Microsoft Intune admin center.
  > 
  >   After the Company Portal app installs, which takes some time, users open the Company Portal app, and sign with their organization Azure AD account (`user@contoso.com`) again. During this second login, any conditional access policies are evaluated, and Azure AD registration is complete. Users can install and use organizational resources, including LOB apps. The device shows as compliant in Azure AD.
  > - If you don't want to use the device before the Company Portal app installs, then use the **Company Portal** app option. The **Company Portal** app option locks the device until the Company Portal app installs. When the install completes, the Company Portal app opens automatically. Users sign in with their Azure AD organization account (`user@contoso.com`), and can use the device.

- If you use the Company Portal app, then decide how the Company Portal app will be installed on the devices. Make this decision before you create the enrollment profile.

  > [!NOTE]
  > Microsoft recommends using the Volume Purchase Program (VPP) when using the Company Portal app to authenticate. It's a better end user experience.

  Don't install the Company Portal app from the app store directly on ADE-enrolled devices. Instead, install the Company Portal app using the following options:

  - **VPP token + Enrolling new devices**: If you have the Volume Purchase Program (VPP), and you're enrolling new devices, then the Company Portal app is included. When you create the enrollment profile in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Install Company Portal with VPP**. No other steps are needed.

    This option:

    - Includes the correct Company Portal app version.
    - You don't have to create another policy to deploy the Company Portal app to devices.
    - The Company Portal app must be updated manually by you, or your users.

  - **No VPP token + Enrolling new devices**: No administrator tasks. Make sure users enter their Apple ID in Setup Assistant.

    When Setup Assistant completes, the Company Portal app tries to automatically install. If users don't enter their Apple ID (`user@iCloud.com` or `user@gmail.com`), then they're continually prompted to enter their Apple ID. Users must enter their Apple ID to get the Company Portal app on their devices. When the Company Portal app installs, users open it, and enter their organization credentials (`user@contoso.com`). When they authenticate, users can install and use apps used by your organization, including LOB apps.

  - **Already enrolled devices**: If devices are already enrolled, if you have VPP or not, then use an app configuration policy:

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal app as a required app, and as a device licensed app.
    2. Create an app configuration policy that includes the Company Portal app as a device licensed app. For more specific information, see [Configure the Company Portal app to support iOS and iPadOS DEP devices](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment).
    3. Deploy the app configuration policy to the same device group as the enrollment profile.
    4. When devices check in with the Intune service, it receives your profile, and the Company Portal app installs.

    This option:

    - Includes the correct Company Portal app version.
    - Requires you to create an enrollment profile, and create an app configuration policy. In your app configuration policy, make it a required app so you know the app deploys to all your devices.
    - The Company Portal app can be automatically updated by changing your existing app configuration policy.

- In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile:

  - Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).
  - Choose where users authenticate: the **Company Portal** app, **Setup Assistant (legacy)**, or **Setup Assistant with modern authentication**.

  For more specific information and suggestions, see [Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

### ADE end user tasks

When you create an enrollment profile in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you choose to associate a user to the device (**Enroll with user affinity**), or have shared devices (**Enroll without user affinity**). The specific steps depend on how you configure the enrollment profile. With Shared iPad, after activation, all Setup Assistant panes are automatically skipped.

- **Enroll with user affinity + Company Portal app**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/ade-user-affinity-company-portal-app.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using automated device enrollment (ADE). Select enroll with user affinity and use the Company Portal app for authentication.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`). Once entered, the Company Portal app is automatically installed from your enrollment profile. It can take some time for the Company Portal app to auto-install.
  2. Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). When they sign-in, the enrollment starts. When enrollment completes, users can install and use apps used by your organization, including LOB apps.

  Users may have to enter more information. For more specific end user steps, see [Enroll your organization-provided iOS device](../user-help/enroll-your-device-dep-ios.md).

- **Enroll with user affinity + Setup Assistant (legacy) + Company Portal app**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/ade-user-affinity-setup-assistant-legacy-company-portal-app.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using automated device enrollment (ADE). Select enroll with user affinity, use the Setup Assistant for authentication, and install the Company Portal app.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`).
  2. The Setup Assistant prompts the user for information.
  3. The Company Portal app automatically opens, and should lock the device in a kiosk-style mode. It can take some time for the Company Portal app to open. Users sign in with their organization credentials (`user@contoso.com`), and the device is enrolled in Intune.

      This step registers the device in Azure AD. Users can install and use apps used by your organization, including LOB apps.

- **Enroll with user affinity + Setup Assistant (legacy) - Company Portal app**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/ade-user-affinity-setup-assistant-legacy-no-company-portal-app.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using automated device enrollment (ADE). Select enroll with user affinity, use the Setup Assistant for authentication, and don't install the Company Portal app.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`).
  2. The Setup Assistant prompts the user for information, and enrolls the device in Intune. The device isn't registered in Azure AD.

- **Enroll with user affinity + Setup Assistant with modern authentication**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/ade-user-affinity-setup-assistant-modern-authentication.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using automated device enrollment (ADE). Select enroll with user affinity, and use the Setup Assistant for authentication. The Company Portal app automatically installs.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`) and their organization Azure AD credentials (`user@contoso.com`).

      When users enter their Azure AD credentials, the enrollment starts.

  2. Setup Assistant prompts the user for additional information. When the home screen appears, setup is complete. The device is fully enrolled, and user device affinity is established. Users can use their devices and see your apps and policies on their devices.

      At this point, the device isn't fully registered with Azure AD and shows as non-compliant in Azure AD. The device shows it's compliant in the Microsoft Intune admin center.

  3. If you **Install Company Portal app with VPP** (recommended), then the Company Portal app automatically installs. Users open the Company Portal app, and sign in with their work or school account (`user@contoso.com`) again. They complete Azure AD registration in the Company Portal app, which fully registers the device with Azure AD. Users then gain access to corporate resources protected by conditional access policies and the device shows as being compliant in Azure AD.

  4. If you don't **Install Company Portal app with VPP**, and want to use the Company Portal app, then:

      1. Users sign in to the Apple app store with their Apple ID (`user@iCloud.com` or `user@gmail.com`). When they sign in, the Company Portal app automatically installs.

          This extra sign-in step slows the enrollment, especially if users don't sign in immediately.

          If they don't sign in to the app store, then the Company Portal app doesn't install. If the app isn't installed, then users can't register the device in Azure AD. Since the device hasn't completed registration, the device shows as non-compliant in Azure AD. Any resources depending on conditional access aren't available.

      2. Users open the Company Portal app, and sign in with their work or school account (`user@contoso.com`) again. They complete Azure AD registration in the Company Portal app, which fully registers the device with Azure AD. At the next check-in, users gain access to corporate resources protected by conditional access policies.

- **Enroll without user affinity**: No actions. Be sure they don't install the Company Portal app from the Apple app store.

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/ade-enroll-without-user-affinity.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using automated device enrollment (ADE). Select enroll without user affinity.":::

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## Apple Configurator enrollment

Use on devices owned by your organization, and includes [Direct Enrollment](../enrollment/apple-configurator-enroll-ios.md#direct-enrollment). This option requires you to physically connect iOS/iPadOS devices to a Mac computer using the USB port.

For more specific information on this enrollment type, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| You need a wired connection, or are having a network issue. | ✔️ |
| Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements.  | ✔️ <br/><br/> The idea of *not* using the ABM or ASM portals is to give administrators less control.|
| A country/region doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM). | ✔️ <br/><br/> If your country/region supports ABS or ASM, then devices should be enrolled using [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article). |
| Devices are owned by the organization or school. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ <br/><br/> If you have a large number of devices, then this method will take some time. |
| Devices are associated with a single user. | ✔️ |
| Devices are user-less, such as kiosk or dedicated device. | ✔️ |
| Devices are personal or BYOD. | ❌ <br/><br/> Not recommended. Applications on BYOD or personal devices can be managed using [MAM](deployment-guide-enrollment-mamwe.md) (opens another Microsoft article), or [User and Device enrollment](#byod-user-and-device-enrollment) (in this article). |
| Devices are managed by another MDM provider. | ❌ <br/><br/> To be fully managed by Intune, users need to unenroll from the current MDM provider, and then enroll in Intune. Or, you can use MAM to manage specifics apps on the device. Since these devices are organization-owned, we recommend enrolling in Intune. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> The DEM account isn't supported. |

---

### Apple Configurator administrator tasks

This task list provides an overview. For more specific information, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

- Requires access to a Mac computer with a USB port.
- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Intune, and is active. This certificate is required to enroll iOS/iPadOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- Decide how users will authenticate on their devices: the **Company Portal** app, or **Setup Assistant**. Make this decision before you create the enrollment profile. Using the Company Portal app is considered modern authentication. We recommend using the Company Portal app.

  - Select the **Company Portal** app when:

    - You want to use multi-factor authentication (MFA).
    - You want to prompt users to update their expired password when they first sign in.
    - You want to prompt users to reset their expired passwords during enrollment.
    - You want devices registered in Azure AD. When they're registered, you can use features available with Azure AD, such as conditional access.
    - You want to automatically install **Company Portal** app during enrollment. If your company uses the Volume Purchase Program (VPP), you can automatically install **Company Portal** app during enrollment.

  - Select the **Setup Assistant** when:

    - You don't want to use modern authentication features, such as MFA.
    - You want to wipe the device.
    - You want to import serial numbers.
    - You don't want to register devices in Azure AD. Setup Assistant authenticates the user with the exported enrollment profile that you copy to the device. If it's acceptable to not register devices in Azure AD, then you don't need to install the Company Portal app. Keep using the Setup Assistant.

      If you want devices registered in Azure AD, then install the **Company Portal** app. When you create the enrollment profile and select Setup Assistant, you can install the Company Portal app. We recommend installing the **Company Portal** app during enrollment.

- If you use the Company Portal app, then the Company Portal app must be installed on devices using an app configuration policy. We recommend creating this policy before you create the enrollment profile.

  Don't install the Company Portal app from the app store directly on Apple Configurator-enrolled devices. Instead, install the Company Portal app using the following options:

  - **Enroll new devices**: No administrator tasks. Make sure users enter their Apple ID in Setup Assistant.

    When Setup Assistant completes, the Company Portal app tries to automatically install. If users don't enter their Apple ID (`user@iCloud.com` or `user@gmail.com`), then they're continually prompted to enter their Apple ID. Users must enter their Apple ID to get the Company Portal app on their devices. When the Company Portal app installs, users open it, and enter their organization credentials (`user@contoso.com`). When they authenticate, users can install and use apps used by your organization, including LOB apps.

  - **Already enrolled devices**: If devices are already enrolled, then use an app configuration policy:

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal app as a required app, and as a device licensed app.
    2. Create an app configuration policy that includes the Company Portal app as a device licensed app. For more specific information, see [Configure the Company Portal app to support iOS and iPadOS DEP devices](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment).
    3. Deploy the app configuration policy to the same device group as the enrollment profile.
    4. When devices check in with the Intune service, it receives your profile, and the Company Portal app installs.

    This option:

    - Includes the correct Company Portal app version.
    - Requires you to create an enrollment profile, and create an app configuration policy. In your app configuration policy, make it a required app so you know the app deploys to all your devices.
    - The Company Portal app can be automatically updated by changing your existing app configuration policy.

- In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile:

  - Choose to **Enroll with user affinity** (associate a user to the device), or **Enroll without user affinity** (user-less devices or shared devices).

  - If you choose **Enroll without user affinity**, then you're automatically using **Direct enrollment**. Remember:

    - You're using the settings from an existing macOS enrollment profile.
    - Users can't use apps that require a user, including the Company Portal app. The Company Portal app isn't used, needed, or supported on enrollments without user affinity. Be sure users don't install the Company Portal app from the Apple app store.

- When the enrollment profile is ready, USB connect the devices to the Mac, and open the **Apple Configurator** app. When the app opens, it detects the USB connected device, and deploys the Intune enrollment profile you created.

For more information on this enrollment option, and its prerequisites, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

### Apple Configurator end user tasks

The tasks depend on the option you configured in the enrollment profile.

- **Enroll with user affinity + Company Portal app**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/configurator-user-affinity-company-portal-app.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using Apple Configurator. Select enroll with user affinity and use the Company Portal app for authentication.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their Apple ID (`user@iCloud.com` or `user@gmail.com`). Once entered, the Company Portal app is automatically installed from the app store. It can take some time for the Company Portal app to auto-install.
  2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). When users sign-in, the enrollment starts. When enrollment completes, users can install and use apps used by your organization, including LOB apps.

  Users may have to enter more information. For more specific steps, see [Enroll your organization-provided iOS device](../user-help/enroll-your-device-dep-ios.md).

- **Enroll with user affinity + Setup Assistant + Company Portal app**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/configurator-user-affinity-setup-assistant-company-portal-app.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using Apple Configurator. Select enroll with user affinity, use Setup Assistant for authentication, and install the Company Portal app.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their organization credentials (`user@contoso.com`). This step enrolls the device in Intune.
  2. The Setup Assistant prompts the user for information, including the Apple ID (`user@iCloud.com` or `user@gmail.com`).
  3. The Company Portal app automatically installs from the app store. Users open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). This step registers the device in Azure AD. Users can install and use apps used by your organization, including LOB apps.

- **Enroll with user affinity + Setup Assistant - Company Portal app**:

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/configurator-user-affinity-setup-assistant-no-company-portal-app.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using Apple Configurator. Select enroll with user affinity, use Setup Assistant for authentication, and don't install the Company Portal app.":::

  1. When the device is turned on, the Apple Setup Assistant runs. Users enter their organization credentials (`user@contoso.com`). This step enrolls the device in Intune.
  2. The Setup Assistant prompts the user for information, including the Apple ID (`user@iCloud.com` or `user@gmail.com`). This step pushes the Intune management profile to the device.
  3. Users install the management profile. The profile checks-in with the Intune service, and enrolls the device. The device isn't registered in Azure AD.

- **Enroll without user affinity**: You're using Direct enrollment. No actions. Be sure they don't install the Company Portal app from the Apple app store.

  :::image type="content" source="./media/deployment-guide-enrollment-ios-ipados/configurator-enroll-without-user-affinity.png" alt-text="In the Intune admin center and Microsoft Intune, enroll iOS/iPadOS devices using Apple Configurator. Select enroll without user affinity.":::

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

## BYOD: User and Device enrollment

These iOS/iPadOS devices are personal or BYOD (bring your own device) devices that can access organization email, apps, and other data. Starting with iOS 13 and newer, this enrollment option targets users or targets devices. It doesn't require resetting the devices.

When you create the enrollment profile, you're asked to choose **User enrollment**, **Device enrollment** or **Determine based on user choice**.

For the specific enrollment steps, and its prerequisites, see [Set up iOS/iPadOS User or Device enrollment](../enrollment/ios-user-enrollment.md).

---
| Feature | Use this enrollment option when |
| --- | --- |
| Devices are personal or BYOD. | ✔️ |
| You want to help protect a specific feature on the device, such as per-app VPN. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are managed by another MDM provider. | ❌ <br/><br/> When a device enrolls, MDM providers install certificates and other files. These files must be removed. The quickest way may be to unenroll, or factory reset the devices. If you don't want to factory reset, then contact the MDM provider. |
| You use the device enrollment manager (DEM) account. | ✔️ |
| Devices are owned by the organization or school. |  ❌ <br/><br/> Not recommended. Organization-owned devices should be enrolled using [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article) or [Apple Configurator](#apple-configurator-enrollment) (in this article). |
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/>Typically, user-less or shared devices are organization-owned. These devices should be enrolled using [Automated Device Enrollment](#automated-device-enrollment-ade-supervised) (in this article) or [Apple Configurator](#apple-configurator-enrollment) (in this article). |

---

### User and Device enrollment administrator tasks

This task list provides an overview. For more specific information, see [Set up iOS/iPadOS and iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- Be sure the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) is added to Intune, and is active. This certificate is required to enroll iOS/iPadOS devices. For more information, see [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).
- In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create the enrollment profile. When you create the enrollment profile, you have the following options:

  - **Device enrollment**: This option is a typical enrollment for personal devices. The device is managed, not just specifics apps or features. With this option, consider the following information:

    - You can deploy certificates that apply to the whole device.
    - Users must install updates. Only devices enrolled using Automated Device Enrollment (ADE) can receive updates using MDM policies or profiles.
    - A user must be associated with the device. This user can be a device enrollment manager (DEM) account.

  - **Determine based on user choice**: Gives end users a choice when they enroll. Depending on their selection, **User enrollment** or **Device enrollment** is used.

  - **User enrollment**: Starting with iOS 13 and newer. This option configures a specific set of features and organization apps, such as password, per-app VPN, Wi-Fi, and Siri. If you use User enrollment, and to help secure apps and their data, then we recommend also using app protection policies.

    For the complete list of what you can and can't do, see [Intune actions and options supported with Apple User Enrollment](../enrollment/ios-user-enrollment-supported-actions.md). For the specific user enrollment steps, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

    > [!NOTE]
    > BYOD can become organization-owned devices. To make these devices corporate, see [Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md).

    User enrollment is considered friendlier to end users. But, it may not provide the feature set and security features administrators need. In some scenarios, user enrollment may not be the best option. Consider the following scenarios:

    - User enrollment creates a work partition on the devices. The features and security you configure in the user enrollment profile only exist in the work partition. They don't exist in the user partition. Users can't factory reset the work partition. Administrators can. Users can factory reset the personal partition. Administrators can't.

    - If users primarily use Microsoft apps, or use apps created with the [Intune App SDK](../developer/app-sdk.md), then users should download these apps from the Apple app store. Then, use app protection policies to protect these apps. In this scenario, you don't need user enrollment.

    - For line of business (LOB) apps, user enrollment might be an option, as it will deploy these apps to the work partition. Application management (MAM) doesn't support LOB apps. So if you need LOB apps, then use User Enrollment.

    - When devices are enrolled using user enrollment, you can't switch to device enrollment. With user enrollment, you can't move an app from unmanaged to managed. Users must unenroll from user enrollment, and then re-enroll to device enrollment.

    - If you install apps before the user enrollment profile is applied, then these apps aren't protected or managed by the user enrollment profile.

      For example, a user downloads the Outlook app from the Apple app store. The app automatically installs to the user partition on the device. The user configures Outlook for their personal email. When users configure their organization email, they're blocked by conditional access, and asked to enroll. They enroll, and a user enrollment profile deploys.

      Since the Outlook app was installed before the user enrollment profile, the user enrollment profile fails. The Outlook app can't be managed because it's installed and configured in the user partition, not the work partition. Users must manually uninstall the Outlook app.

      Once uninstalled, users can sync the device manually, and possibly reapply the user enrollment profile. Or, you may have to create an app configuration policy to deploy Outlook, and make it a required app. Then, deploy an app protection policy to secure the app and its data.

- Assign the enrollment profile to user groups. Don't assign to device groups.

### User and Device enrollment end user tasks

Your users must do the following steps. For the specific user experience, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md).

1. Go to the Apple app store, and [install the Intune Company Portal app](../user-help/sign-in-to-the-company-portal.md).
2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

    Users may have to enter more information. For more specific steps, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md). 

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]

> [!TIP]
> There is a short, step-by-step video to help your users enroll their devices in Intune:
>
> [Enroll your iOS/iPadOS device](https://www.youtube.com/watch?v=mJyv6YcHi7c)

## Next steps

- [MAM](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)
