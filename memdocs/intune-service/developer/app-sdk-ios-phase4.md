---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - App participation features
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. App participation features
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/04/2024
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

# Intune App SDK for iOS - App participation features

The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native iOS app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Plan the Integration].

## Stage 4: App participation features

## Stage Goals

- Learn about the various app participation features offered by the Intune App SDK.
- Integrate app participation features relevant to your app and users.
- Test the integration of those features.

## What are "App Participation Features"?

This SDK integration process attempts to minimize the amount of app-specific code that developers need to write.
By successfully completing the prior stages of the SDK integration your app can now enforce the majority of app protection policy settings, such as file encryption, copy/paste restrictions, screenshot blocking, and data transfer restrictions.

However, there are some settings that require app-specific code to enforce properly; these are called app participation features.
Typically, the SDK doesn't have enough context about your application's code or the end user scenario to automatically enforce these settings, and thus relies on developers to call the SDK APIs appropriately.

App participation features aren't necessarily optional.
Depending on your app's existing features, these features may be required.

The next stages of this guide will describe several important app participation features:

- Multi-identity as covered in [Stage 5: Multi-Identity].
- App Protection CA as covered in [Stage 6: App Protection Conditional Access support]
- Web-view specific features covered in [Stage 7: Web-view features]

The rest of this guide describes the remaining set of app participation features:

- Implement Allowed Accounts
- Implement File Encryption Required
- Implement save-as and open-from controls
- Share Data via UIActivityViewController
- Enable targeted configuration (APP/MAM app config) for your iOS applications
- Telemetry
- Siri Intents
- App Clips
- Printing
- Notifications
- Post build script

## Customize your app's behavior with APIs

The Intune App SDK has several APIs you can call to get information about the Intune APP policy deployed to the app. You can use this data to customize your app's behavior. The following table provides information on some essential Intune classes you use.

Class | Description
----- | -----------
IntuneMAMPolicyManager.h | The IntuneMAMPolicyManager class exposes the Intune APP policy deployed to the application. Notably, it exposes APIs that are useful for [Enabling multi-identity]. |
IntuneMAMPolicy.h | The IntuneMAMPolicy class exposes some MAM policy settings that apply to the app. Most of these policy settings are exposed so the app can customize its UI. Most policy settings are enforced by the SDK and not the app. However, there are some exceptions. App developers should review the comments in this header to determine which APIs are applicable to their application's scenarios. |
IntuneMAMFileProtectionManager.h | The IntuneMAMFileProtectionManager class exposes APIs the app can use to explicitly secure files and directories based on a supplied identity. The identity can be managed by Intune or unmanaged, and the SDK will apply the appropriate MAM policy. Using this class is optional. |
IntuneMAMDataProtectionManager.h | The IntuneMAMDataProtectionManager class exposes APIs the app can use to secure data buffers given a supplied identity. The identity can be managed by Intune or unmanaged, and the SDK will apply encryption appropriately. |

## Implement Allowed Accounts

Intune lets IT admins specify which accounts can be logged into by the user. Apps can query the Intune App SDK for the specified list of allowed accounts and then ensure only allowed accounts are signed into the device.

To query for allowed accounts, the App should check the `allowedAccounts` property on the `IntuneMAMEnrollmentManager`. The `allowedAccounts` property is either an array containing the allowed accounts or nil. If the property is nil then no allowed accounts have been specified. MSAL/OneAuth enabled applications should use the `allowedAccountIds` property on the `IntuneMAMEnrollmentManager` instance to query Entra object ID.

Apps can also react to changes of the `allowedAccounts` property by observing the `IntuneMAMAllowedAccountsDidChangeNotification` notification. The notification is posted whenever the `allowedAccounts` property changes in value.

The following requirements are needed when using APIs for allowed accounts: 
- Identity comparison must be case insensitive for UPN and OID.
- Identity comparison must support both UPN and OID.
- Application must have logging to diagnosis any mismatch between the admin-specified account and user-entered account.

## Implement File Encryption Required

The `isFileEncryptionRequired` API defined in `IntuneMAMPolicy.h` informs applications when the IT administrator requires that applications use Intune encryption on any files saved to disk. If `isFileEncryptionRequired` is true, then it's the app's responsibility to ensure that any files saved to disk by the app are encrypted using the APIs in `IntuneMAMFile.h`, `IntuneMAMFileProtectionManager.h`, and `IntuneMAMFDataProtectionManager.h`.

Apps can react to changes in this policy by observing the `IntuneMAMDataProtectionDidChangeNotification` notification defined in `IntuneMAMFDataProtectionManager.h`.

## Implement save-as and open-from controls

Intune lets IT admins select which storage locations a managed app can save data to or open data from. Apps can query the Intune MAM SDK for allowed save-to storage locations by using the `isSaveToAllowedForLocation:withAccountId:` API, defined in `IntuneMAMPolicy.h`. Apps can also query the SDK for allowed open-from storage locations by using the `isOpenFromAllowedForLocation:withAccountId:` API, also defined in `IntuneMAMPolicy.h`.

Additionally, apps can verify that incoming data from a share extension is allowed by querying the `canReceiveSharedItemProvider:` API, defined in `IntuneMAMPolicy.h`. Apps can also query the `canReceiveSharedFile:` API to verify incoming files from an openURL call, also defined in `IntuneMAMPolicy.h`

> [!NOTE] 
> Changes have been made to internal behavior as of MAM SDK v15.1.0.
> - A `nil` account will no longer be treated as the current account for the LocalDrive/LocalStorage locations. Passing in a `nil` account will have it treated as an unmanaged account. Because app's can control how they handle their sandbox storage, an identity can and should be associated with those locations.
> - A `nil` account will no longer be treated as the current account for single-identity apps. Passing in a `nil` account in a single-identity app will now be treated exactly the same as if it was passed into a multi-identity app. If you are developing a single-identity app, please use the `IntuneMAMPolicy`'s `primaryUser` to refer to the current account if managed and `nil` to refer to the current account if unmanaged.

### Handling save-to scenarios

Before moving data to a new cloud-storage or local location, an app must check with the `isSaveToAllowedForLocation:withAccountId:` API to know if the IT admin has allowed the data transfer. This method is called on an `IntuneMAMPolicy` object. Data being edited and saved in-place doesn't need to be checked with this API.

> [!NOTE] 
> The `IntuneMAMPolicy` object should represent the policies of the owner of the data being saved. To get the `IntuneMAMPolicy` object of a specific identity, call `IntuneMAMPolicyManager`'s `policyForAccountId:` method. If the owner is an unmanaged account with no identity, `nil` can be passed into `policyForAccountId:`.  Even if the data being saved is not organizational data, `isSaveToAllowedForLocation:withAccountId:` should still be called. The account owning the destination location might still have policies restricting incoming unmanaged data.

The `isSaveToAllowedForLocation:withAccountId:` method takes two arguments. The first argument is an enum value of the type `IntuneMAMSaveLocation` defined in `IntuneMAMPolicy.h`. The second argument is the UPN of the identity that owns the location. If the owner isn't known, `nil` can be used instead.

#### Supported save locations

The Intune MAM SDK provides support for the following save locations defined in `IntuneMAMPolicy.h`:

* `IntuneMAMSaveLocationOneDriveForBusiness` - This location represents OneDrive for Business locations. The identity associated with the OneDrive account should be passed in as the second argument.
* `IntuneMAMSaveLocationSharePoint` - This location represents both SharePoint online and Microsoft Entra Hybrid Modern Auth SharePoint on-premises locations. The identity associated with the SharePoint account should be passed in as the second argument.
* `IntuneMAMSaveLocationLocalDrive` - This location represents app-sandbox storage that can only be accessed by the app. This location should **not** be used for saving via a file picker or for saving to files through a share extension. If an identity can be associated with the app-sandbox storage, it should be passed in as the second argument. If there's no identity, `nil` should be passed instead. For example, an app might use separate app-sandbox storage containers for different accounts. In this case, the account that owns the container being accessed should be used as the second argument.
* `IntuneMAMSaveLocationCameraRoll` - This location represents the iOS Photo Library. Because there's no account associated with the iOS Photo Library, only `nil` should be passed as the second argument when this location is used. 
* `IntuneMAMSaveLocationAccountDocument` - This location represents any organization location not previously listed that can be tied to a managed account. The organization account associated with the location should be passed in as the second argument. For example, uploading a photo to an organization’s LOB cloud service that is tied to the organization account.
* `IntuneMAMSaveLocationOther` - This location represents any nonorganizational, not previously listed, or any unknown location. If an account is associated with the location, it should be passed in as the second argument. Otherwise, `nil` should be used instead.

##### Special considerations for save locations

The `IntuneMAMSaveLocationLocalDrive` location should only be used for app-sandbox storage that can only be accessed by the app. For checking if a file can be saved to iOS device storage through a file picker or some other method where the data will be accessible in the Files app, `IntuneMAMSaveLocationOther` should be used.

If the destination location isn't listed, either `IntuneMAMSaveLocationAccountDocument` or `IntuneMAMSaveLocationOther` should be used. If the location contains organizational data that is accessed using the managed account (ie. LOB cloud service for storing organizational data), `IntuneMAMSaveLocationAccountDocument` should be used. If the location doesn't contain organizational data, then the `IntuneMAMSaveLocationOther` location should be used.

### Handling open-from scenarios

Before importing data from a new cloud-storage or local location, an app must check with the `isOpenFromAllowedForLocation:withAccountId:` API to know if the IT admin has allowed the data transfer. This method is called on an `IntuneMAMPolicy` object. Data being opened in-place doesn't need to be checked with this API.

> [!NOTE] 
> The `IntuneMAMPolicy` object should represent the policies of the identity receiving the data. To get the `IntuneMAMPolicy` object of a specific identity, call `IntuneMAMPolicyManager`'s `policyForAccountId:` method. If the receiving account is an unmanaged account with no identity, `nil` can be passed into `policyForAccountId:`. Even if the data being received is not organizational data, `isOpenFromAllowedForLocation:withAccountId:` should still be called. The account owning the data might still have policies restricting the destinations of outgoing data transfers.

The `isOpenFromAllowedForLocation:withAccountId:` method takes two arguments. The first argument is an enum value of the type `IntuneMAMOpenLocation` defined in `IntuneMAMPolicy.h`. The second argument is the UPN of the identity that owns the location. If the owner isn't known, `nil` can be used instead.

#### Supported open locations

The Intune MAM SDK provides support for the following open locations defined in `IntuneMAMPolicy.h`:

* `IntuneMAMOpenLocationOneDriveForBusiness` - This location represents OneDrive for Business locations. The identity associated with the OneDrive account should be passed in as the second argument.
* `IntuneMAMOpenLocationSharePoint` - This location represents both SharePoint online and Microsoft Entra Hybrid Modern Auth SharePoint on-premises locations. The identity associated with the SharePoint account should be passed in as the second argument.
* `IntuneMAMOpenLocationCamera` - This location **only** represents new images taken by the camera. Because there's no account associated with the iOS camera, only `nil` should be passed as the second argument when this location is used. For opening data from the iOS Photo Library, use  `IntuneMAMOpenLocationPhotos`.
* `IntuneMAMOpenLocationPhotos` - This location **only** represents existing images within the iOS Photo Library. Because there's no account associated with the iOS Photo Library, only `nil` should be passed as the second argument when this location is used. For opening images taken directly from the iOS camera, use `IntuneMAMOpenLocationCamera`.
* `IntuneMAMOpenLocationLocalStorage` - This location represents app-sandbox storage that can only be accessed by the app. This location should **not** be used for opening files from a file picker or handling incoming files from an openURL. If an identity can be associated with the app-sandbox storage, it should be passed in as the second argument. If there's no identity, `nil` should be passed instead. For example, an app might use separate app-sandbox storage containers for different accounts. In this case, the account that owns the container being accessed should be used as the second argument. 
* `IntuneMAMOpenLocationAccountDocument` - This location represents any organization location not previously listed that can be tied to a managed account. The organization account associated with the location should be passed in as the second argument. For example, downloading a photo from an organization’s LOB cloud service that is tied to the organization account.
* `IntuneMAMOpenLocationOther` - This location represents any nonorganizational location, not previously listed, or any unknown location. If an account is associated with the location, it should be passed in as the second argument. Otherwise, `nil` should be used instead.

##### Special considerations for open locations

The `IntuneMAMOpenLocationLocalStorage` location should only be used for app-sandbox storage that can be accessed by the app. For checking if a file can be opened from iOS device storage through a file picker or some other method where the data is also accessible in the Files app, `IntuneMAMOpenLocationOther` should be used.

If the destination location isn't listed, either `IntuneMAMOpenLocationAccountDocument` or `IntuneMAMOpenLocationOther` should be used. If the location contains organizational data that is accessed using the managed account. For example, LOB cloud service for storing organizational data, `IntuneMAMOpenLocationAccountDocument` should be used. If the location doesn't contain organizational data, then the `IntuneMAMSaveLocationOther` location should be used.

##### Handling incoming NSItemProviders and Files

For handling NSItemProviders received from a share extension, the `IntuneMAMPolicy`'s `canReceiveSharedItemProvider:` method can be used instead of `isOpenFromAllowedForLocation:withAccountId:`. The `canReceiveSharedItemProvider:` method takes an NSItemProvider and returns whether it's allowed by the IT admin to be opened into the `IntuneMAMPolicy` object's account. The item must be loaded prior to calling this method. For example, by calling `loadItemForTypeIdentifier:options:completionHandler`. This method can also be called from the completion handler passed to the NSItemProvider load call.

For handling incoming files, the `IntuneMAMPolicy`'s `canReceiveSharedFile:` method can be used instead of `isOpenFromAllowedForLocation:withAccountId:`. The `canReceiveSharedFile:` method takes a NSString path and returns whether it's allowed by the IT admin to be opened into the `IntuneMAMPolicy` object's account.

### Sharing blocked alert

A UI helper function can be used when either the `isSaveToAllowedForLocation:withAccountId:` or `isOpenFromAllowedForLocation:withAccountId:` API is called and found to block the save/open action. If the app wants to notify the user  that the action was blocked, it can call the `showSharingBlockedMessage` API defined in `IntuneMAMUIHelper.h` to present an alert view with a generic message.

## Share Data via UIActivityViewController

Starting in release 8.0.2, the Intune App SDK can filter `UIActivityViewController` actions so that only Intune managed share locations are available to select. This behavior will be controlled by the application data transfer policy.

### 'Copy To' actions

When sharing documents via the `UIActivityViewController` and `UIDocumentInteractionController`, iOS displays 'Copy to' actions for each application that supports opening the document being shared. Applications declare the document types they support through the `CFBundleDocumentTypes` setting in their Info.plist. This type of sharing will no longer be available if the policy prohibits sharing to unmanaged applications. As a replacement, user will have to add a non-UI Action extension to their application and link it to the Intune App SDK. The Action extension is merely a stub. The SDK will implement the file sharing behavior. Follow the steps below:

1. Your application must have at least one schemeURL defined under its Info.plist `CFBundleURLTypes` along with its `-intunemam` counterpart. For example:
    ```xml
    <key>CFBundleURLSchemes</key>
	<array>
		<string>launch-com.contoso.myapp</string>
  		<string>launch-com.contoso.myapp-intunemam</string>
	</array>
    ```

2. Both your application and action extension must share at least one App Group, and the App Group must be listed under the `AppGroupIdentifiers` array under the app's and the extension's IntuneMAMSettings dictionaries.

3. Both your application and action extension must have the Keychain Sharing capability and share the `com.microsoft.intune.mam` keychain group.

4. Name the action extension "Open in" followed by the application name. Localize the Info.plist as needed.

5. Provide a template icon for the extension as described by Apple's developer documentation. Alternatively, the IntuneMAMConfigurator tool can be used to generate these images from the application .app directory. To do this, run:

    ```bash
    IntuneMAMConfigurator -generateOpenInIcons /path/to/app.app -o /path/to/output/directory
    ```

6. Under IntuneMAMSettings in the extension's Info.plist, add a Boolean setting named `OpenInActionExtension` with value YES.

7. Configure the `NSExtensionActivationRule` to support a single file and all types from the application's `CFBundleDocumentTypes` prefixed with `com.microsoft.intune.mam`. For example, if the application supports public.text and public.image, the activation rule would be:

    ```objc
    SUBQUERY (
        extensionItems,
        $extensionItem,
        SUBQUERY (
            $extensionItem.attachments,
            $attachment,
            ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.text" ||
            ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.image").@count == 1
    ).@count == 1
    ```

### Update existing Share and Action extensions

If your app already contains Share or Action extensions, then their `NSExtensionActivationRule` will have to be modified to allow the Intune types. For each type supported by the extension, add an additional type prefixed with `com.microsoft.intune.mam`. For example, if the existing activation rule is:  

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.data"
    ).@count > 0
).@count > 0
```

It should be changed to:

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.data" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.data"
    ).@count > 0
).@count > 0
```

> [!NOTE]
> The IntuneMAMConfigurator tool can be used to add the Intune types to the activation rule. If your existing activation rule uses the predefined string constants. For example, NSExtensionActivationSupportsFileWithMaxCount, NSExtensionActivationSupportsText, etc., the predicate syntax can get quite complex. The IntuneMAMConfigurator tool can also be used to convert the activation rule from the string constants to a predicate string while adding the Intune types.

### What the UI should look like

Old UI:

![Sharing data - iOS old sharing UI](./media/app-sdk-ios/sharing-ui-old.png)

New UI:

![Sharing data - iOS new sharing UI](./media/app-sdk-ios/sharing-ui-new.png)

## Enable targeted app configuration for your iOS applications

MAM targeted configuration (also know as MAM app config) allows an app to receive configuration data through the Intune SDK. The format and variants of this data must be defined and communicated to Intune customers by the app owner/developer.

Intune administrators can target and deploy configuration data via the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and Intune Graph API. As of version 7.0.1 of the Intune App SDK for iOS, apps that are participating in MAM targeted configuration can be provided MAM targeted configuration data via the MAM Service. The application configuration data is pushed through our MAM Service directly to the app instead of through the MDM channel. The Intune App SDK provides a class to access the data retrieved from these consoles. The following items are prerequisites:

* The app needs to be enrolled with the Intune MAM service before you access the MAM targeted config UI. For more information, see [Receive app protection policy](../developer/app-sdk-ios-phase3.md#receive-app-protection-policy).

* Include `IntuneMAMAppConfigManager.h` in your app's source file.

* Call `[[IntuneMAMAppConfigManager instance] appConfigForAccountId:]` to get the App Config Object.

* Call the appropriate selector on `IntuneMAMAppConfig` object. For example, if your application's key is a string, you'd want to use `stringValueForKey` or `allStringsForKey`. See `IntuneMAMAppConfig.h` for a detailed description on return values and error conditions.

For more information about the capabilities of the Graph API, see [Graph API Reference](/graph/overview).

For more information about how to create a MAM targeted app configuration policy in iOS, see the section on MAM targeted app config in [How to use Microsoft Intune app configuration policies for iOS/iPadOS](../apps/app-configuration-policies-use-ios.md).

## Telemetry

By default, the Intune App SDK for iOS collects telemetry on the following types of events:

* **App launch**: To help Microsoft Intune learn about MAM-enabled app usage by management type (MAM with MDM, MAM without MDM enrollment, and so on).

* **Enrollment calls**: To help Microsoft Intune learn about success rate and other performance metrics of enrollment calls initiated from the client side.

* **Intune actions**: To help diagnose issues and ensure Intune functionality, we collect information about Intune SDK actions.

> [!NOTE]
> If you choose not to send Intune App SDK telemetry data to Microsoft Intune from your mobile application, you must disable Intune App SDK telemetry capture. Set the property `MAMTelemetryDisabled` to YES in the IntuneMAMSettings dictionary.

## Siri Intents

If your app integrates with Siri Intents or makes Siri Intent Donations, please make sure to read the comments for `areSiriIntentsAllowed` in `IntuneMAMPolicy.h` for instructions on supporting this scenario. 

> [!NOTE]
> In iOS 16 and above, a new App Intents system framework is available for creating Swift App Intents. Apps that implement an App Intent should first check the `areSiriIntentsAllowed` property on the IntuneMAMPolicy object for the user.

 ## App Clips

 If your app includes an app clip target, be sure to verify no managed data is presented in the app clip. The app clip should be considered an unmanaged location. SDK integration into App Clips is not currently supported.
    
 ## Printing

 If your app implements printing and provides a custom print action on a custom menu, be sure to utilize `UIPrintInteractionController.isPrintingAvailable()` to determine if you should add your print action to your custom menu.

 ## Screen capture blocking

For apps that have updated to v19.7.6 or later for Xcode 15 and v20.2.1 or later for Xcode 16 of the SDK, screen capture block will be applied if you have configured `Send Org data to other apps` to a value other than “All apps”. You can configure app configuration policy setting “com.microsoft.intune.mam.screencapturecontrol = Disabled” if you wish to allow screen capture for your iOS devices.
 
## Notifications

If your app receives notifications, please make sure to read the comments for `notificationPolicy` in `IntuneMAMPolicy.h` for instructions on supporting this scenario.  It's recommended that apps register for `IntuneMAMPolicyDidChangeNotification` described in `IntuneMAMPolicyManager.h`, and communicate this value to their `UNNotificationServiceExtension` via the keychain.

## Safari web extensions

If your app has a Safari web extension and supports sending data between the extension and the parent application, in some scenarios, your application might need to support blocking the data. To block the data, in the parent application, call the `isAppSharingAllowed` API in `IntuneMAMPolicy.h`, and then block the web extension.

## Post build script

The **IntuneMAMFrameworkPatcher** command line tool no longer must be run as the last step of the application build process. However, this tool is available as part of the Intune App SDK for iOS on [GitHub](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios).

> [!IMPORTANT]
> As of the 17.7.1 release of the Intune MAM SDK, this step is no longer required. The **IntuneMAMFrameworkPatcher** command line tool no longer must be run.

### Command line usage

```bash
IntuneMAMFrameworkPatcher -i /path/to/directory_or_binary [-resign] [-verbose]
```

**Parameters**:

- `i`, `r`, `v`: This parameter allows you to choose to install, remove, or verify the Intune MAM Framework Patcher for the application build process.
- `path`: The `path` should be the root of the application's *.app* directory.
- `resign`: The `resign` option instructs the tool to resign binaries which had a valid signature prior to patching the binary. This option should be used if the project includes framework dependencies or plugins with the **Embed and Sign** option, even when run prior to the final application signing, or if the tool is run after the final application signing.
- `verbose`: The `verbose` option will cause the tool to output information about each binary which was patched.

**Other usages**:

- Remove the patch:

  `IntuneMAMFrameworkPatcher -r /path/to/directory_or_binary [-resign] [-verbose]`

- Verify the patch:

  `IntuneMAMFrameworkPatcher -v /path/to/directory_or_binary [-verbose]`

**Example script**:

```bash
IntuneMAMFrameworkPatcher -i $BUILT_PRODUCTS_DIR/$EXECUTABLE_FOLDER_PATH -resign -verbose
```

For more information about getting started and downloading the SDK, see [Get started with the Microsoft Intune App SDK](../developer/app-sdk-get-started.md).

## Exit Criteria

### Validating save to / open from restrictions

Skip if you didn't [Implement save-as and open-from controls].

Refamiliarize yourself with every scenario where your app can save data to cloud storages or local locations and open data from cloud storages or local locations.

For simplicity, these tests will assume your app only includes support for saving to and opening data from OneDrive for Business from a single location within the app.
However, you must validate every combination: every supported save location against every place your app allows saving data, and every supported open location against every place your app allows opening data.

For these tests, install your app, integrate it with the SDK and log in with a managed account before starting the test.

Additionally:

- Set the managed account's policy as:
  - "Send org data to other apps" to "Policy managed apps".
  - "Receive data from other apps" to "Policy managed apps".

| Scenario | Preconditions | Steps |
| - | - | - |
| Save to, fully allowed | "Save copies of org data" policy set to "Allow" | - Navigate to where your app can save data to OneDrive for Business. <br> - Attempt to save a document to OneDrive for Business, to the same managed account logged into your app. <br> - Confirm the save is allowed. |
| Save to, exempted | - "Save copies of org data" policy set to "Block" <br> - "Allow user to save copies to selected services" policy set to "OneDrive for Business" only | - Navigate to where your app can save data to OneDrive for Business. <br> - Attempt to save a document to OneDrive for Business, to the same managed account logged into your app. <br> - Confirm the save is allowed. <br> - If your app allows, attempt to save the file to a different cloud storage location and confirm it is blocked. |
| Save to, blocked | "Save copies of org data" policy set to "Block" | - Navigate to where your app can save data to OneDrive for Business. <br> - Attempt to save a document to OneDrive for Business, to the same managed account logged into your app. <br> - Confirm the save is blocked. <br> - If your app allows, attempt to save the file to a different cloud storage location and confirm it is blocked. |
| Open from, fully allowed | "Open data into Org documents" policy set to "Allow" | - Navigate to where your app can open data from OneDrive for Business. <br> - Attempt to open a document from OneDrive for Business, from the same managed account logged into your app's storage. <br> - Confirm the open is allowed. |
| Open from, exempted | - "Open data into Org documents" policy set to "Block" <br> - "Allow users to open data from selected services" policy set to "OneDrive for Business" only | - Navigate to where your app can open data from OneDrive for Business. <br> - Attempt to open a document from OneDrive for Business, from the same managed account logged into your app's storage. <br> - Confirm the open is allowed. <br> - If your app allows, attempt to open another file from a different cloud storage location and confirm it is blocked. |
| Open from, blocked | "Open data into Org documents" policy set to "Block" | - Navigate to where your app can open data from OneDrive for Business. <br> - Attempt to open a document from OneDrive for Business, from the same managed account logged into your app's storage. <br> - Confirm the open is blocked. <br> - If your app allows, attempt to open another file from a different cloud storage location and confirm it is blocked. |

### Validating "Copy To" actions

Skip if you didn't implement ['Copy To' actions].

For simplicity, these tests will assume your app only includes support for copying data to Microsoft Office applications such as Microsoft Word, Excel, etc.
However, you must validate every combination: every supported copy-to location against every place your app allows copying data to.

For these tests, install your app, integrate it with the SDK and log in with a managed account before starting the test.

Additionally:
- Completed all the integration steps from ['Copy To' actions] with an Action Extension for Microsoft Word and build and run the app successfully.
- Set the managed account's policy as:
  - "Send org data to other apps" to "Policy managed apps".

| Scenario | Preconditions | Steps |
| - | - | - |
| Select apps to exempt, None | "Send org data to other apps" policy set to "Policy managed apps" | - Navigate to where your app can copy data to Microsoft Word and launch the sharing option for that data. <br> - Confirm instead of seeing "Copy To Word" as an option, you can see "Open in Word". <br> - Press on "Open in Word" and confirm the document is copied and viewed successfully, given Word is also signed in with the same managed account.|

### Validating Print actions

Skip if you didn't implement [Printing].

For this test, install your app, integrate it with the SDK and log in with a managed account before starting the test.

Additionally:
- Completed all the integration steps from [Printing] and build and run the app successfully.
- Your app already implements alerts/action items to handle the case when printing is not allowed from the APP IT admin. In this test, assuming your app will prompt an alert to end users when printing is blocked.

| Scenario | Steps |
| - | - |
| Printing org data, Block | - Navigate to where your app can view data and launch the sharing option for that data. <br> - Press on "Print". <br> - Confirm a block alert appears and printing is not allowed.|
| Printing org data, Allow | - Navigate to where your app can view data and launch the sharing option for that data. <br> - Press on "Print". <br> - Confirm "Print" view appears and you can select a printer and complete the action successfully.|

### Validating receiving App Configurations

Skip if you didn't [Enable targeted app configuration for your iOS applications].

Intune is responsible for delivering the app configuration policy values to your app; afterwards, your app is responsible for using those values to change behavior or UI inside the app.
Thorough end-to-end testing should cover both components.

To validate that Intune is properly delivering app configuration policy:

1. Configure an app configuration policy, that is targeted to your app, and deployed to your test account.
    - If your app supports app configuration for managed devices, see [application configuration policies for managed iOS Enterprise devices].
    - If your app supports app configuration for managed apps, see [application configuration policies for managed apps].
    - If your app supports both types of app configuration, create both types of policy for testing.
2. Log in to your app with your test account.
3. Navigate through your app to exercise each codepath that calls `IntuneMAMAppConfigManager`'s `appConfigForIdentity`.
    - Logging the results of calls to `appConfigForIdentity` is a simple way to validate which settings are delivered. However, because administrators can enter any data for app configuration settings, be careful not to log any private user data.
4. See [Validate the applied app configuration policy].

Because app configurations are app-specific, only you know how to validate how your app should change behavior or UI for each app configuration setting.

When testing, consider the following:

- Ensuring all scenarios are covered by creating different test app configuration policy with every value your app supports.
- Validating your app's conflict resolution logic by creating multiple test app configuration policies with different values for each setting.

## Next Steps

If you followed this guide in order and have completed all the [Exit Criteria] above, **congratulations**, your app is now fully integrated with the Intune App SDK and can enforce app protection policies!
Please check out other important app participation features such as [Stage 5: Multi-Identity], [Stage 6: App Protection Conditional Access support] and [Stage 7: Web-view features] to integrate these into your app.

App protection is now a core scenario for your app.
Do continue to refer to this guide and the [Appendix] as you continue to develop your app.

<!-- Stage 4 links -->
<!-- internal links -->
[Exit Criteria]:#exit-criteria
[Implement save-as and open-from controls]:#implement-save-as-and-open-from-controls
['Copy To' actions]:#copy-to-actions
[Printing]:#printing
[Enable targeted app configuration for your iOS applications]:#enable-targeted-app-configuration-for-your-ios-applications

[Plan the Integration]:app-sdk-ios-phase1.md
[Enabling multi-identity]:app-sdk-ios-phase5.md
[Stage 5: Multi-Identity]:app-sdk-ios-phase5.md
[Stage 6: App Protection Conditional Access support]:app-sdk-ios-phase6.md
[Stage 7: Web-view features]:app-sdk-ios-phase7.md
[App Protection CA support]:app-sdk-ios-phase6.md
[Appendix]:app-sdk-ios-appendix.md

<!-- external links -->
[application configuration policies for managed iOS Enterprise devices]:/mem/intune-service/apps/app-configuration-policies-use-ios
[application configuration policies for managed apps]:/mem/intune-service/apps/app-configuration-policies-managed-app
[App configuration policies for Microsoft Intune]:/mem/intune-service/apps/app-configuration-policies-overview
[Validate the applied app configuration policy]:/mem/intune-service/apps/app-configuration-policies-overview#validate-the-applied-app-configuration-policy
