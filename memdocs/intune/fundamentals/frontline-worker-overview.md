---
title: Get started with Frontline worker devices in Microsoft Intune
description: Learn how to manage frontline worker devices using Android and iOS/iPadOS devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 05/31/2023
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

Frontline workers rely on process and/or devices to enable their productivity, like scanning concert tickets, medical patient wrist bands, and inventory. If these devices fail, productivity and business can stop. These device types can be business or mission critical to operations.

This article applies to:

- Android
- iOS/iPadOS

## Android

Android devices are in almost every industry across the globe, including healthcare, aviation, manufacturing, and government. This section focuses on Android devices used by frontline workers. It includes decisions admins need to make, including determining how the device is used, and configuring the home screen & device experience.

---
**??**  Is the following paragraph needed? It's kind of confusing. ??

Often, a comparison of management capability enters the discussion and can lead to a checkbox exercise where organizations look at the incumbent solution and compare it to the solution of interest.  Having worked with 1000s of customers, this may lead to a biased form of mindset.  For example, x solution does foo where y solution does bar. However the questions that needs to be answered is, regardless of the haw, is the outcome the same?  It's a matter of disjoining the "how" vs the end result.

Android management is no different and this is where Intune enters the discussion.

---

Intune supports different enrollment options for Android devices, as shown in the following image:

:::image type="content" source="./media/frontline-worker-overview/android-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for Android frontline worker devices in Microsoft Intune.":::

When using Android devices for frontline workers, use the following steps. These steps help you determine the best enrollment option and the best device management experience for you and your end users.

There are other Android enrollment options available. This article focuses on the enrollment options commonly used for FLW. For more information on all the Android enrollment options, go to [Enrollment guide: Enroll Android devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-android.md).

### Step 1 - Select your enrollment platform

The first step is to determine the enrollment platform that's best for your organization and device needs. For FLW devices using the Android platform, the most common enrollment options are **Android Enterprise** and **Android Open Source Project (AOSP)**. This section focuses on these enrollment options.

- **Android Enterprise** enrollment devices require and use [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site). Your organization and/or your end users own these devices (BYOD). They're also used in countries/regions that don't block GMS.

  ✔️ If the device is GMS enabled and is in the [Android Enterprise recommended list](https://www.android.com/enterprise/recommended/) (opens Android's web site), then use Android Enterprise enrollment.

  ❌ If these devices are used in a country/region that blocks GMS, then don't use this enrollment option. Use AOSP.

- **AOSP** devices don't offer or include Google Mobile Services (GMS). These devices:

  - Can be specialty devices, such as augmented or virtual reality devices.
  - Don't support GMS.
  - Are used in countries that block GMS.

  ✔️ If your devices meet these criteria, then use AOSP enrollment.

  ❌ If these devices must use GMS and don't meet these criteria, then use Android Enterprise enrollment.

  To learn more about AOSP, go to [About the Android Open Source Project](https://source.android.com/) (opens Android's web site).

> [!NOTE]
> For Android device administrator (DA), Google is deprecating and reducing features. It's recommended that you move to Android Enterprise or AOSP.

### Step 2 - Shared device or user associated device

The next decision is to determine if the devices are shared with many users or assigned to a single user. This decision depends on your business needs and the end user requirements. It also impacts how these devices are enrolled and managed with Intune.

- **Shared device**

  With shared devices, a user gets the device, completes their tasks, and gives the device to another user. Then, the process repeats.

  When using shared devices:

  - Know what the device is doing and its use case. Android device manufacturers (OEMs) offer different devices, some may be specialty and others may be more generic.

    For example, there's device that's used for augmented or virtual reality. Typically, these specialty devices don't support GMS, which is a requirement for Android Enterprise enrollment. So, the natural enrollment path is AOSP.

  - If you're using Android Enterprise shared devices, then you can enroll your devices as **dedicated devices**. These devices use Google Mobile Services (GMS) and aren't associated with a single or specific user.

  - If you're using AOSP shared devices, then you can enroll your devices as **userless devices**. These devices don't use GMS and aren't associated with a single or specific user.

- **User associated device**

  These devices have one user. This user associates the device with themselves, which typically happens when the user signs in during the Intune enrollment process. The device is associated with the user's identity in Azure Active Directory (Azure AD).

  With user association:

  - If you're using Android Enterprise, then you can enroll your devices as **fully managed** devices. These devices have one user, and are used exclusively for organization work; not personal use.

  - If you're using AOSP, then you can enroll your devices as a **user-associated** device. Remember, these devices don't use Google Mobile Services (GMS).

### Step 3 - Home screen and device experience

So far, you selected the enrollment platform and device type. Next, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

The following scenarios describe some commonly used scenarios:

- **Scenario 1: Device wide access with multiple apps**

  The device is enrolled in Intune as a **fully managed** device. Users have access to the apps and settings on the device. You can restrict users from different features, such as debugging, factory reset, and more.

  To configure devices for this scenario, you deploy the apps to the devices, and then use device configuration policies to allow or block device features.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. [Allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md)

  **??** I assumed this scenario is meant for fully managed. ??

  **??** What about Microsoft Launcher app? If it doesn't apply to this scenario, we should state that info and why. ??

- **Scenario 2: Locked screen device with multiple pinned apps**

  For this scenario, you install an enterprise launcher, which allows you to customize managed device home screens. You can pin apps, select a wallpaper, set icon positions, and more. This scenario is often used for **dedicated devices**, such as kiosks.

  Only features added to the enterprise launcher are available to end users. So, you can restrict end users from accessing settings and other device features.

  Intune uses the Managed Home Screen (MHS) for the enterprise launcher. You don't need to install another enterprise launcher app. Using the MHS, you pin 1 app or several apps.

  For more information on the MHS on dedicated devices, go to the [How to setup Microsoft Managed Home Screen on Dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) blog post.

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. [Configure the Microsoft Managed Home Screen app](../apps/app-configuration-managed-home-screen-app.md)

  > [!TIP]
  > If you're using this scenario, then configure the MHS using the app policy. Don't configure the MHS using a device configuration policy. The app policy has more configuration settings than the device configuration policy.

- **Scenario 3: Locked screen device with one pinned app** 

  **??** This whole scenario. I copied the text from scenario 2, but what's the other solution, besides MHS? ??

  In this scenario, a single app is opened and it's the only app users can access. This is often used for kiosk devices.

  You can use the Managed Home Screen (MHS) for the enterprise launcher. You don't need to install another enterprise launcher app. Using the MHS, you pin 1 app.

  **??** The difference is that the single app can be closed in **Scenario 2** but not the launcher thus still restricting the end user from accessing settings.??

  To get started, use the following links:

  1. [Add apps to Microsoft Intune](../apps/apps-add.md)
  2. [Configure the Microsoft Managed Home Screen app](../apps/app-configuration-managed-home-screen-app.md)

  > [!TIP]
  > If you're using this scenario, then configure the MHS using the app policy. Don't configure the MHS using a device configuration policy. The app policy has more configuration settings than the device configuration policy.
  > **??** Does this tip still apply to this scenario? In the word doc, it says to use a device config profile for scenario 3. If there's another option, we can add that too. ??

[Android Enterprise device experience settings on organization owned devices](../configuration/device-restrictions-android-for-work.md#device-experience)

Below are a few links to help you get started on your journey with scenario #2 as #1 and #3 are configuration settings within Intune device configuration profiles: 

### Azure AD shared device mode for Android Enterprise dedicated devices

Azure AD shared device mode (SDM) is another option for Android, specifically Android Enterprise **dedicated device** enrollments. Azure AD SDM offers an app and identity driven sign-in/sign-out experience that compliments **Scenario 1**, **Scenario 2**, and potentially **Scenario 3** (if MHS is used with a single app).

Android enrollment as a shared device and Azure AD SDM are complimentary. For end users to have the full sign-in/sign-out experience, apps must support Azure AD SDM. Android enrollment as a shared device isn't dependent on Azure AD SDM. Azure AD SDM is an option on top of the Intune shared device enrollment.

For more information on Azure AD SDM, and to get started, go to:

- [Shared device mode for Android devices](/azure/active-directory/develop/msal-android-shared-devices)
- [Enroll Android Enterprise dedicated devices into Azure AD Shared device mode - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/enroll-android-enterprise-dedicated-devices-into-azure-ad-shared/ba-p/1820093) blog post
- [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post
- [Intune supports sign out for apps not optimized with Azure AD shared device mode on AE 9+ - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/endpoint-manager-supports-sign-out-for-apps-not-optimized-with/ba-p/3034398) blog post

### What about?

- OEMConfig
- Zebra

## iOS/iPadOS

iPad devices are a popular device type for frontline workers (FLW). iPads are used in different scenarios and industries, including in the field, office, and warehouse.

It's more common to use iPad devices than iOS devices for FLW scenarios. This section focuses on iPad devices.

For FLW iPad devices, there are two options available - **Shared iPad** or **Azure AD shared device mode**, as shown in the following image:

:::image type="content" source="./media/frontline-worker-overview/ios-ipados-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for iPadOS frontline worker devices in Microsoft Intune.":::

When using iPad devices for FLW, use the following information to help you decide which option is best for your organization.

For iPad devices, admins must pick one option - **Shared iPad** or **Azure AD shared device mode**. This decision impacts how you configure the device.

- **Shared iPad**

  Shared iPads are a feature in Intune, and are the recommended and preferred device type for frontline worker devices. These devices are shared among many users, such as in a hospital or school. Each user has their own profile and data, and they can sign in and out of the device.

  ✔️ If the device is an iPad, then use the Shared iPad feature in Intune.

  ❌ If the device is an iOS device, then use Azure AD shared device mode.

  For more information on Shared iPads, go to [Shared iPad devices in Microsoft Intune](../enrollment/device-enrollment-shared-ipad.md).

  **??** Should we say anything about user affinity? ??

- **Azure AD shared device mode**

  Azure AD shared device mode (SDM) is an option for iOS and iPadOS devices and uses the Microsoft Enterprise SSO plug-in for Apple devices. Azure AD SDM offers an app and identity driven sign-in/sign-out experience, which improves the end user experience and productivity (fewer sign-in prompts). Azure AD shared device mode isn't supported on Shared iPad.  

  When to use Azure AD SDM:

  ✔️ If the device is an iOS device, then use Azure AD shared device mode.

  ✔️ If the device is an iPad, then you can use Azure AD shared device mode. However, Shared iPad is the preferred option for iPad devices.

  ❌ If you configured an iPad to be a Shared iPad in Intune, then don't use Azure AD shared device mode. It's not supported.

  For end users to have the full sign-in/sign-out experience, apps must support Azure AD SDM. For more information on Azure AD SDM, and to get started, go to:

  - [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices)
  - [Set up automated device enrollment for shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md)

For a comparison of both options, go to [Shared iOS and iPadOS devices](../enrollment/device-enrollment-shared-ios.md).

There are other iOS/iPadOS enrollment options available. This article focuses on the enrollment options commonly used for FLW. For more information on all the iOS/iPadOS enrollment options, go to [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

### Shared iPads

This section focuses on Shared iPads used by frontline workers, including decisions admins need to make, determining how the device is used, and configuring the home screen & device experience.

If you're not using Shared iPads, then you can skip this section.

#### Step 1 - Use Automated Device Enrollment (ADE)

For Shared iPad FLW devices, the first step is to enroll devices using **Automated Device Enrollment (ADE) without user affinity**. ADE syncs the devices from Apple Business Manager or Apple School Manager.

**??** Is this the correct first step? Do admins configure an ADE enrollment policy *and* a Shared iPad enrollment policy? Or, do they set up Shared iPad as the enrollment option? Maybe Shared iPad enrollment uses ADE 'behind-the-scenes'? ??

From an Intune perspective, you configure the enrollment profile and assign the profile to the device.

For more information on ADE enrollment, and to get started, go to [Set up automated device enrollment in Intune](../enrollment/device-enrollment-program-enroll-ios.md).

#### Step 2 - Guest access or Partitioned user access

**??** This section depends on the question in step 1. ??

The next decision is to determine if the Shared iPads will be used for guest access or partitioned user access.

- **Guest access**

  Use this option for temporary sessions. Users sign in to the device as a guest. They don't enter a Managed Apple ID or password. All user data, including browsing history, is deleted when the user signs out of the session.

  For example, in healthcare, a medical patient is assigned a shared iPad to check in or fill out forms. Or, in hospitality setting, guests can utilize without having to sign-in. **??**  The hospitality example is confusing. Need to clarify. ??

- **Partitioned user access**

  Use this option when an iPad is used by many users at different times. Each user signs in to the device with their federated Azure AD credentials. User partitions ensure that each user's apps, data, and preferences are stored separately on the iPad.

  When the user signs out, their data remains on the device in their own partition. Then, the device is ready for the next user to sign in and use the device.

  The number of users that can sign in also varies by the amount of storage on the device. So, it's recommended to plan accordingly and configure the enrollment profile to accommodate your needs.

For more information on these options, go to [Set up Shared iPad in Intune](/enrollment/device-enrollment-shared-ipad.md).

#### Step 3 - Home screen layout and device experience

So far, you're using ADE enrollment and determined access. Next, consider what end users will be doing on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

In Intune, you can create device configuration profiles that configure the home screen and run apps in kiosk mode.

For a list of the Shared iPad settings you can configure, go to [Configure settings for Shared iPads](../enrollment/device-enrollment-shared-ipad#configure-settings-for-shared-ipads.md).

For a list of all the device configuration settings, go to:

- [iOS and iPadOS device settings to use common features](../configuration/ios-device-features-settings.md)
- [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md)

## Windows

Windows 365 frontline
cloud PC

- https://www.microsoft.com/windows-365/frontline
- https://learn.microsoft.com/windows-365/enterprise/introduction-windows-365-frontline

## Other MSFT services that do FLW


## Next steps
