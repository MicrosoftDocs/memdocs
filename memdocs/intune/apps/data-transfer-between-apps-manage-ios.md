---
# required metadata

title: Manage transferring data between iOS apps
titleSuffix: Microsoft Intune
description: Understand how to use mobile app management policies in Microsoft Intune to manage data transfers between apps.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: d10b2d64-8c72-4e9b-bd06-ab9d9486ba5e

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- iOS/iPadOS
---

# How to manage data transfer between iOS apps in Microsoft Intune

To help protect company data, restrict file transfers to only the apps that you manage. You can manage iOS apps in the following ways:

- Protect Org data for work or school accounts by configuring an app protection policy for the apps. which we call *policy managed apps*.  See [Microsoft Intune protected apps](apps-supported-intune-apps.md).

- Deploy and manage the apps through iOS device management, which requires devices to enroll in a Mobile Device Management (MDM) solution. The apps you deploy can be *policy managed apps* or other iOS managed apps.

The **Open-in management** feature for enrolled iOS devices can limit file transfers between iOS managed apps. Set *Open-in management* restrictions using an app protection policy that sets **Send org data to other apps** to the **Policy managed apps with Open-In/Share filtering** value and then deploy the policy using Intune.  When a user installs the deployed app, the restrictions you set are applied based on the assigned policy.

## Use Open-in management to protect iOS apps and data
Use App protection policies with the iOS **Open-in management** feature to protect company data in the following ways:

- **Devices not managed by any MDM solution:** You can set the app protection policy settings to control sharing of data with other applications via *Open-in* or *Share extensions*.  To do so, configure the **Send org data to other apps** setting to **Policy managed apps with Open-In/Share filtering** value.  The *Open-in/Share* behavior in the *policy managed app* presents only other *policy managed apps* as options for sharing. For related information, see [App protection policies for iOS/iPadOS and Android apps](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps), [Data Transfer](../apps/app-protection-policy-settings-ios.md#data-transfer), and [iOS share extension](../apps/app-protection-policy.md#ios-share-extension).

- **Devices managed by MDM solutions**: For devices enrolled in Intune or third-party MDM solutions, data sharing between apps with app protection policies and other managed iOS apps deployed through MDM is controlled by Intune APP policies and the iOS **Open-in management** feature. To make sure that apps you deploy using a MDM solution are also associated with your Intune app protection policies, configure the user UPN setting as described in the following section, [Configure user UPN setting](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm). To specify how you want to allow data transfer to other *policy managed apps* and iOS managed apps, configure **Send org data to other apps** setting to **Policy managed apps with OS sharing**. To specify how you want to allow an app to receive data from other apps, enable **Receive data from other apps** and then choose your preferred level of receiving data. For more information about receiving and sharing app data, see [Data relocation settings](app-protection-policy-settings-ios.md#data-protection).

## Configure user UPN setting for Microsoft Intune or third-party EMM
Configuring the user UPN setting is **required** for devices that are managed by Intune or a third-party EMM solution to identify the enrolled user account for the sending *policy managed app* when transferring data to an iOS managed app. The UPN configuration works with the app protection policies you deploy from Intune. The following procedure is a general flow on how to configure the UPN setting and the resulting user experience:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), [create and assign an app protection policy](app-protection-policies.md) for iOS/iPadOS. Configure policy settings per your company requirements and select the iOS apps that should have this policy.

2. Deploy the apps and the email profile that you want managed through Intune or your third-party MDM solution using the following generalized steps. This experience is also covered by *Example 1*.

3. Deploy the app with the following app configuration settings to the managed device:

      **key** = IntuneMAMUPN, **value** = <username@company.com>

      Example: ['IntuneMAMUPN', 'janellecraig@contoso.com']

     > [!NOTE]
     > In Intune, the App Configuration policy enrollment type must be set to **Managed Devices**.
     > Additionally, the app needs to be either installed from the Intune Company Portal (if set as available) or pushed as required to the device.

     > [!NOTE]
     > Deploy IntuneMAMUPN app configuration settings to the target managed app which sends data. Adding the app configuration key to the receiving app is optional.

     > [!NOTE]
     > Currently, there is no support for enrolling with a different user on an app if there is a MDM enrolled account on the same device. 

4. Deploy the **Open-in management** policy using Intune or your third-party MDM provider to enrolled devices.

### Example 1: Admin experience in Intune or third-party MDM console

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) or your third-party MDM provider. Go to the section of the admin center in which you deploy application configuration settings to enrolled iOS devices.

2. In the Application Configuration section, enter the following setting for each *policy managed app* that will transfer data to iOS managed apps:

   **key** = IntuneMAMUPN, **value** = <username@company.com>

   The exact syntax of the key/value pair may differ based on your third-party MDM provider. The following table shows examples of third-party MDM providers and the exact values you should enter for the key/value pair.

   |Third-party MDM provider| Configuration Key | Value Type | Configuration Value|
   | ------- | ---- | ---- | ---- |
   |Microsoft Intune| IntuneMAMUPN | String | {{userprincipalname}}|
   |Microsoft Intune| IntuneMAMOID | String | {{userid}}|
   |VMware AirWatch| IntuneMAMUPN | String | {UserPrincipalName}|
   |MobileIron | IntuneMAMUPN | String | ${userUPN} **or** ${userEmailAddress} |
   |Citrix Endpoint Management | IntuneMAMUPN | String | ${user.userprincipalname} |
   |ManageEngine Mobile Device Manager | IntuneMAMUPN | String | %upn% |

> [!NOTE]  
> For Outlook for iOS/iPadOS, if you deploy a managed devices App Configuration Policy with the option "Using configuration designer" and enable **Allow only work or school accounts**, the configuration key IntuneMAMUPN is configured automatically behind the scenes for the policy. More details can be found in the FAQ section in [New Outlook for iOS and Android App Configuration Policy Experience – General App Configuration](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Outlook-for-iOS-and-Android-App-Configuration-Policy/ba-p/370481).

### Example 2: End-user experience

*Sharing from a* policy managed app *to other applications with OS sharing*

1. A user opens the Microsoft OneDrive app on an enrolled iOS device and signs-in to their work account.  The account the user enters must match the account UPN you specified in the app configuration settings for the Microsoft OneDrive app.

2. After sign-in, your Administrator configured APP settings apply to the user account in Microsoft OneDrive.  This includes configuring the **Send Org data to other apps** setting to the **Policy managed apps with OS sharing** value.

3. The user previews a work file and attempts to share via Open-in to iOS managed app.  

4. The data transfer succeeds and data is now protected by **Open-in management** in the iOS managed app.  Intune APP does not apply to applications that are not *policy managed apps*.

*Sharing from a* iOS managed app *to a* policy managed app *with incoming Org data*

1. A user opens native Mail on an enrolled iOS device with a Managed email profile.  

1. The user opens a work document attachment from native Mail to Microsoft Word.

1. When the Word app launches, one of two experiences occur:
   1. The data is protected by Intune APP when:
      - The user is signed-in to their work account that matches the account UPN you specified in the app configuration settings for the Microsoft Word app. 
      - Your Administrator configured APP settings apply to the user account in Microsoft Word.  This includes configuring the **Receive data from other apps** setting to the **All apps with incoming Org data** value.
      - The data transfer succeeds and the document is tagged with the work identity in the app.  Intune APP protects the user actions for the document.
   1. The data is **not** protected by Intune APP when:
      - The user is **not** signed-in to their work account.
      - Your Administrator configured settings are **not** applied to Microsoft Word because the user is not signed in.
      - The data transfer succeeds and the document is **not** tagged with the work identity in the app.  Intune APP does **not** protects the user actions for the document because it is not active.

    > [!NOTE]
    > The user can add and use their personal accounts with Word. App protection policies don't apply when the user uses Word outside of a work-context. 

### Validate user UPN setting for third-party EMM

After configuring the user UPN setting, validate the iOS app's ability to receive and comply to Intune app protection policy.

For example, the **Require app PIN** policy setting is easy to test. When the policy setting equals **Require**, the user should see a prompt to set or enter a PIN before they can access company data.

First,  [create and assign an app protection policy](app-protection-policies.md) to the iOS app. For more information on how to test app protection policy, See [Validate app protection policies](app-protection-policies-validate.md).


## See also
[What is Intune app protection policy](app-protection-policy.md)
