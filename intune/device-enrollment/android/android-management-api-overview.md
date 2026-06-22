---
title: Android Management API for personally owned work profiles
description: Learn about the transition to Android Management API for personally owned work profile devices, including web-based enrollment, migration steps, and what IT admins need to know.
ms.date: 06/18/2026
ms.topic: overview
ms.reviewer: priyar, grwilso
ms.collection:
- M365-identity-device-management
---

# Use Android Management API for personally owned devices with work profiles

Microsoft Intune is transitioning personally owned work profile management to Google's Android Management API. This change modernizes how Intune delivers policies to Android personally owned work profile devices and introduces a web-based enrollment flow.

This article covers what Android Management API is, how it affects your Intune environment, and what you need to do to prepare.

## What is the Android Management API?

Android Management API is Google's recommended API for Android Enterprise device management. Android Management API uses the **Android Device Policy** app to enforce policies on devices, replacing the need for custom device policy controllers (DPCs) like the Intune Company Portal app.

When Intune first released support for Android personally owned work profile management, it used a custom DPC implementation built into the Company Portal app. Since then, Google released Android Management API and now recommends it for all Android Enterprise management. Google is actively deprecating custom DPC functionality.

Intune already uses Android Management API for the three corporate Android Enterprise management methods:

- Corporate-owned devices with a work profile
- Fully managed devices
- Dedicated devices

The personally owned work profile is the last management method moving to Android Management API.

## Benefits of moving to Android Management API

The transition to Android Management API provides the following advantages for IT admins:

- Faster feature delivery: New Android Enterprise management features release across all Android Enterprise management methods simultaneously instead of requiring separate development for the custom DPC implementation.
- Consistent behavior: All Android Enterprise management methods use the same underlying API, resulting in predictable and uniform behavior.
- Updated user app: The Microsoft Intune app replaces the Company Portal app as the primary user-facing app for device management, diagnostics, and IT contact. This aligns with how corporate Android Enterprise devices already work.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platform:
>
> - Android Enterprise personally owned devices with a work profile enrolled in Intune
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To create the device configuration policy:
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

## Use web-based enrollment for new devices

The move to Android Management API also enables a new web-based enrollment flow for personally owned work profile devices, similar to web-based device enrollment for iOS.

### Enable web-based enrollment

When you enable web-based enrollment, it applies at the tenant level to all new personally owned work profile enrollments. Users can begin enrollment from a webpage with no app installation required. They can access the enrollment page through a URL you provide, or through productivity apps when Conditional Access requires enrollment before accessing corporate resources.

Before you enable web-based enrollment:

- Test in a test tenant before enabling it in production.
- Walk through the enrollment experience and update your internal helpdesk documentation.

To enable web-based enrollment:

1. In the Microsoft Intune admin center, go to **Devices**.  

1. Select the **Android** tab.  

1. Expand **Device onboarding** and select **Enrollment**.  

1. Under **Enrollment Profiles**, select **Personally owned devices with a work profile**.  

1. Select **Use web enrollment for all users enrolling into Android personally owned work profile management**.  

1. Select **Ok** to save your changes. This change can't be reversed.  

## Create a device configuration profile for existing devices

For devices already enrolled in Intune, use the Android Management API device configuration policy to migrate these devices to Android Management API. After they're migrated to Android Management API, they can't roll back to the previous management method.

### Before you migrate

- [Prepare your environment](#prepare-your-environment). There are some features that don't work with Android Management API and other features that might have changed behavior.
- Start small. Migrate a smaller set of devices to validate the experience before migrating your full fleet.
- Notify users. Before migrating devices, email users or configure custom notifications to explain the upcoming changes.
- Monitor progress. Use the **Personal Devices on Android Management API** report to track devices across these states:

  - **AMAPI**: Devices on Android Management API.  
  - **Not targeted to move**: Devices not targeted to move to Android Management API.  
  - **Move pending**: Devices targeted to move and pending completion.  
  - **Error**: Devices that attempted to move and encountered an error.  

### Create the device configuration profile

1. Sign in to the [Microsoft Intune admin center].
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **Templates** > **Move to Android Management API**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Android: Move to Android Management API**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Next**.

    This template doesn't have settings for you to configure. The configuration is done by Intune when the device receives the policy.

8. In **Assignments**, select the device groups that will receive your profile. For information on assigning profiles, go to [Assign user and device profiles](../../device-configuration/assign-device-profile.md).

    Select **Next**.

9. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

When you assign the policy, devices start moving to Android Management API. If you unassign or delete this policy, devices that already moved keep using Android Management API. Targeted devices that haven't received the policy won't be moved to Android Management API.

### What happens to devices during migration

When a device migrates to Android Management API:

- No unenrollment occurs. Users keep access to corporate resources throughout the migration.
- The Microsoft Intune app installs silently and becomes the primary user app. It replaces Company Portal for device management tasks.
- The Android Device Policy app installs in a hidden state to enforce Android Management API policies.
- Wi-Fi access might be affected. Devices connected to corporate Wi-Fi with username/password authentication lose Wi-Fi access until the user signs in again. Devices using certificate-based Wi-Fi authentication aren't affected.

> [!TIP]
> Move to certificate-based Wi-Fi authentication before migrating devices to avoid Wi-Fi disruptions. Certificate authentication is also more secure.

## Apps installed after enrollment or migration

Intune automatically installs the following apps on devices managed by Android Management API:

| App | Purpose |
|---|---|
| **Microsoft Intune** | User-facing app for device management, IT contact, and diagnostic log collection. |
| **Company Portal** | Required for mobile app management. |
| **Android Device Policy** | Enforces Android Management API policies. Installed in a hidden state. Users don't see it. |
| **Microsoft Authenticator** | Provides single sign-on (SSO) for the user's work account. |

## Prepare your environment

Take these actions before the migration to Android Management API to ensure a smooth transition.

### Replace custom configuration policies

[Intune ended support for custom configuration policies for personally owned work profile devices](../../whats-new/archive/index.md#intune-ending-support-for-custom-profiles-for-personally-owned-work-profile-devices). Custom policies don't work with Android Management API. Replace all custom policies with equivalent built-in policies.

For help with the replacement settings, see [Replace custom policies with built-in settings](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-custom-profiles-for-personally-owned-work-profile-devi/4287414). If the setting is available in the [settings catalog](../../device-configuration/settings-catalog/index.md), then create a settings catalog policy. If the setting isn't available in the settings catalog, then use the [device restrictions template](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

### Switch to certificate-based Wi-Fi authentication

If your Wi-Fi policies use username/password authentication, switch to certificate-based authentication. Devices on Android Management API lose Wi-Fi access during migration until the user manually signs back in.

### Evaluate biometric configuration

Android Management API doesn't support policies that prevent users from using biometrics (face, fingerprint, iris) or trust agents to unlock their device at the *device level*. Policies that block biometrics at the *work profile level* are still supported.

If you currently block biometrics at the device level, consider moving that restriction to the work profile level to continue protecting work resources.

> [!NOTE]
> For users who use a unified password (one lock for both the device and work profile), biometric settings configured for the work profile apply to the device as well.

### Review enrollment restrictions

The **Personally owned** device setting in enrollment restrictions (under **Android Enterprise (work profile)**) doesn't apply to devices managed by Android Management API. This setting will be removed from the Intune admin center when all devices are on Android Management API.  

If you currently set **Personally owned** to **Block**, plan an alternative approach:  

- Use a corporate management method instead, such as corporate-owned work profile.
- Configure enrollment restrictions to allow only a specific group of users.

### Update devices to a supported Android version

Ensure devices are running a supported Android version. After you enable enrollment with Android Management API, Devices running any Android OS version can enroll. For a list of all supported versions, see [Supported platforms](../../fundamentals/ref-supported-platforms.md).  

Devices must be running Android 9 or later to migrate to Android Management API.  

Encourage users to update to their device's latest available Android version for the best experience.  

## Changes to be aware of

Some behaviors change on devices managed by Android Management API compared to the custom DPC implementation:

| Area | Custom DPC behavior | Android Management API behavior |
|---|---|---|
| **Required apps** | Users can uninstall required apps; they reinstall automatically within a few hours. | Users can't uninstall required apps. |
| **Caller ID and contact search** | Separate settings for displaying work contact caller ID and searching work contacts from the personal profile. | Single combined setting. If either is blocked, Intune blocks both. |
| **Screen timeout** | Configurable at the device level or work profile level. | Only configurable at the work profile level. Intune uses the lesser of the two values during migration. |
| **Security provider and Google Play Services compliance** | **Up-to-date security provider** and **Google Play Services is configured** compliance settings are available. | Not supported. Security providers update automatically and Google Play Services are required for enrollment. Settings will be removed from compliance policies. |
| **Enrollment reports** | **Enrollment failures** and **Incomplete user enrollments** reports include all devices. | These reports don't include devices enrolled through Android Management API. |
| **Google domain allow listing** | Configured through Intune device restriction policies. | Managed through the Google Admin console under **Third-party integrations**. Setting will be removed from Intune device restriction policies. |

## Related content

For the latest updates on rollout timeline and enforcement changes, see [New policy implementation and web enrollment for Android personally owned work profile](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-policy-implementation-and-web-enrollment-for-android-personally-owned-work-p/4370417).

- [Android Enterprise work profile management overview](enterprise-work-profile.md)
- [Set up enrollment of Android Enterprise personally owned work profile devices](setup-personal-work-profile.md)
- [Redo Workplace Join for Android Enterprise devices](redo-workplace-join-android.md)

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431