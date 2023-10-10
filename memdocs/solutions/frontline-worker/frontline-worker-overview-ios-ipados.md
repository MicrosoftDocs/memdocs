---
title: Get started with iOS/iPadOS frontline worker devices
description: Learn how to manage frontline worker devices using iOS and iPadOS devices in Microsoft Intune. Select the best enrollment option, configure the home screen, and more.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 10/09/2023
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

# Frontline worker for iOS/iPadOS devices in Microsoft Intune


This article applies to:

- iOS and iPadOS devices owned by the organization and enrolled in Intune

iPad devices are a popular device type for frontline workers (FLW). The Shared iPad feature in Intune is designed for frontline workers.

iOS devices can also be used, but it's not common. For iOS FLW devices, it's recommended to use [Azure AD shared device mode](/azure/active-directory/develop/msal-ios-shared-devices) and Intune together. In Intune, you enroll the device and create a device restrictions configuration profile. In the profile, you can allow (or prohibit) specific apps, and can hide apps.

The following diagram shows the iOS/iPadOS options for frontline worker devices in Intune:

:::image type="content" source="./media/ios-ipados-flw-options.png" alt-text="Diagram that shows Apple iOS and iPadOS frontline worker scenario path in Microsoft Intune." lightbox="./media/ios-ipados-flw-options.png":::

> [!NOTE]
> For iPadOS devices, Conditional Access isn't supported for Shared iPad. For more information, go to [Overview of shared device solutions for iOS/iPadOS](../intune/enrollment/device-enrollment-shared-ios.md).

Since iPads are a popular Apple device type for frontline workers (FLW), **this section focuses on iPad devices**.

iPads are used in different scenarios and industries, including in field operations, healthcare, aviation, warehouse, data entry, digital forms, and presentations.

For FLW iPad devices, there are two options available:

- **Shared iPad**
  OR
- **Azure AD shared device mode**

:::image type="content" source="./media/ios-ipados-flw-enrollment-options.png" alt-text="Diagram that shows all the Intune enrollment options for iPadOS frontline worker devices in Microsoft Intune." lightbox="./media/ios-ipados-flw-enrollment-options.png":::

When using iPad devices for FLW, use the following information to help you decide which option is best for your organization.

For iPad devices, admins must pick one option - **Shared iPad** in Intune or **Azure AD shared device mode**. This decision impacts how you configure the device.

- **Shared iPad**

  Shared iPads are a feature in Intune, and are the recommended and preferred device type for frontline worker devices. These devices are shared among many users, such as in a hospital or school. Each user has their own profile and data, and they can sign in and out of the device.

  ✔️ If the device is an iPad, then use the Shared iPad feature in Intune. For more information on Shared iPads in Intune, go to [Shared iPad devices in Intune](../intune/enrollment/device-enrollment-shared-ipad.md).

  ❌ If the device is an iOS device, then use Azure AD shared device mode. For more information, go to [Azure AD shared device mode for FLW](frontline-worker-overview.md#azure-ad-shared-device-mode-for-flw) and [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices).

- **Azure AD shared device mode**

  Azure AD shared device mode (SDM) is an option for iOS and iPadOS devices and uses the [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin). Azure AD SDM offers an app and identity driven sign in/sign out experience, which improves the end user experience and productivity (less sign in prompts). Azure AD shared device mode isn't supported with Shared iPad feature in Intune.

  For more information on Azure AD shared device mode (SDM), go to [Azure AD shared device mode for FLW](frontline-worker-overview.md#azure-ad-shared-device-mode-for-flw).

  When to use Azure AD SDM:

  ✔️ If the device is an iOS device, then use Azure AD shared device mode.

  ✔️ If the device is an iPad, then you can use Azure AD shared device mode **OR** Shared iPad in Intune.

  ❌ If you configured an iPad to be a Shared iPad in Intune, then don't use Azure AD shared device mode. It's not supported.

  For end users to have the full sign in/sign out experience, apps must support Azure AD SDM. For more information on Azure AD SDM and iOS/iPadOS devices, go to:

  - [Shared device mode for iOS devices](/azure/active-directory/develop/msal-ios-shared-devices)
  - [Set up automated device enrollment for shared device mode](../intune/enrollment/automated-device-enrollment-shared-device-mode.md)

For a comparison of both options, go to [Shared iOS and iPadOS devices](../intune/enrollment/device-enrollment-shared-ios.md).

> [!NOTE]
> There are other iOS/iPadOS enrollment options available. This article focuses on the enrollment options commonly used for FLW devices. For more information on all the iOS/iPadOS enrollment options, go to [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../intune/fundamentals/deployment-guide-enrollment-ios-ipados.md).

## Shared iPads

Shared iPads are a feature in Intune. If you're not using Shared iPads, then skip this section.

This section focuses on Shared iPads used by frontline workers, including the decisions admins need to make, determining how the device is used, and configuring the home screen & device experience.

### Step 1 - Use Automated Device Enrollment (ADE), enable Shared iPad, and choose a temporary session type

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

:::image type="content" source="./media/shared-ipad-ade-enrollment-policy.png" alt-text="An Automated Device Enrollment (ADE) policy with Shared iPad enabled, and temporary sessions for Shared iPadOS enabled for frontline worker devices in Microsoft Intune." lightbox="./media/shared-ipad-ade-enrollment-policy.png":::

For more information on these features, and to get started, go to:

- [Set up automated device enrollment in Intune](../intune/enrollment/device-enrollment-program-enroll-ios.md)
- [Set up Shared iPad in Intune](../intune/enrollment/device-enrollment-shared-ipad.md)

### Step 2 - Home screen layout and device experience

Next, consider what end users do on the devices and the device experience they need for their jobs. This decision impacts how you configure the device.

In Intune, you can create device configuration profiles that configure the home screen and the apps that are shown. Specifically, you create a:

- **Device features** policy to configure the home screen layout and other settings you want to apply to the device:

  :::image type="content" source="./media/ios-ipados-device-features-home-screen-layout.png" alt-text="A device features policy with the home screen layout settings configured for iOS and iPadOS device in Microsoft Intune." lightbox="./media/ios-ipados-device-features-home-screen-layout.png":::

- **Device restrictions** policy to configure other device settings, such as using kiosk mode and other settings you want to apply to the device:

  :::image type="content" source="./media/ios-ipados-device-restrictions-kiosk.png" alt-text="A device restrictions policy with the device settings configured for iOS and iPadOS devices in Microsoft Intune." lightbox="./media/ios-ipados-device-restrictions-kiosk.png":::

  In this policy, you can also create a list of approved apps, prohibited apps, and hide some system apps. For more information on the settings you can configure, go to [iOS and iPadOS device settings to allow or restrict features using Intune](../intune/configuration/device-restrictions-ios.md).

For a list of the Shared iPad settings you can configure, go to [Configure settings for Shared iPads](../intune/enrollment/device-enrollment-shared-ipad.md#configure-settings-for-shared-ipads).

For a list of all the device configuration settings, go to:

- [iOS and iPadOS device settings to use common features](../intune/configuration/ios-device-features-settings.md)
- [iOS and iPadOS device settings to allow or restrict features](../intune/configuration/device-restrictions-ios.md)

## Related articles

- [Frontline worker device management overview in Microsoft Intune](frontline-worker-overview.md)
- [FLW for Android devices](frontline-worker-overview-android.md)
- [FLW for Windows devices](frontline-worker-overview-windows.md)
