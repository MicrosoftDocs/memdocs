---
title: Get started with Frontline worker devices in Microsoft Intune
description: Learn how to manage frontline worker devices using Android, iOS/iPadOS, and Windows devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 06/22/2023
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
- iPadOS devices owned by the organization and enrolled in Intune
- Windows devices owned by the organization and enrolled in Intune

Frontline workers also rely on devices to enable their productivity, such as scanning concert tickets, scanning patient wrist bands in healthcare, or scanning inventory. If these devices fail, worker productivity and business operation can stop. Often, these types of devices can be categorized as mission critical.

The article provides guidance on managing and configuring frontline worker (FLW) devices using Intune. These devices play a key role in running business operations. And, they're an extension of the operator who uses and relies on the device to be productive for day-to-day business operations.

## Answers you need to know

When you're planning for FLW devices (including rugged devices), and how you'll manage them, there are questions you need to answer. These questions help you determine the best device management experience for you, your end users, and the needs of your organization.

- Will these devices shared?

  If yes, then <>
  If no, then <>

  ....I have flow charts created, however just answering these in case we don't use them...

  - With whom will the devices be shared with?  For example, will devices be part of a shared pool or assigned to users.  If part of a shared pool a shared device management strategy will apply.

- How will the end user become productive when they pick up a device to work with?  For example, do users need to launch an app and sign-in or is the expectation to have one sign-in where all applications automatically sign in afterwards.  If this is the case, then Azure AD Shared Device mode will help acheive this goal.
- How is user switching and hand-off of the device handled?  For example, if a shared device you may want users to sign out of apps and cradle the device for charging.  Again, a shared device mangement strategy will apply to this scenario.
- What environments will these devices be utilized in?  For example, environmental conditions may require specific device types such as rugged devices that are able to handle rough handling and adverse environments.

Once these questions are answered, the next stage is to identify the platforms you use and how the devices are used (their scenarios).

::: zone pivot="all,android"
## Android

Android devices are in almost every industry across the globe, including healthcare, aviation, construction, manufacturing, logistics, and government. They're commonly used by frontline workers in these industries.

This section focuses on Android devices used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

Intune supports different enrollment options for Android devices, as shown in the following image. For FLW devices using the Android platform, the most common enrollment options are **Android Enterprise** and **Android Open Source Project (AOSP)**.

:::image type="content" source="./media/frontline-worker-overview/android-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for Android frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-flw-enrollment-options.png":::

When you use Android devices for frontline workers, the steps in this section help you determine the best enrollment option and the best device management experience for you and your end users.

> [!NOTE]
> There are other Android enrollment options available. This section focuses on the enrollment options commonly used for FLW devices. For more information on all the Android enrollment options, go to [Enrollment guide: Enroll Android devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-android.md).

### Step 1 - Select your Intune enrollment option (Android)

The first step is to determine the Intune enrollment platform that's best for your organization and device needs. Remember, your organization owns these FLW devices. End users don't own these devices.

For FLW devices using the Android platform, you should use **Android Enterprise** or **Android Open Source Project (AOSP)** enrollment.

Make sure you know what the device is doing and its use case. Android device manufacturers (OEMs) offer different devices, some may be specialty and others may be more generic.

For example, devices that are used for augmented or virtual reality typically don't support GMS, which is a requirement for Android Enterprise enrollment. So, the natural enrollment path for these devices is AOSP.

# [Android Enterprise](#tab/ae)

**Android Enterprise** enrollment devices require and support [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site). These devices are also used in countries/regions that allow GMS.

✔️ If the device is GMS enabled and is in the [Android Enterprise recommended list](https://www.android.com/enterprise/recommended/) (opens Android's web site), then use Android Enterprise enrollment.

❌ If these devices are used in a country/region that blocks GMS, then Android Enterprise enrollment isn't supported. Instead, look into AOSP enrollment.

# [AOSP](#tab/aosp)

**AOSP** enrollment devices don't offer or include Google Mobile Services (GMS). These devices:

- Can be specialty devices, such as augmented or virtual reality devices.
- Don't support GMS.
- Are used in countries that block GMS.

✔️ If your devices meet these criteria, then use AOSP enrollment. Make sure your devices are supported for AOSP management with Intune. For a list of supported devices, go to [Supported operating systems and browsers in Intune - Android](supported-devices-browsers.md#android).

❌ If these devices support GMS and don't meet these criteria, then use Android Enterprise enrollment.

To learn more about AOSP, go to [About the Android Open Source Project](https://source.android.com/) (opens Android's web site).

---

> [!NOTE]
> For Android device administrator (DA), Google is deprecating and reducing features. If possible, it's recommended that you move to Android Enterprise or AOSP.

### Step 2 - Shared device or user associated device (Android)

The next decision is to decide if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are enrolled and managed with Intune.

- **Shared device - No user association**

  With shared devices, a user gets the device, completes their tasks, and gives the device to another user. Typically, these users manually sign into apps; they don't sign in to the device.

  When using shared devices:

  - If you're using Android shared devices and the devices support Android Enterprise enrollment, then you can enroll your devices as **dedicated devices**. These devices support Google Mobile Services (GMS) and aren't associated with a single or specific user.

    For more information on dedicated device enrollment, go to [Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

  - If you're using AOSP shared devices, then you can enroll your devices as **userless devices**. These devices typically don't support GMS and aren't associated with a single or specific user.

    For more information on AOSP userless enrollment, go to [Intune enrollment for AOSP corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md).

- **User associated device**

  These devices have one user. This user associates the device with themselves, which typically happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Azure Active Directory (Azure AD).

  With user association:

  - If you're using Android Enterprise, then you can enroll your devices as **fully managed** devices. These devices have one user, and are used exclusively for organization work; not personal use.

    For more information on fully managed enrollment, go to [Intune enrollment for Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

  - If you're using AOSP, then you can enroll your devices as a **user-associated** device. Remember, AOSP devices don't support Google Mobile Services (GMS). These devices have one user, and are used exclusively for organization work; not personal use.

    For more information on AOSP user-associated enrollment, go to [Intune enrollment for AOSP corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md).

### Step 3 - Home screen and device experience (Android)

This step is optional and depends on your business scenario. If these devices will be shared by many users, then it's recommended to use the home screen and device experience features in Intune.

On Android Enterprise devices, you can configure the Intune Manged Home Screen (MHS) launcher to control the home screen and device experience. This feature isn't available for AOSP devices.

In this step, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device. Remember, your organization owns these FLW devices. End users don't own these devices.

The following scenarios are common:

- **Scenario 1: Device wide access with multiple apps**

  The devices are enrolled in Intune as **dedicated devices** or **fully managed devices**. Users have access to the apps and settings on the device. Using policy settings, you can restrict users from different features, such as debugging, system applications, and more.

  To configure devices for this scenario, you deploy the apps to the devices using application configuration policies. Then, use device configuration policies to allow or block device features.

  > [!TIP]
  > There are two methods to configure the Intune Managed Home Screen:
  >
  > - Device configuration profile
  > - Application configuration policy
  >
  > Application configuration policies support a larger range of configuration option. So, use application configuration polices when you want more settings options. For more information on app configuration policies, go to [App configuration policies in Intune](../apps/app-configuration-policies-overview.md).

  To get started, use the following links:

  1. [Add apps to Intune](../apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.

      If you're using **dedicated devices** enrollment, then you might also need the Managed Home Screen (MHS) app. This requirement depends on the device configuration policy settings you use. For more information, see the next step.

  2. Create a device configuration restrictions policy that [allows or restricts features using Intune](../configuration/device-restrictions-android-for-work.md).

      If you're using **dedicated devices** enrollment with multi-app kiosk mode, then also add the Managed Home Screen (MHS) app.  If you're using **dedicated devices** enrollment with kiosk mode not configured, then MHS isn't required or used. Multi-app is still used, but it's not locked into the MHS.

      - If you use **dedicated devices** enrollment and want to lock end users to only specific apps, then use the **Device experience** > **Dedicated device** > **Kiosk mode** > **Multi-app** settings.

        This scenario requires the Managed Home Screen (MHS) app. You configure the MHS app using the device configuration policy settings you enter. For this scenario, don't configure the MHS using an app policy.

        :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-multi-app.png" alt-text="Screenshot that shows the dedicated device, kiosk mode, and multi app settings you select in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-dedicated-device-kiosk-multi-app.png":::

      - If you use **dedicated devices** enrollment, want users to use specific apps, but don't want the device locked to only those apps, then use **Device experience** > **Dedicated device** > **Kiosk mode** > **Not configured**. This scenario doesn't use the MHS app.

        :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-not-configured.png" alt-text="Screenshot that shows the dedicated device and the kiosk mode not configured in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-dedicated-device-kiosk-not-configured.png":::

      - If you use **Fully managed** enrollment, then use the **Device experience** > **Fully managed** settings:

        :::image type="content" source="./media/frontline-worker-overview/android-fully-managed-kiosk.png" alt-text="Screenshot that shows the fully managed device settings you select in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-fully-managed-kiosk.png":::

- **Scenario 2: Locked screen device with pinned apps**

  The devices are enrolled in Intune as **dedicated devices**.

  For this scenario, you install the Intune Managed Home Screen (MHS) app, which allows you to customize the managed device experience. You can pin one app or many apps, select a wallpaper, set icon positions, require a PIN, and more. This scenario is often used for **dedicated devices**, such as shared devices.

  **What you need to know**:

  - Only features added to the Managed Home Screen (MHS) are available to end users. So, you can restrict end users from accessing settings and other device features.
  - When you pin one app or pin many apps to the MHS, only those apps open. They're the only apps users can access.  
  - The MHS is the enterprise launcher you use. Don't install another enterprise launcher app.

  For more information on the MHS on dedicated devices, go to the [How to setup Microsoft Managed Home Screen on Dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) blog post.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md). When the apps are added, including the MHS app, you create app policies that deploy the apps to the devices.
  2. [Configure the Microsoft Managed Home Screen (MHS) app](../apps/app-configuration-managed-home-screen-app.md).

      In this scenario, configure the MHS app using the app policy. Don't configure the MHS using a device configuration policy. The app policy has more configuration settings than the device configuration policy.

- **Scenario 3: Single app kiosk**

  The devices are enrolled in Intune as **dedicated devices**. This scenario is used on devices that have a single purpose, like scanning inventory.

  A single app is assigned to the device. When the device starts, only this app opens. Users are locked to the single app and can't close the app, or do anything else on the device.

  **What you need to know**:

  - This option is more restrictive, as the device is dedicated to only run a single application.
  - An enterprise launcher isn't used.

  To configure these devices, you assign the app to the device. Then, you create a device configuration policy that sets the device to single app kiosk mode.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md). When the app is added, you create an app policy that deploys the app to the devices.
  2. Create a device configuration restrictions policy that [allows or restricts features using Intune](../configuration/device-restrictions-android-for-work.md). Use the **Device experience** > **Dedicated device** > **Kiosk mode** settings:

      :::image type="content" source="./media/frontline-worker-overview/android-dedicated-device-kiosk-single-app.png" alt-text="Screenshot that shows the dedicated device, kiosk mode, and single app settings you select in an Android Enterprise device configuration profile in Microsoft Intune." lightbox="./media/frontline-worker-overview/android-dedicated-device-kiosk-single-app.png":::

### Azure AD shared device mode for Android Enterprise dedicated devices

Azure AD shared device mode (SDM) is another option for Android, specifically Android Enterprise **dedicated device** enrollments.

Azure AD SDM offers an app and identity driven sign-in/sign-out experience, which improves the end user experience and productivity (fewer sign-in prompts). It compliments **Scenario 1** and **Scenario 2** described at [Step 3 - Home screen and device experience (Android)](#step-3---home-screen-and-device-experience-android) (in this article).

For more information on Azure AD shared device mode (SDM), go to [Azure AD shared device mode for FLW](#azure-ad-shared-device-mode-for-flw) (in this article).

**What you need to know**:

- Android enrollment as a shared device and Azure AD SDM are complimentary. Android enrollment as a shared device isn't dependent on Azure AD SDM. Azure AD SDM is an option on top of the Intune shared device enrollment.

- Azure AD SDM is a feature of Azure AD. It's not an Intune feature. For more information on Azure AD SDM for Android Enterprise devices, go to:

  - [Shared device mode for Android devices](/azure/active-directory/develop/msal-android-shared-devices)
  - [Enroll Android Enterprise dedicated devices into Azure AD Shared device mode - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/enroll-android-enterprise-dedicated-devices-into-azure-ad-shared/ba-p/1820093) blog post
  - [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post
  - [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post
::: zone-end

::: zone pivot="all,ios-ipados"
## iOS/iPadOS

iPad devices are a popular device type for frontline workers (FLW). iPads are used in different scenarios and industries, including in field operations, healthcare, aviation, warehouse, data entry, digital forms, and presentations.

**This section focuses on iPad devices**.

For FLW iPad devices, there are two options available - **Shared iPad** or **Azure AD shared device mode**, as shown in the following image:

:::image type="content" source="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for iPadOS frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png":::

When using iPad devices for FLW, use the following information to help you decide which option is best for your organization.

For iPad devices, admins must pick one option - **Shared iPad** or **Azure AD shared device mode**. This decision impacts how you configure the device.

- **Shared iPad**

  Shared iPads are a feature in Intune, and are the recommended and preferred device type for frontline worker devices. These devices are shared among many users, such as in a hospital or school. Each user has their own profile and data, and they can sign in and out of the device.

  ✔️ If the device is an iPad, then use the Shared iPad feature in Intune. For more information on Shared iPads in Intune, go to [Shared iPad devices in Intune](../enrollment/device-enrollment-shared-ipad.md).

  ❌ If the device is an iOS device, then use Azure AD shared device mode. For more information, go to [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices).

- **Azure AD shared device mode**

  Azure AD shared device mode (SDM) is an option for iOS and iPadOS devices and uses the Microsoft Enterprise SSO plug-in for Apple devices. Azure AD SDM offers an app and identity driven sign-in/sign-out experience, which improves the end user experience and productivity (fewer sign-in prompts). Azure AD shared device mode isn't supported on Shared iPad.  

  For more information on Azure AD shared device mode (SDM), go to [Azure AD shared device mode for FLW](#azure-ad-shared-device-mode-for-flw) (in this article).

  When to use Azure AD SDM:

  ✔️ If the device is an iOS device, then use Azure AD shared device mode.

  ✔️ If the device is an iPad, then you can use Azure AD shared device mode **OR** Shared iPad in Intune.

  ❌ If you configured an iPad to be a Shared iPad in Intune, then don't use Azure AD shared device mode. It's not supported.

  For end users to have the full sign-in/sign-out experience, apps must support Azure AD SDM. For more information on Azure AD SDM and iOS/iPadOS devices, go to:

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
3. **Require Shared iPad temporary session**: This setting determines if the Shared iPads are used for guest access.

    - **Guest access**

      **Yes** enables temporary sessions. Users sign in to the device as a guest. They don't enter a Managed Apple ID or password. All user data, login info, including browsing history, is deleted when the user signs out.

      For example, in healthcare, a medical patient is assigned a shared iPad to check in or fill out forms. When they're done, they sign out and all their local user data is deleted from the device. The next patient can then sign in to the device as a guest and use the device.

    - **Partitioned user access**

      Partitioned user access is the default behavior for Shared iPads. In Intune, **Not configured** uses this default behavior. Use this option when an iPad is used by many authenticated users at different times.

      Each user signs in to the device with their federated Azure AD credentials. User partitions ensure that each user's apps, data, and preferences are stored separately on the iPad. Only the same set of apps across all users support partitioned user access.

      When the user locks their profile, their data remains on the device in their own partition. Then, the device is ready for the next user to sign in and use the device.

      The number of users that can sign in also varies by the amount of storage on the device. So, it's recommended to plan accordingly and configure the enrollment profile to accommodate your needs.

The following image shows a sample Shared iPad enrollment policy that enables guest access:

:::image type="content" source="./media/frontline-worker-overview/shared-ipad-ade-enrollment-policy.png" alt-text="Screenshot that shows Automated Device Enrollment (ADE) policy, Shared iPad enabled, and temporary sessions for Shared iPadOS frontline worker devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/shared-ipad-ade-enrollment-policy.png":::

For more information on these features, and to get started, go to:

- [Set up automated device enrollment in Intune](../enrollment/device-enrollment-program-enroll-ios.md)
- [Set up Shared iPad in Intune](../enrollment/device-enrollment-shared-ipad.md)

#### Step 2 - Home screen layout and device experience (iPadOS)

Next, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

In Intune, you can create device configuration profiles that configure the home screen and the apps that are shown. Specifically, you create a:

- **Device features** policy to configure the home screen layout and other settings you want to apply to the device:

  :::image type="content" source="./media/frontline-worker-overview/ios-ipados-device-features-home-screen-layout.png" alt-text="Screenshot that shows a device features policy with the home screen layout settings for iOS and iPadOS device in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-device-features-home-screen-layout.png":::

- **Device restrictions** policy to configure other device settings, such as using kiosk mode and other settings you want to apply to the device:

  :::image type="content" source="./media/frontline-worker-overview/ios-ipados-device-restrictions-kiosk.png" alt-text="Screenshot that shows a device restrictions policy with the device settings for iOS and iPadOS device in Microsoft Intune." lightbox="./media/frontline-worker-overview/ios-ipados-device-restrictions-kiosk.png":::

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

For more information on Windows 365 Cloud PCs, and to get started, go to:

- [Windows 365 Cloud PCs overview - Enterprise](/windows-365/enterprise/overview)
- [Windows 365 Cloud PCs overview - Small & medium business](/windows-365/business/get-started-windows-365-business)

This section focuses on Windows devices used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

### Step 1 - Select your enrollment option (Windows)

The first step is to determine the enrollment platform that's best for your organization. For FLW devices using the Windows platform, you can use **Windows Autopilot** enrollment or use **provisioning package**. This section focuses on these enrollment options.

# [Windows Autopilot](#tab/autopilot)

**Windows Autopilot** is the recommended option for FLW devices. You can ship the devices directly to the location without ever touching the devices. With self-deploying mode, users just turn on the device, and the enrollment automatically starts.

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

These features are configured using device configuration profiles. When the profile has the settings you want, you assign the profile to the devices. The profile can be deployed during Intune enrollment.

- **Shared device**

  Shared devices allow one user at a time. A user gets the device, completes their tasks, and gives the device to another user. End users sign in to these shared devices with their **Azure AD organization account** or a **guest account**. With this feature, you can delete account information and allow (or prevent) users from saving & viewing files locally.

  For example, shared Windows devices can be public computers in libraries, computer labs in schools & universities, shared workstations in offices, shared laptops in classrooms, and more.

  For more information on this feature, and to get started, go to:

  - [Shared PC or multi-user Windows devices in Intune](../configuration/shared-user-device-settings-windows.md)
  - [Shared PC or multi-user Windows devices in Intune - Settings list](../configuration/shared-user-device-settings.md)

- **User associated device**

  These devices have one user. This user associates the device with themselves, which happens when the user signs in during the Intune enrollment. The device is associated with the user's identity in Azure AD.

  These devices are used in FLW scenarios where the device is only used by that user. Some examples include personal computers for support staff, design computers for architects & graphic artists, and work-from-home setups.

### Step 3 - Device experience and kiosk (Windows)

This step is optional and depends on your business scenario. But, if these devices will be shared by many users, then it's recommended to utilize the device experience features in Intune.

On Windows devices, you can configure the home screen and device experience. In this step, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

Some examples of kiosks include self-service terminals in airports, retail stores, government offices, and other public spaces. These devices allow users to do specific tasks, like checking in for flights, accessing information, or completing transactions.

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
  2. Create a [kiosk profile](../configuration/kiosk-settings.md) and configure the [Windows kiosk profile - settings list](../configuration/kiosk-settings.md).

      The following example shows the kiosk profile settings for a single app. Make sure you add the app to Intune before you configure the kiosk profile.

      :::image type="content" source="./media/frontline-worker-overview/windows-kiosk-single-app.png" alt-text="Screenshot that shows the kiosk device configuration profile settings for a single app on Windows devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/windows-kiosk-single-app.png":::

      The following example shows the kiosk profile settings for multiple apps. Make sure you add the apps to Intune before you configure the kiosk profile.

      :::image type="content" source="./media/frontline-worker-overview/windows-kiosk-multi-app.png" alt-text="Screenshot that shows the kiosk device configuration profile settings for multiple apps on Windows devices in Microsoft Intune." lightbox="./media/frontline-worker-overview/windows-kiosk-multi-app.png":::

- **Scenario 2: Device wide access with multiple apps**

  This is a good scenario for Windows 365 Cloud PCs. Users have access to the apps and settings on the device. You can restrict users from different features, such as simple passwords, features in the Settings app, and more.

  This scenario also applies to physical devices. It expands the boundary of traditional frontline worker scenarios by also including knowledge workers.

  To configure devices for this scenario, you deploy the apps to the devices. Then, use device configuration policies to allow or block device features.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md). When the apps are added, you create app policies that deploy the apps to the devices.
  2. Create a device configuration restrictions policy that [allows or restricts features using Intune](../configuration/device-restrictions-windows-10.md). There are hundreds of settings available for you to configure.

      :::image type="content" source="./media/frontline-worker-overview/windows-device-restrictions.png" alt-text="Screenshot that shows the device restrictions settings for Windows devices in Microsoft Intune.":::

::: zone-end

## Azure AD shared device mode for FLW

You may be trying to decide if Azure AD shared device mode (SDM) is the correct approach for your organization. Azure AD SDM enables the following scenarios.

- **Support multiple users on devices designed for one user**

  Mobile devices running Android and iOS ere designed for single users. Most apps optimize their experience for a single user. Part of this optimized experience enables single sign-on (SSO) across applications and keeps users signed in on their device. When a user removes their account from an application, the app typically doesn't consider it a security-related event. So, many apps keep a user's credentials for quick sign-in. You may have experienced this behavior yourself when you've deleted an application from your mobile device. You reinstall it, and find you're still signed in to the app.

- **Automatic single sign-in and single sign-out**

  To allow an organization's employees to use its apps across a pool of devices shared by those employees, developers need to enable the opposite experience. Employees should be able to pick a device from the pool and do a single gesture to "make it theirs" during their shift. At the end of their shift, they should do another gesture to sign out globally on the device, with all their personal and company information removed so they can return it to the device pool. Furthermore, if an employee forgets to sign out, the device should be automatically signed out at the end of their shift and/or after a period of inactivity.

For more information on Azure AD SDM, go to [Overview of shared device mode](/azure/active-directory/develop/msal-shared-devices).

- Android stated: For end users to have the full sign-in/sign-out experience, apps must support the Microsoft Authentication Library (MSAL).
- iOS states: For end users to have the full sign-in/sign-out experience, apps must support Azure AD SDM.

## Other MSFT services that do FLW

**Microsoft 365 for frontline workers** is a licensing option that's designed for frontline worker scenarios. It's ideal for a mobile workforce that primarily interacts with customers that also needs to stay connected to the rest of the organization. It interacts with other apps and services, including Microsoft Teams, Outlook, SharePoint, and more.

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
