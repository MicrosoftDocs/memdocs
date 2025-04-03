---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide - Get started with MAM
description: Get started with Intune before incorporating Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/14/2024
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

# Intune App SDK for Android - Get started with MAM

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Stage 1: Plan the Integration].

## Stage 3: Getting Started with MAM

## Stage Goals

- Download the Intune App SDK.
- Learn what files are included in the Intune App SDK.
- Reference the Intune App SDK in your application.
- Configure the Intune App Gradle Build Plugin OR utilize the command line build tool.
- Confirm that the Intune App SDK is properly included in your build.

## Background

Now that your application has successfully integrated MSAL, it's time to download the Intune App SDK and include it in your application's build process.

A large portion of integrating the Intune App SDK is replacing standard Android classes and method calls with Intune versions of those classes and method calls.
The SDK includes build tooling that automatically makes most of these replacements for you.
If you'd like to learn more about this replacement logic, see the [class and method replacements] section of the [appendix].

## Download the Intune App SDK

To download the SDK, see [Download the SDK files].

## What's in the SDK?

The Intune App SDK consists of the following files:

- **Microsoft.Intune.MAM.SDK.aar**: The SDK components, except for the Support Library JAR files.
- **com.microsoft.intune.mam.build.jar**: A Gradle plugin, which [aids in integrating the SDK].
- **CHANGELOG.md**: Provides a record of changes made in each SDK version.
- **THIRDPARTYNOTICES.TXT**:  An attribution notice that acknowledges third-party and/or OSS code that will be compiled into your app.
- **Microsoft.Intune.MAM.SDK.DownlevelStubs.aar**: This AAR contains
  stubs for Android system classes that are present only on newer
  devices but that are referenced by methods in [MAMActivity]. Newer
  devices ignore these stub classes. This AAR is necessary only
  if your app performs reflection on classes deriving from
  `MAMActivity`, and **most apps do not need to include it**. The AAR
  contains ProGuard rules to exclude all its classes.

## Referencing Intune App libraries

The Intune App SDK is a standard Android library with no external dependencies.
**Microsoft.Intune.MAM.SDK.aar** contains both the interfaces necessary for enabling app protection policies and the code necessary to interoperate with the Microsoft Intune Company Portal app.

### Android Studio

**Microsoft.Intune.MAM.SDK.aar** must be specified as an Android library reference. To add this dependency to your build, follow [Add your AAR or JAR as a dependency] from Android documentation.

### Visual Studio

The [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)
NuGet package must be added as a dependency.

Follow the process for [Install and manage packages in Visual Studio using the NuGet Package Manager](/nuget/consume-packages/install-use-packages-visual-studio).

The **Microsoft.Intune.MAM.SDK.aar** is bound to create C# references that are scoped to the `Microsoft.Intune.Mam` namespace.

### ProGuard

Your application may already use [ProGuard] (or any other shrinking/obfuscation mechanism) as a build step.
The Intune App SDK has ProGuard configuration rules that must be included in that build step.
Including the *.AAR* in your build, as described above, automatically integrates the SDK's configuration into the ProGuard step, so the necessary class files are kept. If you've properly included the *.AAR*, no other change is needed.

The [Microsoft Authentication Library (MSAL)] ships with its own ProGuard configuration. If your app integrates MSAL, refer to the [MSAL documentation] for more detail.

## Build tooling

The SDK provides build tools (a plugin for Gradle builds, targets for .NET builds, and a command-line tool) that perform MAM replacements automatically.
These tools transform the class files generated by Java compilation; they don't modify the original source code.
**You're required to use either the Gradle plugin, .NET NuGet package, or command-line tool.**

**The build tooling alone is not sufficient to fully integrate your application.**
The tools perform [class and method replacements] only.
They don't perform any more complex SDK integrations such as [Multi-Identity], [Registering for App Protection Policy], [Policy for limiting data transfer between apps and device or cloud storage locations], or [MSAL configuration], which must be completed before your app is fully Intune enabled.
Carefully review the rest of this documentation for integration points relevant to your app.

### Impact on debugging

The build tooling performs replacements after compilation, which will change some method names.
As a result, debugging breakpoints set on method names may be impacted and not halt as expected.
Line number breakpoints are unaffected.

### MAM in the Stack

Because the Intune App SDK integration relies heavily on class and method replacements, you'll start seeing `mam` throughout your stack traces.
When your app doesn't have with an account targeted with app protection policies, all this MAM code lies dormant: `MAMActivity` will work identical to `Activity`, `onMAMCreate` will work identical to `onCreate`, etc.
Whenever you see `mam` in a stack, first check:

- Is the account targeted with app protection policies?
- Is the Intune Company Portal installed?

Unless the answer to both is "yes", the MAM code is acting as simple passthrough.

### What tool do I need?

If you build your app with Gradle, see [Integrating with the Gradle Build Plugin]

If you build your app with [.NET MAUI](https://dotnet.microsoft.com/apps/maui), see [Integrating with the .NET MAUI Targets].

If you build your app with neither of the above, see [Integrating with the Command Line Tool].

## Integrating with the Gradle Build Plugin

The Intune App SDK plugin is distributed as part of the SDK as
**GradlePlugin/com.microsoft.intune.mam.build.jar**.

In order for the plugin to be recognized by Gradle, it must be added to the `buildscript` classpath.
The plugin depends on [Javassist], which must also be added. For more information on the Javassist dependency, see [Dependencies].

To add these to the classpath, add the following to your root `build.gradle`:

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.29.2-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Then, to apply the plugin, add the following to the `build.gradle` file for your app and dynamic feature modules:

```groovy
apply plugin: 'com.microsoft.intune.mam'
```

By default, the plugin operates on `project` dependencies and external libraries.
Test compilation isn't affected.

> [!NOTE]
> Beginning with the 8.0 Intune App SDK, it's no longer possible to process libraries selectively. All libraries are processed.

### Dependencies

> [!NOTE]
> You must be using version 3.6.1 or newer of the Android Gradle plugin and version 5.6.4 or newer of Gradle.

The Gradle plugin has a dependency on [Javassist], which must be made available to Gradle's dependency resolution.
**Javassist is used solely at build time when running the plugin and no Javassist code will be added to your app.**

> [!NOTE]
> Javassist versions may not be backwards compatible.
> Generally, you should use the exact version expected by the Intune App SDK:
>
> - Intune App SDK ≥ 10.0.0 requires Javassist 3.29.2-GA
> - Intune App SDK ≥ 7.0.0 requires Javassist 3.27.0-GA
> - Intune App SDK < 7.0.0 requires Javassist 3.22.0-GA

Additionally, when consuming MAM SDK 8.0.0+, you must ensure the following is set in your Gradle configuration:

```groovy
compileOptions {
  sourceCompatibility JavaVersion.VERSION_1_8
  targetCompatibility JavaVersion.VERSION_1_8
}
```

### Exclusions

Additional configurations may be provided to exclude specific components in your app from rewrites.
Exclusions are predominantly useful for components that aren't relevant for MAM (i.e. don't handle or display corporate data).

Exclusions can be configured for varying scopes:

- `excludeProjects` allows excluding a list of Gradle projects. These exclusions are
  useful for projects that don't interface with Android libraries or system APIs and/or
  don't handle corporate data. For example, a project that exclusively contains native code
  for performing low-level network operations might be a good candidate. If a project
  broadly interfaces with Android libraries or system APIs, these exclusions should be
  avoided.
- `excludeClasses` allows excluding a list of classes. These exclusions are useful
  for classes that don't handle or present corporate data. For example, splash
  screens and onboarding `Activity`s are good candidates. Note that a class can't
  be excluded if any of its superclasses are processed.
- `excludeVariants` enables excluding project variants. These exclusions can refer to
  either a complete variant name or a single flavor. They're especially useful
  if you want to build a non-MAM flavor of your app.
  For example, if your app has build types `debug` and `release` with flavors {`noMAM`, `MAM`} and {`mock`, `production`} you could specify the following:
  - `noMAM` to exclude all variants with the noMAM flavor or
  - `noMAMMockDebug` to exclude only that exact variant.

> [!CAUTION]
> Exclusions should not be taken lightly.
> Incorrectly applying exclusions can result in serious data leaks in your app.
> Always validate the impact of any exclusion you apply.

#### Example partial build.gradle with exclusions

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
    excludeVariants = ['noMAM']
}
```

This would have the following effects:

- `:product:FooLib` isn't rewritten because it's included in `excludeProjects`
- `:product:foo-project` is rewritten, except for `com.contoso.SplashActivity`, which is skipped because it's in `excludeClasses`
- `com.microsoft.bar:baz.1.0.0` is rewritten because all external libraries are included for processing.
- Variants with the `noMAM` flavor aren't rewritten.

### Reporting

The build plugin can generate an html report of the changes it makes.
To request generation of this report, specify `report = true` in the `intunemam` configuration block.
If generated, the report will be written to `outputs/logs` in the build directory.

```groovy
intunemam {
    report = true
}
```

### Verification

The build plugin can run additional verification to look for possible errors in processing classes.
These checks help to safeguard against potential plugin-induced runtime failures.

To request verification is performed in your build, specify `verify = true` in the `intunemam` configuration block.
This may add several seconds to the time taken by the plugin's task.

```groovy
intunemam {
    verify = true
}
```

Generally, a verification failure represents a bug in the build plugin.
For assistance with a failure, escalate the issue with Microsoft support.
If you don't have a Microsoft support contract, [open a GitHub issue][MAM SDK GitHub issues].

### Incremental builds

To enable support for building incrementally, specify `incremental = true`
in the `intunemam` configuration block.
This feature increases build performance by processing only the input files that have changed.
The default configuration for `incremental` is `false`.

```groovy
intunemam {
    incremental = true
}
```

### Dynamic Feature Module configuration

Dynamic Feature Modules build separately from the app project. As such, Dynamic Feature Modules also need to apply the Gradle Build Plugin.

Due to technical limitations in the APIs used by the Gradle plugin, app classes need to be reprocessed when transforming dynamic feature module classes. To ensure that this can be done, all feature modules should be configured with the same settings as the app it is designed for.

For example, if an app excludes a class, the dynamic feature module should also exclude that class.

## Integrating with the .NET MAUI Targets

The Intune App SDK targets are distributed as part of the SDK as
**Microsoft.Intune.Maui.Essentials.android.targets**.

The targets will be automatically imported into your application at compile time once the
[Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android) NuGet package is added.

## Integrating with the Command Line Build Tool

The command-line build tool is available in the `BuildTool` folder of the SDK drop.
It performs the same function as the Gradle plugin/.NET targets detailed above, but can be integrated into custom build systems.
As it's more generic, it's more complex to invoke, so the Gradle plugin / .NET targets should be used whenever possible.

### Using the Command-Line Tool

The command-line tool can be invoked by using the provided helper scripts
located in the `BuildTool\bin` directory.

The tool expects the following parameters.

| Parameter          | Required | Description                                                                                                                                                                      |
| --                 | --       | --                                                                                                                                                                               |
| `--input`          | Yes      | A semi-colon delimited list of jar files and directories of class files to modify. This should include all jars/directories that you intend to rewrite.                          |
| `--output`         | Yes      | A semi-colon delimited list of jar files and directories to store the modified classes to. There should be one output entry per input entry, and they should be listed in order. |
| `--classpath`      | Yes      | The build classpath. This may contain both jars and class directories.                                                                                                           |
| `--processed`      | No       | A semi-colon delimited list of jar files and directories containing classes that have already been processed by a previous invocation of the build tool.                   |
| `--excludeClasses` | No       | A semi-colon delimited list containing the names of the classes that should be excluded from rewriting.                                                                          |
| `--report`         | No       | Directory to write an HTML report about modified classes to. If not specified, no report is written.                                                                             |

The optional `--processed` option is used to enable incremental builds.
The set of files/directories listed here should be disjoint with the input and classpath lists.

> [!TIP]
> On Unix-like systems semi-colon is a command separator.
> To avoid the shell from splitting commands, make sure to escape each semi-colon with '\' or wrap the full parameter in quotation marks.

### Example Command-Line Tool invocation

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

This would have the following effects:

- the `product-foo-project` directory is rewritten to `mam-build\product-foo-project`
- `bar.jar` is rewritten to `mam-build\libs\bar.jar`
- `zap.jar` is **not** rewritten because it's only listed in `--classpath`
- The `com.contoso.SplashActivity` class is **not** rewritten even if it's in `--input`

> [!WARNING]
> The build tool does not currently support aar files.
> If your build system does not already extract `classes.jar` when dealing with aar files, you will need to do so before invoking the build tool.

## Setting MAMApplication

If your app creates a subclass of `android.app.Application`, then the build plugin / command line tool will transform your application class.

If your app doesn't subclass `android.app.Application`, then you **must** set `"com.microsoft.intune.mam.client.app.MAMApplication"` as the `"android:name"` attribute in your AndroidManifest.xml's `<application>` tag.

## Recommended Android best practices

- Use the newest Android SDK build tools.
- Remove all unnecessary and unused libraries (for example, android.support.v4).

After performing automatic replacements, the Intune App SDK still maintains the contract provided by the Android API.
However, failure conditions may be triggered more frequently as a result of policy enforcement.
These Android best practices will reduce the likelihood of failure:

- Android SDK functions that can return `null` now have a higher likelihood of returning `null`. Ensure that `null` checks protect these function calls.
- Features that can be checked for, such as `clipboardManager.getPrimaryClipDescription()`, must be checked for through their MAM replacement APIs, such as `MAMClipboard.getPrimaryClipDescription(clipboardManager)`.
- Any derived functions must call through to their super class versions.
- Avoid use of any API in an ambiguous way. For example, using `Activity.startActivityForResult` without checking the `requestCode` will cause strange behavior.

### Services

Policy enforcement may affect Android [Service] interactions.
Methods that establish a bound service connection such as `Context.bindService` may fail due to underlying policy enforcement in `Service.onBind` and may result in `ServiceConnection.onNullBinding` or `ServiceConnection.onServiceDisconnected`.
Interacting with an established bound service may throw a `SecurityException` due to policy enforcement in `Binder.onTransact`.

Clients of bound services are strongly encouraged to check for exceptions thrown by the service rather than letting exceptions propagate to the rest of the client application.

## Exit Criteria

After you've either configured the build plugin or integrated the command line tool into your build process, validate that it's running successfully:

- Ensure that your build compiles and builds successfully.
- Configure the `report` flag, then open the report document and confirm class and method replacements are occurring:
  - If using the plugin, follow the steps in [Reporting].
  - If using the command line tool, include the `--report` flag.
- If using the plugin, configure the `verify` flag and ensure it doesn't produce errors. See [Verification].
- Double check all exclusions (`excludeProjects`, `excludeClasses`, and `excludeVariants`) in build.gradle. Confirm that each exclusion is necessary and doesn't deal with protected data. Historically many data leak errors have occurred because of over-aggressive exclusions.
- *Without the Intune Company Portal installed*, launch your compiled app, login with a Microsoft Entra user that isn't targeted with App Protection Policy, and confirm that app functions as expected.
  - Logout and repeat this test *with* the Intune Company Portal installed.

## FAQ

### My app previously integrated the SDK without the build plugin; how can I use the build plugin?

Older versions of the Intune App SDK didn't include any automated way to perform class and method replacements, and developers needed to perform these replacements manually in source code.
If your app had previously integrated this way, it's safe to apply the build plugin (or command line build tool) without any source code modifications.
Your project must still list the MAM SDK as a dependency.

## Next Steps

After you've completed all the [Exit Criteria], continue to [Stage 4: MAM Integration Essentials].

<!-- Stage 3 links -->
<!-- internal links -->
[Dependencies]:#dependencies
[aids in integrating the SDK]:#build-tooling
[Integrating with the Gradle Build Plugin]:#integrating-with-the-gradle-build-plugin
[Integrating with the .NET MAUI Targets]:#integrating-with-the-net-maui-targets
[Integrating with the Command Line Tool]:#integrating-with-the-command-line-build-tool
[Exit Criteria]:#exit-criteria
[Reporting]:#reporting
[Verification]:#verification

<!-- Other SDK Guide Markdown documentation -->
[Stage 1: Plan the Integration]:app-sdk-android-phase1.md
[MSAL configuration]:app-sdk-android-phase2.md
[Registering for App Protection Policy]:app-sdk-android-phase4.md#registering-for-app-protection-policy
[Stage 4: MAM Integration Essentials]:app-sdk-android-phase4.md
[Multi-Identity]:app-sdk-android-phase5.md
[Policy for limiting data transfer between apps and device or cloud storage locations]:app-sdk-android-phase7.md#policy-for-limiting-data-transfer-between-apps-and-device-or-cloud-storage-locations
[appendix]:app-sdk-android-appendix.md
[class and method replacements]:app-sdk-android-appendix.md#class-and-method-replacements

<!-- Microsoft Learn documentation -->
[Download the SDK files]:/mem/intune-service/developer/app-sdk-get-started#download-the-sdk-files
[Microsoft Authentication Library (MSAL)]:/azure/active-directory/develop/msal-overview#languages-and-frameworks
[MSAL documentation]:https://github.com/AzureAD/microsoft-authentication-library-for-android

<!-- MAM SDK GitHub -->
[MAM SDK GitHub issues]:https://github.com/microsoftconnect/ms-intune-app-sdk-android/issues

<!-- Class links -->
[MAMActivity]:https://microsoftconnect.github.io/ms-intune-app-sdk-android/reference/com/microsoft/intune/mam/client/app/MAMActivity.html

<!-- 3rd party links -->
[ProGuard]:https://www.guardsquare.com/products/proguard
[Javassist]:https://jboss-javassist.github.io/javassist/
[Service]:https://developer.android.com/reference/android/app/Service
[Add your AAR or JAR as a dependency]: https://developer.android.com/studio/projects/android-library#psd-add-aar-jar-dependency
