---
# required metadata

title: Microsoft Tunnel for MAM iOS SDK developer guide 
description: The Microsoft Tunnel for MAM iOS SDK lets you incorporate support for Mobile Application Management (MAM) Tunnel into your native iOS app.
keywords:
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/23/2023
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
- M365-identity-device-management
- iOS/iPadOS

---

# Microsoft Tunnel for MAM iOS SDK developer guide

The Microsoft Tunnel for MAM iOS SDK developer guide is a resource for developers to help them integrate and configure the SDK into an iOS app.

The guide covers various aspects of the integration process, installing the frameworks, configuring the `info.plist` file, build settings, key sharing, and implementing the SDK's delegate methods.

These components play a crucial role in the development of an iOS app and understanding how to navigate and configure them is essential for any developer. If you are new to Xcode and iOS development, this guide will provide a comprehensive overview of where to find and how to utilize these key elements in your projects.

## What's in the SDK Repository

The SDK repository includes the following frameworks. You use these frameworks in your app project:

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

To use the SDK, you must meet the following requirements:

- A macOS computer with Xcode 14.0 or newer installed
- Your iOS/iPadOS app must be targeted for iOS/iPadOS 14.0 or newer.
- Install the [Intune App SDK for iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios) (opens a GitHub site). At a minimum, install the 16.1.1 version​.
- Install the [Microsoft Authentication Library (MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-objc) (opens a GitHub site). At a minimum, install the 1.2.3​ version.
- Install and set up the [MAM Tunnel-SDK for iOS](https://aka.ms/msintuneappsdk) (opens a GitHub site).
- Review the [Microsoft Tunnel for MAM iOS License Terms](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios).

  For your records, keep a copy of the license terms. By downloading and using the Microsoft Tunnel for MAM iOS SDK, you agree to the license terms. If you don't accept the license terms, then don't use the software.

- ?? Public Preview: Download (THIS NEEDS TO BE A LINK TO GITHUB REPO) the files for the Microsoft Tunnel for MAM iOS SDK on GitHub.

## How the Microsoft Tunnel for MAM iOS SDK works

The Microsoft MAM Tunnel SDK enables iOS/iPadOS apps to establish an "in-app" VPN connection. The VPN connection only exists within the app. These in-app VPN connections are:

- Discrete, not device-level VPN connections
- Scoped only to the application network layer

When an app makes a network call, the SDK intercepts the network call and establishes the VPN connection. The VPN connection isn't shown in the Settings app on the iOS/iPadOS device.

### Architecture: Tunnel for MAM iOS SDK

The following image describes the flow from a managed app that's successfully integrated with Tunnel for MAM iOS SDK:

:::image type="content" source="./media/tunnel-mam-ios-sdk/tunnel-for-mam-ios-flow.png" alt-text="Drawing of the Microsoft Tunnel Gateway for MAM on iOS architecture in Microsoft Intune.":::

0. Upon initial launch of the app, a connection is made using the Tunnel for MAM SDK.  
1. The tunnel gets a device authentication token from Azure AD.

    If the device signed in to another MAM enabled app, such as Outlook, Edge, or Microsoft 365 mobile app, then the device may already have an Azure AD authentication token.

2. A TCP Connect happens, which is a TLS Handshake between the token and the tunnel server.
3. If UDP is enabled on the Microsoft Tunnel Gateway, then a data-channel connection using DTLS is made. If UDP is disabled, then TCP establishes the data channel to Tunnel gateway.

    For more information, go to the TCP and UDP notes in the [Microsoft Tunnel architecture](../protect/microsoft-tunnel-overview.md#architecture).

4. When the mobile app makes a connection to an on-premises corporate resource:

    1. A Microsoft Tunnel for MAM API connect request for that company resource occurs.
    2. An encrypted web request gets made to the corporate resource.

## Build the SDK into your mobile app

?? Is this section needed? It seems to be a repeat of the Prereqs. If it's not needed, I can move the IMPORTANT text to the Prereqs section. ??

Make sure the Intune App SDK for iOS (MAM-SDK) and the Microsoft Authentication Library (MSAL) is successfully integrated into your iOS mobile app into before proceeding.

- Microsoft Intune App SDK for iOS developer guide | Microsoft Learn 
- Setup MSAL 

> [!IMPORTANT]
> Intune regularly releases updates to the Microsoft Tunnel for MAM SDK. Regularly, check the [Tunnel for MAM SDK for iOS](https://aka.ms/MAMTunneliOSGithubLink) for updates. Add these updates into your software development release cycle. You want to make sure your apps support the Microsoft Tunnel Gateway updates and feature enhancements.

## Xcode Tasks

This section lists and describes the Xcode tasks you must complete, including:

- Install the frameworks and libraries​
- Review and update the following features:
  - `info.plist`​ file
  - Build Settings​
  - Keychain Sharing
- Update the Xcode AppDelegate project
- Add a Microsoft Tunnel Delegate file

### Step 1 - Add the frameworks and libraries

The following frameworks include the necessary APIs and delegate methods for communicating with the Intune service. They implement the Microsoft Tunnel VPN features within the app.

??What communicates with the INtune service? Do you mean the app, the Tunnel??

To enable the Tunnel for MAM SDK for iOS, use the following steps:

1. Download and extract the Tunnel for MAM SDK for iOS to a folder on a macOS computer. Copy the following nine frameworks to the Xcode app project frameworks folder:

    - `crypto.xcframework`
    - `MCPCommon.xcframework`
    - `MCPCore.xcframework`
    - `MCPPluginUnencryptedFile.xcframework`
    - `MicrosoftTunnelApi.xcframework`
    - `MSTAPNextPluginSecurityOpenssl.xcframework`
    - `MSTAPNextPluginSwiftSupport.xcframework`
    - `MSTAPNextPluginVpnMicrosoftTunnel.xcframework`
    - `ssl.xcframework`

2. In the Xcode project, add files to your app project. In the following example, the files are added to an app project called “Flash Chat”:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/add-files-xcode-project.png" alt-text="Drawing of adding files to the app project in Xcode on a macOS device.":::

3. In **PROJECT** > **TARGETS**, select **Build Phases** > **Embed Frameworks**. Add (**+**) all nine frameworks:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-embed-frameworks-xcode.png" alt-text="Screenshot that shows embedding frameworks in Xcode on a macOS device.":::

    The following example shows all nine frameworks added:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/all-frameworks-embedded-xcode.png" alt-text="Screenshot that shows all the Microsoft Tunnel frameworks embedded in Xcode on a macOS device.":::

4. In **PROJECT** > **TARGETS**, select **Build Phases** > **Link Binary with Libraries**. In the list, only the `MicrosoftTunnelApi.xcframework` framework should be added. If other frameworks are listed, remove them using the minus (**-**):

    :::image type="content" source="./media/tunnel-mam-ios-sdk/remove-frameworks-link-binary-with-libraries-xcode.png" alt-text="Screenshot that shows how to remove frameworks in Link Binary with Libraries in Xcode on a macOS device.":::

### Step 2 - Update the `info.plist` file

In the info.plist for the Xcode app project, configure the following settings:

- **Bundle ID**: Enter the same the Bundle ID listed in the [Azure AD App registration for the iOS mobile app](../protect/microsoft-tunnel-mam-ios.md).

  To enter the Bundle ID, you have two options:

  - **Option 1**: Expand the app project folder > select **Info**:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/expand-project-folder-select-info-bundleid.png" alt-text="Screenshot that shows expanding the project folder, select info, and add the bundle ID in Xcode on a macOS device.":::

  - **Option 2**: In **PROJECT** > **TARGETS**, select **Info** or **Build Settings**:

    :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-build-settings-bundleid.png" alt-text="Screenshot that shows selecting project, targets, info or build settings to add the bundle ID in Xcode on a macOS device.":::

- **URL Types**: In **PROJECT** > **TARGETS**, select **Info**. In **URL Types**, confirm the `$(PRODUCT_BUNDLE_IDENTIFIER)` variable is there.

  If the variable isn't there, then add it. If you need to add it, then first create the **Queried URL Schemes** for the Intune App SDK for iOS. Then, add the variable.

  The following example shows the `$(PRODUCT_BUNDLE_IDENTIFIER)` variable in **URL Types**:

  :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-url-types-xcode.png" alt-text="Screenshot that shows selecting project, targets, info, URL types in Xcode on a macOS device.":::

- **IntuneMAMSettings**: Follow the guidance in the Intune App SDK for iOS developer guide at [Configure MSAL settings for Intune App SDK](app-sdk-ios.md#configure-msal-settings-for-the-intune-app-sdk).

  In **PROJECT** > **TARGETS** > **Info** > **IntuneMAMSetting**, make sure the following settings are configured with the appropriate Azure AD app registration values:

  - `ADALAuthority`: Enter the Azure AD tenant ID, such as `https://login.microsoftonline.com/USE_YOUR_ Directory (tenant) ID`.
  - `ADALClientId`: Enter the application client ID.
  - `ADALRedirectUri`: Enter `msauth.$(PRODUCT_BUNDLE_IDENTIFIER):/auth`.

  The following example shows these values configured:

  :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-intunemamsettings-xcode.png" alt-text="Screenshot that shows selecting project, targets, info, IntuneMAMSetting in Xcode on a macOS device.":::

- **Queried URL Schemes**: Follow the guidance in the [Intune App SDK for iOS developer guide – Step 5](app-sdk-ios.md#build-the-sdk-into-your-mobile-app).

  The following example shows the info.plist using **Raw Keys & Values**:

  :::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-info-raw-keys-values-xcode.png" alt-text="Screenshot that shows selecting project, targets, info, and the info.plist file using raw keys and values in Xcode on a macOS device.":::

### Step 3 - Turn off Bitcode

In **PROJECT** > **TARGETS** > **Build settings** > **Build options**, set **Enable Bitcode** to **No**:

:::image type="content" source="./media/tunnel-mam-ios-sdk/project-targets-build-settings-enable-bitcode-xcode.png" alt-text="Screenshot that shows selecting project, targets, build settings, build options, and disabling bitcode in Xcode on a macOS device.":::

START HERE

### Step 4 - Add keychain sharing

The Keychain Sharing item may or not be present in the app project.  If not present, add the capability by clicking the “+” button in the “Signing & Capabilities” page.   

Add (+) `com.microsoft.workplacejoin` to the list of Keychain Groups. 

See example below:

INSERT IMAGE

### Step 5 - SDK Integration

Depending on the LOB app and implementation/intended purpose, the use of the MicrosoftTunnelApi may vary. There are some core functionalities to keep in mind as you are integrating. All interactions with the Microsoft Tunnel for MAM iOS SDK are handled through a MicrosoftTunnelApi singleton object. This object interacts with the app using a delegate implementing a MicrosoftTunnelDelegate interface.  

- In Xcode, in whatever code file you intended to interact with the MicrosoftTunnelApi, import “MicrosoftTunnelApi” and MicrosoftTunnel”

- It is highly advised to create a specific delegate class for the MicrosoftTunnel Api, however this is ultimately optional.

- Initialize the MicrosoftTunnelApi using “[MicrosoftTunnelApi init]” or “MicrosoftTunnelApi initWithDelegate:config:”

  If your LOB App already integrates the Intune MAM SDK provide your delegate here

- After initialization, call the MicrosoftTunnelApi to connect

- At this point the SDK should be initialized and connected. It's possible to check the status of the SDK by calling MicrosoftTunnelApi getStatus or getStatusString.

- Interception occurs when the SDK is connected and halts when the SDK is disconnected.

#### Update Xcode project “AppDelegate”

The AppDelegate file is a standard file in every Xcode project and it contains methods that are called at various points during the app's lifecycle. 

The didFinishLaunchingWithOptions method is one such method that is called when the app finishes launching. This is where developers can add code to initialize the Intune framework and set up the Microsoft Tunnel delegate. 

It is also important to note that multiple delegates can be added in the AppDelegate file, but it does not matter the order of them. However, the order of the delegates in the code might affect the functionality of the app. 

The following 2 updates need to be made:

1. Add the MS Tunnel Delegate initialization line to the “didFinishLaunchingWithOptions” method.  The line of code to launch the delegate should be added within this method, and it should be inserted before the “return true” statement to ensure that the delegate is launched before the app finishes launching:  

    - `MicrosoftTunnelDelegate.sharedDelegate.launch()`

2. Add the following method to handle the MSAL URL auth response for Tunnel at the end of the file: 

    ```swift
    Func application(_ application: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionKey: Any] = [:]) -> Bool { 

    Return MicrosoftTunnelDelegate.sharedDelegate.api?handleMSALResponse(url, sourceApplication: options[.sourceApplication] as? String) ?? 

    false
    ```

    See example below:

    INSERT IMAGE

#### Create a Microsoft Tunnel Delegate 

A Tunnel Delegate file must be created in order to integrate the Intune framework into an Xcode project.  Developers will need to use the Tunnel delegate methods in their code to specify how the app should behave when certain events occur, such as when a connection is initialized, connected, disconnected, etc.

See example below:

INSERT IMAGE

> [!NOTE]
> The name of the Microsoft Tunnel delegate is up to the developer performing the integration.  The name used in the example above is “MicrosoftTunnelDelegate”.

Use the following code template snippet to get you started: 

?? NEED CODE

## Sample apps

To get you started, we’ve provided a number of sample apps covering various scenarios.  These apps can be found under the Microsoft Tunnel for MAM iOS SDK repository on GitHub  --- https://aka.ms/MAMTunneliOSGithubLink

## API Functionality

- **Initialize** – Checks and sets the VPN configurations, sets up logging, and sets up the MicrosoftTunnelAPI instance.

- **Connect** – Grabs the MicrosoftTunnelAPI instance and enables network traffic interception. Throws an error if the API is uninitialized.

- **Disconnect** - Grabs the MicrosoftTunnelAPI instance and disables network traffic interception. Throws an error if the API is uninitialized.

- **onTokenRequired** – Optional. If your app already integrates with either IntuneMAM or MSAL, you will need to implement this method. Uses the IntuneMAMSettings and MSAL to grab a valid authentication token to connect.

- **Logging** – There are a few different logging classes, denoted by k, for example kLoggingClassConnect, which produce logging output in the Xcode console. These logging config keys can be added to the delegate config. Examples of this are in the sample apps.

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

> [!IMPORTANT]
> Do not use debug keys in deployed apps as that can log user identifiable information and security data.

### Logging on iOS LOB apps

Integrating the SDK does not automatically enable logging. The developer will need to add the appropriate code to implement the logging delegate framework and make the appropriate logging calls. The specific implementation will vary depending on the SDK and the developer's requirements. 

However, it's important to note that the developer should ensure that they do not include any customer identifiable or end-user identifiable information in their logging to comply with privacy regulations. The respective company/organization privacy team should be consulted for guidance on the appropriate data that can be logged and the appropriate ways of handling sensitive data. It is also important to consult the SDK documentation for any specific guidance regarding logging and data privacy. 

### MAM-Tunnel logging log delegate method used​

INSERT IMAGES

## Known issues

Proxy servers must have either a public DNS record or they must be configured using the IP address

When evaluating Trusted certificates for protected web servers, SANs (Subject Alternative Names) are not honored. Only common names.

If the identity is not managed by the app itself and is delegated to the Tunnel SDK, then to change the logged in account, the app will need to manually call into the MAM SDK to deregister the account ([Microsoft Intune App SDK for iOS developer guide](app-sdk-ios.md#deregister-user-accounts)).

Simply uninstalling the app and reinstalling will not be sufficient since the identity is managed in a separate keychain

Trusted root certificate validation only works for endpoints and not for validation to the VPN server itself.

## Next steps

