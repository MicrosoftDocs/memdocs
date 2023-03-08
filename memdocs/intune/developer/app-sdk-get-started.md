---
# required metadata

title: Get started with the Microsoft Intune App SDK 
description: Quickly enable your mobile app for mobile application management (MAM) with Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/06/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 38ebd3f5-cfcc-4204-8a75-6e2f162cd7c1

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune, has-adal-ref
ms.collection:
- tier3
- M365-identity-device-management
---

# Get started with the Microsoft Intune App SDK

This guide will help you quickly enable your mobile app to support app protection policies with Microsoft Intune. You may find it useful to first understand the benefits of the Intune App SDK, as explained in the [Intune App SDK overview](app-sdk.md).

The Intune App SDK supports similar scenarios across iOS and Android, and is intended to create a consistent experience across the platforms for IT admins. But there are small differences in the support of certain features, because of platform differences and limitations.

## Register your store app with Microsoft

### If your app is internal to your organization and will not be publicly available:

You _**do not need**_ to register your app. For internal [line-of-business (LOB) apps](../apps/apps-add.md#app-types-in-microsoft-intune) that were written by or for your company, the IT administrator will deploy the app internally. Intune will detect that the app has been built with the SDK, and will let the IT administrator apply app protection policies to it. You can skip to the section [Enable your iOS or Android app for app protection policy](#enable-your-ios-or-android-app-for-app-protection-policy).

### If your app will be released to a public app store, like the Apple App Store or Google Play:

You _**must**_ first register your app with Microsoft Intune and agree to the registration terms. IT administrators can then apply an app protection policy to the managed app, which will be listed as an [Partner productivity apps](../apps/apps-supported-intune-apps.md#partner-productivity-apps).

Until registration has been finished and confirmed by the Microsoft Intune team, Intune administrators will not have the option to apply app protection policy to your app's deep link. Microsoft will also add your app to its [Microsoft Intune Partners page](https://www.microsoft.com/cloud-platform/microsoft-intune-apps). There, the app's icon will be displayed to show that it supports Intune app protection policies.

### The registration process
To begin the registration process, and if you are not already working with a Microsoft contact, fill out the [Microsoft Intune App Partner Questionnaire](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR80SNPjnVA1KsGiZ89UxSdVUMEpZNUFEUzdENENOVEdRMjM5UEpWWjJFVi4u).

We will use the email addresses listed in your questionnaire response to reach out and continue the registration process. Additionally, we use your registration email address to contact you if we have any concerns.

> [!NOTE]
> All information collected in the questionnaire and through email correspondence with the Microsoft Intune team will honor the [Microsoft Privacy Statement](https://www.microsoft.com/privacystatement/default.aspx).

**What to expect in the registration process**:

1. After you have submitted the questionnaire, we will contact you via your registration email address, to either confirm successful receipt or request additional information to finish the registration.

2. After we receive all necessary information from you, we will send you the Microsoft Intune App Partner Agreement to sign. This agreement describes the terms that your company must accept before it becomes a Microsoft Intune app partner.

3. You will be notified when your app is successfully registered with the Microsoft Intune service and when your app is featured on the [Microsoft Intune partners](https://www.microsoft.com/cloud-platform/microsoft-intune-apps) site.

4. Finally, your app's deep link will be added to the next monthly Intune Service update. For example, if the registration information is finished in July, the deep link will be supported in mid-August.

The deep link is the link to your app's listing in the public app store. If your app's deep link changes in the future, you will need to re-register your app.

## Download the SDK files

The Intune App SDKs for native iOS and Android are hosted on a Microsoft GitHub account. These public repositories have the SDK files for native iOS and Android, respectively:

* [Intune App SDK for iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios)
* [Intune App SDK for Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android)

If your app is a Xamarin app, use this SDK variant:

* [Intune App SDK Xamarin Bindings](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)

It's a good idea to sign up for a GitHub account that you can use to fork and pull from our repositories. GitHub lets developers communicate with our product team, open issues and receive quick responses, view release notes, and provide feedback to Microsoft. For questions on the Intune App SDK GitHub, contact msintuneappsdk@microsoft.com.

## Enable your iOS or Android app for app protection policy

You will need one of the following developer guides to help you integrate the Intune App SDK into your app:

* **[Intune App SDK for iOS Developer Guide](app-sdk-ios.md)**: This document will walk you step-by-step through enabling your native iOS app with the Intune App SDK.

* **[Intune App SDK for Android Developer Guide](app-sdk-android.md)**: This document will walk you step-by-step through enabling your native Android app with the Intune App SDK.

* **[Intune App SDK Xamarin Bindings guide](app-sdk-xamarin.md)**: This document will help you build iOS and Android apps using Xamarin for Intune app protection policies.

> [!IMPORTANT]
> Intune regularly releases updates to the Intune App SDK. Regularly check the [Intune App SDK](https://github.com/msintuneappsdk) repositories for updates and incorporate into your software development release cycle to ensure your apps support the latest App Protection Policy settings.

## Enable your iOS or Android app for app based Conditional Access

In addition to enabling your app for app protection policy, the following is required for your app to properly function with Azure ActiveDirectory (AAD) app based Conditional Access:

* App is built with the [Microsoft Authentication Library](/azure/active-directory/develop/reference-v2-libraries) and enabled for AAD broker authentication.

* The [AAD Client ID](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#configure-a-native-client-application) for your app must be unique across iOS and Android platforms.

## Configure Telemetry for your app

Microsoft Intune collects data on usage statistics for your app.

* **Intune App SDK for iOS**: The SDK logs SDK telemetry data on usage events by default. This data is sent to Microsoft Intune.

  * If you choose not to send SDK telemetry data to Microsoft Intune from your app, you must disable telemetry transmission by setting the property `MAMTelemetryDisabled` to "YES" in the IntuneMAMSettings dictionary.

* **Intune App SDK for Android**: The Intune App SDK for Android does not control data collection from your app. The Company Portal application logs telemetry data by default. This data is sent to Microsoft Intune. As per Microsoft Policy, we do not collect any personally identifiable information (PII). 

  * If end users choose not to send this data, they must turn off telemetry under Settings on the Company Portal app. To learn more, see [Turn off Microsoft usage data collection](../user-help/turn-off-microsoft-usage-data-collection-android.md). 

## Line-of-business app version numbers

Line-of-business apps in Intune now display the version number for iOS and Android apps. The number displays in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) in the app list and in the app overview blade. End users can see the app number in the Company Portal app and in the web portal.

### Full version number

The full version number identifies a specific release of the app. The number appears as _Version_(_Build_). For example, 2.2(2.2.17560800). 

The full version number has two components:

- **Version**  
  The version number is the human-readable release number of the app. This is used by end users to identify different releases of the app.

- **Build Number**  
  The build number is an internal number that can be used in app detection and to programmatically manage the app. The build number refers to an iteration of the app that references changes in the code.

### Version and build number in Android and iOS

Android and iOS both use version and build numbers in reference to apps. However, both operating systems have meanings that are OS-specific. The following table explains how these terms are related.

When you are developing a line-of-business application for use in Intune, remember to use both the version and the build number. Intune App management features rely on a meaningful **CFBundleVersion** (for iOS) and **PackageVersionCode** (for Android). These numbers are included in the app manifest. 

Intune|iOS|Android|Description|
|---|---|---|---|
Version number|CFBundleShortVersionString|PackageVersionName |This number indicates a specific release of the app for end users.|
Build number|CFBundleVersion|PackageVersionCode |This number is used to indicate an iteration in the app code.|

#### iOS

- **CFBundleShortVersionString**  
  Specifies the release version number of the bundle. This number identifies a released version of the app. The number is used by end users to reference the app.
- **CFBundleVersion**  
  The build version of the bundle, which identifies an iteration of the bundle. The number may be identify a release or unreleased bundle. The number is used for app detection.

#### Android

- **PackageVersionName**  
  The version number shown to users. This attribute can be set as a raw string or as a reference to a string resource. The string has no other purpose than to be displayed to users.
- **PackageVersionCode**  
  An internal version number. This number is used only to determine whether one version is more recent than another, with higher numbers indicating more recent versions. This is not the version 

## Next steps after integration

### Test your app
After you finish the necessary steps to integrate your iOS or Android app with the Intune App SDK, you will need to ensure that all the app protection policies are enabled and functioning for the user and the IT admin. To test your integrated app, you will need the following:

* **Microsoft Intune test account**: To test your Intune-managed app against Intune app protection features, you will need a Microsoft Intune account.

  * If you are an ISV enabling your iOS or Android store apps for Intune app protection policy, you will receive a promo code after you finish the registration with Microsoft Intune, as outlined in the registration step. The promo code will let you sign up for a Microsoft Intune trial for one year of extended use.

  * If you are developing a line-of-business app that will not be shipped to the store, you are expected to have access to Microsoft Intune through your organization. You can also sign up for a one-month free trial in [Microsoft Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0).

  * If you are testing your app on a mobile device using an end user account, ensure that you have given that account an Intune license by in the Microsoft 365 admin center website after logging in with an admin account, see [Assign Microsoft Intune license](../fundamentals/licenses-assign.md).

* **Intune app protection policies**: To test your app against all the Intune app protection policies, you should know what the expected behavior is for each policy setting. See the descriptions for [iOS app protection policies](../apps/app-protection-policy-settings-ios.md) and [Android app protection policies](../apps/app-protection-policy-settings-android.md). If your app has integrated the Intune SDK, but is not listed in the list of targetable apps, you can specify the app's bundle ID (iOS) or package name (Android) in the text box when selecting 'Custom Apps'. 

* **Troubleshoot**: If you run into any issues while manually testing your app's installation user experience, see [Troubleshoot app installation issues](/troubleshoot/mem/intune/troubleshoot-app-install). 

### Give your app access to the Intune app protection service (optional)

If your app is using its own custom Azure Active Directory (AAD) settings for authentication, then the following steps should be taken for both public store apps, as well as internal LOB apps. The steps **do not need to be taken if your app is using the Intune SDK default client ID**. 

Once you have registered your app within an Azure tenant, and it is showing up under **All Applications**, you must give your app access to the Intune app protection service (previously known as MAM service). In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431):

1. Go to the **Azure Active Directory** blade.
2. Under **App registrations**, go to the listing set up for the application.
3. Click **+ Add a permission**.
4. Click on the **APIs my organization uses**. 
5. In the search box, enter **Microsoft Mobile Application Management**.
6. Under **Delegated Permissions**, select the **DeviceManagementManagedApps.ReadWrite: Read and Write the User's App Management Data*** checkbox.
7. Click **Add permissions**.

### Badge your app (optional)

After validating that Intune app protection policies work in your app, you can badge your app icon with the Intune app protection logo.

This badge indicates to IT administrators, end-users, and potential Intune customers that your app works with Intune app protection policies. It encourages the usage and adoption of your app by Intune customers.

The badge is a briefcase icon and can be seen in the samples below:

![Intune app protection policies - Badge example 1](./media/app-sdk-get-started/badge-example-1.png) ![Intune app protection policies - Badge example 2](./media/app-sdk-get-started/badge-example-2.png)

**What you'll need to badge your app**:

* An image manipulation application that can read **.eps** files, or an Adobe application that can read **.ai** files.

* You can find the [Intune app badge assets and guidelines](https://github.com/msintuneappsdk/intune-app-partner-badge) on the Microsoft Intune GitHub.
