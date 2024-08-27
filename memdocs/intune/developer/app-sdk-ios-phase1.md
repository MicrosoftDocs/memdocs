---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - Plan the integration
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. Plan the integration.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/01/2023
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

# Intune App SDK for iOS - Plan the integration

The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. A MAM-enabled application is one that is integrated with the Intune App SDK. IT administrators can deploy app protection policies to your mobile app when Intune actively manages the app.

> [!IMPORTANT]
> Intune regularly releases updates to the [Intune App SDK](https://github.com/microsoftconnect). We recommend subscribing to the [Intune App SDK](https://github.com/microsoftconnect) repositories for updates so that you can incorporate the update into your software development release cycle and ensure your apps support the latest App Protection Policy settings.
> 
> Plan to take mandatory Intune App SDK updates prior to every major OS release to ensure your app continues to run smoothly as OS updates can cause breaking changes. If you do not update to the latest version prior to a major OS release, you might run the risk of encountering a breaking change and/or being unable to apply app protection policies to your app.

## Stage 1: Plan the Integration

This guide is for iOS developers who are looking to add support for Microsoft Intune's App Protection Policies inside their existing iOS app.

## Stage Goals

- Learn what App Protection Policy settings are available for iOS and how these policies will work inside your application.
- Understand the key decision points during the SDK integration process and plan your app's integration.
- Understand the requirements for applications integrating the SDK.
- Create a test Intune tenant and configure an iOS App Protection Policy.

## Understanding MAM

Before you start integrating the Intune App SDK into your iOS application, take a moment to familiarize yourself with Microsoft Intune's Mobile Application Management solution:

- [What is Microsoft Intune app management] provides a high level overview of MAM capabilities on different platforms
  and where to find these features in the Microsoft Intune admin center.  
- [Intune App SDK overview] goes one layer deeper, describing the current features of the SDK.
- [Get Started with Intune App SDK Guide](app-sdk-get-started.md) explains how to prepare for integration on each supported platform.
- [iOS app protection policy settings] describe each iOS setting in detail.
  Your app will support these settings by integrating the SDK.
  During the SDK integration process, you'll also configure these settings in your own test tenant for validation.
- (Optional) [Plan for mobile application management in Microsoft Intune - Training | Microsoft Learn] explains how to plan for mobile application management using Microsoft Intune, with a focus on adding apps to Intune, using app protection policies and app configuration policies, and troubleshooting app protection policy deployment.

## Key Decisions for SDK integration

### Do I need to register my application with the Microsoft identity platform?
 
Yes, all apps integrating with the Intune SDK are required to register with the Microsoft identity platform. Please follow the steps in [Quickstart: Register an app in the Microsoft identity platform - Microsoft identity platform].

### Do I have access to my application's source code?

If you don't have access to your application's source code and only have access to the compiled application in either .app or .ipa format, you won't be able to integrate the SDK into your application.
However, your application may still be compatible with Intune app protection policies.
See [App Wrapping Tool for iOS] for more details.

### Should my application integrate the Microsoft Authentication Library (MSAL)?

Yes, you are required to integrate with MSAL before integrating the Intune SDK. Before integrating with MSAL, all apps are required to register with the Microsoft identity platform. Please follow the steps in [Quickstart: Register an app in the Microsoft identity platform - Microsoft identity platform].

See [Stage 2: MSAL prerequisite and setup] for instructions on integrating MSAL and additional details on identity scenarios inside your application.

### Is my application single-identity or multi-identity?

Without Intune App Protection Policy support, how does your application handle user authentication and accounts?

- Does your application currently only allow a single account to be logged in?
Does your application explicitly force the logged-in account to log out—and delete that previous account's data—before allowing another account to log in?
If so, your application is **single-identity**.

- Does your application currently allow a second account to log in, even if a different account is already logged in?
Does your application display multiple accounts' data on a shared screen?
Does your application store multiple accounts' data?
Does your application let users switch between different logged in accounts?
If so, your application is **multi-identity** and you'll need to follow [Stage 5: Enable multi-identity]. **This section is required for your app.**

Even if your application is multi-identity, follow this integration guide in order.
Initially integrating and testing as single-identity will help ensure proper integration and prevent bugs where corporate data ends up unprotected.

### What if my app builds with [.NET Multi-platform App UI (.NET MAUI)](https://dotnet.microsoft.com/en-us/apps/maui)?

If your app builds with [.NET Multi-platform App UI (.NET MAUI)](https://dotnet.microsoft.com/en-us/apps/maui), see [Intune App SDK for .NET MAUI - iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

### Does my application have or need App Configuration settings?

Intune supports application configurations that apply to SDK-integrated applications, regardless of device management mode. Admins can configure these [application configuration policies for managed apps] in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

The Intune App SDK supports both types of application configuration and provides a single API for accessing configurations from both channels. If your application has or will support either of these types of application configuration, you'll need to follow [Stage 4: Enable targeted configuration (APP/MAM app config) for your iOS applications].

For more information about how to create a MAM targeted app configuration policy in iOS, see the section on MAM targeted app config in [How to use Microsoft Intune app configuration policies for iOS/iPadOS](../apps/app-configuration-policies-use-ios.md).

### Does my application need to define granular protection for data ingress and egress?

If your app lets users save data to or open data from cloud services or to device locations, it must take changes to support enhanced data transfer policy.
See [Manage data transfer between iOS apps in Microsoft Intune].

### Does my application have resources that should be protected by Conditional Access?

[Conditional Access (CA)] is a [Microsoft Entra ID]
feature that can be used to control access to Microsoft Entra resources.
Intune administrators can define CA rules that allow resource access only from devices or apps that are managed by Intune.

Intune supports two types of CA: **device-based CA** and **app-based CA**, also known as [App Protection CA].
Device-based CA blocks access to protected resources until the entire device is managed by Intune.
App-based CA blocks access to protected resources until the specific app is managed by Intune App Protection Policies.

If your app acquires any Microsoft Entra access tokens and accesses resources that can be CA-protected, you'll need to follow [Stage 4: App Protection CA support].

## Creating a test iOS app protection policy

### Demo tenant setup

If you don't already have a tenant with your company, you can create a demo tenant with or without pre-generated data. You must register as a [Microsoft partner] to access Microsoft CDX.
To create a new account:

1. Navigate to the [Microsoft CDX tenant creation site] and create a Microsoft 365 Enterprise tenant.
2. [Set up Intune] to enable mobile device management (MDM).
3. [Create users].
4. [Create groups].
5. [Assign licenses] as appropriate for your testing.

### App protection policy configuration

[Create and assign app protection policies] in the Microsoft Intune admin center. In addition to creating app protection policies, you can create and assign an [app configuration policy] in Intune.

Before you test app protection policy settings within your own application, it's helpful to familiarize yourself with how these settings behave inside other SDK-integrated applications.

> [!TIP]
> If your app isn't listed in the Microsoft Intune admin center, you can target it with a policy by selecting the **more apps** option and providing the package name in the text box.  
> You must target your app with app protection policy and deploy the policy to a user to successfully test your integration.  
> Even if policy is targeted and deployed, your app will not properly enforce policies until it has successfully integrated the SDK.

## Exit Criteria

- Have you familiarized yourself with how different app protection policy settings will behave inside your iOS application?
- Have you reviewed your app and planned your app's integration around MSAL, Conditional Access, Multi-Identity, App Configuration, and all additional SDK features?
- Have you created an iOS app protection policy within your test tenant?

## FAQ

### Where do I download the SDK?

To download the SDK, see [Download the SDK files](../developer/app-sdk-get-started.md#download-the-sdk-files).

### Where do I report issues with integrating the Intune App SDK into my apps?

Please submit a [request for assistance](https://github.com/microsoftconnect/ms-intune-app-sdk-ios/issues) on GitHub.

## Next Steps

After you've completed all the [Exit Criteria] above, continue to [Stage 2: MSAL prerequisite and setup].

<!-- Stage 1 links -->
<!-- internal links -->
[Stage 1: Planning the Integration]:#stage-1-plan-the-integration
[Exit Criteria]:#exit-criteria

<!-- Other SDK Guide Markdown documentation -->
[Stage 2: MSAL prerequisite and setup]:app-sdk-ios-phase2.md
[Stage 5: Enable multi-identity]:app-sdk-ios-phase5.md
[Stage 4: Enable targeted configuration (APP/MAM app config) for your iOS applications]:app-sdk-ios-phase4.md
[Manage data transfer between iOS apps in Microsoft Intune]:/mem/intune/apps/data-transfer-between-apps-manage-ios#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm
[Stage 6: App Protection CA support]:app-sdk-ios-phase6.md#app-protection-ca-support-optional

<!-- Microsoft Learn documentation: Intune overview -->
[Intune App SDK overview]:/mem/intune/developer/app-sdk
[What is Microsoft Intune app management]:/mem/intune/apps/app-management
[iOS app protection policy settings]:/mem/intune/apps/app-protection-policy-settings-ios
[Plan for mobile application management in Microsoft Intune - Training | Microsoft Learn]:/training/modules/plan-for-mobile-application-management
[Overview of the Microsoft Authentication Library (MSAL)]:/azure/active-directory/develop/msal-overview
[Conditional Access (CA)]:/azure/active-directory/develop/active-directory-conditional-access-developer
[Microsoft Entra ID]:https://azure.microsoft.com/services/active-directory/
[App Protection CA]:/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection
[application configuration policies for managed apps]:/mem/intune/apps/app-configuration-policies-managed-app
[App Wrapping Tool for iOS]:/mem/intune/developer/app-wrapper-prepare-ios

<!-- Microsoft Learn documentation: Intune testing -->
[Microsoft partner]:https://partner.microsoft.com/business-opportunities/why-microsoft
[Microsoft CDX tenant creation site]:https://cdx.transform.microsoft.com/my-tenants/create-tenant
[Set up Intune]:/mem/intune/fundamentals/setup-steps
[Create users]:/mem/intune/fundamentals/users-add
[Create groups]:/mem/intune/fundamentals/groups-add
[Assign licenses]:/mem/intune/fundamentals/licenses-assign
[Create and assign app protection policies]:/mem/intune/apps/app-protection-policies
[app configuration policy]:/mem/intune/apps/app-configuration-policies-overview
[Quickstart: Register an app in the Microsoft identity platform - Microsoft identity platform]:/azure/active-directory/develop/quickstart-register-app
