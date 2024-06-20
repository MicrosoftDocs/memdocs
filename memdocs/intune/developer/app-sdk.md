---
title: Benefits of Intune App SDK 
titleSuffix: Microsoft Intune
description: The Intune App SDK is available for both the iOS and Android platforms, and enables mobile app management features with Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: cd9f05e7-26e6-45e0-8d38-67d8232b1cae

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---

# Microsoft Intune App SDK overview
The Intune App SDK, available for both iOS and Android, enables your app to support Intune [app protection policies](../apps/app-protection-policy.md). When your app has app protection policies applied to it, it can be managed by Intune and is recognized by Intune as a managed app. The SDK strives to minimize the amount of code changes required from the app developer. You'll find that you can enable most of the SDK's features without changing your app's behavior. For enhanced end-user and IT administrator experience, you can utilize the SDK's APIs to customize your app behavior to support features that require your app participation.

Once you have enabled your app to support Intune app protection policies, IT administrators can deploy these policies to protect their corporate data within the app.

## App protection features

The following are examples of Intune app protection features that can be enabled with the SDK.

### Control users' ability to move corporate files
IT administrators can control where work or school data in the app can be moved. For instance, they can deploy a policy that disables the app from backing up corporate data to the cloud.

### Configure clipboard restrictions
IT administrators can configure the clipboard behavior in Intune-managed apps. For instance, they can deploy a policy to prevent end users from cutting or copying data from the app and pasting into an unmanaged, personal app.

### Enforce encryption on saved data
IT administrators can enforce a policy that ensures that data saved to the device by the app is encrypted.

### Remotely wipe corporate data
IT administrators can remotely wipe corporate data from an Intune-managed app. This feature is identity-based and will only delete the files associated with the corporate identity of the end user. To do that, the feature requires the app's participation. The app can specify the identity for which the wipe should occur based on user settings. In the absence of these specified user settings from the app, the default behavior is to wipe the application directory and notify the end user that access has been removed.

### Enforce the use of a managed browser
IT administrators can force web links in the app to be opened with the [Microsoft Edge app](../apps/manage-microsoft-edge.md). This functionality ensures that links that appear in a corporate environment are kept within the domain of Intune-managed apps.

### Enforce a PIN policy
IT administrators can require the end-user to enter a PIN before accessing corporate data in the app. This ensures that the person using the app is the same person who initially signed in with their work or school account. When end users configure their PIN, the Intune App SDK uses Microsoft Entra ID to verify the credentials of end-users against the enrolled Intune account.

### Require users to sign in with a work or school account for app access
IT administrators can require users to sign in with their work or school account to access the app. The Intune App SDK uses Microsoft Entra ID to provide a single sign-on experience, where the credentials, once entered, are reused for subsequent logins. We also support authentication of identity management solutions federated with Microsoft Entra ID.

### Check device health and compliance
IT administrators can a check the health of the device and its compliance with Intune policies before end-users access the app. On iOS/iPadOS, this policy checks if the device has been jailbroken. On Android, this policy checks if the device has been rooted.

### Support multi-identity
Multi-identity support is a feature of the SDK that enables coexistence of policy-managed (corporate) and unmanaged (personal) accounts in a single app.

For example, many users configure both corporate and personal email accounts in the Office mobile apps for iOS and Android. When a user accesses data with their corporate account, the IT administrator must be confident that app protection policy will be applied. However, when a user is accessing a personal email account, that data should be outside of the IT administrator's control. The Intune App SDK achieves this by targeting the app protection policy to **only** the corporate identity in the app.

The multi-identity feature helps solve the data protection problem that organizations face with store apps that support both personal and work accounts.
 
### App protection without device enrollment

>[!IMPORTANT]
>Intune app protection without device enrollment is available with the Intune App Wrapping Tools, Intune App SDK for Android, Intune App SDK for iOS, and Intune App SDK Xamarin Bindings.

Many users with personal devices want to access corporate data without enrolling their personal device with a Mobile Device Management (MDM) provider. Since MDM enrollment requires global control of the device, users are often hesitant to give control of their personal device over to their company.

App protection without device enrollment allows the Microsoft Intune service to deploy app protection policy to an app directly, without relying on a device management channel to deploy the policy.

## Next steps

- [Get started with the Microsoft Intune App SDK](app-sdk-get-started.md).
