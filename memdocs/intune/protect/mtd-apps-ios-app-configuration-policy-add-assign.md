---
# required metadata

title: Add and assign MTD apps to Microsoft Intune
titleSuffix: Microsoft Intune
description: Use Intune to add Mobile Threat Defense (MTD) apps, Microsoft Authenticator app, and iOS configuration policy in the Azure portal.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: davera
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

Complete the following steps in Intune. Make sure you’re familiar with the process of:

- [Adding an app into Intune](../apps/apps-add.md).
- [Adding an iOS app configuration policy into Intune](../apps/app-configuration-policies-use-ios.md).
- [Assigning an app with Intune](../apps/apps-deploy.md).

> [!TIP]
> The Intune Company Portal works as the broker on Android devices so users can have their identities checked by Azure AD.

## Configure Microsoft Authenticator for iOS

For iOS devices, you need the [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) so users can have their identities checked by Azure AD. Additionally, you need an iOS app configuration policy that sets the MTD iOS app you use with Intune.

See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Microsoft Authenticator app store URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) when you configure **App information**.

## Configure MTD applications

Choose the section that corresponds to your MTD provider:

- [Lookout for Work](#configure-lookout-for-work-apps)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#configure-symantec-endpoint-protection-mobile-apps)
- [Check Point SandBlast Mobile](#configure-check-point-sandblast-mobile-apps)
- [Zimperium](#configure-zimperium-apps)
- [Pradeo](#configure-pradeo-apps)
- [Better Mobile](#configure-better-mobile-apps)
- [Sophos Mobile](#configure-sophos-apps)
- [Wandera](#configure-wandera-apps)

### Configure Lookout for Work apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Lookout for work Google app store URL](https://play.google.com/store/intune/apps/details?id=com.lookout.enterprise) for the **Appstore URL**.

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
    > See [configure a native client application with Azure AD](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application) for more details.

  - **Add the Lookout for Work ipa file.**

    - Upload the re-signed .ipa file as described in the [Add iOS LOB apps with Intune](../apps/lob-apps-ios.md) article. You also need to set the minimum OS version to iOS 8.0 or later.

### Configure Symantec Endpoint Protection Mobile apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [SEP Mobile app store URL](https://play.google.com/store/intune/apps/details?id=com.skycure.skycure) for the **Appstore URL**.  For **Minimum operating system**, select **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SEP Mobile app store URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) for the **Appstore URL**.

### Configure Check Point SandBlast Mobile apps

- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Check Point SandBlast Mobile app store URL](https://play.google.com/store/intune/apps/details?id=com.lacoon.security.fox) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Check Point SandBlast Mobile app store URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) for the **Appstore URL**.  

### Configure Zimperium apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Zimperium app store URL](https://play.google.com/store/intune/apps/details?id=com.zimperium.zips&hl=en) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Zimperium app store URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) for the **Appstore URL**.  
 
### Configure Pradeo apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Pradeo app store URL](https://play.google.com/store/intune/apps/details?id=net.pradeo.service&hl=en_US) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Pradeo app store URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) for the **Appstore URL**.

### Configure Better Mobile apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Active Shield app store URL](https://play.google.com/store/intune/apps/details?id=com.better.active.shield.enterprise) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield app store URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) for the **Appstore URL**.

### Configure Sophos apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Sophos app store URL](https://play.google.com/store/intune/apps/details?id=com.sophos.smsec) for the **Appstore URL**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield app store URL](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) for the **Appstore URL**.

### Configure Wandera apps

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Wandera Mobile app store URL](https://play.google.com/store/intune/apps/details?id=com.wandera.android) for the **Appstore URL**. For **Minimum operating system**, select **Android 5.0**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Wandera Mobile app store URL](https://itunes.apple.com/app/wandera/id605469330) for the **Appstore URL**.

## Configure your MTD apps with an iOS app configuration policy

### Lookout for Work app configuration policy

Create the iOS app configuration policy as described in the [using iOS app configuration policy](../apps/app-configuration-policies-use-ios.md) article.

### SEP Mobile app configuration policy

Use the same Azure AD account previously configured in the [Symantec Endpoint Protection Management console](https://aad.skycure.com), which should be the same account used to sign in to the Intune.

- **Download** the iOS app configuration policy file:
  - Go to [Symantec Endpoint Protection Management console](https://aad.skycure.com) and sign in with your admin credentials.

  - Go to **Settings**, and under **Integrations**, choose **Intune**. Choose **EMM Integration Selection**. Choose **Microsoft**, and then save your selection.

  - Click the **Integration setup files** link and save the generated \*.zip file. The .zip file contains the ***.plist** file that will be used to create the iOS app configuration policy in Intune.

  - See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the SEP Mobile iOS app configuration policy.

    - For **Configuration settings format**, select **Enter XML data**, copy the content from the ***.plist** file, and paste its content into the configuration policy body.

> [!NOTE]
> If you are unable to retrieve the files, contact [Symantec Endpoint Protection Mobile Enterprise Support](https://support.symantec.com/en_US/contact-support.html).

### Check Point SandBlast Mobile app configuration policy

See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Check Point SandBlast Mobile iOS app configuration policy.

- For **Configuration settings format**, select **Enter XML data**, copy the following content and paste it into the configuration policy body.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### Zimperium app configuration policy

See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Zimperium iOS app configuration policy.

- For **Configuration settings format**, select **Enter XML data**, copy the following content and paste it into the configuration policy body.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### Pradeo app configuration policy

Pradeo doesn't support application configuration policy on iOS.  Instead, to get a configured app, work with Pradeo to implement custom IPA or APK files that are preconfigured with the settings you want.

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

### Sophos Mobile app configuration policy

Create the iOS app configuration policy as described in the [using iOS app configuration policy](../apps/app-configuration-policies-use-ios.md) article.

### Wandera app configuration policy

See the instructions for [using Microsoft Intune app configuration policies for iOS](../apps/app-configuration-policies-use-ios.md) to add the Wandera iOS app configuration policy.

- For **Configuration settings format**, select **Enter XML data**.

Sign in to your RADAR Wandera portal and browse to **Settings** > **EMM Integration** > **App Push**. Select **Intune**, and then copy the content below and paste it into the configuration policy body.  

  ```
  <dict><key>secretKey</key>
  <string>SeeRADAR</string>
  <key>apiKey</key>
  <string> SeeRADAR </string>
  <key>customerId</key>
  <string> SeeRADAR </string>
  <key>email</key>
  <string>{{mail}}</string>
  <key>firstName</key>
  <string>{{username}}</string>
  <key>lastName</key>
  <string></string>
  <key>activationType</key>
  <string>PROVISION_THEN_AWP</string></dict>
  ```

## Assign apps to groups

This step applies to all MTD partners. See instructions for [assigning apps to groups with Intune](../apps/apps-deploy.md).

## Next steps

- [Configure the device compliance policy for MTD](mtd-device-compliance-policy-create.md)
