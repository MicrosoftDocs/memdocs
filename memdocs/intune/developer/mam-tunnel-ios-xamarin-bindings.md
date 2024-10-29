---
title: Microsoft Tunnel for MAM iOS SDK Xamarin Bindings 
description: Use Xamarin Bindings to allow Microsoft Tunnel capabilities for iOS applications. 
author: oluchic 
ms.author: brenduns
manager: dougeby
ms.date: 09/12/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid:

#ROBOTS:
#audience:

ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
- iOS/iPadOS
---

# Microsoft Tunnel for MAM iOS Xamarin Bindings

> [!IMPORTANT]
>
> Xamarin support ended on May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. The information in this article is maintained as a reference for previously created Xamarin Bindings.
>
> Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.
>
> For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android) and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).
>
> 

> [!NOTE]
>
> Consider reading the [Get Started with Microsoft Tunnel iOS SDK](../developer/tunnel-mam-ios-sdk.md) article, which explains how to prepare for integration on each supported platform.

## Overview

The Microsoft Tunnel iOS SDK Xamarin Bindings facilitate the integration of Microsoft Tunnel for MAM functionality for MAM iOS applications developed with Xamarin. These bindings empower developers by providing a straightforward means to embed tunnel connectivity features directly into their Xamarin-based applications, ensuring seamless and secure connectivity for end users.

## How it works

The Intune MAM Xamarin.iOS bindings are the native MAM Tunnel SDK with a  wrapper/bridge to its public APIs. Since Xamarin/.NET apps typically use ADAL or MSAL for .NET as their Microsoft Entra auth library, and the native Intune SDK doesn't know how to call into those libraries for its own enrollment/auth scenarios, the Xamarin bindings depend on the MAM SDK bindings that also contain Objective-C MSAL library, which can share a common token cache with ADAL/MSAL for .NET.

These bindings are also available as a NuGet package which developers can pull into their Xamarin.iOS project directly via the Visual Studio UI.

View the [Xamarin iOS bindings](/xamarin/cross-platform/macios/binding/objective-c-libraries?tabs=macos) for the [Intune MAM Tunnel Objective-C library for iOS](https://github.com/msintuneappsdk/ms-intune-tunnel-sdk-ios)

## What’s supported?

__Developer machines__:

- Windows (Visual Studio version 15.7+)
- macOS

__Mobile app platforms__:

- iOS 15.0 and Higher

__Intune Mobile Application Management scenarios__:

- Intune [MAM](../apps/android-deployment-scenarios-app-protection-work-profiles.md)

## Prerequisites

Review the [license terms](https://github.com/msintuneappsdk/ms-intune-tunnel-sdk-xamarin/blob/main/Microsoft%20License%20Terms%20Tunnel%20for%20Mobile%20Application%20Management%20iOS%20SDK%20Xamarin%20Bindings.pdf). Print and retain a copy of the license terms for your records. By downloading and using the Microsoft Tunnel iOS SDK Xamarin Bindings, you agree to such license terms. If you don't accept them, do not use the software.

The Tunnel for MAM SDK relies on the Intune MAM SDK to enforce application protection policies (APP) and Application Configuration Policies (ACP).

The Tunnel for MAM SDK relies on [Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-overview) for its [authentication](/azure/active-directory/develop/authentication-vs-authorization) and conditional launch scenarios, which require apps to be configured with [Microsoft Entra ID](/azure/active-directory/fundamentals/active-directory-whatis).

If your application is already configured to use MSAL, and has its own custom client ID used to authenticate with Microsoft Entra ID follow the subsequent steps to establish tunnel connectivity for your Xamarin application. For detailed instructions and additional information, refer to the developer guide.

## Security considerations

To prevent potential spoofing, information disclosure, and elevation of privilege attacks:

- Ensure that Xamarin app development is performed on a secure work station.
- Ensure the bindings are from a valid Microsoft source:

  - [MS Microsoft Tunnel iOS SDK NuGet Profile](https://www.nuget.org/packages/Microsoft.Intune.Tunnel.MAM.Xamarin.iOS)
  - [Microsoft Tunnel iOS SDK Xamarin GitHub Repository](https://github.com/msintuneappsdk/ms-intune-tunnel-sdk-xamarin)

- Configure your NuGet config for your project to trust signed, unmodified NuGet packages. For more information, see [installing signed packages](/nuget/consume-packages/installing-signed-packages).
- Secure the output directory that contains the Xamarin app. Consider using a user-level directory for the output.

## Sample Applications

Sample applications highlighting MAM functionality in Xamarin iOS apps are available on [GitHub](https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps).

## Enable Tunnel for MAM Xamarin Bindings


### Integrate your Xamarin App using Sample Application

See the [Sample application](https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps)
 
1. Clone the repository.

2. Open your app `.sln` file in Visual Studio.

3. Use the NuGet Package Manager to update the `Microsoft.Intune.Tunnel.MAM.Xamarin.iOS` package to the latest version.

4. Update `Directory.Build.props` and change the values of `<ApplicationID>`, `<ClientID>` and `<TenantID>` to match the values of your _Bundle ID_, your _AAD application Client ID_ and your _AAD Tenant ID_ respectively.

5. Optionally, update `<ApplicationTitle>` to change the deployed name of the application.

   - Alternatively, you can create a file next to the `Directory.Build.props` file named `Developer.props`.
   - Include the contents:
     ```
     <Project>
        <PropertyGroup>
          <ApplicationID>[your Bundle ID]</ApplicationID>
          <ApplicationTitle>xPlat-Tunnel</ApplicationTitle>
          <ClientID>[your Microsoft Entra Application Client ID]</ClientID>
          <TenantID>[your Microsoft Entra Tenant ID]</TenantID>
        </PropertyGroup>
     </Project>
      ```
   - This file allows you to update these properties without altering the csproj file.

6. Select your target device in Visual Studio and run.

#### Details

The target `GeneratePartialAppManifests` defined in `Directory.Build.props` converts the MSBuild properties defined in the previous section into the appropriate `Info.plist` properties. It also sets the default values for the `IntuneMAMSettings`.

The target `AddPartialAppManifests` merges the newly generated plist file and the main Info.plist.

#### Integration

- Beyond the configuring of `IntuneMAMSettings` as described in the [Details](#details) section of this document, you also need to configure the `Entitlements.plist` as seen in [step 2 of *Enabling Intune app protection policies in your iOS mobile app*](../developer/app-sdk-xamarin.md#enabling-intune-app-protection-policies-in-your-ios-mobile-app) in the _Enabling Intune app protection policies in your iOS mobile app_ section of the _Microsoft Intune App SDK Xamarin Bindings_ article.

- The bulk of the integration can be found in `MicrosoftTunnelDelegate.cs`, which is a class that inherits from `Microsoft.Intune.Tunnel.MAM.iOS.TunnelDelegate` and implements abstract members.

- To facilitate logging and debugging, the `MicrosoftTunnelDelegate.cs` file declares a `LogDelegate` that inherits from `Microsoft.Intune.Tunnel.MAM.iOS.MicrosoftTunnelLogDelegate`.

- The `MicrosoftTunnelDelegate` also passes itself into the `Microsoft.Intune.Tunnel.MAM.iOS.MicrosoftTunnel.SharedInstance.MicrosoftTunnelInitialize` method to start the SDK initialization.

- The final integration point is found in `AppDelegate.cs`. It calls the `MicrosoftTunnelDelegate.Launch` method from within the `FinishedLaunching` method.

### Integrate your Xamarin App using a Custom Application

1. Install the Package
  - Install the `Microsoft.Intune.Tunnel.MAM.Xamarin.iOS` package into your Xamarin application.
    ```
    dotnet add package Microsoft.Intune.Tunnel.MAM.Xamarin.iOS --version 1.0.9
    ```
    [NuGet Package](https://www.nuget.org/packages/Microsoft.Intune.Tunnel.MAM.Xamarin.iOS/#readme-body-tab)

2. Step 2: Configure IntuneMAMSettings
   - Configure the `IntuneMAMSettings` following the instructions in the [Details](#details) section of this document.

3. Configure the Entitlements.plist
   - Update the `Entitlements.plist` as outlined in [step 2 of *Enabling Intune app protection policies in your iOS mobile app*](../developer/app-sdk-xamarin.md#enabling-intune-app-protection-policies-in-your-ios-mobile-app) in the _Microsoft Intune App SDK Xamarin Bindings_ article.

4. Integration in MicrosoftTunnelDelegate.cs
   - The main integration is in the `MicrosoftTunnelDelegate.cs` file, a class inheriting from `Microsoft.Intune.Tunnel.MAM.iOS.TunnelDelegate` implementing abstract members.

5. Enable Logging and Debugging
   - For logging and debugging purposes, the `MicrosoftTunnelDelegate.cs` file declares a `LogDelegate` that inherits from `Microsoft.Intune.Tunnel.MAM.iOS.MicrosoftTunnelLogDelegate`.

6. Initialize the SDK
   - The `MicrosoftTunnelDelegate` passes itself into the `Microsoft.Intune.Tunnel.MAM.iOS.MicrosoftTunnel.SharedInstance.MicrosoftTunnelInitialize` method to begin the SDK initialization.

7. Final Integration Point in AppDelegate.cs
  - The last integration point is in the `AppDelegate.cs` file. It calls the `MicrosoftTunnelDelegate.Launch` method from within the `FinishedLaunching` method.

#### Additional Notes
- Ensure to refer to the documentation and the [Details](#details) section carefully for any additional configurations or settings related to `IntuneMAMSettings` and other functionalities.

### Releases & Dependencies
These bindings are typically kept in sync with the third-party native [MAM Tunnel SDK releases](https://github.com/msintuneappsdk/ms-intune-tunnel-sdk-ios).

These bindings are typically updated to the [latest version of MSAL for Objective-C](https://github.com/AzureAD/microsoft-authentication-library-for-objc/releases), and to the [latest version of the Intune MAM SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios) with each release.

**Provisioning problems**"

Follow the [steps outlined here](/xamarin/ios/get-started/installation/device-provisioning/free-provisioning?tabs=macos) if you have problems provisioning the application.

> [!NOTE]
>
> There is no remapper for iOS/iPadOS. Integrating into a Xamarin.Forms app should be the same as for a regular Xamarin.iOS project.

## Next steps

[Microsoft Tunnel for MAM for iOS/iPadOS - Intune admin guide](../developer/tunnel-mam-ios-sdk.md)
