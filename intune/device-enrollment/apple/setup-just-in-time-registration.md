---
title: Set up just-in-time registration
description: Set up JIT registration in Intune for devices enrolling via a supported Apple device enrollment or user enrollment method.
ms.date: 07/22/2024
ms.topic: install-set-up-deploy
ms.reviewer: rishitasarin
ms.collection:
- M365-identity-device-management
---

# Set up just-in-time registration in Microsoft Intune
**Applies to iOS/iPadOS**

Set up *just-in-time (JIT) registration* in Microsoft Intune to enable device users to initiate and complete device enrollment from a work or school app. The Intune Company Portal isn't required when using JIT registration. Instead, JIT registration utilizes the Apple single sign-on (SSO) extension to complete Microsoft Entra registration and compliance checks. Registration and compliance checks can be fully integrated in a designated Microsoft or non-Microsoft app that's configured with the Apple single sign-on (SSO) app extension.  The extension reduces authentication prompts during the device user's session and establishes SSO across the whole device.

JIT compliance remediation, the feature that initiates compliance checks, is enabled automatically on devices utilizing JIT registration and targeted with compliance policies. Compliance remediation happens in an embedded flow within the app users are registering. They can see their compliance status and take actionable steps to remediate the issues as they complete JIT registration. If their device is noncompliant, for example, the Company Portal website opens in the app and shows them the reason for noncompliance.

This article describes how to enable JIT registration by creating an SSO app extension policy in the Microsoft Intune admin center.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This feature supports the following platforms:
>
> - iOS/iPadOS

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [enrollment-methods](../../includes/requirements/enrollment-methods.md)]

:::column-end:::
:::column span="3":::

> Microsoft Intune supports JIT registration and compliance remediation for all iOS and iPadOS enrollments, including:
>
> - Apple User Enrollment: Account-driven user enrollment and user enrollment with Company Portal
> - Apple Device Enrollment: Web-based device enrollment and device enrollment with Company Portal
> - Apple automated device enrollment: For enrollments that use Setup Assistant with modern authentication as the [authentication method](ref-automated-authentication-methods.md)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::

> To take advantage of JIT compliance remediation, you must assign compliance policies to devices.

:::column-end:::
:::row-end:::

## Best practices for SSO configuration
* The user's first sign-in after they reach the home screen has to happen in a work or school app that's configured with the SSO extension. Otherwise, Microsoft Entra registration and compliance checks can't be completed. We recommend that you point employees to the Microsoft Teams app. The app is integrated with the latest identity libraries and provides the most streamlined experience from the user's home screen.

* The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add the bundle IDs for your Microsoft apps to your policy. You only need to add non-Microsoft apps.

* Don't add the bundle ID for the Microsoft Authenticator app to your SSO extension policy. Since it's a Microsoft app, the SSO extension will automatically work with it.

## Set up JIT registration
Create a single sign-on app extension policy that uses the Apple SSO extension to enable just-in-time (JIT) registration.
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. [Create an iOS/iPadOS device configuration policy](../../device-configuration/templates/configure-device-features-apple.md) under **Device features** > **Category** > [**Single sign-on app extension**](../../device-configuration/templates/configure-device-features-apple.md#single-sign-on-sso).
3. For **SSO app extension type**, select **Microsoft Entra ID**.
4. Add the [app bundle IDs](../../device-configuration/templates/ref-bundle-ids-ios.md) for any non-Microsoft apps using single sign-on (SSO). The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add Microsoft apps to your policy.

    Don't add the Microsoft Authenticator app to the SSO extension either.  That app is added later in an app policy.

    To get the bundle ID of an app added to Intune, [you can use the Intune admin center](../../app-management/collect-bundle-ids.md).

5. Under **Additional configuration**, add the required key-value pair. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.
    * **Key**: device_registration
    * **Type**: String
    * **Value**: {{DEVICEREGISTRATION}}
6. (Recommended) Add the key-value pair that enables SSO in the Safari browser for all apps in the policy. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.
    * **Key**: browser_sso_interaction_enabled
    * **Type**: Integer
    * **Value**: 1
7. Select **Next**.
8. For **Assignments**, assign the profile to all users, or select specific groups.
9. Select **Next**.
10. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.
11. Go to **Apps** > **All Apps** and assign Microsoft Authenticator to groups as a required app. For more information, see [Add apps to Microsoft Intune](../../app-management/deployment/index.md) and [Assign apps to groups](../../app-management/deployment/assign-groups.md).

## Next steps
Create an enrollment policy for enrolling devices. The enrollment policy triggers the device user's enrollment experience, and enables them to initiate enrollment. For information about how to create a profile for supported enrollment types, see the following resources:

* [Account driven user enrollment](setup-account-driven-user.md)
* [User enrollment with Company Portal](setup-user-company-portal.md)
* [Apple automated device enrollment for Setup Assistant with modern authentication](setup-automated-ios.md#create-an-apple-enrollment-policy)
* [Web based device enrollment](setup-web-based-ios.md)
* [Device enrollment with Company Portal](personal-device-options-ios.md#app-or-web-based-enrollment)
