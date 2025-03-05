---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - Appendix
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. Appendix
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/14/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
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
- tier2
- M365-identity-device-management
- iOS/iPadOS
---

# Intune App SDK for iOS - Appendix

## Stage Goals

The guide contains some iOS best practices to integrate Intune SDK, common FAQs and other helpful content.

## iOS best practices

Here are recommended best practices for developing for iOS:

* The iOS file system is case-sensitive. Ensure that the case is correct for file names like `IntuneMAMResources.bundle`.
* Registering custom URL schemes allows specific URLs to redirect into your app. iOS and iPadOS allow multiple apps to register the same custom URL scheme and the OS determines which application is invoked. Refer to the Apple documentation [Defining a custom URL scheme for your app](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app) for recommendations to help avoid custom URL scheme collisions and security guidelines for handling malformed URLs.

## FAQs

### Are all of the APIs addressable through native Swift or the Objective-C and Swift interoperability?

The Intune App SDK APIs are in Objective-C only and don't support **native** Swift. Swift interoperability with Objective-C is required.

### Do all users of my application need to be registered with the APP-WE service?

No. In fact, only work or school accounts should be registered with the Intune App SDK. Apps are responsible for determining if an account is used in a work or school context.

### What about users that have already signed in to the application? Do they need to be enrolled?

The application is responsible for enrolling users after they have been successfully authenticated. The application is also responsible for enrolling any existing accounts that might have been present before the application had MDM-less MAM functionality.

To do this, the application should make use of the `registeredAccounts:` method. This method returns an NSDictionary that has all of the accounts registered into the Intune MAM service. If any existing accounts in the application aren't in the list, the application should register and enroll those accounts via `registerAndEnrollAccount:`.

### How often does the SDK retry enrollments?

The SDK automatically retries all previously failed enrollments on a 24-hour interval. The SDK does this to ensure that if a user's organization enabled MAM after the user signed in to the application, the user will successfully enroll and receive policies.

The SDK stops retrying when it detects that a user has successfully enrolled the application. This is because only one user can enroll an application at a particular time. If the user is unenrolled, the retries begin again on the same 24-hour interval.

### Why does the user need to be deregistered?

The SDK takes these actions in the background periodically:

* If the application isn't yet enrolled, it tries to enroll all registered accounts every 24 hours.
* If the application is enrolled, the SDK checks for MAM policy updates every 8 hours.

Deregistering a user notifies the SDK that the user will no longer use the application, and the SDK can stop any of the periodic events for that user account. It also triggers an app unenroll and selective wipe if necessary.

### Should I set the doWipe flag to true in the deregister method?

This method should be called before the user is signed out of the application.  If the user's data is deleted from the application as part of the sign out, `doWipe` can be set to false. But if the application doesn't remove the user's data, `doWipe` should be set to true so that the SDK can delete the data.

### Are there any other ways that an application can be unenrolled?

Yes, the IT admin can send a selective wipe command to the application. This will deregister and unenroll the user, and it wipes the user's data. The SDK automatically handles this scenario and sends a notification via the unenroll delegate method.

### Is there a sample app that demonstrates how to integrate the SDK?

Yes! See the [Chatr sample app](https://github.com/msintuneappsdk/Chatr-Sample-Intune-iOS-App).

### How can I troubleshoot my app?

The Intune SDK for iOS 9.0.3+ supports the ability to add a diagnostics console within the mobile app for testing policies and logging errors. `IntuneMAMDiagnosticConsole.h` defines the `IntuneMAMDiagnosticConsole` class interface, which developers can use to display the Intune diagnostic console. This allows end users or developers during test to collect and share Intune logs to help diagnose any issue they may have. This API is optional for integrators.
