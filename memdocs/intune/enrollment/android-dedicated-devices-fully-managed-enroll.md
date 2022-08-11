---
# required metadata

title: Enroll Android Enterprise dedicated, fully managed, or corporate-owned work profile devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise dedicated, fully managed, or corporate-owned work profile devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/08/2022
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

To use this method, Zero Touch must be supported on devices and affiliated with a supplier that is part of the service. For more information, see [Android for Enterprise]](https://www.android.com/enterprise/management/zero-touch/)(opens Android website).  

### Step 1 - Add required permission     
The *update app sync* permission is required to enable Zero Touch configuration in the admin center. You can create a new custom role and add the permission or you can edit an existing role, as described in the following steps. 

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

### Step 2 - Enable enrollment for corporate-owned devices  
1. In the admin center, go to **Devices** > **Enroll devices**.  
2. Select **Android enrollment**. 
3. Under **Enrollment profiles**, choose **Corporate-owned, fully managed user devices**.  
4. Verify that the setting for **Allow users to enroll corporate-owned user devices**, is set to **Yes**.  


### Step 3 - Configure Zero Touch  

1. Return to the **Android enrollment** page.  
2. Under **Bulk enrollment methods**, choose **Zero-touch enrollment**.  
3. The Zero Touch console opens.  Select **Next** to begin setup.   
4. Sign in with a Managed Google account that's not linked to Microsoft Intune.  
5. Create a new configuration in the Zero Touch console. 
6. Choose **Microsoft Intune** from the EMM DPC dropdown.
7. In Google's Zero Touch console, copy/paste the following JSON into the DPC extras field. Replace the *YourEnrollmentToken* string with the enrollment token you created as part of your enrollment profile. Be sure to surround the enrollment token with double quotes.

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
        }
    }
    ```

8. Choose **Apply**.  

## Enroll by using Knox Mobile Enrollment
To use Samsung's Knox Mobile Enrollment, the device must be running Android OS version 8.0 or later and Samsung Knox 2.8 or higher. For more information, learn [how to automatically enroll your devices with Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md).  

## Next steps

- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)
