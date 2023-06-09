---
title: Get started with Frontline worker devices in Microsoft Intune
description: Learn how to manage frontline worker devices using Android and iOS/iPadOS devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 06/08/2023
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

# Frontline worker device management for Android and iPadOS devices in Microsoft Intune

A frontline worker (FLW) is a person that works in a critical or essential role. They're typically in direct contact with the public and customers. During a crisis or emergency, such as a pandemic or natural disaster, frontline workers are often at the forefront of the response effort, providing critical services and support. Some examples of frontline workers include healthcare, emergency responders, law enforcement, retail & food service, and transportation.

This article provides guidance on managing and configuring devices that play a key role in running business operations.

Frontline workers rely on process and/or devices to enable their productivity, like scanning concert tickets, medical patient wrist bands, and inventory scanning. If these devices fail, productivity and business can stop. These device types can be business or mission critical to operations.

This article applies to:

- Android
- iOS/iPadOS

## Android

Android devices are in almost every industry across the globe, including healthcare, aviation, manufacturing, and government. This section focuses on Android devices used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

Intune supports different enrollment options for Android devices, as shown in the following image:

:::image type="content" source="./media/frontline-worker-overview/android-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for Android frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-flw-enrollment-options.png":::

When using Android devices for frontline workers, use the following steps. These steps help you determine the best enrollment option and the best device management experience for you and your end users.

There are other Android enrollment options available. This article focuses on the enrollment options commonly used for FLW. For more information on all the Android enrollment options, go to [Enrollment guide: Enroll Android devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-android.md).

### Step 1 - Select your enrollment option (Android)

The first step is to determine the enrollment platform that's best for your organization and device needs. For FLW devices using the Android platform, the most common enrollment options are **Android Enterprise** and **Android Open Source Project (AOSP)**. This section focuses on these enrollment options.

- **Android Enterprise** enrollment devices require and use [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site). Your organization and/or your end users own these devices (BYOD). They're also used in countries/regions that don't block GMS.

  ✔️ If the device is GMS enabled and is in the [Android Enterprise recommended list](https://www.android.com/enterprise/recommended/) (opens Android's web site), then use Android Enterprise enrollment.

  ❌ If these devices are used in a country/region that blocks GMS, then Android Enterprise enrollment is not supported. Look into AOSP enrollment (provided devices are supported for AOSP management with Intune).

- **AOSP** devices don't offer or include Google Mobile Services (GMS). These devices:

  - Can be specialty devices, such as augmented or virtual reality devices.
  - Don't support GMS.
  - Are used in countries that block GMS.

  ✔️ If your devices meet these criteria, then use AOSP enrollment.

  ❌ If these devices must use GMS and don't meet these criteria, then use Android Enterprise enrollment.

  To learn more about AOSP, go to [About the Android Open Source Project](https://source.android.com/) (opens Android's web site).

> [!NOTE]
> For Android device administrator (DA), Google is deprecating and reducing features. It's recommended that you move to Android Enterprise or AOSP.

### Step 2 - Shared device or user associated device (Android)

The next decision is to determine if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are enrolled and managed with Intune.

- **Shared device**

  With shared devices, a user gets the device, completes their tasks, and gives the device to another user.

  When using shared devices:

  - Know what the device is doing and its use case. Android device manufacturers (OEMs) offer different devices, some may be specialty and others may be more generic.

    For example, there's device that's used for augmented or virtual reality. Typically, these specialty devices don't support GMS, which is a requirement for Android Enterprise enrollment. So, the natural enrollment path is AOSP.

  - If you're using Android Enterprise shared devices, then you can enroll your devices as **dedicated devices**. These devices use Google Mobile Services (GMS) and aren't associated with a single or specific user.

  - If you're using AOSP shared devices, then you can enroll your devices as **userless devices**. These devices don't use GMS and aren't associated with a single or specific user.

- **User associated device**

  These devices have one user. This user associates the device with themselves, which typically happens when the user signs in during the Intune enrollment process. The device is associated with the user's identity in Azure Active Directory (Azure AD).

  With user association:

  - If you're using Android Enterprise, then you can enroll your devices as **fully managed** devices. These devices have one user, and are used exclusively for organization work; not personal use.

  - If you're using AOSP, then you can enroll your devices as a **user-associated** device. Remember, these devices don't support Google Mobile Services (GMS).

### Step 3 - Home screen and device experience (Android)

On Android Enterprise devices, you can configure the home screen and device experience. This feature isn't available for AOSP devices.

In this step, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

The following scenarios describe some commonly used scenarios:

- **Scenario 1: Device wide access with multiple apps**

  The devices are enrolled in Intune as **dedicated devices**. Users have access to the apps and settings on the device. You can restrict users from different features, such as debugging, factory reset, and more.

  To configure devices for this scenario, you deploy the apps to the devices. Then, use device configuration policies to pin apps and allow or block device features.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. [Allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md)

      **??** Which settings apply to this scenario? I added the following screen shot, but not sure if this is the correct setting. These settings also mention MHS. ??

      :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-multi-app.png" alt-text="Screenshot that shows the dedicated device, kiosk mode, and multi app settings you select in a device configuration profile in Microsoft Intune.":::

- **Scenario 2: Locked screen device with pinned apps**

  For this scenario, you install the Intune Managed Home Screen (MHS), which allows you to customize managed device experience. You can pin one app or many apps, select a wallpaper, set icon positions, and more. This scenario is often used for **dedicated devices**, such as shared devices.

  What you need to know:

  - Only features added to the Managed Home Screen are available to end users. So, you can restrict end users from accessing settings and other device features.
  - When you pin one app or pin many apps to the MHS, only those apps open. They're the only apps users can access.  
  - The Managed Home Screen (MHS) is the enterprise launcher you use. Don't install another enterprise launcher app.

  For more information on the MHS on dedicated devices, go to the [How to setup Microsoft Managed Home Screen on Dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) blog post.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. [Configure the Microsoft Managed Home Screen app](../apps/app-configuration-managed-home-screen-app.md)

  > [!TIP]
  > If you're using this scenario, then configure the MHS using the app policy. Don't configure the MHS using a device configuration policy. The app policy has more configuration settings than the device configuration policy.

?? Are there scenarios where we recommend confgiuring the MHS using a device configuration policy? ??

- **Scenario 3: Single app kiosk**

  A single app is assigned to the device. When the device starts, only this app opens. Users are locked to the single app and can't close the app, or do anything else on the devices. This scenario is used on devices dedicated to a specific use, like scanning inventory.  

  What you need to know:

  - This option is more restrictive and doesn't allow admins to troubleshoot the devices.
  - An enterprise launcher isn't used.

  To configure these devices, you create a device configuration policy that sets the device to single app kiosk mode. Then, you assign the app to the device.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. Configure the device to be in [single app kiosk mode using a device configuration policy](../configuration/device-restrictions-android-for-work.md#device-experience):

      :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-single-app.png" alt-text="Screenshot that shows the dedicated device, kiosk mode, and single app settings you select in a device configuration profile in Microsoft Intune.":::

### Azure AD shared device mode for Android Enterprise dedicated devices

Azure AD shared device mode (SDM) is another option for Android, specifically Android Enterprise **dedicated device** enrollments. Azure AD SDM offers an app and identity driven sign-in/sign-out experience that compliments **Scenario 1** and **Scenario 2**.

Android enrollment as a shared device and Azure AD SDM are complimentary. For end users to have the full sign-in/sign-out experience, apps must support Azure AD SDM. Android enrollment as a shared device isn't dependent on Azure AD SDM. Azure AD SDM is an option on top of the Intune shared device enrollment.

For more information on Azure AD SDM, and to get started, go to:

- [Shared device mode for Android devices](/azure/active-directory/develop/msal-android-shared-devices)
- [Enroll Android Enterprise dedicated devices into Azure AD Shared device mode - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/enroll-android-enterprise-dedicated-devices-into-azure-ad-shared/ba-p/1820093) blog post
- [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post
- [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post

## iOS/iPadOS

iPad devices are a popular device type for frontline workers (FLW). iPads are used in different scenarios and industries, including in field operations, office, and warehouse.

This section focuses on iPad devices.

For FLW iPad devices, there are two options available - **Shared iPad** or **Azure AD shared device mode**, as shown in the following image:

:::image type="content" source="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for iPadOS frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png":::

When using iPad devices for FLW, use the following information to help you decide which option is best for your organization.

For iPad devices, admins must pick one option - **Shared iPad** or **Azure AD shared device mode**. This decision impacts how you configure the device.

- **Shared iPad**

  Shared iPads are a feature in Intune, and are the recommended and preferred device type for frontline worker devices. These devices are shared among many users, such as in a hospital or school. Each user has their own profile and data, and they can sign in and out of the device.

  ✔️ If the device is an iPad, then use the Shared iPad feature in Intune.

  ❌ If the device is an iOS device, then use Azure AD shared device mode.

  For more information on Shared iPads, go to [Shared iPad devices in Microsoft Intune](../enrollment/device-enrollment-shared-ipad.md).

- **Azure AD shared device mode**

  Azure AD shared device mode (SDM) is an option for iOS and iPadOS devices and uses the Microsoft Enterprise SSO plug-in for Apple devices. Azure AD SDM offers an app and identity driven sign-in/sign-out experience, which improves the end user experience and productivity (fewer sign-in prompts). Azure AD shared device mode isn't supported on Shared iPad.  

  When to use Azure AD SDM:

  ✔️ If the device is an iOS device, then use Azure AD shared device mode.

  ✔️ If the device is an iPad, then you can use Azure AD shared device mode. However, Shared iPad is also an option.

  ❌ If you configured an iPad to be a Shared iPad in Intune, then don't use Azure AD shared device mode. It's not supported.

  For end users to have the full sign-in/sign-out experience, apps must support Azure AD SDM. For more information on Azure AD SDM, and to get started, go to:

  - [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices)
  - [Set up automated device enrollment for shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md)

For a comparison of both options, go to [Shared iOS and iPadOS devices](../enrollment/device-enrollment-shared-ios.md).

There are other iOS/iPadOS enrollment options available. This article focuses on the enrollment options commonly used for FLW. For more information on all the iOS/iPadOS enrollment options, go to [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

### Shared iPads

This section focuses on Shared iPads used by frontline workers, including decisions admins need to make, determining how the device is used, and configuring the home screen & device experience.

If you're not using Shared iPads, then you can skip this section.

#### Step 1 - Use Automated Device Enrollment (ADE), enable Shared iPad, and choose a temporary session type (iPadOS)

For Shared iPad FLW devices, the first step is to create an **Automated Device Enrollment (ADE) profile**. ADE syncs the devices from Apple Business Manager or Apple School Manager.

From an Intune perspective, you configure the enrollment profile and assign the profile to the device. When you create the enrollment profile for Shared iPads, you select the following features:

1. **Enroll without user affinity**: This option doesn't associate the devices with a specific user. This option is required for Shared iPads.
2. **Shared iPad**: This option enables Shared iPad on the device, and is required. It allows many users to sign in.
3. **Require Shared iPad temporary session**: This setting determines if the Shared iPads will be used for guest access or partitioned user access.

    - **Guest access**

      **Yes** enables temporary sessions. Users sign in to the device as a guest. They don't enter a Managed Apple ID or password. All user data, login info, including browsing history, is deleted when the user signs out of the session.

      For example, in healthcare, a medical patient is assigned a shared iPad to check in or fill out forms.

    - **Partitioned user access**

      **Not configured** uses partitioned user access. Use this option when an iPad is used by many authenticated users at different times.

      Each user signs in to the device with their federated Azure AD credentials. User partitions ensure that each user's apps, data, and preferences are stored separately on the iPad. When the user signs out, their data remains on the device in their own partition. Then, the device is ready for the next user to sign in and use the device.

      The number of users that can sign in also varies by the amount of storage on the device. So, it's recommended to plan accordingly and configure the enrollment profile to accommodate your needs.

You Shared iPad enrollment policy looks similar to the following policy:

:::image type="content" source="./media/frontline-worker-overview/shared-ipad-ade-enrollment-policy.png" alt-text="Screenshot that shows Automated Device Enrollment (ADE) policy, Shared iPad enabled, and temporary sessions for Shared iPadOS frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/shared-ipad-ade-enrollment-policy.png":::

For more information on these features, and to get started, go to:

- [Set up automated device enrollment in Intune](../enrollment/device-enrollment-program-enroll-ios.md)
- [Set up Shared iPad in Intune](../enrollment/device-enrollment-shared-ipad.md)

#### Step 2 - Home screen layout and device experience (iPadOS)

Next, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

In Intune, you can create device configuration profiles that configure the home screen and run apps in kiosk mode.

For a list of the Shared iPad settings you can configure, go to [Configure settings for Shared iPads](../enrollment/device-enrollment-shared-ipad.md#configure-settings-for-shared-ipads).

For a list of all the device configuration settings, go to:

- [iOS and iPadOS device settings to use common features](../configuration/ios-device-features-settings.md)
- [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md)

## Windows

Windows has different devices and cloud services that can be used for frontline workers. They're also used globally and in many industries. This section focuses on Windows used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

You can use physical Windows devices or use Windows 365 cloud PCs:

- **Windows 365 cloud PCs** are virtual machines that are hosted in the Windows 365 service, and are accessible from anywhere, on from any device. They include a Windows desktop experience and are associated with a user. Basically, end users have their own PC in the cloud.

  ✔️ These devices are ideal for frontline workers that need a Windows desktop experience, but don't need a physical device. For example, a call center worker that needs access to a Windows desktop app.

  These devices enroll and Intune, and are managed like any other device, including configuration, apps, and updates.

  For more information on Windows 365 cloud PCs, and to get started, go to:

  - [Windows 365 Cloud PCs overview - Enterprise](/windows-365/enterprise/overview)
  - [Windows 365 Cloud PCs overview - Small & medium business](/windows-365/business/get-started-windows-365-business)

- Physical Windows devices

### Step 1 - Select your enrollment option (Windows)

The first step is to determine the enrollment platform that's best for your organization. For FLW devices using the Windows platform, you can use the **Windows automatic enrollment** or **Windows Autopilot** enrollment options. This section focuses on these enrollment options.

?? Are there other enrollment options for FLW? What enrollment option is available for orgs that don't have Azure AD Premium? GPO? ??

- **Windows Autopilot** is the recommended option for FLW devices. You can ship the devices directly to the location without ever touching the devices. Using self-deploying mode, users just turn on the device, and the enrollment automatically starts.

  ✔️ If you have have Azure AD Premium and you're getting new devices from an OEM, then use Windows Autopilot. You can use the Windows OEM version preinstalled on the devices to automatically enroll the devices. Other than turning on the device, no other end user interaction is required.

  ?? Existing devices ??

  ❌ Windows Autopilot requires Azure AD Premium.

- **Windows automatic enrollment** requires someone to sign in with their Azure AD organization account during the out-of-box experience (OOBE). When they do, the enrollment starts. ?? If the devices are local and need to be sent to another location, then an admin or end user with elevated permissions at that location can sign in. ??

  ✔️ If you have Azure AD Premium, and have new or existing devices, then Windows automatic enrollment is an option. For new devices purchased from an OEM, it's recommended to use **Windows Autopilot**.

  ❌ Windows automatic enrollment requires Azure AD Premium.

There are other Windows enrollment options available. This article focuses on the enrollment options commonly used for FLW. For more information on all the Windows enrollment options, go to [Enrollment guide: Enroll Windows client devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-windows.md).

### Step 2 - Shared device or user associated device (Windows)

The next decision is to determine if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are managed with Intune.

These features are configured using device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

- **Shared device**

  Shared devices allow one user at a time. A user gets the device, completes their tasks, and gives the device to another user. End users sign in to these shared devices with their **Azure AD organization account** or a **guest account**. With this feature, you can delete account information and allow (or prevent) users from saving & viewing files locally.

  ?? Need example ??

  ?? Add info on guest accounts and partitioned user access, like in iPadOS? ??

  For more information on this feature, and to get started, go to:

  - [Shared PC or multi-user Windows devices in Intune](../configuration/shared-user-device-settings-windows.md)
  - [Shared PC or multi-user Windows devices in Intune - Settings list](../configuration/shared-user-device-settings.md)

- **User associated device**

  These devices have one user. This user associates the device with themselves, which typically happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Azure AD.

  These devices are used in FLW scenarios where the device is only used by that user, such as ?? need example ??.

  ?? Is this valid for Windows FLW devices? If yes, I feel like we need more. I can say there are hundreds of policies that can be configured, but that seems like too much. How do we narrow down this scope for FLW? Or, maybe we move this text to **Step 3-Scenario 1**? ??

### Step 3 - Device experience and kiosk (Windows)

On Windows devices, you can configure the home screen and device experience. In this step, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

These features are configured using device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

The following scenarios describe some commonly used scenarios:

- **Scenario 1: Device wide access with multiple apps**

  Users have access to the apps and settings on the device. You can restrict users from different features, such as debugging, factory reset, and more.

  To configure devices for this scenario, you deploy the apps to the devices. Then, use device configuration policies to allow or block device features.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. [Apply features and settings on your devices using device profiles in Intune](../configuration/device-profiles.md)

?? This scenario is very broad and may not apply to FLW. ??

- **Scenario 2: Kiosk with one app or many apps**

  For this scenario, you configure the device as a kiosk, which allows you to customize the device experience. You can pin one app or many apps, select a wallpaper, set icon positions, and more. This scenario is often used for dedicated devices, such as shared devices. You can create a Shared PC profile and configure it be a kiosk using the kiosk settings.

  What you need to know:

  - Only features added to the kiosk are available to end users. So, you can restrict end users from accessing settings and other device features.
  - When you pin one app or pin many apps to the kiosk, only those apps open. They're the only apps users can access.
  - A single app is assigned to the device. When the device starts, only this app opens. Users are locked to the single app and can't close the app, or do anything else on the devices. This scenario is used on devices dedicated to a specific use, like scanning inventory.  

    What you need to know:

    - This option is more restrictive and doesn't allow admins to troubleshoot the devices.
    - An enterprise launcher isn't used.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. Create a [kiosk profile](../configuration/kiosk-settings.md) and configure the [Windows kiosk profile - settings list](../configuration/kiosk-settings.md).

  To configure these devices, you create a device configuration policy that sets the device to single app kiosk mode. Then, you assign the app to the device.

## Other MSFT services that do FLW

**Microsoft 365 for frontline workers** is a licensing option that designed for frontline worker scenarios. It's ideal for a mobile workforce that primarily interacts with customers that also needs to stay connected to the rest of the organization. It interacts with other apps and services, including Microsoft Teams, Outlook, SharePoint, and more.

For more information and to get started, go to:

- [Get started with Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-overview?view=o365-worldwide)
- [Choose your scenarios for Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-choose-scenarios)

**Windows 365 Frontline** is a version of Windows 365 that provides a single license to provision some Cloud PC virtual machines. The idea is help organizations save costs. It's ideal for workers who share computing resources and don't require 24/7 dedicated Cloud PCs, including users who are:

- On a rotation schedule
- Working across time zones and regions
- Part-time workers
- Contingent staff

For more information and to get started, go to:

- [Windows 365 Frontline)](https://www.microsoft.com/windows-365/frontline)
- [What is Windows 365 Frontline?](/windows-365/enterprise/introduction-windows-365-frontline)

## Next steps
