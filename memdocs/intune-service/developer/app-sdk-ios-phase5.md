---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - Multi-Identity
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. Multi-Identity
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/31/2024
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

# Intune App SDK for iOS - Multi-Identity

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Stage 1: Plan the Integration].

## Stage 5: Multi-Identity (optional)

By default, the SDK applies a policy to the app as a whole. Multi-identity is a MAM feature that you can enable to apply a policy on a per-identity level. This requires more app participation than other MAM features.

The app must inform the app SDK when it intends to change the active identity. The SDK also notifies the app when an identity change is required. Currently, only one managed identity is supported. After the user enrolls the device or the app, the SDK uses this identity and considers it the primary managed identity. Other users in the app will be treated as unmanaged with unrestricted policy settings.

Note that an identity is simply defined as a string. Identities are case-insensitive. Requests to the SDK for an identity might not return the same casing that was originally used when the identity was set.

## Stage Goals

- Determine if your application needs multi-identity support.
- Understand how the Intune App SDK perceives identities.
- Refactor your application for identity awareness.
- Add code to inform the SDK of active and changing identities throughout your application.
- Thoroughly test app protection policy enforcement for both managed and unmanaged identities.

### Identity overview

An identity is simply the user name of an account (for example, user@contoso.com). Developers can set the identity of the app on the following levels:

* **Process identity**: Sets the process-wide identity and is mainly used for single identity applications. This identity affects all tasks, files, and UI.

* **UI identity**: Determines what policies are applied to UI tasks on the main thread, like cut/copy/paste, PIN, authentication, and data sharing. The UI identity doesn't affect file tasks like encryption and backup.

* **Thread identity**: Affects what policies are applied on the current thread. This identity affects all tasks, files, and UI.

The app is responsible for setting the identities appropriately, whether or not the user is managed.

At any time, every thread has an effective identity for UI tasks and file tasks. This is the identity that's used to check what policies, if any, should be applied. If the identity is "no identity" or the user isn't managed, no policies will be applied. The diagrams below show how the effective identities are determined.

:::image type="content" alt-text="Intune App SDK iOS: Identity determination process" source="./media/app-sdk-ios/ios-thread-identities.png" lightbox="./media/app-sdk-ios/ios-thread-identities.png":::

### Thread queues

Apps often dispatch asynchronous and synchronous tasks to thread queues. The SDK intercepts Grand Central Dispatch (GCD) calls and associates the current thread identity with the dispatched tasks. When the tasks are finished, the SDK temporarily changes the thread identity to the identity associated with the tasks, finishes the tasks, then restores the original thread identity.


Because `NSOperationQueue` is built on top of GCD, `NSOperations` will run on the identity of the thread at the time the tasks are added to `NSOperationQueue`. `NSOperations` or functions dispatched directly through GCD can also change the current thread identity as they are running. This identity will override the identity inherited from the dispatching thread.


In swift, due to a consequence of how the SDK propagates identities for `DispatchWorkItem`, the identity associated with a `DispatchWorkItem` is the identity of the thread that created the item not the thread that dispatches it.

### File owner

The SDK tracks the identities of local file owners and applies policies accordingly. A file owner is established when a file is created or when a file is opened in truncate mode. The owner is set to the effective file task identity of the thread that's performing the task.

Alternatively, apps can set the file owner identity explicitly by using `IntuneMAMFilePolicyManager`. Apps can use `IntuneMAMFilePolicyManager` to retrieve the file owner and set the UI identity before showing the file contents.

### Shared data

If the app creates files that have data from both managed and unmanaged users, the app is responsible for encrypting the managed user's data. You can encrypt data by using the `protect` and `unprotect` APIs in `IntuneMAMDataProtectionManager`.

The `protect` method accepts an identity that can be a managed or unmanaged user. If the user is managed, the data will be encrypted. If the user is unmanaged, a header will be added to the data that's encoding the identity, but the data won't be encrypted. You can use the `protectionInfo` method to retrieve the data's owner.

### Share extensions

If the app has a share extension, the owner of the item being shared can be retrieved through the  `protectionInfoForItemProvider` method in `IntuneMAMDataProtectionManager`. If the shared item is a file, the SDK will handle setting the file owner. If the shared item is data, the app is responsible for setting the file owner if this data is persisted to a file, and for calling the `setUIPolicyAccountId` API before showing this data in the UI.

### Turn on multi-identity

By default, apps are considered single identity. The SDK sets the process identity to the enrolled user. To enable multi-identity support, add a Boolean setting with the name `MultiIdentity` and a value of YES to the IntuneMAMSettings dictionary in the app's Info.plist file.

> [!NOTE]
> When multi-identity is enabled, the process identity, UI identity, and thread identities are set to nil. The app is responsible for setting them appropriately.

### Switch identities

* **App-initiated identity switch**:

    At launch, multi-identity apps are considered to be running under an unknown, unmanaged account. The conditional launch UI won't run, and no policies will be enforced on the app. The app is responsible for notifying the SDK whenever the identity should be changed. Typically, this will happen whenever the app is about to show data for a specific user account.

    An example is when the user attempts to open a document, a mailbox, or a tab in a notebook. The app needs to notify the SDK before the file, mailbox, or tab is actually opened. This is done through the `setUIPolicyAccountId` API in `IntuneMAMPolicyManager`. This API should be called whether or not the user is managed. If the user is managed, the SDK will perform the conditional launch checks, like jailbreak detection, PIN, and authentication.

    The result of the identity switch is returned to the app asynchronously through a completion handler. The app should postpone opening the document, mailbox, or tab until a success result code is returned. If the identity switch failed, the app should cancel the task.
    
    Multi-identity apps should avoid using `setProcessAccountId` as a way to set the identity. Apps that use UIScenes should use the `setUIPolicyAccountId:forWindow` API to set the identity.
    
    Apps can also set the identity for the current thread using `setCurrentThreadIdentity:` and `setCurrentThreadIdentity:forScope:`. For example the app may spawn a background thread, set the identity to the managed identity, and then perform file operations on managed files. If the app uses `setCurrentThreadAccountId:`, the app should also use `getCurrentThreadAccountId` so that it may restore the original identity once it's done. However if the app uses `setCurrentThreadAccountId:forScope:` then restoring the old identity occurs automatically. It's preferred to use `setCurrentThreadAccountId:forScope:`.
    
    In swift, due to async/await, `[IntuneMAMPolicyManager setCurrentThreadAccountId:]` and `[IntuneMAMPolicyManager setCurrentThreadAccountId:forScope:]` are not available. Instead in swift to set the current identity use `IntuneMAMSwiftContextManager.setAccountId(_, forScope:)`. There are variants of this API for async, throwing, and async throwing closures to be passed in.

* **SDK-initiated identity switch**:

    Sometimes, the SDK needs to ask the app to switch to a specific identity. Multi-identity apps must implement the `identitySwitchRequiredForAccountId` method in `IntuneMAMPolicyDelegate` to handle this request.

    When this method is called, if the app can handle the request to switch to the specified identity, it should pass `IntuneMAMAddIdentityResultSuccess` into the completion handler. If it can't handle switching the identity, the app should pass `IntuneMAMAddIdentityResultFailed` into the completion handler.

    The app doesn't have to call `setUIPolicyAccountId` in response to this call. If the SDK needs the app to switch to an unmanaged user account, the empty string will be passed into the `identitySwitchRequiredForAccountId` call.

* **SDK-initiated identity auto-enroll**:

     When the SDK needs to auto-enroll a user in the app to perform an action, apps must implement the `addIdentity:completionHandler:` method in `IntuneMAMPolicyDelegate`. The application must then call the completion handler and pass in IntuneMAMAddIdentityResultSuccess if the app is able to add the identity or IntuneMAMAddIdentityResultFailed otherwise.

* **Selective wipe**:

    When the app is selectively wiped, the SDK will call the `wipeDataForAccountId` method in `IntuneMAMPolicyDelegate`. The app is responsible for removing the specified user's account and any data associated with it. The SDK is capable of removing all files owned by the user and will do so if the app returns FALSE from the `wipeDataForAccountId` call.

    Note that this method is called from a background thread. The app shouldn't return a value until all data for the user has been removed (with the exception of files if the app returns FALSE).

### Exit Criteria

Plan to dedicate significant time for validating your app's integration of multi-identity. Before you start testing:

- Create and assign app protection policy to an account. This will be your test managed account.
- Create, but don't assign app protection policy to, another account. This will be your test unmanaged account. Alternately, if your app supports multiple account types beyond Microsoft Entra accounts, you can use an existing non-AAD account as the unmanaged test account.
- Refamiliarize yourself with how policy is enforced inside your app. Multi-identity testing requires you to easily distinguish when your app is and isn't operating with policy enforced. The app protection policy setting to block screenshots is effective at quickly testing policy enforcement.
- Consider the entire set of UI your app offers. Enumerate the screens where account data is displayed. Does your app only ever present a single account's data at once, or can it present data belonging to multiple accounts at the same time?
- Consider the entire set of files your app creates. Enumerate which of these files contain data belonging to an account, as opposed to system-level data.
  - Determine how you'll validate encryption on each of these files.
- Consider the entire set of ways your app can interact with other apps. Enumerate all the ingress and egress points. What types of data can your app ingest? What intents does it broadcast? What content providers does it implement?
  - Determine how you'll exercise each of these data sharing features.
  - Prepare a test device that has both managed and unmanaged apps that can interact with your app.
- Consider how your app enables the end user to interact with all logged in accounts. Does the user need to manually switch to an account before that account's data is displayed?

Once you've thoroughly assessed your app's current behavior, validate the multi-identity integration by executing the following set of tests.
Note, this isn't a comprehensive list and doesn't guarantee that your app's multi-identity implementation is bug-free.

#### Validating login and logout scenarios

Your multi-identity app supports up to 1 managed account and multiple unmanaged accounts.
These tests help ensure your multi-identity integration doesn't improperly change protections when users login or logout.

For these tests, install your app on a test device; don't log in before starting the test.

| Scenario | Steps |
| - | - |
| Log in managed first | - Log in first with a managed account and validate that account's data are managed. <br> - Log in with an unmanaged account and validate that account's data aren't managed. |
| Log in unmanaged first | - Log in first with an unmanaged account and validate that account's data aren't managed. <br> - Log in with a managed account and validate that account's data are managed. |
| Log in multiple managed | - Log in first with a managed account and validate that account's data are managed. <br> - Log in with a second managed account and validate that the user is blocked from logging in without first removing the original managed account. |
| Log out managed | - Log in to your app with both a managed an unmanaged account. <br> - Log out of the managed account. <br> - Confirm that the managed account is removed from your app and all that account's data has been removed. <br> - Confirm that the unmanaged account is still logged in, none of the unmanaged account's data has been removed, and policy is still not applied. |
| Log out unmanaged | - Log in to your app with both a managed an unmanaged account. <br> - Log out of the unmanaged account. <br> - Confirm that the unmanaged account is removed from your app and all that account's data has been removed. <br> - Confirm that the managed account is still logged in, none of the unmanaged account's data has been removed, and policy is still applied. |

#### Validating active identity and app lifecycle

Your multi-identity app may present views with a single account's data and allow the user to explicitly change the current in-use account.
It may also present views with multiple accounts' data at the same time.
These tests help ensure your multi-identity integration provides the right protections for the active identity on every page throughout the entire app lifecycle.

For these tests, install your app on a test device; log in with both a managed and unmanaged account before starting the test.

| Scenario | Steps |
| - | - |
| Single account view, managed | - Switch to the managed account. <br> - Navigate to all pages in your app that present a single account's data. <br> - Confirm that policy is applied on every page. |
| Single account view, unmanaged | - Switch to the unmanaged account. <br> - Navigate to all pages in your app that present a single account's data. <br> - Confirm that policy isn't applied on any page. |
| Multi-account view | - Navigate to all pages in your app that present multiple accounts' data simultaneously. <br> - Confirm that policy is applied on every page. |
| Managed pause | - On a screen with managed data displayed and policy active, pause the app by navigating to the device home screen or another app. <br> - Resume the app. <br> - Confirm that policy is still applied. |
| Unmanaged pause | - On a screen with unmanaged data displayed and no policy active, pause the app by navigating to the device home screen or another app. <br> - Resume the app. <br> - Confirm that policy isn't applied. |
| Managed kill | - On a screen with managed data displayed and policy active, force kill the app. <br> - Restart the app. <br> - Confirm that, if the app resumes on a screen with the managed account's data (expected), policy is still applied. If the app resumes on a screen with the unmanaged account's data, confirm that policy isn't applied. |
| Unmanaged kill |  - On a screen with unmanaged data displayed and policy active, force kill the app. <br> - Restart the app. <br> - Confirm that, if the app resumes on a screen with the unmanaged account's data (expected), policy isn't applied. If the app resumes on a screen with the managed account's data, confirm that policy is still applied.  |
| Identity switch ad hoc | - Experiment switching between accounts and pausing / resuming / killing  / restarting the app. <br> - Confirm that the managed account's data is always protected and the unmanaged account's data is never protected. |

#### Validating data sharing scenarios

Your multi-identity app may send data to and receive data from other apps.
Intune's app protection policies have settings that dictate this behavior.
These tests help ensure your multi-identity integration honors these data sharing settings.

For these tests, install your app on a test device; log in with both a managed and unmanaged account before starting the test. Additionally:

- Set the managed account's policy as:
  - "Send org data to other apps" to "Policy managed apps".
  - "Receive data from other apps" to "Policy managed apps".
- Install other apps on the test device:
  - A managed app, targeted with the same policy as your app, that can send and receive data (like Microsoft Outlook).
  - Any unmanaged app that can send and receive data.
- Log in to the other managed app with the managed test account. Even if the other managed app is multi-identity, only log in with the managed account.

If your app has the ability to send data to other apps, like Microsoft Outlook sending a document attachment to Microsoft Office:

| Scenario | Steps |
| - | - |
| Managed identity send to unmanaged app | - Switch to the managed account. <br> - Navigate to where your app can send data. <br> - Attempt to send data to an unmanaged app. <br> - You should be blocked from sending data to the unmanaged app. |
| Managed identity send to managed app | - Switch to the managed account. <br> - Navigate to where your app can send data. <br> - Attempt to send data to the other managed app with the managed account signed in. <br> - You should be allowed to send data to the managed app.  |
| Unmanaged identity send to managed app | - Switch to the unmanaged account. <br> - Navigate to where your app can send data. <br> - Attempt to send data to the other managed app with the managed account signed in. <br> - You should be blocked from sending data to the other managed app. |
| Unmanaged identity send to unmanaged app | - Switch to the unmanaged account. <br> - Navigate to where your app can send data. <br> - Attempt to send data to an unmanaged app. <br> - You should always be allowed to send an unmanaged account's data to an unmanaged app. |

Your app may actively import data from other apps, like Microsoft Outlook attaching a file from Microsoft OneDrive.
Your app may also passively receive data from other apps, like Microsoft Office opening a document from a Microsoft Outlook attachment.
The receive app protection policy setting covers both scenarios.

If your app has the ability to actively import data from other apps:

| Scenario | Steps |
| - | - |
| Managed identity import from unmanaged app | - Switch to the managed account. <br> - Navigate to where your app can import data from other apps. <br> - Attempt to import data from an unmanaged app. <br> - You should be blocked from importing data from unmanaged apps. |
| Managed identity import from managed app | - Switch to the managed account. <br> - Navigate to where your app can import data from other apps. <br> - Attempt to import data from the other managed app with the managed account signed in. <br> - You should be allowed to import data from the other managed app. |
| Unmanaged identity import from managed app | - Switch to the unmanaged account. <br> - Navigate to where your app can import data from other apps. <br> - Attempt to import data from the other managed app with the managed account signed in. <br> - You should be blocked from importing data from the other managed app. |
| Unmanaged identity import from unmanaged app | - Switch to the unmanaged account. <br> - Navigate to where your app can import data from other apps. <br> - Attempt to import data from an unmanaged app. <br> - You should always be allowed to import data from unmanaged app for an unmanaged account. |

If your app has the ability to passively receive data from other apps:

| Scenario | Steps |
| - | - |
| Managed identity receive from unmanaged app | - Switch to the managed account. <br> - Switch to the unmanaged app. <br> - Navigate to where it can send data. <br> - Attempt to send data from the unmanaged app to your app. <br> - Your app's managed account shouldn't be able to receive data from the unmanaged app. |
| Managed identity receive from managed app | - Switch to the managed account. <br> - Switch to the other managed app with the managed account signed in. <br> - Navigate to where it can send data. <br> - Attempt to send data from the managed app to your app. <br> - Your app's managed account should be allowed to receive data from the other managed app. |
| Unmanaged identity receive from managed app | - Switch to the unmanaged account. <br> - Switch to the other managed app with the managed account signed in. <br> - Navigate to where it can send data. <br> - Attempt to send data from the managed app to your app. <br> - Your app's unmanaged account shouldn't be able to receive data from the managed app. |
| Unmanaged identity receive from unmanaged app | - Switch to the unmanaged account. <br> - Switch to the unmanaged app. <br> - Navigate to where it can send data. <br> - Attempt to send data from the unmanaged app to your app. <br> - Your app's unmanaged account should always be allowed to receive data from the unmanaged app. |

Failures in these tests may indicate that your app doesn't have the right active identity set when it attempts to send or receive data.
You can investigate this by leveraging the SDK's get identity APIs at the point of sending/receiving to confirm the active identity is set properly.


## Next Steps

After you've completed all the [Exit Criteria] above, your app is now successfully integrated as multi-identity and can enforce app protection policies on a per-identity basis.
The subsequent sections, [Stage 6: App Protection Conditional Access support] and [Stage 7: Web-view features], may or may not be required, depending on your app's desired app protection policy support.


<!-- Stage 5 links -->
[Exit Criteria]:#exit-criteria
[Stage 1: Plan the Integration]:app-sdk-ios-phase1.md
[Stage 6: App Protection Conditional Access support]:app-sdk-ios-phase6.md
[Stage 7: Web-view features]: app-sdk-ios-phase7.md
