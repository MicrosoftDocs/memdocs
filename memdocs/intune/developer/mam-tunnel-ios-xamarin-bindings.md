---
title: Microsoft Tunnel for MAM iOS SDK Xamarin Bindings 
description: Use Xamarin Bindings to allow Microsoft Tunnel capabilities for iOS applications. 
author: oluchic 
ms.author: brenduns
manager: dougeby
ms.date: 09/26/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
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

> [!NOTE]
>
> The current Xamarin bindings for IOS platform only support apps targeting iOS 15.0 and higher.

> [!NOTE]
>
> Consider reading the [Get Started with Microsoft Tunnel iOS SDK](/mem/intune/developer/tunnel-mam-ios-sdk) article, which explains how to prepare for integration on each supported platform.

## Overview

The Microsoft Tunnel iOS SDK Xamarin Bindings facilitate the integration of Microsoft Tunnel for MAM functionality for MAM iOS applications developed with Xamarin. These bindings empower developers by providing a straightforward means to embed tunnel connectivity features directly into their Xamarin-based applications, ensuring seamless and secure connectivity for end users.

## What’s supported?

__Developer machines__:

- Windows (Visual Studio version 15.7+)
- macOS

__Mobile app platforms__:

- iOS 15.0 and Higher

__Intune Mobile Application Management scenarios__:

- Intune [MAM](/mem/intune/apps/android-deployment-scenarios-app-protection-work-profiles)

## Prerequisites

Review the [license terms](https://github.com/msintuneappsdk/ms-intune-tunnel-sdk-xamarin/blob/main/Microsoft%20License%20Terms%20Tunnel%20for%20Mobile%20Application%20Management%20iOS%20SDK%20Xamarin%20Bindings.pdf). Print and retain a copy of the license terms for your records. By downloading and using the Microsoft Tunnel iOS SDK Xamarin Bindings, you agree to such license terms. If you do not accept them, do not use the software.

The Tunnel for MAM SDK relies on the Intune MAM SDK to enforce application protection policies (APP) and Application Configuration Policies (ACP).

The Tunnel for MAM SDK relies on [Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/v2-overview) for its [authentication](/azure/active-directory/develop/authentication-vs-authorization) and conditional launch scenarios, which require apps to be configured with [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis).

If your application is already configured to use MSAL, and has its own custom client ID used to authenticate with Azure Active Directory follow the subsequent steps to establish tunnel connectivity for your Xamarin application. For detailed instructions and additional information, please refer to the developer guide.

## Security considerations

To prevent potential spoofing, information disclosure, and elevation of privilege attacks:

- Ensure that Xamarin app development is performed on a secure work station.
- Ensure the bindings are from a valid Microsoft source:
  - [MS Microsoft Tunnel iOS SDK NuGet Profile](https://www.nuget.org/profiles/msintuneappsdk)
  - [Microsoft Tunnel iOS SDK Xamarin GitHub Repository](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)
- Configure your NuGet config for your project to trust signed, unmodified NuGet packages. For more information, see [installing signed packages](/nuget/consume-packages/installing-signed-packages).
- Secure the output directory that contains the Xamarin app. Consider using a user-level directory for the output.

## Sample Applications

Sample applications highlighting MAM functionality in Xamarin iOS apps are available on [GitHub](https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps). (new link)

## Enabling Tunnel for MAM Xamarin Bindings

Integrate Xamarin App using Sample Application: 

```java
Building the Sample application (https://github.com/msintuneappsdk/ms-intune-tunnel-iOS-sampleapps)

Clone the repository

Open your app sln file in Visual Studio

Use the Nuget Package Manager to update the Microsoft.Intune.Tunnel.MAM.Xamarin.iOS package to the latest version

Update Directory.Build.props and change the values of <ApplicationId>, <ClientId> and <TenantId> to match the values of your Bundle Id, your AAD application Client Id and your AAD Tenant Id respectively

Optionally update <ApplicationTitle> to change the deployed name of the application

Alternatively, you can create a file adjacent to the Directory.Build.props file named Developer.props

Include the contents
<Project>
    <PropertyGroup>
        <ApplicationId>[your Bundle Id]</ApplicationId>
        <ApplicationTitle>xPlat-Tunnel</ApplicationTitle>
        <ClientId>[your AAD Application Client Id]</ClientId>
        <TenantId>[your AAD Tenant Id]</TenantId>
    </PropertyGroup>
</Project>

This will allow you to update these properties without altering the csproj file

Select your target device in Visual Studio and run

Details

The target GeneratePartialAppManifests defined in Directory.Build.props will convert the MSBuild properties defined above into the appropriate Info.plist properties. It also sets the default values for the IntuneMAMSettings 

The target AddPartialAppManifests will merge the newly generated plist file and the main Info.plist

Integration

Beyond the configuring of IntuneMAMSettings as described in the Details section of this document. You also need to configure the Entitlements.plist as seen in step 2 of this document . It has already been done in this sample application.

The bulk of the integration can be found in MicrosoftTunnelDelegate.cs. It is a class that inherits from Microsoft.Intune.Tunnel.MAM.iOS.TunnelDelegate and implements abstract members.

To facilitate logging and debugging, the MicrosoftTunnelDelegate.cs file declares a LogDelegate that inherits from Microsoft.Intune.Tunnel.MAM.iOS.MicrosoftTunnelLogDelegate

The MicrosoftTunnelDelegate also passes itself into the Microsoft.Intune.Tunnel.MAM.iOS.MicrosoftTunnel.SharedInstance.MicrosoftTunnelInitialize method to start the SDK initialization.

The final integration point is found in AppDelegate.cs. It calls the MicrosoftTunnelDelegate.Launch method from within the FinishedLaunching method.

Provisioning problems
Follow the steps outlined here if you have problems provisioning the application (https://learn.microsoft.com/xamarin/ios/get-started/installation/device-provisioning/free-provisioning?tabs=macos).

```

> [!NOTE]
>
> There is no remapper for iOS/iPadOS. Integrating into a Xamarin.Forms app should be the same as for a regular Xamarin.iOS project.

## Next steps

[Microsoft Tunnel for MAM for iOS/iPadOS - Intune admin guide](../developer/tunnel-mam-ios-sdk.md)
