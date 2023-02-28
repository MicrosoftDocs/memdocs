---
# required metadata

title: How to monitor app protection policies 
titleSuffix: Microsoft Intune
description: This topic describes how to monitor app protection policies in Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 9b0afb7d-cd4e-4fc6-83e2-3fc0da461d02

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
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

There are three different places to monitor app protection policies:
- Summary view
- Detailed view
- Reporting view

App protection data is retained for a minimum of 90 days. Any app instances that have checked in to the Intune service within the past 90 days is included in the app protection status report. An *app instance* is a unique user + app + device. 

> [!NOTE]
> For iOS 16 and later devices, the "Device Name" value in all app protection reports will be a generic device name.  For more information, see [Apple Developer documentation](https://developer.apple.com/documentation/uikit/uidevice/1620015-name).

> [!NOTE]
> For more information, see [How to create and assign app protection policies](app-protection-policies.md). 



## Summary view

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Monitor** > **App protection status**.

The following list provides details about app protection status: 
- **Assigned users**: The total number of assigned users in your company who are using an app that is associated with a policy in a work context and are protected and licensed, as well as the assigned users that are unprotected and unlicensed.
- **Flagged users**: The number of users who are experiencing issues with their devices. Jailbroken (iOS/iPadOS) and rooted (Android) devices are reported under **Flagged users**. Also, users with devices that are flagged by the Google SafetyNet device attestation check (if turned on by the IT admin) are reported here. 
- **Users with potentially harmful apps**: The number of users who may have a harmful app on their Android device detected by Google Play Protect. 
- **User status for iOS** and **User status for Android**: The number of users who have used an app who have a policy assigned to them in a work context for the related platform. This information shows the number of users managed by the policy, as well as the number of users who are using an app that is not targeted by any policy in a work context. You might consider adding these users to the policy.
- **Top Protected iOS/iPadOS Apps** and **Top Protected Android Apps**: Based on the most used iOS/iPadOS and Android apps, this information shows the number of protected and unprotected apps by platform.
- **Top Configured iOS/iPadOS Apps Without Enrollment** and **Top Configured Android Apps Without Enrollment**: Based on the most used iOS/iPadOS and Android apps for unenrolled devices, this information shows the number of configured apps by platform  (as in, using an app configuration policy).

    > [!NOTE]
    > If you have multiple policies per platform, a user is considered managed by policy when they have at least one policy assigned to them.

## Detailed view
You can get to the detailed view of the summary by choosing the **Flagged users** tile, and the **Users with potentially harmful apps** tile.

### Flagged users
The detailed view shows the error message, the app that was accessed when the error happened, the device OS platform affected, and a time stamp. The error is typically for jailbroken (iOS/iPadOS) or rooted (Android) devices. Also, users with devices that are flagged by the 'SafetyNet device attestation' conditional launch check are reported here with the reason as reported by Google. For a user to be removed from the report, the status of the device itself needs to have changed, which happens after the next root detection check (or jailbreak check/SafetyNet check happens) that needs to report a positive result. If the device is truly remediated, the refresh on the Flagged Users report will happen when the pane reloads.

### Users with potentially harmful apps
Users with devices that are flagged by the **Require threat scan on apps** conditional launch check are reported here, with the threat category as reported by Google. If there are apps listed in this report that are being deployed through Intune, contact the app developer for the app, or remove the app from being assigned to your users. The detailed view shows:

- **User**: The name of the user.
- **App package ID**: This is the way the Android OS uniquely determines an app.
- **If the app is MAM-enabled**: Whether or not the app is being deployed through Microsoft Intune. 
- The **threat category**: What Google-determined threat category this app falls into. 
- **Email**: The email of the user.
- **Device Name**: Names of any devices that are associated with the user's account.
- **A time stamp**: This is the date of the last sync that Google did with Microsoft Intune regarding potentially harmful apps.

## Reporting view

You can find the same reports at the top of the **App protection status** pane. To view these reports, select **Apps** > **Monitor** > **App protection status** > **Reports**. The **Reports** pane provides several reports based on user and app, including the following:

### User report

You can search for a single user and check the compliance status for that user. The **App reporting** pane shows the following information for a selected user:

- **Icon**: Displays whether the app status is up-to-date.
- **App Name**: The name of the app.
- **Device Name**: Devices that are associated with the user's account.
- **Device Type**: The type of device or operating system the device is running.
- **Policies**: The policies associated with the app.
- **Status**:
  - **Checked in**: The policy was deployed to the user, and the app was used in the work context at least once.
  - **Not checked in**: The policy was deployed to the user, but the app hasn't been used in the work context since then.
- **Last Sync**: When the app was last synced with Intune.

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

To see the reporting for a user, follow these steps:

1. To select a user, choose the **User status** summary tile.

    ![Screenshot of the Summary tile of Intune mobile application management](./media/app-protection-policies-monitor/MAM-reporting-6.png)

2. On the **App reporting** pane, choose **Select user** to search for an Azure Active Directory user.

    ![Screenshot of the Select user option on the App reporting pane](./media/app-protection-policies-monitor/MAM-reporting-2.png)

3. Select the user from the list. You can see the details of the compliance status for that user.

>[!NOTE]
> If the users you searched for do not have the MAM policy deployed to them, you see a message informing you that the user is not targeted by any MAM policies.

### App report
You can search by platform and app, and then this report will provide two different app protection statuses that you can select before generating the report. The statuses can be **Protected** or **Unprotected**.

  - User status for managed MAM activity (**Protected**): This report outlines the activity of each managed MAM app, on a per-user basis. It shows all apps targeted by MAM policies for each user, and the status of each app as checked in with MAM policies. The report also includes the status of each app that was targeted with a MAM policy, but was never checked in.
  - User status for unmanaged MAM activity (**Unprotected**): This report outlines the activity of MAM-enabled apps that are currently unmanaged, on a per-user basis. This might happen because:
    - These apps are either being used by a user or an app that isn't currently targeted by a MAM policy.
    - All apps are checked in, but aren't getting any MAM policies.

    ![Screenshot of a user's App reporting pane, with details for three apps](./media/app-protection-policies-monitor/MAM-reporting-4.png)

### **User configuration report**
Based on a selected user, this report provides details about any app configurations the user has received.

### **App configuration report**
Based on the selected platform and app, this report provides details about which users have received configurations for the selected app.

### App learning report for Windows Information Protection
This report shows which apps are attempting to cross policy boundaries.

### Website learning for Windows Information Protection
This report shows which websites are attempting to cross policy boundaries.

## Export app protection activities
You can export all your app protection policy activities to a single .csv file. This can be helpful to analyze all the app protection statuses reported from the users. The **App Protection .csv file shows**:
- **User**: The name of the user.
- **Email**: The email of the user.
- **App**: The name of the app.
- **App version**: The version of the app.
- **Device Name**: Names of any devices that are associated with the user's account.
- **Device Manufacturer**: This lists the manufacturer of the device (Android only). 
- **Device Model**: This lists the manufacturer of the device (Android only). 
- **Android Patch Version**: The date of the last Android Security Patch.
- **AAD Device ID**: This column gets populated if the device is AAD-joined.
- **MDM Device ID**: This column gets populated if the device is enrolled Microsoft Intune MDM.
- **Platform**: The operating system.
- **Platform version**: The operating system version.
- **Management Type**: Type of management on device. For example, Android Enterprise, unmanaged, or MDM.  
- **App Protection Status**: Unprotected or protected.
- **Policy**: The app protection policies associated with the app.
- **Last Sync**: When the app was last synced with Microsoft Intune. 
- **Compliance State**: Whether the app on the user's device is compliant with any app-based Conditional Access policies.  

Follow these steps to generate App Protection .csv file or App Configuration .csv file:

1. On the Intune mobile application management pane, choose **App protection report**.

    ![Screenshot of the App protection download link](./media/app-protection-policies-monitor/app-protection-report-csv-2.png)

2. Choose **Yes** to save your report, and then choose **Save As**. Select the folder you want to save the report in.

    ![Screenshot of the Save report confirmation box](./media/app-protection-policies-monitor/app-protection-report-csv-1.png)
   
> [!NOTE]
> Intune provides additional device reporting fields, including App Registration ID, Android manufacturer, model, and security patch version, as well as iOS/iPadOS model. In Intune, you access these fields by selecting **Apps** > **App protection status** > **App Protection Report: iOS/iPadOS, Android**. In addition, these parameters help you configure the **Allow** list for the device manufacturer (Android), the **Allow** list for the device model (Android and iOS/iPadOS), and the **minimum Android security patch version** setting.   
 
## See also
- [Manage data transfer between iOS/iPadOS apps](data-transfer-between-apps-manage-ios.md)
- [Where to find work or school apps for iOS/iPadOS (user help)](../user-help/use-managed-apps-on-your-device.md) 
