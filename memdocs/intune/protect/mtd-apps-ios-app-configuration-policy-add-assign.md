---
# required metadata

title: Add and assign MTD apps to Microsoft Intune
titleSuffix: Microsoft Intune
description: Use Intune to add Mobile Threat Defense (MTD) apps, Microsoft Authenticator app, and iOS configuration policy in Microsoft Intune
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/13/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add and assign Mobile Threat Defense (MTD) apps with Intune

You can use Intune to add and deploy Mobile Threat Defense (MTD) apps so that end users can receive notifications when a threat is identified in their mobile devices, and to receive guidance to remediate the threats.

> [!NOTE]
> This article applies to all Mobile Threat Defense partners.

## Before you begin

Complete the following steps in Intune. Make sure you're familiar with the process of:

- [Adding an app into Intune](../apps/apps-add.md).
- [Adding an iOS app configuration policy into Intune](../apps/app-configuration-policies-use-ios.md).
- [Assigning an app with Intune](../apps/apps-deploy.md).

> [!TIP]
> The Intune Company Portal works as the broker on Android devices so users can have their identities checked by Azure AD.

## Configure Microsoft Authenticator for iOS

For iOS devices, you need the [Microsoft Authenticator](/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) so users can have their identities checked by Azure AD. Additionally, you need an iOS app configuration policy that sets the MTD iOS app you use with Intune.

See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Microsoft Authenticator app store URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) when you configure **App information**.

## Configure your MTD apps with an app configuration policy

To simplify user onboarding, the Mobile Threat Defense apps on MDM-managed devices use app configuration. For unenrolled devices, MDM based app configuration is not available, so please refer to [Add Mobile Threat Defense apps to unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md).

### BlackBerry Protect configuration policy

See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the BlackBerry Protect iOS app configuration policy.

<!-- Pending revision to the following to support the BlackBerry app  >

- For **Configuration settings format**, select **Enter XML data**, copy the following content and paste it into the configuration policy body. Replace the `https://client.bmobi.net` URL with the appropriate console URL.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```
-->

### Better Mobile app configuration policy

See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Better Mobile iOS app configuration policy.

- For **Configuration settings format**, select **Enter XML data**, copy the following content and paste it into the configuration policy body. Replace the `https://client.bmobi.net` URL with the appropriate console URL.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### Check Point SandBlast Mobile app configuration policy

See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Check Point SandBlast Mobile iOS app configuration policy.

- For **Configuration settings format**, select **Enter XML data**, copy the following content and paste it into the configuration policy body.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`

### Lookout for Work app configuration policy

Create the iOS app configuration policy as described in the [using iOS app configuration policy](../apps/app-configuration-policies-use-ios.md) article.

### MVISION Mobile app configuration policy

- **Android Enterprise**
   
   See the instructions for [using Microsoft Intune app configuration policies for Android](../apps/app-configuration-policies-use-android.md) to add the MVISION Android app configuration policy. 
   
   For **Configuration settings format**, select **Use configuration designer**, and add the following settings: 

| Configuration key  | Value type | Configuration value  |
|---|---|---|
|  MDMDeviceID | string  | `{{AzureADDeviceId}}`  |
|  tenantid | string  | Copy value from admin console “Manage” page in the MVISION console |
|  defaultchannel | string   | Copy value from admin console “Manage” page in the MVISION console  |

- **iOS**
   
   See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the MVISION Mobile iOS app configuration policy.
   
   For **Configuration settings format**, select **Use configuration designer**, and add the following settings: 

| Configuration key  | Value type | Configuration value  |
|---|---|---|
|  MDMDeviceID | string  | `{{AzureADDeviceId}}`  |
|  tenantid | string  | Copy value from admin console “Manage” page in the MVISION console |
|  defaultchannel | string   | Copy value from admin console “Manage” page in the MVISION console  |

### Pradeo app configuration policy

Pradeo doesn't support application configuration policy on iOS/iPadOS.  Instead, to get a configured app, work with Pradeo to implement custom IPA or APK files that are preconfigured with the settings you want.

### SEP Mobile app configuration policy

Use the same Azure AD account previously configured in the [Symantec Endpoint Protection Management console](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/getting-up-and-running-on-for-the-first-time-v45150512-d43e1033/logging-on-to-the-console-v8025272-d23e2462.html), which should be the same account used to sign in to the Intune.

- **Download** the iOS app configuration policy file:
  - Go to [Symantec Endpoint Protection Management console](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/getting-up-and-running-on-for-the-first-time-v45150512-d43e1033/logging-on-to-the-console-v8025272-d23e2462.html) and sign in with your admin credentials.

  - Go to **Settings**, and under **Integrations**, choose **Intune**. Choose **EMM Integration Selection**. Choose **Microsoft**, and then save your selection.

  - Click the **Integration setup files** link and save the generated \*.zip file. The .zip file contains the ***.plist** file that will be used to create the iOS app configuration policy in Intune.

  - See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the SEP Mobile iOS app configuration policy.

    - For **Configuration settings format**, select **Enter XML data**, copy the content from the ***.plist** file, and paste its content into the configuration policy body.

> [!NOTE]
> If you are unable to retrieve the files, contact [Symantec Endpoint Protection Mobile Enterprise Support](https://support.symantec.com/en_US/contact-support.html).

### Sophos Mobile app configuration policy

Create the iOS app configuration policy as described in the [using iOS app configuration policy](../apps/app-configuration-policies-use-ios.md) article. For additional information, see [Sophos Intercept X for Mobile iOS - Available managed settings](https://community.sophos.com/kb/133963) in the Sophos knowledge base.

### Wandera app configuration policy

> [!NOTE]
> For initial testing, use a test group when assigning users and devices in the Assignments section of the configuration policy. 

- **Android Enterprise**

   See the instructions for [using Microsoft Intune app configuration policies for Android](../apps/app-configuration-policies-use-android.md) to add the Wandera Android app configuration policy using the information below when prompted.

1. In the **RADAR Wandera Portal**, click the **Add** button under **Configuration settings** format.
2. Select **Activation Profile URL** from the list of **Configuration Keys**. Click **OK**.
3. For **Activation Profile URL** select **string** from the **Value type** menu then copy the **Shareable Link URL** from the desired Activation Profile in RADAR.
4. In the **Intune admin console app configuration UI**, select **Settings**, define **Configuration settings format > Use Configuration Designer** and paste the **Shareable Link URL**.  

> [!NOTE] 
> Unlike iOS, you will need to define a unique Android Enterprise app configuration policy for each Wandera Activation Profile. If you don’t require multiple Wandera Activation Profiles, you may use a single Android app configuration for all target devices. When creating Activation Profiles in Wandera, be sure to select “Azure Active Directory” under the Associated User configuration to ensure Wandera is able to synchronize the device with Intune via UEM Connect.

- **iOS**

   See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Wandera iOS app configuration policy using the information below when prompted.

1. In **RADAR Wandera Portal**, navigate to **Devices > Activations** and select any activation profile. Click **Deployment Strategies > Managed Devices > Microsoft Intune** and locate the **iOS App Configuration settings**.  
2. Expand the box to reveal the iOS app configuration XML and copy it to your system clipboard.  
3. In **Intune admin console app configuration UI Settings,** define **Configuration settings format > Enter XML data**. 
4. Paste the XML in the app configuration text box.

> [!NOTE]
> A single iOS configuration policy may be used across all devices that are to be provisioned with Wandera.  

### Zimperium app configuration policy

- **Android Enterprise**
   
   See the instructions for [using Microsoft Intune app configuration policies for Android](../apps/app-configuration-policies-use-android.md) to add the Zimperium Android app configuration policy. 
   
   For **Configuration settings format**, select **Use configuration designer**, and add the following settings: 

| Configuration key  | Value type | Configuration value  |
|---|---|---|
|  MDMDeviceID | string  | `{{AzureADDeviceId}}`  |
|  tenantid | string  | Copy value from admin console “Manage” page in the Zimperium console |
|  defaultchannel | string   | Copy value from admin console “Manage” page in the Zimperium console  |

- **iOS**
   
   See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Zimperium iOS app configuration policy.

   For **Configuration settings format**, select **Use configuration designer**, and add the following settings:

| Configuration key  | Value type | Configuration value  |
|---|---|---|
|  MDMDeviceID | string  | `{{AzureADDeviceId}}`  |
|  tenantid | string  | Copy value from admin console “Manage” page in the Zimperium console |
|  defaultchannel | string   | Copy value from admin console “Manage” page in the Zimperium console  |

## Assigning Mobile Threat Defense apps to end users via Intune

To install the Mobile Threat Defense app on the end user device, you can follow the steps that are detailed in the following sections. Make sure you're familiar with the process of:

- [Assigning apps to groups with Intune](../apps/apps-deploy.md)

Choose the section that corresponds to your MTD provider:

- [Better Mobile](#assigning-better-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Lookout for Work](#assigning-lookout-for-work)
- [MVISION Mobile](#assigning-mvision-mobile)
- [Pradeo](#assigning-pradeo)
- [Sophos Mobile](#assigning-sophos)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Wandera](#assigning-wandera)
- [Zimperium](#assigning-zimperium)

### Assigning Better Mobile

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Active Shield app store URL](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield app store URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) for the **Appstore URL**.

### Assigning Check Point SandBlast Mobile

- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Check Point SandBlast Mobile app store URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Check Point SandBlast Mobile app store URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) for the **Appstore URL**.  


### Assigning Lookout for Work

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Lookout for work Google app store URL](https://play.google.com/store/apps/details?id=com.lookout.enterprise) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Lookout for Work iOS app store URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) for the **Appstore URL**.

- **Lookout for Work app outside the Apple store**
  - You must re-sign the Lookout for Work iOS app. Lookout distributes its Lookout for Work iOS app outside of the iOS App Store. Before distributing the app, you must re-sign the app with your iOS Enterprise Developer Certificate.  
  - For detailed instructions to re-sign the Lookout for Work iOS apps, see [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) on the Lookout website.

  - **Enable Azure AD authentication for Lookout for Work iOS app users.**

    1. Go to the [Azure portal](https://portal.azure.com), sign in with your credentials, then navigate to the application page.

    2. Add the **Lookout for Work iOS app** as a **native client application**.

    3. Replace the **com.lookout.enterprise.yourcompanyname** with the customer bundle ID you selected when you signed the IPA.

    4. Add additional redirect URI: **&lt;companyportal://code/>** followed by a URL encoded version of your original redirect URI.

    5. Add **Delegated Permissions** to your app.

    > [!NOTE]
    > See [configure a native client application with Azure AD](/azure/app-service/configure-authentication-provider-aad#optional-configure-a-native-client-application) for more details.

  - **Add the Lookout for Work ipa file.**

    - Upload the re-signed .ipa file as described in the [Add iOS LOB apps with Intune](../apps/lob-apps-ios.md) article. You also need to set the minimum OS version to iOS 8.0 or later.

### Assigning MVISION Mobile

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [MVISION Mobile app store URL](https://play.google.com/store/apps/details?id=com.mcafee.mvision) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [MVISION Mobile app store URL](https://apps.apple.com/us/app/mcafee-mvision-mobile/id1435156022) for the **Appstore URL**.


### Assigning Pradeo

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Pradeo app store URL](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Pradeo app store URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) for the **Appstore URL**.

### Assigning Sophos

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Sophos app store URL](https://play.google.com/store/apps/details?id=com.sophos.smsec) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield app store URL](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) for the **Appstore URL**.

### Assigning Symantec Endpoint Protection Mobile

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [SEP Mobile app store URL](https://play.google.com/store/apps/details?id=com.skycure.skycure) for the **Appstore URL**.  For **Minimum operating system**, select **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SEP Mobile app store URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) for the **Appstore URL**.

### Assigning Wandera

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Wandera Mobile app store URL](https://play.google.com/store/apps/details?id=com.wandera.android) for the **Appstore URL**. For **Minimum operating system**, select **Android 8.0**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Wandera Mobile app store URL](https://itunes.apple.com/app/wandera/id605469330) for the **Appstore URL**.

### Assigning Zimperium

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Zimperium app store URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Zimperium app store URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) for the **Appstore URL**.  

## Next steps

- [Configure the device compliance policy for MTD](mtd-device-compliance-policy-create.md)
