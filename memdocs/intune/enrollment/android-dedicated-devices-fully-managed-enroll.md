---
# required metadata

title: Enroll Android Enterprise dedicated devices or fully managed devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise dedicated devices or fully managed devices in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: conceptual
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
ms.collection: M365-identity-device-management
---

# Enroll your Android Enterprise dedicated devices or fully managed devices

After you've set up your [Android Enterprise dedicated devices](android-kiosk-enroll.md) or [fully managed devices](android-fully-managed-enroll.md) in Intune, you can enroll the devices. Intune enrollment for both dedicated devices and fully managed devices start with a factory reset. How you enroll your Android Enterprise devices depends on the operating system.

| Enrollment method | Minimum Android OS version for dedicated and fully managed devices |
| ----- | ----- |
| Near Field Communication | 6.0 |
| Token entry | 6.0 |
| QR code | 7.0 |
| Zero Touch  | 8.0\* |

\* On participating manufacturers.

## Enroll by using Near Field Communication (NFC)

For devices 6 and later that support NFC, you can provision your devices by creating a specially formatted NFC tag. You can use your own app or any NFC tag creator tool. For more information, see [C-based Android Enterprise device enrollment with Microsoft Intune](https://blogs.technet.microsoft.com/cbernier/2018/10/15/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune/) and [Google's Android Management API documentation](https://developers.google.com/android/management/provision-device#nfc_method).

## Enroll by using a token

For Android 6 and later devices, you can use the token to enroll the device. Android 6.1 and later versions can also leverage QR code scanning when using the **afw#setup** enrollment method.

1. Turn on your wiped device.
2. On the **Welcome** screen, select your language.
3. Connect to your **Wifi** and then choose **NEXT**.
4. Accept the Google Terms and conditions and then choose **NEXT**.
5. On the Google sign-in screen, enter **afw#setup** instead of a Gmail account, and then choose **NEXT**.
6. Choose **INSTALL** for the **Android Device Policy** app.
7. Continue installation of this policy.  Some devices may require additional terms acceptance.
8. On the **Enroll this device** screen, allow your device to scan the QR code or choose to enter the token manually.
9. Follow the on-screen prompts to complete enrollment.

## Enroll by using a QR code

On Android 7 and later devices, you can scan the QR code from the enrollment profile to enroll the device.

> [!Note]
> Browser zoom can cause devices to not be able to scan QR code. Increasing the browser zoom resolves the issue.

1. To launch a QR read on the Android device, tap multiple times on the first screen you see after a wipe.
2. For Android 7 and 8 devices, you'll be prompted to install a QR reader. Android 9 and later devices already have a QR reader installed.
3. Use the QR reader to scan the enrollment profile QR code and then follow the on-screen prompts to enroll.

## Enroll by using Google Zero Touch

To use Google's Zero Touch system, the device must support it and be affiliated with a supplier that is part of the service.  For more information, see [Google's Zero Touch program website](https://www.android.com/enterprise/management/zero-touch/).

1. Create a new Configuration in the Zero Touch console.
2. Choose **Microsoft Intune** from the EMM DPC dropdown.
3. In Google's Zero Touch console, copy/paste the following JSON into the DPC extras field. Replace the *YourEnrollmentToken* string with the enrollment token you created as part of your enrollment profile. Be sure to surround the enrollment token with double quotes.

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

4. Choose **Apply**.


## Next steps
- [Deploy Android apps](../apps/apps-deploy.md)
- [Add Android configuration policies](../configuration/device-profiles.md)

