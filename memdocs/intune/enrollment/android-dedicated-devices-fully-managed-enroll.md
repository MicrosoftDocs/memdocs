---
# required metadata

title: Enroll Android Enterprise dedicated, fully managed, or corporate-owned work profile devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise dedicated, fully managed, or corporate-owned work profile devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/16/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla, chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Enroll your Android Enterprise dedicated, fully managed, or corporate-owned with work profile devices

> [!IMPORTANT]
>  It's important that device users do not restart devices until enrollment is complete. If device users setting up fully managed devices or corporate-owned devices with a work profile restart their devices in the middle of enrollment, their devices may not be able to register with Microsoft Intune. Devices that restarted may appear to be enrolled but they won't be protected by your Intune policies.  

After you've set up your Android Enterprise [dedicated devices](android-kiosk-enroll.md), [fully managed devices](android-fully-managed-enroll.md), or [corporate-owned work profile devices](android-corporate-owned-work-profile-enroll.md) in Intune, you can enroll the devices. Intune enrollment for dedicated devices, fully managed devices, and corporate-owned with a work profile start with a factory reset. How you enroll your Android Enterprise devices depends on the operating system.

| Enrollment method | Minimum Android OS version for dedicated and fully managed devices |
| ----- | ----- |
| Near Field Communication | 8.0 |
| Token entry | 8.0 |
| QR code | 8.0 |
| Zero Touch  | 8.0<br><br> On participating manufacturers. |
| [Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md)  | 8.0<br><br> On Samsung Knox 2.8 or higher devices only. |

> [!TIP]
> Corporate-owned work profile (COPE) device management is available on Android version 8.0 and newer.

> [!NOTE]
> If you have an Azure AD Conditional Access policy defined that uses the *require a device to be marked as compliant* Grant control or a Block policy and applies to **All Cloud apps**, **Android**, and **Browsers**, you must exclude the **Microsoft Intune** cloud app from this policy. This is because the Android setup process uses a Chrome tab to authenticate your users during enrollment. For more information, see [Azure AD Conditional Access documentation](/azure/active-directory/conditional-access/).

## Enroll by using Near Field Communication (NFC)

Create a specially-formatted NFC tag to provision NFC-supported devices running Android 8.0 or later. You can use your own app or any NFC tag-creation tool. For more information, see [C-based Android Enterprise device enrollment with Microsoft Intune](/archive/blogs/cbernier/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune) and [Google's Android Management API documentation](https://developers.google.com/android/management/provision-device#nfc_method).

For corporate-owned work profile (COPE) devices, the NFC enrollment method is only supported on devices running Android versions 8.0 to 10.0. It's not supported with Android 11.0 or later. 

## Enroll by using a token

- For Android 8.0 and later devices, you can use the token value, such as `12345`, to enroll the device.
- You can leverage QR code scanning when using the **afw#setup** enrollment method to enroll devices running Android 8.0 and later.  
- For corporate-owned work profile (COPE) devices, the **afw#setup** enrollment method is only supported on devices running Android versions 8.0 to 10.0. It's not supported with Android 11.0 or later. For more information, see the [Google developer docs](https://developers.google.com/android/management/provision-device#company-owned_devices_for_work_and_personal_use:~:text=Note%3A%20DPC%20identifier%20method%20only%20supports%20full%20device%20management%20provisioning%20and%20cannot%20be%20used%20for%20corporate%2Downed%2C%20personally%20enabled,(COPE)%20provisioning%20on%20Android%2011%20devices.,-Company%2Downed).  

### Steps

1. Turn on your wiped device.
2. On the **Welcome** screen, select your language.
3. Connect to your **Wi-fi**, and then choose **NEXT**.
4. Accept the Google Terms and conditions, and then choose **NEXT**.
5. On the Google sign-in screen, enter **afw#setup** instead of a Gmail account, and then choose **NEXT**.
6. Choose **INSTALL** for the **Android Device Policy** app.
7. Continue installation of this policy. Some devices may require additional terms acceptance.
8. On the **Enroll this device** screen, allow your device to scan the QR code. Or, choose to enter the token manually.
9. Follow the on-screen prompts to complete enrollment.

## Enroll by using a QR code

Scan the QR code from the enrollment profile to enroll devices running Android 8.0 and later.   

> [!Note]
> Browser zoom can cause devices to not be able to scan QR code. Increasing the browser zoom resolves the issue.

1. After you wipe the device, tap the first screen you see repeatedly to launch the QR reader.    
2. On devices running Android 8.0, you'll be prompted to install a QR reader. Devices running Android 9 and later are pre-installed with a QR reader.
3. Use the QR reader to scan the enrollment profile QR code and then follow the on-screen prompts to enroll.  

## Enroll by using Google Zero Touch 

To use this method, zero-touch enrollment must be supported on devices and affiliated with a supplier that is part of the Android zero-touch enrollment service. For more information, such as prerequisites, where to purchase devices, and how to set up your Google Account, see [Zero-touch enrollment for IT admins](https://support.google.com/work/android/answer/7514005)(opens Android Enterprise Help). 

This section describes how to:    
* Configure new Android zero-touch configurations in the zero-touch enrollment portal  
* Enable the zero-touch enrollment iframe in the admin center  
* Link a zero-touch account to Microsoft Intune  

### Create zero-touch configuration    

Add a zero-touch configuration in the Google zero-touch enrollment portal.   

1. Sign in to the zero-touch enrollment portal with your Google Account.
2. Select the option to add a new configuration.
3. Fill out the information in the configuration panel. 
4. Select **Microsoft Intune** as the EMM DPC app.   
5. Copy the following JSON test into the DPC extras field. Replace `YourEnrollmentToken` with the enrollment token you created as part of your enrollment profile. Be sure to surround the enrollment token with double quotes.  

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
 6. Enter your organization's name and support information, which is shown on screen while users set up their devices.   
 
For information about how to assign a default configruation or apply a configuration in the zero-touch portal, see [Zero-touch enrollment for IT admins](https://support.google.com/work/android/answer/7514005)(opens Android Enterprise Help).  

### Enable zero-touch iframe    
Complete these steps to enable the zero-touch iframe in the Microsoft Endpoint Manager admin center. The iframe lets you access the Google zero-touch enrollment portal from inside the admin center.     

#### Step 1: Add required permission   
Add the *update app sync* permission.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
admin.
2. Select **Tenant administration** > **Roles**. 
3. Select your role from the list.  
4. Select **Properties**.
5. Go to **Permissions** and then select **Edit**.  
5. Select **Android for Work**.  
6. Next to **Update app sync**, select **Yes**.
9. Select **Review + save** to review your changes.  
9. Select **Save**.  

#### Step 2: Enable enrollment for corporate-owned devices  

1. In the admin center, go to **Devices** > **Enroll devices**.  
2. Select **Android enrollment**. 
3. Under **Enrollment profiles**, choose **Corporate-owned, fully managed user devices**.  
4. Verify that the setting for **Allow users to enroll corporate-owned user devices**, is set to **Yes**.             

### Link zero-touch account to Intune    
Use the zero-touch iframe in the admin center to link a zero-touch account with Microsoft Intune.   

1. In the admin center, go to **Devices** > **Enroll devices**.  
2. Select **Android enrollment**. 
2. Under **Bulk enrollment methods**, choose **Zero-touch enrollment**.  
3. The iframe opens.  Select **Next** to begin setup.   
4. Sign in with the Google account you provided to yuor reseller. 
5. Select the zero-touch account you want to link, and then select **Link**.  
6. A screen appears with basic information about the configuration your devices will use. The configuration will act as the default and be automatically applied to any device that doesn't have an existing configuration. Select **Next** to continue.    

> [!TIP]
> The token used for the default configuration is for a fully managed device. If you want to create a zero-touch configuration for a corporate-owned work profile device or a dedicated device, see [Create configuration in Zero Touch](android-dedicated-devices-fully-managed-enroll.md#create-zero-touch-configuration) (in this article). 
6. Add support information to assist device users during setup. 
7. Select **Save**.  

Once your account is linked with Intune, zero-touch enabled devices are ready to receive the default configuration. You can view existing zero-touch configurations, edit support information, unlink the account, and link other accounts in the admin center. To change or create new configurations, use the steps in [Create a zero-touch configuration](android-dedicated-devices-fully-managed-enroll.md#create-zero-touch-configuration) (in this article).  

## Enroll by using Knox Mobile Enrollment
To use Samsung's Knox Mobile Enrollment, the device must be running Android OS version 8.0 or later and Samsung Knox 2.8 or higher. For more information, learn [how to automatically enroll your devices with Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md).  

## Next steps

- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)
