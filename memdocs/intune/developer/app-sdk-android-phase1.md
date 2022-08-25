---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide, stage 1
description: The Microsoft Intune App SDK for Android lets you incorporate Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/24/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- M365-identity-device-management
- Android
ms.custom: intune-classic
---


# Microsoft Intune App SDK for Android developer guide
> [!NOTE]
> This guide is broken into several distinct stages.  Start at [Stage 1: Planning the Integration].

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

# Stage 1: Planning the Integration

This guide is for Android developers who are looking to add support for Microsoft Intune's App Protection Policies inside their existing Android app.

## Stage Goals

* Learn what App Protection Policy settings are available for Android and how these policies will work inside your application.
* Understand the key decision points during the SDK integration process and plan your app's integration.
* Understand the requirements for applications integrating the SDK.
* Create a test Intune tenant and configure an Android App Protection Policy.

## Understanding MAM

Before you start integrating the Intune App SDK into your Android application, take a moment to familiarize yourself with Microsoft Intune's Mobile Application Management solution:

* [What is Microsoft Intune app management] provides a high level overview of MAM capabilities on different platforms
  and where to find these features in the Microsoft Endpoint Manager console.  
* [Intune App SDK overview] goes one layer deeper, describing the current features of the SDK.
* [Android app protection policy settings] describes each Android setting in detail.
  Your app will support these settings by integrating the SDK.
  During the SDK integration process, you will also configure these settings in your own test tenant for validation.

> [!NOTE]
> Some Android App Protection Policy settings require specific code to support.
> See [Stage 7: App Participation Features] for more detail.

## Key Decisions for SDK integration

### Do I have access to my application's source code?

If you do not have access to your application's source code and only have access to the compiled application in either .apk or .aab format, you will not be able to integrate the SDK into your application.
However, your application may still be compatible with Intune app protection policies.
See [App Wrapping Tool for Android] for more details.

### Should my application integrate the Microsoft Authentication Library (MSAL)?

Refer to [Overview of the Microsoft Authentication Library (MSAL)] to determine whether your application will need to integrate MSAL.
Most applications must integrate MSAL before integrating the Intune SDK.

Your app can skip integrating MSAL **only if all of the following are true**:

* Your application does not have or need an interactive log-in and log-out end user experience.
* Your application does not support multiple accounts logged in simultaneously.
* Your application does not need to support non-Intune accounts.
* Your application does not grant access to any resources protected by Conditional Access.

If your app satisfies **all of the above conditions** and does not integrate MSAL, it can still be protected by App Protection Policy, albeit with no option for unmanaged usage. See [Default Enrollment] for details.

See [Stage 2: The MSAL Prerequisite] for instructions on integrating MSAL and additional details on identity scenarios inside your application.

### Is my application single-identity or multi-identity?

Without Intune App Protection Policy support, how does your application handle user authentication and accounts?

* Does your application currently only allow a single account to be logged in?
Does your application explicitly force the logged-in account to log-out *and delete that previous account's data* before allowing another account to log-in?
If so, your application is **single-identity**.

* Does your application currently allow a second account to log-in, even if a different account is already logged in?
Does your application display multiple accounts' data on a shared screen?
Does your application store multiple accounts' data?
Does your application let users switch between different logged in accounts?
If so, your application is **multi-identity** and you will need to follow [Stage 5: Multi-Identity]. **This section is required for your app.**

Even if your application is multi-identity, follow this integration guide in order.
Initially integrating and testing as single-identity will help ensure proper integration and prevent bugs where corporate data ends up unprotected.

### Does my application have or need App Configuration settings?

Android supports [application-specific management configurations] that apply to applications deployed under Android Enterprise management modes. Admins can configure these [application configuration policies for managed Android Enterprise devices] in Microsoft Endpoint Manager.

Intune also supports application configurations that apply to SDK-integrated applications, regardless of device management mode. Admins can configure these [application configuration policies for managed apps] in Microsoft Endpoint Manager.

The Intune App SDK supports both types of application configuration and provides a single API for accessing configurations from both channels. If you application has or will support either of these types of application configuration, you will need to follow [Stage 6: App Configuration].

### Does my application need to define granular protection for data ingress and egress?

If your app lets users save data to or open data from cloud services or to device locations, it must take changes to support enhanced data transfer policy.
See [Policy for limiting data transfer between apps and device or cloud storage locations] in [Stage 7: App Participation Features].

### Does my application display notifications that contain user specific information?

Multi-identity apps must take code changes to properly honor notification policy. Single-identity apps may want to take code changes so this notification policy does not block 100% of their app's notifications. See [Policy for restricting content inside notifications] in [Stage 7: App Participation Features].

### Does my application support Android's backup and restore functionality?

Android supports [backup and restore] functionality to preserve data and personalization for users when they upgrade to a new device or re-install your app.

Intune also supports backup and restore functionality for SDK-integrated applications, to ensure corporate data cannot be leaked through a restore. 

If your app supports this functionality, it must take code changes to protect corporate data during restore. 
See [Policy for protecting backup data] in [Stage 7: App Participation Features].

### Does my application have resources that should be protected by Conditional Access?

[Conditional Access (CA)] is an [Azure Active Directory (AAD)]
feature which can be used to control access to AAD resources.
Intune administrators can define CA rules which allow resource access only from devices or apps which are managed by Intune.

Intune supports 2 types of CA: **device-based CA** and **app-based CA**, aka [App Protection CA].
Device-based CA blocks access to protected resources until the entire device is managed by Intune.
App-based CA blocks access to protected resources until the specific app is managed by Intune App Protection Policies.

If your app acquires any AAD access tokens and accesses resources which can be CA-protected, you will need to follow [Support App Protection CA] in [Stage 7: App Participation Features].

### Does my application have a distinct theme that needs to persist across UI shown by the Intune App SDK?

By default, the Intune App SDK will display policy enforcement UI components colored according to the default theme.

The ability to override the default theme is cosmetic and optional. See [Providing a Custom Theme] in [Stage 7: App Participation Features].

## Requirements

### Company Portal app

The Intune App SDK for Android relies on the presence of the [Company Portal] app on the device to enable app protection policies. The Company Portal retrieves app protection policies from the Intune service. When an SDK-integrated app initializes, it loads policy and code to enforce that policy from the Company Portal.

> [!NOTE]
> When the Company Portal app is not on the device, an SDK-integrated app behaves the same as a normal app that does not support Intune app protection policies.
> Even if the Company Portal app is on the device, an SDK-integrated app behaves the same as a normal when the end user is not targeted with app protection policy.

The user is ***not*** required to sign into or even launch the Company Portal app for App Protection Policy to function.

### Android versions

The SDK fully supports Android API 28 (Android 9.0) through Android API 32 (Android 12L).
In order to target Android API 31-32 (Android 12-12L), you must use Intune App SDK `v8.0.0` or later.

APIs 26 through 27 (Android 8.0 - 8.1) are in limited support.
The Company Portal app is not supported below Android API 26 (Android 8.0).
App Protection Policy is not supported below Android API 28 (Android 9.0).

If your app declares `minSdkVersion` to an API level below API 28 (Android 9.0), the Intune App SDK will not block app usage for users who are not targeted by App Protection Policy.

### Telemetry

The Intune App SDK for Android does not control data collection from your app. The Company Portal application logs system-generated data by default. This data is sent to Microsoft Intune. As per Microsoft Policy, Intune does not collect any personal data.

> [!TIP]
> If end users choose not to send this data, they must turn off telemetry under Settings on the Company Portal app. To learn more, see [Turn off Microsoft usage data collection].

## Creating a test Android app protection policy

### Demo tenant setup

If you do not already have a tenant with your company, you can create a demo tenant with or without pre-generated data. You must register as a [Microsoft partner] to access Microsoft CDX.
To create a new account:

1. Navigate to the [Microsoft CDX tenant creation site] and create a Microsoft 365 Enterprise tenant.
2. [Set up Intune] to enable mobile device management (MDM).
3. [Create users].
4. [Create groups].
5. [Assign licenses] as appropriate for your testing.

### App protection policy configuration

[Create and assign app protection policies] in the Microsoft Endpoint Manager admin center. In addition to creating app protection policies, you can create and assign an [app configuration policy] in Endpoint Manager.

Before you test app protection policy settings within your own application, it's helpful to familiarize yourself with how these settings behave inside other SDK-integrated applications.

> [!TIP]
> If your app isn't listed in the Microsoft Endpoint Manager portal, you can target it with a policy by selecting the **more apps** option and providing the package name in the text box.  
> You must target your app with app protection policy and deploy the policy to a user to successfully test your integration.  
> Even if policy is targeted and deployed, your app will not properly enforce policies until it has successfully integrated the SDK.

## Exit Criteria

* Have you familiarized yourself with how different app protection policy settings will behave inside your Android application?
* Have you reviewed your app and planned your app's integration around MSAL, Conditional Access, Multi-Identity, App Configuration, and all additional SDK features?
* Have you created an Android app protection policy within your test tenant?

## FAQ

### Why is the Company Portal app required for Application Protection Policies on Android?

The Android Company Portal retrieves and persists app protection policies from the Intune service on behalf of all the MAM-enabled applications on device.
When MAM-enabled applications initialize, policy details and code to enforce those policy settings are imported from the Company Portal.
The Company Portal also contains code to reduce the number of authentication prompts shown to end users.
Lastly, the Company Portal collects system data to improve the Intune service; see [Telemetry] for details.

> [!NOTE]
> This Company Portal functionality for app protection policy is specific to Android.

### What happens when users with unsupported devices have App Protection Policy targeted?

The end user experience on Android devices unsupported by Intune app protection policies depends on the device's Android OS version:

| Android OS versions | Google Play behavior | MAM app behavior |
| - | - | - |
| Below Android 8.0           | The Company Portal app will be unavailable to download from Google Play.  Devices that already have the Company Portal installed will not be able to update to new versions of the Company Portal. | MAM functionality will not be universally blocked. However, as SDK-integrated apps ship with new versions of the SDK, MAM-targeted users will be blocked from entering these apps, as they cannot update the Company Portal. When a user, who has MAM policy targeted and has previously logged in to the app, launches such an app, they will be prompted to upgrade the Company Portal.  Users can mitigate this behavior by removing the MAM-targeted account from the application.  If users uninstall the Company Portal, their account will automatically be removed from the app, but they will not be able to log back in with the MAM-targeted account. |
| Android 8.x                 |  The Company Portal app will be available to download from Google Play.  Devices that already have the Company Portal installed will still be able to update to new versions of the Company Portal. | MAM functionality is not actively blocked.  However, Android 8.x is unsupported, and MAM features may not work as expected. |

### What is the App Wrapping tool?

Android app developers have multiple ways to integrate Intune functionality into their applications. In addition to the SDK, which this guide describes, developers can also use the [App Wrapping Tool for Android]. See [Prepare line-of-business apps for app protection policies] for a detailed comparison between the SDK and App Wrapping tool.

## Next Steps

After you have completed all the [Exit Criteria] above, continue to [Stage 2: The MSAL Prerequisite].

<!-- Stage 1 links -->
<!-- internal links -->
[Stage 1: Planning the Integration]:#stage-1-planning-the-integration
[Telemetry]:#telemetry
[Exit Criteria]:#exit-criteria

<!-- Other SDK Guide Markdown docs -->
[Stage 2: The MSAL Prerequisite]:app-sdk-android-phase2.md
[Default Enrollment]:app-sdk-android-appendix.md#default-enrollment
[Stage 5: Multi-Identity]:app-sdk-android-phase5.md
[Stage 6: App Configuration]:app-sdk-android-phase6.md
[Stage 7: App Participation Features]:app-sdk-android-phase7.md
[Policy for limiting data transfer between apps and device or cloud storage locations]:app-sdk-android-phase7.md#policy-for-limiting-data-transfer-between-apps-and-device-or-cloud-storage-locations
[Policy for restricting content inside notifications]:app-sdk-android-phase7.md#policy-for-restricting-content-inside-notifications
[Policy for protecting backup data]:app-sdk-android-phase7.md#policy-for-protecting-backup-data
[Support App Protection CA]:app-sdk-android-phase7.md#support-app-protection-ca
[Providing a Custom Theme]:app-sdk-android-phase7.md#providing-a-custom-theme

<!-- Microsoft docs: Intune overview -->
[Intune App SDK overview]:/mem/intune/developer/app-sdk
[What is Microsoft Intune app management]:/mem/intune/apps/app-management
[Android app protection policy settings]:/mem/intune/apps/app-protection-policy-settings-android
[Overview of the Microsoft Authentication Library (MSAL)]:/azure/active-directory/develop/msal-overview
[Conditional Access (CA)]:/azure/active-directory/develop/active-directory-conditional-access-developer
[Azure Active Directory (AAD)]:https://azure.microsoft.com/services/active-directory/
[App Protection CA]:/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection
[application configuration policies for managed Android Enterprise devices]:/mem/intune/apps/app-configuration-policies-use-android
[application configuration policies for managed apps]:/mem/intune/apps/app-configuration-policies-managed-app
[App Wrapping Tool for Android]:/mem/intune/developer/app-wrapper-prepare-android
[Prepare line-of-business apps for app protection policies]:/mem/intune/developer/apps-prepare-mobile-application-management
[Turn off Microsoft usage data collection]:/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android

<!-- Microsoft docs: Intune testing -->
[Microsoft partner]:https://partner.microsoft.com/business-opportunities/why-microsoft
[Microsoft CDX tenant creation site]:https://cdx.transform.microsoft.com/my-tenants/create-tenant
[Set up Intune]:/mem/intune/fundamentals/setup-steps
[Create users]:/mem/intune/fundamentals/users-add
[Create groups]:/mem/intune/fundamentals/groups-add
[Assign licenses]:/mem/intune/fundamentals/licenses-assign
[Create and assign app protection policies]:/mem/intune/apps/app-protection-policies
[app configuration policy]:/mem/intune/apps/app-configuration-policies-overview

<!-- 3rd party links -->
[application-specific management configurations]:https://developer.android.com/work/managed-configurations
[backup and restore]:https://developer.android.com/guide/topics/data/backup
[Company Portal]:https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal
