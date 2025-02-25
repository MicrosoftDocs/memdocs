---
# required metadata

title: Manage Microsoft 365 (Office) for iOS and Android with Intune 
titleSuffix: 
description: Use Intune app protection and configuration policies with Microsoft 365 (Office) for iOS and Android to ensure collaboration experiences are always accessed with safeguards in place. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/18/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- iOS/iPadOS
- Android
- FocusArea_Apps_SpecificApp
---

# Manage collaboration experiences in Microsoft 365 (Office) for iOS and Android with Microsoft Intune

Microsoft 365 (Office) for iOS and Android delivers several key benefits including:

- Combining Word, Excel, and PowerPoint in a way that simplifies the experience with fewer apps to download or switch between. It requires far less phone storage than installing individual apps while maintaining virtually all the capabilities of the existing mobile apps people already know and use.
- Integrating Microsoft Lens technology to unlock the power of the camera with capabilities like converting images into editable Word and Excel documents, scanning PDFs, and capturing whiteboards with automatic digital enhancements to make the content easier to read.
- Adding new functionality for common tasks people often encounter when working on a phone—things like making quick notes, signing PDFs, scanning QR codes, and transferring files between devices.

The richest and broadest protection capabilities for Microsoft 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra ID P1 or P2 features, such as Conditional Access. At a minimum, you will want to deploy a Conditional Access policy that allows connectivity to Microsoft 365 (Office) for iOS and Android from mobile devices and an Intune app protection policy that ensures the collaboration experience is protected.

## Apply Conditional Access
Organizations can use Microsoft Entra Conditional Access policies to ensure that users can only access work or school content using Microsoft 365 (Office) for iOS and Android. To do this, you will need a Conditional Access policy that targets all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

1. Follow the steps in [Require approved client apps or app protection policy with mobile devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices), which allows Microsoft 365 (Office) for iOS and Android, but blocks third-party OAuth capable mobile device clients from connecting to Microsoft 365 endpoints.

   >[!NOTE]
   > This policy ensures mobile users can access all Microsoft 365 endpoints using the applicable apps.

> [!NOTE]
> To leverage app-based Conditional Access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is required. For more information, see [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

Regardless of whether the device is enrolled in a unified endpoint management (UEM) solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](app-protection-policies.md). These policies, at a minimum, must meet the following conditions:

1. They include all Microsoft 365 mobile applications, such as Edge, Outlook, OneDrive, Microsoft 365 (Office), or Teams, as this ensures that users can access and manipulate work or school data within any Microsoft app in a secure fashion.

2. They are assigned to all users. This ensures that all users are protected, regardless of whether they use Microsoft 365 (Office) for iOS or Android.

3. Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

For more information on the available settings, see [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> To apply Intune app protection policies against apps on Android devices that are not enrolled in Intune, the user must also install the Intune Company Portal.
>  For Android App Protection Policies, add the Office Hub, Office Hub [HL], and Office Hub [ROW] apps. For more information, see [Support Tip: How to enable Intune app protection policies with the Office mobile](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

## Utilize app configuration

Microsoft 365 (Office) for iOS and Android supports app settings that allow unified endpoint management, like Microsoft Intune, administrators to customize the behavior of the app.

App configuration can be delivered either through the mobile device management (MDM) OS channel on enrolled devices ([Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the Intune App Protection Policy (APP) channel. Microsoft 365 (Office) for iOS and Android supports the following configuration scenarios:

- Only allow work or school accounts
- General app configuration
- Data protection settings

> [!IMPORTANT]
> For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise and Microsoft 365 (Office) for Android must be deployed via the Managed Google Play store. For more information, see [Set up enrollment of Android Enterprise personally-owned work profile devices](../enrollment/android-work-profile-enroll.md) and [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).
>  For Android App Configurations, add the Office Hub, Office Hub [HL], and Office Hub [ROW] apps. For more information, see [Support Tip: How to enable Intune app protection policies with the Office mobile](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

Each configuration scenario highlights its specific requirements. For example, whether the configuration scenario requires device enrollment, and thus works with any UEM provider, or requires Intune App Protection Policies.

> [!IMPORTANT]
> App configuration keys are case sensitive. Use the proper casing to ensure the configuration takes effect.

> [!NOTE]
> With Microsoft Intune, app configuration delivered through the MDM OS channel is referred to as a **Managed Devices** App Configuration Policy (ACP); app configuration delivered through the App Protection Policy channel is referred to as a **Managed Apps** App Configuration Policy.

## Only allow work or school accounts

Respecting the data security and compliance policies of our largest and highly regulated customers is a key pillar to the Microsoft 365 value. Some companies have a requirement to capture all communications information within their corporate environment, as well as, ensure the devices are only used for corporate communications. To support these requirements, Microsoft 365 (Office) for Android on enrolled devices can be configured to only allow a single corporate account to be provisioned within the app.

You can learn more about configuring the org allowed accounts mode setting here:

- [Android setting](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-apps)
- [iOS setting](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-apps)

This configuration scenario only works with enrolled devices. However, any UEM provider is supported. If you are not using Microsoft Intune, you need to consult with your UEM documentation on how to deploy these configuration keys.

## General app configuration scenarios

Microsoft 365 (Office) for iOS/iPadOS and Android offers administrators the ability to customize the default configuration for several in-app settings using either [iOS/iPadOS](../apps/app-configuration-policies-use-ios.md) or [Android](../apps/app-configuration-policies-use-android.md) app configuration policies.  This capability is offered for both enrolled devices via any UEM provider and for devices that are not enrolled when Microsoft 365 (Office) for iOS and Android has an Intune App Protection Policy applied.

> [!NOTE]
> If an App Protection Policy is targeted to the users, the recommendation is to deploy the general app configuration settings in a **Managed Apps** enrollment model. This ensures the App Configuration Policy is deployed to both enrolled devices and unenrolled devices. 

Microsoft 365 (Office) supports the following settings for configuration:

- [Manage the creation of Sticky Notes](#manage-the-creation-of-sticky-notes)
- [Set add-ins preference](#set-add-ins-preference)
- [Manage Teams apps running on Microsoft 365 (Office) for iOS and Android](#manage-teams-apps-running-on-microsoft-365-office-for-ios-and-android)
- [Enable or disable Microsoft 365 Feed for iOS and Android](#enable-or-disable-microsoft-365-feed-for-ios-and-android)

### Manage the creation of Sticky Notes

By default, Microsoft 365 (Office) for iOS and Android enables users to create Sticky Notes. For users with Exchange Online mailboxes, the notes are synchronized into the user's mailbox. For users with on-premises mailboxes, these notes are only stored on the local device.

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.NotesCreationEnabled    |    **true** (default) enables Sticky Notes creation for the work or school account<br>**false** disables Sticky Notes creation for the work or school account    |

### Set add-ins preference

For iOS/iPadOS devices running Office, you (as the admin) can set whether Microsoft 365 (Office) add-ins are enabled. These app settings can be deployed using an [app configuration policy](../apps/app-configuration-policies-use-ios.md) in Intune.

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.OfficeWebAddinDisableAllCatalogs    |    **true** (default) disables the entire add-in platform<br>**false** enables the add-in platform    |

If you need to enable or disable the Microsoft 365 (Office) Store portion of the platform for iOS devices, you can use the following key.

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.OfficeWebAddinDisableOMEXCatalog    |    **true** (default) disables only the Microsoft 365 (Office) Store portion of the platform<br>**false** enables the Microsoft 365 (Office) Store portion of the platform<br>**NOTE:** Sideloaded will continue to work.    |

For more information about adding configuration keys, see [Add app configuration policies for managed iOS/iPadOS devices](../apps/app-configuration-policies-use-ios.md).

### Manage Teams apps running on Microsoft 365 (Office) for iOS and Android

IT admins can manage access to Teams apps by creating [custom permission policies](/MicrosoftTeams/teams-app-permission-policies#create-a-custom-app-permission-policy) and [assigning these policies to users](/MicrosoftTeams/policy-assignment-overview) using Teams admin center. You can now also run Teams personal tab apps in Microsoft 365 (Office) for iOS and Android. Teams personal tab apps built using [Microsoft Teams JavaScript client SDK v2](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk?tabs=javascript%2Cmanifest-teams-toolkit) (version 2.0.0) and [Teams App manifest](/microsoftteams/platform/resources/schema/manifest-schema) (version 1.13) appear in Microsoft 365 (Office) for iOS and Android under the “Apps” menu.

There may be additional management requirements specific to Microsoft 365 (Office) for iOS and Android. You may want to:
- Only allow specific users in your organization to try enhanced Teams apps on Microsoft 365 (Office) for iOS and Android, or
- Block all users in your organization from using enhanced Teams apps on Microsoft 365 (Office) for iOS and Android.

To manage these, you can use the following key:

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.officemobile.TeamsApps.IsAllowed    |    **true** (default) enables Teams apps on Microsoft 365 (Office) for iOS and Android<br>**false** disables Teams apps on Microsoft 365 (Office) for iOS and Android    |

This key can be used both by managed devices and managed apps.

### Data protection settings in Microsoft 365 (Office)

You can enable or disable offline caching when **Save As to Local Storage** is blocked by the [app protection policy](../apps/app-protection-policies.md). 

> [!IMPORTANT]
> This setting is only applicable to the Microsoft 365 (Office) app on Android.
To configure this setting, you can use the following key:

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.IntuneMAMOnly.AllowOfflineCachingWhenSaveAsBlocked   |    **false** (default) disables offline caching when **Save As to local storage** is blocked<br>**true** enables offline caching when **Save As to local storage** is blocked    |


### Enable or disable Microsoft 365 Feed for iOS and Android

Admins can now enable or disable the Microsoft 365 Feed by configuring the following setting in the Intune admin center. To deploy this app setting, use an [app configuration policy](app-configuration-policies-overview.md) in Intune.

To manage the Microsoft 365 Feed, you can use the following key:

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.officemobile.Feed.IsAllowed    |    **true** (default) Feed is enabled for the tenant<br>**false** disables Feed for the tenant    |

This key can be used by managed devices and managed apps.


### Copilot with enterprise data protection

Admins can now enable or disable Copilot in Microsoft 365 app by configuring the following setting in the Intune admin center. To deploy this app setting, use an [app configuration policy](app-configuration-policies-overview.md) in Intune.

To manage Copilot in Microsoft 365 app, you can use the following key:

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.officemobile.BingChatEnterprise.IsAllowed    |    **true** (default) Copilot is enabled for the tenant<br>**false** disables Copilot for the tenant    |

This key can be used by managed devices and managed apps.

## Next steps

- [What are app protection policies?](app-protection-policy.md) 
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
