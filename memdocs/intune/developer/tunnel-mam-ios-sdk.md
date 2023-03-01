---
# required metadata

title: Microsoft Tunnel for MAM iOS SDK developer guide 
description: The Microsoft Tunnel for MAM iOS SDK lets you incorporate support for Mobile Application Management (MAM) Tunnel into your native iOS app. iOS/iPadOS app developers should use this article to integrate per-app VPN when they're creating and developing line of business (LOB) apps.
keywords:
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/31/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid:  
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ochukwunyere, wicale
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: has-adal-ref
ms.collection:
- tier2
- M365-identity-device-management
- iOS/iPadOS

---

# Microsoft Tunnel for MAM iOS SDK developer guide

The Microsoft Tunnel for MAM iOS SDK developer guide is a resource for developers. It helps developers integrate and configure the SDK into an iOS/iPadOS app. For an overview of the Microsoft Tunnel for MAM, go to [Microsoft Tunnel for MAM for iOS/iPadOS - Intune admin guide](../protect/microsoft-tunnel-mam-ios.md).

This guide covers different parts of the integration process in your Xcode app project, including installing the frameworks, configuring the `info.plist` file, build settings, key sharing, and implementing the SDK's delegate methods.

These components are critical in the development of an iOS/iPadOS app. Developers must understand how to navigate and configure the SDK components. If you're new to Xcode and iOS/iPadOS app development, then this guide can help. It provides an overview of where to find the different SDK components and how to use these elements in your app projects.

This feature applies to:

- iOS/iPadOS

## What's in the SDK Repository

The SDK repository includes the following frameworks. You'll add these frameworks to your app project in a later step:

- `crypto.xcframework`
- `MCPCommon.xcframework`
- `MCPCore.xcframework`
- `MCPPluginUnencryptedFile.xcframework`
- `MicrosoftTunnelApi.xcframework`
- `MSTAPNextPluginSecurityOpenssl.xcframework`
- `MSTAPNextPluginSwiftSupport.xcframework`
- `MSTAPNextPluginVpnMicrosoftTunnel.xcframework`
- `ssl.xcframework`

## Prerequisites

To use the Microsoft Tunnel for MAM iOS SDK, the following prerequisites are required:

- A macOS computer with Xcode 14.0 or newer installed
- Your line of business (LOB) iOS/iPadOS app must be targeted for iOS/iPadOS 14.0 or newer.
- There are two GitHub SDKs you need to download and integrate with your iOS app in Xcode. Make sure the following projects build successfully before you continue with the Microsoft Tunnel for MAM iOS SDK:

  1. **[Intune App SDK for iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios)** (opens a GitHub site): At a minimum, install the 16.1.1 version​.

      At this site, also review the **Microsoft License Terms Intune App SDK for iOS** file.

      For your records, keep a copy of the license terms. By downloading and using the Microsoft Tunnel for MAM iOS SDK, you agree to the license terms. If you don't accept the license terms, then don't use the software.

  2. **[Microsoft Authentication Library (MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-objc)** (opens a GitHub site): At a minimum, install the 1.2.3​ version.

- Install and set up the [Microsoft Tunnel for MAM iOS SDK (public preview)](https://aka.ms/MAMTunneliOSGithubLink) (opens a GitHub site). This SDK is the focus of this article.

  > [!IMPORTANT]
  > Intune regularly releases updates to the Microsoft Tunnel for MAM iOS SDK. Regularly, check the [Microsoft Tunnel for MAM iOS SDK](https://aka.ms/MAMTunneliOSGithubLink) for updates. Add these updates into your software development release cycle. You want to make sure your apps support the Microsoft Tunnel Gateway updates and feature enhancements.

## How the Microsoft Tunnel for MAM iOS SDK works

The Tunnel for MAM iOS SDK enables iOS/iPadOS apps to establish an "in-app" VPN connection. The VPN connection only exists within the app.

To summarize, these in-app VPN connections are:

- Discrete, not device-level VPN connections
- Scoped only to the application network layer

When an app makes a network call, the SDK intercepts the network call and establishes the VPN connection. This in-app VPN connection isn't shown in the Settings app on the iOS/iPadOS device.

### Architecture: Tunnel for MAM iOS SDK

The following image describes the flow from a managed app that's successfully integrated with Tunnel for MAM iOS SDK:

:::image type="content" source="./media/tunnel-mam-ios-sdk/tunnel-for-mam-ios-flow.png" alt-text="Drawing of the Microsoft Tunnel Gateway for MAM on iOS/iPadOS architecture in Microsoft Intune." lightbox="./media/tunnel-mam-ios-sdk/tunnel-for-mam-ios-flow.png":::

0. Upon initial launch of the app, a connection is made using the Microsoft Tunnel for MAM SDK for iOS.  
1. The tunnel gets a device authentication token from Azure AD.

    If the device signed in to another MAM enabled app, such as Outlook, Edge, or Microsoft 365 mobile app, then the device may already have an Azure AD authentication token. If a valid authentication token already exists, then the existing token is used.

2. A TCP Connect happens, which is a TLS Handshake between the token and the tunnel server.
3. If UDP is enabled on the Microsoft Tunnel Gateway, then a data-channel connection using DTLS is made. If UDP is disabled, then TCP establishes the data channel to Tunnel gateway.

    For more information, go to the TCP and UDP notes in the [Microsoft Tunnel overview - architecture](../protect/microsoft-tunnel-overview.md#architecture).

4. When the mobile app makes a connection to an on-premises corporate resource:

    1. A Microsoft Tunnel for MAM API requests to connect to the company resource.
    2. An encrypted web request is created and sent to the corporate resource.

## Xcode Tasks

This section lists and describes the Xcode tasks you must complete, including:

- Add the frameworks and libraries​
- Review and update the following features:
  - `info.plist`​ file
  - Build settings​
  - Keychain sharing
- Use the samples to update the Xcode AppDelegate project and add a Microsoft Tunnel delegate file

### Step 1 - Add the frameworks and libraries

The following frameworks include the necessary APIs and delegate methods for communicating with the [Intune Microsoft Tunnel Gateway](../protect/microsoft-tunnel-overview.md). They implement the Microsoft Tunnel VPN features within the app.

To enable the Tunnel for MAM iOS SDK, use the following steps:

1. Download and extract the Tunnel for MAM iOS SDK to a folder on a macOS computer. This task is also listed in the [Prerequisites](#prerequisites).

    Copy the following nine frameworks to the Xcode app project frameworks folder:

    - `crypto.xcframework`
    - `MCPCommon.xcframework`
    - `MCPCore.xcframework`
    - `MCPPluginUnencryptedFile.xcframework`
    - `MicrosoftTunnelApi.xcframework`
    - `MSTAPNextPluginSecurityOpenssl.xcframework`
    - `MSTAPNextPluginSwiftSupport.xcframework`
    - `MSTAPNextPluginVpnMicrosoftTunnel.xcframework`
    - `ssl.xcframework`

2. In the Xcode project, select your app project > **Add files**. In the following example, files are added to an app project called “Flash Chat”:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/add-files-xcode-project.png" alt-text="Screen that shows how to add files to the app project in Xcode on a macOS device.":::

3. In **PROJECT** > **TARGETS**, select **Build Phases** > **Embed Frameworks**. Add (**+**) all nine frameworks:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-embed-frameworks-xcode.png" alt-text="Screenshot that shows embedding frameworks in Xcode on a macOS device.":::

    The following example shows all nine frameworks added:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/all-frameworks-embedded-xcode.png" alt-text="Screenshot that shows all the Microsoft Tunnel frameworks embedded in Xcode on a macOS device.":::

4. In **PROJECT** > **TARGETS**, select **Build Phases** > **Link Binary with Libraries**. In the list, only the `MicrosoftTunnelApi.xcframework` framework should be added. If other frameworks are listed, remove them using the minus (**-**):

    :::image type="content" source="./media/tunnel-mam-ios-sdk/remove-frameworks-link-binary-with-libraries-xcode.png" alt-text="Screenshot that shows how to remove frameworks in Link Binary with Libraries in Xcode on a macOS device.":::

### Step 2 - Update the `info.plist` file

In the `info.plist` for the Xcode app project, confirm the following settings:

- **Bundle ID**: Make sure the same Bundle ID listed in the [Azure AD App registration for the iOS mobile app](../protect/microsoft-tunnel-mam-ios.md) is the same Bundle ID in your app project:

  To check the Bundle ID:

  1. Go to **PROJECT** > **TARGETS** > **General**.
  2. Select **Identity** > **Bundle Identifier**:

      :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-general-identity-bundleid.png" alt-text="Screenshot that shows selecting project, targets, general, and identity to add the bundle ID in Xcode on a macOS device." lightbox="./media/tunnel-mam-ios-sdk/project-targets-general-identity-bundleid.png":::

- **URL Types**: In **PROJECT** > **TARGETS**, select **Info**.

  In **URL Types**, confirm the `$(PRODUCT_BUNDLE_IDENTIFIER)` variable is there. When you integrated the **Intune App SDK for iOS** with your app project ([a required prerequisite](#prerequisites)), this variable should have been created.

  **If the variable isn't there**, then you need to add it:

  1. Using the **Intune App SDK for iOS** ([a required prerequisite](#prerequisites)), create an `info.plist` **Array** property and name it **Queried URL Schemes**.

      Add the string items listed in the [Intune App SDK for iOS developer guide – Step 5](app-sdk-ios.md#build-the-sdk-into-your-mobile-app). This step creates the Intune MAM SDK URL schemes.
  
      The following example shows the info.plist using **Queried URL Schemes**:

      :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-queried-url-schemes-xcode.png" alt-text="Screenshot that shows selecting project, targets, info, queried URL schemes values in Xcode on a macOS device." lightbox="./media/tunnel-mam-ios-sdk/project-targets-info-queried-url-schemes-xcode.png":::

  2. Add the `$(PRODUCT_BUNDLE_IDENTIFIER)` variable.

      The following example shows the `$(PRODUCT_BUNDLE_IDENTIFIER)` variable in **URL Types**:

      :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-url-types-xcode.png" alt-text="Screenshot that shows selecting project, targets, info, URL types in Xcode on a macOS device." lightbox="./media/tunnel-mam-ios-sdk/project-targets-info-url-types-xcode.png":::

- **IntuneMAMSettings**: Confirm the following MSAL settings are configured with the appropriate Azure AD app registration values:

  1. Go to **PROJECT** > **TARGETS** > **Info**.
  2. Select **IntuneMAMSettings**. Confirm your settings:

      - `ADALAuthority`: Enter the Azure AD tenant ID, like `https://login.microsoftonline.com/USE_YOUR_ Directory (tenant) ID`.
      - `ADALClientId`: Enter the application client ID.
      - `ADALRedirectUri`: Enter `msauth.$(PRODUCT_BUNDLE_IDENTIFIER):/auth`.

  When you integrated the **Intune App SDK for iOS** with your app project ([a required prerequisite](#prerequisites)), these settings should have been configured.

  **If these settings aren't configured**, then you need to configure them. To create the IntuneMAMSettings `info.plist` Dictionary property and associated Microsoft Authentication Library strings, follow the **Intune App SDK for iOS** ([a required prerequisite](#prerequisites)) developer guide at [Configure MSAL settings for Intune App SDK](app-sdk-ios.md#configure-msal-settings-for-the-intune-app-sdk) guidance.

  The following example shows these values configured:

  :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-intunemamsettings-xcode.png" alt-text="Screenshot that shows selecting project, targets, info, IntuneMAMSetting in Xcode on a macOS device." lightbox="./media/tunnel-mam-ios-sdk/project-targets-info-intunemamsettings-xcode.png":::

### Step 3 - Turn off Bitcode

1. Go to **PROJECT** > **TARGETS** > **Build settings**.
2. Select **Build options** > **Enable Bitcode**.
3. Select **No**.

:::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-build-settings-enable-bitcode-xcode.png" alt-text="Screenshot that shows selecting project, targets, build settings, build options, and disabling bitcode in Xcode on a macOS device." lightbox="./media/tunnel-mam-ios-sdk/project-targets-build-settings-enable-bitcode-xcode.png":::

### Step 4 - Add keychain sharing

Keychain sharing may or not be present in the app project. If it's not there, add it:

1. Go to **PROJECT** > **TARGETS** > **Signing & Capabilities**.
2. Select **Keychain sharing**.
3. In the **Keychain Groups** list, add (**+**) `com.microsoft.workplacejoin`.

:::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-signing-capabilities-keychain-sharing-xcode.png" alt-text="Screenshot that shows selecting project, targets, Signing & Capabilities, keychain sharing, and adding a keychain group in Xcode on a macOS device." lightbox="./media/tunnel-mam-ios-sdk/project-targets-signing-capabilities-keychain-sharing-xcode.png":::

### Step 5 - Integrate the SDK with your app

✔️ **Use the [`TunnelMAMTestApp2.xcproject`](https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps) sample app**.

Depending on the LOB app and its implementation/intended purpose, the use of the `MicrosoftTunnelApi` may vary. There are some core functionalities to know as you're integrating the SDK with your app:

- All interactions with the Microsoft Tunnel for MAM iOS SDK are handled through a `MicrosoftTunnelAPI` singleton object.
- The `MicrosoftTunnelAPI` object interacts with the app using a delegate that implements a `MicrosoftTunnelDelegate` interface.  

To understand how to write the Microsoft Tunnel delegate and how to initialize the `MicrosoftTunnelAPI`, use the [Microsoft Tunnel for MAM iOS SDK sample apps](https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps) (opens a GitHub site).

In the sample apps, the Xcode project AppDelegate shows:

- How to handle MSAL URL callbacks
- How to start the enrollment and initialization process required for Tunnel

To get started, open the `TunnelMAMTestApp2.xcproject` sample app, and look at the AppDelegate & MicrosoftTunnelDelegate in the app project.

## Sample apps

✔️ **Download at [Microsoft Tunnel for MAM iOS SDK sample apps](https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps)** (opens a GitHub site).

These sample apps can help you get started and cover different scenarios.

## MicrosoftTunnelAPI methods

The `MicrosoftTunnelAPI` includes the following methods:

- `Initialize` – Checks and sets the VPN configurations, sets up logging, and sets up the `MicrosoftTunnelAPI` instance.

- `Connect` – Gets the `MicrosoftTunnelAPI` instance and enables network traffic interception. If the API is uninitialized, an error is shown.

- `Disconnect` - Gets the `MicrosoftTunnelAPI` instance and disables network traffic interception. If the API is uninitialized, an error is shown.

- `onTokenRequired` – Optional. If your app already integrates with either `IntuneMAM` or MSAL, you'll need to implement this `onTokenRequired` method. This method uses the `IntuneMAMSettings` and MSAL to get a valid authentication token to connect to the Microsoft Tunnel Gateway.

- `Logging` – There are some different logging classes, denoted by `k`. For example, `kLoggingClassConnect` creates logging output in the Xcode console. These logging config keys can be added to the delegate config. There are some examples of these logging classes in the [sample apps](#sample-apps).

  - `kLoggingClassInternal`
  - `kLoggingClassConnect`
  - `kLoggingClassPacket`
  - `kLoggingClassSocket`
  - `kLoggingClassHttp`
  - `kLoggingClassIntune`
  - `kLoggingClassMobileAccess`
  - `kLoggingSeverityDebug`
  - `kLoggingSeverityInfo`
  - `kLoggingSeverityWarn`
  - `kLoggingSeverityMinor`
  - `kLoggingSeverityMajor`
  - `kLoggingSeverityCrit`

> [!WARNING]
> Don't use debug keys in deployed apps. The keys can log and show user identifiable information and security data.

### Logging on iOS/iPadOS LOB apps

Integrating the SDK doesn't automatically enable logging. The developer must add the appropriate code to implement the logging delegate framework and make the appropriate logging calls. The specific implementation varies depending on the SDK and the developer's requirements.

The developer should:

- Make sure they don't include any customer identifiable or end-user personal data in their logging. They must comply with privacy regulations.

- Consult and work with the organization's company/organization privacy team. The privacy team can provide guidance on the appropriate data that can be logged and the appropriate ways of handling sensitive data.

> [!WARNING]
> Consult the [Microsoft Tunnel for MAM iOS SDK privacy documentation](https://github.com/msintuneappsdk/ms-intune-tunnel-sdk-ios/blob/main/MAM-Tunnel-Privacy-Doc.pdf) (opens a PDF file in GitHub) for specific guidance regarding logging and data privacy.

### MAM-Tunnel log delegate method example

:::image type="content" source="./media/tunnel-mam-ios-sdk/log-delegate-method-example.png" alt-text="Screenshot that shows a sample Microsoft Tunnel log delegate method in Xcode on a macOS device.":::

:::image type="content" source="./media/tunnel-mam-ios-sdk/log-delegate-method-output-example.png" alt-text="Screenshot that shows a sample Microsoft Tunnel log output in Xcode on a macOS device.":::

## Microsoft Tunnel for Mobile Application Management Privacy information  
Your privacy is important to us.  Review the following privacy related online documentation:

- [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement)
- [Privacy and personal data in Intune](../protect/privacy-personal-data.md)
- [Data storage and processing in Intune](../protect/privacy-data-store-process.md)

When integrating the Microsoft Tunnel for MAM iOS SDK into mobile apps, the following data is collected when a developer:

- Enables the Intune MAM telemetry module in the app

**The data collected may include the following areas:**

- Microsoft Tunnel for MAM SDK version
- Microsoft-generated user information
  - Device ID
- Hardware and software information
  - Device make
  - Device model
  - Device OS version
- Admin and account information
  - Intune Tenant ID
  - Azure AD tenant ID
- Usage measurement:  
  - VPN initialization
  - VPN connect and disconnect events
- Error information
  - Errors related to VPN connection failure

No user identifiable information is collected.

> [!IMPORTANT]
> As a developer, when integrating the SDK it is important to not include any user identifiable data when using code to address and capture messages in your application.

## Known issues

For more known issues, go to the [Microsoft Tunnel for MAM for iOS/iPadOS - Intune admin guide](../protect/microsoft-tunnel-mam-ios.md#known-issues).

- Proxy servers must have a public DNS record or they must be configured using the IP address.

- When you evaluate trusted certificates for protected web servers, SANs (Subject Alternative Names) aren't honored. Only common names are honored.

- If the app doesn't manage the identity **and** the identity is delegated to the Microsoft Tunnel for MAM iOS SDK, then to change the logged in account, the app must manually call into the **Intune App SDK for iOS** to deregister the account.

  For more information on deregistering the account, go to [Microsoft Intune App SDK for iOS developer guide](app-sdk-ios.md#deregister-user-accounts).

  The app identity is managed in a separate keychain. So if you want to use a different user account to sign in and connect to the Tunnel Gateway server, then you must reset the device. Uninstalling and reinstalling the app isn't enough to change the user account.

- Trusted root certificate validation only works for endpoints. It doesn't validate the VPN server.

## Next steps

[Microsoft Tunnel for MAM for iOS/iPadOS - Intune admin guide](../protect/microsoft-tunnel-mam-ios.md)
