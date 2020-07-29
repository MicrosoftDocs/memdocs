---
# required metadata

title: Device enrollment guide for Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/29/2020
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


Azure AD deployment guides: https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-deployment-plans

## Prerequisites

- Intune is set up, and ready to enroll users and devices. Be sure:

  - The [MDM Authority](../fundamentals/mdm-authority-set.md) is set to Intune, even when using [co-management](https://docs.microsoft.com/configmgr/comanage/overview) with Intune + Configuration Manager.
  - [Intune licenses are assigned](../fundamentals/licenses-assign.md).

  For more information, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).

- Your devices [are supported](../fundamentals/supported-devices-browsers.md). This requirement includes devices that are co-managed, or hybrid Azure Active Directory (Azure AD) joined devices.

- Sign in as a member of the **Global Administrator** or **Intune Service Administrator** Azure AD roles. [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) has more information. If you created an Intune trial subscription, then the account that created the subscription is the **Global administrator**.

- Different platforms may have additional requirements. For example, iOS/iPadOS and macOS devices require an [MDM push certificate from Apple](../enrollment/apple-mdm-push-certificate-get.md). Any additional platform requirements are listed in this article.

  | Platform | Additional requirements |
  | --- | --- |
  | Android | none |
  | Android Enterprise | none |
  | iOS/iPadOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)<br/>Apple ID |
  | macOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) |
  | Windows | none |

- Have your users groups and device groups ready to receive your enrollment policies. If you haven't reviewed or created your group structure, and want some guidance, then see [Planning Guide: Task 4: Review existing policies and infrastructure](intune-planning-guide.md#task-4-review-existing-policies-and-infrastructure).

- If you're bulk enrolling devices, consider creating the **Device enrollment manager** (DEM) account. This account is an Intune permission that's applied to an Azure AD user account. The DEM account can enroll up to 1,000 mobile devices. Use this account to enroll and configure the devices before giving them to users.

  For more information, see [Enroll devices in Intune by using a device enrollment manager account](../enrollment/device-enrollment-manager-enroll.md).

Azure AD deployment guides: https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-deployment-plans

## Pilot groups

When assigning your profiles, start small, and use a staged approach. Assign the profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the profile to more pilot groups.

For more information and suggestions, see the [Planning guide: Task 5: Create a rollout plan](../fundamentals/intune-planning-guide.md#task-5-create-a-rollout-plan).

## Unenroll from existing MDM and factory reset

If devices are currently enrolled in another MDM provider, then unenroll the devices from the existing MDM provider. Typically, unenrolling doesn't remove existing features and settings you configured. Most MDM providers have remote actions that remove organization-specific data from devices. Before enrolling in Intune, you can remove organization-specific data from these devices. But, it's not required.

Depending on the platform, a factory reset may be required before enrolling in Intune.

-----
| Platform | Factory reset required? |
| --- | --- |
| Android device administrator | No |
| Android Enterprise dedicated devices (COSU) | Yes |
| Android Enterprise fully managed (COBO) | Yes |
| Android Enterprise work profile (profile owner) | No |
| iOS/iPadOS | Yes |
| macOS | Yes |
| Windows | No |

-----

On the platforms that don't require a factory reset, when these devices enroll in Intune, they'll start receiving your Intune policies. If you don't configure a setting in Intune, then Intune doesn't change or update that setting. So, it's possible that any previously configured settings remain configured on the device.

## Enroll Android devices

Can enroll personal or BYOD, and organization-owned devices.

For an overview enrollment on Android and Android Enterprise devices, see [Enroll Android device administrator and Android Enterprise devices](../enrollment/android-enroll.md).

- Android device administrator
- Android Enterprise dedicated devices
- Android Enterprise fully managed
- Android Enterprise work profile (profile owner)

### Android device administrator

> [!NOTE]
> Google is decreasing device administrator support in new Android releases. To avoid reduced functionality, Microsoft recommends:
>
> - Enroll new devices using [Android Enterprise work profiles](#android-enterprise-work-profile) (in this article). Do **not** enroll new devices using Android device administrator.
> - If devices will update to Android 10, then migrate devices off device administrator management.
> - Move existing Android device administrator devices to Android Enterprise work profiles. For more information, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md).

These Android devices are personal or BYOD (bring your own device) devices that can access work or school email, apps, and other data.

- **Administrator tasks**:

  - In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable device administrator enrollment. For the specific steps, see [Android device administrator enrollment](../enrollment/android-enroll-device-administrator.md).
  - Be sure your devices are [supported](supported-devices-browsers.md).

- **End users**: Your users must do the following. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

  1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
  2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

      Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-company-portal.md).

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

### Android Enterprise dedicated devices

These devices are organization-owned, with a sole purpose of being a kiosk-style. These devices are commonly used to scan items, print tickets, get digital signatures, manage inventory, and more. They're commonly referred to as COSU (corporate-owned, single-use) devices.

Use this enrollment option when:

- Your devices are owned by the organization.
- Your devices are shared devices, and aren't associated with a single or specific user.
- You have existing or new devices.
- You need to enroll a small number of devices or a large number of devices (bulk enrollment).

Don't use this enrollment option when:

- Your devices are personal or BYOD.

- **Administrator tasks**:

  1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
  2. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an enrollment profile, and have your dedicated device group(s) ready. For the specific steps, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).
  3. Factory reset the devices. This step is required.
  4. Be sure your devices are [supported](supported-devices-browsers.md).
  5. Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise dedicated devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md).

      On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

- **End users**: It's not recommended for users to enroll Android Enterprise dedicated devices. This task should be completed by administrators.

### Android Enterprise fully managed

These devices are organization-owned, and have one user. They are used exclusively for organization work; not personal use. They're commonly referred to as COBO (corporate-owned, business only) devices.

Use this enrollment option when:

- Your devices are owned by the organization, and are associated with a single user.
- You have existing or new devices.
- You need to enroll a small number of devices or a large number of devices (bulk enrollment).

Don't use this enrollment option when:

- Your devices are personal or BYOD.

- **Administrator tasks**:

  1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
  2. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), enable fully managed user devices in Intune. For the specific steps, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/enrollment/android-fully-managed-enroll.md).
  3. Factory reset the devices. This step is required.
  4. Be sure your devices are [supported](supported-devices-browsers.md).
  5. Enroll the devices in Intune. For the specific steps, see [Enroll your Android Enterprise fully managed devices](../enrollment/enrollment/android-dedicated-devices-fully-managed-enroll.md).

      On Samsung's Knox devices, you can automatically enroll a large number of Android Enterprise devices using Samsung Knox Mobile Enrollment (KME). For more information, see [Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md).

- **End users**: It's not recommended for users to enroll Android Enterprise fully managed devices. This task should be completed by administrators.

### Android Enterprise work profile

These devices are personal or BYOD (bring your own devices) Android devices that can access work or school email, apps, and other data.

Use this enrollment option when:

- Your devices are personal or BYOD.
- You have existing or new devices.
- You need to enroll a small number of devices or a large number of devices (bulk enrollment).

Don't use this enrollment option when:

- Your devices are owned by the organization.

- **Administrator tasks**:

  1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), connect your Intune organization account to your Managed Google Play account. When you connect, Intune automatically adds the Company Portal app and other common Android Enterprise apps to the devices. For the specific steps, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
  2. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create an [enrollment restriction](../enrollment/enrollment-restrictions-set.md), and **allow** devices that support Android Enterprise work profiles. For the specific steps, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md).
  3. Be sure your devices are [supported](supported-devices-browsers.md).

- **End users**: Your users must do the following. For the specific user experience, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

  1. Go to the Google Play store, and install the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintunecompanyportal).
  2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

      Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-device-android-work-profile.md).

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

## Enroll iOS/iPadOS devices

You can enroll personal BYOD and organization-owned devices in Intune. For an overview, see [Enroll iOS/iPadOS devices](../enrollment/ios-enroll.md).

### User and Device enrollment

These iOS/iPadOS devices are personal or BYOD (bring your own device) devices that can access work or school email, apps, and other data.

Starting with iOS 13 and newer, this enrollment option targets users or targets devices. It doesn't require resetting the devices. Use this enrollment option when:

- Your devices are personal or BYOD.
- You have new or existing devices.
- You need to enroll a small number of devices or a large number of devices (bulk enrollment).
- You want to help protect a specific feature on the device, such as per-app VPN.

Don't use this enrollment option when:

- Not recommended for organization-owned devices.

For the specific enrollment steps, and its prerequisites, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).??Need to update the title of this article, is it applies to User enrollment and Device enrollment??

- **Administrator tasks**:

  - Be sure you have an [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md). This certificate is a required to enroll iOS/iPadOS devices.
  - Be sure your iOS/iPadOS devices are [supported](supported-devices-browsers.md).
  - In Intune, you create the enrollment profile. When you create the profile, you have the following options:

    - **Apple user enrollment**: Starting with iOS 13 and newer. This option configures a specific set of features and organization apps, such as password, VPN, Wi-Fi, Siri, and more. For the complete list of what you can and can't do, see [Intune actions and options supported with Apple User Enrollment](../enrollment/ios-user-enrollment-supported-actions.md).

      For the specific user enrollment steps, see [Set up iOS/iPadOS User Enrollment](../enrollment/ios-user-enrollment.md).

      It creates a work partition on the devices, per-app certs, app protection policies

      If your enrollment profile targets only personal devices, then use **User enrollment** or **Determine based on user choice**.

    Only need a very specific set of functionality. The key thing is per-app VPN. Recommendations:

      - Deploy all MSFT apps, and all apps with MAM SDK outside of corporate partition. Basically, deploy to user partition. Users must download from Apple app store. Then, preferably, protect these apps with app protect policies.

      Recommend not using this enrollment method. App protect policies provides specific set of

      - For LOB apps, deploy to corp partition. That is a key feature that app protect policies don't have. 

      Ensure a certain app is managed using MDM. User enrollment can't move app from unmanaged to managed. User donwloads outlook, CA is blocked by CA, and must enroll. If user enrollment, Outlook can't be taken over by MDM. Users would have to delete Outlook app from device.

      Has a very scoped subset of features. There's no easy path from user enrollment to device enrollment. User must enroll, and then re-enroll. 

      The real goal is friendlier to end users, less scary warnings. Admin has a scope set of things, so users can't factory reset personal partition. Admins can reset corp partition.

      If you use user enrollment, we suggest also using app protection policies. W/o app protect policy, can't manage existing apps on device installed before user enrollment. If user has outlook or edge prior to enroll, user enrollment won't work. So, admin can't protect those apps. user would have to manually remove the app, and admins would have to deploy outlook/edge as managed app. Push outlook as required app.  limited on security

    - **Apple device enrollment**: This is t typical enrollment for BYOD/personal. If you want to have full control over users' personal devices, then you can use this option. Many users may not want to give you, their ID administrators, full control over their personal devices. There are pros and cons to having full control.

      For some guidance, see [Planning guide: Task 2: Inventory your devices](intune-planning-guide.md#personal-devices-vs-organization-owned-devices).

      Secures the entire device.??What does this mean??
      - Creates an enrollment baseline that acts as default. Can deploy certs to whole device, but can't deploy updates as it required supervised.
      - Requires a user be associated with the device. User could be a device enrollment mngr account. Not good for user-less devices, such as kiosk.

      MAMWE is the standard of ios personal devices.

    - **Determine based on user choice**: Gives end users a choice when they enroll. Depending on their selection, **User enrollment** or **Device enrollment** is used.

      If your enrollment profile targets personal and organization-owned devices, then use **Determine based on user choice**. If your enrollment profile targets only personal devices, then use **User enrollment** or **Determine based on user choice**.

  - Assign the enrollment profile to user groups. Don't assign to device groups.

- **End users**: Your users must do the following. For the specific user experience, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md).

  1. Go to the Apple App Store, and [install the Intune Company Portal app](../user-help/install-and-sign-in-to-the-intune-company-portal-app-ios.md).
  2. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, your enrollment profile applies to the device.

      Users may have enter more information. For more specific steps, see [enroll the device](../user-help/enroll-your-device-in-intune-ios.md). 

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

### Automated Device Enrollment (ADE) (supervised)

Previously called Apple Device Enrollment Program (DEP). Use Apple Business Manager (ABM) or Apple School Manager (ASM) to enroll a large number of devices, without you ever touching the devices. These devices are purchased from Apple, have your pre-configured settings, and can be shipped directly to users or schools.

Use this enrollment option when:

- You need new devices that are owned by the organization or school.
- You need to enroll a large number of devices (bulk enrollment).
- Get supervised, such as deploying software updates, restrict features

Don't use this enrollment option when:

- Your devices are personal or BYOD.

For more specific information on this enrollment type, see:

- [Apple Business Manager enrollment](../enrollment/device-enrollment-program-enroll-ios.md)
- [Apple School Manager enrollment](../enrollment/apple-school-manager-set-up-ios.md)

  For more information on Apple School Manager, see [Apple education](https://www.apple.com/education/k12/it/) (opens Apple's web site).

- **Administrator tasks**:

  - Need access to the [Apple Business Manager (ABM) portal](https://business.apple.com/), or the [Apple School Manager (ASM) portal](https://school.apple.com/).
  - Have the Apple token (.p7m) ready.
  - Have the [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) ready. This certificate is required to enroll iOS/iPadOS devices.
  - Be sure your iOS/iPadOS devices are [supported](supported-devices-browsers.md).
  - In Intune, create an enrollment profile. When users connect their devices to the internet, and sign in to the Company Portal app with their organization credentials (`user@contoso.com`), they receive the profile and your settings.

      When you create an enrollment profile in Intune, you:

        - Choose to assign a user with the device (**with user affinity**), or have shared devices (**without user affinity**).
        - Choose how users authenticate: the Setup Assistant, or the Company Portal app

          If you want to use MFA, prompt users to update their expired password when they first sign in, or prompt users to reset their expired passwords during enrollment, then select the Company Portal app.

    Devices enrolled using ADE aren't compatible with the Company Portal app version in the Apple app store. Do not install this app store version. Instead, install the Company Portal app using the following options:

    **Option 1**: In Intune, in your ADE enrollment profile, deploy the Company Portal app using the **Install Company Portal with VPP** (Volume Purchase Program) option. This option:

    - Already includes the correct Company Portal app version.
    - You don't have to create another policy to deploy the Company Portal app to devices.
    - The Company Portal app must be updated manually by you, or your users.

    **Option 2**: In Intune, create an app configuration policy that deploys the Company Portal app to enrolled devices using the Volume Purchase Program. This option:

    - Already includes the correct Company Portal app version.
    - Requires you to create an enrollment profile and an app configuration policy.
    - In your app configuration policy, make it a required app so you know it's deployed to all your devices.
    - The Company Portal app can be automatically updated by changing your existing app configuration policy.

    For more information on this enrollment option, see [Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

- **End users**: When you create an enrollment profile in Intune, you choose to associate a user to the device (with user affinity), or have shared devices (without user affinity).

  - **With user affinity**:  
    1. When the device is turned on, the Apple Setup Assistant runs.
    2. When setup is complete, they enter their Apple ID, such as `user@iCloud.com` or `user@gmail.com`. Once entered, the Company Portal app is automatically installed from your profile. It can take some time for Company Portal app to auto-install.
    3. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). After they sign in, the device is checked for compliance, and may be Azure AD registered.

      Users may have to enter more information. For more specific steps, see [Enroll your organization-provided iOS device](../user-help/enroll-your-device-dep-ios.md).

  - **Without user affinity**: No actions. Be sure they don't install the Company Portal app from the Apple app store.

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

### Apple Configurator enrollment

Enrolls iOS/iPadOS devices by physically connecting these devices to the USB port on a Mac computer. Use this enrollment option when:

- You need a wired connection, or are having a network issue.
- You're enrolling a few devices.
- A country doesn't support Apple Business Manager (ABM) or Apple School Manager (ASM).
- Your organization doesn't want administrators to use the ABM or ASM portals, or doesn't want to set up all the requirements. The idea of *not* using these portals is to give administrators less control.

Don't use this enrollment option when:

- You use the device enrollment manager account. Apple Configurator can't use the device enrollment manager account.

For more specific information on this enrollment type, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

- **Administrator tasks**:

  - Requires access to a Mac computer with a USB port.
  - In Intune, you create an enrollment profile. When you create an enrollment profile in Intune, you choose to associate a user to the device (with user affinity), or have shared devices (without user affinity).

    If you choose with user affinity, then also choose if users will authenticate using **Setup Assistant** or the **Company Portal app**. Remember:

    - **Company Portal app**: Select this option to use MFA, prompt users to update their expired password when they first sign in, or prompt users to reset their expired passwords during enrollment.

    - **Setup Assistant**: Select this option to wipe the device, and import serial numbers.

    If you choose without user affinity, then you're automatically using **Direct enrollment**. Remember:

    - Users can't use apps that require a user, including the Company Portal app. Be sure they don't install the Company Portal app from the Apple app store.
    - You use the settings from an existing iOS/iPadOS enrollment profile, without serial numbers.

  - When the profile is ready, USB connect the devices to the Mac, and open the **Apple Configurator** app. When the app opens, it detects the USB connected device, and deploys the Intune enrollment profile you created.

  For more information on this enrollment option, and its prerequisites, see [Apple Configurator enrollment](../enrollment/apple-configurator-enroll-ios.md).

- **End users**:

  - **Setup Assistant enrollment**: Go to the Apple App Store, and [install the Intune Company Portal app](../user-help/install-and-sign-in-to-the-intune-company-portal-app-ios.md). Once installed, they'll can install apps, including LOB apps, used by your organization.
    - Admins should push comp port app from VPP
  - **Without user affinity (Direct enrollment)**: No actions. Be sure they don't install the Company Portal app from the Apple app store.

  Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

## Enroll macOS devices

[Enroll macOS devices](../enrollment/macos-enroll.md)

1. Be sure you have an [Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).

Be sure your devices are [supported](supported-devices-browsers.md).

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

OEMs that support AUtopilot: https://www.microsoft.com/microsoft-365/windows/windows-autopilot

## Personal or BYOD

Users enroll using the Company Portal app. 

## Common issues and resolutions

In this section, add extra information provided by CSS and PFE teams.

[Troubleshoot device enrollment](../enrollment/troubleshoot-device-enrollment-in-intune.md)

## Next steps

[Intune setup deployment guide](deployment-guide-intune-setup.md)  
[Compliance and configuration deployment guide](deployment-guide-compliance-configuration.md)  
App deployment guide (MFA)