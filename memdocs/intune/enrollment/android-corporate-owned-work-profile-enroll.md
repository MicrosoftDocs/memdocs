---
# required metadata

title: Set up Android Enterprise work profile for corporate owned devices
titleSuffix: Microsoft Intune
description: Set up Android Enterprise work profile for corporate-owned devices enrolling in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/28/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile

Android Enterprise corporate-owned devices with a work profile are single user devices intended for corporate and personal use.

End users can keep their work and personal data separate and are guaranteed that personal data and applications remain private. Admins can control some settings and features for the entire device, including: 

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
> - Tokens for corporate-owned devices with a work profile will not expire automatically. If an admin decides to revoke a token , the profile associated with it will not be displayed in **Devices** > **By platform** > **Android** > **Device onboarding** > **Enrollment** > **Corporate-owned devices with work profile**. To see all profiles associated with both active and inactive tokens, click on **Filter** and check the boxes for both "Active" and "Inactive" policy states.
> - For corporate-owned work profile (COPE) devices, the `afw#setup` enrollment method and the Near Field Communication (NFC) enrollment method are only supported on devices running Android 8-10. They are not available on Android 11. For more information, see the Google developer docs [here](https://developers.google.com/android/management/provision-device#company-owned_devices_for_work_and_personal_use:~:text=Note%3A%20DPC%20identifier%20method%20only%20supports%20full%20device%20management%20provisioning%20and%20cannot%20be%20used%20for%20corporate%2Downed%2C%20personally%20enabled,(COPE)%20provisioning%20on%20Android%2011%20devices.,-Company%2Downed).

You must create an enrollment profile so that users can enroll corporate-owned work profile devices. When the profile is created, it provides you with an enrollment token (random string) and a QR code. Depending on the Android OS and version of the device, you can use either the token or QR code to [enroll the dedicated device](#enroll-the-corporate-owned-work-profile-devices).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  

2. Go to **Devices** > **Enrollment**.  

3. Select the **Android** tab.  

4. Under **Android Enterprise** > **Enrollment Profiles**, choose **Corporate-owned devices with work profile**.  

5. Select **Create profile**.  

6. Enter the basics for your profile:

    - **Name**: Give the profile a name. Note the name down for later, because you need it when you set up the dynamic device group.   

    - **Description**: Enter a description for the profile. This setting is optional, but recommended.   
    - **Token type**: Choose the type of token you want to use to enroll devices. For more information, see [Token types](#token-types) in this article. Your options:  

      - **Corporate-owned with work profile (default)**
        
      - **Corporate-owned with work profile, via staging**  

    - **Token expiration date**: Only available with the staging token. Enter the date you want the token to expire, up to 65 years in the future. Acceptable date format: `MM/DD/YYYY` or `YYYY-MM-DD` The token expires on the selected date at 12:59:59 PM in the time zone it was created.   

8. Select **Next** to continue to **Scope tags**.  

9. Optionally, apply one or more scope tags to limit restriction visibility and management to certain admin users in Intune. For more information about how to use scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).     

10. Choose **Next** to continue to **Create + review**.  

11. Review your choices, and then select **Create** to finish creating the profile.  

### Access enrollment token  
After you create a profile, Intune generates the token you need for enrollment.  

1. Return to **Devices** > **Enrollment**, and select the Android tab.   

2. In the **Enrollment Profiles** section, choose **Corporate-owned devices with work profile**.  

3. From the list, select your enrollment profile. 

4. Select **Token**. 

Another way to find the token is:  

1. Locate your profile in the list, and then select the **More** (**...**) menu that's next to it.  

2. Select **View enrollment token**.  

The token appears as an eight-digit string and a QR code. Use this token to enroll based on the enrollment mechanisms described in the [Android Enterprise corporate-owned device enrollment document](android-dedicated-devices-fully-managed-enroll.md).

### Revoke or Export tokens

- **Revoke token**: You can immediately expire the token/QR code. From this point on, the token/QR code is no longer usable. You might use this option if you:  

  - Accidentally share the token/QR code with an unauthorized party. 
  - Complete all enrollments and no longer need the token/QR code.  

- **Export token**: You can export the JSON content of the token/QR code. You can use this option to copy/paste JSON content for [Zero Touch Enrollment (ZTE)](android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch) or [Knox Mobile Enrollment (KME)](android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-knox-mobile-enrollment). 

Revoking or exporting a token/QR code doesn't have any effect on devices that are already enrolled.

1. In the admin center, go to **Devices** > **Enrollment**.  
3. Select the **Android** tab.  
4. Under **Android Enterprise** > **Enrollment Profiles**, choose **Corporate-owned devices with work profile**.  
5. Choose the profile that you want to work with.  
6. Choose **Token**.
7. To revoke the token, choose **Revoke token** > **Yes**.  
8. To export the token, choose **Export token**.  

### Create a device group

You can target apps and policies to either assigned or dynamic device groups. You can configure dynamic Microsoft Entra device groups to automatically populate devices that are enrolled with a particular enrollment profile by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
2. Go to **Groups** > **All groups** > **New group**.  
2. Fill out the required fields as follows:  
    - **Group type**: Security
    - **Group name**: Type an intuitive name, like *Factory 1 devices*  
    - **Membership type**: Dynamic device  
3. Select **Add dynamic query**.
4. For **Dynamic membership rules**, fill out the fields as follows:
    - **Add dynamic membership rule**: Simple rule  
    - **Add devices where**: enrollmentProfileName  
    - In the middle box, choose **Equals**.  
    - In the last field, enter the enrollment profile name that you created earlier.
    For more information about dynamic membership rules, see [Dynamic membership rules for groups in Microsoft Entra ID](/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Choose **Add query** > **Create**.  

## Enroll the corporate-owned work profile devices

Users can now [enroll their corporate-owned work profile devices](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> The Microsoft Intune app automatically installs on corporate-owned work profile devices during enrollment. This app is required for enrollment and can't be uninstalled. If you deploy the Intune Company Portal app to a device and the user attempts to launch the app, they will be redirected to the Microsoft Intune app, and the Company Portal app icon will be hidden.
> The Microsoft Authenticator app automatically installs on corporate-owned work profile devices during enrollment. This app is required for enrollment and can't be uninstalled. 

## Token types   
When you create the enrollment profile in the admin center, you have to select a token type. There are two types of tokens. Each type enables a different enrollment flow.   

The default token, *corporate-owned work profile*, enrolls devices into Microsoft Intune as standard Android Enterprise corporate-owned devices with work profiles. This token requires you to complete pre-provisioning steps before you distribute the devices. End users complete the remaining steps on the device when they sign in with their work or school account. 

The device staging token, *Corporate-owned work profile, via staging*, enrolls devices into Microsoft Intune in a staging mode so that you or a partner vendor can complete all pre-provisioning steps. End users complete the last step of provisioning by signing into the Microsoft Intune app with their work or school account. Devices are ready to use upon sign-in. Intune supports device staging for Android Enterprise devices running Android 8 or later.  

For more information, see [Device staging overview](device-staging-overview.md).  

## Managing apps on Android Enterprise corporate-owned work profile devices

Apps are installed from the Managed Google Play store in the same manner as Android Enterprise personally owned work profile devices. 

Apps are automatically updated on managed devices when the app developer publishes an update to Google Play.

To remove an app from Android Enterprise corporate-owned work profile devices, you can either: 
- Delete the Required app deployment.
- Create an uninstall deployment for the app.  

## Limitations 

The limitations in this section apply to corporate-owned devices with a work profile.    

Private space is a feature introduced with Android 15 that lets people create a space on their device for sensitive apps and data they want to keep hidden. The private space is considered a personal profile. Microsoft Intune doesn't support mobile device management within the private space or provide technical support for devices that attempt to enroll the private space.     

## Next steps
- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)
