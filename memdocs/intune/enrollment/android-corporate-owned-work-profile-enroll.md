---
# required metadata

title: Setup Intune enrollment for Android Enterprise corporate-owned devices with corporate-owned work profile
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise corporate-owned devices with work profile in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/22/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile

Android Enterprise corporate-owned devices with a work profile are single user devices intended for corporate and personal use.

End users can keep their work and personal data separate and are guaranteed that their personal data and applications will remain private. Admins can control some settings and features for the entire device, including:

- Setting requirements for the device password
- Controlling Bluetooth and data roaming
- Configuring factory reset protection

Intune helps you deploy apps and settings to Android Enterprise corporate-owned devices with work profile. For specific details about Android Enterprise, see [Android enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## Device requirements

Devices must meet these requirements to be managed as Android Enterprise corporate-owned work profile devices:

- Android OS version 8.0 and above.
- Devices must run a distribution of Android that has Google Mobile Services (GMS) connectivity. Devices must have GMS available and must be able to connect to GMS.

## Set up Android Enterprise corporate-owned work profile device management

To set up Android Enterprise corporate-owned work profile device management, follow these steps:

1. To prepare to manage mobile devices, you must [set the mobile device management (MDM) authority to **Microsoft Intune**](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you're first setting up Intune for mobile device management.
2. [Connect your Intune tenant account to your Managed Google Play account](connect-intune-android-enterprise.md).
3. [Create an enrollment profile.](#create-an-enrollment-profile)
4. [Create a device group](#create-a-device-group).
5. [Enroll the corporate-owned work profile devices](#enroll-the-corporate-owned-work-profile-devices).

### Create an enrollment profile

> [!NOTE]
> - Tokens for corporate-owned devices with a work profile will not expire automatically. If an admin decides to revoke a token , the profile associated with it will not be displayed in **Devices** > **Android** > **Android enrollment** > **Corporate-owned devices with work profile**. To see all profiles associated with both active and inactive tokens, click on **Filter** and check the boxes for both "Active" and "Inactive" policy states.
> - For corporate-owned work profile (COPE) devices, the `afw#setup` enrollment method and the Near Field Communication (NFC) enrollment method are only supported on devices running Android 8-10. They are not available on Android 11. For further details, refer to the Google developer docs [here](https://developers.google.com/android/management/provision-device#company-owned_devices_for_work_and_personal_use:~:text=Note%3A%20DPC%20identifier%20method%20only%20supports%20full%20device%20management%20provisioning%20and%20cannot%20be%20used%20for%20corporate%2Downed%2C%20personally%20enabled,(COPE)%20provisioning%20on%20Android%2011%20devices.,-Company%2Downed).

You must create an enrollment profile so that users can enroll corporate-owned work profile devices. When the profile is created, it provides you with an enrollment token (random string) and a QR code. Depending on the Android OS and version of the device, you can use either the token or QR code to [enroll the dedicated device](#enroll-the-corporate-owned-work-profile-devices).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Android** > **Android enrollment** > **Corporate-owned devices with work profile**.
2. Choose **Create profile** and fill out the fields.
    - **Name**: Type a name that you'll use when assigning the profile to the dynamic device group.
    - **Description**: Add a profile description (optional).
3. Choose **Next**.
5. On the **Review + create** page, choose **Create** to create the policy.

### Access enrollment token  
After you create a profile, Intune generates a token that's needed for enrollment. There are two ways to access the token:

One way is:
1. Choose **Devices** > **Android** > **Android enrollment** > **Android Enterprise** > **Corporate-owned devices with work profile**.
2. From the list, select your enrollment profile. 
2. Select **Token**. 

Another way to find the token is:
1. Choose **Devices** > **Android** > **Android enrollment** > **Android Enterprise** > **Corporate-owned devices with work profile**.
2. Locate your profile in the list, and then select the **More** (**...**) menu that's next to it.
3. Select **View enrollment token**.  

The token appears as an eight-digit string and a QR code. Use this token to enroll based on the enrollment mechanisms described in the [Android Enterprise corporate-owned device enrollment document](/mem/intune/enrollment/android-dedicated-devices-fully-managed-enroll). 

### Revoke or Export tokens

- **Revoke token**: You can immediately expire the token/QR code. From this point on, the token/QR code is no longer usable. You might use this option if you:
  - accidentally share the token/QR code with an unauthorized party
  - complete all enrollments and no longer need the token/QR code
- **Export token**: You can export the JSON content of the token/QR code. You might use this option to easily paste JSON content to enroll with [Zero Touch Enrollment (ZTE)](/mem/intune/enrollment/android-dedicated-devices-fully-managed-enroll#enroll-by-using-google-zero-touch) or [Knox Mobile Enrollment (KME)](/mem/intune/enrollment/android-dedicated-devices-fully-managed-enroll#enroll-by-using-knox-mobile-enrollment). 

Revoking or exporting a token/QR code won't have any effect on devices that are already enrolled.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Android** > **Android enrollment** > **Corporate-owned devices with work profile**.
2. Choose the profile that you want to work with.
3. Choose **Token**.
5. To revoke the token, choose **Revoke token** > **Yes**.
6. To export the token, choose **Export token**.

### Create a device group

You can target apps and policies to either assigned or dynamic device groups. You can configure dynamic Azure AD device groups to automatically populate devices that are enrolled with a particular enrollment profile by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Groups** > **All groups** > **New group**.
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

## Enroll the corporate-owned work profile devices

Users can now [enroll their corporate-owned work profile devices](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> The Microsoft Intune app is automatically installed during enrollment. This app is required for enrollment and can't be uninstalled.  If you deploy the Intune Company Portal app to a device and the user attempts to launch the app, they will be redirected to the Microsoft Intune app, and the Company Portal app icon will be hidden.  

## Managing apps on Android Enterprise corporate-owned work profile devices

Apps are installed from the Managed Google Play store in the same manner as Android Enterprise personally-owned work profile devices.

Apps are automatically updated on managed devices when the app developer publishes an update to Google Play.

To remove an app from Android Enterprise corporate-owned work profile devices, you can do either of the following:
- Delete the Required app deployment.
- Create an uninstall deployment for the app.

## Next steps
- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)
