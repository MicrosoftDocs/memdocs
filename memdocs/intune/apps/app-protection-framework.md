---
# required metadata

title: Data protection framework using app protection policies 
titleSuffix: Microsoft Intune
description: Learn how App Protection Policies (APP) ensure an organization's data remains safe or contained in a managed app, regardless of whether the device is enrolled. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/10/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Data protection framework using app protection policies 

As more organizations implement mobile device strategies for accessing work or school data, protecting against data leakage becomes paramount. Intune's mobile application management solution for protecting against data leakage is App Protection Policies (APP). APP are rules that ensure an organization's data remains safe or contained in a managed app, regardless of whether the device is enrolled. For more information, see [App protection policies overview](app-protection-policy.md).

When configuring App Protection Policies, the number of various settings and options enable organizations to tailor the protection to their specific needs. Due to this flexibility, it may not be obvious which permutation of policy settings are required to implement a complete scenario. To help organizations prioritize client endpoint hardening endeavors, Microsoft has introduced a new taxonomy for [security configurations in Windows 10](https://aka.ms/secconframework), and Intune is leveraging a similar taxonomy for its APP data protection framework for mobile app management.  

The APP data protection configuration framework is organized into three distinct configuration scenarios:

- Level 1 enterprise basic data protection – Microsoft recommends this configuration as the minimum data protection configuration for an enterprise device.

- Level 2 enterprise enhanced data protection – Microsoft recommends this configuration for devices where users access sensitive or confidential information. This configuration is applicable to most mobile users accessing work or school data. Some of the controls may impact user experience.

- Level 3 enterprise high data protection – Microsoft recommends this configuration for devices run by an organization with a larger or more sophisticated security team, or for specific users or groups who are at uniquely high risk (users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization). An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.

## APP Data Protection Framework deployment methodology

As with any deployment of new software, features or settings, Microsoft recommends investing in a ring methodology for testing validation prior to deploying the APP data protection framework. Defining deployment rings is generally a one-time event (or at least infrequent), but IT should revisit these groups to ensure that the sequencing is still correct.

Microsoft recommends the following deployment ring approach for the APP data protection framework:

| Deployment ring  | Tenant  | Assessment teams  | Output  | Timeline  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Quality Assurance  | Pre-production tenant  | Mobile capability owners, Security, Risk Assessment, Privacy, UX  | Functional scenario validation, draft documentation  | 0-30 days  |
| Preview  | Production tenant  | Mobile capability owners, UX  | End-user scenario validation, user facing documentation  | 7-14 days, post Quality Assurance  |
| Production  | Production tenant  | Mobile capability owners, IT help desk  | N/A  | 7 days to several weeks, post Preview  |

As the above table indicates, all changes to the App Protection Policies should be first performed in a pre-production environment to understand the policy setting implications. Once testing is complete, the changes can be moved into production and applied to a subset of production users, generally, the IT department and other applicable groups. And finally, the rollout can be completed to the rest of the mobile user community. Rollout to production may take a longer amount of time depending on the scale of impact regarding the change. If there is no user impact, the change should roll out quickly, whereas, if the change results in user impact, rollout may need to go slower due to the need to communicate changes to the user population.

When testing changes to an APP, be aware of the [delivery timing](app-protection-policy-delivery.md). The status of APP delivery for a given user can monitored. For more information, see [How to monitor app protection policies](app-protection-policies-monitor.md).

Individual APP settings for each app can be validated on devices using Edge and the URL *about:Intunehelp*. For more information, see [Review client app protection logs](app-protection-policy-settings-log.md) and [Use Edge for iOS and Android to access managed app logs](manage-microsoft-edge.md#use-edge-for-ios-and-android-to-access-managed-app-logs).

## APP Data Protection Framework settings

The following App Protection Policy settings should be enabled for the applicable apps and assigned to all mobile users. For more information on each policy setting, see [iOS app protection policy settings](app-protection-policy-settings-ios.md) and [Android app protection policy settings](app-protection-policy-settings-android.md).

Microsoft recommends reviewing and categorizing usage scenarios, and then configuring users using the prescriptive guidance for that level. As with any framework, settings within a corresponding level may need to be adjusted based on the needs of the organization as data protection must evaluate the threat environment, risk appetite, and impact to usability.

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [Intune App Protection Policy Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

### Conditional Access Policies

To ensure that only apps supporting App Protection Polices access work or school account data, Azure Active Directory Conditional Access policies are required. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

 See **Require approved client apps or app protection policy with mobile devices** in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection) for steps to implement the specific policies. Finally, implement the steps in [Block legacy authentication](/azure/active-directory/conditional-access/block-legacy-authentication) to block legacy authentication capable iOS and Android apps.

> [!NOTE]
> These policies leverage the grant controls [Require approved client app](/azure/active-directory/conditional-access/concept-conditional-access-grant#require-approved-client-app) and [Require app protection policy](/azure/active-directory/conditional-access/concept-conditional-access-grant#require-app-protection-policy).

### Apps to include in the App Protection Policies  

For each App Protection Policy, the Core Microsoft Apps group is targeted, which includes the following apps:

- Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- SharePoint
- Teams
- To Do
- Word

The policies should include other Microsoft apps based on business need, additional third-party public apps that have integrated the Intune SDK used within the organization, as well as line-of-business apps that have integrated the [Intune SDK](../developer/app-sdk.md) (or have been wrapped).

### Level 1 enterprise basic data protection

Level 1 is the minimum data protection configuration for an enterprise mobile device. This configuration replaces the need for basic Exchange Online device access policies by requiring a PIN to access work or school data, encrypting the work or school account data, and providing the capability to selectively wipe the school or work data. However, unlike Exchange Online device access policies, the below App Protection Policy settings apply to all the apps selected in the policy, thereby ensuring data access is protected beyond mobile messaging scenarios.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users and mirror the default data protection and access requirements settings when creating an App Protection Policy within Microsoft Endpoint Manager.  

#### Data protection

| Setting | Setting description |             Value  |             Platform        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Data   Transfer |             Back up org data to…  |             Allow  |             iOS/iPadOS, Android        |
| Data   Transfer |       Send org   data to other apps  |             All apps  |             iOS/iPadOS, Android        |
| Data   Transfer |       Receive   data from other apps  |             All apps  |             iOS/iPadOS, Android        |
| Data   Transfer |       Restrict   cut, copy, and paste between apps  |             Any app  |             iOS/iPadOS, Android        |
| Data   Transfer |       Third-party keyboards  |             Allow  |             iOS/iPadOS        |
| Data   Transfer |       Approved keyboards  |             Not required  |             Android        |
| Data   Transfer |       Screen   capture and Google Assistant  |             Allow  |             Android        |
| Encryption |             Encrypt org data  |             Require  |             iOS/iPadOS, Android        |
| Encryption |       Encrypt   org data on enrolled devices  |             Require  |             Android        |
| Functionality  |             Sync app with native contacts app  |             Allow  |             iOS/iPadOS, Android        |
| Functionality  |       Printing   org data  |             Allow  |             iOS/iPadOS, Android        |
| Functionality  |       Restrict   web content transfer with other apps  |             Any app  |             iOS/iPadOS, Android        |
| Functionality  |       Org data notifications  |             Allow  |             iOS/iPadOS, Android        |

#### Access requirements

| Setting  | Value  | Platform  | Notes  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PIN for access  | Require  | iOS/iPadOS, Android  |   |
| PIN type  | Numeric  | iOS/iPadOS, Android  |   |
| Simple PIN  | Allow  | iOS/iPadOS, Android  |   |
| Select Minimum PIN length  | 4  | iOS/iPadOS, Android  |   |
| Touch ID instead of PIN for access (iOS 8+/iPadOS)  | Allow  | iOS/iPadOS  |   |
| Fingerprint instead of PIN for access (Android 9.0+)  | Allow  | Android  |   |
| Override biometrics with PIN after timeout  | Require  | iOS/iPadOS  |   |
| Override fingerprint with PIN after timeout  | Require  | Android  |   |
| Timeout (minutes of activity)  | 720  | iOS/iPadOS, Android  |   |
| Face ID instead of PIN for access (iOS 11+/iPadOS)  | Allow  | iOS/iPadOS  |   |
| Biometric instead of PIN for access  | Allow  | iOS/iPadOS, Android  |   |
| PIN reset after number of days  | No  | iOS/iPadOS, Android  |   |
| Select number of previous PIN values to maintain  | 0  | Android  |   |
| App PIN when device PIN is set  | Require  | iOS/iPadOS, Android  | If the device is enrolled in Intune, administrators can consider setting this to "Not required" if they are enforcing a strong device PIN via a device compliance policy.  |
| Work or school account credentials for access  | Not required  | iOS/iPadOS, Android  |   |
| Recheck the access requirements after (minutes of inactivity)  | 30  | iOS/iPadOS, Android  |   |

#### Conditional launch

| Setting | Setting description |          Value / Action  |          Platform        | Notes |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| App conditions |       Max PIN   attempts  |          5 / Reset   PIN  |          iOS/iPadOS,   Android  |                  |
| App conditions |       Offline   grace period  |          720 /   Block access (minutes)  |          iOS/iPadOS,   Android  |                  |
| App conditions |       Offline   grace period  |          90 / Wipe   data (days)  |          iOS/iPadOS,   Android  |                  |
| Device conditions  |       Jailbroken/rooted   devices  |        N/A / Block   access  |          iOS/iPadOS,   Android  |                  |
| Device conditions  |       SafetyNet   device attestation  |          Basic   integrity and certified devices / Block access  |          Android  |          <p>This   setting configures Google's SafetyNet Attestation on end-user   devices. Basic integrity validates the integrity of the device. Rooted   devices, emulators, virtual devices, and devices with signs of tampering fail   basic integrity. </p><p> Basic  integrity and certified devices validates the compatibility of   the device with Google's services. Only unmodified devices that have been   certified by Google can pass this check.</p>  |
| Device conditions  |       Require   threat scan on apps  |        N/A / Block   access  |          Android  |          This   setting ensures that Google's Verify Apps scan is turned on for end   user devices. If configured, the end-user will be blocked from access until   they turn on Google's app scanning on their Android device.        |
| Device conditions  |       Require device lock  |        N/A / Block   access  |         Android  |          This   setting ensures that Android devices have a device PIN, password, or pattern are set to enable a device lock.  This condition does not distinguish between lock options or the complexity.                |

#### Level 2 enterprise enhanced data protection

Level 2 is the data protection configuration recommended as a standard for devices where users access more sensitive information. These devices are a natural target in enterprises today. These recommendations do not assume a large staff of highly skilled security practitioners, and therefore should be accessible to most enterprise organizations. This configuration expands upon the configuration in Level 1 by restricting data transfer scenarios and by requiring a minimum operating system version.

The policy settings enforced in level 2 include all the policy settings recommended for level 1 but only lists those settings below that have been added or changed to implement more controls and a more sophisticated configuration than level 1. While these settings may have a slightly higher impact to users or to applications, they enforce a level of data protection more commensurate with the risks facing users with access to sensitive information on mobile devices.

#### Data protection

| Setting | Setting description |             Value  |             Platform        | Notes |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data Transfer |       Back up org   data to…  |          Block  |          iOS/iPadOS,   Android  |                  |
| Data Transfer |       Send org   data to other apps  |          Policy   managed apps  |          iOS/iPadOS,   Android  |          <p>With   iOS/iPadOS, administrators can configure this value to be "Policy managed   apps", "Policy managed apps with OS sharing", or "Policy managed apps   with Open-In/Share filtering". </p><p>Policy managed apps with OS   sharing is available when the device is also enrolled with Intune. This   setting allows data transfer to other policy managed apps, as well as   file transfers to other apps that have are managed by   Intune. </p><p>Policy managed apps with Open-In/Share filtering   filters the OS Open-in/Share dialogs to only display policy managed   apps. </p><p> For more information, see [iOS app protection policy   settings](app-protection-policy-settings-ios.md).</p> |
| Data Transfer |       Select apps to exempt  |          Default / skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;  |          iOS/iPadOS  |                  |
| Data Transfer |       Save   copies of org data  |          Block  |          iOS/iPadOS,   Android  |                  |
| Data Transfer |       Allow   users to save copies to selected services  |          OneDrive   for Business, SharePoint Online |          iOS/iPadOS,   Android  |                  |
| Data Transfer |       Transfer telecommunication data to  |          Any dialer app |          iOS/iPadOS,   Android  |                  |
| Data Transfer |       Restrict   cut, copy, and paste between apps  |          Policy   managed apps with paste in  |          iOS/iPadOS,   Android  |                  |
| Data Transfer |       Screen   capture and Google Assistant  |          Block  |          Android  |                  |
| Functionality |       Restrict   web content transfer with other apps  |          Microsoft   Edge  |          iOS/iPadOS,   Android  |                  |
| Functionality |       Org data   notifications  |          Block Org   Data  |          iOS/iPadOS,   Android  |          For a list   of apps that support this setting, see [iOS app protection policy   settings](app-protection-policy-settings-ios.md) and [Android   app protection policy   settings](app-protection-policy-settings-android.md).       |

#### Conditional launch

| Setting | Setting description |          Value / Action  |          Platform        | Notes |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       App   conditions  |          Disabled account  |        N/A / Block access  |          iOS/iPadOS,   Android        |  |
| Device conditions  |       Min   OS version  |          *Format: Major.Minor.Build <br>Example:   14.8* / Block access |          iOS/iPadOS        | Microsoft recommends configuring the minimum iOS   major version to match the supported iOS versions for Microsoft apps.   Microsoft apps support a N-1 approach where N is the current iOS major   release version. For minor and build version values, Microsoft recommends   ensuring devices are up to date with the respective security updates. See   [Apple security updates](https://support.apple.com/en-us/HT201222) for Apple's latest recommendations |
| Device conditions  |       Min   OS version  |          *Format: Major.Minor<br>   Example: 9.0* / Block access   |          Android        | Microsoft recommends configuring   the minimum Android major version to match the supported Android versions for   Microsoft apps. OEMs and devices adhering to Android Enterprise recommended   requirements must support the current shipping release + one letter upgrade.   Currently, Android recommends Android 9.0 and later for knowledge workers.   See [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/) for Android's latest   recommendations |
| Device conditions  |       Min patch   version  |          *Format:   YYYY-MM-DD <br> Example: 2020-01-01* / Block access  |          Android        | Android devices can receive monthly security patches, but the   release is dependent on OEMs and/or carriers. Organizations should ensure   that deployed Android devices do receive security updates before implementing   this setting. See [Android Security Bulletins](https://source.android.com/security/bulletin/) for the latest patch   releases.  |
| Device conditions  |       Required SafetyNet evaluation type  |          Hardware-backed key  |          Android  |          Hardware backed attestation enhances the existing SafetyNet attestation service check by leveraging a new evaluation type called [Hardware Backed](https://developer.android.com/training/safetynet/attestation#evaluation-types), providing a more robust root detection in response to newer types of rooting tools and methods that cannot always be reliably detected by a software only solution.<p> As its name implies, hardware backed attestation leverages a hardware-based component which shipped with devices installed with Android 8.1 and later. Devices that were upgraded from an older version of Android to Android 8.1 are unlikely to have the hardware-based components necessary for hardware backed attestation. While this setting should be widely supported starting with devices that shipped with Android 8.1, Microsoft strongly recommends testing devices individually before enabling this policy setting broadly.</p>  |

#### Level 3 enterprise high data protection

Level 3 is the data protection configuration recommended as a standard for organizations with large and sophisticated security organizations, or for specific users and groups who will be uniquely targeted by adversaries. Such organizations are typically targeted by well-funded and sophisticated adversaries, and as such merit the additional constraints and controls described. This configuration expands upon the configuration in Level 2 by restricting additional data transfer scenarios, increasing the complexity of the PIN configuration, and adding mobile threat detection.  

The policy settings enforced in level 3 include all the policy settings recommended for level 2 but only lists those settings below that have been added or changed to implement more controls and a more sophisticated configuration than level 2. These policy settings can have a potentially significant impact to users or to applications, enforcing a level of security commensurate with the risks facing targeted organizations.  

#### Data protection

| Setting | Setting description |             Value  |             Platform        | Notes |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Data Transfer |       Transfer telecommunication data to  |          Any policy-managed dialer app |          Android  | Administrators can also configure this setting to use a dialer app that does not support App Protection Policies by selecting **A specific dialer app** and providing the **Dialer App Package ID** and **Dialer App Name** values.   |
| Data Transfer |       Transfer telecommunication data to  |          A specific dialer app |          iOS/iPadOS  |  |
| Data Transfer |       Dialer App URL Scheme  |          *replace_with_dialer_app_url_scheme* |          iOS/iPadOS  | On iOS/iPadOS, this value must be replaced with the URL scheme for the custom dialer app being used. If the URL scheme is not known, contact the app developer for more information. For more information on URL schemes, see [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app).|
| Data transfer |       Receive   data from other apps  |          Policy   managed apps  |          iOS/iPadOS, Android         |  |
| Data transfer |       Open data into Org documents  |          Block  |          iOS/iPadOS, Android         |  |
| Data transfer |       Allow users to open data from selected services  |          OneDrive for Business, SharePoint, Camera, Photo Library |          iOS/iPadOS, Android         | For related information, see [Android app protection policy settings](..\apps\app-protection-policy-settings-android.md) and [iOS app protection policy settings](..\apps\app-protection-policy-settings-ios.md).  |
| Data transfer |       Third-party   keyboards  |          Block  |          iOS/iPadOS        | On iOS/iPadOS, this blocks all third-party keyboards from   functioning within the app.  |
| Data transfer |       Approved   keyboards  |          Require  |          Android        |  |
| Data transfer |       Select   keyboards to approve  |          *add/remove   keyboards*  |          Android        | With Android, keyboards must be selected in   order to be used based on your deployed Android devices.  |
| Functionality |       Printing org data  |          Block  |          iOS/iPadOS, Android         |  |

#### Access requirements

|       Setting  |          Value  |          Platform  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       Simple   PIN  |          Block  |          iOS/iPadOS,   Android  |
|       Select   Minimum PIN length  |          6  |          iOS/iPadOS,   Android  |
|       PIN reset   after number of days  |          Yes  |          iOS/iPadOS,   Android  |
|       Number of   days  |          365  |          iOS/iPadOS,   Android  |

#### Conditional launch

| Setting | Setting description |          Value / Action  |          Platform        | Notes |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Device   conditions  |          Jailbroken/rooted devices  |        N/A / Wipe data  |          iOS/iPadOS,   Android        |  |
|       Device   conditions  |          Max   allowed threat level  |          Secured / Block access  |          iOS/iPadOS,   Android        | <p>Unenrolled devices can be   inspected for threats using Mobile Threat Defense. For more information,   see  [Mobile Threat Defense for   unenrolled devices](../protect/mtd-enable-unenrolled-devices.md).      </p><p>     If the device is enrolled, this setting can be skipped in favor of   deploying Mobile Threat Defense for enrolled devices. For more information,   see [Mobile Threat Defense for enrolled   devices](../protect/mtd-device-compliance-policy-create.md).</p> |
| Device conditions  |       Max   OS version  |          *Format: Major.Minor<br>   Example: 11.0* / Block access   |          Android        | Microsoft recommends configuring   the maximum Android major version to ensure beta or unsupported versions of the operating system are not used.   See [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/) for Android's latest   recommendations |
| Device conditions  |       Max   OS version  |          *Format: Major.Minor.Build <br>Example:   15.0* / Block access |          iOS/iPadOS        | Microsoft recommends configuring   the maximum iOS/iPadOS major version to ensure beta or unsupported versions of the operating system are not used. See   [Apple security updates](https://support.apple.com/en-us/HT201222) for Apple's latest recommendations |

## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [Intune App Protection Policy Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## See also

- [How to create and deploy app protection policies with Microsoft Intune](app-protection-policies.md)
- [Available Android app protection policy settings with Microsoft Intune](app-protection-policy-settings-android.md)
- [Available iOS/iPadOS app protection policy settings with Microsoft Intune](app-protection-policy-settings-ios.md)

