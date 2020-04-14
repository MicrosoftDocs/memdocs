---
# required metadata

title: App configuration policies for Microsoft Intune
titleSuffix: 
description: Learn how to use app configuration policies on an iOS/iPadOS or Android device in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 834B4557-80A9-48C0-A72C-C98F6AF79708

# optional metadata 

#ROBOTS:
#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# App configuration policies for Microsoft Intune

App configuration policies can help you eliminate app setup up problems by letting you assign configuration settings to a policy that is assigned to end-users before they run the app. The settings are then supplied automatically when the app is configured on the end-users device, and end-users don't need to take action. The configuration settings are unique for each app. 

You can create and use app configuration policies to provide configuration settings for both iOS/iPadOS or Android apps. These configuration settings allow an app to be customized by using app configuration and management. The configuration policy settings are used when the app checks for these settings, typically the first time the app is run. 

An app configuration setting, for example, might require you to specify any of the following details:

- A custom port number
- Language settings
- Security settings
- Branding settings such as a company logo

If end-users were to enter these settings instead, they could do this incorrectly. App configuration policies can help provide consistency across an enterprise and reduce helpdesk calls from end-users trying to configure settings on their own. By using app configuration policies, the adoption of new apps can be easier and quicker.

The available configuration parameters are ultimately decided by the developers of the app. Documentation from the application vendor should be reviewed to see if an app supports configuration and what configurations are available. For some applications, Intune will populate the available configuration settings. 

> [!NOTE]
> In the Managed Google Play Store, apps that support configuration will be marked as such:
> 
> ![Screenshot of a configured app](./media/app-configuration-policies-overview/configured-app.png)
>
> You will only see apps from [Managed Google Play store](https://play.google.com/work), not the [Google Play store](https://play.google.com/store/apps), when using Managed Devices as the Enrollment Type for Android devices. Managed Google Play Store, which you may also know as Android for Work (AfW) and Android Enterprise, are the apps in the Work Profile that contain the app versions that support app configuration.

You can assign an app configuration policy to a group of end-users and devices by using a combination of [include and exclude assignments](apps-inc-exl-assignments.md). Once you add an app configuration policy, you can set the assignments for the app configuration policy. When you set the assignments for the policy, you can choose to include and exclude the [groups](../fundamentals/groups-add.md) of end-users for which the policy applies. When you choose to include one or more groups, you can choose to select specific groups to include or select built-in groups. Built-in groups include **All Users**, **All Devices**, and **All Users + All Devices**.

You have two options to use app configuration policies with Intune:
- **Managed devices** - The device is managed by Intune as the mobile device management (MDM) provider. The app must be designed to support the app configuration.
- **Managed apps** - An app that has been developed to integrate the Intune App SDK. This is known as Mobile Application Management without enrollment ([MAM-WE](app-management.md#mobile-application-management-mam-basics)). You can also wrap an app to implement and support the Intune App SDK. For more information about wrapping an app, see [Prepare line-of-business apps for app protection policies](../developer/apps-prepare-mobile-application-management.md).

    > [!NOTE]
    > Intune managed apps will check-in with an interval of 30 minutes for Intune App Configuration Policy status, when deployed in conjunction with an Intune App Protection Policy. If an Intune App Protection Policy isn't assigned to the user, then the Intune App Configuration Policy check-in interval is set to 720 minutes.

## Apps that support app configuration

### Managed devices
You can use app configuration policies for apps that support it. To support app configuration in Intune, apps must be written to support the use of app configurations as defined by the OS. Consult your app vendor for details for which app config keys they support.

### Managed apps
You can prepare your line-of-business apps by either incorporating the [Intune App SDK](../developer/app-sdk.md) into the app, or wrapping the app after it is developed using the [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md). The Intune App SDK strives to minimize the amount of code changes required from the app developer. For more information, see the [Intune App SDK overview](../developer/app-sdk.md). For a comparison between the Intune App SDK and the Intune App Wrapping Tool, see [Prepare line-of-business apps for app protection policies](../developer/apps-prepare-mobile-application-management.md#feature-comparison).

Selecting **Managed apps** as the **Device Enrollment Type** specifically refers to apps configured by Intune configuration policies on a device that is not enrolled in device management, whereas **Managed devices** applies to apps deployed through the MDM channel and thus are managed by Intune. Select the appropriate choice based on these descriptions. 

![Device enrollment type](./media/app-configuration-policies-overview/device-enrollment-type.png)

> [!NOTE]
> For multi-identity apps, such as Microsoft Outlook, user preferences may be considered. Focused Inbox, for example, will respect the user setting and not change the configuration. Other parameters do let you control whether a user can or cannot change the setting. For more information, see [Deploying Outlook for iOS/iPadOS and Android app configuration settings](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## Android app configuration policies

For Android app configuration policies, you can select the device enrollment type before creating an app configuration profile. You can account for certificate profiles that are based on enrollment type (Work profile or Device Owner). This update provides the following:

1. If a new profile is created and Work Profile and Device Owner Profile are selected for device enrollment type, you will not be able to associate a certificate profile with the app config policy.
2. If a new profile is created and Work Profile only is selected, Work Profile certificate policies created under Device Configuration can be utilized.
3. If a new profile is created and Device Owner only is selected, Device Owner certificate policies created under Device Configuration can be utilized. 

> [!IMPORTANT]
> Existing policies created prior to the release of this feature (April 2020 release - 2004) that do not have any certificate profiles associated with the policy will default to Work Profile and Device Owner Profile for device enrollment type. Also, existing policies created prior to the release of this feature that have certificate profiles associated with them will default to Work Profile only.

Existing policies will not remediate or issue new certificates.

Additionally, you can use Gmail and Nine email configuration profiles that will work for both Work Profile and Device Owner enrollment types, including the use of certificate profiles on both email configuration types. Any Gmail or Nine policies that you have created under Device Configuration for Work Profiles will continue to apply to the device and it is not necessary to move them to app configuration policies.

## Validate the applied app configuration policy

You can validate the app configuration policy using the following three methods:

   1. Visibly on the device. Is the targeted app exhibiting the behavior applied in the App Configuration policy?
   2. Via Diagnostic Logs (see the Diagnostic Logs section below).
   3. In the Intune Portal. The **Monitor** section of a policy can provide the relevant status:

      ![First screenshot of device install status](./media/app-configuration-policies-overview/device-install-status-1.png)

      ![Second screenshot of device install status](./media/app-configuration-policies-overview/device-install-status-2.png)

      Additionally, under **Intune** -> **Devices** -> **All Devices** on the left side of the screen, the **App Configuration** option will display all the assigned policies and their state:

      ![Screenshot of app configuration](./media/app-configuration-policies-overview/app-configuration.png)

## Diagnostic Logs

### iOS/iPadOS configuration on unmanaged devices

You can validate iOS/iPadOS configuration with the **Intune Diagnostic Log** on unmanaged devices for managed app configuration. In addition to the below steps, you can access managed app logs using Microsoft Edge. For more information, see [Use Microsoft Edge on iOS/iPadOS to access managed app logs](manage-microsoft-edge.md#use-microsoft-edge-to-access-managed-app-logs).

1. If not already installed on the device, download and install the **Microsoft Edge** from the App Store. For more information, see [Microsoft Intune protected apps](apps-supported-intune-apps.md).
2. Launch the **Microsoft Edge** and select **about** > **intunehelp** from the navigation bar.
3. Click **Get Started**.
4. Click **Share Logs**.
5. Use the mail app of your choice to send the log to yourself so they can be viewed on your PC. 
6. Review **IntuneMAMDiagnostics.txt** in your text file viewer.
7. Search for `ApplicationConfiguration`. The results will look like the following:

    ``` JSON
        {
            (
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.BlockListURLs";
                    Value = "https://www.aol.com";
                },
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.bookmarks";
                    Value = "Outlook Web|https://outlook.office.com||Bing|https://www.bing.com";
                }
            );
        },
        {
            ApplicationConfiguration =             
            (
                {
                Name = IntuneMAMUPN;
                Value = "CMARScrubbedM:13c45c42712a47a1739577e5c92b5bc86c3b44fd9a27aeec3f32857f69ddef79cbb988a92f8241af6df8b3ced7d5ce06e2d23c33639ddc2ca8ad8d9947385f8a";
                },
                {
                Name = "com.microsoft.outlook.Mail.NotificationsEnabled";
                Value = false;
                }
            );
        }
    ```

Your application configuration details should match the application configuration policies configured for your tenant. 

![Targeted app config](./media/app-configuration-policies-overview/targeted-app-configuration-3.png)

### iOS/iPadOS configuration on managed devices

You can validate iOS/iPadOS configuration with the **Intune Diagnostic Log** on managed devices for managed app configuration.

1. If not already installed on the device, download and install the **Microsoft Edge** from the App Store. For more information, see [Microsoft Intune protected apps](apps-supported-intune-apps.md).
2. Launch **Microsoft Edge** and select **about** > **intunehelp** from the navigation bar.
3. Click **Get Started**.
4. Click **Share Logs**.
5. Use the mail app of your choice to send the log to yourself so they can be viewed on your PC. 
6. Review **IntuneMAMDiagnostics.txt** in your text file viewer.
7. Search for `AppConfig`. Your results should match the application configuration policies configured for your tenant.

### Android configuration on managed devices

You can validate Android configuration with the **Intune Diagnostic Log** on managed devices for managed app configuration.

To collect logs from an Android device, you or the end user must download the logs from the device via a USB connection (or the **File Explorer** equivalent on the device). Here are the steps:

1. Connect the Android device to your computer with the USB cable.
2. On the computer, look for a directory that has the name of your device. In that directory, find `Android Device\Phone\Android\data\com.microsoft.windowsintune.companyportal`.
3. In the `com.microsoft.windowsintune.companyportal` folder, open the Files folder and open `OMADMLog_0`.
3. Search for `AppConfigHelper` to find app configuration related messages. The results will look similar to the following block of data:

    `2019-06-17T20:09:29.1970000       INFO   AppConfigHelper     10888  02256  Returning app config JSON [{"ApplicationConfiguration":[{"Name":"com.microsoft.intune.mam.managedbrowser.BlockListURLs","Value":"https:\/\/www.aol.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.bookmarks","Value":"Outlook Web|https:\/\/outlook.office.com||Bing|https:\/\/www.bing.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.homepage","Value":"https:\/\/www.arstechnica.com"}]},{"ApplicationConfiguration":[{"Name":"IntuneMAMUPN","Value":"AdeleV@M365x935807.OnMicrosoft.com"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled","Value":"false"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled.UserChangeAllowed","Value":"false"}]}] for user User-875363642`
    
## Graph API support for app configuration

You can use Graph API to accomplish app configuration tasks. For details, see [Graph API Reference MAM Targeted Config](https://docs.microsoft.com/graph/api/resources/intune-shared-targetedmanagedappconfiguration?view=graph-rest-beta). For more information about Intune and Graph, see [Working with Intune in Microsoft Graph](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-beta).

## Troubleshooting

### Using logs to show a configuration parameter
When the logs show a configuration parameter that is confirmed to be applying but doesn't seem to work, there may be an issue with the configuration implementation by the app developer. Reaching out to that app developer first, or checking their knowledge base, may save you a support call with Microsoft. If it is an issue with how the configuration is being handled within an app, it would have to be addressed in a future updated version of that app.

## Next steps

### Managed devices

- Learn how to use app configuration with your iOS/iPadOS devices.  See [Add app configuration policies for managed iOS/iPadOS devices](app-configuration-policies-use-ios.md).
- Learn how to use app configuration with your Android devices.  See [Add app configuration policies for managed Android devices](app-configuration-policies-use-android.md).

### Managed apps

- Learn how to use app configuration with managed apps. See [Add app configuration policies for managed apps without device enrollment](app-configuration-policies-managed-app.md).
