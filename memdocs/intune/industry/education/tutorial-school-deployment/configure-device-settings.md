---
title: Configure and secure devices with Microsoft Intune
description: Learn how to configure policies with Microsoft Intune in preparation for device deployment.
zone_pivot_groups: platforms-windows-ios
ms.topic: tutorial
author: scottbreenmsft
ms.author: scbree
ms.manager: dougeby
ms.date: 5/2/2024
ms.service: microsoft-intune
ms.subservice: education
---

# Configure and secure devices with Microsoft Intune

With Intune, you can configure settings for devices in the school, to ensure that they comply with specific policies.
For example, you may need to secure your devices, ensuring that they are kept up to date. Or you may need to configure all the devices with the same look and feel.

Settings can be assigned to groups:

- If you target settings to a **group of users**, those settings apply, regardless of what managed devices the targeted users sign in to
- If you target settings to a **group of devices**, those settings apply regardless of who is using the devices

## Introduction

✅ Learn about the different types of settings

::: zone pivot="windows"

### [Intune](#tab/intune)

Device profiles allow you to add and configure settings, and then push these settings to devices in your organization. You have some options when creating policies:

- **Baselines**: Baselines include preconfigured security settings. If you want to create security policy using recommendations by Microsoft security teams, then security baselines are for you.

  For more information, see [Security baselines](/mem/intune/protect/security-baselines).

- **Settings catalog**: Use the settings catalog to see all the available settings, and in one location. For example, you can see all the settings that apply to BitLocker, and create a policy that just focuses on BitLocker.

  For more information, see [Settings catalog](/mem/intune/configuration/settings-catalog).

- **Templates**: Templates include a logical grouping of settings that configure a feature or concept, such as VPN, email, kiosk devices, and more. If you're familiar with creating device configuration policies in Microsoft Intune, then you're already using these templates.

  For more information, including the available templates, see [Apply features and settings on your devices using device profiles](/mem/intune/configuration/device-profiles).

> [!TIP]
> You can find a list of common configurations used in K-12 organizations at [Common Education configuration overview](/mem/intune/industry/education/tutorial-school-deployment/common-config-overview).

### [Intune For Education](#tab/intune-for-education)

There are two ways to manage settings in Intune for Education:

- **Express Configuration.** This option is used to configure a selection of settings that are commonly used in school environments
- **Group settings.** This option is used to configure all settings offered by Intune for Education

> [!NOTE]
> Express Configuration is ideal when you are getting started. Settings are pre-configured to Microsoft-recommended values, but can be changed to fit your school's needs.

With Express Configuration, you can get Intune for Education up and running in just a few steps. You can select a group of devices or users, select applications to distribute, and choose settings from the most commonly used in schools.

::: zone-end

::: zone pivot="ios"

### [Intune](#tab/intune)

Device profiles allow you to add and configure settings, and then push these settings to devices in your organization. You have some options when creating policies:

- **Settings catalog**: Use the settings catalog to see all the available settings, and in one location. For example, you can see all the settings that apply to Networking, and create a policy that just focuses on Network.

  For more information, see [Settings catalog](/mem/intune/configuration/settings-catalog).

- **Templates**: Templates include a logical grouping of settings that configure a feature or concept, such as VPN, email, kiosk devices, and more. If you're familiar with creating device configuration policies in Microsoft Intune, then you're already using these templates.

  For more information, including the available templates, see [Apply features and settings on your devices using device profiles](/mem/intune/configuration/device-profiles).

### [Intune For Education](#tab/intune-for-education)

There are two ways to manage settings in Intune for Education:

- **Express Configuration.** This option is used to configure a selection of settings that are commonly used in school environments.
- **Group settings.** This option is used to configure all settings that are offered by Intune for Education.

> [!NOTE]
> Express Configuration is ideal when you are getting started. Settings are pre-configured to Microsoft-recommended values, but can be changed to fit your school's needs.

With Express Configuration, you can get Intune for Education up and running in just a few steps. You can select a group of devices or users, select applications to distribute, and choose settings from the most commonly used in schools.

> [!TIP]
> To learn more, and practice step-by-step Express Configuration in Intune for Education, try [this interactive demo](https://www.microsoft.com/education/interactive-demos/deploy-apps-and-policies).

::: zone-end

## Device settings

✅ Configure settings and assign them to devices

::: zone pivot="windows"

### [Intune](#tab/intune)

To create a device configuration profile in Microsoft Intune, you need to follow these steps:

- Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
- Go to **Devices** > **Manage devices** > **Configuration** > **+ Create profile**.
- Select **Platform** as **Windows 10 and later**.
- Select **Profile type**:
  - For general settings, select [**Settings Catalog**](/mem/intune/configuration/settings-catalog).
  - For templates including certificates, Wi-Fi, and VPN, select **Templates** and     then choose the required template.
- Follow the steps to create and configure the profile as necessary.

### [Intune For Education](#tab/intune-for-education)

Groups are used to manage users and devices with similar management needs, allowing you to apply changes to many devices or users at once. To review the available group settings:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Groups** > Pick a group to manage.
1. Select **Windows device settings**.
1. Expand the different categories and review information about individual settings.

Settings that are commonly configured for student devices include:

- Wallpaper and lock screen background. See [Lock screen and desktop][INT-7].
- Wi-Fi connections. See [Add Wi-Fi profiles][INT-8].
- Enablement of the integrated testing and assessment solution *Take a Test*. See [Add Take a Test profile][INT-9].

For more information, see [Windows device settings in Intune for Education][INT-3].

> [!NOTE]
> If you require more sophisticated device settings, you can create them in Microsoft Intune. For more information, see [Apply features and settings on your devices using device profiles](/mem/intune/configuration/device-profiles).

::: zone-end

::: zone pivot="ios"

### [Intune](#tab/intune)

To create a device configuration profile in Microsoft Intune, you need to follow these steps:

- Sign in to the Microsoft Intune admin center.
- Go to **Devices** > **Manage devices** > **Configuration** > **+ Create profile**.
- Select **Platform** as **iOS/iPadOS**.
- Select **Profile type**:
  - For general settings, select **Settings Catalog**.
  - For templates including certificates, Wi-Fi, and VPN, select **Templates** and then choose the required template.
- Follow the steps to create and configure the profile as necessary.

### [Intune For Education](#tab/intune-for-education)

Groups are used to manage users and devices with similar management needs, allowing you to apply changes to many devices or users at once. To review the available group settings:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com/).
1. Select **Groups** > Pick a group to manage.
1. Select **iOS device settings**.
1. Expand the different categories and review information about individual settings.

Settings that are commonly configured for student devices include:

- Lock screen and wallpaper. See [Lock screen and wallpaper](/intune-education/all-edu-settings-ios#lock-screen-and-wallpaper).
- Wi-Fi connections. See [Add Wi-Fi profiles][INT-8].

For more information, see [iOS device settings in Intune for Education](/intune-education/all-edu-settings-ios).

> [!NOTE]
> If you require more sophisticated device settings, you can create them in Microsoft Intune. For more information, see [Apply features and settings on your devices using device profiles](/mem/intune/configuration/device-profiles).

::: zone-end

## Update policies

✅ Configure update policies and assign to devices

::: zone pivot="windows"

### [Intune](#tab/intune)

It is important to keep Windows devices up to date with the latest security updates. You can create Windows Update policies using Intune.

- [What is Windows Update for Business?][WIN-1]
- [Manage Windows software updates in Intune][MEM-1]

### [Intune For Education](#tab/intune-for-education)

It is important to keep Windows devices up to date with the latest security updates. You can create Windows Update policies using Intune for Education.

To create a Windows Update policy:

1. Select **Groups** > Pick a group to manage.
1. Select **Windows device settings**.
1. Expand the category **Update and upgrade**.
1. Configure the required settings as needed.

For more information, see [Updates and upgrade][INT-6].

> [!NOTE]
> If you require a more complex Windows Update policy, you can create it in Microsoft Intune. For more information:
>
> - [What is Windows Update for Business?][WIN-1]
> - [Manage Windows software updates in Intune][MEM-1]

::: zone-end

::: zone pivot="ios"

### [Intune](#tab/intune)

It is important to keep iOS devices up to date with the latest security updates. You can create control updates with Intune using three different methods:

- **Option 1** - iOS and iPadOS 17.0 and newer devices (recommended) - [Managed software update policy](/mem/intune/protect/managed-software-updates-ios-macos).
- **Option 2** - iOS and iPadOS 17.0 and older (recommended) - [Software update policy](/mem/intune/protect/software-updates-ios).
- **Option 3** (not recommended) - End users manually install the updates.

At **Devices** > **Manage devices** > **Configuration** > **Create** > **Settings catalog** > **Restrictions**, you can use the following settings to delay how long after an update is released that users can manually install the updates.

- **Defer software updates**: Yes/No
- **Delay default visibility of software updates**: 0-90

> [!TIP]
> The **Settings Catalog** > **Declarative Device Management** > **Software Update** settings take precedence over the **Settings Catalog** > **Restrictions** settings. For more information, go to [Precedence of settings in iOS updates policy](/mem/intune/protect/managed-software-updates-ios-macos).

For more information, see [Software updates planning guide and scenarios for supervised iOS/iPadOS devices in Microsoft Intune](/mem/intune/protect/software-updates-guide-ios-ipados).

### [Intune For Education](#tab/intune-for-education)

It is important to keep iOS devices up to date with the latest security updates. You can control when Intune triggers iOS devices to update using Intune for Education.

To create a iOS update restrictions policy:

1. Select **Groups** > Pick a group to manage.
1. Select **iOS device settings**.
1. Expand the category **Update restrictions**.
1. Configure the required settings as needed.

For more information about the other update options in the Intune console, see [Software updates planning guide and scenarios for supervised iOS/iPadOS devices in Microsoft Intune](/mem/intune/protect/software-updates-guide-ios-ipados).

::: zone-end

## Security policies

✅ Configure security policies and assign them to devices

::: zone pivot="windows"

### [Intune](#tab/intune)

It is critical to ensure that the devices you manage are secured using the different security technologies available in Windows.

- [Antivirus][MEM-2]
- [Disk encryption][MEM-3]
- [Firewall][MEM-4]
- [Endpoint detection and response][MEM-5]
- [Attack surface reduction][MEM-6]
- [Account protection][MEM-7]
- [Security Baselines](/mem/intune/protect/security-baselines)
- [Local Administrator Password Solution](/windows-server/identity/laps/laps-overview)
- [Web Content Filtering on Edge](/deployedge/microsoft-edge-web-content-filtering)

Microsoft recommmends phishing resistant credentials and using Windows Hello for Business on Windows devices where possible. For more informaiton, and to find out how to do this for students, see [Passwordless for Students](/microsoft-365/education/deploy/protect-passwordless-students?tabs=windows).

### [Intune For Education](#tab/intune-for-education)

It is critical to ensure that the devices you manage are secured using the different security technologies available in Windows.
Intune for Education provides different settings to secure devices.

To create a security policy:

1. Select **Groups** > Pick a group to manage.
1. Select **Windows device settings**.
1. Expand the category **Security**.
1. Configure the required settings as needed, including:
    - Windows Defender
    - Windows Encryption
    - Windows SmartScreen

For more information, see [Security][INT-4].

> [!NOTE]
> If you require more sophisticated security policies, you can create them in Microsoft Intune. For more information, see:
>
> - [Antivirus][MEM-2]
> - [Disk encryption][MEM-3]
> - [Firewall][MEM-4]
> - [Endpoint detection and response][MEM-5]
> - [Attack surface reduction][MEM-6]
> - [Account protection][MEM-7]
> - [Security Baselines](/mem/intune/protect/security-baselines)
> - [Local Administrator Password Solution](/windows-server/identity/laps/laps-overview)
> - [Web Content Filtering on Edge](/deployedge/microsoft-edge-web-content-filtering)

::: zone-end

::: zone pivot="ios"

### [Intune](#tab/intune)

In Intune, you can configure iOS security settings using Settings Catalog.

To create a settings catalog device configuration profile in Microsoft Intune, you need to follow these steps:

- Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
- Go to **Devices** > **Manage devices** > **Configuration** > **+ Create profile**.
- Select **Platform** as **iOS/iPadOS**.
- Select **Profile type**.
- Select **Settings Catalog**.
- Follow the steps to create and configure the profile as necessary.

Common areas for security include:

- Restrictions
- Security

### [Intune For Education](#tab/intune-for-education)

In Intune for Education, you can configure iOS security settings using Groups.

1. Select **Groups** > Pick a group to manage.
1. Select **iOS device settings**.
1. Configure the required settings as needed.

Common areas for security include:

- Device restrictions
- Passcode, Touch ID, and Face ID

> [!NOTE]
> If you require more sophisticated security settings, you can create them in Microsoft Intune. For more information, see [Apply features and settings on your devices using device profiles](/mem/intune/configuration/device-profiles).

::: zone-end

---

## Next steps

Now that you've configured your device settings, you can configure applications to deploy to your students' and teachers' devices.

> [!div class="nextstepaction"]
> [Next: Configure applications >](configure-device-apps.md)

<!-- Reference links in article -->

[INT-2]: /intune-education/express-configuration-intune-edu
[INT-3]: /intune-education/all-edu-settings-windows
[INT-4]: /intune-education/all-edu-settings-windows#security
[INT-6]: /intune-education/all-edu-settings-windows#updates-and-upgrade
[INT-7]: /intune-education/all-edu-settings-windows#lock-screen-and-desktop
[INT-8]: /intune-education/add-wi-fi-profile
[INT-9]: /intune-education/take-a-test-profiles

[WIN-1]: /windows/deployment/update/waas-manage-updates-wufb

[MEM-1]: /mem/intune/protect/windows-update-for-business-configure
[MEM-2]: /mem/intune/protect/endpoint-security-antivirus-policy
[MEM-3]: /mem/intune/protect/encrypt-devices
[MEM-4]: /mem/intune/protect/endpoint-security-firewall-policy
[MEM-5]: /mem/intune/protect/endpoint-security-edr-policy
[MEM-6]: /mem/intune/protect/endpoint-security-asr-policy
[MEM-7]: /mem/intune/protect/endpoint-security-account-protection-policy
