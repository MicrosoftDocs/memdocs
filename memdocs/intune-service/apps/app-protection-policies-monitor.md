---
# required metadata

title: How to monitor app protection policies 
titleSuffix: Microsoft Intune
description: This topic describes how to monitor app protection policies in Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/14/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 9b0afb7d-cd4e-4fc6-83e2-3fc0da461d02

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# How to monitor app protection policies
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

You can monitor the status of the app protection policies that you've applied to users from the Intune app protection pane in Intune. Additionally, you can find information about the users affected by app protection policies, policy compliance status, and any issues that your users might be experiencing.

App protection data is retained for a minimum of 90 days. Any app instances that have checked in to the Intune service within the past 90 days is included in the app protection status report. 

> [!NOTE]
> For iOS 16 and later devices, the **Device Name** value in all app protection reports will be a generic device name. For related information, see [Apple Developer documentation](https://developer.apple.com/documentation/uikit/uidevice/1620015-name).

## View the **App protection status** report

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Monitor** > **App protection status**.

- **User**: The name of the user.
- **Email**: The email of the user.
- **App**: The name of the app that is being protected.
- **App version**: The version of the app.
- **Device Name**: Names of any devices that are associated with the user's account.
- **App Instance ID**: The string that identities a unique user + app + device that has checked-in with the Intune service.
- **Device type**: The type of device or operating system of the device.
- **Microsoft Entra Device ID**: The Microsoft Entra device ID is displayed if the device is Microsoft Entra joined.
- **Management type**: The type of management on the device. For example, **unmanaged**, **MDM**, or **Android Enterprise**.  
- **Platform**: The operating system of the device.
- **Policy name**: The name of the app protection policy targeted to the app for the user.
- **Last sync**: The timestamp of the last sync of the app with Microsoft Intune.
- **Device Name**: Names of any devices that are associated with the user's account.
- **Device manufacturer**: The manufacturer of the Android device.
- **Device model**: The Android device model.
- **Android patch version**: The date of the last Android Security Patch received by the device.
- **MDM device ID**: The MDM device ID is displayed if the device is enrolled with Microsoft Intune MDM.
- **Platform version**: The operating system version. When Rapid Security Response version for iOS/iPadOS is applicable, a letter will appear after the software version number, as in this example: 16.4.1.a
- **App Protection Status**: The app is considered protected if it is targeted with a MAM policy.
- **iOS SDK version**: The current iOS MAM SDK version of the iOS app.
- **Compliance State**: The app meets compliance if it is targeted with MAM policy.
 
>[!NOTE]
> The **Last Sync** column represents the same value in both the in-console User status report and the App Protection Policy [exportable .csv report](/mem/intune-service/apps/app-protection-policies-monitor#export-app-protection-activities). The difference is a small delay in synchronization between the value in the two reports.
>
> The time referenced in Last Sync is when Intune last saw the app instance. When a user launches an app, it might notify the Intune App Protection service at that launch time, depending on when it last checked in. See [the retry interval times for App Protection Policy check-in](app-protection-policy-delivery.md). If a user hasn't used that particular app in the last check-in interval (which is usually 30 minutes for active usage), and they launch the app, then:
>
> - The App Protection Policy exportable .csv report has the newest time, within 1 minute (minimum) to 30 minutes (maximum).
> - The User status report has the newest time instantly.
>
> For example, consider a targeted and licensed user who launches a protected app at 12:00 PM:
>
> - If this is a sign in for the first time, that means the user was signed out before, and doesn't have an app instance registration with Intune. After the user signs in, the user gets a new app instance registration, and can be checked-in immediately (with the same time delays listed previously for future check-ins). Thus, the Last Sync time is 12:00 PM in the User status report, and 12:01 PM (or 12:30 PM at latest) in the App Protection Policy report.
> - If the user is just launching the app, the Last Sync time reported depends on when the user last checked in.

## See also

- [How to create and assign app protection policies](../apps/app-protection-policies.md)
- [Intune reports](../fundamentals/reports.md)
