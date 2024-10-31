---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide - Multi-Identity 
description: Understand Multi-Identity when incorporating Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2023
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

# Intune App SDK for Android - Multi-Identity

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Stage 1: Plan the Integration].

## Stage 5: Multi-Identity

## Stage Goals

- Determine if your application needs multi-identity support.
- Understand how the Intune App SDK perceives identities.
- Refactor your application for identity awareness.
- Add code to inform the SDK of active and changing identities throughout your application.
- Thoroughly test app protection policy enforcement for both managed and unmanaged identities.

### Identity terminology

The terms "user", "account", and "identity" are often used interchangeably.
This guide attempts to differentiate as follows:

- **User**: the human being using the software product. Further differentiated as **end user**, the human using the Android app, and **admin** / **admin user** / **IT admin** / **IT Pro**, the human using the [Microsoft Intune admin center].
- **Account**: the software record belonging to an organization that uniquely identifies a user's entity. A human user can have multiple accounts.
- **Identity**: the set of data that the Intune App SDK uses to uniquely identify an account.

## Background

By default, the Intune App SDK applies policy to your entire application.
After registering an account with app protection policy targeted, the SDK associates every file and every activity with that account's identity and will apply that account's targeted policy universally.

For many developers, this is the desired app protection behavior for their application.
These applications are considered *single-identity*.
By completing the previous stages, your application has successfully integrated as single-identity and can enforce all basic policies.
Apps that are intended to stay single-identity can skip this section and proceed to [Stage 6: App Configuration].

The Intune App SDK can optionally enforce policy on a per-identity level.
If your application already supports multiple accounts logged in simultaneously, and you want to retain this multi-account support with app protection policies, your application is considered *multi-identity*.

> [!TIP]
> If you are unclear if application should support single-identity or multi-identity protections, revisit [Is my application single-identity or multi-identity?]

> [!WARNING]
> Supporting multi-identity is significantly more complex than other app protection features.
> Improperly integrating multi-identity can result in data leaks and other security issues.
> Review this section carefully and plan ample time for testing before proceeding to the next stage.

### "Identity" to the SDK

When an SDK-integrated application registers an account using the [registerAccountForMAM], the SDK saves all of the provided parameters (upn, aadId, tenantId, and authority) as the identity.
However, most of the SDK's identity APIs use the provided OID (also known as Microsoft Entra ID or AAD ID) as the identifier for the identity.
The MAM SDK APIs will return the OID string as the identity and will require the OID string parameter for the identity.
Some methods may also take or return a UPN string, in which case the UPN is for informational purposes only.

Identity parameters are case-insensitive.
Requests to the SDK for an identity may not return the same casing that was used when either registering or setting the identity.

> [!CAUTION]
> For apps using deprecated methods that take or return a UPN string, apps must
> make sure that the identity UPN string passed to various API calls is
> consistent. Passing inconsistent UPN strings may result in data leaks.

### Managed vs Unmanaged Identities

As described in [Registering for App Protection Policy], your application is responsible for informing the SDK when a user logs in.
At the moment of login, the user's account may or may not be targeted with app protection policy.
If the account is targeted with app protection policy, the SDK considers it managed; otherwise, it is unmanaged.

The SDK will enforce policy for identities it considers managed.
The SDK won't enforce policy for identities it considers unmanaged.

Currently, the Intune App SDK only supports a single managed identity per device.
As soon as *any* SDK-integrated application registers a managed identity, all subsequently registered identities, even if they're currently targeted with app protection policies, will be treated as unmanaged.

If a managed identity has already been registered on the device and your app registers another identity that is also targeted with app protection policy, the SDK will return `MAMEnrollmentManager.Result.WRONG_USER` and prompt the end user with options to remediate.
See [Register for notifications from the SDK] for more detail.

> [!NOTE]
> An account that is not targeted with app protection policy at registration time will be considered unmanaged.
> Even if the account is not licensed for or targeted with app protection policy, the SDK will periodically check if this account becomes licensed and targeted at a later time.
> If no other managed identity has been registered, the SDK will start treating this identity as managed once it is targeted with policy.
> The user does not need to log out and log back into this account to make this change.

### The Active Identity

Your application must always keep the SDK informed of the identity that is in current use, otherwise known as the active identity.
If the active identity is managed, the SDK will apply protections.
If the active identity isn't managed, the SDK won't apply protections.

Because the SDK has no application-specific knowledge, it must trust the application to share the correct active identity.

- If the application incorrectly tells the SDK that an unmanaged identity is active when the managed identity is actually in use, the SDK won't apply protections.
This could cause a data leak that places users' data at risk.

- If the application incorrectly tells the SDK that the managed identity is active when an unmanaged identity is actually in use, then the SDK will inappropriately apply protections.
This isn't a data leak, but this can needlessly restrict unmanaged users and put unmanaged users' data at risk of deletion.

If your application displays any user's data, it must only display data that belongs to the active identity.
If your application isn't currently aware of who owns data that is displayed, you may need to refactor your application for greater identity awareness before starting to integrate multi-identity support.

### Organizing App Data by Identity

Whenever your application writes a new file, the SDK associates (also known as "tags") an identity with that file based on the current active thread and process identity.
Alternately, your app can directly call the SDK to manually tag a file with a particular identity (see [Writing Protected Files] for details). The SDK uses this tagged file identity for both file encryption and selective wipe.

If the managed identity is targeted with encryption policy, only files tagged with the managed identity will be encrypted.

If administrator action or configured policy requests that managed data is wiped, only files tagged with the managed identity will be deleted.

The SDK can't associate multiple identities with a single file.
If your app stores data belonging to multiple users in the same file, the SDK's default behavior will result in under-protecting or over-protecting this data.
**You are strongly encouraged to organize your app's data by identity**.

If your app absolutely must store data belonging to different identities in the same file, the SDK provides features for identity-tagging subsets of data within a file.
See [Data Buffer Protection] for details.

## Implementing Multi-Identity

To declare multi-identity support for your app, start by placing the following metadata in AndroidManifest.xml.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### Setting the Active Identity

Your application can set the active identity on the following levels in descending priority:

  1. Thread level
  2. `Context` (generally `Activity`) level
  3. Process level

An identity set at the thread level supersedes an identity set at the `Context` level, which supersedes an identity set at the process level.

An identity set on a `Context` is only used in appropriate associated scenarios.
File IO operations, for example, don't have an associated `Context`.
Most commonly, apps will set the `Context` identity on an `Activity`.
Consider setting the `Context` identity in `Activity.onCreate`.
An app *must not* display data for an identity unless the `Activity` identity is set to that same identity.

In general, the process-level identity is only useful if the app works only with a single identity at a time on all threads.
This isn't typical behavior for apps that support multiple accounts.
You're strongly encouraged to segregate account data and set the active identity on the thread or `Context` levels.

If your app uses the `Application` context to acquire system services, ensure that the thread or process identity has been set, or that you have set the UI identity on your app's `Application` context.

If your app uses a `Service` context to launch intents, uses content resolvers, or leverages other system services, be sure to set the identity on the `Service` context.
Similarly, if your app uses a `JobService` context to perform these actions, be sure to set the identity on the `JobService` context or thread as required by your `JobService` implementation.
For example, if your `JobService` processes jobs for a single identity, consider setting the identity on the `JobService` context.
If your `JobService` processes jobs for multiple identities, consider setting the identity at the thread level.

> [!CAUTION]
> Apps that use `WorkManager` should take special care when setting the identity.
> Specifically, these apps should avoid setting an identity on the `Context` passed in the `Worker` constructor.
> This `Context` instance may be shared among multiple `Worker` instances simultaneously.
> To avoid undefined behavior, apps should instead set a thread identity in `Worker.doWork()` as required by the `Worker` implementation.

> [!NOTE]
> Because the `CLIPBOARD_SERVICE` is used for UI operations, the SDK uses the UI identity of the foreground activity for `ClipboardManager` operations.

The following methods in [MAMPolicyManager] may be used to set the active identity and retrieve the identity values previously set.

```java
public static void setUIPolicyIdentityOID(final Context context, final String oid,
                    final MAMSetUIIdentityCallback mamSetUIIdentityCallback, final EnumSet<IdentitySwitchOption> options);

public static String getUIPolicyIdentityOID(final Context context);

public static MAMIdentitySwitchResult setProcessIdentityOID(final String oid);

public static String getProcessIdentityOID();

public static MAMIdentitySwitchResult setCurrentThreadIdentityOID(final String oid);

public static String getCurrentThreadIdentityOID();

/**
 * Get the current app policy. This does NOT take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use the overload below.
 */
public static AppPolicy getCurrentThreadPolicy();

/**
 * Get the current app policy. This DOES take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use this function.
 */
public static AppPolicy getPolicy(final Context context);


public static AppPolicy getPolicyForIdentityOID(final String oid);

public static boolean getIsIdentityOIDManaged(final String oid);
```

As a convenience, you can also set the identity of an activity directly through a method in [MAMActivity] instead of calling `MAMPolicyManager.setUIPolicyIdentityOID`.
Use following method to do so:

```java
     public final void switchMAMIdentityOID(final String newIdentityOid, final EnumSet<IdentitySwitchOption> options);
```

> [!NOTE]
> If your app has not declared multi-identity support in the manifest, calling these methods to set the identity will not execute any action and, if they return a `MAMIdentitySwitchResult`, will always return `FAILED`.

#### Common Identity Switch Pitfalls

- For calls to `startActivity`, the Intune App SDK assumes that the active identity at the `Context` level is associated with the provided `Intent` parameter.
We strongly recommend setting the `Context` level identity with an `Activity`'s context, not the `Application`'s context.

- Setting the `Context` identity during an Activity's `onCreate` method is recommended.
However, be sure to also cover other entry points like `onNewIntent`.
Otherwise, when the same Activity is reused to display data for both managed and unmanaged identities, policy may be incorrectly applied, leading to either unprotected corporate data or improperly restricted personal data.

#### Identity Switch Results

All the methods used to set the identity report back result values via [MAMIdentitySwitchResult]. There are four values that can be returned:

| Return value | Scenario |
|--            |--        |
| `SUCCEEDED`    | The identity change was successful. |
| `NOT_ALLOWED`  | The identity change isn't allowed. This occurs if an attempt is made to set the UI (`Context`) identity when a different identity is set on the current thread. |
| `CANCELLED`    | The user canceled the identity change, generally by pressing the back button on a PIN or authentication prompt. |
| `FAILED`       | The identity change failed for an unspecified reason.|

The app should verify the [MAMIdentitySwitchResult] is `SUCCEEDED` before displaying or using a managed account's data.

Most methods for setting the active identity return  [MAMIdentitySwitchResult] synchronously.
In the case of setting a `Context` identity via [setUIPolicyIdentityOID], the result is reported asynchronously.
The app may implement a [MAMSetUIIdentityCallback] to receive this result, or may pass null for the callback object.
If a call is made to `setUIPolicyIdentityOID` while the result from a previous call to `setUIPolicyIdentityOID` *on the same `Context`* hasn't yet been delivered, the new callback will supersede the old one and the original callback will never receive a result.

> [!CAUTION]
> If the `Context` provided to [setUIPolicyIdentityOID] is an `Activity`, the SDK does not know if the identity change succeeded until after it performs the admin configured conditional launch checks.
> This may require the user to enter a PIN or corporate credentials.

Currently, process and thread identity switches will always succeed for a multi-identity-enabled app.
The SDK reserves the right to add failure conditions in the future.

The UI identity switch may fail for invalid arguments, if it would conflict with the thread identity, or if the user cancels out of conditional launch requirements (for example, presses the back button on the PIN screen).

The default behavior for a failed UI identity switch on an activity is to finish the activity.
To change this behavior and receive notifications on identity change attempts for an activity, you can override a method in `MAMActivity`.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

If you do override `onSwitchMAMIdentityComplete` (or call the `super` method), you *must* ensure that a managed account's data isn't displayed after a failed identity switch.

> [!NOTE]
> Switching the identity may require recreating the activity.
> In this case, the `onSwitchMAMIdentityComplete` callback will be delivered to the new instance of the activity.

#### Identity, Intents, and IdentitySwitchOptions

In addition to automatically tagging new files with the active identity, the SDK also tags *intents* with the active identity.
By default, the SDK will check the identity on an incoming intent and compare it to the active identity.
If these identities don't match, the SDK typically(*) requests an identity switch (see [Implicit Identity Changes] below for more details).

The SDK also stores this incoming intent identity for later use.
When the app explicitly changes the UI identity, the SDK compares the identity the app is attempting to switch to against the most recent incoming intent identity.
If these identities don't match, the SDK will typically(*) fail the identity switch.

The SDK performs this check because it assumes that the app is still displaying content from the intent that belongs to the identity tagged on the intent.
This assumption protects against the app unintentionally turning protections off when displaying managed data; however this assumption may not be correct to the app's actual behavior.

The optional [IdentitySwitchOption] enums can be passed to the [setUIPolicyIdentityOID] and [switchMAMIdentityOID] APIs to modify the SDK's default behavior.

- **`IGNORE_INTENT`**: when requesting an identity switch at the UI layer, this option informs the SDK to skip comparing the requested identity parameter against the most recently stored intent identity.
This is useful when your app is no longer displaying content belonging to that identity, and the SDK shouldn't block this identity switch.
For example:
  1. Your app is a document viewer. It can render documents passed in from other apps. It also contains a feature where users can switch accounts. Whenever the user uses this account-switch feature, the app navigates to an account-specific landing page with that account's recent documents.
  2. Your app receives an intent to display a document. This intent is tagged with the managed identity.
  3. Your app is switched to the managed identity and displays this document, with protections properly applied.
  4. The user uses the account-switcher to change to their personal account.

  Your app must change the UI identity in step 4.
  In this case, because the app's behavior is to navigate away from the managed account's data (the document in the intent), it should use `IGNORE_INTENT` in the identity switch call.
  This avoids the SDK inappropriately failing this call.

- **`DATA_FROM_INTENT`**: when requesting an identity switch at the UI layer, this option informs the SDK that data from the most recently stored intent identity will continue to be displayed *after the identity switch succeeds*.
As a result, the SDK will fully evaluate receive policy against the previous intent identity to determine if it is allowed to be displayed.
For example:

  1. Your app is a document viewer. It can render documents passed in from other apps. It also contains a feature where users can switch accounts. Unlike the earlier example, whenever the user uses this account-switch feature, the app navigates to a shared page that shows recent documents for *all accounts'*.
  2. Your app receives an intent to display a document. This intent is tagged with the managed identity.
  3. Your app is switched to the managed identity and displays this document, with protections properly applied.
  4. The user uses the account-switcher to change to their personal account.

  Your app must change the UI identity in step 4.
  In this case, because the app's behavior is to continue displaying the managed identity's data (a preview of the document in the intent), it should use `DATA_FROM_INTENT` in the identity switch call.
  This informs the SDK to check the configured app protection policy to determine if it's appropriate for the data to continue to be displayed.

(*) The SDK's default behavior does include special casing that skips this data ingress check if, for example, the intent comes from inside the same app or from the system launcher.

#### Clearing the Active Identity

Your application may have scenarios that are account-agnostic.
Your application may also have scenarios for local unmanaged scenarios that don't require any log in.
In both of these cases, your app may not want the SDK to enforce the managed identity's policies, but you may not have an explicit identity to switch to.

You can clear the active identity by calling any of the set identity methods with the identity OID parameter set to `null`.
Clearing the identity at one level will cause the SDK to look for the active identity at other levels, based on the order of precedence.

Alternately, you can pass empty string as the identity OID parameter, which sets the identity to a special empty value which is treated as an unmanaged identity.
Setting the active identity to empty string tells the SDK not to enforce *any* app protection policy.

### Implicit Identity Changes

The above section describes the different ways your app can explicitly set the active identity at the thread, context, and process levels.
However, the active identity in your app can also change without your app calling any of these methods.
This section describes how your app can listen for and respond to these implicit identity changes.

Listening for these implicit identity changes is optional, but recommended.
The SDK will never change the active identity without providing these implicit identity change notifications.

> [!CAUTION]
> If your app choses not to listen for implicit identity changes, be extra careful not to assume the active identity.
> When in doubt, use the `getCurrentThreadIdentityOID`, `getUIPolicyIdentityOID`, and `getProcessIdentityOID` methods to confirm the active identity.

#### Sources of Implicit Identity Changes

- Data ingress from **other Intune-managed apps** can change the active identity on the thread and context level.
  - If an activity is launched from an `Intent` sent by another MAM app, the activity's identity will be set based on the active identity in the other app at the point the `Intent` was sent.
    - For example, an activity to view a Word document is launched from an intent from Microsoft Outlook when a user selects a document attachment. Office's document viewer activity's identity is switched to the identity from Outlook.
  
  - For services, the thread identity will be set similarly for the duration of an `onStart` or `onBind` call. Calls into the `Binder` returned from `onBind` will also temporarily set the thread identity.

  - Calls into a `ContentProvider` will similarly set the thread identity for their duration.

- **User interaction** with an activity can change the active identity on the context level. For example:
  - A user canceling out of an authorization prompt during `Resume` will result in an implicit switch to an empty identity.

#### Handling Implicit Identity Changes

Your app can optionally listen for and react to these implicit identity changes.
For example, your application may require multiple steps before an added account is usable, like an email app setting up a new inbox.
Upon seeing an attempted identity switch to this incomplete account's identity, your app's handler could redirect the user to the account setup activity before accepting the identity switch.
Alternately, your app's handler could display an error dialog and block the identity switch.

Your app can implement the [MAMIdentityRequirementListener] interface on a `Service` or `ContextProvider` for identity changes applying to this thread. Your implementation must override:

```java
public abstract void onMAMIdentitySwitchRequired(String upn, String oid,
        AppIdentitySwitchResultCallback callback);
```

Your app can implement the [MAMActivityIdentityRequirementListener] interface on an `Activity` for identity changes applying to this activity.
Your implementation must override:

```java
public abstract void onMAMIdentitySwitchRequired(String upn, String oid,
        AppIdentitySwitchReason reason,
        AppIdentitySwitchResultCallback callback);
```

The `AppIdentitySwitchReason` enum parameter describes the source of the implicit identity switch.

| Enum value | Default SDK behavior | Description |
| - | - | - |
| `CREATE` | Allow the identity switch. | The identity switch is occurring because of an activity creation. |
| `NEW_INTENT` | Allow the identity switch. | The identity switch is occurring because a new intent is being assigned to an activity. |
| `RESUME_CANCELLED` | Block the identity switch. | The identity switch is occurring because a resume was canceled. This is most common when the end user presses the back button on the PIN, authentication, or compliance UI. |

The [AppIdentitySwitchResultCallback] parameter allows developers to override the default behavior for the identity switch:

```java
public interface AppIdentitySwitchResultCallback {
  /**
    * @param result
    *            whether the identity switch can proceed.
    */
  void reportIdentitySwitchResult(AppIdentitySwitchResult result);
}
// Where [AppIdentitySwitchResult] is either `SUCCESS` or `FAILURE`.
```

`onMAMIdentitySwitchRequired` is called for all implicit identity changes except for those made through a Binder returned from `MAMService.onMAMBind`.
The default implementations of `onMAMIdentitySwitchRequired` immediately call:

- `callback.reportIdentitySwitchResult(FAILURE)` when the reason is `RESUME_CANCELLED`.

- `callback.reportIdentitySwitchResult(SUCCESS)` in all other cases.

It isn't expected that most apps will need to block or delay an identity switch in a different manner, but if an app needs to do so, the following points must be considered:

- If an identity switch is blocked, the end user behavior is the same as if the SDK's "receive data from other apps" app protection setting had prohibited the data ingress.

- If a Service is running on the main thread, `reportIdentitySwitchResult` **must** be called synchronously, or the UI thread stops responding.

- For `Activity` creation, [onMAMIdentitySwitchRequired] will be called before `onMAMCreate`. If the app must show UI to determine whether to allow the identity switch, that UI must be shown using a *different* activity.

- In an `Activity`, when a switch to the empty identity is requested with the reason as `RESUME_CANCELLED`, the app must modify the resumed activity to display data consistent with that identity switch.  If this isn't possible, the app should refuse the switch, and the user will be asked again to comply with policy for the resuming identity (for example, by being presented with the app PIN entry screen).

> [!CAUTION]
> A multi-identity app can receive incoming data from both managed and unmanaged apps.
> **It is the responsibility of the app to treat data from managed identities in a managed manner.**

If a requested identity is managed (use [MAMPolicyManager.getIsIdentityOIDManaged][getIsIdentityOIDManaged] to check), but the app isn't able to use that account (for example, because accounts, such as email accounts, must be set up in the app first) then the identity switch should be refused.

The default behavior for `MAMActivity.onMAMIdentitySwitchRequired` can be accessed by calling the static method `MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, upn, oid,
reason, callback)`.

Similarly, if you need to override `MAMActivity.onSwitchMAMIdentityComplete`, you may implement `MAMActivityIdentitySwitchListener` without explicitly inheriting from `MAMActivity`.

### Identity Switches and Screenshot Restrictions

The Intune App SDK uses the `Window` flag `FLAG_SECURE` to enforce screenshot policy.
Some apps may also set `FLAG_SECURE` for their own purposes.
When app protection policy doesn't restrict screenshots, the SDK won't modify `FLAG_SECURE`.

On an identity switch from an identity whose policy requires disabling screenshots to an identity whose policy doesn't, the SDK will clear `FLAG_SECURE`.
As a result, your app shouldn't rely on `FLAG_SECURE` remaining set after an identity switch.

### Preserving Identity In Async Operations

Apps often dispatch background tasks from the UI thread to handle operations on other threads.
A multi-identity app must ensure that these background tasks operate with the appropriate identity, which is often the same identity used by the activity that dispatched them.

The Intune App SDK provides [MAMAsyncTask] and [MAMIdentityExecutors] as a convenience to aid in preserving the identity in asynchronous operations. Your app must either use these (or explicitly set the thread identity on the tasks) if its asynchronous operations can:

- Write data belonging to a managed identity to a file
- Communicate with other apps

#### MAMAsyncTask

To use `MAMAsyncTask`, simply inherit from it instead of `AsyncTask` and replace overrides of `doInBackground` and `onPreExecute` with `doInBackgroundMAM` and `onPreExecuteMAM` respectively.
The `MAMAsyncTask` constructor takes an activity context.
For example:

```java
AsyncTask<Object, Object, Object> task = new MAMAsyncTask<Object, Object, Object>(thisActivity) {

    @Override
    protected Object doInBackgroundMAM(final Object[] params) {
        // Do operations.
    }

    @Override
    protected void onPreExecuteMAM() {
        // Do setup.
    };
}
```

`MAMAsyncTask` will assume the active identity based on normal order of precedence.

#### MAMIdentityExecutors

`MAMIdentityExecutors` allows you to wrap an existing `Executor` or `ExecutorService` instance as an identity-preserving `Executor`/`ExecutorService` with `wrapExecutor` and `wrapExecutorService` methods. For example

```java
Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

`MAMIdentityExecutors` will assume the active identity based on normal order of precedence.

### File Protection

#### Writing Protected Files

As mentioned in [Organizing App Data by Identity] above, the Intune App SDK associates the active identity (from the thread/process level) with files as they're written.
It is critical to have the correct identity set at file creation time to ensure proper encryption and selective wipe functionality.

Your app may query or change a file’s identity using the [MAMFileProtectionManager] class, specifically `MAMFileProtectionManager.getProtectionInfo` for querying and `MAMFileProtectionManager.protectForOID` for changing.

The `protectForOID` method can also be used to protect directories.
Directory protection applies recursively to all files and subdirectories contained in the directory.
When a directory is protected, all new files created within the directory will automatically have the same protection applied.
Because directory protection is applied recursively, the `protectForOID` call can take some time to complete for large directories.
For that reason, apps applying protection to a directory that contains a large number of files might wish to run `protectForOID` asynchronously on a background thread.

Calling `protectForOID` with empty string for the identity parameter will tag the file/directory with the unmanaged identity.
This operation will remove encryption from the file/directory if it was previously encrypted.
When a selective wipe command is issued, the file/directory won't be deleted.

> [!WARNING]
> It is important to ensure that only files belonging to a particular identity become protected
> with that identity. Otherwise, other identities may experience data loss when the owning identity
> signs out, as files will be wiped and encryption key access will be lost.

#### Displaying Protected File Content

It is equally critical to have the correct identity set when file content is being *displayed* to prevent unauthorized users from viewing managed data.
The SDK can't automatically infer a relationship between files being read and data being displayed in an `Activity`.
Apps *must* set the UI identity appropriately before displaying any managed data.
This includes data read from files.

If a file comes from outside the app (either from a
`ContentProvider` or read from a publicly writable location), the app *must* attempt to determine the file identity (using the correct
[MAMFileProtectionManager.getProtectionInfo][MAMFileProtectionManager] overload for the data source) before displaying information read from the file.

If `getProtectionInfo` reports a non-null, non-empty identity, the app *must* set the UI identity to match this identity using either [MAMActivity.switchMAMIdentityOID][switchMAMIdentityOID] or
[MAMPolicyManager.setUIPolicyIdentityOID][setUIPolicyIdentityOID].
If the identity switch fails, data from the file *must not* be displayed.

When reading from a content URI, it may be necessary to first read the identity (via the `getProtectionInfo` overload taking a `Uri`), then set the context or thread identity appropriately.
This must be done before opening a file descriptor or input stream on the `ContentResolver`, or else the operation may fail.

An example flow might look something like the following:

- User selects a document to open in the app.
- During the open flow, prior to reading data from disk, the app confirms the identity that should be used to display the content:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentityOID(activity, info.getIdentityOID(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

- The app waits until a result is reported to callback.
- If the reported result is a failure, the app doesn't display the document.
- The app opens and renders the file.
  
If an app uses the Android `DownloadManager` to download files,
the SDK will attempt to protect these files automatically using
the [identity priority described previously](#setting-the-active-identity).
The context used to retrieve the `DownloadManager` will be used if
the thread identity is unset.
If the downloaded files contain corporate data, it is the app's responsibility to call [protectForOID] if the files are moved or recreated after download.

#### Single-Identity to Multi-Identity Transition

If an app which previously released with single-identity Intune
integration later integrates multi-identity, previously installed apps will experience a transition.
This transition isn't visible to the user.

The app is *not required* to handle this transition.
All files created before the transition will continue being regarded as managed (so they'll stay encrypted if encryption policy is on).

If you don't want all previous app data to be associated with the managed identity, you can detect this transition and explicitly remove protection.

- Detect the upgrade by comparing your app's version to a known version where multi-identity support was added.
- Call `protectForOID` with empty string for the identity parameter on files or directories that you don't want associated with the managed identity.

#### Offline Scenarios

The Intune App SDK runs in "offline" mode when the Company Portal app isn't installed.
File identity tagging is sensitive to offline mode:

- If the Company Portal isn't installed, files can't be identity-tagged. Calling [MAMFileProtectionManager.protectForOID][protectForOID] in offline mode is safe, but it will have no effect.

- If the Company Portal is installed, but the app doesn't have App Protection Policy, files can't reliably be identity-tagged.

- When file identity tagging becomes available, all previously created files are treated as personal/unmanaged (belonging to the empty-string identity), except in cases where the app was previously installed as a single-identity managed app, as described in [Single-Identity to Multi-Identity Transition].

To avoid these cases, apps should avoid creating files containing account data until account registration completes successfully.
If your app absolutely must create files while offline, it can use [MAMFileProtectionManager.protectForOID][protectForOID] to correct the file's associated identity once the SDK is online.

### Data Buffer Protection

> [!WARNING]
> Writing data belonging to multiple accounts in a single file is not recommended.
> If possible, organize your app's files by identity.

The SDK's [MAMDataProtectionManager] provides methods for checking and changing the tagged identity on specific data buffers in either `byte[]` or `InputStream` format.

`MAMDataProtectionManager.protectForOID` allows an app to associate data with an identity and, if the identity is currently targeted with encryption policy, encrypt the data.
This encrypted data is suitable for storing to disk in a file.

`MAMDataProtectionManager` also allows you to query the data associated with the identity and unencrypt it.

Apps that make use of `MAMDataProtectionManager` should implement a receiver for the `MANAGEMENT_REMOVED` notification. See [Register for notifications from the SDK] for more detail.

After this notification completes, buffers that were protected via this class will no longer be readable (if file encryption was enabled when the buffers were protected).
An app can prevent these buffers becoming unreadable by calling `MAMDataProtectionManager.unprotect` on all buffers when handling the `MANAGEMENT_REMOVED` notification.
It is also safe to call `protectForOID` during this notification, if you wish to preserve identity information.
Encryption is guaranteed to be disabled during the notification and calling `protectForOID` in the handler won't encrypt data buffers.

> [!WARNING]
> Encryption operations should be avoided early in the app process. The SDK will perform encryption
> initialization asynchronously as early as possible after app startup. However, if an app makes
> an encryption request in app startup, it may be blocked until encryption initialization is
> complete.

> [!NOTE]
> The Intune App SDK encryption API should be used only to encrypt data as required by Intune
> policy. No protection will be applied to accounts that are not targeted with encryption policy
> enabled, so it cannot be used as general-purpose encryption library.

### Content Providers

A multi-identity app must also protect data shared through `ContentProvider`s to prevent inappropriately sharing managed content.

Your app must call the static [MAMContentProvider] method `isProvideContentAllowedForOid(provider, oid)` before returning content.
If this function returns false, the content *must not* be returned to the caller.

Calling `isProvideContentAllowedForOid` isn't required if your `ContentProvider` is returning a `ParcelFileDescriptor`.
File descriptors returned through a content provider are handled automatically based on the file identity.

### Selective Wipe

By default, the Intune App SDK will automatically handle selective wipes, deleting all *files* that have been associated with the managed identity.
Afterwards, the SDK will close the app gracefully, finishing activities and killing the app process.

The SDK provides the optional ability for your app to either supplement (recommended) or override the default wipe behavior.

The SDK's default wipe handler doesn't handle data buffers protected by  `MAMDataProtectionManager`.
If your app used this feature, it **must** supplement or override the default wipe handler to remove that data.

> [!NOTE]
> Supplementing and overriding default wipe behavior require handling specific SDK notifications.
> See [Register for notifications from the SDK] for more detail on implementing notification handlers.

#### Supplementing Default Wipe Behavior

To supplement the default SDK wipe behavior, your app can register for the `WIPE_USER_AUXILIARY_DATA` [MAMNotificationType].

This notification will be sent by the SDK *before* it performs the default selective wipe.
The SDK will wait for your app's notification handler to complete before deleting data and terminating the app.
Your app should clear data synchronously and not return until all cleanup is complete.

Apps should strongly consider supplementing the default wipe behavior with `WIPE_USER_AUXILIARY_DATA`, as app-specific cleanup is common for multi-identity apps.

#### Overriding Default Wipe Behavior

To override the default SDK wipe behavior, your app can register for the `WIPE_USER_DATA` [MAMNotificationType].

> [!WARNING]
> An app must never register for both `WIPE_USER_DATA` and `WIPE_USER_AUXILIARY_DATA`.

**Overriding the default SDK wipe behavior places considerable risk on your app.**
Your app will be fully responsible for removing all data associated with the managed identity, including all files and data buffers that have been tagged for that identity.

- If the managed identity was protected with encryption, and your app's custom wipe handler doesn't fully remove all managed data, any remaining managed files will remain encrypted. This data will become inaccessible, and your app may not handle attempting to read encrypted data gracefully.
- Your app's wipe handler may result in data loss for unmanaged users, if it removes files that aren't tagged with the managed identity.

If your app's custom wipe handler removes managed data from a file but wishes to leave other data in the file, it *must* change the identity of the file (via [MAMFileProtectionManager.protectForOID][protectForOID]) to either an unmanaged identity or empty string.

Your overridden wipe handler should clear data synchronously and not return until all cleanup is complete.

Consider closing your app manually after completing your custom wipe handler steps to prevent the user from accessing in-memory data after a wipe occurs.

### Exit Criteria

Plan to dedicate significant time for validating your app's integration of multi-identity. Before you start testing:

- Create and assign app protection policy to an account. This will be your test managed account.
- Create, but don't assign app protection policy to, another account. This will be your test unmanaged account. Alternately, if your app supports multiple account types beyond Microsoft Entra accounts, you can use an existing non-Entra account as the unmanaged test account.
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

For these tests, install your app and the Intune Company Portal; don't log in before starting the test.

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

For these tests, install your app and the Intune Company Portal; log in with both a managed and unmanaged account before starting the test.

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

For these tests, install your app and the Intune Company Portal; log in with both a managed and unmanaged account before starting the test. Additionally:

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

#### Validating selective wipe scenarios

Your multi-identity app may have supplemented or overridden the SDK's default wipe behavior.
These tests help ensure your multi-identity integration properly removes managed data when wipes are initiated, without impacting unmanaged data.

> [!WARNING]
> Reminder, if your app leveraged `MAMDataProtectionManager.protectForOID`, it **must** implement a handler for either `WIPE_USER_AUXILIARY_DATA` or `WIPE_USER_DATA`.

For these tests, install your app and the Intune Company Portal; log in with both a managed and unmanaged account before starting the test. For both accounts, exercise app scenarios that store account data.

| Scenario | Preconditions | Steps |  
| - | - | - |
| Supplemental wipe handler | Your app has implemented a handler for `WIPE_USER_AUXILIARY_DATA` | - [Issue a selective wipe from the Microsoft Intune admin center]. <br> - Confirm (typically via logging) that your wipe handler has executed successfully. <br> - Confirm that the managed account is removed from your app and all that account's data has been removed. <br> - Confirm that the unmanaged account is still logged in, none of the unmanaged account's data has been removed, and policy is still not applied.
| Overridden wipe handler | Your app has implemented a handler for `WIPE_USER_DATA` | - [Issue a selective wipe from the Microsoft Intune admin center]. <br> - Confirm (typically via logging) that your wipe handler has executed successfully. <br> - Confirm that the managed account is removed from your app and all that account's data has been removed. <br> - Confirm that the unmanaged account is still logged in, none of the unmanaged account's data has been removed, and policy is still not applied. <br> - Confirm that your app has either exited gracefully or is still in a healthy state after your wipe handler finishes.
| Manual file protection | - Your app calls `MAMFileProtectionManager.protectForOID` <br> - Your app has implemented a handler for `WIPE_USER_DATA` | - Ensure you have exercised scenarios where your app would manually protect at least one file belonging to the managed account. <br> - [Issue a selective wipe from the Microsoft Intune admin center]. <br> - Confirm that the files are removed. |
| Manual data buffer protection | - Your app calls `MAMDataProtectionManager.protectForOID` <br> - Your app has implemented a handler for either `WIPE_USER_AUXILIARY_DATA` or `WIPE_USER_DATA` | - Ensure you have exercised scenarios where your app would manually protect at least one data buffer belonging to the managed account. <br> - [Issue a selective wipe from the Microsoft Intune admin center]. <br> - Confirm that the data buffers are removed from whatever files they were stored in, and your app can still read the unmanaged data from those files. |

## Next Steps

After you've completed all the [Exit Criteria] above, your app is now successfully integrated as multi-identity and can enforce app protection policies on a per-identity basis.
The subsequent sections, [Stage 6: App Configuration] and [Stage 7: App Participation Features], may or may not be required, depending on your app's desired app protection policy support.
If you're unsure if any of these sections apply to your app, revisit [Key Decisions for SDK integration].

<!-- Stage 5 links -->
[Organizing App Data by Identity]:#organizing-app-data-by-identity
[Writing Protected Files]:#writing-protected-files
[Single-Identity to Multi-Identity Transition]:#single-identity-to-multi-identity-transition
[Data Buffer Protection]:#data-buffer-protection
[Implicit Identity Changes]:#implicit-identity-changes
[Exit Criteria]:#exit-criteria

<!-- Other SDK Guide Markdown docs -->
[Stage 1: Plan the Integration]:app-sdk-android-phase1.md
[Key Decisions for SDK integration]:app-sdk-android-phase1.md#key-decisions-for-sdk-integration
[Is my application single-identity or multi-identity?]:app-sdk-android-phase1.md#is-my-application-single-identity-or-multi-identity
[Registering for App Protection Policy]:app-sdk-android-phase4.md#registering-for-app-protection-policy
[Stage 6: App Configuration]:app-sdk-android-phase6.md
[Stage 7: App Participation Features]:app-sdk-android-phase7.md
[Register for notifications from the SDK]:app-sdk-android-phase7.md#register-for-notifications-from-the-sdk

<!-- Links to other Intune docs -->
[Issue a selective wipe from the Microsoft Intune admin center]:/mem/intune/apps/apps-selective-wipe

<!-- Class links -->
[AppIdentitySwitchResultCallback]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/AppIdentitySwitchResultCallback.html
[IdentitySwitchOption]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/IdentitySwitchOption.html
[MAMActivity]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html
[MAMActivityIdentityRequirementListener]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivityIdentityRequirementListener.html
[MAMAsyncTask]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMAsyncTask.html
[MAMContentProvider]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/content/MAMContentProvider.html
[MAMDataProtectionManager]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMDataProtectionManager.html
[MAMFileProtectionManager]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMFileProtectionManager.html
[MAMIdentityExecutors]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMIdentityExecutors.html
[MAMIdentityRequirementListener]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMIdentityRequirementListener.html
[MAMIdentitySwitchResult]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/MAMIdentitySwitchResult.html
[MAMNotificationType]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/notification/MAMNotificationType.html
[MAMPolicyManager]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html
[MAMSetUIIdentityCallback]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMSetUIIdentityCallback.html

<!-- Method links -->
<!-- MMI TODO: fix links when javadocs are published to github 
  https://dev.azure.com/msazure/Intune/_workitems/edit/26505930
-->
[getIsIdentityOIDManaged]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html#getIsIdentityOIDManaged(java.lang.String)
[protectForOID]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMFileProtectionManager.html#protectForOID(android.os.ParcelFileDescriptor,%20java.lang.String)
[onMAMIdentitySwitchRequired]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivityIdentityRequirementListener.html#onMAMIdentitySwitchRequired(java.lang.String,%20java.lang.String,%20com.microsoft.intune.mam.client.app.AppIdentitySwitchReason,%20com.microsoft.intune.mam.client.app.AppIdentitySwitchResultCallback)
[registerAccountForMAM]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/policy/MAMEnrollmentManager.html#registerAccountForMAM(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)
[setUIPolicyIdentityOID]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html#setUIPolicyIdentityOID(android.content.Context,%20java.lang.String,%20com.microsoft.intune.mam.client.identity.MAMSetUIIdentityCallback,%20java.util.EnumSet%3Ccom.microsoft.intune.mam.client.app.IdentitySwitchOption%3E)
[switchMAMIdentityOID]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html#switchMAMIdentityOID(java.lang.String,%20java.util.EnumSet%3Ccom.microsoft.intune.mam.client.app.IdentitySwitchOption%3E)


<!-- Other Microsoft links -->
[Microsoft Intune admin center]:https://go.microsoft.com/fwlink/?linkid=2109431
