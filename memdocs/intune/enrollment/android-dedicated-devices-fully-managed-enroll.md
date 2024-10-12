---
# required metadata

title: Enroll Android Enterprise dedicated, fully managed, or corporate-owned work profile devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise dedicated, fully managed, or corporate-owned work profile devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/27/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla, chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Enroll your Android Enterprise dedicated, fully managed, or corporate-owned with work profile devices

> [!IMPORTANT]
>  Device users shouldn't restart devices until enrollment is complete. If device users setting up fully managed devices or corporate-owned devices with a work profile restart their devices in the middle of enrollment, their devices may not be able to register with Microsoft Intune. Devices that restarted may appear to be enrolled but they won't be protected by your Intune policies.  

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
> If you have a Microsoft Entra Conditional Access policy defined that uses the *require a device to be marked as compliant* Grant control or a Block policy and applies to **All Cloud apps**, **Android**, and **Browsers**, you must exclude the **Microsoft Intune** cloud app from this policy. This is because the Android setup process uses a Chrome tab to authenticate your users during enrollment. For more information, see [Microsoft Entra Conditional Access documentation](/azure/active-directory/conditional-access/).  

## Enroll by using a QR code  

Intune admins can scan the QR code directly from the enrollment profile to enroll a device. We recommend this enrollment method for most customer scenarios.   

1. After you wipe the device, tap the first screen you see repeatedly to launch the QR reader.    
2. If prompted to, install a QR reader on your device. Devices running Android 9.0 and later are preinstalled with a QR reader.  
3. Scan the enrollment profile QR code, and then follow the on-screen prompts to complete enrollment.  
    > [!TIP]
    > Browser zoom settings may prevent your device from scanning the QR code. Zoom in and try again if your device has difficulty scanning the code.   

## Enroll by using Google Zero Touch 

>[!IMPORTANT]
> Devices must be purchased from an authorized zero-touch reseller and support zero-touch enrollment. For more information, such as prerequisites, where to purchase devices, and how to associate a Google Account with your corporate email, see [Zero-touch enrollment for IT admins](https://support.google.com/work/android/answer/7514005) (opens Android Enterprise Help docs).    

This method utilizes zero-touch enrollment and the Google zero-touch enrollment portal to provision and enroll company-owned devices. Provisioning begins right out of the box when users turn their devices on. This section describes how to:    
* Create a zero-touch configuration with provisioning details in the Microsoft Intune admin center.    
* Create a zero-touch configuration with provisioning details in the zero-touch enrollment portal.    

### Create zero-touch configuration in admin center        
The zero-touch iframe gives you access to the zero-touch enrollment portal and zero-touch configurations in the Microsoft Intune admin center. 
  
To enable the iframe, you must first add the *update app sync* permission and enable enrollment for corporate-owned, fully managed devices. Once you enable the iframe, you can:  

  * Link your zero-touch account to Intune  
  * Add support information  
  * Configure zero-touch enabled devices  
  * Customize provisioning extras  

Complete the steps in this section to enable the iframe. To create configurations in the zero-touch enrollment portal instead, skip to [Create configuration in zero-touch enrollment portal](android-dedicated-devices-fully-managed-enroll.md#create-configuration-in-zero-touch-enrollment-portal).  

#### Step 1: Add required permission   
Add the *update app sync* permission.     

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
admin.
2. Select **Tenant administration** > **Roles**. 
3. Select your role from the list.  
4. Select **Properties**.
5. Go to **Permissions** and then select **Edit**.  
6. Select **Android Enterprise**.  
7. Next to **Update app sync**, select **Yes**.
8. Select **Review + save** to review your changes.  
9. Select **Save**.  

#### Step 2: Enable enrollment for corporate-owned devices  
Verify that enrollment is enabled for corporate-owned, fully managed devices.   

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **By platform** > **Android**.  
2. Select **Android enrollment**. 
3. Under **Enrollment profiles**, choose **Corporate-owned, fully managed user devices**.  
4. Verify that the setting for **Allow users to enroll corporate-owned user devices**, is set to **Yes**.             

#### Step 3: Link zero-touch account to Intune    
Link a zero-touch account with your Microsoft Intune account.   

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **By platform** > **Android**.  
2. Select **Device onboarding** > **Enrollment**.  
3. Under **Bulk enrollment methods**, choose **Zero-touch enrollment**.  
4. The iframe opens.  Select **Next** to begin setup.   
5. Sign in with the Google account you provided to your reseller. 
6. Select the zero-touch account you want to link, and then select **Link**.  
7. A default configuration is created. A screen appears with basic information about the configuration. Intune will automatically apply the default configuration to any zero-touch enabled device that's without an existing configuration.  

   > [!CAUTION]
   > The token used for the default configuration is meant for a fully managed device. Once you link your account, the default zero-touch configuration created in Intune overrules the default configuration profile set in the zero-touch enrollment portal. If you want to create a zero-touch configuration for a corporate-owned work profile device or a dedicated device, don't link your account to Intune. Instead, select **View devices in the zero-touch portal**. Then continue to [Create configuration in zero-touch enrollment portal](android-dedicated-devices-fully-managed-enroll.md#create-configuration-in-zero-touch-enrollment-portal) in this article for next steps.  

8. Select **Next** to continue.  
9. Add support information to assist device users during setup.  
10. Select **Save**.  

Once your account is linked with Intune, the default configuration is applied to zero-touch enabled devices that don't already have a configuration, and to future devices added by a reseller. You can view existing zero-touch configurations, edit support information, unlink the account, and link other accounts in the admin center. 

### Create configuration in zero-touch enrollment portal        

Add a zero-touch configuration in the [zero-touch enrollment portal](https://enterprise.google.com/android/zero-touch/customers). You can use the portal by itself to manage configurations, or you can use it in combination with the zero-touch iframe. The portal supports configurations for fully managed and dedicated devices, and corporate-owned devices with a work profile. 

1. Sign in to the zero-touch enrollment portal with your Google account.
2. Select the option to add a new configuration.  
3. Fill out the information in the configuration panel. 
4. Select **Microsoft Intune** as the EMM DPC app.   
5. Copy the following JSON text into the DPC extras field. Replace `YourEnrollmentToken` with the enrollment token you created as part of your enrollment profile. Be sure to surround the enrollment token with double quotes.  

    ```json
    {
    "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",
    "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",
    "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",
    "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
        "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
    }
    }

 6. Enter your organization's name and support information, which is shown on screen while users set up their devices.   
 
For more information about how to assign a default configuration or apply a configuration in the zero-touch portal, see [Zero-touch enrollment for IT admins](https://support.google.com/work/android/answer/7514005) (opens Android Enterprise Help docs).  

## Enroll by using Knox Mobile Enrollment
To use Samsung Knox Mobile Enrollment, the device must be running Android OS version 8.0 or later and Samsung Knox 2.8 or higher. For more information, learn [how to automatically enroll your devices with Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md).  

## Enroll by using Near Field Communication (NFC)

Create a specially formatted NFC tag to provision NFC-supported devices running Android 8.0 or later. You can use your own app or any NFC tag-creation tool. For more information, see [C-based Android Enterprise device enrollment with Microsoft Intune](/archive/blogs/cbernier/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune) and [Google's Android Management API documentation](https://developers.google.com/android/management/provision-device#nfc_method).  

For corporate-owned work profile (COPE) devices, the NFC enrollment method is only supported on devices running Android versions 8.0 or later. It's not supported with Android 11.0. For more information, see the [Google developer docs](https://developers.google.com/android/management/provision-device#company-owned_devices_for_work_and_personal_use:~:text=Note%3A%20DPC%20identifier%20method%20only%20supports%20full%20device%20management%20provisioning%20and%20cannot%20be%20used%20for%20corporate%2Downed%2C%20personally%20enabled,(COPE)%20provisioning%20on%20Android%2011%20devices.,-Company%2Downed).  

## Enroll by using a token  
We recommend this method for new or factory-reset devices, in scenarios where the QR code or NFC method aren't available. It requires the person provisioning the device to type in the enrollment token string (example: `12345`) that they're provided. When you're ready for enrollment, share the token directly with targeted users or post it to your organization's support site for easy retrieval. The token works for all Intune-licensed users and doesn't expire.   

This method is supported on corporate-owned devices running Android 8.0 and later. It isn't supported on: 

* Corporate-owned, personally enabled (COPE) devices running Android 11 and later.  
* Devices enrolled via device enrollment manager accounts.    

You can use this method in conjunction with the Microsoft Intune DPC identifier to set up fully managed devices.

1. Turn on the device.  
2. On the **Welcome** screen, select your language.  
3. Connect to your wireless network, and then choose **NEXT**.  
4. Accept the Google Terms and conditions, and then choose **NEXT**.  
5. On the Google sign-in screen, enter **afw#setup** instead of a Gmail account. This value is the DPC identifier for Microsoft Intune. Choose **NEXT**. 
6. Choose **INSTALL** for the Android Device Policy app.  
7. Continue to install the policy. Some devices may require additional terms acceptance.
8. On the **Enroll this device** screen, allow your device to scan the QR code. Or, enter the token manually.
9. Follow the on-screen prompts to complete enrollment.

For more information about provisioning devices with the DPC identifier method, see the [Google developer docs](https://developers.google.com/android/management/provision-device#company-owned_devices_for_work_and_personal_use:~:text=Note%3A%20DPC%20identifier%20method%20only%20supports%20full%20device%20management%20provisioning%20and%20cannot%20be%20used%20for%20corporate%2Downed%2C%20personally%20enabled,(COPE)%20provisioning%20on%20Android%2011%20devices.,-Company%2Downed).   

## Next steps

- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)
