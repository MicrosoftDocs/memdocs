---
# required metadata

title: Wrap Android apps with the Intune App Wrapping Tool 
description: Learn how to wrap your Android apps without changing the code of the app itself. Prepare the apps so you can apply mobile app management policies.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: e9c349c8-51ae-4d73-b74a-6173728a520b

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

# Prepare Android apps for app protection policies with the Intune App Wrapping Tool

Use the Microsoft Intune App Wrapping Tool for Android to change the behavior of your in-house Android apps by restricting features of the app without changing the code of the app itself.

The tool is a Windows command-line application that runs in PowerShell and creates a wrapper around your Android app. After the app is wrapped, you can change the app's functionality by configuring [mobile application management policies](../apps/app-protection-policies.md) in Intune.

Before running the tool, review [Security considerations for running the App Wrapping Tool](#security-considerations-for-running-the-app-wrapping-tool). To download the tool, go to the [Microsoft Intune App Wrapping Tool for Android](https://github.com/microsoftconnect/intune-app-wrapping-tool-android) on GitHub.

> [!NOTE]
> If you have issues with using the Intune App Wrapping Tool with your apps, submit a [request for assistance](https://github.com/microsoftconnect/intune-app-wrapping-tool-android/issues) on GitHub.

## Fulfill the prerequisites for using the App Wrapping Tool

- Your app must use up-to-date libraries
  
- Your app must be compatible with the [Google Play requirements](https://developer.android.com/google/play/requirements/target-sdk)
  
- If your app is complex, it must integrate with the [Intune App SDK for Android](../developer/app-sdk-android-phase1.md)

- You must run the App Wrapping Tool on a Windows computer running Windows 10 or later.

- Your input app must be a valid Android application package with the file extension .apk and:

  - It cannot be encrypted.
  - It must not have previously been wrapped by the Intune App Wrapping Tool.
  - It must be written for Android 9.0 or later.

  > [!NOTE]
  > If your input app is an Android App Bundle (.aab), you will need to convert it to an APK before using the Intune App Wrapping Tool. For details, see [Convert Android App Bundle (AAB) to APK](#convert-android-app-bundle-aab-to-apk). As of August 2021, [new private apps can still be published to the Google Play Store as APKs](https://support.google.com/googleplay/work/answer/6145139?hl=en).
  
- The app must be developed by or for your company. You cannot use this tool on apps that are available in the Google Play Store. This includes downloading or obtaining the app from the Google Play Store.

- To run the App Wrapping Tool, you must install the latest version of the [Java Runtime Environment](https://java.com/download/) and then ensure that the Java path variable has been set to C:\ProgramData\Oracle\Java\javapath in your Windows environment variables. For more help, see the [Java documentation](https://java.com/en/download/help/index.html).

    > [!NOTE]
    > In some cases, the 32-bit version of Java may result in memory issues. It's a good idea to install the 64-bit version.

- Android requires all app packages (.apk) to be signed. For **reusing** existing certificates and overall signing certificate guidance, see [Reusing signing certificates and wrapping apps](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps). After you have wrapped the .apk file using the Intune App Wrapping Tool, the recommendation is to use [Google's provided Apksigner tool]( https://developer.android.com/studio/command-line/apksigner). This will ensure that once your app gets to end user devices, it can be launched properly by Android standards.

- (Optional) Sometimes an app may hit the Dalvik Executable (DEX) size limit due to the Intune MAM SDK classes that are added during wrapping. DEX files are a part of the compilation of an Android app. The Intune App Wrapping Tool automatically handles DEX file overflow during wrapping for apps with a min API level of 21 or higher (as of [v. 1.0.2501.1](https://github.com/microsoftconnect/intune-app-wrapping-tool-android/releases)). For apps with a min API level of < 21, best practice would be to increase the min API level using the wrapper's `-UseMinAPILevelForNativeMultiDex` flag. For customers unable to increase the app's minimum API level, the following DEX overflow workarounds are available. In certain organizations, this may require working with whoever compiles the app (ie. the app build team):

  - Use ProGuard to eliminate unused class references from the app's primary DEX file.
  - For customers using v3.1.0 or higher of the Android Gradle plugin, disable the [D8 dexer](https://android-developers.googleblog.com/2018/04/android-studio-switching-to-d8-dexer.html).  

## How often should I rewrap my Android application with the Intune App Wrapping Tool?

The main scenarios in which you would need to rewrap your applications are as follows:

- The application itself has released a new version. The previous version of the app was wrapped and uploaded to the Microsoft Intune admin center.

- The Intune App Wrapping Tool for Android has released a new version that enables key bug fixes, or new, specific Intune application protection policy features. This happens every 6-8 weeks through GitHub repo for the [Microsoft Intune App Wrapping Tool for Android](https://github.com/microsoftconnect/intune-app-wrapping-tool-android).

Some best practices for rewrapping include:

- Maintaining signing certificates used during the build process, see [Reusing signing certificates and wrapping apps](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps)

## Install the App Wrapping Tool

1. From the [GitHub repository](https://github.com/microsoftconnect/intune-app-wrapping-tool-android), download the installation file InstallAWT.exe for the Intune App Wrapping Tool for Android to a Windows computer. Open the installation file.

2. Accept the license agreement, then finish the installation.

Note the folder to which you installed the tool. The default location is: C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool.

## Run the App Wrapping Tool

> [!IMPORTANT]
> Intune regularly releases updates to the Intune App Wrapping Tool. Regularly check the [Intune App Wrapping Tool for Android](https://github.com/microsoftconnect/intune-app-wrapping-tool-android) for updates and incorporate into your software development release cycle to ensure your apps support the latest App Protection Policy settings.

1. On the Windows computer where you installed the App Wrapping Tool, open a PowerShell window.

2. From the folder where you installed the tool, import the App Wrapping Tool PowerShell module:

   ```PowerShell
   Import-Module .\IntuneAppWrappingTool.psm1
   ```

3. Run the tool by using the **invoke-AppWrappingTool** command, which has the following usage syntax:

   ```PowerShell
   Invoke-AppWrappingTool [-InputPath] <String> [-OutputPath] <String> [<CommonParameters>]
   ```

   The following table details the properties of the **invoke-AppWrappingTool** command:

|Property|Information|
|-------------|--------------------|
|**-InputPath**&lt;String&gt;|Path of the source Android app (.apk).|
 |**-OutputPath**&lt;String&gt;|Path to the output Android app. If this is the same directory path as InputPath, the packaging will fail.|
| **&lt;CommonParameters&gt;** | (Optional) The command supports common PowerShell parameters like verbose and debug. |


- For a list of common parameters, see the [Microsoft Script Center](/powershell/module/microsoft.powershell.core/about/about_commonparameters?view=powershell-7&preserve-view=true).

- To see detailed usage information for the tool, enter the command:

    ```PowerShell
    Help Invoke-AppWrappingTool
    ```

**Example:**

Import the PowerShell module.

```PowerShell
Import-Module "C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool\IntuneAppWrappingTool.psm1"
```

Run the App Wrapping Tool on the native app HelloWorld.apk.

```PowerShell
invoke-AppWrappingTool -InputPath .\app\HelloWorld.apk -OutputPath .\app_wrapped\HelloWorld_wrapped.apk -Verbose
```

The wrapped app and a log file are generated and saved in the output path you specified.

## Reusing signing certificates and wrapping apps

Android requires that all apps must be signed by a valid certificate in order to be installed on Android devices.

Wrapped apps can be signed *after* wrapping using your existing signing tools (any signing information in the app before wrapping is discarded). If possible, the signing information that was already used during the build process should be used during wrapping. In certain organizations, this may require working with whoever owns the keystore information (ie. the app build team).

If the previous signing certificate cannot be used, or the app has not been deployed before, you may create a new signing certificate by following the instructions in the [Android Developer Guide](https://developer.android.com/studio/publish/app-signing.html#signing-manually).

If the app has been deployed previously with a different signing certificate, the app can't be uploaded to Intune after upgrade. App upgrade scenarios will be broken if your app is signed with a different certificate than the one the app is built with. As such, any new signing certificates should be maintained for app upgrades. 

## Security considerations for running the App Wrapping Tool

To prevent potential spoofing, information disclosure, and elevation of privilege attacks:

- Ensure that the input line-of-business (LOB) application, and the output application are on the same Windows computer where the App Wrapping Tool is running.

- Import the output application to Intune on the same machine where the tool is running. See [keytool](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/keytool.html) for more about the Java keytool.

- If the output application and the tool are on a Universal Naming Convention (UNC) path and you are not running the tool and input files on the same computer, set up the environment to be secure by using [Internet Protocol Security (IPsec)](https://wikipedia.org/wiki/IPsec) or [Server Message Block (SMB) signing](https://support.microsoft.com/kb/887429).

- Ensure that the application is coming from a trusted source.

- Secure the output directory that has the wrapped app. Consider using a user-level directory for the output.

## Convert Android App Bundle (AAB) to APK

The Intune App Wrapping Tool currently only supports APK inputs. Android App Bundles must first be converted to an APK for use with the tool.

An Android App Bundle can be converted to an APK using [Google's command line tool, `bundletool`](https://developer.android.com/studio/command-line/bundletool). The latest version of `bundle-tool` can be downloaded from Google's [bundletool GitHub repo](https://github.com/google/bundletool/releases).

`bundletool` can be used to produce a single universal APK for use with the Intune App Wrapping Tool using the following command:

```
bundletool build-apks --bundle=input.aab --mode=universal --output=input.apks
```

The `.apks` output file is a ZIP archive containing a single universal APK file. Unzip the archive and use that APK file as input to the Intune App Wrapping Tool.

## See also

- [Decide how to prepare apps for mobile application management with Microsoft Intune](../developer/apps-prepare-mobile-application-management.md)

- [Microsoft Intune App SDK for Android developer guide](../developer/app-sdk-android-phase1.md)
