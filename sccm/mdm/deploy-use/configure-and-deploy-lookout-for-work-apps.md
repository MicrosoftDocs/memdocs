---
title: "Deploy Lookout for Work app"
titleSuffix: "Configuration Manager"
description: "Configure and deploy Lookout for Work apps."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision:
author: dougeby
ms.author: dougeby
manager: angrobe

---
# Configure and deploy Lookout for Work apps

*Applies to: System Center Configuration Manager (Current Branch)*

This article explains how to configure and deploy the Lookout for Work app for Android and iOS devices.

## Android (Google Play Store app)
1.  In the Configuration Manager console, click **Software Library** > **Application Management** > **Applications**.

2.  On the **General** page of the Deploy Software Wizard, specify the following information:
  * Type: select **App package for Android on Google Play**.
  * Location: copy the Lookout for work app link from the Google Play store as paste it here
  * Publisher: Lookout Mobile Security
  * Name: Lookout for Work
  * Description: Lookout offers the best protection against mobile threats to keep your device safe. When the Lookout app is installed on the device, the app protects your device from threats and will alert you, and your company administrator, if any are found.
  * Administrative category: Computer Management

  Upon successful completion, you will now see the Lookout for work app in your list of applications.

3.  On the **Home** tab, in the **Deployment** group, choose **Deploy** to deploy the Lookout for Work app to users.
>[!IMPORTANT]
>You must select the same users added in to the Enrollment Management option in the Lookout MTP console.

  Choose the **Required Install** option to require that the Lookout app be installed on the user’s device.

## iOS (Enterprise-signed version of Lookout app)

* **Step 1:** Make sure **iOS management** is set up on your device. For instruction on how to setup your device for iOS management, see [Set up iOS and Mac device management]().

* **Step 2:** **Re-sign** the Lookout for Work iOS app. Lookout distributes its Lookout for Work iOS app outside of the iOS App Store. **Before distributing the app**, you must re-sign the app with your iOS Enterprise Developer Certificate. For detailed instructions to re-sign the Lookout for Work iOS apps, see [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/en-us/articles/114094038714) on the Lookout site.


* **Step 3:** Enable Azure Active Directory authentication for the iOS users by doing the following:
  1.  Login to the [Azure Active Directory management portal](https://manage.windowsazure.com), and navigate to the application page.
  2.  Add the **Lookout for Work iOS app** as a **native client application**.
  ![screenshot of the add apps dialog showing the native client app option](media/aad-add-app.png)

  3. Replace the **com.lookout.enterprise.yourcompanyname** with the customer bundle ID you selected when you signed the IPA.
  4.  Add additional redirect URI: **&lt;companyportal://code/>** followed by a URLencoded version of your original redirect URI.
  5.  Add **Delegated Permissions** to your app.

  For more details, see [Configure a native client application](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Step 4:** Upload the re-signed .ipa file as described in the [Create iOS applications in System Center Configuration Manager topic](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications) topic. Set the minimum OS version to iOS 8.0 or later.


* **Step 5:** Create the managed app configuration policy as described in the [Configure iOS apps with mobile app configuration policies in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) topic.


* **Step 6:** **To deploy the app to users**, select the Lookout for Work app in the **Applications** page, from the **Home** tab, in the **Deployment** group, choose **Deploy**.

  You must select the same users that were added to the Enrollment Management option in the Lookout console.  
Choose the **Required Install** option to require that the Lookout app be installed on the user’s device.

## What happens when the deployed app is opened on the device




When the user opens the Lookout for Work on the device they are prompted to activate the app, and choose the Sign in with Azure Active Directory option. A detailed walkthrough with the end-user flow can be found in the following topics:

* [You are prompted to install Lookout for Work on your Android device](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [You need to resolve a threat that Lookout for Work found on your Android device](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## Next steps
* [Enable device threat protection rule in the compliance policy](enable-device-threat-protection-rule-compliance-policy.md)
