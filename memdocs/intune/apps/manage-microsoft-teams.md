---
# required metadata

title: Manage Teams for iOS and Android with Intune 
titleSuffix: 
description: Use Intune app protection and configuration policies with Teams for iOS and Android to ensure team collaboration experiences are always accessed with safeguards in place. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Manage team collaboration access by using Teams for iOS and Android with Microsoft Intune

Microsoft Teams is the hub for team collaboration in Microsoft 365 that integrates the people, content, and tools your team needs to be more engaged and effective.

The richest and broadest protection capabilities for Office 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Azure Active Directory Premium features, such as conditional access. At a minimum, you will want to deploy a conditional access policy that allows connectivity to Teams for iOS and Android from mobile devices and an Intune app protection policy that ensures the collaboration experience is protected.

## Apply Conditional Access
Organizations can use use Azure AD Conditional Access policies to ensure that users can only access work or school content using Teams for iOS and Android. To do this, you will need a conditional access policy that targets all potential users. Details on creating this policy can be found in [Require app protection policy for cloud app access with Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Follow "Step 1: Configure an Azure AD Conditional Access policy for Office 365" in [Scenario 1: Office 365 apps require approved apps with app protection policies](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), which allows Teams for iOS and Android, but blocks third-party OAuth capable mobile device clients from connecting to Office 365 endpoints.

   >[!NOTE]
   > This policy ensures mobile users can access all Office endpoints using the applicable apps.

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

Regardless of whether the device is enrolled in an unified endpoint management (UEM) solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](app-protection-policies.md). These policies, at a minimum, must meet the following conditions:

1. They include all Microsoft mobile applications, such as Outlook, OneDrive, Office, or Teams, as this will ensure that users can access and manipulate work or school data within any Microsoft app in a secure fashion.

2. They are assigned to all users. This ensures that all users are protected, regardless of whether they use Teams for iOS or Android.

3. Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

For more information on the available settings, see [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> To apply Intune app protection policies against apps on Android devices that are not enrolled in Intune, the user must also install the Intune Company Portal. For more information, see [What to expect when your Android app is managed by app protection policies](../fundamentals/end-user-mam-apps-android.md).

## Utilize app configuration

Teams for iOS and Android supports app settings that allow unified endpoint management, like Microsoft Endpoint Manager, administrators to customize the behavior of the app.

App configuration can be delivered either through the mobile device management (MDM) OS channel on enrolled devices ([Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the Intune App Protection Policy (APP) channel. Teams for iOS and Android supports the following configuration scenarios:

- Only allow work or school accounts

> [!IMPORTANT]
> For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise and Teams for Android must be deployed via the Managed Google Play store. For more information, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md) and [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).

Each configuration scenario highlights its specific requirements. For example, whether the configuration scenario requires device enrollment, and thus works with any UEM provider, or requires Intune App Protection Policies.

> [!NOTE]
> With Microsoft Endpoint Manager, app configuration delivered through the MDM OS channel is referred to as a **Managed Devices** App Configuration Policy (ACP); app configuration delivered through the App Protection Policy channel is referred to as a **Managed Apps** App Configuration Policy.

## Only allow work or school accounts

Respecting the data security and compliance policies of our largest and highly regulated customers is a key pillar to the Microsoft 365 value. Some companies have a requirement to capture all communications information within their corporate environment, as well as, ensure the devices are only used for corporate communications. To support these requirements, Teams for iOS and Android on enrolled devices can be configured to only allow a single corporate account to be provisioned within the app.

You can learn more about configuring the org allowed accounts mode setting here:

- [Android setting](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS setting](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

This configuration scenario only works with enrolled devices. However, any UEM provider is supported. If you are not using Microsoft Endpoint Manager, you need to consult with your UEM documentation on how to deploy these configuration keys.