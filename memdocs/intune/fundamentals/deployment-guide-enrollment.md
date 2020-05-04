---
# required metadata

title: Device enrollment guide for Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Deployment guide: Enroll devices in Microsoft Intune

THIS GUIDE IS STILL BEING WRITTEN, AND MAY CONTAIN INCORRECT INFORMATION.

Enrolling devices in Intune allows them to receive the policies you create. This includes compliance policies that help users and devices meet your rules. And, it includes configuration profiles that configure features and settings on devices.

Intune includes several "parts": app configuration, app protection, user and device compliance, and device configuration. You can use these parts individually, or together. When users and devices enroll, they can receive these policies during enrollment. Or, they can receive your policies after they enroll. The order depends on your organization's needs.

Many organizations create a baseline of what all users and devices must have. Typically, these policies get deployed during enrollment. For more information on enrollment, see [What is device enrollment?](../enrollment/device-enrollment.md).

When a device is enrolled, it's issued an MDM certificate. This certificate communicates with the Intune service.

This deployment guide includes details to enroll devices running different platforms, and separates the administrative tasks from the end user tasks.


Azure AD deployment guides: https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-deployment-plans

## Prerequisites

- Intune is set up, and ready to enroll users and devices. Be sure:

  - The [MDM Authority](../fundamentals/mdm-authority-set.md) is set to Intune, even when using [co-management](https://docs.microsoft.com/configmgr/comanage/overview) with Intune + Configuration Manager.
  - [Intune licenses are assigned](../fundamentals/licenses-assign.md).

  For more information, see [Intune setup deployment guide](deployment-guide-intune-setup.md).

- Your devices [are supported](../fundamentals/supported-devices-browsers.md). This requirement includes devices that are co-managed, or hybrid Azure Active Directory (Azure AD) joined devices.

- Sign in as a member of the **Global Administrator** or **Intune Service Administrator** Azure AD roles. [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) has more information. If you created an Intune trial subscription, then the account that created the subscription is the **Global administrator**.

- For your iOS/iPadOS and macOS devices, you need an MDM push certificate from Apple. For the specific steps, see [get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).

- Have your users groups and device groups ready to receive your enrollment policies. If you haven't reviewed or created your group structure, and want some guidance, then see [Planning Guide: Task 4: Review existing policies and infrastructure](intune-planning-guide.md#task-4-review-existing-policies-and-infrastructure).

Azure AD deployment guides: https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-deployment-plans

## Pilot groups

When assigning your profiles, start small, and use a staged approach. Assign the profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the profile to more pilot groups.

Using a staged approach, you can get feedback from a wide range of user types.

For more information and suggestions, see the [Planning guide: Task 5: Create a rollout plan](../fundamentals/intune-planning-guide.md#task-5-create-a-rollout-plan).

## Unenroll from existing MDM and factory reset

If devices are currently enrolled in another MDM provider, then unenroll the devices from the existing MDM provider. Unenrolling may not remove existing features and settings you configured. MDM providers have remote actions that remove organization-specific data from devices. Before enrolling in Intune, you can remove this data from these devices. But, it's not required.

It's required to factory reset devices running the following platforms:

- Android Enterprise dedicated devices (COSU)
- Android Enterprise fully managed (COBO)
- iOS/iPadOS
- macOS

If you don't factory reset, then <get info from PFE, CSS>.

On other platforms, when these devices enroll in Intune, they'll start receiving your Intune policies. If you don't configure a setting in Intune, then Intune doesn't change or update that setting. So, it's possible that any previously configured settings remain configured on the device.

## Enroll Android devices

Can enroll personal or BYOD, and organization-owned devices.

For an overview enrollment on Android and Android Enterprise devices, see [Enroll Android device administrator and Android Enterprise devices](../enrollment/android-enroll.md).

- Android device administrator
- Android Enterprise dedicated devices
- Android Enterprise fully managed
- Android Enterprise work profile

### Android device administrator

> [!NOTE]
> Google is decreasing device administrator support in new Android releases. To avoid reduced functionality, Microsoft recommends:
>
> - Enroll new devices using [Android Enterprise work profiles](#android-enterprise-work-profile) (in this article). Do **not** enroll new devices using Android device administrator.
> - If devices will update to Android 10, then migrate devices off device administrator management.
> - Move existing Android device administrator devices to Android Enterprise work profiles. For more information, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md).

These devices are personal or BYOD (bring your own device) Android devices that can access work or school email, apps, and other data.

- **Administrators**: In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable device administrator enrollment. For the specific steps, see [Android device administrator enrollment](../enrollment/android-enroll-device-administrator.md).
- **End users**: Your users must do the following:

  1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
  2. Open the Company Portal app, and [enroll the device](../user-help/enroll-device-android-company-portal.md).

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

### Android Enterprise dedicated devices

These devices are organization-owned, with a sole purpose of being a kiosk-style. These devices are commonly used to scan items, print tickets, digitally sign, manage inventory, and more. They're commonly referred to as COSU (corporate-owned, single-use) devices.

- **Administrators**:

  1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
  2. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your dedicated device group(s) ready. For the specific steps, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).
  3. Factory reset the devices. This step is required.
  4. Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise dedicated devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

      On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

- **End users**: It's not recommended for users to enroll Android Enterprise dedicated devices. This task should be completed by administrators.

### Android Enterprise fully managed

These devices are organization-owned, and have one user. They are used exclusively for organization work; not personal use. They're commonly referred to as COBO (corporate-owned, business only) devices.

- **Administrators**:

  1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
  2. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable fully managed user devices in Intune. For the specific steps, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/enrollment/android-fully-managed-enroll.md).
  3. Factory reset the devices. This step is required.
  4. Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise fully managed devices](../enrollment/enrollment/android-dedicated-devices-fully-managed-enroll.md).

      On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

- **End users**: It's not recommended for users to enroll Android Enterprise dedicated devices. This task should be completed by administrators.

### Android Enterprise work profile

These devices are personal or BYOD (bring your own devices) Android devices that can access work or school email, apps, and other data.

- **Administrators**:

  1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
  2. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an [enrollment restriction](../enrollment/enrollment-restrictions-set.md), and **allow** devices that support Android Enterprise work profiles. For the specific steps, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).

- **End users**: Your users must do the following:

  1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
  2. Open the Company Portal app, and [enroll the device](../user-help/enroll-device-android-work-profile.md).

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

## Enroll iOS/iPadOS devices

personal and organization-owned devices. For an overview, see [Enroll iOS/iPadOS devices](../enrollment/ios-enroll.md).

### Personal devices

These devices are personal or BYOD (bring your own device) iOS/iPadOS devices that can access work or school email, apps, and other data.

- **Administrators**:

  1. Be sure you have an [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md). This is a [prerequisite](#prerequisites) (in this article) to enroll iOS/iPadOS devices.
  2. Choose the type of enrollment. Your options:

      - **Apple user enrollment**: Starting with iOS 13 and newer. This option gives you a specific set of features you can configure, such as password, VPN, Wi-Fi, Siri, and more. For the complete list of what you can and can't do, see [Intune actions and options supported with Apple User Enrollment](../enrollment/ios-user-enrollment-supported-actions.md).

        For the specific user enrollment steps, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

      - **Device enrollment**: This option gives you the full set of features you can configure. NEED INFO FROM ERIK K.

- **End users**: Your users must do the following:

  1. Go to the Apple App Store, and [install the Intune Company Portal app](../user-help/install-and-sign-in-to-the-intune-company-portal-app-ios.md).
  2. Open the Company Portal app, and [enroll the device](../user-help/enroll-your-device-in-intune-ios.md).

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

### Organization-owned devices

These devices are organization-owned, and given to users.

- **Administrators**: Apple has programs that ships devices to users, and uses your pre-configured settings to enroll devices. Your options include:

  - Apple's Automated Device Enrollment (ADE) (supervised): Formerly DEP.
  - Apple School Manager: 
  - Apple Configurator Setup Assistant enrollment: 
  - Apple Configurator direct enrollment: 
  - Device enrollment manager (DEM) account: This account is an Intune permission that's applied to an Azure AD user account. The DEM account can enroll up to 1,000 mobile devices. Use this option to enroll and configure the devices before giving them to users.

    For the specific enrollment steps, see [Enroll devices in Intune by using a device enrollment manager account](../enrollment/device-enrollment-manager-enroll.md).

- **End users**: 

## Enroll macOS devices

[Enroll macOS devices](../enrollment/macos-enroll.md)

1. Be sure you have an [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).

> - User enrollment (Intune isn’t support for now but it is a type of Apple MDM enrollment)
> - Device enrollment without user approval
> - Device enrollment with user approval 
> - Automated device enrollment (formerly DEP) 


## Enroll Windows devices

[Enroll Windows devices](../enrollment/windows-enrollment-methods.md)

**Option 1 - Windows only**: You can set up [hybrid Active Directory and Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) for your devices. Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. Devices in Azure AD are available to Intune. Devices that aren't registered in Azure AD aren't available to Intune.

  Hybrid Azure AD support Windows devices. For other prerequisites, including sign-in requirements, see [Plan your hybrid Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

**Option 2 - All platforms**: Reset the device, and enroll the device in Intune. It's considered a new device, and receives the policies and profiles you create. 

## AutoPilot

Admin's enroll
Use AutoPilot to enroll - See Erik's articles.

Remote workers, which includes supported Home SKU

[Tutorial: Use Autopilot to enroll Windows devices in Intune](../enrollment/tutorial-use-autopilot-enroll-devices.md)

OEMs that support AUtopilot: https://www.microsoft.com/en-us/microsoft-365/windows/windows-autopilot

## Personal or BYOD

Users enroll using the Company Portal app. 

## Common issues and resolutions

In this section, add extra information provided by CSS and PFE teams.

[Troubleshoot device enrollment](../enrollment/troubleshoot-device-enrollment-in-intune.md)

## Next steps

[Intune setup deployment guide](deployment-guide-intune-setup.md)  
[Compliance and configuration deployment guide](deployment-guide-compliance-configuration.md)  
App deployment guide (MFA)