---
title: Set up Intune enrollment for Android Enterprise dedicated devices
description: Configure enrollment in Microsoft Intune for Android Enterprise dedicated devices.
ms.date: 05/08/2025
ms.topic: how-to
ms.reviewer: grwilso
ms.collection:
- M365-identity-device-management
- highpri
---

# Set up Intune enrollment of Android Enterprise dedicated devices

Use the Android Enterprise dedicated devices solution with Microsoft Intune to set up corporate-owned, single-use kiosk-style devices for frontline workers. These devices are used for a single purpose, such as digital signage, ticket printing, or inventory management. As an administrator, you can lock down the usage of a device to a single app, or a limited set of apps, inclusive of web apps. Users are prevented from adding other apps or taking actions on the device unless explicitly approved by you.

Devices intended for dedicated use can be enrolled in Microsoft Intune in two ways:

* As a standard Android Enterprise dedicated device. These devices are enrolled into Intune without a user account and aren't associated with a user. These devices aren't intended for personal apps, or apps such as Microsoft Outlook or Google Mail that require user-specific account data.

* As a standard Android Enterprise dedicated device that's automatically set up with Microsoft Authenticator and configured for [Microsoft Entra shared device mode](/azure/active-directory/develop/msal-shared-devices) during enrollment. These devices are enrolled in Intune without a user account and aren't associated with a user. These devices are intended for use with apps that integrate with Microsoft Entra shared device mode, and allow for single sign-in and sign-out between users across participating apps.

This article describes how to set up and configure Microsoft Intune to enroll dedicated devices. For more information about Android Enterprise management solutions, see [Get started with Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)(opens Android Enterprise Help Center).

## Device requirements

Devices must have:

- Android OS version 8.0 or later.
- A distribution of Android that has Google Mobile Services (GMS) connectivity. Devices must have GMS available and must be able to connect to GMS.
- Support for Android Enterprise. For more information about requirements and support, see:
    * [Android Enterprise help - General FAQs](https://support.google.com/work/android/answer/14772109?hl=en#zippy=%2cif-my-device-is-not-android-enterprise-recommended-aer-can-i-still-use-android-enterprise)
    * [Check & fix Play Protect certification status](https://support.google.com/googleplay/answer/7165974?hl=en#zippy=%2Cdevice-isnt-certified)

## Set up Android Enterprise dedicated device management

To set up Android Enterprise dedicated device management, follow these steps:

1. To prepare to manage mobile devices, you must [set the mobile device management (MDM) authority to **Microsoft Intune**](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you're first setting up Intune for mobile device management.
2. [Connect your Intune tenant account to your Managed Google Play account](connect-intune-android-enterprise.md).
3. [Create an enrollment profile.](#create-an-enrollment-profile)
4. [Create a device group](#create-a-device-group).
5. [Enroll the dedicated devices](#enroll-the-dedicated-devices).

### Create an enrollment profile

> [!NOTE]
> After a token expires, the profile associated with it disappears from view under Android enrollment > **Enrollment Profiles** > **Corporate-owned dedicated devices**. To see all profiles associated with both active and inactive tokens, choose **Filter**. Then select the checkboxes for **Active** and **Inactive** policy states.

You must create an enrollment profile so that you can enroll your dedicated devices. When the profile is created, it provides you with an enrollment token in the form of a string and QR code.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices**, and then under **Device onboarding** select **Enrollment**.
3. Select the **Android** tab.
4. In the **Enrollment Profiles** section, choose **Corporate-owned dedicated devices**.
5. Select **Create profile**.
6. Enter the basics for your profile:
    - **Name**: Give your profile a name so you can easily identify it later.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Token type**: Choose the type of token you want to use to enroll dedicated devices.
        - **Corporate-owned dedicated device (default)**: This token enrolls devices as a standard Android Enterprise dedicated device. These devices require no user credentials at any point. This is the default token type that dedicated devices will enroll with unless updated by Admin at time of token creation.
        - **Corporate-owned dedicated device with Microsoft Entra ID shared mode**: This token enrolls devices as a standard Android Enterprise dedicated device and, during enrollment, deploys Microsoft's Authenticator app configured into Microsoft Entra shared device mode. With this option, users can achieve single sign-in and single sign-out across apps on the device that are integrated with the Microsoft Entra Microsoft Authentication Library and global sign-in/sign-out calls.
    - **Token expiration date**: Enter the date you want the token to expire, up to 65 years in the future. The token expires on the selected date at 12:59:59 PM in the time zone it was created. Acceptable date format: `MM/DD/YYYY` or `YYYY-MM-DD`

    - **Naming Template**: The default behavior names devices using properties of the device, such as enrollment type, device ID, and time of enrollment. Example: *AndroidForWork_01/01/2025_12:00 PM*

       To create a custom naming template:

         1. Under **Apply device name template**, choose **Yes**.

         2. Enter the naming template you want to apply to the devices. Names can contain letters, numbers, and hyphens.

         You can use the following strings to create your naming template. Intune replaces the strings with device-specific values.

         - {{SERIAL}} for the device's serial number.

         - {{SERIALLAST4DIGITS}} for the last 4 digits of the device’s serial number.

         - {{DEVICETYPE}} for the device type. Example: *AndroidForWork*

         - {{ENROLLMENTDATETIME}} for the date and time of enrollment.

         - {{UPNPREFIX}} for the user's first name. Example: *Eric*, when device is user affiliated.

         - {{USERNAME}} for the user's username when the device is user affiliated. Example: *EricSolomon*

         - {{RAND:x}} for a random string of numbers, where *x* is between 1 and 9 and indicates the number of digits to add. Intune adds the random digits to the end of the name.

         Edits you make to the naming template only apply to new enrollments.

    - **Token expiration date**: Enter the date you want the token to expire, up to 65 years in the future. The token expires on the selected date at 12:59:59 PM in the time zone it was created. Acceptable date format: `MM/DD/YYYY` or `YYYY-MM-DD`

1. Select **Next** to continue to **Device group**.
1. Optionally, select where to group devices at enrollment time. Select **Search by group name**. Then find and select a static Microsoft Entra device group. For information about how to create a device group to use for grouping, see [Set up enrollment time grouping](enrollment-time-grouping.md).

   > [!TIP]
   > Be sure to select a device group, not a user group.

7. Select **Next** to continue to **Scope tags**.
8.  Optionally, apply one or more scope tags to limit profile visibility and management to certain admin users in Intune. For more information about how to use scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
9. Select **Next** to continue to **Review + create**.
10. Review your choices, and then select **Create** to finish creating the profile.

### Access enrollment token
Access the enrollment token in the admin center.

1. Go to **Devices** > **Enrollment**.
2. Select the **Android** tab.
3. In the **Enrollment Profiles** section, choose **Corporate-owned dedicated devices**.
4. From the list, select your enrollment profile.
5. Select **Token**.

The token appears as a 20-digit string and a QR code. Use this token to enroll devices via the mechanisms described in [Enroll dedicated, fully managed, or corporate-owned work profile devices](android-dedicated-devices-fully-managed-enroll.md). At the time of enrollment, the device user is prompted for the enrollment token. You can provide the string or QR, as long as it's supported by the Android OS and version of the enrolling device.

### Replace, remove, or export token

Select a token to access these options:

- **Replace token**: Generate a new token that's nearing expiration.
- **Revoke token**: Immediately expire the token. Once revoked, the token is no longer usable. This option is useful if you:
  - Accidentally share the token with an unauthorized party.
  - Complete all enrollments and no longer need the token.
- **Export token**: Export the JSON content of the token. This option is useful for obtaining the JSON content that's needed to configure [Google Zero Touch](android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch) or [Knox Mobile Enrollment](android-samsung-knox-mobile-enroll.md).

When applied, these actions don't have any effect on devices that are already enrolled.

### Create a device group

You can target apps and policies to either assigned or dynamic device groups. You can configure dynamic Microsoft Entra device groups to automatically populate devices that are enrolled with a particular enrollment profile by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Groups** > **All groups** > **New group**.
2. Complete all required fields as follows:
    - **Group type**: Security
    - **Group name**: Type an intuitive name, like *Factory 1 devices*
    - **Membership type**: Dynamic Device
3. Choose **Add dynamic query**.
4. On the Dynamic membership rules page, complete all fields as follows:

    - **Property**: enrollmentProfileName
    - **Operator**: Equals
    - **Value**: Enter the enrollment profile name that you created earlier.

    For more information about dynamic membership rules, see [Dynamic membership rules for groups in Microsoft Entra ID](/azure/active-directory/users-groups-roles/groups-dynamic-membership).
5. Choose **Save** to finalize the rule.

## Enroll the dedicated devices

You can now [enroll your dedicated devices](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> The Microsoft Intune app will be automatically installed during enrollment of a dedicated device.  This app is required for enrollment and cannot be uninstalled.
> The Microsoft Authenticator app will be automatically installed during enrollment of a dedicated device when using the token type **Corporate-owned dedicated device with Microsoft Entra ID shared mode**. This app is required for this enrollment method and cannot be uninstalled.

## Managing apps on Android Enterprise dedicated devices

Only apps that have assignment type [set to Required](../apps/apps-deploy.md#assign-an-app) can be installed on Android Enterprise dedicated devices. Apps are installed from the Managed Google Play store in the same manner as Android Enterprise personal and corporate owned work profile devices.

Apps are automatically updated on managed devices when the app developer publishes an update to Google Play.

To remove an app from Android Enterprise dedicated devices, you can do either of the following:

- Delete the required app deployment.
- Create an uninstall deployment for the app.

## Next steps

- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)
