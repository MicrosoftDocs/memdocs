---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide, appendix
description: The Microsoft Intune App SDK for Android lets you incorporate Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/24/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- M365-identity-device-management
- Android
ms.custom: intune-classic
---


# Microsoft Intune App SDK for Android developer guide
> [!NOTE]
> This guide is broken into several distinct stages.  Start at [Stage 1: Planning the Integration].

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

## Stage Goals
The Appendix contains greater detail about the Intune App SDK's architecture, information about uncommon integration steps, and other helpful content.

## The SDK in Greater Detail

### Class and Method Replacements
Through the [build tooling], the Intune App SDK attempts to minimize the integration burden of Android developers.
Prior to the build tooling, developers needed to perform all replacements manually.

> [!NOTE] 
> Apps *must* now integrate with the SDK [build tooling], which will perform all of these replacements automatically (except for [manifest replacements]).

Android base classes are replaced with their respective MAM equivalents in order to enable Intune management.
The SDK classes live between the Android base class and the app's own derived version of that class.
For example, an app activity might end up with an inheritance hierarchy that looks like: `AppSpecificActivity` extends `MAMActivity` extends `Activity`.
The MAM layer filters calls to system operations in order to seamlessly provide your app with a managed view of the world.

In addition to base classes, some classes your app might use without deriving from (e.g. `MediaPlayer`) also have required MAM equivalents, and [some method calls must also be replaced].
The table below lists many of the MAM replacements.

| Android base class | Intune App SDK replacement |
|--|--|
| android.app.Activity | MAMActivity |
| android.app.ActivityGroup | MAMActivityGroup |
| android.app.AliasActivity | MAMAliasActivity |
| android.app.Application | MAMApplication |
| android.app.Dialog | MAMDialog |
| android.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| android.app.DialogFragment | MAMDialogFragment |
| android.app.ExpandableListActivity | MAMExpandableListActivity |
| android.app.Fragment | MAMFragment |
| android.app.IntentService | MAMIntentService |
| android.app.LauncherActivity | MAMLauncherActivity |
| android.app.ListActivity | MAMListActivity |
| android.app.ListFragment | MAMListFragment |
| android.app.NativeActivity | MAMNativeActivity |
| android.app.PendingIntent | MAMPendingIntent (see [Pending Intent]) |
| android.app.Service | MAMService |
| android.app.TabActivity | MAMTabActivity |
| android.app.TaskStackBuilder | MAMTaskStackBuilder |
| android.app.backup.BackupAgent | MAMBackupAgent |
| android.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| android.app.backup.FileBackupHelper | MAMFileBackupHelper |
| android.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
| android.app.job.JobService | MAMJobService |
| android.content.BroadcastReceiver | MAMBroadcastReceiver |
| android.content.ContentProvider | MAMContentProvider |
| android.os.Binder | MAMBinder (Only necessary if the Binder is not generated from an Android Interface Definition Language (AIDL) interface) |
| android.media.MediaPlayer | MAMMediaPlayer |
| android.media.MediaMetadataRetriever | MAMMediaMetadataRetriever |
| android.media.MediaRecorder | MAMMediaRecorder |
| android.provider.DocumentsProvider | MAMDocumentsProvider |
| android.preference.PreferenceActivity | MAMPreferenceActivity |
| android.support.multidex.MultiDexApplication | MAMMultiDexApplication |
| android.widget.PopupWindow | MAMPopupMenu |
| android.widget.PopupWindow | MAMPopupWindow |
| android.widget.ListPopupWindow | MAMListPopupWindow |
| android.widget.TextView | MAMTextView |
| android.widget.AutoCompleteTextView | MAMAutoCompleteTextView |
| android.widget.CheckedTextView | MAMCheckedTextView |
| android.widget.EditText | MAMEditText |
| android.inputmethodservice.ExtractEditText | MAMExtractEditText |
| android.widget.MultiAutoCompleteTextView | MAMMultiAutoCompleteTextView |
| android.view.LayoutInflater | MAMLayoutInflaterManagement |
| android.view.ViewGroup | MAMViewGroup |
| android.view.SurfaceView | MAMSurfaceView |
| android.opengl.GLSurfaceView | MAMGLSurfaceView |
| android.widget.VideoView | MAMVideoView |

### Renamed Methods
In many cases, a method available in the Android class has been marked as final in the MAM replacement class.
In this case, the MAM replacement class provides a similarly named method (generally suffixed with `MAM`) that you should override instead.
For example, when deriving from [MAMActivity], instead of overriding `onCreate()` and calling `super.onCreate()`, `Activity` must override `onMAMCreate()` and call `super.onMAMCreate()`.
The Java compiler should enforce the final restrictions to prevent accidental override of the original method instead of the MAM equivalent.

### Wrapped System Services
For some system service classes, it is necessary to call a static
method on a MAM wrapper class instead of directly invoking the desired
method on the service instance.
For example, a call to
`getSystemService(ClipboardManager.class).getPrimaryClip()` must
become a call to
`MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)`.
Again, the required build plugin automatically makes these replacements.

| Android Class | Intune App SDK replacement |
|--|--|
| android.content.ClipboardManager | MAMClipboard |
| android.content.ContentProviderClient | MAMContentProviderClientManagement |
| android.content.ContentResolver | MAMContentResolverManagement |
| android.content.pm.PackageManager | MAMPackageManagement |
| android.app.DownloadManager | MAMDownloadManagement |
| android.print.PrintManager | MAMPrintManagement |
| android.support.v4.print.PrintHelper | MAMPrintHelperManagement |
| android.view.View | MAMViewManagement |
| android.view.DragEvent | MAMDragEventManagement |
| android.app.NotificationManager | MAMNotificationManagement |
| android.support.v4.app.NotificationManagerCompat | MAMNotificationCompatManagement |
| android.app.blob.BlobStoreManager | MAMBlobStoreManager |
| android.app.blob.BlobStoreManager.Session | MAMBlobStoreManager.Session |

Some classes have most of their methods wrapped, e.g. `ClipboardManager`, `ContentProviderClient`, `ContentResolver`,
and `PackageManager` while other classes have only one or two methods wrapped, e.g. `DownloadManager`, `PrintManager`, `PrintHelper`,
`View`, `DragEvent`, `NotificationManager` and `NotificationManagerCompat`. 

### Manifest Replacements
It may be necessary to perform some of the above class replacements in the manifest as well as in Java code. Of special note:
* Manifest references to `android.support.v4.content.FileProvider` must be replaced with `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider`.

### MDM and MAM Enrollment
As discussed in [Stage 4's Registration vs Enrollment], the Intune App SDK will "enroll" accounts that your app registers so that account is protected with policy.
The account becomes managed after this enrollment succeeds, and MAM policies should now be applied to this account.

The term "enrollment" can also refer to the end-user initiated process for enabling Device Management (MDM). 
MDM enrollment is entirely separate from App Protection Policy enrollment. 

An SDK-integrated app can have an account enrolled for App Protection Policy without that account being enrolled for Device Management. 
Likewise, a user can have enrolled a device for Device Management without having any SDK-integrated apps with accounts enrolled for App Protection Policy.

Typically, when developers and administrators refer to enrollment, they are referring to MDM enrollment, as App Protection Policy enrollment is largely invisible to both developers and end users.
See [Enroll Android devices] for more details on MDM enrollment.

## Integration Tips

### Understanding Company Portal logs
Company Portal logs contain information that Microsoft engineers use for issue investigations.
Some of the logs can be useful for developers integrating the SDK as well.

In particular, the file `DiagnosticsInfo-scrubbed.log` contains information on what apps are managed by MAM and the MAM policy details in the `PolicyDB Information` section. 
Every managed app has an entry in the `PolicyDB Information` section.
You should look for your app's package name here to confirm that MAM
policy is correctly targeted to your app. 
If you don't see your app's package name here, it indicates that the account logged in doesn't have MAM policy applied.

For description on each MAM policy setting, refer to
[Android app protection policy settings in Microsoft Intune]. 
For a description of how these settings will show up in the Company Portal logs, refer to [Review client app protection logs]. 
When MAM policy is not being enforced as expected, we recommend that you check Company Portal logs or the diagnostic UI, verify that your app is managed by MAM policy, and confirm the policy settings have expected values.

You can collect Company Portal logs in one of the following ways:
- Through the Company Portal
  - Open the Company Portal app
  - Click on the three dots menu on the up right corner
  - Click Settings
  - Under Diagnostic Logs, click Save Logs
  - Follow the prompt to choose the output directory to save the Company Portal logs. 
  - Use `adb shell pull` command to pull the logs from your Android device to your local machine.
- [Use Edge for Android to access managed app logs]. This will display UI for
collecting Company Portal logs and viewing MAM diagnostics.
- Call `MAMPolicyManager.showDiagnostics(context)` to display the same UI for collecting Company Portal logs.

### Quickly testing with changing policy
As you are developing and testing your app's integration of the Intune App SDK, you may frequently change the App Protection Policy settings for your test user.

By default, integrated apps will check-in with the Intune service for updated policy every 30 minutes, when active. 
You can avoid this wait and force a check-in through the Company Portal:

1. Launch the Company Portal. You do not need to sign in.
2. Click the ... menu icon.
3. Click Settings.
4. Scroll to the setting called "Management Policy".
5. Press the Sync button.

This will immediately schedule a check-in and will retrieve up-to-date policy targeted to your app and account.

### Troubleshooting AndroidX Migration
If you integrated the Intune App SDK *before* leveraging AndroidX, you may encounter an error like this while migrating to AndroidX:

```log
incompatible types: android.support.v7.app.ActionBar cannot be converted to androidx.appcompat.app.ActionBar
```

These errors can occur because your app references the SDK's legacy support classes.
The MAM support classes wrap Android support classes that have moved in AndroidX. 
To combat such errors, replace all MAM support class references with their AndroidX equivalents. 
This can be achieved by first removing the MAM support library dependencies from your Gradle build files. 
The lines in question will look something like the following:

```Gradle
implementation "com.microsoft.intune.mam:android-sdk-support-v4:$intune_mam_version"
implementation "com.microsoft.intune.mam:android-sdk-support-v7:$intune_mam_version"
```

Then, fix the resulting compile-time errors by replacing all references to MAM classes in the `com.microsoft.intune.mam.client.support.v7` and `com.microsoft.intune.mam.client.support.v4` packages with their AndroidX equivalents. 
For example, references to `MAMAppCompatActivity` should be changed to AndroidX's `AppCompatActivity`. 
As discussed above, the MAM build plugin/tool will automatically rewrite classes in the AndroidX libraries with the appropriate MAM equivalents at compile-time.


## Limitations and Special Cases

### Default enrollment
Your application can alternately register for App Protection Policies through a simplified process called **default enrollment**.
This feature is primarily to support private line-of-business apps that have not integrated MSAL.

> [!WARNING]
> Default enrollment comes with significant tradeoffs and is **not recommended**.
> Apps leveraging default enrollment do not support Conditional Access, do not benefit from SSO with Microsoft services, and cannot be used by non-Intune accounts.
> If your app ships to a public app store, default enrollment is not supported.

Default enrollment will force the end user to install the Company Portal and complete a MAM enrollment flow before allowing users into your application.

> [!NOTE] 
> Default enrollment is sovereign cloud aware.

Enable default enrollment with the following steps:

1. If your app integrates MSAL or you need to enable SSO,
   [configure MSAL](#configure-microsoft-authentication-library-msal)
   following [common MSAL configurations](#common-msal-configurations) #2. If not, you may skip this step.
   
2. Enable default enrollment by adding the following value in the manifest under the `<application>` tag:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />
   ```

3. Enable MAM policy required by adding the following value in the manifest under the `<application>` tag:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />
   ```

### Isolated Processes
The Intune App SDK cannot apply protections to isolated processes.
Support for isolated processes (`android:isolatedProcess`) requires the addition of the meta-data tag below. 

> [!Warning]
> By adding this meta-data, your application is declaring that the isolated process cannot expose organization data.
> Your application is responsible for guaranteeing this.

  ```xml
  <meta-data android:name="com.microsoft.intune.mam.AllowIsolatedProcesses" android:value="true" />
  ```

### Custom Screen Capture Restrictions
If your app contains a custom screen capture feature that bypasses Android's `Window`-level `FLAG_SECURE` restriction, you must check screen capture policy before allowing full access to the feature. 
For example, if your app uses a custom rendering engine to render the current view to a PNG file, you must first check `AppPolicy.getIsScreenCaptureAllowed()`. 

If your app does not contain any custom or third-party screen capture features, you are not required to take any action to restrict screen captures. 
Screen capture policy is automatically enforced at the `Window` level for all MAM integrated apps. 

Any attempts by the OS or another app to capture a `Window` in your app will be blocked as required. 
For example, if a user attempts to capture your app's screen through Android's built-in screenshot or screen recording features, the capture will be automatically restricted without participation from your app. 

### Policy enforcement limitations

* **Using Content Resolvers**: The "transfer or receive" Intune policy may block or partially block the use of a content resolver to
access the content provider in another app.
This will cause `ContentResolver` methods to return null or throw a failure value (for example, `openOutputStream` will throw `FileNotFoundException` if blocked).
The app can determine whether a failure to write data through a content resolver was caused by policy (or would be caused by policy) by making the call:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    or if there is no associated activity:

    ```java
    MAMPolicyManager.getCurrentThreadPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    In this second case, multi-identity apps must take care to set the thread identity appropriately (or pass an explicit identity to a `getPolicyForIdentity` call).

### Exported services
The AndroidManifest.xml file included in the Intune App SDK contains **MAMNotificationReceiverService**, which must be an exported service to allow the Company Portal to send notifications to a managed app.
The service checks the caller to ensure that only the Company Portal is allowed to send notifications.

### Reflection limitations
Some of the MAM base classes (for example, `MAMActivity`, `MAMDocumentsProvider`) contain methods (based on the original Android base classes) which use parameter or return types only present above certain API levels. 
For this reason, it may not always be possible to use reflection to enumerate all methods of app components.
This restriction is not limited to MAM, it is the same restriction that would apply if the app itself implemented these methods from the Android base classes.

### Robolectric
Testing Intune App SDK behavior under Robolectric is not supported. 
There are known issues running the SDK under Robolectric due to behaviors present under Robolectric that do not accurately mimic those on real devices or emulators.

If you need to test your application under Robolectric, the recommended workaround is to move your application class logic to a helper and produce your unit-testing apk with an application class that does not inherit from MAMApplication.


<!-- Appendix links -->
<!-- internal links -->
[manifest replacements]:#manifest-replacements
[some method calls must also be replaced]:#wrapped-system-services
[Pending Intent]:#pendingintent
[MAMApplication]:#mamapplication

<!-- Other SDK Guide Markdown docs -->
[Stage 1: Planning the Integration]:app-sdk-android-phase1.md
[build tooling]:app-sdk-android-phase3.md#build-tooling
[Stage 4's Registration vs Enrollment]:app-sdk-android-phase4.md#registration-vs-enrollment

<!-- Other MEM docs -->
[Review client app protection logs]:/mem/intune/apps/app-protection-policy-settings-log#android-app-protection-policy-settings
[Android app protection policy settings in Microsoft Intune]:/mem/intune/apps/app-protection-policy-settings-android
[Use Edge for Android to access managed app logs]:/mem/intune/apps/manage-microsoft-edge#use-edge-for-ios-and-android-to-access-managed-app-logs
[Enroll Android devices]:/mem/intune/enrollment/android-enroll 

<!-- Class links -->
[MAMActivity]:https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html
