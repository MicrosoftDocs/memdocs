---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide - App configuration
description: Understand app configuration features when incorporating Intune mobile app management (MAM) into your Android app.
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
- tier3
- M365-identity-device-management
- Android
ms.custom: intune-classic
---

# Intune App SDK for Android - App configuration

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Plan the Integration](..\developer\app-sdk-android-phase1.md).

## Stage 6: App Configuration

## Stage Goals

- Learn about application configuration options on Android.
- Decide which configurations, if any, your application should add.
- Integrate the Intune App SDK application configuration APIs.
- Implement conflict-resolution logic for your custom application configurations.

## App Configuration on Android

Application configurations, also referred to as managed configurations or application restrictions, are application-specific and developer-defined settings you can add to your app to give administrators added control over the app experience when used in a managed setting.
For example, if your app is a browser, you may choose to add configurations that let administrators pre-set bookmarks, block certain web pages, or disable incognito modes.
Application configuration is an entirely optional, but powerful, tool to enhance your app's management experience.

See [App configuration policies for Microsoft Intune][] for more detail.

### Android's Built-In App Configurations

Android has app configuration built into the platform, called [managed configurations].
These configurations have no dependency on the Intune App SDK and can be enabled on apps that don't integrate the Intune App SDK.
These configurations only apply when your application is used on a device that is managed with one of Google's Android Enterprise modes.
See [Enroll Android devices][] for details on how to set up these Android Enterprise modes in Microsoft Endpoint Manager.
Admins can configure these [application configuration policies for managed Android Enterprise devices][] in Microsoft Endpoint Manager.

Your app can retrieve these admin-configured values either through [Android's `RestrictionsManager`][] or through the Intune App SDK.
See [retrieving app configuration from the SDK][] for more information.

### Intune App SDK App Configurations

The Intune App SDK supports another mechanism for delivering app configurations, separate from Android Enterprise managed configurations.
These configurations are exclusive to Microsoft Intune and only apply to apps that have integrated the Intune App SDK.
However, these configurations aren't limited to devices with Android Enterprise management.
Admins can configure these [application configuration policies for managed apps][] in Microsoft Endpoint Manager.

> [!NOTE]
> App config can also be configured using the Graph API.
> For information, see the [Graph API documentation for MAM Targeted Config][].

Your app must retrieve these admin-configured values through the Intune App SDK.
See [retrieving app configuration from the SDK][] for more information.

## What configurations should I add to my app?

**This guide cannot answer this question for you.**
Only you and your team know what features make your app more valuable when under management.

The following questions may help guide discussions and reveal configurations you may want to add to your app:

- What features does your app offer today?
  - Is there value in disabling any of these features while under management?
  - Is there value in changing any of these features while under management?
- How is your app used under management today?
  - Are there any options that admins could pre-configure on behalf of their users?
  - Are there any actions that admins or end users take, exclusive to managed scenarios?
  - Have your managed users requested features that might not be appropriate for your entire user population?

For every configuration you decide to add to your app, you'll need to define three items:

- **Key** - this string uniquely identifies this setting from other settings. It should be human-readable, as it will be configured by administrators.
- **Type** - what data type is this setting? Is it a string, boolean, integer, array, etc.?
- **Conflict resolution strategy** - how will your app respond if administrators configure multiple values for the same key? In the aforementioned browser example, a bookmark list may combine all values, while a setting to disable incognito may choose to disable if any of the conflicting values is "true".

### Should my app support configuration for Managed Devices or Managed Apps?

Configurations that apply to managed devices and configurations that apply to managed apps are **not mutually exclusive**.
You should consider your users' needs when deciding which type (or both) of configuration to support.

| Configuration area  | Configuration for Managed Devices | Configuration for Managed Apps |
| - | - | - |
| **Device Applicability** | Only applies on devices under Android Enterprise device management. | Applies to all devices, as long as the app integrates the Intune App SDK and the Company Portal is installed. |
| **Platform** | Android only, limited to devices with Google services | iOS App SDK supports the same configurations. As a developer, you can share these keys for a consistent cross-platform experience. |
| **Applicability** | Any EMM | Exclusive to Microsoft Intune |
| **Schema Discoverability** | Schema is publicly available after app upload to Play | Schema discoverability under developer control |

Both types of app configuration rely on key-value pairs.
Microsoft Intune doesn't inspect the contents of these configurations and simply passes the admin-configured values to your app.

The Intune App SDK app configuration API includes admin-configured values from **both** channels.
If your app supports both types of app configuration, use the API as described below.

## Retrieving app configuration from the SDK

Applications can receive configurations from both channels using the [MAMAppConfigManager][] and [MAMAppConfig][] classes.

```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
```

If there's no MAM-registered account, but your app would still like to retrieve Android Enterprise configuration values (which won't be targeted at a specific account), you can pass a `null` or empty string.

> [!NOTE]
> If your app uses the Intune App SDK to retrieve Android Enterprise managed configurations and the Company Portal is not installed, these configurations will be delivered via a `MAMUserNotification` with an empty identity.

Your app can also request the raw data as a list of sets of key-value pairs, instead of querying by specific keys.

```java
List<Map<String, String>> getFullData()
```

Your app can also register for the `REFRESH_APP_CONFIG` notification that informs the app that new app configuration data is available.
If your app caches app configuration data, it **must** register for this notification and invalidate any cached data in the handler.
See [Register for notifications from the SDK][] for more detail.

## Resolving conflicts

 If multiple app configuration policies are targeted at the same app and account, there may be multiple conflicting values available for the same key.

> [!NOTE]
> A value set in the MAM app config will override a value with the same key set in Android Enterprise config.

If an admin configures conflicting values for the same key, Intune doesn't have any way of resolving this conflict automatically and will make all values available to your app.
This type of conflict could happen if the admin targets different app config sets with the same key to multiple groups containing the same account.

Your app can request all values for a given key from a [MAMAppConfig][] object, so you can resolve conflicts with your own business logic:

```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

Alternately, you can request a value to be chosen with one of the built-in conflict resolution strategies:

```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)
```

The available built-in conflict resolution strategies include:

- `BooleanQueryType.Any`, `BooleanQueryType.And`, `BooleanQueryType.Or`
- `NumberQueryType.Any`, `NumberQueryType.Min`, `NumberQueryType.Max`
- `StringQueryType.Any`, `StringQueryType.Min`, `StringQueryType.Max`, where min and max are from an alphabetically ordered list.

## Exit Criteria

Intune is responsible for delivering the app configuration policy values to your app; afterwards, your app is responsible for using those values to change behavior or UI inside the app.
Thorough end-to-end testing should cover both components.

To validate that Intune is properly delivering app configuration policy:

1. Configure an app configuration policy, that is targeted to your app, and deployed to your test account.
    - If your app supports app configuration for managed devices, see [application configuration policies for managed Android Enterprise devices].
    - If your app supports app configuration for managed apps, see [application configuration policies for managed apps].
    - If your app supports both types of app configuration, create both types of policy for testing.
2. Log in to your app with your test account.
    - For managed devices, see [Android enterprise app configuration policies][] and [Enroll Android devices][].
    - For managed apps:
      1. Install both your app and the Intune Company Portal.
      2. Log in to your app with your test account.
3. Navigate through your app to exercise each codepath that calls `MAMAppConfigManager`'s `getAppConfig` or `getFullData`.
    - Logging the results of calls to `getAppConfig` is a simple way to validate which settings are delivered. However, because administrators can enter any data for app configuration settings, be careful not to log any private user data.
4. See [Validate the applied app configuration policy].

Because app configurations are app-specific, only you know how to validate how your app should change behavior or UI for each app configuration setting.

When testing, consider the following:

- Ensuring all scenarios are covered by creating different test app configuration policy with every value your app supports.
- Validating your app's conflict resolution logic by creating multiple test app configuration policies with different values for each setting.
- If your app has registered for the `REFRESH_APP_CONFIG` notification, updating the app configuration policy while your app is in active use, waiting for policy to update, and confirming this codepath is properly exercised.
- If your app supports both types of app configuration, testing both scenarios to ensure your implementation provides the correct identity to `getAppConfig`.


## Next Steps

After you've completed all the [Exit Criteria][] above, your app is now successfully integrated as with app configuration policy.

The subsequent section, [Stage 7: App Participation Features], may or may not be required, depending on your app's desired app protection policy support.
If you're unsure if any of these features apply to your app, revisit [Key Decisions for SDK integration].

<!-- Stage 6 links -->
<!-- internal links -->
[retrieving app configuration from the SDK]:#retrieving-app-configuration-from-the-sdk
[Exit Criteria]:#exit-criteria

<!-- Other SDK Guide Markdown documentation -->
[Stage 1: Planning the Integration]:app-sdk-android-phase1.md
[Key Decisions for SDK integration]:app-sdk-android-phase1.md#key-decisions-for-sdk-integration
[Register for notifications from the SDK]:app-sdk-android-phase7.md#register-for-notifications-from-the-sdk
[Stage 7: App Participation Features]:app-sdk-android-phase7.md

<!-- Microsoft Learn documentation -->
[App configuration policies for Microsoft Intune]:/mem/intune/apps/app-configuration-policies-overview
[Enroll Android devices]:/mem/intune/enrollment/android-enroll 
[application configuration policies for managed Android Enterprise devices]:/mem/intune/apps/app-configuration-policies-use-android
[application configuration policies for managed apps]:/mem/intune/apps/app-configuration-policies-managed-app
[Graph API documentation for MAM Targeted Config]:/graph/api/resources/intune-mam-targetedmanagedappconfiguration
[Validate the applied app configuration policy]:/mem/intune/apps/app-configuration-policies-overview#validate-the-applied-app-configuration-policy
[Android enterprise app configuration policies]:/mem/intune/apps/app-configuration-policies-overview#android-enterprise-app-configuration-policies

<!-- 3rd party links -->
[managed configurations]:https://developer.android.com/work/managed-configurations
[Android's `RestrictionsManager`]:https://developer.android.com/reference/android/content/RestrictionsManager

<!-- Class links -->
[MAMAppConfigManager]:https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/appconfig/MAMAppConfigManager.html
[MAMAppConfig]:https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/appconfig/MAMAppConfig.html