---
# required metadata

title: Manage Outlook for iOS and Android with Intune
description: Use Intune app protection and configuration policies with Outlook for iOS and Android to ensure team collaboration experiences are always accessed with safeguards in place.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/12/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.reviewer: smithre4

# optional metadata
#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- M365-identity-device-management
- Android
ms.custom: intune-azure
---

# Manage messaging collaboration access by using Outlook for iOS and Android with Microsoft Intune

The Outlook for iOS and Android app is designed to enable users in your organization to do more from their mobile devices, by bringing together email, calendar, contacts, and other files.

The richest and broadest protection capabilities for Microsoft 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Azure Active Directory Premium features, such as conditional access. At a minimum, you will want to deploy a conditional access policy that allows connectivity to Outlook for iOS and Android from mobile devices and an Intune app protection policy that ensures the collaboration experience is protected.

## Apply Conditional Access
Organizations can use Azure AD Conditional Access policies to ensure that users can only access work or school content using Outlook for iOS and Android. To do this, you will need a conditional access policy that targets all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

1. Follow the steps in [Require approved client apps or app protection policy with mobile devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices). This policy allows Outlook for iOS and Android, but blocks OAuth and basic authentication capable Exchange ActiveSync mobile clients from connecting to Exchange Online.

    > [!NOTE]
    > This policy ensures mobile users can access all Microsoft 365 endpoints using the applicable apps.

2. Follow the steps in [Block Exchange ActiveSync on all devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#block-exchange-activesync-on-all-devices), which prevents Exchange ActiveSync clients using basic authentication on non-mobile devices from connecting to Exchange Online.

   The above policies leverage the grant access control [Require app protection policy](/azure/active-directory/active-directory-conditional-access-technical-reference), which ensures that an Intune App Protection Policy is applied to the associated account within Outlook for iOS and Android prior to granting access. If the user isn't assigned to an Intune App Protection Policy, isn't licensed for Intune, or the app isn't included in the Intune App Protection Policy, then the policy prevents the user from obtaining an access token and gaining access to messaging data.

3. Follow the steps in [How to: Block legacy authentication to Azure AD with Conditional Access](/azure/active-directory/conditional-access/block-legacy-authentication) to block legacy authentication for other Exchange protocols on iOS and Android devices; this policy should target only Microsoft Exchange Online cloud app and iOS and Android device platforms. This ensures mobile apps using Exchange Web Services, IMAP4, or POP3 protocols with basic authentication cannot connect to Exchange Online.

> [!NOTE]
> To leverage app-based conditional access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is required. For more information, see [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

Regardless of whether the device is enrolled in a unified endpoint management (UEM) solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](app-protection-policies.md). These policies, at a minimum, must meet the following conditions:

- They include all Microsoft 365 mobile applications, such as Edge, Outlook, OneDrive, Office, or Teams, as this ensures that users can access and manipulate work or school data within any Microsoft app in a secure fashion.

- They are assigned to all users. This ensures that all users are protected, regardless of whether they use Outlook for iOS or Android.

- Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

For more information on the available settings, see [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> To apply Intune app protection policies against apps on Android devices that are not enrolled in Intune, the user must also install the Intune Company Portal.  

## Use app configuration

Outlook for iOS and Android supports app settings that allow unified endpoint management, like Microsoft Endpoint Manager, administrators to customize the behavior of the app.

App configuration can be delivered either through the mobile device management (MDM) OS channel on enrolled devices ([Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the Intune App Protection Policy (APP) channel. Outlook for iOS and Android supports the following configuration scenarios:

- Only allow work or school accounts
- General app configuration settings
- S/MIME settings
- Data protection settings

For specific procedural steps and detailed documentation on the app configuration settings Outlook for iOS and Android supports, see [Deploying Outlook for iOS and Android app configuration settings](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## Next steps

- [What are app protection policies?](app-protection-policy.md) 
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
