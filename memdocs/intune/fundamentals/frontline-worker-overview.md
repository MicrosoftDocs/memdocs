---
title: Get started with Frontline worker devices in Microsoft Intune
description: Learn how to manage frontline worker devices using Android, iOS/iPadOS, and Windows devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 08/23/2023
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
zone_pivot_groups: flw-platforms
---

# Frontline worker device management for Android, iOS/iPadOS, and Windows devices in Microsoft Intune

A frontline worker (FLW) is a person that works in an essential or critical role to your business. They're typically in direct contact with the public and customers. During a crisis or emergency, such as a pandemic or natural disaster, frontline workers are often at the forefront of the response effort, providing critical services and support. Some popular examples of frontline workers include healthcare, emergency responders, law enforcement, retail & food service, and transportation.

This article applies to:

- Android devices owned by the organization and enrolled in Intune
- iOS and iPadOS devices owned by the organization and enrolled in Intune
- Windows devices owned by the organization and enrolled in Intune

> [!NOTE]
> FLW devices are typically owned by the organization. End user personal devices can be used as FLW devices. Personal devices aren't covered in this article. This article focuses on corporate-owned devices.

Frontline workers also rely on devices to enable their productivity, such as devices used to scan barcodes or devices utilized for field operations. If these devices fail, worker productivity and business operation can stop. Often, these types of devices can be categorized as mission critical.

The article provides guidance on managing and configuring frontline worker (FLW) devices using Intune. These devices play a key role in running business operations. And, they're an extension of the operator who uses and relies on the device to be productive for day-to-day business operations.

## Before you begin

When you're planning for FLW devices (including rugged devices) and how you'll manage them, there are questions you need to answer. These questions help you determine the best device management experience for you, your end user frontline workers, and the needs of your organization.

- Determine how the **devices will be used**.

  For example, you can provide a device wide experience where frontline workers access all the apps and settings on the device. Or, provide a locked screen experience where frontline workers only access specific apps. You can configure the device for a single purpose, such as scanning inventory, or for multiple purposes, such as using an app to check in customers and using another app to check email.

  Intune has built-in kiosk features that can run one app or run many apps for Android, iPadOS, and Windows. This article provides more details about these device management scenarios.

- Determine if the **devices will be shared** with other users, or if the devices are assigned to specific users.

  For example, if the devices are part of a shared pool, then your device management strategy should focus on shared device management. If the devices are assigned to specific users, then your device management strategy should focus on user associated device management.

  Intune has built-in features that offer shared device management for Android, iPadOS, and Windows devices. This article provides more details about shared devices, and the decisions you need to make.

- Determine the **sign-in/sign-out experience** and how user switching will happen, including device hand-off. For example, before cradling the device for charging, you may want users to sign out of apps.

  Intune has built-in features that allow users to sign in as a guest, sign in with their Azure AD organization credentials, or only sign into apps. There are also features that use single sign-on and single sign out for your apps. This article provides more details about these features.

- Determine the **starting app experience**. For example, users can sign in to the device and then launch an app, or users can get the device and have an app automatically start.

  Intune has built-in features that allow you to configure the starting app experience. This article provides more details about these features.

When you have this information, the next step is to identify the platforms you use and the devices scenarios.

::: zone pivot="all,android"
## Android

This section focuses on Android devices used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

Android devices are in almost every industry across the globe, including healthcare, aviation, construction, manufacturing, logistics, and government. They're commonly used by frontline workers in these industries.

Intune supports different enrollment options for Android devices, as shown in the following image:

:::image type="content" source="./media/frontline-worker-overview/android-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for Android frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-flw-enrollment-options.png":::

For FLW Android devices, the most common enrollment options are **Android Enterprise** and **Android Open Source Project (AOSP)**. You can use the following image to help decide the path that's best for your FLW devices:

:::image type="content" source="./media/frontline-worker-overview/android-flw-options.png" alt-text="Diagram that shows Android Enterprise frontline worker scenario path in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-flw-options.png":::

When you use Android devices for frontline workers, the steps in this section help you determine the best enrollment option & the best device management experience for you and your end users.

> [!NOTE]
> There are other Android enrollment options available. This section focuses on the enrollment options commonly used for FLW devices. For more information on all the Android enrollment options, go to [Enrollment guide: Enroll Android devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-android.md).

### Step 1 - Select your Intune enrollment option (Android)

The first step is to determine the Intune enrollment platform that's best for your organization and device needs.

For FLW devices using the Android platform, you should use **Android Enterprise** or **Android Open Source Project (AOSP)** enrollment.

Make sure you know what the device is doing and its use case. Android device manufacturers (OEMs) offer different devices, some may be specialty and others may be more generic.

For example, devices that are used for augmented or virtual reality typically don't support GMS, which is a requirement for Android Enterprise enrollment. So, the natural enrollment path for these devices is Android (AOSP).

# [Android Enterprise](#tab/ae)

**Android Enterprise** enrollment devices require and support [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site). These devices are also used in countries/regions that allow GMS.

✔️ If the device is GMS enabled and is in the [Android Enterprise recommended list](https://www.android.com/enterprise/recommended/) (opens Android's web site), then use Android Enterprise enrollment.

❌ If these devices are used in a country/region that blocks GMS, then Android Enterprise enrollment isn't supported. Instead, use Android (AOSP) enrollment.

# [Android (AOSP)](#tab/aosp)

**Android (AOSP)** enrollment devices don't offer or include Google Mobile Services (GMS). These devices:

- Can be specialty devices, such as augmented or virtual reality devices, including Realwear and HTC.
- Don't support GMS.
- Are used in countries/regions that block GMS.

✔️ If your devices meet these criteria, then use Android (AOSP) enrollment. Make sure your devices are supported for Android (AOSP) management with Intune. For a list of supported devices, go to [AOSP supported devices](android-os-project-supported-devices.md).

❌ If these devices support GMS and don't meet these criteria, then use Android Enterprise enrollment.

To learn more about Android (AOSP), go to [About the Android Open Source Project](https://source.android.com/) (opens Android's web site).

---

> [!NOTE]
> For Android device administrator (DA), Google is deprecating and reducing features. It's recommended that you move to Android Enterprise or Android (AOSP) for your FLW devices.

### Step 2 - Shared device or user associated device (Android)

The next decision is to decide if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are enrolled and managed with Intune.

- **Shared device with no user association (userless)**

  With shared devices, a user gets the device, completes their tasks, and gives the device to another user. Typically, these users manually sign into apps; they don't sign into the device.

  When using shared devices:

  - If you're using Android shared devices and the devices support Android Enterprise enrollment, then enroll your devices as **dedicated devices**. These devices support Google Mobile Services (GMS) and aren't associated with a single or specific user.

    For more information on dedicated device enrollment, go to [Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

  - If you're using Android (AOSP) shared devices, then you can enroll your devices as **userless devices**. These devices typically don't support GMS and aren't associated with a single or specific user.

    For more information on Android (AOSP) userless enrollment, go to [Intune enrollment for Android (AOSP) corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md).

- **User associated device**

  These devices have one user. This user associates the device with themselves, which typically happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Azure Active Directory (Azure AD).

  With user association:

  - If you're using **Android Enterprise**, then you can enroll your devices as **Fully managed** or **Corporate-owned device with a work profile**. These devices have one user, and are used exclusively for organization work; not personal use.

    These enrollment options aren't common for FLW devices and expand the boundary of traditional frontline worker scenarios. But, they can be used if their features are best for your business scenario. They have many settings you can configure. For example, when using **fully managed** enrollment, you can configure the Microsoft Launcher, add a custom wallpaper, and more.

    For more information on these enrollment methods, go to:

    - [Intune enrollment for Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md)
    - [Intune enrollment for corporate-owned devices with a work profile](/mem/intune/enrollment/android-corporate-owned-work-profile-enroll)

    For a list of some of the settings can you can configure, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

  - If you're using **Android (AOSP)**, then you can enroll your devices as a **user-associated** device. Remember, Android (AOSP) devices don't support Google Mobile Services (GMS). These devices have one user, and are used exclusively for organization work; not personal use.

    - For more information on Android (AOSP) user-associated enrollment, go to [Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md).
    - For a list of some of the settings can you can configure, go to [Android (AOSP) device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-aosp.md).

### Step 3 - Home screen and device experience (Android)

For **Android (AOSP)**, there isn't a home screen experience to configure when devices are enrolled in Intune using AOSP. When frontline workers get AOSP-enrolled devices, they turn on the devices, sign-in to an app (or don't sign in, depending on the user association), like Microsoft Teams, and then just start using them.

For **Android Enterprise dedicated devices**, there are home screen and device experience features you can configure in Intune. This section and steps apply to:

- **Android Enterprise dedicated devices**

This step is optional and depends on your business scenario. If these devices will be shared by many users, then it's recommended to use the home screen and device experience features described in this section.

On Android Enterprise devices, you can configure the Intune Managed Home Screen (MHS) app to control the home screen and device experience.

In this step, consider what end users are doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

The following scenarios are common for FLW:

- **Scenario 1: Device wide access with multiple apps**

  The devices are enrolled in Intune as **Android Enterprise dedicated devices**.

  Users have access to the apps and settings on the device. Using policy settings, you can restrict users from different features, such as debugging, system applications, and more.

  For this scenario, you want users to use specific apps, but don't want the device locked to only those apps.

  To configure devices for this scenario, you deploy the apps, and configure the apps using application configuration policies. Then, use device configuration policies to allow or block device features.

  To get started, use the following links:

  1. [Add apps to Intune](../apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.

  2. [Create app configuration policies](../apps/app-configuration-policies-overview.md) to configure app features. You can also add a JSON file with all the configuration settings you want.

  3. Create a device configuration restrictions profile that [allows or restricts features using Intune](../configuration/device-restrictions-android-for-work.md).

      In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Device restrictions** > **Device experience** > **Dedicated device** > **Kiosk mode**. Set it to **Not configured**:

      :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-not-configured.png" alt-text="Dedicated device is the enrollment profile type and kiosk mode is set to not configured in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-dedicated-device-kiosk-not-configured.png":::

- **Scenario 2: Locked screen device with pinned apps**

  The devices are enrolled in Intune as **Android Enterprise dedicated devices**.

  For this scenario, you install the Intune Managed Home Screen (MHS) app, which allows you to customize the managed device experience. You can pin one app or many apps, select a wallpaper, set icon positions, require a PIN, and more. This scenario is often used for **dedicated devices**, such as shared devices.

  **What you need to know**:

  - Only features added to the Managed Home Screen (MHS) are available to end users. So, you can restrict end users from accessing settings and other device features.
  - When you pin one app or pin many apps to the MHS, only those apps open. They're the only apps users can access.  
  - The MHS is the enterprise launcher you use. Don't install another enterprise launcher app.

  For more information on the MHS app on dedicated devices, go to the [How to setup Microsoft Managed Home Screen on Dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) blog post.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md), including the MHS app. When the apps are added, you create app policies that deploy the apps to the devices.

  2. Use a [device restrictions configuration profile](../configuration/device-restrictions-configure.md) to set the kiosk mode to multi-app, and select your apps. This step locks the device to only the apps you select:

      In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Device restrictions** > **Device experience** > **Dedicated device** > **Kiosk mode** > **Multi-app** > **Add**. Add the apps you want in multi-app kiosk mode:

      :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-multi-app.png" alt-text="Enrollment profile type is set to dedicated device, and kiosk mode is set to multi app in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-dedicated-device-kiosk-multi-app.png":::

  3. Configure the Microsoft Managed Home Screen (MHS) app using one of the following options:

      - **Option 1 - Device restrictions configuration profile**: In the same device restrictions configuration profile, configure the device features you want when in multi-app kiosk mode.

        For a list of settings you can configure, go to [Android Enterprise - Device experience settings](../configuration/device-restrictions-android-for-work.md#device-experience).

      - **Option 2 - App configuration policy**: The app configuration policy has more configuration settings than the device restrictions configuration profile. You can also add a JSON file with all the configuration settings you want.

        For more information, go to [Configure the Microsoft Managed Home Screen app](../apps/app-configuration-managed-home-screen-app.md).

- **Scenario 3: Single app kiosk**

  The devices are enrolled in Intune as **Android Enterprise dedicated devices**.

  This scenario is used on devices that have a single purpose, like scanning inventory.

  **What you need to know**:

  - A single app is assigned to the device. When the device starts, only this app opens. Users are locked to the single app and can't close the app, or do anything else on the device.
  - This option is more restrictive, as the device is dedicated to only run a single application.
  - An enterprise launcher isn't used.

  To configure these devices, you assign the app to the device. Then, you create a device configuration policy that sets the device to single app kiosk mode.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md). When the app is added, you create an app policy that deploys the app to the devices.
  2. Create a device configuration restrictions profile that [allows or restricts features using Intune](../configuration/device-restrictions-android-for-work.md):

      In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Device restrictions** > **Device experience** > **Dedicated device** > **Kiosk mode** and select **Single app**:

      :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-single-app.png" alt-text="Enrollment profile type is set to dedicated device, and the kiosk mode is set to single app in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-dedicated-device-kiosk-single-app.png":::

### Azure AD shared device mode for Android Enterprise dedicated devices

Azure AD shared device mode (SDM) is another option for **Android Enterprise dedicated device** enrollments.

Azure AD SDM offers an app and identity driven sign in/sign out experience, which improves the end user experience and productivity (less sign in prompts). It compliments **Scenario 1** and **Scenario 2** described at [Step 3 - Home screen and device experience (Android)](#step-3---home-screen-and-device-experience-android) (in this article).

For more information on Azure AD shared device mode (SDM), go to [Azure AD shared device mode for FLW](#azure-ad-shared-device-mode-for-flw) (in this article).

**What you need to know**:

- Android enrollment in Intune as a shared device and Azure AD SDM are complimentary. Android enrollment in Intune as a shared device doesn't depend on Azure AD SDM. Azure AD SDM is an option on top of the Intune shared device enrollment.

- Azure AD SDM is a feature of Azure AD. It's not an Intune feature. For more information on Azure AD SDM for Android Enterprise devices, go to:

  - [Shared device mode for Android devices](/azure/active-directory/develop/msal-android-shared-devices)
  - [Enroll Android Enterprise dedicated devices into Azure AD Shared device mode - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/enroll-android-enterprise-dedicated-devices-into-azure-ad-shared/ba-p/1820093) blog post
  - [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post

- For end users to have the full sign in/sign out experience, apps must support the Microsoft Authentication Library (MSAL). For more information, go to [Enable cross-app SSO on Android using MSAL](/azure/active-directory/develop/msal-android-single-sign-on).
::: zone-end

::: zone pivot="all,ios-ipados"
## iOS/iPadOS

iPad devices are a popular device type for frontline workers (FLW). The Shared iPad feature in Intune is designed for frontline workers.

iOS devices can also be used, but it's not common. For iOS FLW devices, it's recommended to use [Azure AD shared device mode](/azure/active-directory/develop/msal-ios-shared-devices) and Intune together. In Intune, you enroll the device and create a device restrictions configuration profile. In the profile, you can allow (or prohibit) specific apps, and can hide apps.

The following diagram shows the iOS/iPadOS options for frontline worker devices in Intune:

:::image type="content" source="./media/frontline-worker-overview/ios-ipados-flw-options.png" alt-text="Diagram that shows Apple iOS and iPadOS frontline worker scenario path in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-flw-options.png":::

> [!NOTE]
> For iPadOS devices, Conditional Access isn't supported for Shared iPad. For more information, go to [Overview of shared device solutions for iOS/iPadOS](../enrollment/device-enrollment-shared-ios.md).

Since iPads are a popular Apple device type for frontline workers (FLW), **this section focuses on iPad devices**.

iPads are used in different scenarios and industries, including in field operations, healthcare, aviation, warehouse, data entry, digital forms, and presentations.

For FLW iPad devices, there are two options available:

- **Shared iPad**
  OR
- **Azure AD shared device mode**

:::image type="content" source="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for iPadOS frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png":::

When using iPad devices for FLW, use the following information to help you decide which option is best for your organization.

For iPad devices, admins must pick one option - **Shared iPad** in Intune or **Azure AD shared device mode**. This decision impacts how you configure the device.

- **Shared iPad**

  Shared iPads are a feature in Intune, and are the recommended and preferred device type for frontline worker devices. These devices are shared among many users, such as in a hospital or school. Each user has their own profile and data, and they can sign in and out of the device.

  ✔️ If the device is an iPad, then use the Shared iPad feature in Intune. For more information on Shared iPads in Intune, go to [Shared iPad devices in Intune](../enrollment/device-enrollment-shared-ipad.md).

  ❌ If the device is an iOS device, then use Azure AD shared device mode. For more information, go to [Azure AD shared device mode for FLW](#azure-ad-shared-device-mode-for-flw) (in this article) and [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices).

- **Azure AD shared device mode**

  Azure AD shared device mode (SDM) is an option for iOS and iPadOS devices and uses the [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin). Azure AD SDM offers an app and identity driven sign in/sign out experience, which improves the end user experience and productivity (less sign in prompts). Azure AD shared device mode isn't supported with Shared iPad feature in Intune.

  For more information on Azure AD shared device mode (SDM), go to [Azure AD shared device mode for FLW](#azure-ad-shared-device-mode-for-flw) (in this article).

  When to use Azure AD SDM:

  ✔️ If the device is an iOS device, then use Azure AD shared device mode.

  ✔️ If the device is an iPad, then you can use Azure AD shared device mode **OR** Shared iPad in Intune.

  ❌ If you configured an iPad to be a Shared iPad in Intune, then don't use Azure AD shared device mode. It's not supported.

  For end users to have the full sign in/sign out experience, apps must support Azure AD SDM. For more information on Azure AD SDM and iOS/iPadOS devices, go to:

  - [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices)
  - [Set up automated device enrollment for shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md)

For a comparison of both options, go to [Shared iOS and iPadOS devices](../enrollment/device-enrollment-shared-ios.md).

> [!NOTE]
> There are other iOS/iPadOS enrollment options available. This article focuses on the enrollment options commonly used for FLW devices. For more information on all the iOS/iPadOS enrollment options, go to [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

### Shared iPads

Shared iPads are a feature in Intune. If you're not using Shared iPads, then skip this section.

This section focuses on Shared iPads used by frontline workers, including the decisions admins need to make, determining how the device is used, and configuring the home screen & device experience.

#### Step 1 - Use Automated Device Enrollment (ADE), enable Shared iPad, and choose a temporary session type (iPadOS)

For Shared iPad FLW devices, the first step is to create an **Automated Device Enrollment (ADE) profile**. ADE is the required enrollment option for Shared iPads. ADE syncs the devices from Apple Business Manager or Apple School Manager.

From an Intune perspective, you configure the enrollment profile and assign the profile to the device. When you create the enrollment profile for Shared iPads, you select the following features:

1. **Enroll without user affinity**: This option doesn't associate the devices with a specific user. This option is required for Shared iPads.
2. **Shared iPad**: This option enables Shared iPad on the device, and is required. It allows many users to sign in to the device.
3. **Require Shared iPad temporary session**: This setting determines if the Shared iPads are used for guest access. Your options:

    - **Guest access**

      **Yes** enables temporary sessions. Users sign in to the device as a guest. They don't enter a Managed Apple ID or password. All user data, sign in info, including browsing history, is deleted when the user signs out.

      For example, in healthcare, a medical patient is assigned a shared iPad to check in or fill out forms. When they're done, they sign out and all their local user data is deleted from the device. The next patient can then sign in to the device as a guest and use the device.

    - **Partitioned user access**

      Partitioned user access is the default behavior for Shared iPads. In Intune, **Not configured** uses this default behavior. Use this option when an iPad is used by many authenticated users at different times.

      Each user signs in to the device with their federated Azure AD credentials. User partitions ensure that each user's apps, data, and preferences are stored separately on the iPad. Only the same set of apps used across all device users support partitioned user access.

      When the user locks their profile, their data remains on the device in their own partition. Then, the device is ready for the next user to sign in and use the device.

      The number of users that can sign in also varies by the amount of storage on the device. So, it's recommended to plan accordingly and configure the enrollment profile to accommodate your needs.

The following image shows a sample Shared iPad enrollment policy in Intune that enables guest access:

:::image type="content" source="./media/frontline-worker-overview/shared-ipad-ade-enrollment-policy.png" alt-text="An Automated Device Enrollment (ADE) policy with Shared iPad enabled, and temporary sessions for Shared iPadOS enabled for frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/shared-ipad-ade-enrollment-policy.png":::

For more information on these features, and to get started, go to:

- [Set up automated device enrollment in Intune](../enrollment/device-enrollment-program-enroll-ios.md)
- [Set up Shared iPad in Intune](../enrollment/device-enrollment-shared-ipad.md)

#### Step 2 - Home screen layout and device experience (iPadOS)

Next, consider what end users do on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

In Intune, you can create device configuration profiles that configure the home screen and the apps that are shown. Specifically, you create a:

- **Device features** policy to configure the home screen layout and other settings you want to apply to the device:

  :::image type="content" source="./media/frontline-worker-overview/ios-ipados-device-features-home-screen-layout.png" alt-text="A device features policy with the home screen layout settings configured for iOS and iPadOS device in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-device-features-home-screen-layout.png":::

- **Device restrictions** policy to configure other device settings, such as using kiosk mode and other settings you want to apply to the device:

  :::image type="content" source="./media/frontline-worker-overview/ios-ipados-device-restrictions-kiosk.png" alt-text="A device restrictions policy with the device settings configured for iOS and iPadOS devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-device-restrictions-kiosk.png":::

  In this policy, you can also create a list of approved apps, prohibited apps, and hide some system apps. For more information on the settings you can configure, go to [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

For a list of the Shared iPad settings you can configure, go to [Configure settings for Shared iPads](../enrollment/device-enrollment-shared-ipad.md#configure-settings-for-shared-ipads).

For a list of all the device configuration settings, go to:

- [iOS and iPadOS device settings to use common features](../configuration/ios-device-features-settings.md)
- [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md)
::: zone-end

::: zone pivot="all,windows"
## Windows

Windows has different devices and cloud services that can be used for frontline workers. They're also used globally and in many industries.

You can use physical Windows devices or use Windows 365 Cloud PCs.

**Windows 365 Cloud PCs** are virtual machines that are hosted in the Windows 365 service, and are accessible from anywhere & from any device. They include a Windows desktop experience and are associated with a user. Basically, end users have their own PC in the cloud.

✔️ Windows 365 Cloud PCs are ideal for frontline workers that need a Windows desktop experience, but don't need a physical device. For example, a call center worker that needs access to a Windows desktop app.

These devices enroll in Intune, and are managed like any other device, including apps, configuration settings, and updates.

For more information on Windows 365 Cloud PCs, and to learn more, go to:

- [Windows 365 Cloud PCs overview - Enterprise](/windows-365/enterprise/overview)
- [Windows 365 Cloud PCs overview - Small & medium business](/windows-365/business/get-started-windows-365-business)

This section focuses on Windows devices used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

### Step 1 - Select your enrollment option (Windows)

The first step is to determine the enrollment platform that's best for your organization. For FLW devices using the Windows platform, you can use **Windows Autopilot** enrollment or use a **provisioning package**. This section focuses on these enrollment options.

# [Windows Autopilot](#tab/autopilot)

**Windows Autopilot** is the recommended option for FLW devices. You can ship the devices directly to the location without ever touching the devices. With self-deploying mode, users turn on the device, and the enrollment automatically starts.

✔️ If you have Azure AD Premium and you're getting new devices from an OEM, then use Windows Autopilot. You can use the Windows OEM version preinstalled on the devices to automatically enroll the devices. Other than turning on the device, no other end user interaction is required.

You can use Windows Autopilot on existing devices. When the existing devices are reset, the Windows Autopilot enrollment can automatically start.

❌ Windows Autopilot requires Azure AD Premium. If you don't have Azure AD Premium, then use a provisioning package. There are other Windows enrollment options available, but they're not commonly used for FLW devices.

For more information on Windows Autopilot, go to [Windows Autopilot overview](/mem/autopilot/windows-autopilot) and [Windows Autopilot self-deploying mode](/mem/autopilot/self-deploying).

# [Provisioning package](#tab/provpackage)

This option uses the Windows Configuration Designer (WCD) app to create a provisioning package (`.ppkg`). When you create the package, you configure the enrollment settings you want. Then, you make the package available to users on a USB drive or network location (including a SharePoint site).

✔️ If you don't have Azure AD Premium, then use a provisioning package. You can use the provisioning package to bulk enroll many devices. You can also use the provisioning package to enroll new and existing devices.

❌ If you have Azure AD Premium, then use Windows Autopilot. Windows Autopilot requires Azure AD Premium.

For more information on using a provisioning package with Intune, go to [Bulk enrollment for Windows devices](../enrollment/windows-bulk-enroll.md).

---

> [!NOTE]
> There are other Windows enrollment options available. This article focuses on the enrollment options commonly used for FLW devices. For more information on all the Windows enrollment options, go to [Enrollment guide: Enroll Windows client devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-windows.md).

### Step 2 - Shared device or user associated device (Windows)

The next decision is to determine if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are managed with Intune.

These features are configured using Intune device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

- **Shared device**

  **Shared PC** is a feature in Intune, and allows devices to be shared with many users, one user at a time. A user gets the device, completes their tasks, and gives the device to another user. End users sign in to these shared devices with their **Azure AD organization account** or a **guest account**. With this feature, you can delete account information and allow (or prevent) users from saving & viewing files locally.

  For example, shared Windows devices can be public computers in libraries, computer labs in schools & universities, shared workstations in offices, shared laptops in classrooms, and more.

  For more information on this feature, and to get started, go to:

  - [Shared PC or multi-user Windows devices in Intune](../configuration/shared-user-device-settings-windows.md)
  - [Shared PC or multi-user Windows devices in Intune - Settings list](../configuration/shared-user-device-settings.md)

- **User associated device**

  These devices have one user. This user associates the device with themselves, which happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Azure AD.

  These devices are used in FLW scenarios where the device is only used by that user. Some examples include personal computers for support staff, design computers for architects & graphic artists, and work-from-home setups.

### Step 3 - Device experience and kiosk (Windows)

This step is optional and depends on your business scenario. But, if these devices are shared by many users, then it's recommended to use the device experience features described in this section.

On Windows devices, you can configure the home screen and device experience. In this step, consider what frontline workers are doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

Some examples of kiosks include self-service terminals in airports, retail stores, government offices, and other public spaces. These devices allow users to do specific tasks, like check-in for flights, access information, or complete transactions.

These features are configured using device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

The following scenarios are common:

- **Scenario 1: Kiosk with one app or many apps**

  For this scenario, you configure the device as a kiosk, which allows you to customize the device experience.

  For example, you can use the device in a lobby so customers can see your product catalog. Or, use the device to show visual content as a digital sign. For more information, go to [Configure kiosks and digital signs on Windows desktop editions](/windows/configuration/kiosk-methods) (opens another Microsoft web site).

  You can pin one app or many apps, select a wallpaper, set icon positions, and more. This scenario is often used for dedicated devices, such as shared devices. You can create a Shared PC profile and configure it be a kiosk using the kiosk settings in Intune.

  **What you need to know**:

  - Only features added to the kiosk are available to end users. So, you can restrict end users from accessing settings and other device features.
  - When you pin one app or pin many apps to the kiosk, only those apps open. They're the only apps users can access. Users are locked to those apps, can't close the apps, or do anything else on the devices. This scenario is used on devices dedicated to a specific use, like airport terminals.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.
  2. Create a device configuration [kiosk profile](../configuration/kiosk-settings.md) and configure the [Windows kiosk profile - settings list](../configuration/kiosk-settings.md).

      The following example shows the kiosk profile settings for a single app. Make sure you add the app to Intune before you configure the kiosk profile.

      :::image type="content" source="./media/frontline-worker-overview/windows-kiosk-single-app.png" alt-text="The kiosk device configuration profile settings for a single app on Windows devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/windows-kiosk-single-app.png":::

      The following example shows the kiosk profile settings for multiple apps. Make sure you add the apps to Intune before you configure the kiosk profile.

      :::image type="content" source="./media/frontline-worker-overview/windows-kiosk-multi-app.png" alt-text="The kiosk device configuration profile settings for multiple apps on Windows devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/windows-kiosk-multi-app.png":::

- **Scenario 2: Device wide access with multiple apps**

  This scenario is a good scenario for Windows 365 Cloud PCs. Users have access to the apps and settings on the device. You can restrict users from different features, such as simple passwords, features in the Settings app, and more.

  This scenario also applies to physical devices. It expands the boundary of traditional frontline worker scenarios by also including knowledge workers.

  To configure devices for this scenario, you deploy the apps to the devices. Then, use device configuration policies to allow or block device features.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.
  2. Create a device configuration restrictions profile that [allows or restricts features using Intune](../configuration/device-restrictions-windows-10.md). There are hundreds of settings available for you to configure, including more in the [Settings Catalog](../configuration/settings-catalog.md).

      :::image type="content" source="./media/frontline-worker-overview/windows-device-restrictions.png" alt-text="All the device restrictions settings for Windows devices in Microsoft Intune.":::

::: zone-end

## Azure AD shared device mode for FLW

Azure AD shared device mode (SDM) is designed for frontline workers (FLW). It's an Azure AD feature that focuses on building apps so the apps can be used by many users on the same device. Users sign in/sign out of apps, have all their data removed, and have the device ready for the next user.

Some of the benefits of Azure AD SDM include:

- Azure AD SDM supports multiple users on devices designed for one user. Some mobile devices running Android and iOS are designed for single users. Most apps optimize their experience for a single user. Apps built with Azure AD SDM support multiple users on one device.

- Azure AD SDM does automatic single sign in and single sign out. Employees can sign in once and get single sign-on (SSO) to all apps that support Azure AD SDM, giving them faster access to information.

  This feature is good for organizations that use a set of apps in a device pool that's shared by employees. Devices can be immediately ready for use by the next employee with no access to the previous user's data.

- Apps built for Azure AD SDM use the Microsoft Authentication Library (MSAL) and the Microsoft Authenticator app. When a device is in shared device mode, and with (MSAL) and the Microsoft Authenticator app, Microsoft provides information to your app. This information allows the app to modify its behavior based on the state of the user on the device, which helps protect user data.

For more information on Azure AD SDM, go to [Overview of shared device mode](/azure/active-directory/develop/msal-shared-devices).

## More Microsoft services for FLW

**Microsoft 365 for frontline workers** is a licensing option that's designed for frontline worker scenarios. It's ideal for a mobile workforce that primarily interacts with customers and needs to stay connected to the rest of the organization. It interacts with other apps and services, including Microsoft Teams, Outlook, SharePoint, and more.

For more information and to get started, go to:

- [Get started with Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-overview)
- [Choose your scenarios for Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-choose-scenarios)

**Windows 365 Frontline** is a version of Windows 365 that provides a single license to provision some Cloud PC virtual machines. It can help organizations save costs. It's ideal for workers who share computing resources and don't require 24/7 devices, including users who are:

- On a rotation schedule
- Working across time zones and regions
- Part-time workers
- Contingent staff

For more information and to get started, go to:

- [Windows 365 Frontline)](https://www.microsoft.com/windows-365/frontline)
- [What is Windows 365 Frontline?](/windows-365/enterprise/introduction-windows-365-frontline)

## Next steps

- [Microsoft Intune securely manages identities, manages apps, and manages devices](what-is-intune.md)
- [Microsoft Intune planning guide](intune-planning-guide.md)
- [Migration guide: Set up or move to Microsoft Intune](deployment-guide-intune-setup.md)
