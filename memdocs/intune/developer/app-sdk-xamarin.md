---
# required metadata

title: Microsoft Intune App SDK Xamarin Bindings 
description: The Intune App SDK Xamarin Bindings enable Intune app protection policy in iOS and Android apps built with Xamarin. 
keywords: sdk, Xamarin, intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/06/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 275d574b-3560-4992-877c-c6aa480717f4


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune, has-adal-ref
ms.collection:
- tier3
- M365-identity-device-management
---

# Microsoft Intune App SDK Xamarin Bindings

> [!NOTE]
> The current Xamarin bindings for Android platform only support apps targeting Android 9.0 and lower and Xamarin Forms 4.4 and lower. Microsoft is working on improving support for newer versions on Android starting Q2CY2023. We anticipate having a beta release for .NET MAUI support available in March 2023. For more information about migrating your apps from Xamarin Forms to .NET MAUI, see [Migrate your app from Xamarin.Forms](/dotnet/maui/get-started/migrate). 

> [!NOTE]
> You may wish to first read the [Get Started with Intune App SDK](app-sdk-get-started.md) article, which explains how to prepare for integration on each supported platform.

## Overview
The [Intune App SDK Xamarin Bindings](https://github.com/msintuneappsdk/intune-app-sdk-xamarin) enable [Intune app protection policy](../apps/app-protection-policy.md) in iOS and Android apps built with Xamarin. The bindings allow developers to easily build in Intune app protection features into their Xamarin-based app.

The Microsoft Intune App SDK Xamarin Bindings let you incorporate Intune app protection policies (also known as APP or MAM policies) into your apps developed with Xamarin. A MAM-enabled application is one that is integrated with the Intune App SDK. IT administrators can deploy app protection policies to your mobile app when Intune actively manages the app.

## What's supported?

### Developer machines
* Windows (Visual Studio version 15.7+)
* macOS

### Mobile app platforms
* Android
* iOS

### Intune Mobile Application Management scenarios

* Intune [MAM](../apps/android-deployment-scenarios-app-protection-work-profiles.md#mam)
* Intune MDM-enrolled devices
* Third-party EMM-enrolled devices

Xamarin apps built with the Intune App SDK Xamarin Bindings can now receive Intune app protection policies on both Intune mobile device management (MDM) enrolled devices and unenrolled devices.

## Prerequisites

Review the [license terms](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20Xamarin%20Component.pdf). Print and retain a copy of the license terms for your records. By downloading and using the Intune App SDK Xamarin Bindings, you agree to such license terms. If you do not accept them, do not use the software.

The Intune SDK relies on [Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/v2-overview) for its [authentication](/azure/active-directory/develop/authentication-vs-authorization) and conditional launch scenarios, which require apps to be configured with [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis). 

If your application is already configured to use MSAL, and has its own custom client ID used to authenticate with Azure Active Directory, ensure the steps to give your Xamarin app permissions to the Intune Mobile Application Management (MAM) service are followed. Use the instructions in the "[Give your app access to the Intune app protection service](app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional)" section of the [getting started with the Intune SDK guide](app-sdk-get-started.md).

## Security Considerations

To prevent potential spoofing, information disclosure, and elevation of privilege attacks:

* Ensure that Xamarin app development is performed on a secure work station.
* Ensure the bindings are from a valid Microsoft source:
  * [MS Intune App SDK NuGet Profile](https://www.nuget.org/profiles/msintuneappsdk)
  * [Intune App SDK Xamarin GitHub Repository](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)
* Configure your NuGet config for your project to trust signed, unmodified NuGet packages.
See [installing signed packages](/nuget/consume-packages/installing-signed-packages)
for more information.
* Secure the output directory that contains the Xamarin app. Consider using a user-level directory for the output.


## Enabling Intune app protection policies in your iOS mobile app

> [!IMPORTANT]
> Intune regularly releases updates to the Intune App SDK. Regularly check the [Intune App SDK Xamarin Bindings](https://github.com/msintuneappsdk/intune-app-sdk-xamarin) for updates and incorporate into your software development release cycle to ensure your apps support the latest App Protection Policy settings.

1. Add the [Microsoft.Intune.MAM.Xamarin.iOS NuGet package](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.iOS) to your Xamarin.iOS project.
2. Follow the general steps required for integrating the Intune App SDK into an iOS mobile app. You can begin with step 3 of the integration instructions from the [Intune App SDK for iOS Developer Guide](app-sdk-ios.md#build-the-sdk-into-your-mobile-app). You can skip the final step in that section of running the IntuneMAMConfigurator, as this tool is included in the Microsoft.Intune.MAM.Xamarin.iOS package and will be run automatically at build time.
    **Important**: Enabling keychain sharing for an app is slightly different in Visual Studio from Xcode. Open the app's Entitlements plist and make sure the "Enable Keychain" option is enabled and the appropriate keychain sharing groups are added in that section. Then, ensure the Entitlements plist is specified in the "Custom Entitlements" field of the project's "iOS Bundle Signing" options for all the appropriate Configuration/Platform combinations.
3. Once the bindings are added and the app is properly configured, your app can begin using the Intune SDK's APIs. To do so, you must include the following namespace:

      ```csharp
      using Microsoft.Intune.MAM;
      ```

4. To begin receiving app protection policies, your app must enroll in the Intune MAM service. If your app does not use [Microsoft Authentication Library](https://www.nuget.org/packages/Microsoft.Identity.Client) (MSAL) to authenticate users, and you'd like the Intune SDK to handle authentication, your app should provide the user's UPN to the IntuneMAMEnrollmentManager's LoginAndEnrollAccount method:

      ```csharp
       IntuneMAMEnrollmentManager.Instance.LoginAndEnrollAccount([NullAllowed] string identity);
      ```

      Apps may pass in null if the user's UPN is unknown at the time of the call. In this case, users will be prompted to enter both their email address and password.
      
      If your app already uses MSAL to authenticate users, you can configure a single-sign-on (SSO) experience between your app and the Intune SDK. First, you'll need to override the default AAD settings used by the Intune SDK with those of your app. You can do so via the IntuneMAMSettings dictionary in the app's Info.plist, as mentioned in the [Intune App SDK for iOS Developer Guide](app-sdk-ios.md#configure-settings-for-the-intune-app-sdk), or you can do so in code via the AAD override properties of the IntuneMAMSettings class. The Info.plist approach is recommended for applications whose MSAL settings are static while the override properties are recommended for applications that determine those values at runtime. Once all of the SSO settings have been configured, your app should provide the user's UPN to the IntuneMAMEnrollmentManager's RegisterAndEnrollAccount method after it has successfully authenticated:

      ```csharp
      IntuneMAMEnrollmentManager.Instance.RegisterAndEnrollAccount(string identity);
      ```

      Apps can determine the result of an enrollment attempt by implementing the EnrollmentRequestWithStatus method in a subclass of IntuneMAMEnrollmentDelegate and setting the IntuneMAMEnrollmentManager's Delegate property to an instance of that class. 

      Upon a successful enrollment, apps can determine the UPN of the enrolled account (if previously unknown) by querying the following property: 

      ```csharp
       string enrolledAccount = IntuneMAMEnrollmentManager.Instance.EnrolledAccount;
      ```      
### Sample Applications
Sample applications highlighting MAM functionality in Xamarin.iOS apps are available on [GitHub](https://github.com/msintuneappsdk/sample-intune-xamarin-ios).

> [!NOTE] 
> There is no remapper for iOS/iPadOS. Integrating into a Xamarin.Forms app should be the same as for a regular Xamarin.iOS project. 

## Enabling Intune app protection policies in your Android mobile app
1. Add the [Microsoft.Intune.MAM.Xamarin.Android NuGet package](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.Android) to your Xamarin.Android project.
    1. For a Xamarin.Forms app, add the [Microsoft.Intune.MAM.Remapper.Tasks NuGet package](https://www.nuget.org/packages/Microsoft.Intune.MAM.Remapper.Tasks) to your Xamarin.Android project as well. 
2. Follow the general steps required for [integrating the Intune App SDK](app-sdk-android.md) into an Android mobile app while referring to this document for additional details.

### Xamarin.Android integration

A complete overview for integrating the Intune App SDK can be found in the [Microsoft Intune App SDK for Android developer guide](app-sdk-android.md). As you read through the guide and integrate the Intune App SDK with your Xamarin app the following sections are intended to highlight differences between the implementation for a native Android app developed in Java and a Xamarin app developed in C#. These sections should be treated as supplemental and cannot act as a substitute for reading the guide in its entirety.

#### Remapper
Beginning with the 1.4428.1 release, the `Microsoft.Intune.MAM.Remapper` package can be added to a Xamarin.Android application as [build tooling](app-sdk-android.md#build-tooling) to perform the MAM class, method, and systems services replacements. If the Remapper is included, the MAM equivalent replacement portions of the Renamed Methods and MAM Application sections will be automatically performed when the application is built.

To exclude a class from MAM-ification by the Remapper the following property can be added in your projects `.csproj` file.

```xml
  <PropertyGroup>
    <ExcludeClasses>Semicolon separated list of relative class paths to exclude from MAM-ification</ExcludeClasses>
  </PropertyGroup>
```

> [!NOTE]
> The Remapper currently prevents debugging in Xamarin.Android apps. Manual integration is recommended to debug your application.

#### [Renamed Methods](app-sdk-android.md#renamed-methods)
In many cases, a method available in the Android class has been marked as final in the MAM replacement class. In this case, the MAM replacement class provides a similarly named method (suffixed with `MAM`) that you should override instead. For example, when deriving from `MAMActivity`, instead of overriding `OnCreate()` and calling `base.OnCreate()`, `Activity` must override `OnMAMCreate()` and call `base.OnMAMCreate()`.

#### [MAM Application](app-sdk-android.md#mamapplication)
Your app must define an `Android.App.Application` class. If manually integrating MAM, it must inherit from `MAMApplication`. Be sure that your subclass is properly decorated with the `[Application]` attribute and overrides the `(IntPtr, JniHandleOwnership)` constructor.

```csharp
    [Application]
    class TaskrApp : MAMApplication
    {
    public TaskrApp(IntPtr handle, JniHandleOwnership transfer)
        : base(handle, transfer) { }
```

> [!NOTE]
> An issue with the MAM Xamarin bindings can cause the application to crash when deployed in Debug mode. As a workaround, the `Debuggable=false` attribute must be added to the `Application` class and the `android:debuggable="true"` flag must be removed from the manifest if it was manually set.

#### [Enable features that require app participation](app-sdk-android.md#enable-features-that-require-app-participation)
Example: Determine if PIN is required for the app

```csharp
MAMPolicyManager.GetPolicy(currentActivity).IsPinRequired;
```

Example: Determine the primary Intune user

```csharp
IMAMUserInfo info = MAMComponents.Get<IMAMUserInfo>();
return info?.PrimaryUser;
```

Example: Determine if saving to device or cloud storage is permitted

```csharp
MAMPolicyManager.GetPolicy(currentActivity).GetIsSaveToLocationAllowed(SaveLocation service, String username);
```

#### [Register for notifications from the SDK](app-sdk-android.md#register-for-notifications-from-the-sdk)
Your app must register for notifications from the SDK by creating a `MAMNotificationReceiver` and registering it with `MAMNotificationReceiverRegistry`. This is done by providing the receiver and the type of notification desired in `App.OnMAMCreate`, as the example below illustrates:

```csharp
public override void OnMAMCreate()
{
    // Register the notification receivers
    IMAMNotificationReceiverRegistry registry = MAMComponents.Get<IMAMNotificationReceiverRegistry>();
    foreach (MAMNotificationType notification in MAMNotificationType.Values())
    {
        registry.RegisterReceiver(new ToastNotificationReceiver(this), notification);
    }
    ...
```

#### [MAM Enrollment Manager](app-sdk-android.md#mamenrollmentmanager)

```csharp
IMAMEnrollmentManager mgr = MAMComponents.Get<IMAMEnrollmentManager>();
```

### Xamarin.Forms integration

For `Xamarin.Forms` applications the `Microsoft.Intune.MAM.Remapper` package performs MAM class replacement automatically by injecting `MAM` classes into the class hierarchy of commonly used `Xamarin.Forms` classes. 

> [!NOTE]
> The Xamarin.Forms integration must be done in addition to the Xamarin.Android integration detailed above. The Remapper behaves differently for Xamarin.Forms apps, so the manual MAM replacements must still be done.

Once the Remapper is added to your project you will need to perform the MAM equivalent replacements. For example, `FormsAppCompatActivity` and `FormsApplicationActivity` can continue to be used in your application provided overrides to `OnCreate` and `OnResume` are replaced with the MAM equivalents `OnMAMCreate` and `OnMAMResume` respectively.

```csharp
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        protected override void OnMAMCreate(Bundle savedInstanceState)
        {
            base.OnMAMCreate(savedInstanceState);
            global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
            LoadApplication(new App());
        }
```

If the replacements are not made then you may encounter the following compilation errors until you make the replacements:
* [Compiler Error CS0239](/dotnet/csharp/misc/cs0239). This error is commonly seen in this form
``'MainActivity.OnCreate(Bundle)': cannot override inherited member 'MAMAppCompatActivityBase.OnCreate(Bundle)' because it is sealed``.
This is expected because when the Remapper modifies the inheritance of Xamarin classes, certain functions will be made `sealed` and a new MAM variant is added to override instead.
* [Compiler Error CS0507](/dotnet/csharp/language-reference/compiler-messages/cs0507): This error is commonly seen in this form ``'MyActivity.OnRequestPermissionsResult()' cannot change access modifiers when overriding 'public' inherited member ...``. When the Remapper changes the inheritance of some of the Xamarin classes, certain member functions will be changed to `public`. If you override any of these functions, you will need to change those the access modifiers for those overrides to be `public` as well.

> [!NOTE]
> The Remapper re-writes a dependency that Visual Studio uses for IntelliSense auto-completion. Therefore, you may need to reload and rebuild the project when the Remapper is added for IntelliSense to correctly recognize the changes.

#### Troubleshooting
* If you encounter a blank, white screen in your application on launch, then you may need to force the navigation calls to execute on the main thread.
* The Intune SDK Xamarin Bindings do not support apps that are using a cross-platform framework such as MvvmCross due to conflicts between MvvmCross and Intune MAM classes. While some customers may have had success with integration after moving their apps to plain Xamarin.Forms, we do not provide explicit guidance or plugins for app developers using MvvmCross.

### Company Portal app
The Intune SDK Xamarin Bindings rely on the presence of the [Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) Android app on the device to enable app protection policies. The Company Portal retrieves app protection policies from the Intune service. When the app initializes, it loads policy and code to enforce that policy from the Company Portal. The user does not need to be signed in.

> [!NOTE]
> When the Company Portal app is not on the **Android** device, an Intune-managed app behaves the same as a normal app that does not support Intune app protection policies.

For app protection without device enrollment, the user is _**not**_ required to enroll the device by using the Company Portal app.

### Sample Applications
Sample applications highlighting MAM functionality in Xamarin.Android and Xamarin.Forms apps are available on [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Xamarin-Android-Apps).

## Support
If your organization is an existing Intune customer, please work with your Microsoft support representative to open a support ticket and create an issue [on the GitHub issues page](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/issues). We will help as soon as we can.
