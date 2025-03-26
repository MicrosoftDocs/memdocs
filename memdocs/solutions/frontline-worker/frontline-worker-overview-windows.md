---
title: Get started with Windows frontline worker devices
description: Learn how to manage frontline worker devices using Windows devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 08/19/2024
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: cbernier
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Frontline worker for Windows devices in Microsoft Intune

Windows has different devices and cloud services that can be used for frontline workers (FLW). These devices are used globally and in many industries & scenarios, including digital signage, check-in tasks, presentations, kiosks, and more.

You can use physical Windows devices or use Windows 365 Cloud PCs.

Using Intune, you can manage Windows devices used by frontline workers in your organization. This article:

- Helps you determine the best enrollment option and the best device management experience for you and your end users.
- Includes decisions admins need to make, including determining how the device is used, and configuring the device experience.

This article applies to:

- Windows devices owned by the organization and enrolled in Intune

For an overview on FLW devices in Intune, go to [FLW device management in Intune](frontline-worker-overview.md).

Use this article to get started with Windows FLW devices in Intune. Specifically:

- [Windows 365 Cloud PCs](#windows-365-cloud-pcs)
- [Step 1 - Select your enrollment option](#step-1---select-your-enrollment-option)
- [Step 2 - Shared device or user associated device](#step-2---shared-device-or-user-associated-device)
- [Step 3 - Device experience and kiosk](#step-3---device-experience-and-kiosk)

## Windows 365 Cloud PCs

**Windows 365 Cloud PCs** are virtual machines that are hosted in the Windows 365 service. They're accessible from anywhere and from any device. They include a Windows desktop experience and are associated with a user. Basically, end users have their own PC in the cloud.

✅ Windows 365 Cloud PCs are ideal for frontline workers that need a Windows desktop experience, but don't need a physical device. For example, a call center worker that needs access to a Windows desktop app.

These devices enroll in Intune, and are managed like any other device, including apps, configuration settings, and updates.

For information on Windows 365 Cloud PCs, and to learn more, go to:

- [Windows 365 Cloud PCs overview - Enterprise](/windows-365/enterprise/overview)
- [Windows 365 Cloud PCs overview - Small & medium business](/windows-365/business/get-started-windows-365-business)

## Step 1 - Select your enrollment option

✅ **Determine the enrollment option** that's best for your organization.

Determining the enrollment option is the first step. Enrollment determines how the devices are added to Intune for you to manage. The option you choose depends on your business needs and the devices you have.

For FLW devices using Windows, you can use **Windows Autopilot** enrollment or use a **provisioning package**. This section focuses on these enrollment options.

# [Windows Autopilot](#tab/autopilot)

**Windows Autopilot** is the recommended option for FLW devices. You can ship the devices directly to the location without ever touching the devices. With self-deploying mode, users turn on the device, and the enrollment automatically starts.

✅ If you have Microsoft Entra Premium and you're getting new devices from an OEM, then use Windows Autopilot. You can use the Windows OEM version preinstalled on the devices to automatically enroll the devices. End users only need to turn on the device; no other end user interaction is required.

You can use Windows Autopilot on existing devices. When the existing devices are reset, the Windows Autopilot enrollment can automatically start.

❌ Windows Autopilot requires Microsoft Entra Premium. If you don't have Entra Premium, then use a provisioning package. There are other Windows enrollment options available, but they're not commonly used for FLW devices.

For information on Windows Autopilot, go to [Windows Autopilot overview](/autopilot/overview) and [Windows Autopilot self-deploying mode](/autopilot/self-deploying).

# [Provisioning package](#tab/provpackage)

This option uses the Windows Configuration Designer (WCD) app to create a provisioning package (`.ppkg`). When you create the package, you configure the enrollment settings you want. Then, you make the package available to users on a USB drive or network location (including a SharePoint site).

✅ If you don't have Microsoft Entra Premium, then use a provisioning package. You can use the provisioning package to bulk enroll many devices. You can also use the provisioning package to enroll new and existing devices.

❌ If you have Microsoft Entra Premium, then use Windows Autopilot. Windows Autopilot requires Entra Premium.

For information on using a provisioning package with Intune, go to [Bulk enrollment for Windows devices](../../intune-service/enrollment/windows-bulk-enroll.md).

---

> [!NOTE]
> There are other Windows enrollment options available. This article focuses on the enrollment options commonly used for FLW devices. For information on all the Windows enrollment options, go to [Enrollment guide: Enroll Windows client devices in Microsoft Intune](../../intune-service/fundamentals/deployment-guide-enrollment-windows.md).

## Step 2 - Shared device or user associated device

✅ Determine if the devices are **shared with many users** or **assigned to a single user**.

In this step, this decision depends on your business needs and the end user requirements. It also impacts how these devices are managed with Intune.

These features are configured using Intune device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

# [Shared device](#tab/shared)

**Shared PC** is a feature in Intune, and allows devices to be shared with many users, one user at a time. A user gets the device, completes their tasks, and gives the device to another user. End users sign in to these shared devices with their **Microsoft Entra organization account** or a **guest account**. With this feature, you can delete account information and allow (or prevent) users from saving & viewing files locally.

For example, shared Windows devices can be public computers in libraries, computer labs in schools & universities, shared workstations in offices, and shared laptops in classrooms.

For information on this feature, and to get started, go to:

- [Shared PC or multi-user Windows devices in Intune](../../intune-service/configuration/shared-user-device-settings-windows.md)
- [Shared PC or multi-user Windows devices in Intune - Settings list](../../intune-service/configuration/shared-user-device-settings.md)

# [User associated device](#tab/single)

These devices have one user. This user associates the device with themselves, which happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Microsoft Entra.

These devices are used in FLW scenarios where the device is only used by that user. Some examples include personal computers for support staff, design computers for architects & graphic artists, and work-from-home setups.

---

## Step 3 - Device experience and kiosk

✅ **Configure the device experience**.

This step is optional and depends on your business scenario. If many users share these devices, then we recommended you configure the device experience using the features described in this section.

On Windows devices, you can configure the home screen and device experience. In this step, consider what frontline workers are doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

Some examples of kiosks include self-service terminals in airports, retail stores, government offices, and other public spaces. These devices allow users to do specific tasks, like check-in for flights, access information, or complete transactions.

These features are configured using device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

The following scenarios are common.

### Scenario 1 - Kiosk with one app or many apps

For this scenario, you configure the device as a kiosk, which allows you to customize the device experience.

For example, you can use the device in a lobby so customers can see your product catalog. Or, use the device to show visual content as a digital sign. For information, go to [Configure kiosks and digital signs on Windows desktop editions](/windows/configuration/kiosk-methods) (opens another Microsoft web site).

You can pin one app or many apps, select a wallpaper, set icon positions, and more. This scenario is often used for dedicated devices, such as shared devices. You can create a Shared PC profile and configure it be a kiosk using the kiosk settings in Intune.

**What you need to know**:

- Only features added to the kiosk are available to end users. So, you can restrict end users from accessing settings and other device features.
- When you pin one app or pin many apps to the kiosk, only those apps open. They're the only apps users can access. Users are locked to those apps, can't close the apps, or do anything else on the devices. This scenario is used on devices dedicated to a specific use, like airport terminals.

To get started, use the following links:

1. [Add apps to Microsoft Intune](../../intune-service/apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.
2. Create a device configuration [kiosk profile](../../intune-service/configuration/kiosk-settings.md) and configure the [Windows kiosk profile - settings list](../../intune-service/configuration/kiosk-settings.md).

    The following example shows the kiosk profile settings for a single app. Make sure you add the app to Intune before you configure the kiosk profile.

    :::image type="content" source="./media/windows-kiosk-single-app.png" alt-text="The kiosk device configuration profile settings for a single app on Windows devices in Microsoft Intune." lightbox="./media/windows-kiosk-single-app.png":::

    The following example shows the kiosk profile settings for multiple apps. Make sure you add the apps to Intune before you configure the kiosk profile.

    :::image type="content" source="./media/windows-kiosk-multi-app.png" alt-text="The kiosk device configuration profile settings for multiple apps on Windows devices in Microsoft Intune." lightbox="./media/windows-kiosk-multi-app.png":::

### Scenario 2 - Device wide access with many apps

This scenario is a good scenario for Windows 365 Cloud PCs. Users have access to the apps and settings on the device. You can restrict users from different features, such as simple passwords, features in the Settings app, and more.

This scenario also applies to physical devices. It expands the boundary of traditional frontline worker scenarios by also including knowledge workers.

To configure devices for this scenario, you deploy the apps to the devices. Then, use device configuration policies to allow or block device features.

To get started, use the following links:

1. [Add apps to Microsoft Intune](../../intune-service/apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.
2. Create a device configuration restrictions profile that [allows or restricts features using Intune](../../intune-service/configuration/device-restrictions-windows-10.md). There are hundreds of settings available for you to configure, including more in the [Settings Catalog](../../intune-service/configuration/settings-catalog.md).

    :::image type="content" source="./media/windows-device-restrictions.png" alt-text="All the device restrictions settings for Windows devices in Microsoft Intune.":::

## Related articles

- [Frontline worker device management overview in Microsoft Intune](frontline-worker-overview.md)
- [FLW for Android devices](frontline-worker-overview-android.md)
- [FLW for iOS/iPadOS devices](frontline-worker-overview-ios-ipados.md)
