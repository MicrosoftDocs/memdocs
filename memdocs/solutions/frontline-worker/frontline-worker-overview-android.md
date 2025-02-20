---
title: Get started with Android frontline worker devices
description: Learn how to manage frontline worker devices using Android devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 02/19/2025
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

# Frontline worker for Android devices in Microsoft Intune

Android devices are in almost every industry across the globe, including healthcare, aviation, construction, manufacturing, logistics, and government. They're commonly used by frontline workers (FLW) in these industries and more.

Using Intune, you can manage Android devices used by frontline workers in your organization. This article:

- Includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.
- Helps you determine the best enrollment option and the best device management experience for you and your end users.

This article applies to:

- Android devices owned by the organization and enrolled in Intune

For an overview on FLW devices in Intune, go to [FLW device management in Intune](frontline-worker-overview.md).

Use this article to get started with Android FLW devices in Intune. Specifically:

- [Step 1 - Select your Intune enrollment option](#step-1---select-your-intune-enrollment-option)
- [Step 2 - Choose between a shared device or a user associated device](#step-2---shared-device-or-user-associated-device)
- [Step 3 - Configure the home screen and device experience](#step-3---home-screen-and-device-experience)
- [Microsoft Entra shared device mode for Android Enterprise dedicated devices](#microsoft-entra-shared-device-mode-for-android-enterprise-dedicated-devices)

## Before you begin

Intune supports different enrollment options for Android devices, as shown in the following image:

:::image type="content" source="./media/android-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for Android frontline worker devices in Microsoft Intune." lightbox="./media/android-flw-enrollment-options.png":::

This article focuses on the enrollment options commonly used for FLW devices. For more information on all the Android enrollment options, go to [Enrollment guide: Enroll Android devices in Microsoft Intune](../../intune/fundamentals/deployment-guide-enrollment-android.md).

## Step 1 - Select your Intune enrollment option

The first step is to determine the Intune enrollment platform that's best for your organization and device needs.

For FLW Android devices, you should use **Android Enterprise** or **Android Open Source Project (AOSP)** enrollment.

You can use the following image to help decide the path that's best for your FLW devices:

:::image type="content" source="./media//android-flw-options.png" alt-text="Diagram that shows Android Enterprise frontline worker scenario path in Microsoft Intune." lightbox="./media//android-flw-options.png":::

Make sure you know what the device is doing and its use case. Android device manufacturers (OEMs) offer different devices, some might be specialty devices and others might be more generic.

For example, devices that are used for augmented or virtual reality typically don't support GMS, which is a requirement for Android Enterprise enrollment. So, the natural enrollment path for these devices is Android (AOSP).

# [Android Enterprise](#tab/ae)

**Android Enterprise** enrollment devices require and support [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site). These devices are also used in countries/regions that allow GMS.

✅ If the device is GMS enabled and is in the [Android Enterprise recommended list](https://www.android.com/enterprise/recommended/) (opens Android's web site), then use Android Enterprise enrollment.

❌ If these devices are used in a country/region that blocks GMS, then Android Enterprise enrollment isn't supported. Instead, use Android (AOSP) enrollment.

# [Android (AOSP)](#tab/aosp)

**Android (AOSP)** enrollment devices don't offer or include Google Mobile Services (GMS). These devices:

- Can be specialty devices, like augmented or virtual reality devices, including Realwear and HTC.
- Don't support GMS.
- Are used in countries/regions that block GMS.

✅ If your devices meet these criteria, then use Android (AOSP) enrollment. Make sure your devices are supported for Android (AOSP) management with Intune. For a list of supported devices, go to [AOSP supported devices](../../intune/fundamentals/android-os-project-supported-devices.md).

❌ If these devices support GMS and don't meet these criteria, then use Android Enterprise enrollment.

To learn more about Android (AOSP), go to [About the Android Open Source Project](https://source.android.com/) (opens Android's web site).

---

> [!NOTE]
> For Android device administrator (DA), Google is deprecating and reducing features. We recommended that you move to Android Enterprise or Android (AOSP) for your FLW devices.

## Step 2 - Shared device or user associated device

The next decision is to decide if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are enrolled and managed with Intune.

- **Shared device with no user association (userless)**

  With shared devices, a user gets the device, completes their tasks, and gives the device to another user. Typically, these users manually sign into apps; they don't sign into the device.

  When using shared devices:

  - If you're using Android shared devices and the devices support Android Enterprise enrollment, then enroll your devices as **dedicated devices**. These devices support Google Mobile Services (GMS) and aren't associated with a single or specific user.

    For more information on dedicated device enrollment, go to [Intune enrollment of Android Enterprise dedicated devices](../../intune/enrollment/android-kiosk-enroll.md).

  - If you're using Android (AOSP) shared devices, then you can enroll your devices as **userless devices**. These devices typically don't support GMS and aren't associated with a single or specific user.

    For more information on Android (AOSP) userless enrollment, go to [Intune enrollment for Android (AOSP) corporate-owned userless devices](../../intune/enrollment/android-aosp-corporate-owned-userless-enroll.md).

- **User associated device**

  These devices have one user. This user associates the device with themselves, which typically happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Microsoft Entra.

  With user association:

  - If you're using **Android Enterprise**, then you can enroll your devices as **Fully managed** or **Corporate-owned device with a work profile**. These devices have one user, and are used exclusively for organization work; not personal use.

    These enrollment options aren't common for FLW devices and expand the boundary of traditional frontline worker scenarios. But, they can be used if their features are best for your business scenario. They have many settings you can configure. For example, when using **fully managed** enrollment, you can configure the Microsoft Launcher, add a custom wallpaper, and more.

    For more information on these enrollment methods, go to:

    - [Intune enrollment for Android Enterprise fully managed devices](../../intune/enrollment/android-fully-managed-enroll.md)
    - [Intune enrollment for corporate-owned devices with a work profile](../../intune/enrollment/android-corporate-owned-work-profile-enroll.md)

    For a list of some of the settings can you can configure, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../../intune/configuration/device-restrictions-android-for-work.md).

  - If you're using **Android (AOSP)**, then you can enroll your devices as a **user-associated** device. These devices have one user, and are used exclusively for organization work; not personal use.

    Remember, Android (AOSP) devices don't support Google Mobile Services (GMS).

    - For more information on Android (AOSP) user-associated enrollment, go to [Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../../intune/enrollment/android-aosp-corporate-owned-user-associated-enroll.md).
    - For a list of some of the settings can you can configure, go to [Android (AOSP) device settings to allow or restrict features using Intune](../../intune/configuration/device-restrictions-android-aosp.md).

## Step 3 - Home screen and device experience

For **Android (AOSP)**, there isn't a home screen experience to configure when devices are enrolled in Intune using AOSP. When frontline workers get AOSP-enrolled devices, they turn on the devices, sign-in to an app (or don't sign in, depending on the user association), like Microsoft Teams. Then, they just start using the devices.

For **Android Enterprise dedicated devices**, there are home screen and device experience features you can configure in Intune. This section and steps apply to:

- **Android Enterprise dedicated devices**

This step is optional and depends on your business scenario. If these devices are shared by many users, then it's recommended to use the home screen and device experience features described in this section.

On Android Enterprise devices, you can configure the Intune Managed Home Screen (MHS) app to control the home screen and device experience.

In this step, consider what end users are doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

The following scenarios are common for FLW:

- **Scenario 1: Device wide access with multiple apps**

  The devices are enrolled in Intune as **Android Enterprise dedicated devices**.

  Users have access to the apps and settings on the device. Using policy settings, you can restrict users from different features, like debugging, system applications, and more.

  For this scenario, you want users to use specific apps, but don't want the device locked to only those apps.

  To configure devices for this scenario, you deploy the apps, and configure the apps using application configuration policies. Then, use device configuration policies to allow or block device features.

  To get started, use the following links:

  1. [Add apps to Intune](../../intune/apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.

  2. [Create app configuration policies](../../intune/apps/app-configuration-policies-overview.md) to configure app features. You can also add a JSON file with all the configuration settings you want.

  3. Create a device configuration restrictions profile that [allows or restricts features using Intune](../../intune/configuration/device-restrictions-android-for-work.md).

      In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Templates** > **Device restrictions** > **Device experience** > **Dedicated device** > **Kiosk mode**. Set it to **Not configured**:

      :::image type="content" source="./media/android-dedicated-device-kiosk-not-configured.png" alt-text="Dedicated device is the enrollment profile type and kiosk mode isn't configured in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/android-dedicated-device-kiosk-not-configured.png":::

- **Scenario 2: Locked screen device with pinned apps**

  The devices are enrolled in Intune as **Android Enterprise dedicated devices**.

  For this scenario, you install the Intune Managed Home Screen (MHS) app, which allows you to customize the managed device experience. You can pin one app or many apps, select a wallpaper, set icon positions, require a PIN, and more. This scenario is often used for **dedicated devices**, like shared devices.

  **What you need to know**:

  - Only features added to the Managed Home Screen (MHS) are available to end users. So, you can restrict end users from accessing settings and other device features.
  - When you pin one app or pin many apps to the MHS, only those apps open. They're the only apps users can access.  
  - The MHS is the enterprise launcher you use. Don't install another enterprise launcher app.

  For more information on the MHS app on dedicated devices, go to the [Setup Microsoft MHS on dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) blog post.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../../intune/apps/apps-add.md), including the MHS app. When the apps are added, you create app policies that deploy the apps to the devices.

  2. Use a [device restrictions configuration profile](../../intune/configuration/device-restrictions-configure.md) to set the kiosk mode to multi-app, and select your apps. This step locks the device to only the apps you select:

      In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Templates** > **Device restrictions** > **Device experience** > **Dedicated device** > **Kiosk mode** > **Multi-app** > **Add**. Add the apps you want in multi-app kiosk mode:

      :::image type="content" source="./media/android-dedicated-device-kiosk-multi-app.png" alt-text="Enrollment profile type is set to dedicated device, and kiosk mode is set to multi app in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/android-dedicated-device-kiosk-multi-app.png":::

  3. Configure the Microsoft Managed Home Screen (MHS) app using one of the following options:

      - **Option 1 - Device restrictions configuration profile**: In the same device restrictions configuration profile, configure the device features you want when in multi-app kiosk mode.

        For a list of settings you can configure, go to [Android Enterprise - Device experience settings](../../intune/configuration/device-restrictions-android-for-work.md#device-experience).

      - **Option 2 - App configuration policy**: The app configuration policy has more configuration settings than the device restrictions configuration profile. You can also add a JSON file with all the configuration settings you want.

        For more information, go to [Configure the Microsoft Managed Home Screen app](../../intune/apps/app-configuration-managed-home-screen-app.md).

- **Scenario 3: Single app kiosk**

  The devices are enrolled in Intune as **Android Enterprise dedicated devices**.

  This scenario is used on devices that have a single purpose, like scanning inventory.

  **What you need to know**:

  - A single app is assigned to the device. When the device starts, only this app opens. Users are locked to the single app and can't close the app, or do anything else on the device.
  - This option is more restrictive, as the device is dedicated to only run a single application.
  - An enterprise launcher isn't used.

  To configure these devices, you assign the app to the device. Then, you create a device configuration policy that sets the device to single app kiosk mode.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../../intune/apps/apps-add.md). When the app is added, you create an app policy that deploys the app to the devices.
  2. Create a device configuration restrictions profile that [allows or restricts features using Intune](../../intune/configuration/device-restrictions-android-for-work.md):

      In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** **Configuration** > **Templates** > **Device restrictions** > **Device experience** > **Dedicated device** > **Kiosk mode** and select **Single app**:

      :::image type="content" source="./media/android-dedicated-device-kiosk-single-app.png" alt-text="Enrollment profile type is set to dedicated device, and the kiosk mode is set to single app in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/android-dedicated-device-kiosk-single-app.png":::

## Microsoft Entra shared device mode for Android Enterprise dedicated devices

Microsoft Entra shared device mode (SDM) is another option for **Android Enterprise dedicated device** enrollments.

Microsoft Entra SDM offers an app and identity driven sign in/sign out experience, which improves the end user experience and productivity (less sign in prompts). It compliments **Scenario 1** (Device wide access with multiple apps) and **Scenario 2** (Locked screen device with pinned apps) described at [Step 3 - Home screen and device experience](#step-3---home-screen-and-device-experience) (in this article).

For more information on Microsoft Entra shared device mode (SDM), go to [Microsoft Entra shared device mode for FLW](frontline-worker-overview.md#microsoft-entra-shared-device-mode-for-flw).

**What you need to know**:

- Android enrollment in Intune as a shared device and Microsoft Entra SDM are complimentary. Android enrollment in Intune as a shared device doesn't depend on Microsoft Entra SDM. Microsoft Entra SDM is an option on top of the Intune shared device enrollment.

- Microsoft Entra SDM is a feature of Microsoft Entra. It's not an Intune feature. For more information on Microsoft Entra SDM for Android Enterprise devices, go to:

  - [Shared device mode for Android devices](/azure/active-directory/develop/msal-android-shared-devices)
  - [Enroll Android Enterprise dedicated devices into Microsoft Entra Shared device mode - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/enroll-android-enterprise-dedicated-devices-into-azure-ad-shared/ba-p/1820093) blog post
  - [Intune supports sign out for apps not optimized with Microsoft Entra shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post

- For end users to have the full sign in/sign out experience, apps must support the Microsoft Authentication Library (MSAL). For more information, go to [Enable cross-app single sign-on (SSO) on Android using MSAL](/azure/active-directory/develop/msal-android-single-sign-on).

## Related articles

- [Frontline worker device management overview in Microsoft Intune](frontline-worker-overview.md)
- [FLW for iOS/iPadOS devices](frontline-worker-overview-ios-ipados.md)
- [FLW for Windows devices](frontline-worker-overview-windows.md)
