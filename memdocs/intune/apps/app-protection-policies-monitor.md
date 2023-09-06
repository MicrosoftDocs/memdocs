---
# required metadata

title: How to monitor app protection policies 
titleSuffix: Microsoft Intune
description: This topic describes how to monitor app protection policies in Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/26/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
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

The following list provides details about app protection status: 

- **Assigned users**: The total number of assigned users in your company who are using an app that is associated with a policy in a work context and are protected and licensed, as well as the assigned users that are unprotected and unlicensed.
- **Flagged users**: The number of users who are experiencing issues with their devices. Jailbroken (iOS/iPadOS) and rooted (Android) devices are reported under **Flagged users**. Also, users with devices that are flagged by the Google Play’s device integrity check (if turned on by the IT admin) are reported here. 
- **Users with potentially harmful apps**: The number of users who may have a harmful app on their Android device detected by Google Play Protect. 
- **User status for iOS** and **User status for Android**: The number of users who have used an app who have a policy assigned to them in a work context for the related platform. This information shows the number of users managed by the policy, as well as the number of users who are using an app that is not targeted by any policy in a work context. You might consider adding these users to the policy.
- **Top Protected iOS/iPadOS Apps** and **Top Protected Android Apps**: Based on the most used iOS/iPadOS and Android apps, this information shows the number of protected and unprotected apps by platform.
- **Top Configured iOS/iPadOS Apps Without Enrollment** and **Top Configured Android Apps Without Enrollment**: Based on the most used iOS/iPadOS and Android apps for unenrolled devices, this information shows the number of configured apps by platform  (as in, using an app configuration policy).

    > [!NOTE]
    > If you have multiple policies per platform, a user is considered managed by policy when they have at least one policy assigned to them.

## Detailed view
You can get to the detailed view of the summary by choosing the **Flagged users** tile, and the **Users with potentially harmful apps** tile.

### Flagged users
The detailed view shows the error message, the app that was accessed when the error happened, the device OS platform affected, and a time stamp. The error is typically for jailbroken (iOS/iPadOS) or rooted (Android) devices. Also, users with devices that are flagged by the 'Play integrity verdict' conditional launch check are reported here with the reason as reported by Google. For a user to be removed from the report, the status of the device itself needs to have changed, which happens after the next root detection check (or jailbreak check/Play integrity verdict happens) that needs to report a positive result. If the device is truly remediated, the refresh on the Flagged Users report will happen when the pane reloads.

### Users with potentially harmful apps
Users with devices that are flagged by the **Require threat scan on apps** conditional launch check are reported here, with the threat category as reported by Google. If there are apps listed in this report that are being deployed through Intune, contact the app developer for the app, or remove the app from being assigned to your users. The detailed view shows:

- **User**: The name of the user.
- **Email**: The email of the user.
- **App**: The name of the app that is being protected.
- **App version**: The version of the app.
- **Device Name**: Names of any devices that are associated with the user's account.
- **App Instance ID**: The string that identities a unique user + app + device that has checked-in with the Intune service.
- **Device type**: The type of device or operating system of the device.
- **AAD Device ID**: The AAD device ID is displayed if the device is AAD-joined.
- **Management type**: The type of management on the device. For example, **unmanaged**, **MDM**, or **Android Enterprise**.  
- **Platform**: The operating system of the device.
- **Policy name**: The name of the app protection policy targeted to the app for the user.
- **Last sync**: The timestamp of the last sync of the app with Microsoft Intune.
- **Device Name**: Names of any devices that are associated with the user's account.
- **Device manufacturer**: The manufacturer of the Android device.
- **Device model**: The Android device model.
- **Android patch version**: The date of the last Android Security Patch received by the device.
- **MDM device ID**: The MDM device ID is displayed if the device is enrolled with Microsoft Intune MDM.
- **Platform version**: The operating system version.
- **App Protection Status**: The app is considered protected if it is targeted with a MAM policy.
- **iOS SDK version**: The current iOS MAM SDK version of the iOS app.
- **Compliance State**: The app meets compliance if it is targeted with MAM policy.
 
>[!NOTE]
> The **Last Sync** column represents the same value in both the in-console User status report and the App Protection Policy [exportable .csv report](/intune/app-protection-policies-monitor#export-app-protection-activities). The difference is a small delay in synchronization between the value in the two reports.
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