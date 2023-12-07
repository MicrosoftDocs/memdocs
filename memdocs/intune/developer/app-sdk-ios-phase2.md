---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - MSAL prerequisite and setup 
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. MSAL prerequisite and setup
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/01/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 8e280d23-2a25-4a84-9bcb-210b30c63c0b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: has-adal-ref
ms.collection:
- tier3
- M365-identity-device-management
- iOS/iPadOS
---

# Intune App SDK for iOS - MSAL prerequisite and setup

## Setup MSAL

The Intune App SDK uses the [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-objc) for its authentication and conditional launch scenarios. It also relies on MSAL to register the user identity with the MAM service for management without device enrollment scenarios.

<a name='set-up-and-configure-an-aad-app-registration'></a>

### Set up and configure a Microsoft Entra app registration
MSAL requires apps to [register](/azure/active-directory/develop/quickstart-register-app) with Microsoft Entra ID and create a unique client ID and redirect URI, to guarantee the security of the tokens granted to the app. If your application already uses MSAL for its own authentication, then there should already be a Microsoft Entra app registration/client ID/redirect URI associated with the app. 

If your app doesn't already use MSAL, you'll need to configure an app registration in Microsoft Entra ID and specify the client ID and redirect URI that the Intune SDK should use.  

If your app currently uses ADAL to authenticate users, see [Migrate applications to MSAL for iOS and macOS](/azure/active-directory/develop/migrate-objc-adal-msal) for more information on migrating your app from ADAL to MSAL.

It's recommended that your app links to the latest release of [MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-objc/releases).

### Link MSAL to Your Project

Follow the [installation](https://github.com/AzureAD/microsoft-authentication-library-for-objc#installation) section to put the MSAL binaries in your app.

### Configure MSAL

Follow the [configuration](https://github.com/AzureAD/microsoft-authentication-library-for-objc#configuring-msal) section to configure MSAL. Make sure you follow all the steps in the configuration section. Disregard step one if your app is already registered in Microsoft Entra ID. 

The points below contain additional information to configure MSAL and link to it. Follow these if they apply to your application.

* If your app doesn't have any keychain access groups defined, add the app's bundle ID as the first group.
* Enable MSAL single sign-on (SSO) by adding `com.microsoft.adalcache` to the keychain access groups.
* In the case you're explicitly setting the MSAL shared cache keychain group, make sure it's set to `<appidprefix>.com.microsoft.adalcache`. MSAL will set this for you unless you override it. If you want to specify a custom keychain group to replace `com.microsoft.adalcache`, specify that in the Info.plist file under IntuneMAMSettings, by using the key `ADALCacheKeychainGroupOverride`.


### Configure MSAL settings for the Intune App SDK

Once an app registration has been configured for your application in Microsoft Entra ID, you can configure the Intune App SDK to use the settings from your app registration during authentication against Microsoft Entra ID. See [Configure settings for the Intune App SDK](#configure-msal-settings-for-the-intune-app-sdk) for information on populating the following settings:  

* ADALClientId
* ADALAuthority
* ADALRedirectUri
* ADALRedirectScheme
* ADALCacheKeychainGroupOverride

The following configurations are required:

1. In the project's Info.plist file, under the **IntuneMAMSettings** dictionary with the key name `ADALClientId`, specify the client ID to be used for MSAL calls.

2. If the Microsoft Entra app registration which maps to the client ID configured in step 1 is configured for use in only a single Microsoft Entra tenant, configure the `ADALAuthority` key under the **IntuneMAMSettings** dictionary within the application's Info.plist file. Specify the Microsoft Entra authority to be used by MSAL for acquiring tokens for the Intune mobile application management service.

3. Also under the **IntuneMAMSettings** dictionary with the key name `ADALRedirectUri`, specify the redirect URI to be used for MSAL calls. Alternatively, you could specify `ADALRedirectScheme` instead, if the application's redirect URI is in the format `scheme://bundle_id`.

   Alternatively, apps can override these Microsoft Entra settings at runtime. To do this, simply set the `aadAuthorityUriOverride`, `aadClientIdOverride`, and `aadRedirectUriOverride` properties on the `IntuneMAMSettings` class.

4. Ensure the steps to give your iOS app permissions to the Intune Mobile App Management (MAM) service are followed. Use the instructions in the [getting started with the Intune SDK guide](app-sdk-get-started.md#next-steps-after-integration) under [Give your app access to the Intune Mobile App Management service](app-sdk-get-started.md#give-your-app-access-to-the-intune-mobile-app-management-service).  

   > [!NOTE]
   > If the app protection policy is related to managed devices, creating an app configuration profile of the application that has Intune integrated is also necessary.
   >
   > The Info.plist approach is recommended for all settings which are static and do not need to be determined at runtime. Values assigned to the `IntuneMAMSettings` class properties at runtime take precedence over any corresponding values specified in the Info.plist, and will persist even after the app is restarted. The SDK will continue to use them for policy check-ins until the user is unenrolled or the values are cleared or changed.

### Special considerations when using MSAL for app-initiated authentication

It's recommended that applications don't use SFSafariViewController, SFAuththenticationSession or ASWebAuthenticationSession as their webview for any app-initiated MSAL interactive auth operations. By default, MSAL uses ASWebAuthenticationSession, so app developers should [explicitly set the webview type](/azure/active-directory/develop/customize-webviews#change-the-default-browser-for-the-request) to WKWebView. If for some reason your app must use a webview type other than WKWebView for any interactive MSAL auth operations, then it must also set `SafariViewControllerBlockedOverride` to `true` under the `IntuneMAMSettings` dictionary in the application's Info.plist. 

> [!WARNING]
> This will turn off Intune's SafariViewController hooks to enable the auth session. This does risk data leaks elsewhere in the app if the application uses SafariViewController to view corporate data, so the application shouldn't show corporate data in any of those webview types.