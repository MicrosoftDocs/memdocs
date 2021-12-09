---
# required metadata

title: Setup Intune enrollment for Android Enterprise dedicated devices
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise dedicated devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Set up Intune enrollment of Android Enterprise dedicated devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Android Enterprise supports corporate-owned, single-use, kiosk-style devices with its dedicated devices solution set. Such devices are used for a single purpose, such as digital signage, ticket printing, or inventory management, to name just a few. Admins can lock down the usage of a device to a single app, or a limited set of apps, inclusive of web apps. Users are prevented from adding other apps or taking actions on the device that unless explicitly approved by admins.

Devices that you manage in this way can be enrolled into Intune in two different ways:

1. As a standard Android Enterprise dedicated device. These devices are enrolled into Intune without a user account and are not associated with any end user. These devices          are not intended for personal use applications or apps that have a strong requirement for user-specific account data such as Outlook or Gmail.

2. As a standard Android Enterprise dedicated device that is automatically set up with Microsoft's Authenticator application configured into [Azure AD Shared device mode](/azure/active-directory/develop/msal-shared-devices) during enrollment. These devices are enrolled into Intune without a user account and are not associated with any end user. These devices are intended for use with applications that have integrated with Azure AD's Shared device mode to allow for single sign-in and single sign-out between users across participating applications.

Intune helps you deploy apps and settings to Android Enterprise dedicated devices. For specific details about Android Enterprise, see [Android enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## Device requirements

Devices must meet these requirements to be managed as an Android Enterprise dedicated device:

- Android OS version 6.0 and above.
- Devices must run a distribution of Android that has Google Mobile Services (GMS) connectivity. Devices must have GMS available and must be able to connect to GMS.

## Set up Android Enterprise dedicated device management

To set up Android Enterprise dedicated device management, follow these steps:

1. To prepare to manage mobile devices, you must [set the mobile device management (MDM) authority to **Microsoft Intune**](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you're first setting up Intune for mobile device management.
2. [Connect your Intune tenant account to your Managed Google Play account](connect-intune-android-enterprise.md).
3. [Create an enrollment profile.](#create-an-enrollment-profile)
4. [Create a device group](#create-a-device-group).
5. [Enroll the dedicated devices](#enroll-the-dedicated-devices).

### Create an enrollment profile

> [!NOTE]
> If a token has expired, the profile associated with it will not be displayed in **Device enrollment** > **Android enrollment** > **Corporate-owned dedicated devices**. To see all profiles associated with both active and inactive tokens, click on **Filter** and check the boxes for both "Active" and "Inactive" policy states.

You must create an enrollment profile so that you can enroll your dedicated devices. When the profile is created, it provides you with an enrollment token (random string) and a QR code. Depending on the Android OS and version of the device, you can use either the token or QR code to [enroll the dedicated device](#enroll-the-dedicated-devices).

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Android** > **Android enrollment** > **Corporate-owned dedicated devices**.
2. Choose **Create** and fill out the required fields.
    - **Name**: Type a name that you'll use when assigning the profile to the dynamic device group.
    - **Token type**: Choose the type of token you want to use to enroll dedicated devices.
        - **Corporate-owned dedicated device (default)**: This token enrolls devices as a standard Android Enterprise dedicated device. These devices require no user credentials at any point. This is the default token type that dedicated devices will enroll with unless updated by Admin at time of token creation.
        - **Corporate-owned dedicated device with Azure AD shared mode**: This token enrolls devices as a standard Android Enterprise dedicated device and, during enrollment, deploys Microsoft's Authenticator app configured into Azure AD Shared device mode. With this option, users can achieve single sign-in and single sign-out across apps on the device that are integrated with the Azure AD Microsoft Authentication Library and global sign-in/sign-out calls.
    - **Token expiration date**: The date when the token expires. Google enforces a maximum of 90 days.
3. Choose **Create** to save the profile.

### Create a device group

You can target apps and policies to either assigned or dynamic device groups. You can configure dynamic Azure AD device groups to automatically populate devices that are enrolled with a particular enrollment profile by following these steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Groups** > **All groups** > **New group**.
2. In the **Group** blade, fill out the required fields as follows:
    - **Group type**: Security
    - **Group name**: Type an intuitive name (like Factory 1 devices)
    - **Membership type**: Dynamic device
3. Choose **Add dynamic query**.
4. In the **Dynamic membership rules** blade, fill out the fields as follows:
    - **Add dynamic membership rule**: Simple rule
    - **Add devices where**: enrollmentProfileName
    - In the middle box, choose **Equals**.
    - In the last field, enter the enrollment profile name that you created earlier.
    For more information about dynamic membership rules, see [Dynamic membership rules for groups in Azure AD](/azure/active-directory/users-groups-roles/groups-dynamic-membership).
5. Choose **Add query** > **Create**.

### Replace or remove tokens

- **Replace token**: You can generate a new token/QR code when one nears expiration by using Replace Token.
- **Revoke token**: You can immediately expire the token/QR code. From this point on, the token/QR code is no longer usable. You might use this option if you:
  - accidentally share the token/QR code with an unauthorized party
  - complete all enrollments and no longer need the token/QR code

Replacing or revoking a token/QR code won't have any effect on devices that are already enrolled.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Android** > **Android enrollment** > **Corporate-owned dedicated devices**.
2. Choose the profile that you want to work with.
3. Choose **Token**.
4. To replace the token, choose **Replace token**.
5. To revoke the token, choose **Revoke token**.

## Enroll the dedicated devices

You can now [enroll your dedicated devices](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> The **Microsoft Intune** app will be automatically installed during enrollment of a dedicated device.  This app is required for enrollment and cannot be uninstalled.
> The **Microsoft Authenticator** app will be automatically installed during enrollment of a dedicated device when using the token type **Corporate-owned dedicated device with Azure AD shared mode**. This app is required for this enrollment method and cannot be uninstalled.

## Managing apps on Android Enterprise dedicated devices

Only apps that have Assignment type [set to Required](../apps/apps-deploy.md#assign-an-app) can be installed on Android Enterprise dedicated devices. Apps are installed from the Managed Google Play store in the same manner as Android Enterprise personally-owned and corporate-owned work profile devices.

Apps are automatically updated on managed devices when the app developer publishes an update to Google Play.

To remove an app from Android Enterprise dedicated devices, you can do either of the following:

- Delete the Required app deployment.
- Create an uninstall deployment for the app.

## Next steps

- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)