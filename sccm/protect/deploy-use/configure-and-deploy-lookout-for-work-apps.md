---
title: "Deploy Lookout for Work app | System Center Configuration Manager"
description: "Configure and deploy Lookout for Work apps."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfdbfee6-4b9b-4d53-816a-62bbc3a43b6e
caps.latest.revision:
author: karthikaraman
ms.author: karaman
manager: angrobe

---
# Configure and deploy Lookout for Work apps

*Applies to: System Center Configuration Manager (Current Branch)*

This article explains how to configure and deploy the Lookout for Work app for Android and iOS devices.

## Android (Google Play Store app)


## iOS (Enterprise-signed version of Lookout app)

* **Step 1:** Make sure **iOS management** is set up on your device. For instruction on how to setup your device for iOS management, see [Set up iOS and Mac device management](set-up-ios-and-mac-management-with-microsoft-intune.md).

* **Step 2:** **Re-sign** the Lookout for Work iOS app. Lookout distributes its Lookout for Work iOS app outside of the iOS App Store. **Before distributing the app**, you must re-sign the app with your iOS Enterprise Developer Certificate. For detailed instructions to re-sign the Lookout for Work iOS apps, see [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/en-us/articles/114094038714) on the Lookout site.


* **Step 3:** Enable Azure Active Directory authentication for the iOS users by doing the following:
  1.  Login to the [Azure Active Directory management portal](https://manage.windowsazure.com), and navigate to the application page.
  2.  Add the **Lookout for Work iOS app** as a **native client application**.
  ![screenshot of the add apps dialog showing the native client app option](../media/mtp/aad-add-app.png)

  3. Replace the **com.lookout.enterprise.yourcompanyname** with the customer bundle ID you selected when you signed the IPA.
  4.  Add additional redirect URI: **&lt;companyportal://code/>** followed by a URLencoded version of your original redirect URI.
  5.  Add **Delegated Permissions** to your app.

  For more details, see [Configure a native client application](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Step 4:** Upload the re-signed .ipa file as described in the [Add app for mobile devices in Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) topic. Set the minimum OS version to iOS 8.0 or later.

  ![screenshot of the apps page in the Intune administrator console with the Lookout for work app displayed in the list of apps](../media/mtp/ios-app-uploaded-intune.png)

* **Step 5:** Create the managed app configuration policy as described in the [Configure iOS apps with mobile app configuration policies in Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/configure-ios-apps-with-mobile-app-configuration-policies-in-microsoft-intune) topic.

  ![screenshot of hte create a new policy wizard with the iOS 8.0 or later app configuration policy highlighted](../media/mtp/ios-app-config.png)

* **Step 6:** **To deploy the app to users**, select the Lookout for Work app, and choose **Manage Deployment**.

  You must select the same users that were added to the Enrollment Management option in the Lookout  console.  See Step 3 in the [configure your subscription with Lookout device threat protection section](set-up-your-subscription-with-lookout-mtp#configure-your-subscription-with-lookout-mtp) for information about adding user groups to Lookout MTP.
>[!IMPORTANT]
> The Intune app deployment wizard is not aware of the Azure AD user groups and uses the Intune user groups instead, so you must create an Intune user group based on the Azure AD user group that is enrolled in the Lookout console as described in [this](plan-your-user-and-device-groups.md) topic.

Choose the **Required Install** option to require that the Lookout app be installed on the user’s device.

## What happens when the deployed app is opened on the device




When the user opens the Lookout for Work on the device they are prompted to activate the app, and choose the Sign in with Azure Active Directory option. A detailed walkthrough with the end-user flow can be found in the following topics:

* [You are prompted to install Lookout for Work on your Android device](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [You need to resolve a threat that Lookout for Work found on your Android device](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## Next steps
* [Enable device threat protection rule in the compliance policy](enable-device-threat-protection-rule-in-compliance-policy.md)
