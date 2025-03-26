---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide - MSAL Prerequisite
description: Understand the MSAL prerequisite to incorporate Intune mobile app management (MAM) into your Android app.
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

# Intune App SDK for Android - Understand the MSAL Prerequisite

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Stage 1: Plan the Integration].

## Stage 2: The MSAL Prerequisite

## Stage Goals

- Register your application with Microsoft Entra ID.
- Integrate MSAL into your Android application.
- Verify that your application can obtain a token that grants access to protected resources.

## Background

The [Microsoft Authentication Library (MSAL)] gives your application the ability to use the Microsoft Cloud by supporting [Microsoft Entra ID] and [Microsoft accounts].  

MSAL *isn't* specific to Intune.
Intune has a dependency on Microsoft Entra ID; all Intune user accounts are Microsoft Entra accounts.
**As a result, the vast majority of Android applications that integrate the Intune App SDK will need to integrate MSAL as a prerequisite.**

This stage of the SDK guide overviews the MSAL integration process as it relates to Intune; **follow the linked MSAL guides in their entirety**.

To simplify the Intune App SDK integration process, **Android app developers are strongly encouraged to fully integrate and test MSAL before downloading the Intune App SDK.**
The Intune App SDK integration process *does* require code changes around MSAL token acquisition.
It will be easier to test the Intune-specific token acquisition changes if you have already confirmed your app's original token acquisition implementation works as expected.

To learn more about Microsoft Entra ID, see [What is Microsoft Entra ID?]

To learn more about MSAL, see the [MSAL Wiki] and [list of MSAL libraries].

## Register your Application with Microsoft Entra ID

Before integrating MSAL into your Android application, all apps are required to register with the Microsoft identity platform. Follow the steps in [Quickstart: Register an app in the Microsoft identity platform - Microsoft identity platform].
This generates a **Client ID** for your application.

Next, follow the instructions to [give your app access to the Intune Mobile App Management service].

## Configure Microsoft Authentication Library (MSAL)

First, read the MSAL integration guidelines found in the [MSAL repository on GitHub], specifically the section [using MSAL].

This guide describes how to:

- Add MSAL as a dependency to your Android application.
- Create an MSAL configuration file.
- Configure your application's `AndroidManifest.xml`.
- Add code to acquire a token.

### Brokered Authentication

Single sign-on (SSO) allows users to only enter their credentials once and have those credentials automatically work across applications.
MSAL can enable SSO across your suite of apps; by using a broker application (either the Microsoft Authenticator or Microsoft Intune Company Portal), you can extend SSO across the entire device.
Brokered authentication is also required for Conditional Access.
See [Enable cross-app SSO on Android using MSAL] for more details on brokered authentication.

This guide assumes that you're enabling brokered authentication within your application(s) following the steps at the link above, especially [Generate a redirect URI for a broker] and [Configure MSAL to use a broker] for configuration and [Verify broker integration] for testing.

**If you are not enabling brokered authentication in your application, pay extra attention to [Intune-specific MSAL configuration]**.

### Intune-specific MSAL environment configuration

By default, Intune will request tokens from the Microsoft Entra public environment. If your application requires a non-default environment,
such as a Sovereign cloud, the following setting must be added to your application's `AndroidManifest.xml`.
When set, the Microsoft Entra authority entered will issue the tokens for your application.
This ensures Intune's authentication policy is properly enforced.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
```

> [!CAUTION]
> **Most apps should not set the Authority parameter.** Additionally, applications that do not integrate MSAL **must not** include
> this property in the manifest.

For more detail on non-Intune-specific MSAL configuration options, see [Android Microsoft Authentication Library configuration file].

For more detail on Sovereign clouds, see [Use MSAL in a national cloud environment].

## Exit Criteria

- Have you integrated MSAL into your application?
- Have you enabled broker authentication by generating a redirect URI and setting it in the MSAL configuration file?
- Have you configured the Intune-specific MSAL settings in the `AndroidManifest.xml`?
- Have you tested brokered authentication, confirmed that a work account is added to Android's Account Manager, and tested SSO with other Microsoft 365 apps?
- If you implemented Conditional Access, have you tested both device-based CA and app-based CA to validate your CA implementation?

## FAQ

### What about ADAL?

Microsoft's previous authentication library, [Azure Active Directory Authentication Library (ADAL)], is **deprecated**.

If your application has already integrated ADAL, see [Update your applications to use Microsoft Authentication Library (MSAL)].
To migrate your app from ADAL to MSAL, see [Migrate Android ADAL to MSAL] and [Differences between ADAL and MSAL].

**It is recommended to migrate from ADAL to MSAL prior to integrating the Intune App SDK.**

## Next Steps

After you've completed all the [Exit Criteria] above, continue to [Stage 3: Getting Started with MAM].

<!-- Stage 2 links -->
<!-- internal links -->
[Intune-specific MSAL configuration]:#intune-specific-msal-environment-configuration
[Exit Criteria]:#exit-criteria

<!-- Other SDK Guide Markdown documentation -->
[Stage 1: Plan the Integration]:app-sdk-android-phase1.md
[Stage 3: Getting Started with MAM]:app-sdk-android-phase3.md

<!-- Microsoft Learn documentation: AAD -->
[Microsoft Entra ID]:https://azure.microsoft.com/services/active-directory/
[Microsoft accounts]:https://account.microsoft.com/
[What is Microsoft Entra ID?]:/azure/active-directory/fundamentals/active-directory-whatis
[Quickstart: Register an app in the Microsoft identity platform - Microsoft identity platform]:/azure/active-directory/active-directory-app-registration

<!-- Microsoft Learn documentation: MSAL-->
[Microsoft Authentication Library (MSAL)]:/azure/active-directory/develop/msal-overview
[list of MSAL libraries]:/azure/active-directory/develop/reference-v2-libraries
[MSAL Wiki]:https://github.com/AzureAD/
[using MSAL]: https://github.com/AzureAD/microsoft-authentication-library-for-android#using-msal
[Enable cross-app SSO on Android using MSAL]:/azure/active-directory/develop/msal-android-single-sign-on
[Generate a redirect URI for a broker]:/azure/active-directory/develop/msal-android-single-sign-on#generate-a-redirect-uri-for-a-broker
[Configure MSAL to use a broker]:/azure/active-directory/develop/brokered-auth#configure-msal-to-use-a-broker
[Verify broker integration]:/azure/active-directory/develop/msal-android-single-sign-on#verify-broker-integration
[Use MSAL in a national cloud environment]:/azure/active-directory/develop/msal-national-cloud
[Android Microsoft Authentication Library configuration file]:/azure/active-directory/develop/msal-configuration
[MSAL repository on GitHub]: https://github.com/AzureAD/microsoft-authentication-library-for-android

<!-- Microsoft Learn documentation: ADAL -->
[Azure Active Directory Authentication Library (ADAL)]:/azure/active-directory/azuread-dev/active-directory-authentication-libraries

<!-- Microsoft Learn documentation: ADAL to MSAL -->
[Update your applications to use Microsoft Authentication Library (MSAL)]:https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363
[Migrate Android ADAL to MSAL]:/azure/active-directory/develop/migrate-android-adal-msal
[Differences between ADAL and MSAL]:/azure/active-directory/develop/msal-overview#differences-between-adal-and-msal

<!-- Microsoft Learn documentation -->
[give your app access to the Intune Mobile App Management service]:/mem/intune-service/developer/app-sdk-get-started#give-your-app-access-to-the-intune-mobile-app-management-service
