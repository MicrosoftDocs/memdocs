---
title: include file
description: include file
author: erikre 
ms.service: microsoft-intune
ms.topic: include
ms.date: 07/31/2024
ms.author: erikre
ms.custom: include file
---
#### Level 3 enterprise high data protection

Level 3 is the data protection configuration recommended as a standard for organizations with large and sophisticated security organizations, or for specific users and groups who will be uniquely targeted by adversaries. Such organizations are typically targeted by well-funded and sophisticated adversaries, and as such merit the additional constraints and controls described. This configuration expands upon the configuration in Level 2 by restricting additional data transfer scenarios, increasing the complexity of the PIN configuration, and adding mobile threat detection.  

> [!IMPORTANT]
> The policy settings enforced in level 3 include all the policy settings recommended for level 2 but only lists those settings below that have been added or changed to implement more controls and a more sophisticated configuration than level 2. These policy settings can have a potentially significant impact to users or to applications, enforcing a level of security commensurate with the risks facing targeted organizations.  

#### Data protection

| Setting | Setting description |             Value  |             Platform        | Notes |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Data Transfer |       Transfer telecommunication data to  |          Any policy-managed dialer app |          Android  | Administrators can also configure this setting to use a dialer app that doesn't support App Protection Policies by selecting **A specific dialer app** and providing the **Dialer App Package ID** and **Dialer App Name** values.   |
| Data Transfer |       Transfer telecommunication data to  |          A specific dialer app |          iOS/iPadOS  |  |
| Data Transfer |       Dialer App URL Scheme  |          *replace_with_dialer_app_url_scheme* |          iOS/iPadOS  | On iOS/iPadOS, this value must be replaced with the URL scheme for the custom dialer app being used. If the URL scheme isn't known, contact the app developer for more information. For more information on URL schemes, see [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app).|
| Data transfer |       Receive   data from other apps  |          Policy   managed apps  |          iOS/iPadOS, Android         |  |
| Data transfer |       Open data into Org documents  |          Block  |          iOS/iPadOS, Android         |  |
| Data transfer |       Allow users to open data from selected services  |          OneDrive for Business, SharePoint, Camera, Photo Library |          iOS/iPadOS, Android         | For related information, see [Android app protection policy settings](/mem/intune/apps/app-protection-policy-settings-android) and [iOS app protection policy settings](/mem/intune/apps/app-protection-policy-settings-ios).  |
| Data transfer |       Third-party   keyboards  |          Block  |          iOS/iPadOS        | On iOS/iPadOS, this blocks all third-party keyboards from   functioning within the app.  |
| Data transfer |       Approved   keyboards  |          Require  |          Android        |  |
| Data transfer |       Select   keyboards to approve  |          *add/remove   keyboards*  |          Android        | With Android, keyboards must be selected in   order to be used based on your deployed Android devices.  |
| Functionality |       Print org data  |          Block  |          iOS/iPadOS, Android, Windows         |  |

#### Access requirements

|       Setting  |          Value  |          Platform  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       Simple   PIN  |          Block  |          iOS/iPadOS,   Android  |
|       Select   Minimum PIN length  |          6  |          iOS/iPadOS,   Android  |
|       PIN reset   after number of days  |          Yes  |          iOS/iPadOS,   Android  |
|       Number of   days  |          365  |          iOS/iPadOS,   Android  |
|       Class 3 Biometrics (Android 9.0+)   |          Require  |          Android  |
|       Override Biometrics with PIN after biometric updates   |          Require  |          Android  |

#### Conditional launch

| Setting | Setting description |          Value / Action  |          Platform        | Notes |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device conditions |       Require device lock  |          High/Block Access  |          Android        | This setting ensures that Android devices have a device password that meets the minimum password requirements.  |
|       Device   conditions  |          Max   allowed device threat level  |          Secured / Block access  |          Windows        |
|       Device   conditions  |          Jailbroken/rooted devices  |        N/A / Wipe data  |          iOS/iPadOS,   Android        |  |
|       Device   conditions  |          Max   allowed threat level  |          Secured / Block access  |          iOS/iPadOS,   Android        | <p>Unenrolled devices can be   inspected for threats using Mobile Threat Defense. For more information, see  [Mobile Threat Defense for unenrolled devices](/mem/intune/protect/mtd-enable-unenrolled-devices).</p><p>If the device is enrolled, this setting can be skipped in favor of   deploying Mobile Threat Defense for enrolled devices. For more information, see [Mobile Threat Defense for enrolled devices](/mem/intune/protect/mtd-device-compliance-policy-create).</p> |
| Device conditions  |       Max   OS version  |          *Format: Major.Minor<br>   Example: 11.0* / Block access   |          Android        | Microsoft recommends configuring   the maximum Android major version to ensure beta or unsupported versions of the operating system aren't used.   See [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/) for Android's latest   recommendations |
| Device conditions  |       Max   OS version  |          *Format: Major.Minor.Build <br>Example:   15.0* / Block access |          iOS/iPadOS        | Microsoft recommends configuring   the maximum iOS/iPadOS major version to ensure beta or unsupported versions of the operating system aren't used. See   [Apple security updates](https://support.apple.com/en-us/HT201222) for Apple's latest recommendations |
| Device conditions  |       Max   OS version  |          *Format: Major.Minor<br>   Example: 22631.* / Block access   |          Windows        | Microsoft recommends configuring   the maximum Windows major version to ensure beta or unsupported versions of the operating system aren't used. |
| Device conditions  |       Samsung Knox device attestation  | Wipe data |          Android        | Microsoft recommends configuring the **Samsung Knox device attestation** setting to **Wipe data** to ensure the org data is removed if the device doesn't meet Samsung's Knox hardware-based verification of device health.  This setting verifies all Intune MAM client responses to the Intune service were sent from a healthy device.  <p> This setting will apply to all devices targeted.  To apply this setting only to Samsung devices, you can use "Managed apps" assignment filters.  For more information on assignment filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](/mem/intune/fundamentals/filters).|
| App conditions | Offline grace period | 30 / Wipe data (days) | iOS/iPadOS, Android, Windows | |

