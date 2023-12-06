---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide 
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app.
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

# Intune App SDK for iOS - Plan the integration

> [!NOTE]
> Consider reading the [Get Started with Intune App SDK Guide](app-sdk-get-started.md) article, which explains how to prepare for integration on each supported platform.
>
> If your app builds with [.NET Multi-platform App UI (.NET MAUI)](https://dotnet.microsoft.com/en-us/apps/maui), see [Intune App SDK for .NET MAUI - iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).
>
> To download the SDK, see [Download the SDK files](../developer/app-sdk-get-started.md#download-the-sdk-files).
>
> If you have issues with integrating the Intune App SDK into your apps, submit a [request for assistance](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/issues) on GitHub.

The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. A MAM-enabled application is one that is integrated with the Intune App SDK. IT administrators can deploy app protection policies to your mobile app when Intune actively manages the app.

> [!IMPORTANT]
> Intune regularly releases updates to the [Intune App SDK](https://github.com/msintuneappsdk). We recommend subscribing to the [Intune App SDK](https://github.com/msintuneappsdk) repositories for updates so that you can incorporate the update into your software development release cycle and ensure your apps support the latest App Protection Policy settings.
> 
> Plan to take mandatory Intune App SDK updates prior to every major OS release to ensure your app continues to run smoothly as OS updates can cause breaking changes. If you do not update to the latest version prior to a major OS release, you might run the risk of encountering a breaking change and/or being unable to apply app protection policies to your app.

## Prerequisites

- You'll need a macOS computer which has Xcode 14.0 or later installed.

- Your app must be targeted for iOS 14.0 or above.

- Review the [Intune App SDK for iOS License Terms](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20for%20iOS.pdf). Print and retain a copy of the license terms for your records. By downloading and using the Intune App SDK for iOS, you agree to such license terms.  If you don't accept them, don't use the software.

- Download the files for the Intune App SDK for iOS on [GitHub](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios).

## What's in the SDK Repository

* **IntuneMAMSwift.xcframework**: The Intune App SDK framework. It's recommended that you link this framework to your app/extensions to enable Intune client application management. However, some developers might prefer the performance benefits of the static library. See the following:

* **libIntuneMAMSwift.xcframework**: The Intune App SDK static library. Developers might choose to link the static library instead of the framework. Because static libraries are embedded directly into the app/extension binary at build time, there are some launch-time performance benefits to using the static library. However, integrating it into your app is a more complicated process. If your app includes any extensions, linking the static library to the app and extensions will result in a larger app bundle size, as the static library will be embedded into each app/extension binary. When using the framework, apps and extensions can share the same Intune SDK binary, resulting in a smaller app size.

* **IntuneMAMSwiftStub.xcframework**: The Intune App SDK Swift Stub framework. This is a required dependency of both IntuneMAMSwift.xcframework and libIntuneMAMSwift.xcframework which apps/extensions must link.

* **IntuneMAMResources.bundle**: A resource bundle that contains resources that the SDK relies on. The resources bundle is required only for apps which integrate the static library (libIntuneMAMSwift.xcframework).

* **IntuneMAMConfigurator**: A tool used to configure the app or extension's Info.plist with the minimum required changes for Intune management. Depending on the functionality of your app or extension, you might need to make additional manual changes to the Info.plist.


## How the Intune App SDK works

The objective of the Intune App SDK for iOS is to add management capabilities to iOS applications with minimal code changes. The fewer the code changes the less time to market, but without affecting the consistency and stability of your mobile application.

### Process flow

The following diagram provides the Intune App SDK for iOS process flow:

:::image type="content" source="media/app-sdk-ios/intune-app-sdk-ios-process-flow.svg" alt-text="High-level architectural diagram for Microsoft Intune."  lightbox="media/app-sdk-ios/intune-app-sdk-ios-process-flow.png" :::