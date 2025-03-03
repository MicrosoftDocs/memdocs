---
# required metadata

title: Manage Teams for iOS and Android with Intune 
titleSuffix: 
description: Use Intune app protection and configuration policies with Teams for iOS and Android to ensure team collaboration experiences are always accessed with safeguards in place. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- iOS/iPadOS
- Android
- FocusArea_Apps_SpecificApp
---

# Manage collaboration experiences in Teams for iOS and Android with Microsoft Intune

Microsoft Teams is the hub for team collaboration in Microsoft 365 that integrates the people, content, and tools your team needs to be more engaged and effective.

The richest and broadest protection capabilities for Microsoft 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra ID P1 or P2 features, such as Conditional Access. At a minimum, you'll want to deploy a Conditional Access policy that allows connectivity to Teams for iOS and Android from mobile devices and an Intune app protection policy that ensures the collaboration experience is protected.

## Apply Conditional Access

Organizations can use Microsoft Entra Conditional Access policies to ensure that users can only access work or school content using Teams for iOS and Android. To do this, you will need a Conditional Access policy that targets all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

> [!NOTE]
> To leverage app-based Conditional Access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is required. For more information, see [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

Follow the steps in [Require approved client apps or app protection policy with mobile devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices), which allows Teams for iOS and Android, but blocks third-party OAuth capable mobile device clients from connecting to Microsoft 365 endpoints.

   >[!NOTE]
   > This policy ensures mobile users can access all Microsoft 365 endpoints using the applicable apps.

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

Regardless of whether the device is enrolled in a unified endpoint management (UEM) solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](app-protection-policies.md). These policies, at a minimum, must meet the following conditions:

1. They include all Microsoft 365 mobile applications, such as Edge, Outlook, OneDrive, Office, or Teams, as this ensures that users can access and manipulate work or school data within any Microsoft app in a secure fashion.

1. They're assigned to all users. This ensures that all users are protected, regardless of whether they use Teams for iOS or Android.

1. Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

For more information on the available settings, see [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> To apply Intune app protection policies against apps on Android devices that aren't enrolled in Intune, the user must also install the Intune Company Portal.  

## Utilize app configuration

Teams for iOS and Android supports app settings that allow unified endpoint management, like Microsoft Intune, administrators to customize the behavior of the app.

App configuration can be delivered either through the mobile device management (MDM) OS channel on enrolled devices ([Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the Intune App Protection Policy (APP) channel. Teams for iOS and Android supports the following configuration scenarios:

- Only allow work or school accounts

> [!IMPORTANT]
> For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise and Teams for Android must be deployed via the Managed Google Play store. For more information, see [Set up enrollment of Android Enterprise personally-owned work profile devices](../enrollment/android-work-profile-enroll.md) and [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).

Each configuration scenario highlights its specific requirements. For example, whether the configuration scenario requires device enrollment, and thus works with any UEM provider, or requires Intune App Protection Policies.

> [!IMPORTANT]
> App configuration keys are case sensitive. Use the proper casing to ensure the configuration takes effect.

> [!NOTE]
> With Microsoft Intune, app configuration delivered through the MDM OS channel is referred to as a **Managed Devices** App Configuration Policy (ACP); app configuration delivered through the App Protection Policy channel is referred to as a **Managed Apps** App Configuration Policy.

## Only allow work or school accounts

Respecting the data security and compliance policies of our largest and highly regulated customers is a key pillar to the Microsoft 365 value. Some companies have a requirement to capture all communications information within their corporate environment, as well as, ensure the devices are only used for corporate communications. To support these requirements, Teams for iOS and Android on enrolled devices can be configured to only allow a single corporate account to be provisioned within the app.

You can learn more about configuring the org allowed accounts mode setting here:

- [Android setting](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-apps)
- [iOS setting](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-apps)

This configuration scenario only works with enrolled devices. However, any UEM provider is supported. If you aren't using Microsoft Intune, you need to consult with your UEM documentation on how to deploy these configuration keys. 

## Simplify the sign-in experience with domain-less sign in 

You can simplify the sign-in experience on Teams for iOS and Android by pre-filling the domain name on the sign-in screen for users on shared and managed devices by applying the following policies: 
   
   | Name | Value |
   |---|---|
   | domain_name | A string value providing the domain of the tenant to appended. Use a semicolon delimited value to add multiple domains. This policy only works on enrolled devices. |
   | enable_numeric_emp_id_keypad | A boolean value used to indicate that the employee ID is all numeric and the number keypad should be enabled for easy entry. If the value is not set, then the alphanumeric keyboard will open. This policy only works on enrolled devices.  |

> [!NOTE]
> These policies will only work on enrolled shared and managed devices.

## Notification settings in Microsoft Teams

Notifications keep you up to date about what's happening or going to happen around you. They appear on home screen or lock screen based on the settings. 
Use the following options to configure your notifications on the portal through an app protection policy. 

|Options|Description|
|:--- |:---|
|Allow |Display actual notification with all the details (title and content). |
|Block org data |Remove title and replace content with “You have a new message” for chat notifications, and “There is new activity” for others. A user won't be able to **Reply** to a notification from a lock screen. |
|Blocked |Suppresses notification and doesn't notify user. |

### To set the policies in Intune

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. In the left navigation pane, navigate to **Apps** > **Protection**.
1. Click **Create Policy** and select your desired platform, such as **iOS/iPadOS**.
1. On the **Basics** page, add details such as **Name** and **Description**. Click **Next**.
1. On the **Apps** page, click **Select public apps**, then find and select the **Microsoft Teams** apps. Click **Next**.
1. On the **Data Protection** page, find the **Org data notifications** setting and select the **Block org Data** option. Set the **Assignments** for the groups of users to include and then create your policy.
1. Once the app protection policy has been created, go to **Apps** > **Configuration** > **Create** > **Managed apps**. 
1. On the **Basics** page, add a **Name** and click **Select public apps**, then find and select the **Microsoft Teams** apps. Click **Next**.
1. Under **General configuration settings**, set any of the notification keys to **1** to turn the feature **ON** for chat, channels, all other notifications or any of these combinations. And, set to **0** to turn off the feature. 

   | Name | Value |
   |---|---|
   | com.microsoft.teams.chat.notifications.IntuneMAMOnly | **1** for on, **0** for off |
   | com.microsoft.teams.channel.notifications.IntuneMAMOnly | **1** for on, **0** for off |
   | com.microsoft.teams.other.notifications.IntuneMAMOnly | **1** for on, **0** for off |

   :::image type="content" source="./media/managed-microsoft-teams/managed-microsoft-teams-02.png" alt-text="app-configuration-properties-at-a-glance" border="true" :::

1. Set the **Assignments** for the groups of users to include and then create your policy.

1. Once the policy has been created, go to **Apps** > **Protection**. Find your newly created **App protection policy** and check whether the policy has been deployed by reviewing the **Deployed** column. The **Deployed** column should display **Yes** for the created policy. If it displays **No**, refresh the page, and check after 10 minutes.

### For the notifications to show up on iOS and Android devices

1. On the device, sign in to both Teams and Company Portal. Set it to **Show Previews** > **Always** to make sure your device notification settings allow notifications from Teams. 
1. Lock the device and send notifications to the user logged in on that device. Tap on a notification to expand it on the lock screen, without unlocking the device. 
1. Notifications on the lock screen should look as follows (screenshots are from iOS, but the same strings should be shown on Android):
   - No option for **Reply** or other quick notification reactions from lock screen should be visible. 
   - The sender’s avatar isn't visible; however, initials are fine.  
   - The notification should display title but replace content with "You have a new message" for chat notifications, and "There is new activity" for others.

      :::image type="content" source="./media/managed-microsoft-teams/managed-microsoft-teams-04.png" alt-text="iphone-screenshot" border="true" :::

For more information about app configuration policies and app protection policies, see the following topics:
- [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [App protection policies overview](../apps/app-protection-policy.md)

## Next steps

- [What are app protection policies?](app-protection-policy.md) 
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
