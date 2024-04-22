---
# required metadata

title: Troubleshooting Remote Help on Android. 
description: Sometimes a Remote Help session starts in service but the client connection isn't established. Learn more about the possible causes in this article, and how to resolve them.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 08/16/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: Karawang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---
 
# Troubleshooting Remote Help on Android

If a Remote Help session for Android is unable to connect, check for the following possibilities:

  | Check if                      | Solution                                           |
  |-----------------------------------|-----------------------------------------------|
  | The device has been newly enrolled with Intune. | On newly enrolled devices, push notifications (needed for Remote Help to receive session initiation requests) may take a while to start working. Wait for 15 minutes and try again later.|
  | The Remote Help app isn't installed. | Install the app, see [Remote Help on Android](remote-help-android.md#deploy-remote-help-app) for details. |
  | All the required permissions have been granted to the Remote Help app. | Review and ensure that all required permissions are granted. See [Remote Help on Android](remote-help-android.md#prerequisites-for-remote-help-on-android) for details. |
  | The Intune app version isn't updated. | Update the Intune app to the latest version. |
  | The device doesn't have access to Google services. | Remote Help requires access to Google Mobile Services to function, so make sure the device has Google services. You can do this by verifying that the Play Store is present on the device. See [Android: Google Mobile Services](https://www.android.com/gms/). |
  | There's no response from the end user. | Screen Sharing and Full Control Sessions time out automatically after 5 minutes if there's no response from [Android: Google Mobile Services](https://www.android.com/gms/) on the end user device. Make sure the user accepts the prompt to start the session. |
  | The device manufacturer or OS/Zebra MX/Samsung Knox version isn't supported | Make sure the device is supported. See [Remote Help on Android](remote-help-android.md#supported-devices) |
  | (On Samsung devices only) The Knox license on the device is expired/invalid or has network issues.  | Make sure that all Knox permissions have been granted, and that the device has an active Knox license; see [License activation errors](https://configure.samsungknox.com/files/knox-configure-getting-started/Content/license-activation-errors.htm) for troubleshooting Knox activation errors. |
  | (On Samsung devices only) Other apps are actively using the Samsung Knox remote desktop APIs (you're using another remote assistance app on the device). | Close or uninstall any other apps that may be using remote viewing/control capabilities on the device. |

## Next steps

[Get support in Microsoft Intune admin center](../../get-support.md)
