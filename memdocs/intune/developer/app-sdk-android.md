---
# required metadata

title: Microsoft Intune App SDK for Android developer guide
description: The Microsoft Intune App SDK for Android lets you incorporate Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
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
> You might want to first read the [Intune App SDK overview](app-sdk.md), which covers the current features of the SDK and describes how to prepare for integration on each supported platform.
>
> To download the SDK, see [Download the SDK files](../developer/app-sdk-get-started.md#download-the-sdk-files).
>
> If you have issues with integrating the Intune App SDK into your apps, submit a [request for assistance](https://github.com/msintuneappsdk/ms-intune-app-sdk-android/issues) on GitHub.

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.


## What's in the SDK

The Intune App SDK consists of the following files:

* **Microsoft.Intune.MAM.SDK.aar**: The SDK components, except for the Support Library JAR files.
* **Microsoft.Intune.MAM.SDK.DownlevelStubs.aar**: This AAR contains
  stubs for Android system classes, which are present only on newer
  devices, but which are referenced by methods in [MAMActivity]. Newer
  devices will ignore these stub classes. This AAR is necessary only
  if your app performs reflection on classes deriving from
  `MAMActivity`, and most apps do not need to include it. The AAR
  contains ProGuard rules to exclude all its classes.
* **com.microsoft.intune.mam.build.jar**: A Gradle plugin, which [aids in integrating the SDK](#build-tooling).
* **CHANGELOG.md**: Provides a record of changes made in each SDK version.
* **THIRDPARTYNOTICES.TXT**:  An attribution notice that acknowledges third-party and/or OSS code that will be compiled into your app.

## Requirements

### Android versions

The SDK fully supports Android API 28 (Android 9.0) through Android
API 31 (Android 12.0). In order to target Android API 31, you must
use Intune App SDK v8.0 or later. APIs 23 through 27 are in limited
support. MAM usage and the Company Portal are not supported below
Android API 23. If your app declares `minSdkVersion` to an API level
below API 23, the MAM SDK will not block app usage for users who are
not targeted by MAM policy.

### AndroidX

From Intune APP SDK 8.0.0 onwards, the legacy Android Support Library
is no longer supported. Apps are expected to use AndroidX (either
directly or through the Jetifier) if they need support library
functionality.

### Company Portal app

The Intune App SDK for Android relies on the presence of the [Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) app on the device to enable app protection policies. The Company Portal retrieves app protection policies from the Intune service. When the app initializes, it loads policy and code to enforce that policy from the Company Portal.

> [!NOTE]
> When the Company Portal app is not on the device, an Intune-managed app behaves the same as a normal app that does not support Intune app protection policies.

For app protection without device enrollment, the user is _**not**_ required to enroll the device by using the Company Portal app.

## SDK integration

> [!IMPORTANT]
> Intune regularly releases updates to the Intune App SDK. Regularly check the [Intune App SDK for Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android) for updates and incorporate into your software development release cycle to ensure your apps support the latest App Protection Policy settings.

### Sample apps
Examples of how to integrate with the Intune App SDK properly include:

- [Taskr - A Microsoft Intune Android MAM SDK Example](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App). This example uses the [Gradle build plugin](#gradle-build-plugin).
- [Taskr - A Microsoft Intune React Native + Android MAM SDK Example](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App/tree/master/ReactMAM)

### Referencing Intune App libraries

The Intune App SDK is a standard Android library with no external dependencies. **Microsoft.Intune.MAM.SDK.aar** contains both the interfaces necessary for an app protection policy enablement and the code necessary to interoperate with the Microsoft Intune Company Portal app.

**Microsoft.Intune.MAM.SDK.aar** must be specified as an Android library reference. To do this, open your app project in Android Studio and go to **File > New > New module** and select **Import .JAR/.AAR Package**. Then select our Android archive package Microsoft.Intune.MAM.SDK.aar to create a module for the *.AAR* file type. Right-click the module or modules containing your app code and go to **Module Settings** > **Dependencies tab** > **+ icon** > **Module dependency** > Select the MAM SDK AAR module you just created > **OK**. This will ensure that your module compiles with the MAM SDK when you build your project.

#### ProGuard

If [ProGuard](https://www.guardsquare.com/products/proguard) (or any other shrinking/obfuscation mechanism) is used as a build step, 
the SDK has additional configuration rules, which must be included. When including the *.AAR* in your build, our rules are 
automatically integrated into the proguard step and the necessary class files are kept.

The [Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-overview#languages-and-frameworks) may have its own ProGuard restrictions. If your app integrates MSAL, you must follow the MSAL documentation on these restrictions.

### Policy enforcement
The Intune App SDK is an Android library, which allows your app to
support and participate in the enforcement of Intune policies. 

Most policies are enforced semi-automatically, but certain policies require 
[explicit participation from your app to enforce](#enable-features-that-require-app-participation).
Regardless of whether you perform source integration or utilize build tooling for integration
the policies requiring explicit participation will need to be coded for.

For policies that are automatically enforced, apps are required to replace inheritance from several Android base
classes with inheritance from MAM equivalents and similarly replace
calls to certain Android system service classes with calls to MAM
equivalents. The specific replacements needed are detailed
[below](#class-and-method-replacements) and can be manually performed with source integration 
or performed automatically through build tooling.

### Build tooling
The SDK provides build tools (a plugin for Gradle
builds and a command-line tool for non-Gradle builds) that perform
MAM equivalent replacements automatically. These tools transform the class files
generated by Java compilation, and do not modify the original source
code.

The tools perform [direct
replacements](#class-and-method-replacements)
only. They do not perform any more complex SDK integrations such as
[Save-As Policy](#enable-features-that-require-app-participation),
[Multi-Identity](#multi-identity-optional), [MAM
registration](#mam-managed-applications),
[AndroidManifest modifications](#manifest-replacements) or [MSAL
configuration](#configure-microsoft-authentication-library-msal)
so these must be completed before your app is fully Intune
enabled. Carefully review the rest of this documentation for
integration points relevant to your app.

> [!NOTE]
> It is fine to run the tools against a project which has already
> performed partial or complete source integration of the MAM SDK
> through manual replacements. Your project must still list
> the MAM SDK as a dependency.

### Gradle Build Plugin
If your app does not build with gradle, skip to [Integrating with the
Command Line Tool](#command-line-build-tool). 

The App SDK plugin is distributed as part of the SDK as
**GradlePlugin/com.microsoft.intune.mam.build.jar**. For Gradle to be
able to find the plugin, it must be added to the buildscript
classpath. The plugin depends on
[Javassist](https://jboss-javassist.github.io/javassist/), which must
also be added. To add these to the classpath, add the following to
your root `build.gradle`

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.27.0-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Then, in the `build.gradle` file for your APK project, simply apply the plugin as

```groovy
apply plugin: 'com.microsoft.intune.mam'
```

By default, the plugin will operate on `project` dependencies and
external libraries. Since SDK 8.0, it is no longer possible to process
libraries selectively -- all are processed.
Test compilation not affected. Configuration may be provided to list
* Projects to exclude
* Specific classes to exclude from processing
* Variants to exclude from processing. These can refer to either a
  complete variant name or a single flavor. For example
  * if your app has build types `debug` and `release` with flavors
    {`savory`, `sweet`} and {`vanilla`, `chocolate`} you could specify
  * `savory` to exclude all variants with the savory flavor or
    `savoryVanillaRelease` to exclude only that exact variant.

#### Example partial build.gradle

```groovy

apply plugin: 'com.microsoft.intune.mam'

dependencies {
    implementation project(':product:FooLib')
    implementation project(':product:foo-project')
    implementation "com.microsoft.bar:baz:1.0.0"

    // Include the MAM SDK
    implementation files("$PATH_TO_MAM_SDK/Microsoft.Intune.MAM.SDK.aar")
}
intunemam {
    excludeProjects = [':product:FooLib']
    excludeClasses = ['com.contoso.SplashActivity']
    excludeVariants=['savory']
}
```

This would have the following effects:
* `:product:FooLib` is not rewritten because it is included in `excludeProjects`
* `:product:foo-project` is rewritten, except for `com.contoso.SplashActivity` which is skipped because it's in `excludeClasses`
* `com.microsoft.bar:baz.1.0.0` is rewritten because all external libraries are included for processing.

#### Reporting
The build plugin can generate an html report of the changes it
makes. To request generation of this report, specify `report = true`
in the `intunemam` configuration block. If generated, the report will
be written to `outputs/logs` in the build directory.

```groovy
intunemam {
    report = true
}
```

#### Verification
The build plugin can run additional verification to look for possible
errors in processing classes. To request this, specify `verify = true`
in the `intunemam` configuration block. Note that this may add several
seconds to the time taken by the plugin's task.

```groovy
intunemam {
    verify = true
}
```


#### Incremental builds
To enable support for building incrementally, specify `incremental = true`
in the `intunemam` configuration block.  This is an experimental feature
aimed at increasing build performance by processing only the input files
that have changed.  The default configuration is `false`.

```groovy
intunemam {
    incremental = true
}
```


#### Dependencies

The gradle plugin has a dependency on
[Javassist](https://jboss-javassist.github.io/javassist/), which must
be available to Gradle's dependency resolution (as described
above). Javassist is used solely at build time when running the
plugin. No Javassist code will be added to your app.

> [!NOTE] 
> You must be using version 3.6.1 or newer of the Android Gradle plugin and Gradle 5.6.4 or newer.

When consuming MAM SDK 8.0.0+, you must ensure the following is set in your Gradle configuration:

```groovy
compileOptions {
	sourceCompatibility JavaVersion.VERSION_1_8
	targetCompatibility JavaVersion.VERSION_1_8
}
```

### Command Line Build Tool
If your build uses Gradle, skip to the [next section](#class-and-method-replacements).

The command-line build tool is available in the `BuildTool` folder of
the SDK drop. It performs the same function as the Gradle plugin
detailed above, but can be integrated into custom or non-Gradle build
systems. As it is more generic, it is more complex to invoke, so the
Gradle plugin should be used when it is possible to do so.

#### Using the Command-Line Tool

The command-line tool can be invoked by using the provided helper scripts
located in the `BuildTool\bin` directory.

The tool expects the following parameters.

| Parameter          | Required | Description                                                                                                                                                                      |
| --                 | --       | --                                                                                                                                                                               |
| `--input`          | Yes      | A semi-colon delimited list of jar files and directories of class files to modify. This should include all jars/directories that you intend to rewrite.                          |
| `--output`         | Yes      | A semi-colon delimited list of jar files and directories to store the modified classes to. There should be one output entry per input entry, and they should be listed in order. |
| `--classpath`      | Yes      | The build classpath. This may contain both jars and class directories.                                                                                                           |
| `--processed`      | No       | A semi-colon delimited list of jar files and directories containing classes which have already been processed by a previous invocation of the build tool.                   |
| `--excludeClasses` | No       | A semi-colon delimited list containing the names of the classes that should be excluded from rewriting.                                                                          |
| `--report`         | No       | Directory to write an HTML report about modified classes to. If not specified, no report is written.                                                                             |

The optional `--processed` option is used to enable incremental builds. The set of files/directories listed here should be disjoint with the input and classpath lists.

> [!NOTE]
> On Unix-like systems semi-colon is a command separator. To avoid the shell from splitting commands, make sure to escape each semi-colon with '\' or wrap the full parameter in quotation marks.

#### Example Command-Line Tool invocation

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

This would have the following effects:

* the `product-foo-project` directory is rewritten to `mam-build\product-foo-project`
* `bar.jar` is rewritten to `mam-build\libs\bar.jar`
* `zap.jar` is **not** rewritten because it is only listed in `--classpath`
* The `com.contoso.SplashActivity` class is **not** rewritten even if it is in `--input`

> [!NOTE] 
> The build tool does not currently support aar files. If your build
> system does not already extract `classes.jar` when dealing with aar files, you
> will need to do so before invoking the build tool.


## Class and method replacements
> [!NOTE] 
> Apps *should* integrate with the SDK [build tooling](#build-tooling), which will perform all of these replacements automatically 
> (except for [manifest replacements](#manifest-replacements)

Android base classes must be replaced with their respective MAM
equivalents in order to enable Intune management. The SDK classes live
between the Android base class and the app's own derived version of
that class. For example, an app activity might end up with an
inheritance hierarchy that looks like: `Activity` > `MAMActivity` >
`AppSpecificActivity`. The MAM layer filters calls to system
operations in order to seamlessly provide your app with a managed view
of the world.

In addition to base classes, some classes your app might use without
deriving (e.g. `MediaPlayer`) also have required MAM equivalents, and
[some method calls must also be replaced](#wrapped-system-services). The precise details are given below.

> [!NOTE] 
> If your app is integrating with SDK [build tooling](#build-tooling), the following class and method replacements
> are performed automatically.

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
| android.app.PendingIntent | MAMPendingIntent (see [Pending Intent](#pendingintent)) |
| android.app.Service | MAMService |
| android.app.TabActivity | MAMTabActivity |
| android.app.TaskStackBuilder | MAMTaskStackBuilder |
| android.app.backup.BackupAgent | MAMBackupAgent |
| android.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| android.app.backup.FileBackupHelper | MAMFileBackupHelper |
| android.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
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
| android.view.ViewGroup | MAMViewGroup |


> [!NOTE]
> Even if your application does not have a need for its own derived `Application` class, [see `MAMApplication` below](#mamapplication)

### Renamed Methods

In many cases, a method available in the Android class has been marked as final in the MAM replacement class. In this case, the MAM replacement class provides a similarly named method (generally suffixed with `MAM`) that you should override instead. For example, when deriving from [MAMActivity], instead of overriding `onCreate()` and calling `super.onCreate()`, `Activity` must override `onMAMCreate()` and call `super.onMAMCreate()`. The Java compiler should enforce the final restrictions to prevent accidental override of the original method instead of the MAM equivalent.

### MAMApplication
If your app creates a subclass of `android.app.Application`, then the build plugin will transform your application class. If your app does not subclass `android.app.Application`, then you **must** set `"com.microsoft.intune.mam.client.app.MAMApplication"` as the `"android:name"` attribute in your AndroidManifest.xml's `<application>` tag.

### PendingIntent
Instead of `PendingIntent.get*`, you must use the `MAMPendingIntent.get*` method. After this, you can use the resultant `PendingIntent` as usual.

### Wrapped System Services
For some system service classes, it is necessary to call a static
method on a MAM wrapper class instead of directly invoking the desired
method on the service instance. For example, a call to
`getSystemService(ClipboardManager.class).getPrimaryClip()` must
become a call to
`MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)`. It
is not recommended to make these replacements manually. Instead, let
the BuildPlugin do it.

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
| android.view.Window | MAMWindowManagement |
| android.view.DragEvent | MAMDragEventManagement |
| android.app.NotificationManager | MAMNotificationManagement |
| android.support.v4.app.NotificationManagerCompat | MAMNotificationCompatManagement |
| android.app.blob.BlobStoreManager | MAMBlobStoreManager |
| android.app.blob.BlobStoreManager.Session | MAMBlobStoreManager.Session |

Some classes have most of their methods wrapped, e.g. `ClipboardManager`, `ContentProviderClient`, `ContentResolver`,
and `PackageManager` while other classes have only one or two methods wrapped, e.g. `DownloadManager`, `PrintManager`, `PrintHelper`,
`View`, `DragEvent`, `NotificationManager` and `NotificationManagerCompat`. Consult APIs exposed by the MAM equivalent
classes for the exact method if you do not use the BuildPlugin.

### Manifest Replacements
It may be necessary to perform some of the above class replacements in the manifest as well as in Java code. Of special note:
* Manifest references to `android.support.v4.content.FileProvider` must be replaced with `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider`.

## AndroidX Libraries
With Android P, Google announced a new (renamed) set of support libraries called
AndroidX, and version 28 is the last major release of the existing
android.support libraries.

Unlike with the android support libs, we do not provide MAM variants
of the AndroidX libraries. Instead, AndroidX is treated as any other
external library and rewritten. For Gradle builds, this is done
automatically.  Invocations of the command-lines tool must list all
jar files explicitly.

### Troubleshooting AndroidX Migration
While migrating your SDK-integrated app to AndroidX, you may encounter an error like the following:

```log
incompatible types: android.support.v7.app.ActionBar cannot be converted to androidx.appcompat.app.ActionBar
```

These errors can occur because your app references MAM support classes. MAM support classes wrap Android support 
classes that have moved in AndroidX. To combat such errors, replace all MAM support class references with their 
AndroidX equivalents. This can be achieved by first removing the MAM support library dependencies from your Gradle 
build files. The lines in question will look something like the following:

```Gradle
implementation "com.microsoft.intune.mam:android-sdk-support-v4:$intune_mam_version"
implementation "com.microsoft.intune.mam:android-sdk-support-v7:$intune_mam_version"
```

Then, fix the resulting compile-time errors by replacing all references to MAM classes in the
`com.microsoft.intune.mam.client.support.v7` and `com.microsoft.intune.mam.client.support.v4`
packages with their AndroidX equivalents. For example, references to `MAMAppCompatActivity` should be changed to
AndroidX's `AppCompatActivity`. As discussed above, the MAM build plugin/tool will automatically rewrite classes
in the AndroidX libraries with the appropriate MAM equivalents at compile-time.

## Logging

Logging should be initialized early to get the most value out of logged data. `Application.onMAMCreate()` is typically the best place to initialize logging.

To receive MAM logs in your app, create a [Java Handler](https://docs.oracle.com/javase/7/docs/api/java/util/logging/Handler.html) and add it to the **MAMLogHandlerWrapper**. This will invoke `publish()` on the application handler for every log message.

```java
/**
 * Global log handler that enables fine grained PII filtering within MAM logs.  
 *
 * To start using this you should build your own log handler and add it via
 * MAMComponents.get(MAMLogHandlerWrapper.class).addHandler(myHandler, false);  
 *
 * You may also remove the handler entirely via
 * MAMComponents.get(MAMLogHandlerWrapper.class).removeHandler(myHandler);
 */
public interface MAMLogHandlerWrapper {
    /**
     * Add a handler, PII can be toggled.
     *
     * @param handler handler to add.
     * @param wantsPII if PII is desired in the logs.    
     */
    void addHandler(final Handler handler, final boolean wantsPII);

    /**
     * Remove a handler.
     *
     * @param handler handler to remove.
     */
    void removeHandler(final Handler handler);
}
```

## Diagnostics Information
Apps can invoke `MAMPolicyManager.showDiagnostics(context)`
method that starts an activity displaying UI for collecting Company Portal logs and viewing MAM diagnostics.
This is an optional feature that may assist in debugging.

When Company Portal is not installed on device, a dialog will be
prompted to inform the user that this information is currently not available. When apps are managed by MAM policy, detailed MAM policy settings will be displayed.

## MAM Strict Mode
MAM Strict Mode provides a mechanism to detect "smells" in app usage
of MAM APIs or MAM-restricted platform APIs. It is loosely patterned
after Android's StrictMode, and runs a set of checks which raise
errors when they fail. It is not intended to be left enabled in
production builds, but you are *strongly encouraged* to use it in your
app's internal development, debug, and/or dogfood builds.

To enable, call

```java
MAMStrictMode.enable();
```
 early in application initialization
(e.g. `Application.onCreate`). 

When a MAM Strict Mode check fails, try to determine whether it is a
real issue that can be fixed in your app, or a false positive. If you
believe it's a false positive or you aren't sure, let the
Intune MAM team know. This will allow us to make sure we agree with
the false positive determination and to attempt to improve detection
for future releases. To suppress false positives, disable the failing
check (more info below).

### Handling Violations
When a check fails, it runs a **MAMStrictViolationHandler**. The default
handler throws an `Error`, which is expected to crash the app. This is
to make failures as noisy as possible, and fits with the intention
that strict mode should not be enabled in production builds.

If your app would like to handle violations differently, it can supply its own handler by calling:

```java
MAMStrictMode.global().setHandler(handler);
```

where `handler` implements `MAMStrictViolationHandler`.

### Suppressing Checks
If a check fails in a situation where your app is doing nothing
incorrect, report it as mentioned above. At some times,
however, it may be necessary to disable the check encountering a false
positive, at least while waiting for an updated SDK. The check which
failed will be shown in the error raised by the default handler, or
will be passed to a custom handler if set.

Suppression can be done globally, but temporarily disabling per-thread at the
specific call site is preferred. The following examples show various
ways to disable **MAMStrictCheck.IDENTITY_NO_SUCH_FILE MAMStrictCheck** (raised if an
attempt is made to protect a file which doesn't exist).


#### Per-Thread Temporary Suppression
This is the preferred suppression mechanism.
```java
try (StrictScopedDisable disable = MAMStrictMode.thread().disableScoped(MAMStrictCheck.IDENTITY_NO_SUCH_FILE)) {
    // Perform the operation which raised a violation here
}
// The check is no longer disabled once the block exits
```

#### Per-Thread Permanent Suppression
```java
MAMStrictMode.thread().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```

#### Global (Process-Wide) Suppression
```java
MAMStrictMode.global().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```



## Enable features that require app participation

There are some app protection policies the SDK cannot enforce on its own:
* Enforce restrictions on saving files to local or cloud storage.
* Enforce restrictions on opening files from local or cloud storage.
* Enforce restrictions on content in notifications.

Your app should use the methods in the **AppPolicy** interface to ask whether these actions
are allowed. To test if saving or opening a file/document is allowed, use
**getIsSaveToLocationAllowed** and **getIsOpenFromLocationAllowed**. To determine restrictions
on notification content, use `getNotificationRestriction`. Expanded examples for all these
scenarios are given later in this section.

Note that methods in **AppPolicy** which do not pertain to the above policies provide
information which your app may use to present a better user experience but are not
required for policy enforcement. For example, **AppPolicy** exposes information on PIN and
screenshot policies, but these are enforced automatically.

To retrieve an `AppPolicy` instance, use one of the [MAMPolicyManager] methods. 

> [!NOTE]
> `MAMPolicyManager` will always return a non-null App Policy, even if the device or app is not under an Intune management policy.

### Example: Determine if PIN is required for the app

If the app has its own PIN user experience, you might want to disable it if the IT administrator has configured the SDK to prompt for an app PIN. To determine if the IT administrator has deployed the app PIN policy to this app, for the current end user, call the following method:

```java

MAMPolicyManager.getPolicy(currentActivity).getIsPinRequired();
```

### Example: Determine the primary Intune user

In addition to the APIs exposed in AppPolicy, the user principal name (**UPN**) is also exposed by the **getPrimaryUser()SaveLocation** API defined inside the **MAMUserInfo** interface. To get the UPN, call the following:

```java
MAMComponents.get(MAMUserInfo.class).getPrimaryUser();
```

### Example: Data transfer between apps and device or cloud storage locations

Many apps implement features that allow the end user to save data to or open data from
local file storage or cloud storage services.
The Intune App SDK allows IT administrators to protect against data ingress and leakage by
applying policy restrictions as they see fit in their organization.

**App participation is needed to enable the feature.**
If your app allows saving to personal or cloud locations directly from the app *or*
allows for data to be opened directly into the app,
you must implement the respective feature to ensure that the IT administrator can control whether
saving to / opening from a location is allowed.

#### Saving to device or cloud storage

The API below lets the app know whether saving to a personal store is allowed by the current Intune administrator's policy.

To determine if the policy is enforced, make the following call:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(
SaveLocation service, String username);
```

The `service` parameter must be one of the following **SaveLocation** values:

* `SaveLocation.ONEDRIVE_FOR_BUSINESS`
* `SaveLocation.SHAREPOINT`
* `SaveLocation.LOCAL`
* `SaveLocation.ACCOUNT_DOCUMENT`
* `SaveLocation.OTHER`

For determining whether `ACCOUNT_DOCUMENT` or `OTHER` should be passed to `getIsSaveToLocationAllowed`
see [Unknown or unlisted locations](#unknown-or-unlisted-locations) for more information.

For the `username` parameter, see [Username for data transfer](#username-for-data-transfer) for more information.

The previous method of determining whether a user’s policy allowed them to save data to various locations was
`getIsSaveToPersonalAllowed()` within the same **AppPolicy** class.
This function is now **deprecated** and should not be used,
the following invocation is equivalent to `getIsSaveToPersonalAllowed()`:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(SaveLocation.LOCAL, null);
```

#### Opening data from a local or cloud storage location

The API below lets the app know whether opening from a personal store is allowed by the current Intune administrator's policy.

To determine if the policy is enforced, make the following call:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsOpenFromLocationAllowed(
OpenLocation location, String username);
```

The `location` parameter must be one of the following **OpenLocation** values:

* `OpenLocation.ONEDRIVE_FOR_BUSINESS`
* `OpenLocation.SHAREPOINT`
* `OpenLocation.CAMERA`
* `OpenLocation.LOCAL`
* `OpenLocation.ACCOUNT_DOCUMENT`
* `OpenLocation.OTHER`

The `OpenLocation.CAMERA` location should be passed in when the app is opening data from the camera.
The `OpenLocation.LOCAL` location should be passed in when the app is opening data from the external storage on the local device.
The `OpenLocation.ACCOUNT_DOCUMENT` location should be passed in when the app is opening data that belongs to an
AAD account signed into the app.

For determining whether `ACCOUNT_DOCUMENT` or `OTHER` should be passed to `getIsOpenFromLocationAllowed`
see [Unknown or unlisted locations](#unknown-or-unlisted-locations) for more information.

For the `username` parameter, see [Username for data transfer](#username-for-data-transfer) for more information.

#### Unknown or unlisted locations

When the desired location is not listed in the `SaveLocation` or `OpenLocation` enums or it is unknown
there are two options for the `service`/`location` parameter, `ACCOUNT_DOCUMENT` and `OTHER`.
`ACCOUNT_DOCUMENT` should be used when the data belongs to an AAD account signed into the app,
but is not `ONEDRIVE_FOR_BUSINESS` or `SHAREPOINT` whereas `OTHER` should be used when that is not the case.

It is important to make the distinction clear between the managed account and an account that shares the managed account's UPN.
For example, a managed account with UPN "user@contoso.com" signed into OneDrive is not the same as an account with UPN "user@contoso.com" signed into Dropbox.
If an unknown or unlisted service is accessed by signing into the managed account (e.g. "user@contoso.com" signed into OneDrive),
it should be represented by the `ACCOUNT_DOCUMENT` location.
If the unknown or unlisted service signs in through another account (e.g. "user@contoso.com" signed into Dropbox),
it is not accessing the location with a managed account and should be represented by the `OTHER` location.

#### Username for data transfer

When checking the save policy, the `username` should be the UPN/username/email associated with the
cloud service being saved to (*not* necessarily the same as the user owning the document being saved).
`SaveLocation.LOCAL` is not a cloud service and so should always be used with a `null` username parameter.

When checking the open policy, the `username` should be the UPN/username/email associated with the
file or cloud service being opened from. `OpenLocation.LOCAL` is not a cloud service location, but may be tagged with 
an identity to indicate ownership. When opening a file from local storage, the file owner must always be considered, 
because the file owner's save-as policy may or may not permit other users to open the file. For identity-tagged files, 
`username` should be the file owner's identity. For files without an identity tag, 
`username` should be null. 

>[!NOTE]
>For convenience, we provide an SDK method `AppPolicy.isOpenFromLocalStorageAllowed` that takes a `File` parameter
>for a file in local storage. It terms of enforcing policy, is functionally identical to calling
>`AppPolicy.isOpenFromLocationAllowed(OpenLocation.LOCAL, username)` except it handles parsing the file owner's
>`username` from the `File`.

`OpenLocation.CAMERA` is not a cloud service location and so should always be used with a `null` username parameter.

The following locations will always expect a username that contains a mapping between the AAD UPN and the cloud service username:
`ONEDRIVE_FOR_BUSINESS`, `SHAREPOINT`, and `ACCOUNT_DOCUMENT`.

If a mapping between the AAD UPN and the cloud service username does not exist or the username is not known use `null`.

#### Sharing blocked dialog

The SDK provides a dialog to notify the user that a data transfer action was blocked by MAM policy.

The dialog should be displayed to the user when the [isSaveToAllowedForLocation] or [isOpenFromAllowedForLocation] API call
results in the save/open action being blocked.
The dialog displays a generic message and will return to the `Activity` that called it when dismissed.

To display the dialog, make the following call:

``` java
MAMUIHelper.showSharingBlockedDialog(currentActivity)
```

### Allow for file sharing

If saving to public storage locations is not allowed your app should still allow for the user to view files by 
downloading them to [app private storage](https://developer.android.com/training/data-storage) and then 
opening them with the system chooser.

### Example: Determine if notifications with organization data need to be restricted

If your app displays notifications, you must check the notification restriction policy for the user associated with the notification before showing the notification. To determine if the policy is enforced, make the following call.

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentity(notificationIdentity).getNotificationRestriction();
```

If the restriction is `BLOCKED`, the app must not show any notifications for the user associated with this policy. If `BLOCK_ORG_DATA`, the app must show a modified notification that does not contain organization data. If `UNRESTRICTED`, all notifications are allowed.

If `getNotificationRestriction` is not invoked, the MAM SDK will make a best effort to restrict notifications automatically for single-identity apps. If automatic blocking is enabled and `BLOCK_ORG_DATA` is set, the notification will not be shown at all. For more fine-grained control, check the value of `getNotificationRestriction` and modify app notifications appropriately.

### Bypassing conditional launch restrictions

In very rare scenarios, it may be necessary for conditional launch restrictions to be bypassed for a particular Activity.  For example, a dialer app may want to allow for an incoming call to be answered without the user having to enter their PIN first.  For a multi-identity app (see [Multi-Identity](#multi-identity-optional) below), this can be accomplished by setting the identity associated with the Activity to an unmanaged identity.  To allow for a similar bypass of conditional launch restrictions in a single-identity app, an Activity can be registered for bypass with the MAMPolicyManager.

```java
MAMPolicyManager.bypassConditionalLaunchChecks(this);
```

This method must be called before `onMAMCreate()` is called, in order to effectively bypass the conditional launch checks.  For example, it could be called from the Activity's constructor, or from an override to `attachBaseContext()`.  If you choose to override `attachBaseContext()`, remember to call the superclass's `attachBaseContext()`, or data leaks could occur.

>[!NOTE]
> Because this method allows the bypass of conditional launch policy checks, **it should only be used after consulting with Microsoft** to confirm there is no other supported way to achieve your app’s desired behavior.

## Register for notifications from the SDK

### Overview
The Intune App SDK allows your app to control the behavior of certain policies, such as selective wipe, when they are deployed by the IT administrator. When an IT administrator deploys such a policy, the Intune service sends down a notification to the SDK.

Your app must register for notifications from the SDK by creating a **MAMNotificationReceiver** and  registering it with **MAMNotificationReceiverRegistry**. This is done by providing the receiver and the type of notification desired in  `App.onCreate`, as the example below illustrates:

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

### MAMNotificationReceiver

The **MAMNotificationReceiver** interface simply receives notifications from the Intune service. Some notifications are handled by the SDK directly, while others require the app's participation. An app **must** return either true or false from a notification. It must always return true unless some action it tried to take as a result of the notification failed.

* This failure may be reported to the Intune service. An example of a scenario to report is if the app fails to wipe user data after the IT administrator initiates a wipe.

>[!NOTE]
> It is safe to block in `MAMNotificationReceiver.onReceive` because its callback is not running on the UI thread.


### Types of notifications

The following **notifications MAMNotificationType** are sent to the app and some of them may require app participation:

* **WIPE_USER_DATA**: This notification is sent in a
  **MAMUserNotification**. When this notification is received, the
  app *must* delete all data associated with the managed identity
  (from `MAMUserNotification.getUserIdentity()`). The notification may
  occur for diverse reasons, including when your app calls
  **unregisterAccountForMAM**, when an IT admin initiates a wipe, or
  when admin-required conditional access policies are not
  satisfied. If your app does not register for this notification,
  default wipe behavior will be performed. The default behavior will
  delete all files for a single-identity app or all files tagged with
  the managed identity for a multi-identity app. This notification
  will never be sent on the UI thread.

* **WIPE_USER_AUXILIARY_DATA**: Apps can register for this
  notification if they'd like the Intune App SDK to perform the
  default selective wipe behavior, but would still like to remove some
  auxiliary data when the wipe occurs. This notification is not
  available to single identity-apps -- it will only be sent to
  multi-identity apps. This notification will never be sent on the UI
  thread.

* **REFRESH_POLICY**: This notification is sent in a
  **MAMUserNotification**. When this notification is received, any
  Intune policy decisions cached by your app must be invalidated and
  updated. If your app does not store any policy assumptions, it need
  not register for this notification. No guarantees are made as to
  what thread this notification will be sent on.

* **REFRESH_APP_CONFIG**: This notification is sent in a
  **MAMUserNotification**. When this notification is received, any
  cached Application Configuration data must be invalidated and
  updated. No guarantees are made as to what thread this notification
  will be sent on.

* **MANAGEMENT_REMOVED**: This notification is sent in a
  **MAMUserNotification** and informs the app that it is about to become
  unmanaged. Once unmanaged, it will no longer be able to read
  encrypted files, read data encrypted with MAMDataProtectionManager,
  interact with the encrypted clipboard, or otherwise participate in
  the managed-app ecosystem. See further details below. This
  notification will never be sent on the UI thread.

* **MAM_ENROLLMENT_RESULT**: This notification is sent in a
  **MAMEnrollmentNotification** to inform the app that an APP-WE
  enrollment attempt has completed and to provide the status of that
  attempt. No guarantees are made as to what thread this notification
  will be sent on.

* **COMPLIANCE_STATUS**: This notification is sent in a
  **MAMComplianceNotification** to inform the app of the result of a
  compliance remediation attempt. No guarantees are made as to what
  thread this notification will be sent on.

> [!NOTE]
> An app should never register for both the `WIPE_USER_DATA` and `WIPE_USER_AUXILIARY_DATA` notifications.

### MANAGEMENT_REMOVED

The `MANAGEMENT_REMOVED` notification indicates that a previously
policy-managed user will no longer be managed by Intune MAM
policy. This does not require wiping user data or signing out the
user (if a wipe were required, a `WIPE_USER_DATA` notification would
be sent). Many apps may not need to handle this notification at all,
however apps which use [MAMDataProtectionManager] should 
[take special note of this notification](#data-protection).

When MAM calls the app's `MANAGEMENT_REMOVED` receiver, the following will be true:
* MAM has already decrypted previously encrypted files (but not
  protected data buffers) belonging to the app. Files in public
  locations on the sdcard that don't directly belong to the app
  (e.g. the Documents or Download folders) are not decrypted.
* New files or protected data buffers created by the receiver method
  (or any other code running after the receiver starts) will not
  be encrypted.
* The app still has access to encryption keys, so operations such as
  decryption data buffers will succeed.

Once your app's receiver returns, it will no longer have access to encryption keys.

## Configure Microsoft Authentication Library (MSAL)

> [!NOTE]
> Azure Active Directory Authentication Library (ADAL) is deprecated.
> For more information, see [Update your applications to use Microsoft Authentication Library (MSAL)].
> To migrate your app from ADAL to MSAL, see [Migrate Android ADAL to MSAL] and [Differences between ADAL and MSAL].

First, read the MSAL integration guidelines found in the [MSAL repository on GitHub].
For more information, see [Overview of Microsoft Authentication Library (MSAL)] and the [MSAL Wiki].

Due to ADALs deprecation, apps should integrate with [MSAL].
However, the SDK still relies on [ADAL] for its authentication and conditional launch scenarios.
The necessary configuration values are communicated to the SDK via `AndroidManifest` metadata.

To ensure Intune's authentication policy can be applied properly, add the following to the app node in `AndroidManifest.xml`.
Some of these configurations are only required (see [common MSAL configurations](#common-msal-configurations) below)
if your app uses MSAL for authentication in general;
in that case, you will need the specific values your app uses to register itself with AAD.
This is done to ensure that the end user does not get prompted for authentication twice,
due to AAD recognizing two separate registration values: one from the app and one from the SDK.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
```

### MSAL metadata

* **Authority** is the AAD authority in use. If this value is absent, the AAD public environment is used.
    > [!NOTE]
    > Do not set this field if your application is sovereign cloud aware.

* **ClientID** is the AAD ClientID (also known as Application ID) to be used. You should use your own app's ClientID if it is registered with Azure AD or leverage [Default Enrollment](#default-enrollment-optional) if it does not integrate MSAL.

* **NonBrokerRedirectURI** is the [AAD redirect URI] to use in broker-less cases. If none is specified, a default value of `urn:ietf:wg:oauth:2.0:oob` is used. This default is suitable for most apps.

  * The NonBrokerRedirectURI is only used when SkipBroker is "true".

* **SkipBroker** is used to override the default MSAL SSO participation behavior. SkipBroker should only be specified for apps that specify a ClientID **and** do not support brokered authentication/device-wide SSO. In this case it should be set to "true". Most apps should not set the SkipBroker parameter.

  * A ClientID **must** be specified in the manifest to specify a SkipBroker value.

  * When a ClientID is specified, the default value is "false".

  * When SkipBroker is "true," the NonBrokerRedirectURI will be used. Apps that do not integrate MSAL (and therefore have no ClientID) will also default to "true".

### Common MSAL configurations

The following are common ways an app can be configured with MSAL. Find
your app's configuration and make sure to set the MSAL metadata
parameters (explained above) to the necessary values. In all cases,
the Authority may be specified if desired for non-default
environments. If not specified, the public production AAD authority
will be used.

#### 1. App does not integrate MSAL or ADAL

MSAL/ADAL metadata **must not** be present in the manifest.

#### 2. App integrates MSAL

|Required MSAL parameter| Value |
|--|--|
| ClientID | The app's ClientID (generated by Azure AD when the app is registered) |

Authority may be specified if necessary.

You must register your app with Azure AD and give your app access to the app protection policy service:
* See [Register your application with Azure Active Directory] for information about registering an application with Azure AD.
* Ensure the steps to give your Android app permissions to the app protection policy (APP) service are followed.
Use the instructions in the "Get started with Intune App SDK" guide under ["Give your app access to the Intune app protection service (optional)"].

Also see the requirements for [Conditional Access](#conditional-access) below.

#### 3. App integrates MSAL but does not support brokered authentication/device-wide SSO

|Required MSAL parameter| Value |
|--|--|
| ClientID | The app's ClientID (generated by Azure AD when the app is registered) |
| SkipBroker | **True** |

Authority and NonBrokerRedirectURI may be specified if necessary.

## MAM managed applications

### Overview
MAM supports both enrolled and unenrolled devices. The Company Portal is still required to be installed on the device, but the user does not need to sign into the Company Portal and enroll the device.


### Workflow

When an app creates a new user account, it should register the account for management with the Intune App SDK. The SDK will handle the details of enrolling the app in the APP-WE service; if necessary, it will retry any enrollments at appropriate time intervals if failures occur.

The app can also query the Intune App SDK for the status of a registered user to determine if the user should be blocked from accessing corporate content. Multiple accounts may be registered for management, but currently only one account can be actively enrolled with the APP-WE service at a time. This means only one account on the app can receive app protection policy at a time.

The app is required to provide a callback to acquire the appropriate access token from the Microsoft Authentication Library (MSAL) or the Azure Active Directory Authentication Library (ADAL) on behalf of the SDK. It is assumed that the app already uses MSAL or ADAL for user authentication and to acquire its own access tokens.

When the app removes an account completely, it should unregister that account to indicate that the app should no longer apply policy for that user. If the user was enrolled in the MAM service, the user will be unenrolled and the app will be wiped.


### Overview of app requirements

To implement APP-WE integration, your app must register the user account with the MAM SDK:

1. The app _must_ implement and register an instance of the [MAMServiceAuthenticationCallback] interface. The callback instance must be registered in the `onCreate()` (or `onMAMCreate()`) method of the Application subclass.

2. When a user account is created and the user successfully signs in with MSAL, the app _must_ call **registerAccountForMAM**.

3. When a user account is removed, the app should call **unregisterAccountForMAM** to remove the account from Intune management.

    > [!NOTE]
    > The call may initiate a wipe to completely remove corporate data for the user.


### MAMEnrollmentManager

All the necessary authentication and registration APIs can be found in the **MAMEnrollmentManager** interface. A reference to the `MAMEnrollmentManager` can be obtained as follows:

```java
MAMEnrollmentManager mgr = MAMComponents.get(MAMEnrollmentManager.class);

// make use of mgr
```

The `MAMEnrollmentManager` instance returned is guaranteed not to be null. The API methods fall into two categories: **authentication** and **account registration**.

### Account authentication

This section describes the authentication API methods in `MAMEnrollmentManager` and how to use them.

```java
interface MAMServiceAuthenticationCallback {
    String acquireToken(String upn, String aadId, String resourceId);
}
void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
void updateToken(String upn, String aadId, String resourceId, String token);
```

1. The app must implement the [MAMServiceAuthenticationCallback] interface to allow the SDK to request an AAD token for the given user and resource ID. The callback instance must be provided to the `MAMEnrollmentManager` by calling its registerAuthenticationCallback method. A token may be needed early in the app lifecycle for enrollment retries or app protection policy refresh check-ins, so the callback must be registered in the `onCreate()` (or `onMAMCreate()`) method of the app's Application subclass.

2. The **acquireToken** method should acquire the access token for the requested resource ID for the given user. If it can't acquire the requested token, it should return null.

    > [!NOTE]
    > Ensure that your app utilizes the `resourceId` and the `aadId` parameters passed to `acquireToken()`
    > so that the correct token is acquired.
    > The `resourceId` should be used to generate the proper scopes and the `aadId` should be used
    > to pass along the correct account.

    ```java
    class MAMAuthCallback implements MAMServiceAuthenticationCallback {
        public String acquireToken(String upn, String aadId, String resourceId) {
            final String[] scopes = {resourceId + "/.default"};

            final IAccount account = getAccount(aadId);
            if (account == null) {
                callback.onError(
                        new MsalUiRequiredException(MsalUiRequiredException.NO_ACCOUNT_FOUND, "no account found for " + aadId));
                return;
            }

            AcquireTokenSilentParameters params =
                new AcquireTokenSilentParameters.Builder()
                        .forAccount(account)
                        .fromAuthority(account.getAuthority())
                        .withScopes(Arrays.asList(scopes))
                        .withCallback(callback)
                        .build();

            return mMsalClientApplication.acquireTokenSilent(params);
        }

        private static IAccount getAccount(String aadId) throws InterruptedException, MsalException {
          IAccount account = null;

          if (mMsalClientApplication instanceof IMultipleAccountPublicClientApplication) {
              IMultipleAccountPublicClientApplication multiAccountPCA =
                      (IMultipleAccountPublicClientApplication) mMsalClientApplication;

              account = multiAccountPCA.getAccount(aadId);
          } else {
              ISingleAccountPublicClientApplication singleAccountPCA =
                      (ISingleAccountPublicClientApplication) mMsalClientApplication;

              ICurrentAccountResult accountResult = singleAccountPCA.getCurrentAccount();
              if (accountResult != null) {
                  account = accountResult.getCurrentAccount();
                  // make sure this is the correct user
                  if (account != null && !account.getId().equals(aadId))
                      account = null;
              }
          }
          return account;
      }
    }
    ```

3. In case the app is unable to provide a token when the SDK calls `acquireToken()`  -- for example, if silent authentication fails and it is an inconvenient time to show a UI -- the app can provide a token at a later time by calling the **updateToken** method. The same UPN, AAD ID, and resource ID that were requested by the prior call to `acquireToken()` must be passed to `updateToken()`, along with the token that was finally acquired. The app should call this method as soon as possible after returning null from the provided callback.

    > [!NOTE]
    > Do not call `updateToken()` from within your implementation of `acquireToken()`. `updateToken()` should be used in the case where `acquireToken()` is unable to acquire a token.

    > [!NOTE]
    > The SDK will call `acquireToken()` periodically to get the token, so calling `updateToken()` is not strictly required. However, it is strongly recommended as it can help enrollments and app protection policy check-ins complete in a timely manner.


### Account Registration

This section describes the account registration API methods in **MAMEnrollmentManager** and how to use them.

```java
void registerAccountForMAM(String upn, String aadId, String tenantId);
void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
void unregisterAccountForMAM(String upn);
Result getRegisteredAccountStatus(String upn);
```

1. To register an account for management, the app should call `registerAccountForMAM()`. A user account is identified by both its UPN and its AAD user ID. The tenant ID is also required to associate enrollment data with the user's AAD tenant. The user's authority may also be provided to allow enrollment against specific sovereign clouds; for more information see [Sovereign Cloud Registration](#sovereign-cloud-registration).  The SDK may attempt to enroll the app for the given user in the MAM service; if enrollment fails, it will periodically retry enrollment until the account is unregistered. The retry period will typically be 12-24 hours. The SDK provides the status of enrollment attempts asynchronously via notifications.

2. Because AAD authentication is required, the best time to register the user account
   is after the user has signed into the app and is successfully authenticated using MSAL.
   The user's AAD ID and tenant ID are returned from the MSAL authentication call
   as part of the [`IAccount`] related to the [`IAuthenticationResult`].
    * The account comes from the `IAuthenticationResult.getAccount()` method and contains the pertinent user information.
    * The tenant ID comes from the `IAccount.getTenantId()` method.
    * The AAD ID comes from the `IAccount.getId()` method.
3. To unregister an account from Intune management, the app should call `unregisterAccountForMAM()`. If the account has been successfully enrolled and is managed, the SDK will unenroll the account and wipe its data. Periodic enrollment retries for the account will be stopped. The SDK provides the status of unenrollment request asynchronously via notification.

### Sovereign Cloud Registration

Applications that are [sovereign cloud aware] **must** provide the `authority` to `registerAccountForMAM()`.

#### MSAL Guidance

For MSAL, set `multiple_clouds_supported` to `true` in the [MSAL configuration file].

``` json
{
  "multiple_clouds_supported": true,
}
```

#### ADAL Guidance

> [!NOTE]
> Support for sovereign cloud registration requires version 1.14.0 (or greater) of the ADAL library.

For ADAL, pass `instance_aware=true` to `acquireToken` as an `extraQueryParameters` parameter
followed by invoking `getAuthority()` on the `AuthenticationCallback` `AuthenticationResult`.

```java
mAuthContext.acquireToken(this, RESOURCE_ID, CLIENT_ID, REDIRECT_URI, PromptBehavior.FORCE_PROMPT, "instance_aware=true",
        new AuthenticationCallback<AuthenticationResult>() {
            @Override
            public void onError(final Exception exc) {
                // authentication failed
            }

            @Override
            public void onSuccess(final AuthenticationResult result) {
                mAuthority = result.getAuthority();
                // handle other parts of the result
            }
        });
```

> [!NOTE]
> Do not set the `com.microsoft.intune.mam.aad.Authority` meta-data item in AndroidManifest.xml.

> [!NOTE]
> Ensure that the authority is correctly set in your `MAMServiceAuthenticationCallback::acquireToken()` method.

#### Currently Supported Sovereign Clouds

1. Azure US Government Cloud
2. Microsoft Azure operated by 21Vianet (Azure China)


### Important implementation notes

#### Authentication

* When the app calls [registerAccountForMAM], it may receive a callback on its [MAMServiceAuthenticationCallback] interface shortly thereafter, on a different thread. Ideally, the app acquired its own AAD token prior to registering the account to expedite the acquisition of the requested token. If the app returns a valid token from the callback, enrollment will proceed and the app will get the final result via a notification.

* If the app doesn't return a valid AAD token, the final result from the enrollment attempt will be `AUTHORIZATION_NEEDED`. If the app receives this Result via notification, it is strongly recommended to expedite the enrollment process by acquiring the token for the user and resource previously requested from **acquireToken** and calling the **updateToken** method to initiate the enrollment process again.

* The app's registered `MAMServiceAuthenticationCallback` will also be called to acquire a token for periodic app protection policy refresh check-ins. If the app is unable to provide a token when requested, it will not get a notification, but it should attempt to acquire a token and call `updateToken()` at the next convenient time to expedite the check-in process. If a token is not provided, the callback will still be called at the next check-in attempt.

* Support for sovereign clouds requires providing the authority.

#### Registration

* For your convenience, the registration methods are idempotent; for example, [registerAccountForMAM] will only register an account and attempt to enroll the app if the account is not already registered, and **unregisterAccountForMAM** will only unregister an account if it is currently registered. Subsequent calls are no-ops, so there is no harm in calling these methods more than once. Additionally, correspondence between calls to these methods and notifications of results are not guaranteed: i.e. if `registerAccountForMAM()` is called for an identity that is already registered, the notification may not be sent again for that identity. It is possible that notifications are sent that don't correspond to any calls to these methods, since the SDK may periodically try enrollments in the background, and unenrollments may be triggered by wipe requests received from the Intune service.

* The registration methods can be called for any number of different identities, but currently only one user account can become successfully enrolled. If multiple user accounts that are licensed for Intune and targeted by app protection policy are registered at or near the same time, there is no guarantee on which one will win the race.

* Finally, you can query the **MAMEnrollmentManager** to see if a particular account is registered and to get its current status using the **getRegisteredAccountStatus** method. If the provided account is not registered, this method will return **null**. If the account is registered, this method will return the account's status as one of the members of the **MAMEnrollmentManager.Result** enumeration.

### Result and status codes

When an account is first registered, it begins in the `PENDING` state, indicating that the initial MAM service enrollment attempt is incomplete. After the enrollment attempt finishes, a notification will be sent with one of the Result codes in the table below. In addition, the **getRegisteredAccountStatus** method will return the account's status so the app can always determine if access to corporate content is blocked for that user. If the enrollment attempt fails, the account's status may change over time as the SDK retries enrollment in the background.

|Result code | Explanation |
| -- | -- |
| `AUTHORIZATION_NEEDED` | This result indicates that a token was not provided by the app's registered [MAMServiceAuthenticationCallback] instance, or the provided token was invalid.  The app should acquire a valid token and call **updateToken** if possible. |
| `NOT_LICENSED` | The user is not licensed for Intune, or the attempt to contact the Intune MAM service failed.  The app should continue in an unmanaged (normal) state and the user should not be blocked.  Enrollments will be retried periodically in case the user becomes licensed in the future. |
| `ENROLLMENT_SUCCEEDED` | The enrollment attempt succeeded, or the user is already enrolled.  In the case of a successful enrollment, corresponding `REFRESH_POLICY` and `REFRESH_APP_CONFIG` notifications are sent before this notification.  Access to corporate data should be allowed. |
| `ENROLLMENT_FAILED` | The enrollment attempt failed.  Further details can be found in the device logs.  The app should not allow access to corporate data in this state, since it was previously determined that the user is licensed for Intune. All apps should ensure that corporate data access is unauthorized, until `ENROLLMENT_SUCCEEDED` is obtained by your app.|
| `WRONG_USER` | Only one user per device can enroll an app with the MAM service. This result indicates that the user for whom this result was delivered (the second user) is targeted with MAM policy, but a different user is already enrolled. Because MAM policy cannot be enforced for the second user, your app must not allow access to this user's data (possibly by removing the user from your app) unless/until enrollment for this user succeeds at a later time. Concurrent with delivering this `WRONG_USER` result, MAM will prompt with the option to remove the existing account. If the human user answers in the affirmative, it will indeed be possible to enroll the second user a short time later. As long as the second user remains registered, MAM will retry enrollment periodically. |
| `UNENROLLMENT_SUCCEEDED` | Unenrollment was successful.|
| `UNENROLLMENT_FAILED` | The unenrollment request failed.  Further details can be found in the device logs. In general, this will not occur as long as the app passes a valid (neither null nor empty) UPN. There is no direct, reliable remediation the app can take. If this value is received when unregistering a valid UPN, report as a bug to the Intune MAM team.|
| `PENDING` | The initial enrollment attempt for the user is in progress.  The app can block access to corporate data until the enrollment result is known, but is not required to do so. |
| `COMPANY_PORTAL_REQUIRED` | The user is licensed for Intune, but the app cannot be enrolled until the Company Portal app is installed on the device. The Intune App SDK will attempt to block access to the app for the given user and direct them to install the Company Portal app (see below for details). |


### Company Portal requirement prompt override (optional)

If the `COMPANY_PORTAL_REQUIRED` Result is received, the SDK will block use of activities that use the identity for which enrollment was requested. Instead, the SDK will cause those activities to display a prompt to download the Company Portal. If you want to prevent this behavior in your app, activities may implement [MAMActivity.onMAMCompanyPortalRequired].

This method is called before the SDK displays its default blocking UI. If the app changes the activity identity or unregisters the user who attempted to enroll, the SDK will not block the activity. In this situation, it is up to the app to avoid leaking corporate data. Only multi-identity apps (discussed later) will be able to change the activity identity.

If you do not explicitly inherit [MAMActivity] (because the build tooling
will make that change), but still need to handle this notification you
may instead implement **MAMActivityBlockingListener**.

### Notifications

If the app registers for notifications of type **MAM_ENROLLMENT_RESULT**, a **MAMEnrollmentNotification** will be sent in order to inform the app that the enrollment request has completed. The `MAMEnrollmentNotification` will be received through the **MAMNotificationReceiver** interface as described in the [Register for notifications from the SDK](#register-for-notifications-from-the-sdk) section.

```java
public interface MAMEnrollmentNotification extends MAMUserNotification {
    MAMEnrollmentManager.Result getEnrollmentResult();
}
```

The **getEnrollmentResult** method returns the result of the enrollment request.  Since `MAMEnrollmentNotification` extends `MAMUserNotification`, the identity of the user for whom the enrollment was attempted is also available. The app must implement the `MAMNotificationReceiver` interface to receive these notifications, detailed in the [Register for notifications from the SDK](#register-for-notifications-from-the-sdk) section.

The registered user account's status may change when an enrollment notification is received, but it will not change in all cases (for example, if `AUTHORIZATION_NEEDED` notification is received after a more informative result such as `WRONG_USER`, the more informative result will be maintained as the account's status).  Once the account is successfully enrolled, the status will remain as `ENROLLMENT_SUCCEEDED` until the account is unenrolled or wiped.

### Conditional Access
Conditional Access (CA) is an Azure Active Directory
[feature](/azure/active-directory/develop/active-directory-conditional-access-developer)
which can be used to control access to AAD resources. [Intune
administrators can define CA rules](../protect/conditional-access.md)
which allow resource access only from devices or apps which are
managed by Intune. In order to ensure that your app is able to access
resources when appropriate, it is necessary to follow the steps
below. If your app does not acquire any AAD access tokens, or accesses
only resources which cannot be CA-protected, you may skip these steps.

1. Register your application with Azure Active Directory. This will generate a Client ID for your application.
2. Follow the steps for [Using MSAL] and [Configure MSAL to use a broker].
3. Set the manifest meta-data parameters per [Common MSAL configurations](#common-msal-configurations) for [App Integrates MSAL](#2-app-integrates-msal), see above.

## App Protection CA

### Overview
With App Protection CA (Conditional Access), access to resources is conditionalized on the application of Intune App Protection Policies.  AAD enforces this by requiring the app to be enrolled and managed by APP before granting a token to access a CA protected resource.  

> [!NOTE]
> Support for App Protection CA requires version 1.0.0 (or greater) of the MSAL library.

### Handle non-compliance with MSAL
When acquiring a token for a user, the MSAL library may return or throw an `MsalIntuneAppProtectionPolicyRequiredException` to indicate non-compliance with APP management. Additional parameters can be extracted from the exception for use in remediating compliance (see **MAMComplianceManager**). Once the remediation is successful, the app can re-attempt the token acquisition through MSAL.

### MAMComplianceManager

The **MAMComplianceManager** interface is used when the policy-required error is received from MSAL.  It contains the **remediateCompliance** method that should be called to attempt to put the app into a compliant state. A reference to the `MAMComplianceManager` can be obtained as follows:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

The `MAMComplianceManager` instance returned is guaranteed not to be null.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

The `remediateCompliance()` method is called to attempt to put the app under management to satisfy the conditions for AAD to grant the requested token.
The first four parameters can be extracted from the exception received by the MSAL `AuthenticationCallback.onError()` method (see code sample below).
The final parameter is a boolean which controls whether a UX is shown during the compliance attempt.
This is a simple blocking progress style interface provided as a default for apps that don't have a need to show customized UX during this operation.
It will only block while the compliance remediation is in progress and will not display the final result.
The app should register a notification receiver to handle the success or failure of the compliance remediation attempt (see below).

The `remediateCompliance()` method may do a MAM enrollment as part of establishing compliance.  The app may receive an enrollment notification if it has registered a notification receiver for enrollment notifications.  The app's registered [MAMServiceAuthenticationCallback] will have its **acquireToken** method called to get a token for the MAM enrollment. `acquireToken()` will be called before the app has acquired its own token, so any bookkeeping or account creation tasks that the app does after a successful token acquisition may not have been done yet.  The callback must be able to acquire a token in this case.  If you can't return a token from `acquireToken()`, the compliance remediation attempt will fail.  If you call **updateToken** later with a valid token for the requested resource, the compliance remediation will be retried immediately with the given token.

> [!NOTE]
> Silent token acquisition will still be possible in `acquireToken()` because the user will have already been guided to install the broker and register the device
> before the `MsalIntuneAppProtectionPolicyRequiredException` exception is received.
> This results in the broker having a valid refresh token in its cache, allowing silent acquisition of the requested token to succeed.

Here is a sample of receiving the policy-required error in the `AuthenticationCallback.onError()` method, and calling the **MAMComplianceManager** to handle the error.

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

### Status Notifications

If the app registers for notifications of type **COMPLIANCE_STATUS**, a **MAMComplianceNotification** will be sent in order to inform the app of the final status of the compliance remediation attempt. The `MAMComplianceNotification` will be received through the **MAMNotificationReceiver** interface as described in the [Register for notifications from the SDK](#register-for-notifications-from-the-sdk) section.

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

The `getComplianceStatus()` method returns the result of the compliance remediation attempt as a value from the **MAMCAComplianceStatus** enum.

|Status code | Explanation |
| -- | -- |
| UNKNOWN | Status is unknown. This could indicate an unanticipated failure reason. Additional information may be found in the Company Portal logs. |
| COMPLIANT | Compliance remediation succeeded and the app is now compliant with policy. The MSAL token acquisition should be retried. |
| NOT_COMPLIANT | The attempt to remediate compliance failed.  The app is not compliant and MSAL token acquisition should not be retried until the error condition is corrected.  Additional error information is sent with the MAMComplianceNotification. |
| SERVICE_FAILURE | There was a failure while attempting to retrieve compliance data from the Intune Service. Additional information may be found in the Company Portal logs. |
| NETWORK_FAILURE | There was an error connecting to the Intune Service. The app should try its token acquisition again when the network connection is restored. |
| CLIENT_ERROR | The attempt to remediate compliance failed for some reason related to the client.  For example, no token or wrong user. Additional error information is sent with the MAMComplianceNotification. |
| PENDING | The attempt to remediate compliance failed because the status response had not yet been received from the service when the time limit was exceeded. The app should try its token acquisition again later. |
| COMPANY_PORTAL_REQUIRED | The Company Portal must be installed on the device in order for compliance remediation to succeed.  If the Company Portal is already installed on the device, the app needs to be restarted.  In this case, a dialog will be shown asking the user to restart the app. |

If the compliance status is `MAMCAComplianceStatus.COMPLIANT`, the app should re-initiate its original token acquisition (for its own resource). If the compliance remediation attempt failed, the `getComplianceErrorTitle()` and `getComplianceErrorMessage()` methods will return localized strings that the app can display to the end user if it chooses.  Most of the error cases aren't remediable by the app, so for the general case it may be best to fail account creation or login and allow the user to try again later.  If a failure is persistent, the MAM logs may help determine the cause.  The end user can submit the logs. For more information, see [Upload and email logs](../user-help/send-logs-to-your-it-admin-by-email-android.md).

Since `MAMComplianceNotification` extends `MAMUserNotification`, the identity of the user for whom the remediation was attempted is also available.

Here is an example of registering a receiver using an anonymous class to implement the MAMNotificationReceiver interface:

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

### Declaring support for App CA
Once your app is ready to handle App CA remediation, you can tell Microsoft Identity your app is App CA ready.  To do this in your MSAL application, build your Public Client using the Client Capabilities of "protapp"

```java
{
	  "client_id" : "4b0db8c2-9f26-4417-8bde-3f0e3656f8e0",
	  "authorization_user_agent" : "DEFAULT",
	  "redirect_uri" : "msauth://com.microsoft.identity.client.sample.local/1wIqXSqBj7w%2Bh11ZifsnqwgyKrY%3D",
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


### Implementation Notes

> [!NOTE]
> The app's `MAMServiceAuthenticationCallback.acquireToken()` method should pass *false* for
> `forceRefresh` flag to `acquireTokenSilentAsync()`.
>  ```java
>  AcquireTokenSilentParameters acquireTokenSilentParameters =
>          builder.withScopes(Arrays.asList(scopes))
>                 .forceRefresh(false)
>                 .build();
>
> acquireTokenSilentAsync(acquireTokenSilentParameters);
> ```

> [!NOTE]
> If you want to show a custom blocking UX during the remediation attempt, you should pass *false* for the showUX parameter to `remediateCompliance()`. You must ensure that you show your UX and register your notification listener first before calling `remediateCompliance()`.  This will prevent a race condition where the notification could be missed if `remediateCompliance()` fails very quickly.  For example, the `onCreate()` or `onMAMCreate()` method of an Activity subclass is the ideal place to register the notification listener and then call `remediateCompliance()`.  The parameters for `remediateCompliance()` can be passed to your UX as Intent extras.  When the compliance status notification is received, you can display the result or simply finish the activity.

> [!NOTE]
> `remediateCompliance()` will register the account and attempt enrollment.  Once the main token is acquired, calling `registerAccountForMAM()` is not necessary, but there is no harm in doing so. On the other hand, if the app fails to acquire its token and wishes to remove the user account, it must call `unregisterAccountForMAM()` to remove the account and prevent background enrollment retries.

## Protecting Backup data

You can read more about Android's backup and restore options in the
[Android API guide](https://developer.android.com/guide/topics/data/backup.html)
and the changes introduced in Android S / 12 here:
[Change to backup and restore](https://developer.android.com/about/versions/12/backup-restore).

### Auto Backup for Apps

Beginning with Android M, Android began offering
[automatic full backups](https://developer.android.com/guide/topics/data/autobackup.html)
to Google Drive for apps, regardless of the app's target API.

Intune allows you to utilize all the
[Auto Backup features](https://developer.android.com/guide/topics/data/autobackup.html)
available from Android, including the ability to define custom rules in XML, with specific Intune integration guidance to ensure
data protection is applied.

#### Manifest Values

By default, `android:allowBackup` is set to **true** as outlined
in [enable and disable backup](https://developer.android.com/guide/topics/data/autobackup#EnablingAutoBackup).

If your app does not require full backup and restore functionality,
set `android:allowBackup` to **false**. 
*In this case, no further action is necessary and
"corporate" data will stay within the app.*

If your app requires full backup and restore functionality,
set `android:allowBackup` to **true**  and perform the following
additional steps:

1. If your app does **not** use its own custom `BackupAgent`, use the default [MAMBackupAgent]
to allow for automatic full backups that are Intune policy compliant.
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
See the following sections. Consider switching to using Intune's [MAMDefaultBackupAgent],
described in step 1, which provides easy back-up on Android M and above.

3. When you decide which type of full backup your app should receive (unfiltered, filtered, or none),
you'll need to set the attribute `android:fullBackupContent` to true, false, or an XML resource in your app.

4. Then, you _**must**_ copy the value for `android:fullBackupContent`
into the `com.microsoft.intune.mam.FullBackupContent` metadata tag
and for apps that support the new XML configuration format added in API 31, into the
`com.microsoft.intune.mam.DataExtractionRules` metadata tag.

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

The [Key/Value Backup](https://developer.android.com/guide/topics/data/keyvaluebackup.html) option is available to all APIs 8+ and uploads app data to the [Android Backup Service](https://developer.android.com/google/backup/index.html). The amount of data per user of your app is limited to 5 MB. If you use Key/Value Backup, you must use a [BackupAgentHelper] or a [BackupAgent].

### BackupAgentHelper

[BackupAgentHelper] is easier to implement than [BackupAgent] both in terms of native Android functionality and Intune MAM integration. BackupAgentHelper allows the developer to register entire files and shared preferences to a `FileBackupHelper` and `SharedPreferencesBackupHelper` (respectively) which are then added to the BackupAgentHelper upon creation. Follow the steps below to use a BackupAgentHelper with Intune MAM:

1. To utilize multi-identity backup with a `BackupAgentHelper`, follow the Android guide to [Extending BackupAgentHelper](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper).

2. Have your class extend the MAM equivalent of BackupAgentHelper, FileBackupHelper, and SharedPreferencesBackupHelper.

|Android class | MAM equivalent |
|--|--|
|BackupAgentHelper |[MAMBackupAgentHelper] |
|FileBackupHelper | [MAMFileBackupHelper]
|SharedPreferencesBackupHelper| [MAMSharedPreferencesBackupHelper]|

Following these guidelines will lead to a successful multi-identity backup and restore.

### BackupAgent

A BackupAgent allows you to be much more explicit about what data is backed up. Because the developer is fairly responsible for the implementation, there are more steps required to ensure appropriate data protection from Intune. Since most of the work is pushed onto you, the developer, Intune integration is slightly more involved.

**Integrate MAM:**

1. Carefully read the Android guide for [Key/Value Backup](https://developer.android.com/guide/topics/data/keyvaluebackup.html) and specifically [Extending BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) to ensure your BackupAgent implementation follows Android guidelines.

2. Have your class extend [MAMBackupAgent].

**Multi-identity Backup:**

1. Before beginning your backup, check that the files or data buffers you plan to back up are indeed **permitted by the IT administrator to be backed up** in multi-identity scenarios. We provide you with the `isBackupAllowed` function in [MAMFileProtectionManager] and [MAMDataProtectionManager] to determine this. If the file or data buffer is not allowed to be backed up, then you should not continue including it in your backup.

2. At some point during your backup, if you want to back up the identities for the files you checked in step 1, you must call `backupMAMFileIdentity(BackupDataOutput data, File … files)` with the files from which you plan to extract data. This will automatically create new backup entities and write them to the `BackupDataOutput` for you. These entities will be automatically consumed upon restore.

**Multi-identity Restore:**

The Data Backup guide specifies a general algorithm for restoring your application’s data and provides a code sample in the [Extending BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) section. In order to have a successful multi-identity restore, you must follow the general structure provided in this code sample with special attention to the following:

1. You must utilize a `while(data.readNextHeader())`* loop to go through the backup entities.

2. You must call `data.skipEntityData()`* if `data.getKey()`* does not match the key you wrote in `onBackup`. Without performing this step, your restores may not succeed.

3. Avoid returning while consuming backup entities in the `while(data.readNextHeader())`* construct, as the entities we automatically write will be lost.

* Where `data` is the local variable name for the **MAMBackupDataInput** that is passed to your app upon restore.

## Multi-Identity (optional)

### Overview
By default, the Intune App SDK will apply policy  to the app as a whole. Multi-identity is an optional Intune app protection feature that can be enabled to allow policy to be applied on a per-identity level. This requires significantly more app participation than other app protection features.

> [!NOTE]
> A lack of the correct app participation can result in data leaks and other security issues.

Once the user enrolls the device or the app, the SDK registers this identity and considers it the primary Intune managed identity. Other users in the app will be treated as unmanaged, with unrestricted policy settings.

> [!NOTE]
> Currently, only one Intune managed identity is supported per device.

An identity is defined as a string. Identities are case-insensitive, and requests to the SDK for an identity may not return the same casing that was originally used when setting the identity.

The app *must* inform the SDK when it intends to change the active
identity. In some cases, the SDK will also notify the app when an
identity change is required. In most cases, however, MAM cannot know
what data is being displayed in the UI or used on a thread at a given
time and relies on the app to set the correct identity in order to
avoid data leak. In the sections that follow, some particular
scenarios which require app action will be called out.

### Enabling Multi-Identity

By default, all apps are considered to be single-identity apps. You can declare an app to be multi-identity aware by placing the following metadata in AndroidManifest.xml.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### Setting the Identity

Developers can set the identity of the app user on the following levels in descending priority:

  1. Thread level
  2. `Context` (generally `Activity`) level
  3. Process level

An identity set at the thread level supersedes an identity set at the
`Context` level, which supersedes an identity set at the process
level. An identity set on a `Context` is only used in appropriate
associated scenarios. File IO operations, for example, do not have an
associated `Context`. Most commonly, apps will set the `Context` identity
on an `Activity`. An app *must* not display data for a managed identity
unless the `Activity` identity is set to that same identity. In
general, the process-level identity is only useful if the app works
only with a single user at a time on all threads. Many apps may not
need to make use of it.

If your app uses the `Application` context to acquire system services, ensure that the thread or process identity has been set, or
that you have set the UI identity on your app's `Application` context.

If your app uses a `Service` context to launch intents, use content resolvers, or leverage other system services be sure 
to set the identity on the `Service` context.

To handle special cases when updating the UI identity with [setUIPolicyIdentity] or [switchMAMIdentity], both methods can be passed
a set of **IdentitySwitchOption** values.

* `IGNORE_INTENT`: Use if requesting an identity switch that should ignore the intent associated with the current activity.
  For example:

  1. Your app receives an intent from a managed identity containing a managed document, and your app displays the document.
  2. The user switches to their personal identity, so your app requests a UI identity switch. In the personal identity, your app
     is no longer displaying the document, so you use `IGNORE_INTENT` when requesting the identity switch.
     
* `DATA_FROM_INTENT`: Use if requesting an identity switch when data
   from the intent will be displayed in the activity. The opposite of
   `IGNORE_INTENT`. This will cause the receive policy for the new
   identity to treat the intent as incoming data.
   
   For example: Your app receives an intent containing metadata that
   correlates it to a specific account. Your app requests an identity
   switch, but will be displaying data from the original intent.


If neither is set, the default behavior is somewhere in-between for
historical compatibility. MAM will assume that the most recent intent
is still being used in the app as with `DATA_FROM_INTENT`, however a
range of special conditions including the intent having been sent from
within the same app or from the system launcher will bypass data
ingress checking.

>[!NOTE]
> Because the `CLIPBOARD_SERVICE` is used for UI operations, the SDK uses the UI identity of the foreground activity for
> `ClipboardManager` operations.

The following methods in [MAMPolicyManager] may be used to set the identity and retrieve the identity values previously set.

```java
public static void setUIPolicyIdentity(final Context context, final String identity, final MAMSetUIIdentityCallback mamSetUIIdentityCallback,
final EnumSet<IdentitySwitchOption> options);

public static String getUIPolicyIdentity(final Context context);

public static MAMIdentitySwitchResult setProcessIdentity(final String identity);

public static String getProcessIdentity();

public static MAMIdentitySwitchResult setCurrentThreadIdentity(final String identity);

public static String getCurrentThreadIdentity();

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


public static AppPolicy getPolicyForIdentity(final String identity);

public static boolean getIsIdentityManaged(final String identity);
```

>[!NOTE]
> You can clear the identity of the app by setting it to null.
>
> The empty string may be used as an identity that will never have app protection policy.

#### Results
All the methods used to set the identity report back result values via **MAMIdentitySwitchResult**. There are four values that can be returned:

| Return value | Scenario |
|--            |--        |
| `SUCCEEDED`    | The identity change was successful. |
| `NOT_ALLOWED`  | The identity change is not allowed. This occurs if an attempt is made to set the UI (`Context`) identity when a different identity is set on the current thread. |
| `CANCELLED`    | The user canceled the identity change, generally by pressing the back button on a PIN or authentication prompt. |
| `FAILED`       | The identity change failed for an unspecified reason.|

The app should ensure that an identity switch is successful before
displaying or using corporate data. Currently, process and thread
identity switches will always succeed for a multi-identity-enabled
app, however we reserve the right to add failure conditions. The UI
identity switch may fail for invalid arguments, if it would conflict
with the thread identity, or if the user cancels out of conditional
launch requirements (for example, presses the back button on the PIN
screen). The default behavior for a failed UI identity switch on an
activity is to finish the activity (see `onSwitchMAMIdentityComplete`
below).

In the case of setting a `Context` identity via [setUIPolicyIdentity], the result is reported asynchronously. If the `Context` is an `Activity`, the SDK doesn't know if the identity change succeeded until after conditional launch is performed -- which may require the user to enter a PIN or corporate credentials. The app may implement a **MAMSetUIIdentityCallback** to receive this result, or may pass null for the callback object. Note that if a call is made to `setUIPolicyIdentity` while the result from a previous call to `setUIPolicyIdentity` *on the same context* has not yet been delivered, the new callback will supersede the old one and the original callback will never receive a result.

You can also set the identity of an activity directly through a method in [MAMActivity] instead of calling `MAMPolicyManager.setUIPolicyIdentity`. Use following method to do so:

```java
     public final void switchMAMIdentity(final String newIdentity, final EnumSet<IdentitySwitchOption> options);
```

You can also override a method in `MAMActivity` if you want the app to be notified of the result of attempts to change the identity of that activity.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

If you do not override `onSwitchMAMIdentityComplete` (or call the
`super` method), a failed identity switch on an activity will result
in the activity being finished. If you do override the method, you
must take care that corporate data is not displayed after a failed
identity switch.

>[!NOTE]
> Switching the identity may require recreating the activity. In this case, the `onSwitchMAMIdentityComplete` callback will be delivered to the new instance of the activity.


### Implicit Identity Changes

In addition to the app's ability to set the identity, a thread, or a context's identity may change based on data ingress from another Intune-managed app that has app protection policy.

#### Examples
1. If an activity is launched from an `Intent` sent by another MAM app, the activity's identity will be set based on the effective identity in the other app at the point the `Intent` was sent.

2. For services, the thread identity will be set similarly for the duration of an `onStart` or `onBind` call. Calls into the `Binder` returned from `onBind` will also temporarily set the thread identity.

3. Calls into a `ContentProvider` will similarly set the thread identity for their duration.


  In addition, user interaction with an activity may cause an implicit identity switch.

  **Example:** A user canceling out of an authorization prompt during `Resume` will result in an implicit switch to an empty identity.

  The app is given an opportunity to be made aware of these changes, and, if it must, the app can forbid them. [MAMService] and [MAMContentProvider] expose the following method that subclasses may override:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchResultCallback callback);
  ```

  In the `MAMActivity` class, an additional parameter is present in the method:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchReason reason,
          final AppIdentitySwitchResultCallback callback);
  ```

  * The **AppIdentitySwitchReason** captures the source of the implicit switch, and can accept the values `CREATE`, `RESUME_CANCELLED`, and `NEW_INTENT`.  The `RESUME_CANCELLED` reason is used when activity resume causes PIN, authentication, or other compliance UI to be displayed and the user attempts to cancel out of that UI, generally through use of the back button.


    * The **AppIdentitySwitchResultCallback** is as follows:

      ```java
      public interface AppIdentitySwitchResultCallback {
          /**
            * @param result
            *            whether the identity switch can proceed.
            */
          void reportIdentitySwitchResult(AppIdentitySwitchResult result);
        }
        ```

      Where **AppIdentitySwitchResult** is either `SUCCESS` or `FAILURE`.

The method `onMAMIdentitySwitchRequired` is called for all implicit identity changes except for those made through a Binder returned from `MAMService.onMAMBind`. The default implementations of `onMAMIdentitySwitchRequired` immediately call:

* `callback.reportIdentitySwitchResult(FAILURE)` when the reason is `RESUME_CANCELLED`.

* `callback.reportIdentitySwitchResult(SUCCESS)` in all other cases.

  It is not expected that most apps will need to block or delay an identity switch in a different manner, but if an app needs to do so, the following points must be considered:

  * If an identity switch is blocked, the result is the same as if `Receive` sharing settings had prohibited the data ingress.

  * If a Service is running on the main thread, `reportIdentitySwitchResult` **must** be called synchronously or the UI thread stops responding.

  * For `Activity` creation, **onMAMIdentitySwitchRequired** will be called before `onMAMCreate`. If the app must show UI to determine whether to allow the identity switch, that UI must be shown using a *different* activity.

  * In an `Activity`, when a switch to the empty identity is requested with the reason as `RESUME_CANCELLED`, the app must modify the resumed activity to display data consistent with that identity switch.  If this is not possible, the app should refuse the switch, and the user will be asked again to comply with policy for the resuming identity (for example, by being presented with the app PIN entry screen).

    > [!NOTE]
    > A multi-identity app will always receive incoming data from both managed and unmanaged apps. It is the responsibility of the app to treat data from managed identities in a managed manner.

  If a requested identity is managed (use [MAMPolicyManager.getIsIdentityManaged][getIsIdentityManaged] to check), but the app is not able to use that account (for example, because accounts, such as email accounts, must be set up in the app first) then the identity switch should be refused.

#### Build plugin / tool considerations
If you do not explicitly inherit from [MAMActivity], [MAMService], or
[MAMContentProvider] (because you allow the build tooling to make that
change), but still need to process identity switches, you may instead
implement **MAMActivityIdentityRequirementListener** for an `Activity` or
**MAMIdentityRequirementListener** for a `Service` or `ContentProviders`.
The default behavior for `MAMActivity.onMAMIdentitySwitchRequired` can be
accessed by calling the static method
`MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, identity,
reason, callback)`.

Similarly, if you need to override
`MAMActivity.onSwitchMAMIdentityComplete`, you may implement
`MAMActivityIdentitySwitchListener` without explicitly inheriting from
`MAMActivity`.

### Identity Switches and Screenshot Restrictions
MAM controls the `Window` flag `FLAG_SECURE` to enforce screenshot
policy. Some apps may also set `FLAG_SECURE` for their own
purposes. When MAM policy does not restrict screenshots, MAM will not
modify `FLAG_SECURE`. On transition from an identity whose policy
requires disabling screenshots to an identity whose policy does not,
MAM will clear `FLAG_SECURE`. Thus, the app should not rely on
`FLAG_SECURE` remaining set after an identity transition.

### Preserving Identity In Async Operations
It is common for operations on the UI thread to dispatch background tasks to another thread. A multi-identity app will want to make
sure that these background tasks operate with the appropriate identity, which is often the same identity used by the activity that
dispatched them. The MAM SDK provides [MAMAsyncTask] and [MAMIdentityExecutors] as a convenience to aid in preserving the identity.
These must be used if the asynchronous operation could write corporate data to a file or could communicate with other apps.

#### MAMAsyncTask

To use `MAMAsyncTask`, simply inherit from it instead of `AsyncTask` and replace overrides of `doInBackground` and `onPreExecute` with `doInBackgroundMAM` and `onPreExecuteMAM` respectively. The `MAMAsyncTask` constructor takes an activity context. For example:

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

### MAMIdentityExecutors
`MAMIdentityExecutors` allows you to wrap an existing `Executor` or `ExecutorService` instance as an identity-preserving `Executor`/`ExecutorService` with `wrapExecutor` and `wrapExecutorService` methods. For example

```java
Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

### File Protection
Every file has an identity associated with it at the time of creation, based on thread and process identity. This identity will be used for both file encryption and selective wipe. Only files whose identity is managed and has policy requiring encryption will be encrypted. The SDK's default selective functionality wipe will only wipe files associated with the managed identity for which a wipe has been requested. The app may query or change a file’s identity using the [MAMFileProtectionManager] class.

#### App Responsibility
MAM cannot automatically infer a relationship between files being read and
data being displayed in an `Activity`. Apps *must* set the UI identity
appropriately before displaying corporate data. This includes data
read from files. If a file comes from outside the app (either from a
`ContentProvider` or read from a publicly writable location), the app
*must* attempt to determine the file identity (using the correct
[MAMFileProtectionManager.getProtectionInfo][MAMFileProtectionManager] overload for the data source)
before displaying information read from the file. If `getProtectionInfo` reports a
non-null, non-empty identity, the UI identity *must* be set to match
this identity (using [MAMActivity.switchMAMIdentity][switchMAMIdentity] or
[MAMPolicyManager.setUIPolicyIdentity][setUIPolicyIdentity]). If the identity switch fails,
data from the file *must not* be displayed. When reading from a
content URI, it may be necessary to first read the identity (via the
`getProtectionInfo` overload taking a `Uri`), then set the context or
thread identity appropriately before opening a file descriptor or input
stream on the `ContentResolver` will succeed.

An example flow might look something like the following:
  * User selects a document to open in the app.
  * During the open flow, prior to reading data from disk, the app confirms the identity that should be used to display the content:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentity(activity, info.getIdentity(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

  * The app waits until a result is reported to callback.
  * If the reported result is a failure, the app does not display the document.
  * The app opens and renders the file.
  
If an app uses the Android `DownloadManager` to download files,
the MAM SDK will attempt to protect these files automatically using
the [identity priority described previously](#setting-the-identity).
The context used to retrieve the `DownloadManager` will be used if
the thread identity is unset. If the downloaded files contain corporate data,
it is the app's responsibility to call [protect] if the files are moved
or recreated after download.

#### Single-Identity to Multi-Identity Transition
If an app which previously released with single-identity Intune
integration later integrates multi-identity, previously installed apps
will experience a transition (not visible to the user, there is no
associated UX). The app is not *required* to do anything explicit to
handle this transition. All files created before the transition will
continue being regarded as managed (so they will stay encrypted if
encryption policy is on). If desired, you can detect the upgrade and
use [MAMFileProtectionManager.protect][protect] to tag specific files or
directories with the empty identity (which will remove encryption if
they were encrypted).

#### Offline Scenarios
File identity tagging is sensitive to offline mode. The following points should be taken into account:

* If the Company Portal is not installed, files cannot be identity-tagged.

* If the Company Portal is installed, but the app does not have Intune MAM policy, files cannot be reliably tagged with identity.

* When file identity tagging becomes available, all previously created files are treated as personal/unmanaged (belonging to the empty-string identity) unless the app was previously installed as a single-identity managed app in which case they are treated as belonging to the enrolled user.

### Directory Protection

Directories may be protected using the same [protect] method used to protect files. Directory protection applies recursively to all files and subdirectories contained in the directory, and to new files created within the directory. Because directory protection is applied recursively, the `protect` call can take some time to complete for large directories. For that reason, apps applying protection to a directory that contains a large number of files might wish to run `protect` asynchronously on a background thread.

### Data Protection

It is not possible to tag a file as belonging to multiple identities. Apps that must store data belonging to different users in the same file can do so manually, using the features provided by [MAMDataProtectionManager]. This allows the app to encrypt data and tie it to a particular user. The encrypted data is suitable for storing to disk in a file. You can query the data associated with the identity and the data can be unencrypted later.

Apps that make use of [MAMDataProtectionManager] should implement a receiver for the
`MANAGEMENT_REMOVED` notification. After this notification completes, buffers that were protected via this class will no longer be readable if file encryption was
enabled when the buffers were protected. An app can remediate this situation by calling
`MAMDataProtectionManager.unprotect` on all buffers during this notification. It
is also safe to call protect during this notification if it is desired to preserve identity
information (encryption is guaranteed to be disabled during the notification).


### Content Providers

If the app provides corporate data other than a `ParcelFileDescriptor` through a `ContentProvider`, the app must call the method `isProvideContentAllowed(String)` in [MAMContentProvider], passing the owner identity's UPN (user principal name) for the content. If this function returns false, the content *must not* be returned to the caller. File descriptors returned through a content provider are handled automatically based on the file identity.

If you do not inherit `MAMContentProvider` explicitly and instead
allow the build tooling to make that change, you may call a
static version of the same method:
`MAMContentProvider.isProvideContentAllowed(provider, contentIdentity)`.

### Selective Wipe

If a multi-identity app registers for the **WIPE_USER_DATA**
notification, it is the app's responsibility to remove all data for
the user being wiped, including all files that have been
identity-tagged as belonging to that user. If the app removes user
data from a file but wishes to leave other data in the file, it *must*
change the identity of the file (via
[MAMFileProtectionManager.protect][protect] to a personal user or the empty
identity). If encryption policy is in use, any remaining files
belonging to the user being wiped will not be decrypted and will
become inaccessible to the app after wipe.

An app registering for `WIPE_USER_DATA` will not receive the benefit
of the SDK's default selective wipe behavior. For multi-identity aware
apps, this loss may be more significant since MAM default selective
wipe will wipe only files whose identity is targeted by a wipe. If a
multi-identity aware application wishes MAM default selective wipe to
be done _**and**_ wishes to perform its own actions on wipe, it should
register for **WIPE_USER_AUXILIARY_DATA MAMNotificationType** notifications. This
notification will be sent immediately by the SDK before it performs
the MAM default selective wipe. An app should never register for both
`WIPE_USER_DATA` and `WIPE_USER_AUXILIARY_DATA`.

The default selective wipe will close the app gracefully, finishing activities and killing the app
process. If your app overrides the default selective wipe, you may want to consider closing your
app manually to prevent the user from accessing in-memory data after a wipe occurs.


## Enabling MAM targeted configuration for your Android applications (optional)
Application-specific key-value pairs may be configured in the Intune
console for [MAM](../apps/app-configuration-policies-managed-app.md)
and [Android Enterprise](../apps/app-configuration-policies-use-android.md).
These key-value pairs are not interpreted by Intune at all,
but are passed on to the app. Applications that want to
receive such configuration can use the **MAMAppConfigManager** and
**MAMAppConfig** classes to do so. If multiple policies are targeted at
the same app, there may be multiple conflicting values available for
the same key.

> [!NOTE] 
> Configurations setup for delivery via App Configuration Policies (ACP) can not be delivered in `offline` (when the Company Portal is not installed).  Only Android Enterprise AppRestrictions will be delivered via a `MAMUserNotification` on an empty identity in this case.

### Get the App Config For a User
App config may be retrieved as follows:
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
```

If there is no MAM-registered user, but your app would still like to
retrieve Android Enterprise configuration (which will not be targeted at
a specific user), you can pass a null or empty string.

### Conflicts
A value set in MAM app config will override a value with the same key
set in Android Enterprise config. 

If an admin configures conflicting values for the same key (e.g by
targeting different app config sets with the same key to multiple
groups containing the same user), Intune does not have any way of
resolving this conflict automatically and will make all values
available to your app. 

Your app can request all values for a given key from a **MAMAppConfig** object:
```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

or request a value to be chosen:
```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)
```

Your app can also request the raw data as a list of sets of key-value pairs.

```java
List<Map<String, String>> getFullData()
```


### Full Example
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = null;
if (appConfig.hasConflict("foo")) {
    List<String> values = appConfig.getAllStringsForKey("foo");
    fooValue = chooseBestValue(values);
} else {
    valueToUse = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
}
Long barValue = appConfig.getIntegerForKey("bar", MAMAppConfig.NumberQueryType.Min);
```

### Notification
App config adds a new notification type:
* **REFRESH_APP_CONFIG**: This notification is sent in a **MAMUserNotification** and informs the app that new app config data is available.

### Further Reading
For more information about how to create a MAM targeted app configuration policy in Android, see the section on MAM targeted app config in [How to use Microsoft Intune app configuration policies for Android](../apps/app-configuration-policies-managed-app.md).

App config can also be configured using the Graph API. For information, see the [Graph API docs for MAM Targeted Config](/graph/api/resources/intune-mam-targetedmanagedappconfiguration).

## Custom Themes (optional)
A custom theme can be provided to the MAM SDK which will be applied to all MAM screens and dialogs. If a theme is not provided, a default MAM theme will be used.

### How to provide a theme
To provide a theme, you need to add the following line of code in the `Application.onCreate` method:

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

In the above example, you need to replace `R.style.AppTheme` with the style theme that you want the SDK to apply.

## Style Customization (deprecated)

This is now deprecated and Custom Themes (above) is the preferred way of customizing views.

Views generated by the MAM SDK can be visually customized to more closely match the app in which it is integrated. You can customize primary, secondary, and background colors, as well as the size of the app logo. This style customization is optional and defaults will be used if no custom style is configured.


### How to customize
In order to have style changes apply to the Intune MAM views, you must first create a style override XML file. This file should be placed in the "/res/xml" directory of your app and you may name it whatever you like. Below is an example of the format this file needs to follow.

```xml
<?xml version="1.0" encoding="utf-8"?>
<styleOverrides>
    <item
        name="foreground_color"
        resource="@color/red"/>
    <item
        name="accent_color"
        resource="@color/blue"/>
    <item
        name="background_color"
        resource="@color/green"/>
    <item
        name="logo_image"
        resource="@drawable/app_logo"/>
</styleOverrides>
```

You must reuse resources that already exist within your app. For example, you must define the color green in the colors.xml file and reference it here. You cannot use the Hex color code "#0000ff". The maximum size for the app logo is 110 dip (dp). You may use a smaller logo image, but adhering to the maximum size will yield the best looking results. If you exceed the 110 dip limit, the image will scale down and possibly cause blurring.

Below is the complete list of allowed style attributes, the UI elements they control, their XML attribute item names, and the type of resource expected for each.

|Style attribute | UI elements affected | Attribute item name | Expected resource type |
| -- | -- | -- | -- |
| Background color | PIN screen background color <Br>PIN box fill color | background_color | Color |
| Foreground color | Foreground text color <br> PIN box border in default state <br> Characters (including obfuscated characters) in PIN box when user enters a PIN| foreground_color | Color|
| Accent color | PIN box border when highlighted <br> Hyperlinks |accent_color | Color |
| App logo | Large icon that appears in the Intune app PIN screen | logo_image | Drawable |

## Default enrollment (optional)

The following is guidance for requiring user prompt on app launch for an automatic APP-WE service enrollment (we call this **default enrollment** in this section), requiring Intune app protection policies to allow only Intune protected users to use your SDK-integrated Android LOB app. It also covers how to enable SSO for your SDK-integrated Android LOB app. This is **not** supported for store apps that can be used by non-Intune users.

> [!NOTE] 
> The benefits of **default enrollment** include a simplified method of obtaining policy from APP-WE service for an app on the device.

> [!NOTE] 
> **Default enrollment** is sovereign cloud aware.

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

   > [!NOTE] 
   > This forces the user to download the Company Portal on the device and complete the default enrollment flow before use.


## Limitations

### Policy enforcement limitations

* **Using Content Resolvers**: The "transfer or receive" Intune policy may block or partially block the use of a content resolver to
access the content provider in another app. This will cause `ContentResolver` methods to return null or throw a failure value (for
example, `openOutputStream` will throw `FileNotFoundException` if blocked). The app can determine whether a failure to write data
through a content resolver was caused by policy (or would be caused by policy) by making the call:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    or if there is no associated activity:

    ```java
      MAMPolicyManager.getCurrentThreadPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    In this second case, multi-identity apps must take care to set the thread identity appropriately (or pass an explicit identity to a `getPolicyForIdentity` call).

### Exported services
The AndroidManifest.xml file included in the Intune App SDK contains **MAMNotificationReceiverService**, which must be an exported service to allow the Company Portal to send notifications to a managed app. The service checks the caller to ensure that only the Company Portal is allowed to send notifications.

### Reflection limitations
Some of the MAM base classes (for example, `MAMActivity`, `MAMDocumentsProvider`)
contain methods (based on the original Android base classes) which use
parameter or return types only present above certain API levels. For
this reason, it may not always be possible to use reflection to
enumerate all methods of app components. This restriction is not
limited to MAM, it is the same restriction that would apply if the
app itself implemented these methods from the Android base classes.

### Robolectric
Testing MAM SDK behavior under Robolectric is not supported. There are
known issues running the MAM SDK under Robolectric due to behaviors
present under Robolectric that do not accurately mimic those on real
devices or emulators.

If you need to test your application under Robolectric, the
recommended workaround is to move your application class logic to a
helper and produce your unit-testing apk with an application class
that does not inherit from MAMApplication.

## Expectations of the SDK consumer

The Intune SDK maintains the contract provided by the Android API, though failure conditions may be triggered more frequently as a result of policy enforcement. These Android best practices will reduce the likelihood of failure:

* Android SDK functions that may return null have a higher likelihood of being null now.  To minimize issues, ensure that null checks are in the right places.

* Features that can be checked for must be checked for through their MAM replacement APIs.

* Any derived functions must call through to their super class versions.

* Avoid use of any API in an ambiguous way. For example, using `Activity.startActivityForResult` without checking the requestCode will cause strange behavior.

### Services
Policy enforcement may affect service interactions.
Methods that establish a bound service connection such as `Context.bindService` may fail due to underlying policy enforcement in `Service.onBind` and
may result in `ServiceConnection.onNullBinding` or `ServiceConnection.onServiceDisconnected`.
Interacting with an established bound service may throw a `SecurityException` due to policy enforcement in `Binder.onTransact`.

## Telemetry

The Intune App SDK for Android does not control data collection from your app. The Company Portal application logs system-generated data by default. This data is sent to Microsoft Intune. As per Microsoft Policy, we do not collect any personal data.

> [!NOTE]
> If end users choose not to send this data, they must turn off telemetry under Settings on the Company Portal app. To learn more, see [Turn off Microsoft usage data collection](../user-help/turn-off-microsoft-usage-data-collection-android.md). 

## Recommended Android best practices

* All library projects should share the same `android:package` where possible. This will not sporadically fail in run-time; this is purely a build-time problem. Newer versions of the Intune App SDK will remove some of the redundancy.

* Use the newest Android SDK build tools.

* Remove all unnecessary and unused libraries (for example, android.support.v4)

## Testing
See the [Testing Guide](app-sdk-android-testing-guide.md).

<!-- Class links -->
[BackupAgent]: https://developer.android.com/reference/android/app/backup/BackupAgent
[BackupAgentHelper]: https://developer.android.com/reference/android/app/backup/BackupAgentHelper
[MAMActivity]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html
[MAMActivityIdentitySwitchListener]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivityIdentitySwitchListener.html
[MAMApplication]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMApplication.html
[MAMAsyncTask]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMAsyncTask.html
[MAMBackupAgent]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMBackupAgent.html
[MAMBackupAgentHelper]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMBackupAgentHelper.html
[MAMContentProvider]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/content/MAMContentProvider.html
[MAMDataProtectionManager]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMDataProtectionManager.html
[MAMDefaultBackupAgent]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMDefaultBackupAgent.html
[MAMFileBackupHelper]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMFileBackupHelper.html
[MAMFileProtectionManager]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMFileProtectionManager.html
[MAMIdentityExecutors]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMIdentityExecutors.html
[MAMPolicyManager]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html
[MAMService]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMService.html
[MAMSharedPreferencesBackupHelper]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/backup/MAMSharedPreferencesBackupHelper.html

<!-- Method links -->
[getIsIdentityManaged]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html#getIsIdentityManaged(java.lang.String)
[protect]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMFileProtectionManager.html#protect(android.os.ParcelFileDescriptor,%20java.lang.String)
[setUIPolicyIdentity]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/identity/MAMPolicyManager.html#setUIPolicyIdentity(android.content.Context,%20java.lang.String,%20com.microsoft.intune.mam.client.identity.MAMSetUIIdentityCallback,%20java.util.EnumSet%3Ccom.microsoft.intune.mam.client.app.IdentitySwitchOption%3E)
[switchMAMIdentity]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html#switchMAMIdentity(java.lang.String,%20java.util.EnumSet%3Ccom.microsoft.intune.mam.client.app.IdentitySwitchOption%3E)
[MAMActivity.onMAMCompanyPortalRequired]: https://msintuneappsdk.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html#onMAMCompanyPortalRequired(java.lang.String)

<!-- Intune -->
["Give your app access to the Intune app protection service (optional)"]: ./app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional

<!-- Azure Active Directory -->
[Microsoft Azure Active Directory]: /azure/active-directory/fundamentals/active-directory-whatis
[Register your application with Azure Active Directory]: /azure/active-directory/active-directory-app-registration
[AAD redirect URI]: /azure/active-directory/develop/msal-client-application-configuration#redirect-uri

<!-- ADAL -->
[ADAL]: /azure/active-directory/azuread-dev/active-directory-authentication-libraries

<!-- MSAL-->
[MSAL]: /azure/active-directory/develop/reference-v2-libraries
[MSAL repository on GitHub]: https://github.com/AzureAD/microsoft-authentication-library-for-android
[MSAL Wiki]: https://github.com/AzureAD/microsoft-authentication-library-for-android/wiki
[Overview of Microsoft Authentication Library (MSAL)]: /azure/active-directory/develop/msal-overview
[Update your applications to use Microsoft Authentication Library (MSAL)]: https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363
[Migrate Android ADAL to MSAL]: /azure/active-directory/develop/migrate-android-adal-msal
[Differences between ADAL and MSAL]: /azure/active-directory/develop/msal-overview#differences-between-adal-and-msal
[Using MSAL]: https://github.com/AzureAD/microsoft-authentication-library-for-android#using-msal
[Configure MSAL to use a broker]: /azure/active-directory/develop/brokered-auth#configure-msal-to-use-a-broker
[`IAccount`]: https://github.com/AzureAD/microsoft-authentication-library-for-android/blob/dev/msal/src/main/java/com/microsoft/identity/client/IAccount.java
[`IAuthenticationResult`]: https://github.com/AzureAD/microsoft-authentication-library-for-android/blob/dev/msal/src/main/java/com/microsoft/identity/client/IAuthenticationResult.java

<!-- Sovereign Cloud -->
[sovereign cloud aware]: https://www.microsoft.com/trustcenter/cloudservices/nationalcloud
[MSAL configuration file]: /azure/active-directory/develop/msal-configuration#multiple_clouds_supported
