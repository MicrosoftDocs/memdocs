---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - Multi-Identity
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. Multi-Identity
keywords:
author: Anh Tran
ms.author: tranamft
manager: shrua
ms.date: 12/19/2023
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

# Intune App SDK for iOS - Multi-Identity

## Enable multi-identity (optional)

By default, the SDK applies a policy to the app as a whole. Multi-identity is a MAM feature that you can enable to apply a policy on a per-identity level. This requires more app participation than other MAM features.

The app must inform the app SDK when it intends to change the active identity. The SDK also notifies the app when an identity change is required. Currently, only one managed identity is supported. After the user enrolls the device or the app, the SDK uses this identity and considers it the primary managed identity. Other users in the app will be treated as unmanaged with unrestricted policy settings.

Note that an identity is simply defined as a string. Identities are case-insensitive. Requests to the SDK for an identity might not return the same casing that was originally used when the identity was set.

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

If the app has a share extension, the owner of the item being shared can be retrieved through the  `protectionInfoForItemProvider` method in `IntuneMAMDataProtectionManager`. If the shared item is a file, the SDK will handle setting the file owner. If the shared item is data, the app is responsible for setting the file owner if this data is persisted to a file, and for calling the `setUIPolicyIdentity` API before showing this data in the UI.

### Turn on multi-identity

By default, apps are considered single identity. The SDK sets the process identity to the enrolled user. To enable multi-identity support, add a Boolean setting with the name `MultiIdentity` and a value of YES to the IntuneMAMSettings dictionary in the app's Info.plist file.

> [!NOTE]
> When multi-identity is enabled, the process identity, UI identity, and thread identities are set to nil. The app is responsible for setting them appropriately.

### Switch identities

* **App-initiated identity switch**:

    At launch, multi-identity apps are considered to be running under an unknown, unmanaged account. The conditional launch UI won't run, and no policies will be enforced on the app. The app is responsible for notifying the SDK whenever the identity should be changed. Typically, this will happen whenever the app is about to show data for a specific user account.

    An example is when the user attempts to open a document, a mailbox, or a tab in a notebook. The app needs to notify the SDK before the file, mailbox, or tab is actually opened. This is done through the `setUIPolicyIdentity` API in `IntuneMAMPolicyManager`. This API should be called whether or not the user is managed. If the user is managed, the SDK will perform the conditional launch checks, like jailbreak detection, PIN, and authentication.

    The result of the identity switch is returned to the app asynchronously through a completion handler. The app should postpone opening the document, mailbox, or tab until a success result code is returned. If the identity switch failed, the app should cancel the task.
    
    Multi-identity apps should avoid using `setProcessIdentity` as a way to set the identity. Apps that use UIScenes should use the `setUIPolicyIdentity:forWindow` API to set the identity.
    
    Apps can also set the identity for the current thread using `setCurrentThreadIdentity:` and `setCurrentThreadIdentity:forScope:`. For example the app may spawn a background thread, set the identity to the managed identity, and then perform file operations on managed files. If the app uses `setCurrentThreadIdentity:`, the app should also use `getCurrentThreadIdentity` so that it may restore the original identity once it's done. However if the app uses `setCurrentThreadIdentity:forScope:` then restoring the old identity occurs automatically. It's preferred to use `setCurrentThreadIdentity:forScope:`.
    
    In swift, due to async/await, `[IntuneMAMPolicyManager setCurrentThreadIdentity:]` and `[IntuneMAMPolicyManager setCurrentThreadIdentity:forScope:]` are not available. Instead in swift to set the current identity use `IntuneMAMSwiftContextManager.setIdentity(_, forScope:)`. There are variants of this API for async, throwing, and async throwing closures to be passed in.

* **SDK-initiated identity switch**:

    Sometimes, the SDK needs to ask the app to switch to a specific identity. Multi-identity apps must implement the `identitySwitchRequired` method in `IntuneMAMPolicyDelegate` to handle this request.

    When this method is called, if the app can handle the request to switch to the specified identity, it should pass `IntuneMAMAddIdentityResultSuccess` into the completion handler. If it can't handle switching the identity, the app should pass `IntuneMAMAddIdentityResultFailed` into the completion handler.

    The app doesn't have to call `setUIPolicyIdentity` in response to this call. If the SDK needs the app to switch to an unmanaged user account, the empty string will be passed into the `identitySwitchRequired` call.

* **SDK-initiated identity auto-enroll**:

     When the SDK needs to auto-enroll a user in the app to perform an action, apps must implement the `addIdentity:completionHandler:` method in `IntuneMAMPolicyDelegate`. The application must then call the completion handler and pass in IntuneMAMAddIdentityResultSuccess if the app is able to add the identity or IntuneMAMAddIdentityResultFailed otherwise.

* **Selective wipe**:

    When the app is selectively wiped, the SDK will call the `wipeDataForAccount` method in `IntuneMAMPolicyDelegate`. The app is responsible for removing the specified user's account and any data associated with it. The SDK is capable of removing all files owned by the user and will do so if the app returns FALSE from the `wipeDataForAccount` call.

    Note that this method is called from a background thread. The app shouldn't return a value until all data for the user has been removed (with the exception of files if the app returns FALSE).