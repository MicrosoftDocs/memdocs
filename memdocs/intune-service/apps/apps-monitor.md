---
# required metadata

title: Monitor app information and assignments
titleSuffix: Microsoft Intune
description: After you've assigned an app to users or devices, use this information to help you monitor the app's status.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/18/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 64e5133d-1e23-4ee6-b556-f5d32c0e95da

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Monitor app information and assignments with Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune provides several ways to monitor the properties of apps that you manage and to manage app assignment status.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps**.
3. In the list of apps, select an app to monitor. You'll then see the app pane, which includes an overview of the device status and the user status.

> [!NOTE]
> Microsoft Store and Android Store apps that are deployed as **Available** do not report their installation status.
>
> For Managed Google Play apps deployed to Android Enterprise personally-owned work profile devices, you can view the status and version number of the app installed on a device using Intune.
>
> From the **Installed apps** page of the Windows Company Portal or the Company Portal website, end users can view the installation status and details for device-assigned required apps. This functionality is provided in addition to the installation status and details of user-assigned required apps.

## App overview pane

In the app pane, you can review details about the status of an app in your environment.

### Essentials
The **Essentials** section provides the following information about the app if applicable:

 | **App details**            | **Description**                                                      |
|------------------------|------------------------------------------------------------------|
| **Publisher**          | The publisher of the app                                            |
| **Operating system**   | The app operating system (Windows, iOS/iPadOS, Android, and so on) |
| **Version**            | If applicable, the version number of the app |
| **MAM SDK enabled**    | If applicable, whether the app uses the Intune MAM SDK (**Yes** or **No**)                  |
| **Created**             | The date and time when this revision was created <b>**Note**: This date value is updated when an admin changes app metadata, such as changing the app category or app description.                        |
| **Assigned**           | Whether the app has been assigned (**Yes** or **No**)          
| **App package file**   | If applicable, the app package file name            |


### Device and user status graphs
The graphs show the number of apps for the following status:

| **Device status**       | **Description**                                       |
|-----------------------|-------------------------------------------------------|
| **Installed**         | The number of apps installed                         |
| **Not Installed**     | The number of apps not installed                     |
| **Failed**            | The number of failed installations                   |
| **Install Pending**   | The number of apps that are in the process of being installed |
| **Not Applicable**           | The number of apps for which status isn't applicable            |

> [!NOTE]
> Be aware that Android LOB apps (.APK) deployed as **Available with or without enrollment** only report app installation status for enrolled devices. App installation status is not available for devices that are not enrolled in Intune.

### Device install status

A device status list is shown when you select **Device install status** in the **Monitor** section of the menu. The details table includes the following columns:

| **Device column**      | **Description**                                                                                                                                                                                                                                            |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Device name**      | The name of the device on platforms that allow naming a device <b>**Note**: On other platforms, Intune creates a name from other properties. This attribute isn't available to any other device.                                                                       |
| **User name**        | The name of the user                                                                                                                                                                                                                                      |
| **Platform**         | The operating system of the device (Windows, iOS/iPadOS, Android, and so on)                                                                                                                                                                                           |
| **Version**          | The version number of the app <b>**Note**: For line-of-business (LOB) apps, the full version number of the app is shown. The full version number identifies a specific release of the app. The number appears as _Version_(_Build_). For example,  2.2(2.2.17560800). For standard Store apps, no versions are shown. |
| **Status**           | The status of the app                                                                                                                                                                                                                                     |
| **Status details**   | The details of the status                                                                                                                                                                                                                                   |
| **Last check-in**    | The date of the device's last sync with Intune                                                                                                                                                                                                                  |

> [!NOTE]
> Even if the App is targetted to device context and into a device group, the user name will always be reported. You may refer to the corresponded [API Call](/graph/api/intune-apps-mobileappinstallstatus-get). Additionally, the system context may appear as "No user".

### User install status

A user status list is shown when you select **User install status** in the **Monitor** section of the menu. The details table includes the following columns:

| **User column**     | **Description**                           |
|---------------------|-------------------------------------------|
| **Name**            | The name of the user in Microsoft Entra ID     |
| **User name**       | The unique name of the user              |
| **Installations**   | The number of apps installed by the user |
| **Failures**        | The number of failed app installations for the user     |
| **Not installed**   | The number of apps not installed by the user |

## App installation error reporting

Additional error details are available for Line of Business (LOB) apps on Android Open Source Project (AOSP) devices. You can view installation error codes for LOB apps in Intune.

### LOB apps on AOSP devices

The following table provides addition installation error code details for LOB apps on AOSP devices:

| Error code | Error string | Retry automatically | Additional information |
|---|---|---|---|
| 0x87D54FB0 | Couldn't install the app because the user didn't allow it or accept permissions. | Yes | Ask the end user to accept any installation request when prompted. |
| 0x87D54FB1 | The operating system couldn't install the app. | No | The Android system failed to install the app. |
| 0x87D54FB2 | The operating system blocked installation. | Yes | A device policy or the Android package verifier may have blocked the operation. |
| 0x87D54FB3 | Either the user or the system stopped the installation. | Yes | The end user may have declined a permission request or is missing permissions. The OS might also block the APK for security reasons. For example, the APK could have been marked as "dangerous" by Google Play Protect. |
| 0x87D54FB4 | Couldn't install the app because it's corrupt or not valid. | No | The Android system detected the APK as being invalid. This error could have occurred for several reasons. For example, the APK isn't signed, or the package manifest is missing or is malformed. Upload a new APK. Check that the APK wasn't corrupted before upload. |
| 0x87D54FB5 | Installation failed. | No |  |
| 0x87D54FB6 | Couldn't install the app because it conflicts with the version of the app already on the device. Remove the existing app first. | Yes | The conflict could be for a variety of reasons. For example, the package on the device could have a different signature than the one being installed. If the policy is intended to upgrade an existing application, sign the upgraded version with the same certificate used for the original app. If not, uninstall the existing app before deploying the new one. Or, there could be an existing package that defines a permission that the installing app also defines. In that case, the OS rejects the installation because certain permissions can only be owned by one app. Uninstall the existing application for the policy to succeed. |
| 0x87D54FB7 | Install failed. Insufficient storage space on device. | Yes | Free up space on the device. |
| 0x87D54FB8 | Installation failed because this app won't work with the device. | No | Upload a new APK that is compatible with the device architecture and SDK version running on the device, or upgrade the device. |
| 0x87D54FB9 | Installation failed because it took too long. | Yes |  |
| 0x87D54FBA | Installation failed because it took too long. | No |  |
| 0x87D54FBB | Couldn't uninstall the app.  | No |  |
| 0x87D55014 | Couldn't download the app. | Yes | A generic download failure occurred. |
| 0x87D55015 | Couldn't download the app because there's not enough room on the device. | Yes | Free up space on the device. |
| 0x87D55016 | Couldn't download the app because the service gave a bad response. | Yes |  |
| 0x87D55017 | Couldn't download the app because it was too large. | No | The admin uploaded an APK that exceeded the allowable download size of 2GB. Upload a smaller APK. |
| 0x87D55018 | Couldn't download the app because there was no network connection. | Yes | The download resumes when the network resumes. |
| 0x87D55019 | Couldn't download the app because of a network error. | Yes | The download failed due to an unspecified network error. The admin may have a firewall restriction, or something else is blocking the network. The admin could temporarily enroll the device using a different Wi-Fi network, which may allow enrollment SCEP certificates to be installed and more secure firewall rules to take effect. |
| 0x87D5501A | Couldn't download the app. | No | Confirm the network connection and sufficient bandwidth. Additionally, confirm nothing is interfering with network traffic. |
| 0x87D5501B | Couldn't download the app. Contact Microsoft Intune support and include the error code. | No | The app couldn't be downloaded. Contact Microsoft Intune support and include the error code. |
| 0x87D5501C | Couldn't download the app because the downloaded file couldn't be found. | No | The downloaded content was corrupted or deleted before it was installed. The downloaded app files were removed before the app could install. Make sure the app is installed immediately after downloading. Ask the end user to accept the installation request when prompted. |
| 0x87D5501D | Couldn't download the app because of an input/output error. | Yes |  |
| 0x87D5501E | Couldn't download the app because it took too long. | Yes | If a download takes more than 8 hours, Intune cancels and retries the download. |
| 0x87D5501F | The downloaded app couldn't be validated.  | Yes | The hash code of the downloaded content doesn't equal the hash code of the content from the policy. There are multiple reasons this could occur. The OS may not support encryption/decryption. In this case, you should try updating the OS to latest version. Alternatively, an intermittent issue occurred which may have corrupted the download. Lastly, a less likely scenario where this error occurs is due to a machine in the middle (MITM) attack. |
| 0x87D55078 | Couldn't download the app because Intune had an error. | Yes |  |
| 0x87D55079 | Couldn't download the app because of a network error. | Yes | A generic HTTP failure occurred. |
| 0x87D5507A | Couldn't download the app because it doesn't seem to exist or it isn't assigned to this device. | No | While the policy was being applied, the policy was removed by the admin. |
| 0x87D5507B | Couldn't download the app because Intune had an error. | Yes |  |
| 0x87D5507C | Couldn't download the app because Intune had an error. | Yes |  |
| 0x87D5507D | Couldn't download the app because Intune had an error.  | Yes |  |
| 0x87D550DC | The uploaded app is missing the versionCode property. | No | The versionCode is missing from the uploaded APK. For more information on versionCode, see Android documentation. |
| 0x87D550DD | The uploaded app is missing the minSdkVersion value. | No | Ensure the android:minSdkVersion parameter is specified in the APK manifest. |
| 0x87D550DE | The policy is missing the minSdkVersion value. | No | If the admin creates the policy in the admin portal, there's a requirement that the admin specifies what the minimum SDK version the policy supports. If the admin creates the policy by Graph, this property isn't always required. If this parameter is missing, this exception is thrown. |
| 0x87D550DF | Couldn't uninstall this app because there's another policy to install the same app. | No | If you have two policies that target the same package and version, but one is an install and one is an uninstall, the install is applied and the uninstall is marked as a conflict. |
| 0x87D550E0 | Couldn't install this app because there's another policy to install a newer version of the same app. | No | If there is more than one install policy for the same package but with different versions, the policy with the highest package version takes priority. Remove the conflicting policy. |
| 0x87D550E1 | Couldn't find the app on the device. Intune will try to reinstall it. | Yes | Data indicates that the install policy was previously applied successfully (package was installed), but the package isn't found on the device anymore. The end user shouldn't be able to uninstall any required apps, so this scenario is less likely. |
| 0x87D550E2 | Intune will try to uninstall the app.  | Yes | This error may happen if the end user manually reinstalled an app that was supposed to be uninstalled. This error is unlikely to persist. |

## Next steps

- To learn more about working with your Intune data, see [Use the Intune Data Warehouse](../developer/reports-nav-create-intune-reports.md).
- To learn about app configuration policies, see [App configuration policies for Intune](app-configuration-policies-overview.md).
