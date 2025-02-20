---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide - App participation features
description: Understand App participation features when incorporating Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/31/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
- Android
ms.custom: intune-classic
---

# Intune App SDK for Android - App participation features

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.
> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Plan the Integration].

## Stage 7: App participation features

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
See [Key Decisions for SDK integration] for details.

Previous stages of this guide have already described several app participation features:

- Multi-identity as covered in [Stage 5: Multi-Identity].
- App configuration as covered in [Stage 6: App Configuration].

The rest of this guide describes the remaining set of app participation features:

- Enforce policy restricting saving files to / opening files from local or cloud storage.
- Enforce policy restricting content in notifications.
- Enforce policy protecting backup data.
- Enforce policy restricting screen capture (if your app has custom screen capture code).
- Support App Protection CA.
- Register for notifications from the SDK.
- Apply custom application theming.
- Use trusted certificates from Intune to ensure chain of trust to on-premise endpoints.

## App Participation Feature basics

The [AppPolicy] interface contains many methods that inform your app whether certain actions are allowed.

Most app participation features involve:

- Identifying the right place in your app's code to check if an action is allowed.
- Calling an `AppPolicy` method to check if an action is allowed, based on currently configured policy.
- Depending on the result, either allowing the action to complete, or modifying the app behavior when the action is blocked.

To retrieve an `AppPolicy` instance, use one of the [MAMPolicyManager] methods, such as `getPolicy(final Context context)` or `getPolicyForIdentityOID(final String oid)`.

### Informational methods in AppPolicy

Not every method in `AppPolicy` is tied to an app participation feature.
Some methods are informational, giving your app data on which policies are currently configured, even if those policies are automatically enforced by the SDK.
These methods exist to give your app opportunities to present custom user experience when specific policies are configured.

#### Example: Determine if screenshots are blocked

If your app has a control that lets the user take a screenshot, you might want to disable or hide that control if App Protection Policy has screenshots blocked.

Your app could check this by calling `MAMPolicyManager.getPolicy(currentActivity).getIsScreenCaptureAllowed()`.

## Policy for limiting data transfer between apps and device or cloud storage locations

Many apps allow the end user to save data to or open data from local file storage or cloud storage services.
The Intune App SDK allows IT administrators to protect against data ingress and data leakage by restricting where apps can save data to and open data from.

> [!NOTE]
> **If your app allows saving to personal or cloud locations directly from the app *or* allows for data to be opened directly into the app,
> you must implement this Intune App SDK app participation feature** to enable IT administrators to block this saving / opening.

### Saving to device or cloud storage

The `getIsSaveToLocationAllowedForOID` API lets your app know whether saving to certain locations is allowed for a given identity, based on the configured policy:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowedForOID(
SaveLocation service, String oid);
```

To determine whether your app should implement the `getIsSaveToLocationAllowedForOID` check, determine if your app supports data egress by reviewing the following table:

| `service` Parameter: `SaveLocation` Enum  Value | Use Case | Associated OID |
| - | - | - |
| `ONEDRIVE_FOR_BUSINESS` | The app is saving data to OneDrive. | An OID for an account that is used for both cloud service authentication and Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `SHAREPOINT` | The app is saving data to Sharepoint. | An OID for an account that is used for both cloud service authentication and Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `BOX` | This app is saving data to Box. | An OID for an account that is used for both cloud service authentication and Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `LOCAL` | The app is saving data to an external storage location on the device that is **not** the app's private storage. | The external storage isn't considered a cloud service and so should always be used with a `null` oid parameter. |
| `PHOTO_LIBRARY` | The app is saving data to Android local photo storage. | The Android local photo storage isn't considered a cloud service and so should always be used with a `null` oid parameter. |
| `ACCOUNT_DOCUMENT` | The app is saving data to a location that is associated with an account within the app and isn't one of the specific cloud locations specified above. *This location should be used to determine if data can be passed between accounts within a multi-identity app.- | An OID for an account that is used for Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `OTHER` | The app is saving data to a location that isn't specified above and doesn't satisfy the criteria for `ACCOUNT_DOCUMENT`. | The `oid` isn't evaluated for this location and so should be `null`. |

Files placed in private app storage that are either necessary for app
operation or downloaded temporarily for display are always allowed; you don't need to check `getIsSaveToLocationAllowedForOID`.
Do check `SaveLocation.LOCAL` for

1. Files saved outside of private app storage.
2. Files downloaded to private app storage that aren't necessary for
   app operation (for example, user deliberately choosing to download to the
   device).

> [!NOTE]
> When checking the save policy, `oid` should be the OID of the account associated with the cloud service being saved **to** (*not* necessarily the same as the account owning the document being saved).

### Opening data from a local or cloud storage location

The `getIsOpenFromLocationAllowedForOID` API lets your app know whether opening from certain locations is allowed for a given identity, based on the configured policy:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsOpenFromLocationAllowedForOID(
OpenLocation location, String oid);
```

To determine whether your app should implement the `getIsOpenFromLocationAllowedForOID` check, determine if your app supports data ingress by reviewing the following table:

| `location` Parameter: `OpenLocation` Enum Value | Use Case | Associated OID |
| - | - | - |
| `ONEDRIVE_FOR_BUSINESS` | The app is opening data from OneDrive. | An OID for an account that is used for both cloud service authentication and Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `SHAREPOINT` | The app is opening data from Sharepoint. | An OID for an account that is used for both cloud service authentication and Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `CAMERA` | The app is opening data from the camera. | A `null` value, because the device camera isn't a cloud service. |
| `LOCAL` | The app is opening data from an external storage location on the device that is **not** the app's private storage. | Although the external storage isn't a cloud service location, an `oid` parameter is expected because it indicates ownership. <br>  When opening a file from local storage, the file owner must always be considered, because the file owner's save-as policy may or may not permit other identities to open the file: <br> - **For identity-tagged files,** `oid` should be the file owner's identity. <br> - **For files without an identity tag,** `oid` should be `null`. |
| `PHOTO_LIBRARY` | The app is opening data from Android photo local storage. | The Android local photo storage isn't considered a cloud service and so should always be used with a `null` oid parameter. |
| `ACCOUNT_DOCUMENT` | The app is opening data from a location that is associated with an account within the app and isn't one of the specific cloud locations specified above. *This location should be used to determine if data can be passed between accounts within a multi-identity app.- | An OID for an account that is used for Microsoft Entra authentication. If such an account doesn't exist or the OID isn't known use `null`. |
| `OTHER` | The app is opening data from a location that isn't specified above and doesn't satisfy the criteria for `ACCOUNT_DOCUMENT`. | The `oid` isn't evaluated for this location and so should be `null`. |

> [!NOTE]
> When checking the open policy, `oid` should be the OID of the account associated with the file or cloud service being opened **from** (*not* necessarily the same as the account who is opening the document).

> [!TIP]
> For convenience, the SDK provides the method `AppPolicy.isOpenFromLocalStorageAllowed` that takes a `File` parameter for a file in local storage.
> It terms of enforcing policy, is functionally identical to calling `AppPolicy.getIsOpenFromLocationAllowedForOID(OpenLocation.LOCAL, oid)` except it handles parsing the file owner's `oid` from the `File`.

### Sharing blocked dialog

The SDK provides a dialog to notify the user that a data transfer action was blocked by MAM policy.

The dialog should be displayed to the user whenever the `getIsSaveToLocationAllowedForOID` or `getIsOpenFromLocationAllowedForOID` API call results in the save/open action being blocked.
The dialog displays a generic message and will return to the calling `Activity` when dismissed.

To display the dialog, add the following code:

``` java
MAMUIHelper.showSharingBlockedDialog(currentActivity)
```

### Allow for file sharing

If saving to public storage locations isn't allowed, your app should still allow for the user to view files by downloading them to [app private storage] and then opening them with the system chooser.

## Policy for restricting content inside notifications

For single-identity apps, the Intune App SDK's default behavior will attempt to block *all* notifications when App Protection Policy restricts notifications.

The SDK's default behavior is limited.
The SDK can't automatically honor the "Block org data" value, which is intended to remove only managed content from notifications.
For multi-identity apps, the SDK can't determine which notifications contain managed content.

If your app displays notifications, and it is either multi-identity and/or it wishes to honor the "Block org data" value, it must check the notification restriction policy for the account associated with the notification before showing the notification.

To determine if the policy is enforced, make the following call:

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentityOID(notificationIdentityOid).getNotificationRestriction();
```

The returned `NotificationRestriction` enum has the following values:

| `NotificationRestriction` Enum | Expected App Behavior  |
| - | - |
| `BLOCKED` | The app *must not* show any notifications for the account associated with this policy. For *single-identity* apps, the Intune App SDK will block all notifications automatically, and no additional code is required. |
| `BLOCK_ORG_DATA` | The app must show a modified notification that doesn't contain organization data. |
| `UNRESTRICTED` | The app should show all notifications. |

If your app doesn't properly invoke `getNotificationRestriction`, the MAM SDK will make a best effort to restrict notifications automatically *for single-identity apps only*.

In this case, `BLOCK_ORG_DATA` is treated the same as `BLOCKED` and the notification won't be shown at all.

For more fine-grained control, check the value of `getNotificationRestriction` and modify app notifications appropriately.

## Policy for protecting backup data

The Intune App SDK can block data upload to Android's built-in backup and restore feature.
To learn more about backup and restore in Android, see the [Android API guide] and the changes introduced in Android S / 12 here: [Change to backup and restore].

### Auto Backup for Apps

Beginning with Android M, Android began offering [automatic full backups] to Google Drive for apps, regardless of the app's target API.

Intune allows you to utilize all the autobackup features available from Android, including the ability to define custom rules in XML, with specific Intune integration guidance to ensure data protection is applied.

### Configuring backup behavior in the app's manifest

By default, `android:allowBackup` is set to **true** as outlined
in [enable and disable backup].

If your app doesn't require full backup and restore functionality,
set `android:allowBackup` to **false**.
*In this case, no further action is necessary and "corporate" data will stay within the app.*

If your app requires full backup and restore functionality,
set `android:allowBackup` to **true**  and perform the following
additional steps:

1. If your app does **not** use its own custom `BackupAgent`, use the default [MAMBackupAgent] to allow for automatic full backups that are Intune policy compliant.
Place the following in the app manifest:

    ```xml
    <application
    ...
      android:fullBackupOnly="true"
      android:backupAgent="com.microsoft.intune.mam.client.app.backup.MAMDefaultBackupAgent"
      ...>
      </application>
    ```

2. **[Optional]** If you implemented an optional custom `BackupAgent`,
you need to make sure to use [MAMBackupAgent] or [MAMBackupAgentHelper].
See the following sections.
Consider switching to using Intune's [MAMDefaultBackupAgent], described in step 1, which provides easy back-up on Android M and above.

3. When you decide which type of full backup your app should receive (unfiltered, filtered, or none), you'll need to set the attribute `android:fullBackupContent` to true, false, or an XML resource in your app.

4. Then, you ***must*** copy the value for `android:fullBackupContent`
into the `com.microsoft.intune.mam.FullBackupContent` metadata tag
and for apps that support the new XML configuration format added in API 31, into the `com.microsoft.intune.mam.DataExtractionRules` metadata tag.

    - **Example 1**: If you want your app to have full backups without exclusions, you must set the attributes and metadata tags
    to **true**:

      ```xml
      <application
        ...
        android:fullBackupContent="true"
        ...>
      </application>
      ...
      <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="true" />
      <meta-data android:name="com.microsoft.intune.mam.DataExtractionRules" android:value="true" />
      ```

    - **Example 2**: If you want your app to use its custom
    `BackupAgent` and opt out of full, Intune policy compliant,
    automatic backups, you must set the attributes and metadata tags
    to **false**:

      ```xml
      <application
        ...
        android:fullBackupContent="false"
        ...>
      </application>
      ...
      <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="false" />
      <meta-data android:name="com.microsoft.intune.mam.DataExtractionRules" android:value="false" />
      ```

    - **Example 3**: If you want your app to have full backups according to your custom rules
    defined in an XML file, set the attribute and metadata tag to the same XML resource:

      ```xml
      <application
        ...
        android:fullBackupContent="@xml/my_full_backup_content_scheme"
        android:dataExtractionRules="@xml/my_data_extraction_rules_scheme"
        ...>
      </application>
      ...
      <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:resource="@xml/my_full_backup_content_scheme" />
      <meta-data android:name="com.microsoft.intune.mam.DataExtractionRules" android:resource="@xml/my_data_extraction_rules_scheme" />
      ```

### Key/Value Backup

The [Key/Value Backup] option is available to all APIs 8+ and uploads app data to the [Android Backup Service].
The amount of data per app is limited to 5 MB.
If you use Key/Value Backup, you must use a [BackupAgentHelper] or a [BackupAgent].

### BackupAgentHelper

[BackupAgentHelper] is easier to implement than [BackupAgent] both in terms of native Android functionality and Intune MAM integration
BackupAgentHelper allows the developer to register entire files and shared preferences to a `FileBackupHelper` and `SharedPreferencesBackupHelper` (respectively) which are then added to the BackupAgentHelper upon creation.
Follow the steps below to use a BackupAgentHelper with Intune MAM:

1. To utilize multi-identity backup with a `BackupAgentHelper`, follow the Android guide to [Extending BackupAgentHelper].

2. Have your class extend the MAM equivalent of BackupAgentHelper, FileBackupHelper, and SharedPreferencesBackupHelper.

| Android class | MAM equivalent |
| - | - |
| BackupAgentHelper | [MAMBackupAgentHelper] |
| FileBackupHelper | [MAMFileBackupHelper] |
| SharedPreferencesBackupHelper | [MAMSharedPreferencesBackupHelper] |

Following these guidelines will lead to a successful multi-identity backup and restore.

### BackupAgent

A BackupAgent allows you to be much more explicit about what data is backed up.
Because the developer is fairly responsible for the implementation, there are more steps required to ensure appropriate data protection from Intune.
Since most of the work is pushed onto you, the developer, Intune integration is slightly more involved.

**Integrate MAM:**

1. Carefully read the Android guide for [Key/Value Backup] and specifically [Extending BackupAgent] to ensure your BackupAgent implementation follows Android guidelines.

2. Have your class extend [MAMBackupAgent].

**Multi-identity Backup:**

1. Before beginning your backup, check that the files or data buffers you plan to back up are indeed **permitted by the IT administrator to be backed up** in multi-identity scenarios.
Use `isBackupAllowed` in [MAMFileProtectionManager] and [MAMDataProtectionManager] to determine this.
If the file or data buffer isn't allowed to be backed up, then you shouldn't include it in your backup.

2. At some point during your backup, if you want to back up the identities for the files you checked in step 1, you must call `backupMAMFileIdentity(BackupDataOutput data, File … files)` with the files from which you plan to extract data.
This will automatically create new backup entities and write them to the `BackupDataOutput` for you.
These entities will be automatically consumed upon restore.

**Multi-identity Restore:**
The Data Backup guide specifies a general algorithm for restoring your application’s data and provides a code sample in the [Extending BackupAgent] section.
In order to have a successful multi-identity restore, you must follow the general structure provided in this code sample with special attention to the following:

1. You must utilize a `while(data.readNextHeader())`* loop to go through the backup entities.

2. You must call `data.skipEntityData()` *if `data.getKey()`* doesn't match the key you wrote in `onBackup`.
Without performing this step, your restores may not succeed.

3. Avoid returning while consuming backup entities in the `while(data.readNextHeader())`* construct, as the entities we automatically write will be lost.

- Where `data` is the local variable name for the [MAMBackupDataInput] that is passed to your app upon restore.

## Custom Screen Capture Restrictions

If your app contains a custom screen capture feature that bypasses Android's `Window`-level `FLAG_SECURE` restriction, you must check screen capture policy before allowing full access to the feature.
For example, if your app uses a custom rendering engine to render the current view to a PNG file, you must first check
`AppPolicy.getIsScreenCaptureAllowed()`.

>[!NOTE]
> If your app does not contain any custom or third-party screen capture features, you are not required to take any action to restrict screen captures.
> Screen capture policy is automatically enforced at the `Window` level for all MAM integrated apps.
> Any attempts by the OS or another app to capture a `Window` in your app will be blocked as required.
> For example, if a user attempts to capture your app's screen through Android's built-in screenshot or screen recording features, the capture will be automatically restricted without participation from your app.

## Support App Protection CA

[App Protection CA] (Conditional Access), also known as app-based CA, restricts access to resources until your application is managed by Intune App Protection Policies.
Microsoft Entra ID enforces this by requiring the app to be enrolled and managed by APP before granting a token to access a CA protected resource.

> [!NOTE]
> Support for App Protection CA requires version 1.0.0 (or greater) of the MSAL library.

### Handle non-compliance with MSAL

When acquiring a token for an account, the MSAL library may return or throw an `MsalIntuneAppProtectionPolicyRequiredException` to indicate non-compliance with app protection policy management.
Additional parameters can be extracted from the exception for use in remediating compliance (see [MAMComplianceManager]).
Once the remediation is successful, the app can reattempt the token acquisition through MSAL.

### MAMComplianceManager

The [MAMComplianceManager] interface is used when the policy-required error is received from MSAL.
It contains the [remediateCompliance] method that should be called to attempt to put the app into a compliant state.
A reference to the `MAMComplianceManager` can be obtained as follows:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

The `MAMComplianceManager` instance returned is guaranteed not to be `null`.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

The `remediateCompliance()` method is called to attempt to put the app under management to satisfy the conditions for Microsoft Entra ID to grant the requested token.
The first four parameters can be extracted from the exception received by the MSAL `AuthenticationCallback.onError()` method (see code sample below).
The final parameter is a boolean which controls whether a UX is shown during the compliance attempt.

`remediateCompliance` displays a simple blocking progress dialog so apps don't need to show customized UX during this operation.
This dialog will only be displayed while the compliance remediation is in progress; it will not display the final result.
Your app can register a receiver for the `COMPLIANCE_STATUS` notification to handle the success or failure of the compliance remediation attempt.
See [Compliance status notifications] for detail.

`remediateCompliance()` may initiate a MAM enrollment as part of establishing compliance.
The app may receive an enrollment notification if it has registered a notification receiver for enrollment notifications.
The app's registered `MAMServiceAuthenticationCallback` will have its `acquireToken()` method called to get a token for the enrollment.
`acquireToken()` will be called before the app has acquired its own token, so any bookkeeping or account creation tasks that the app does after a successful token acquisition may not have been done yet.
The callback must be able to acquire a token in this case.

If you can't return a token from `acquireToken()`, the compliance remediation attempt will fail.

If you call `updateToken` later with a valid token for the requested resource, the compliance remediation will be retried immediately with the given token.

> [!NOTE]
> Silent token acquisition will still be possible in `acquireToken()` because the user will have already been guided to install the broker and register the device before the `MsalIntuneAppProtectionPolicyRequiredException` exception is received.
> This results in the broker having a valid refresh token in its cache, allowing silent acquisition of the requested token to succeed.

Here's a sample of receiving the policy-required error in the `AuthenticationCallback.onError()` method, and calling the [MAMComplianceManager] to handle the error.

```java
public void onError(@Nullable MsalException exc) {
    if (exc instanceof MsalIntuneAppProtectionPolicyRequiredException) {

        final MsalIntuneAppProtectionPolicyRequiredException policyRequiredException =
            (MsalIntuneAppProtectionPolicyRequiredException) ex;

        final String upn = policyRequiredException.getAccountUpn();
        final String aadId = policyRequiredException.getAccountUserId();
        final String tenantId = policyRequiredException.getTenantId();
        final String authority = policyRequiredException.getAuthorityURL();

        MAMComplianceManager complianceManager = MAMComponents.get(MAMComplianceManager.class);
        complianceManager.remediateCompliance(upn, aadId, tenantId, authority, showUX);
    }
}
```

### Compliance status notifications

If the app registers for notifications of type `COMPLIANCE_STATUS`, a `MAMComplianceNotification` will be sent in order to inform the app of the final status of the compliance remediation attempt.
See [Register for notifications from the SDK] for detail on registering.

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

The `getComplianceStatus()` method returns the result of the compliance remediation attempt as a value from the [MAMCAComplianceStatus] enum.

| Status code | Explanation |
| - | - |
| `UNKNOWN` | Status is unknown. This could indicate an unanticipated failure reason. Additional information may be found in the Company Portal logs. |
| `COMPLIANT` | Compliance remediation succeeded and the app is now compliant with policy. The MSAL token acquisition should be retried. |
| `NOT_COMPLIANT` | The attempt to remediate compliance failed.  The app isn't compliant and MSAL token acquisition shouldn't be retried until the error condition is corrected.  Additional error information is sent with the MAMComplianceNotification. |
| `SERVICE_FAILURE` | There was a failure while attempting to retrieve compliance data from the Intune Service. Additional information may be found in the Company Portal logs. |
| `NETWORK_FAILURE` | There was an error connecting to the Intune Service. The app should try its token acquisition again when the network connection is restored. |
| `CLIENT_ERROR` | The attempt to remediate compliance failed for some reason related to the client.  For example, no token or wrong user. Additional error information is sent with the MAMComplianceNotification. |
| `PENDING` | The attempt to remediate compliance failed because the status response hadn't yet been received from the service when the time limit was exceeded. The app should try its token acquisition again later. |
| `COMPANY_PORTAL_REQUIRED` | The Company Portal must be installed on the device in order for compliance remediation to succeed.  If the Company Portal is already installed on the device, the app needs to be restarted.  In this case, a dialog will be shown asking the user to restart the app. |

If the compliance status is `MAMCAComplianceStatus.COMPLIANT`, the app should reinitiate its original token acquisition (for its own resource).

If the compliance remediation attempt failed, the `getComplianceErrorTitle()` and `getComplianceErrorMessage()` methods will return localized strings that the app can display to the end user if it chooses.
Most of the error cases aren't remediable by the app, so for the general case it may be best to fail account creation or login and allow the user to try again later.

If a failure is persistent, the Company Portal logs may help determine the cause.  The end user can submit the logs. For more information, see [Upload and email logs](../user-help/send-logs-to-your-it-admin-by-email-android.md).

Here's an example of registering a receiver using an anonymous class to implement the MAMNotificationReceiver interface:

```java
final MAMNotificationReceiverRegistry notificationRegistry = MAMComponents.get(MAMNotificationReceiverRegistry.class);
// create a receiver
final MAMNotificationReceiver receiver = new MAMNotificationReceiver() {
    public boolean onReceive(MAMNotification notification) {
        if (notification.getType() == MAMNotificationType.COMPLIANCE_STATUS) {
            MAMComplianceNotification complianceNotification = (MAMComplianceNotification) notification;
            
            // take appropriate action based on complianceNotification.getComplianceStatus()
            
            // unregister this receiver if no longer needed
            notificationRegistry.unregisterReceiver(this, MAMNotificationType.COMPLIANCE_STATUS);
        }
        return true;
    }
};
// register the receiver
notificationRegistry.registerReceiver(receiver, MAMNotificationType.COMPLIANCE_STATUS);
```

> [!NOTE]
> The notification receiver must be registered before calling `remediateCompliance()` to avoid a race condition that could result in the notification being missed.

### Declaring support for App Protection CA

Once your app is ready to handle App CA remediation, you can tell Microsoft Identity your app is App CA ready.
To do this in your MSAL application, build your Public Client using the Client Capabilities of "protapp"

```java
{
      "client_id" : "[YOUR_CLIENT_ID]",
      "authorization_user_agent" : "DEFAULT",
      "redirect_uri" : "[YOUR_REDIRECT_URI]",
      "multiple_clouds_supported":true,
      "broker_redirect_uri_registered": true,
      "account_mode": "MULTIPLE",
      "client_capabilities": "protapp",
      "authorities" : [
        {
          "type": "AAD",
          "audience": {
            "type": "AzureADandPersonalMicrosoftAccount"
          }
        }
      ]
    }
```

Once you've completed the above, proceed to [Validating App Protection CA] below.

### Implementation Notes

> [!NOTE]
> The app's `MAMServiceAuthenticationCallback.acquireToken()` method should pass *false* for
> `forceRefresh` flag to `acquireTokenSilentAsync()`.
>
>  ```java
>  AcquireTokenSilentParameters acquireTokenSilentParameters =
>          builder.withScopes(Arrays.asList(scopes))
>                 .forceRefresh(false)
>                 .build();
>
> acquireTokenSilentAsync(acquireTokenSilentParameters);
> ```

> [!NOTE]
> If you want to show a custom blocking UX during the remediation attempt, you should pass *false* for the showUX parameter to `remediateCompliance()`.
> You must ensure that you show your UX and register your notification listener first before calling `remediateCompliance()`.
> This will prevent a race condition where the notification could be missed if `remediateCompliance()` fails very quickly.
> For example, the `onCreate()` or `onMAMCreate()` method of an Activity subclass is the ideal place to register the notification listener and then call `remediateCompliance()`.
> The parameters for `remediateCompliance()` can be passed to your UX as Intent extras.
> When the compliance status notification is received, you can display the result or simply finish the activity.

> [!NOTE]
> `remediateCompliance()` will register the account and attempt enrollment.  Once the main token is acquired, calling `registerAccountForMAM()` is not necessary, but there is no harm in doing so.
> On the other hand, if the app fails to acquire its token and wishes to remove the user account, it must call `unregisterAccountForMAM()` to remove the account and prevent background enrollment retries.

## Register for notifications from the SDK

The Intune App SDK guide has already discussed several scenarios where your app may be required to register for notifications from the SDK, such as:

- Multi-identity apps handling `WRONG_USER` (see [Managed vs Unmanaged Identities])
- Multi-identity apps handling `MANAGEMENT_REMOVED` (see [Data Buffer Protection]).
- Multi-identity apps handling `WIPE_USER_DATA` or `WIPE_USER_AUXILIARY_DATA` (see [Selective Wipe]).
- Apps that implement app configuration handling `REFRESH_APP_CONFIG` (see [Retrieving app configuration from the SDK]).

This section describes every type of notification the SDK can send, when and why your application would want to listen for it, and how to implement a notification receiver.

### Types of notifications

All SDK notifications implement the [MAMNotification] interface, which has a single function, `getType()`, returning a [MAMNotificationType] enum.

Most notifications are [MAMUserNotification]s, which provide information specific to a single identity. The identity's OID can be retrieved via the `getUserOid()` function, and the identity's UPN can be retrieved via `getUserIdentity()`.

[MAMEnrollmentNotification] and [MAMComplianceNotification] further extend `MAMUserNotification`, which contain results for attempts to enroll a user/device with the MAM Service and result for attempting to remediate compliance for App Protection CA, respectively.

| Notification type | Notification class | Reason for notification | Applicability | Tips for handling | Thread info |
| - | - | - | - | - | - |
| `COMPLIANCE_STATUS` | `MAMComplianceNotification` | Returns the result of a compliance remediation attempt. | Apps that implement App Protection CA must handle this. | - | Nondeterministic |
| `MAM_ENROLLMENT_RESULT` | `MAMEnrollmentNotification` | Returns the result of an enrollment attempt. | All apps will receive this. | - | Nondeterministic |
| `MANAGEMENT_REMOVED` | `MAMUserNotification` | App is about to become unmanaged. | Apps that utilize `MAMDataProtectionManager` must handle this. | See [MANAGEMENT_REMOVED] below. | Never on UI thread |
| `REFRESH_APP_CONFIG` | `MAMUserNotification` | App config values may have changed. | Apps that implement app configuration and cache app configuration data must handle this. | Apps must invalidate and update any cached app configuration data. | Nondeterministic |
| `REFRESH_POLICY` | `MAMUserNotification` | App protection policy may have changed. | Apps that cache app protection policy must handle this. | Apps must invalidate and update any cached app protection policy data. | Nondeterministic |
| `WIPE_USER_DATA` | `MAMUserNotification` | Wipe is about to occur(*). | Apps that utilize `MAMDataProtectionManager` must handle this **or** `WIPE_USER_AUXILIARY_DATA`. | See [Selective Wipe]. | Never on UI thread |
| `WIPE_USER_AUXILIARY_DATA` | `MAMUserNotification` | Wipe is about to occur(*). | Only multi-identity apps will receive this. <br> Apps that utilize `MAMDataProtectionManager` must handle this **or** `WIPE_USER_DATA`.  | See [Selective Wipe]. | Never on UI thread |
| `WIPE_COMPLETED` | `MAMUserNotification` | Wipe has completed. | Always optional. | Delivered after `WIPE_USER_DATA` or `WIPE_USER_AUXILIARY_DATA`. *If the app reports a failure from its handler for `WIPE_USER_DATA` or `WIPE_USER_AUXILIARY_DATA`, this notification won't be sent.- | Never on UI thread |

(*) Wipes may occur for many reasons, for example:

- Your app called [unregisterAccountForMAM].
- An IT admin initiated a remote wipe.
- Admin-required Conditional Access policies weren't satisfied.

> [!WARNING]
> An app should never register for both the `WIPE_USER_DATA` and `WIPE_USER_AUXILIARY_DATA` notifications.

### MANAGEMENT_REMOVED

The `MANAGEMENT_REMOVED` notification informs that app that a previously policy-managed account is about to become unmanaged.
Once the account is unmanaged, the app will no longer be able to read that account's encrypted files, read the account's data encrypted with `MAMDataProtectionManager`, interact with the encrypted clipboard, or otherwise participate in the managed-app ecosystem.

This doesn't require wiping user data or signing out the user (if a wipe were required, a `WIPE_USER_DATA` notification would be sent).
Many apps may not need to handle this notification, but apps which use `MAMDataProtectionManager` must handle this.
See [Data Buffer Protection] for details.

When the SDK calls the app's `MANAGEMENT_REMOVED` receiver, the following will be true:

- The SDK has already decrypted previously encrypted files (but not protected data buffers) belonging to the app.
Files in public locations on the sdcard that don't directly belong to the app (for example, the Documents or Download folders) aren't decrypted.

- New files or protected data buffers created by the receiver method (or any other code running after the receiver starts) won't be encrypted.

- The app still has access to encryption keys, so operations such as decrypting data buffers will succeed.

Once your app's receiver returns, it will no longer have access to encryption keys.

### Implementing MAMNotificationReceiver

To register for notifications from the SDK, your app must create a [MAMNotificationReceiver] and register it with [MAMNotificationReceiverRegistry].

To register the receiver, call `registerReceiver` with your receiver and the desired notification type in your `Application.onCreate` method:

```java
@Override
public void onCreate() {
  super.onCreate();
  MAMComponents.get(MAMNotificationReceiverRegistry.class)
    .registerReceiver(
      new ToastNotificationReceiver(),
      MAMNotificationType.WIPE_USER_DATA);
}
```

Your app's [MAMNotificationReceiver] implementation must include the `onReceive(MAMNotification notification)` method.
This method will be invoked individually for each notification received, and it must return a `boolean`.
Generally, this method should always return `true`, unless your application encountered a failure responding to a notification.

As with other types of Android receivers, your application has flexibility with handling notifications:

- It may create distinct [MAMNotificationReceiver] implementations for distinct notification types (described below). In this case, make sure to register each implementation and each notification type separately.
- It may use a single [MAMNotificationReceiver] implementation that contains logic for responding to multiple distinct notification types. In this case, it must be registered for each type of notification it can respond to.
- It may create multiple [MAMNotificationReceiver] implementations that each respond to the same notification type. In this case, both must be registered to the same notification type.

> [!TIP]
> It is safe to block in `MAMNotificationReceiver.onReceive` because its callback is not running on the UI thread.

## Custom Themes

A custom theme can be provided to the Intune App SDK; this custom theme will be applied to all SDK screens and dialogs.
If a theme isn't provided, the default SDK theme will be used.

### Providing a Custom Theme

To provide a theme, you need to add the following line of code in the `Application.onMAMCreate` method:

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

In the above example, you need to replace `R.style.AppTheme` with the style theme that you want the SDK to apply.

## Trusted Root Certificates Management

If your application requires SSL/TLS certificates issued by an on-premise or private certificate authority to provide secure access to internal websites and applications, the Intune App SDK has added support for certificate trust management using the API classes [MAMTrustedRootCertsManager] and [MAMCertTrustWebViewClient].

> [!NOTE]
> [MAMCertTrustWebViewClient] supports Android 10 or higher.

Trusted Root Certificates Management provides support for:

- SSLContext
- SSLSocketFactory
- TrustManager
- WebView

### Requirements

- Trusted Root Certificates Management requires a Microsoft Tunnel for Mobile Application Management license. To learn more visit: [Microsoft Tunnel with Mobile Application Management].
- Configure Intune App Configuration Policies to deliver trusted root certificates to line of business apps and Edge on Android. See: [Use Microsoft Tunnel VPN with Android devices that don't enroll with Microsoft Intune].

> [!NOTE]
> Trusted Root Certificates Management can be used independently of Microsoft Tunnel VPN Gateway, however you must license Microsoft MAM Tunnel for use.

### Using Trusted Root Certificates from Intune to Establish Trust Anchors

Trusted Root Certificates Management allows your app to use trusted root certificates from Intune in combination with certificates from the device.

The API classes [MAMTrustedRootCertsManager] and [MAMCertTrustWebViewClient] use the Intune trusted root certificates delivered via App Configuration Policy as a fallback option if the device’s trusted root certificate stores do not contain the required trusted root certificates to establish a secure connection to on-premise resources. This way, the app can use both device and Intune certificates to verify secure connections and communication with trusted sources.

To enhance its network security settings, an app can use the Network Security Configuration XML file. Trusted Root Certificates Management respects this extra security by verifying if the app’s Network Security Configuration XML has any of these features:

- Custom trust anchors with additional CAs such as self-signed certificates.
- Domain-specific rules for limiting trusted CAs.
- Pin sets for certificates for specific domains.

> [!NOTE]
> Learn more about Android Network Security Configuration at: [Network security configuration]

If any of these applies to a domain that is being checked for trust, then Trusted Root Certificates Management will skip the custom trust checks for this domain and let only the platform’s default trust managers do the checks.

#### Class MAMTrustedRootCertsManager

This class provides the following APIs:

- `createSSLContextForOID(String oid, String protocol)`: creates an `SSLContext` object that uses trusted root certificates for the specified identity and the specified SSL/TLS protocol. The returned `SSLContext` object from this class is already initialized correctly with `X509TrustManager` objects that use the combined trusted root certificates from the device and the MAM service.
- `createSSLSocketFactoryForOID(String oid, String protocol)`: creates an `SSLSocketFactory` object that uses trusted root certificates for the specified identity and the specified SSL/TLS protocol. The returned `SSLSocketFactory` object is referenced from the same `SSLContext` object in this class.
- `createX509TrustManagersForOID(String oid)`: creates an array of `X509TrustManager` objects that use the combined trusted root certificates from the device and the MAM service for the specified identity.

> [!NOTE]
> The `oid` parameter is expected to be the Microsoft Entra User ID (OID) for a particular user running the application. In the case the user identifier is unknown beforehand, a value of null can be passed in and MAM will attempt to discover the correct identity from the thread or process in which these APIs are invoked. The identity must be set on the process or thread correctly for MAM to discover the identity. To learn more about setting the active identity on a process or thread visit: [Stage 5: Multi-Identity]
> [!NOTE]
> When the `protocol` parameter is not provided, the highest supported SSL/TLS protocol on the platform is used.

Here are some examples of using this class.

##### Example Using HttpsUrlConnection

```java
// Create an SSL socket factory using supplying the optional parameters identity and protocol
SSLSocketFactory sslSocketFactory = MAMTrustedRootCertsManager.createSSLSocketFactoryForOID(oid, "TLSv1.3");

// Create a URL object for the desired endpoint
URL url = new URL("https://example.com");

// Open a connection using the URL object
HttpsURLConnection httpsURLConnection = (HttpsURLConnection) url.openConnection();

// Set the SSL socket factory for the connection
httpsURLConnection.setSSLSocketFactory(sslSocketFactory);

// Perform any other configuration or operations on the connection as needed
...
```

##### Example Using OkHttpClient

```java
// Get the TrustManager instances for an identity from the SDK
TrustManager[] trustManagers = MAMTrustedRootCertsManager.createX509TrustManagersForOID(oid);

// Get SSLContext from the platform
SSLContext sslContext = SSLContext.getInstance("TLSv1.3");

// Initialize the SSLContext with the trust managers from the Intune App SDK
sslContext.init(null, trustManagers, null);  

// Create an OkHttpClient.Builder object
OkHttpClient.Builder builder = new OkHttpClient.Builder();

// Set the SSLSocketFactory and the trust managers from the SDK
builder.sslSocketFactory(sslContext.socketFactory, trustManagers[0] as X509TrustManager).build();

// Build an OkHttpClient object from the builder
OkHttpClient okHttpClient = builder.build();

// Create a Request object for the desired endpoint
Request request = new Request.Builder().url("https://example.com").build();

// Execute the request using the OkHttpClient object and get a Response object
Response response = okHttpClient.newCall(request).execute();

// Perform any other operations on the response as needed
...
```

#### Class MAMCertTrustWebViewClient

This class provides a custom implementation of the Android class `android.webkit.WebViewClient` that provides a way to handle the SSL error `android.net.http.SslError.SSL_UNTRUSTED` in `WebView`. In handling the error, the class uses trusted root certificates that are configured in Intune and received from the MAM service to check the trustworthiness of the host from the target URL that generated the SSL error in `WebView`. If the custom implementation does not handle the SSL error, the default behavior inherited from the superclass will be invoked. When using this class, you should create an instance of it and then call `WebView.setWebViewClient(WebViewClient)` to register it with a `WebView` instance.

Here is an example of using this class.

##### Example Using WebView

```java
// Get the MAM implementation of WebViewClient from the Intune App SDK
MAMCertTrustWebViewClient mamCertTrustWebViewClient = new MAMCertTrustWebViewClient();

// Set the MAM WebViewClient from the SDK as the current handler on the instance of WebView
webView.setWebViewClient(mamCertTrustWebViewClient);

// Perform any other operations on WebView
...
```

## Exit Criteria

Refer to [Quickly testing with changing policy] for ease of testing.

### Validating save to / open from restrictions

Skip if you didn't implement [Policy for limiting data transfer between apps and device or cloud storage locations].

Refamiliarize yourself with every scenario where your app can save data to cloud services or local data and open data from cloud services or local data.

For simplicity, these tests will assume your app only includes support for saving to and opening data from OneDrive for Business from a single location within the app.
However, you must validate every combination: every supported save location against every place your app allows saving data, and every supported open location against every place your app allows opening data.

For these tests, install your app and the Intune Company Portal; log in with a managed account before starting the test.
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

### Validating notification restrictions

Skip if you didn't implement [Policy for restricting content inside notifications].

As far as App Protection Policy is concerned, your application may fire three different types of notifications:

 1. Notifications that don't contain any account data.
 2. Notifications that contain data belonging to a managed account.
 3. Notifications that contain data belonging to an unmanaged account.

If your application is single-identity, only the first 2 are relevant, since no protections will be applied if the sole account is unmanaged.

Notification restrictions can be validated by triggering all three types of notifications with different policy values configured.

For these tests, install your app and the Intune Company Portal; log in with a managed account before starting the test.
If your app is multi-identity, also log in to your app with an unmanaged account.

| Scenario | Preconditions | Steps |
| - | - | - |
| Full content blocked | "Org data notifications" policy set to "Block" | - Trigger your app to fire a notification with no account data. <br> - Confirm this notification doesn't display any content. <br> - Trigger your app to fire a notification with the managed account's data. <br> - Confirm this notification doesn't display any content. <br> - Trigger your app to fire a notification with the unmanaged account's data. <br> - Confirm this notification doesn't display any content. |
| Partial content blocked | "Org data notifications" policy set to "Block org data" | - Trigger your app to fire a notification with no account data. <br> - Confirm this notification displays its full content. <br> - Trigger your app to fire a notification with the managed account's data. <br> - Confirm this notification redacts the managed account's content. <br> - Trigger your app to fire a notification with the unmanaged account's data. <br> - Confirm this notification displays its full content. |
| No content blocked | "Org data notifications" policy set to "Allow" |

### Validating data backup and restore

Skip if you didn't implement [Policy for protecting backup data].

Re-familiarize yourself with the content (files and/or key-value pairs) your app has configured for backup.
You should validate that *only* expected content is part of the restore.
Extra content in the restore can lead to a data leak.

For these tests, install your app and the Intune Company Portal; log in with a managed account before starting the test.
If your app is multi-identity, also log in to your app with an unmanaged account.

Follow [Android's official instructions for testing backup].
These instructions differ for autobackup and key/value backups, so follow closely.

### Validating custom screen capture against policy

Skip if you didn't implement [Custom Screen Capture Restrictions].

If your application has a feature that bypasses Android's `Window`-level `FLAG_SECURE`, validate that this feature is blocked by app protection policy screen capture restrictions.

For these tests, install your app and the Intune Company Portal; log in with a managed account before starting the test.

| Scenario | Preconditions | Steps |
| - | - | - |
| Screen capture blocked | "Screen capture and Google Assistant" policy set to "Block" | - Navigate to the location in your app that leverages your custom FLAG_SECURE code. <br> - Attempt to utilize that feature. <br> - Confirm the feature is blocked. |
| Screen capture allowed | "Screen capture and Google Assistant" policy set to "Allow" | - Navigate to the location in your app that leverages your custom FLAG_SECURE code. <br> - Attempt to utilize that feature. <br> - Confirm the feature is allowed. |

### Validating App Protection CA

Skip if you didn't implement [Support App Protection CA].

In addition to the typical validation steps of creating and assigning app protection policy to your app and test account, you must also create and assign an App Protection Conditional Access policy to your test account.
See [Set up app-based Conditional Access policies with Intune] for details.

Test steps:

 1. Uninstall Microsoft Authenticator and Intune Company Portal before starting this test.
 2. Install your app.
 3. Log in to your app with your test account that is targeted with both app protection policy and app-based CA policy.
 4. Confirm your app prompts you to install the Company Portal.
 5. Log in again.
 6. Confirm your app prompts you to register your device. Follow the prompts. *If your app doesn't prompt for registration here, confirm that your test device had uninstalled other SDK-enabled apps, Company Portal, and Authenticator first. If this still doesn't prompt, revisit the implementation instructions above.*
 7. Confirm you're able to access all app data after registering.

### Validating notification receivers

Skip if you didn't implement [Register for notifications from the SDK].

Validation steps depend on the type of notifications your app has registered for. For all types of notifications, do add logging to ensure that your receiver is properly being invoked.

`MAM_ENROLLMENT_RESULT` can be triggered simply by first logging into your application with an account targeted with app protection policy.

`REFRESH_APP_CONFIG` and `REFRESH_POLICY` can be triggered by updating the respective App Configuration Policy and App Protection Policy targeted to your test account and waiting for the SDK to receive updated policy.

> [!TIP]
> See [Quickly testing with changing policy] to speed up this process.

`MANAGEMENT_REMOVED`, `WIPE_USER_DATA`, `WIPE_USER_AUXILIARY_DATA`, `WIPE_COMPLETED` notifications can all be triggered by [issuing a selective wipe] from Microsoft Intune.

### Validating custom themes

Skip if you didn't implement [Custom Themes].

Custom theme support can be validated by inspecting the colors on the SDK's dialogs.
The simplest dialog to check is the MAM PIN screen.

Preconditions:

- Set the managed account's policy as:
  - "PIN for access" to "Required".
- Install your app and the Intune Company Portal.

Test Steps:

 1. Launch your application and log in with the test account.
 2. Confirm the MAM PIN screen appears and is themed based on the custom theme you provided to the SDK.

## Next Steps

If you followed this guide in order and have completed all the [Exit Criteria] above, **congratulations**, your app is now fully integrated with the Intune App SDK and can enforce app protection policies!
If you skipped either of the previous app participation sections, [Stage 5: Multi-Identity] and [Stage 6: App Configuration], and are unsure if your app should support these features, revisit [Key Decisions for SDK integration].

App protection is now a core scenario for your app.
Do continue to refer to this guide and the [Appendix] as you continue to develop your app.

<!-- Stage 7 links -->
<!-- internal links -->
[Policy for limiting data transfer between apps and device or cloud storage locations]:#policy-for-limiting-data-transfer-between-apps-and-device-or-cloud-storage-locations
[Policy for restricting content inside notifications]:#policy-for-restricting-content-inside-notifications
[Policy for protecting backup data]:#policy-for-protecting-backup-data
[Custom Screen Capture Restrictions]:#custom-screen-capture-restrictions
[MAMComplianceManager]:#mamcompliancemanager
[Compliance status notifications]:#compliance-status-notifications
[Support App Protection CA]:#support-app-protection-ca
[Register for notifications from the SDK]:#register-for-notifications-from-the-sdk
[MANAGEMENT_REMOVED]:#management_removed
[Custom Themes]:#custom-themes
[Exit Criteria]:#exit-criteria
[Validating App Protection CA]:#validating-app-protection-ca

<!-- Other SDK Guide Markdown documentation -->
[Plan the Integration]: app-sdk-android-phase1.md
[Key Decisions for SDK integration]:app-sdk-android-phase1.md#key-decisions-for-sdk-integration
[Stage 5: Multi-Identity]:app-sdk-android-phase5.md
[Managed vs Unmanaged Identities]:app-sdk-android-phase5.md#managed-vs-unmanaged-identities
[Data Buffer Protection]:app-sdk-android-phase5.md#data-buffer-protection
[Selective Wipe]:app-sdk-android-phase5.md#selective-wipe
[Stage 6: App Configuration]:app-sdk-android-phase6.md
[Retrieving app configuration from the SDK]:app-sdk-android-phase6.md#retrieving-app-configuration-from-the-sdk
[Appendix]:app-sdk-android-appendix.md
[Quickly testing with changing policy]:app-sdk-android-appendix.md#quickly-testing-with-changing-policy

<!-- Microsoft Learn documentation -->
[App Protection CA]:/mem/intune-service/protect/app-based-conditional-access-intune
[issuing a selective wipe]:/mem/intune-service/apps/apps-selective-wipe
[Set up app-based Conditional Access policies with Intune]:/mem/intune-service/protect/app-based-conditional-access-intune-create
[Microsoft Tunnel with Mobile Application Management]: /mem/intune-service/protect/microsoft-tunnel-mam
[Use Microsoft Tunnel VPN with Android devices that don't enroll with Microsoft Intune]: /mem/intune-service/protect/microsoft-tunnel-mam-android

<!-- 3rd party links -->
[app private storage]:https://developer.android.com/training/data-storage
[Android API guide]:https://developer.android.com/guide/topics/data/backup.html
[Change to backup and restore]:https://developer.android.com/about/versions/12/backup-restore
[automatic full backups]:https://developer.android.com/guide/topics/data/autobackup.html
[enable and disable backup]:https://developer.android.com/guide/topics/data/autobackup#EnablingAutoBackup
[Android Backup Service]:https://developer.android.com/google/backup/index.html
[BackupAgent]: https://developer.android.com/reference/android/app/backup/BackupAgent
[BackupAgentHelper]: https://developer.android.com/reference/android/app/backup/BackupAgentHelper
[Extending BackupAgentHelper]:https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper
[Key/Value Backup]:https://developer.android.com/guide/topics/data/keyvaluebackup.html
[Extending BackupAgent]:https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent
[Android's official instructions for testing backup]:https://developer.android.com/guide/topics/data/testingbackup
[Network security configuration]:https://developer.android.com/training/articles/security-config

<!-- Class links -->
[AppPolicy]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/AppPolicy.html
[MAMBackupAgent]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMBackupAgent.html
[MAMBackupAgentHelper]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMBackupAgentHelper.html
[MAMBackupDataInput]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMBackupDataInput.html
[MAMDataProtectionManager]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMDataProtectionManager.html
[MAMDefaultBackupAgent]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMDefaultBackupAgent.html
[MAMEnrollmentNotification]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/notification/MAMEnrollmentNotification.html
[MAMFileBackupHelper]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMFileBackupHelper.html
[MAMFileProtectionManager]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMFileProtectionManager.html
[MAMNotification]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/notification/MAMNotification.html
[MAMNotificationType]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/notification/MAMNotificationType.html
[MAMComplianceNotification]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/notification/MAMComplianceNotification.html
[MAMNotificationReceiver]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/notification/MAMNotificationReceiver.html
[MAMNotificationReceiverRegistry]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/notification/MAMNotificationReceiverRegistry.html
[MAMPolicyManager]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html
[MAMSharedPreferencesBackupHelper]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMSharedPreferencesBackupHelper.html
[MAMUserNotification]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/notification/MAMUserNotification.html
[MAMTrustedRootCertsManager]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMTrustedRootCertsManager.html
[MAMCertTrustWebViewClient]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMCertTrustWebViewClient.html

<!-- Method links -->
[unregisterAccountForMAM]: https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/MAMEnrollmentManager.html#unregisterAccountForMAM(java.lang.String,%20java.lang.String)

