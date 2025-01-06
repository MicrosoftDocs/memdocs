---
# required metadata

title: Data transfer policy exceptions for apps 
titleSuffix: Microsoft Intune
description: Create exceptions to the Intune App Protection Policy (APP) data transfer policy.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: f9015e3a-c22c-42eb-90e6-ba48dee3a41d

# optional metadata

#ROBOTS:

#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# How to create exceptions to the Intune App Protection Policy (APP) data transfer policy

As an administrator, you can create exceptions to the Intune App Protection Policy (APP) data transfer policy. An exception allows you to specifically choose which unmanaged apps can transfer data to and from managed apps. Your IT must trust the unmanaged apps that you include in the exception list. 

>[!WARNING] 
> You're responsible for making changes to the data transfer exception policy. Additions to this policy allow unmanaged apps (apps that aren't managed by Intune) to access data protected by managed apps. This access to protected data may result in data security leaks. Only add data transfer exceptions for apps that your organization must use, but that don't support Intune APP (Application Protection Policies). Additionally, only add exceptions for apps that you don't consider to be data leak risks.

Within an Intune Application Protection Policy, setting **Allow app to transfer data to other apps** to **Policy managed apps** means that the app can transfer data only to apps managed by Intune. If you need to allow data to be transferred to specific apps that don't support Intune APP, you can create exceptions to this policy by using **Select apps to exempt**. Exemptions allow applications managed by Intune to invoke unmanaged applications based on URL protocol (iOS/iPadOS) or package name (Android). By default, Intune adds vital native applications to this list of exceptions. 

> [!NOTE]
> Modifying or adding to the data transfer policy exceptions doesn't impact other App Protection Policies, such as cut, copy, and paste restrictions. 

## iOS data transfer exceptions
For a policy targeting iOS/iPadOS, you can configure data transfer exceptions by URL protocol. To add an exception, check the documentation provided by the developer of the app to find information about supported URL protocols. For more information about iOS/iPadOS data transfer exceptions, see [iOS/iPadOS app protection policy settings - Data transfer exemptions](app-protection-policy-settings-ios.md#data-transfer-exemptions).

> [!NOTE]
> Microsoft doesn't have a method to manually find the URL protocol for creating app exceptions for third-party applications. 

## Android data transfer exceptions
For a policy targeting Android, you can configure data transfer exceptions by app package name. You can check the **Google Play** store page for the app you would like to add an exception for to find the app package name. For more information about Android data transfer exceptions, see [Android app protection policy settings - Data transfer exemptions](app-protection-policy-settings-android.md#data-transfer-exemptions).


>[!TIP]
> You can find the package ID of an app by browsing to the app on the Google Play store. The package ID is contained in the URL of the app's page. For example, the package ID of the Microsoft Word app is **com.microsoft.office.word**.

### Example
By adding the **Webex** package as an exception to the MAM data transfer policy, Webex links inside a managed Outlook email message are allowed to open directly in the Webex application. Data transfer is still restricted in other unmanaged apps.

- iOS/iPadOS **Webex** example:
    To exempt the **Webex** app so that it's allowed to be invoked by Intune managed apps, you must add a data transfer exception for the following string: <code>wbx</code>
    
- iOS/iPadOS **Maps** example:
    To exempt the native **Maps** app so that it's allowed to be invoked by Intune managed apps, you must add a data transfer exception for the following string: <code>maps</code>

- Android **Webex** example:
    To exempt the **Webex** app so that it's allowed to be invoked by Intune managed apps, you must add a data transfer exception for the following string: <code>com.cisco.webex.meetings</code>
    
- Android **SMS** example:
    To exempt the native **SMS** app so that it's allowed to be invoked by Intune managed apps across different messaging apps and Android devices, you must add data transfer exceptions for the following strings: 
    <code>com.google.android.apps.messaging</code>
    
    <code>com.android.mms</code>
    
    <code>com.samsung.android.messaging</code>

## Next steps

- [Create and deploy app protection policies](app-protection-policies.md)
- [iOS/iPadOS app protection policy settings - Data transfer exemptions](app-protection-policy-settings-ios.md#data-transfer-exemptions)
- [Android app protection policy settings - Data transfer exemptions](app-protection-policy-settings-android.md#data-transfer-exemptions)
