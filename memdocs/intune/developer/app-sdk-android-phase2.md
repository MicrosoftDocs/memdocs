---
# required metadata

title: Microsoft Intune App SDK for Android developer integration and testing guide - MSAL Prerequisite
description: Understand the MSAL prerequisite to incorporate Intune mobile app management (MAM) into your Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2023
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
- tier3
- M365-identity-device-management
- Android
ms.custom: intune-classic
---

# Intune App SDK for Android - Understand the MSAL Prerequisite

The Microsoft Intune App SDK for Android lets you incorporate Intune app protection policies (also known as **APP** or MAM policies) into your native Java/Kotlin Android app. An Intune-managed application is one that is integrated with the Intune App SDK. Intune administrators can easily deploy app protection policies to your Intune-managed app when Intune actively manages the app.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Plan the Integration](..\developer\app-sdk-android-phase1.md).

## Stage 2: The MSAL Prerequisite

## Stage Goals

- Register your application with Azure Active Directory (AAD).
- Integrate MSAL into your Android application.
- Verify that your application can obtain a token that grants access to protected resources.

## Background

The [Microsoft Authentication Library (MSAL)] gives your application the ability to use the Microsoft Cloud by supporting [Microsoft Azure Active Directory (AAD)] and [Microsoft accounts].  

MSAL *isn't* specific to Intune.
Intune has a dependency on AAD; all Intune user accounts are AAD accounts.
**As a result, the vast majority of Android applications that integrate the Intune App SDK will need to integrate MSAL as a prerequisite.**

This stage of the SDK guide overviews the MSAL integration process as it relates to Intune; **follow the linked MSAL guides in their entirety**.

To simplify the Intune App SDK integration process, **Android app developers are strongly encouraged to fully integrate and test MSAL before downloading the Intune App SDK.**
The Intune App SDK integration process *does* require code changes around MSAL token acquisition.
It will be significantly easier to test the Intune-specific token acquisition changes if you have already confirmed your app's original token acquisition implementation works as expected.

To learn more about AAD, see [What is Azure Active Directory?]

To learn more about MSAL, see the [MSAL Wiki] and [list of MSAL libraries].

## Register your Application with AAD

Before integrating MSAL into your Android application, follow the instructions to [register your application with Azure Active Directory].
This will generate a **Client ID** for your application.

Next, follow the instructions to [give your app access to the Intune app protection service].

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

### Intune-specific MSAL configuration

Intune has up to four settings you may need to add to your application's `AndroidManifest.xml`.
These settings help ensure that Intune's authentication policy can be properly enforced and prevent unnecessary authentication prompts for end users.

These settings include:

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
```

| Setting | Description | Required for MSAL? | Required by Intune? |
| - | - | - | - |
| `ClientID`             | The AAD ClientID (also known as the "Application ID") for your app. <br> There's no default `ClientID`. Use the `ClientID` from [Register your Application with AAD] for your app. |  Yes | No |
| `Authority`            | The AAD authority to issue a token. <br> By default, this value is the AAD public environment. If overridden, the AAD authority entered will issue the token for your application, which allows authentication to nondefault environments, such as Sovereign clouds. | No | If your application requires a nondefault authority, yes. **Most apps should not set the Authority parameter.** |
| `SkipBroker`           | Boolean value for altering the default MSAL SSO behavior. <br> By default, this value is "false". | No | If your app doesn't support brokered authentication/device-wide SSO, yes and set `SkipBroker` to "true". **Most apps should not set the SkipBroker parameter.** |
| `NonBrokerRedirectURI` | [AAD redirect URI] to use in broker-less cases. By default, this value isn't present. | No | If the `SkipBroker` setting is set to "true" and your app requires a redirect URI, yes. **Most apps should not set the NonBrokerRedirectURI parameter.** |

> [!CAUTION]
> Applications that do not integrate MSAL **must not** include any of these 4 properties in the manifest.

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
[Register your Application with AAD]:#register-your-application-with-aad
[Intune-specific MSAL configuration]:#intune-specific-msal-configuration
[Exit Criteria]:#exit-criteria

<!-- Other SDK Guide Markdown documentation -->
[Stage 1: Planning the Integration]:app-sdk-android-phase1.md
[Stage 3: Getting Started with MAM]:app-sdk-android-phase3.md

<!-- Microsoft Learn documentation: AAD -->
[Microsoft Azure Active Directory (AAD)]:https://azure.microsoft.com/services/active-directory/
[Microsoft accounts]:https://account.microsoft.com/
[What is Azure Active Directory?]:/azure/active-directory/fundamentals/active-directory-whatis
[register your application with Azure Active Directory]:/azure/active-directory/active-directory-app-registration

<!-- Microsoft Learn documentation: MSAL-->
[Microsoft Authentication Library (MSAL)]:/azure/active-directory/develop/msal-overview
[list of MSAL libraries]:/azure/active-directory/develop/reference-v2-libraries
[MSAL Wiki]:https://github.com/AzureAD/
[using MSAL]: https://github.com/AzureAD/microsoft-authentication-library-for-android#using-msal
[Enable cross-app SSO on Android using MSAL]:/azure/active-directory/develop/msal-android-single-sign-on
[Generate a redirect URI for a broker]:/azure/active-directory/develop/msal-android-single-sign-on#generate-a-redirect-uri-for-a-broker
[Configure MSAL to use a broker]:/azure/active-directory/develop/brokered-auth#configure-msal-to-use-a-broker
[Verify broker integration]:/azure/active-directory/develop/msal-android-single-sign-on#verify-broker-integration 
[AAD redirect URI]:/azure/active-directory/develop/msal-client-application-configuration#redirect-uri
[Use MSAL in a national cloud environment]:/azure/active-directory/develop/msal-national-cloud
[Android Microsoft Authentication Library configuration file]:/azure/active-directory/develop/msal-configuration
[MSAL repository on GitHub]: https://github.com/AzureAD/microsoft-authentication-library-for-android

<!-- Microsoft Learn documentation: ADAL -->
[Azure Active Directory Authentication Library (ADAL)]:/azure/active-directory/azuread-dev/active-directory-authentication-libraries

<!-- Microsoft Learn documentation: ADAL to MSAL -->
[Update your applications to use Microsoft Authentication Library (MSAL)]:https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363
[Migrate Android ADAL to MSAL]:/azure/active-directory/develop/migrate-android-adal-msal
[Differences between ADAL and MSAL]:/azure/active-directory/develop/msal-overview#differences-between-adal-and-msal

<!-- Microsoft Learn documentation: CA -->
[Conditional Access (CA)]:/azure/active-directory/develop/active-directory-conditional-access-developer
[device-based CA]:/mem/intune/protect/conditional-access-intune-common-ways-use#device-based-conditional-access
[app-based CA]:/mem/intune/conditional-access-intune-common-ways-use#app-based-conditional-access
[configuring app-based CA]:/mem/intune/protect/app-based-conditional-access-intune-create

<!-- Microsoft Learn documentation -->
[give your app access to the Intune app protection service]:/mem/intune/developer/app-sdk-get-started#give-your-app-access-to-the-intune-app-protection-service-optional

<!-- Other Microsoft links -->
[Microsoft Intune admin center]:https://go.microsoft.com/fwlink/?linkid=2109431
