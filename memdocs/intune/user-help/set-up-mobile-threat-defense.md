---
# required metadata

title: Install mobile threat defense app on your mobile device | Microsoft Intune
description: Find out what mobile threat defense apps are and how to set one up to meet your organization's access requirements.   
keywords:
author: lenewsad
ms.author: lanewsad  
manager: dougeby
ms.date: 06/14/2023
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: aanavath  
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser, contperf-fy21q1
ms.collection:
- tier2
---  

# Install mobile threat defense app  

> [!TIP]
> There are a variety of MTD apps on the market. Your organization should tell you which one to use. If you're prompted to install an MTD app and you're not immediately redirected to set up or install the app, contact your IT support person for help. This article also provides the links to store listings.   

Your organization might require you to install a mobile threat defense (MTD) app on any personal device you're using for work. This type of app detects and alerts you to threats, such as suspicious apps, networks, or operating system vulnerabilities. If you don't have the required MTD app, you are blocked from signing in to apps such as Microsoft Excel or OneDrive with your work or school account. In this article, you'll learn how to facilitate and set up an MTD app and regain access.    

## MTD apps for Apple devices 

After you receive the prompt to install the MTD app, the system should direct you to your organization's required MTD app. If you aren't redirected but the app name is given, you can install the app directly from the Apple App Store. If no name is given, contact your IT support person for help. 

The following MTD apps are commonly used on Apple devices. Select an app to open its listing in the App Store.   

* [ActiveShield](https://apps.apple.com/app/activeshield/id980234260)
* [Microsoft Defender for Endpoint](https://apps.apple.com/app/microsoft-defender-atp/id1526737990)
* [Lookout for Work](https://apps.apple.com/app/lookout-for-work/id997193468)
* [Pradeo Security](https://apps.apple.com)(opens Apple App Store)
* [Harmony Mobile Protect](https://apps.apple.com/app/sandblast-mobile-protect/id1006390797)
* [SEP Mobile](https://apps.apple.com/app/sep-mobile/id695620821)
* [Sophos Intercept X for Mobile](https://apps.apple.com/app/sophos-mobile-security/id1086924662)
* [Wandera](https://apps.apple.com/app/wandera/id605469330)
* [Zimperium MTD](https://apps.apple.com/app/zimperium-zips/id1030924459)  

## MTD apps for Android 
After you receive the prompt to install the MTD app, the system should direct you to your organization's required MTD app. If you aren't redirected but the app name is given, you can install the app directly from the Google Play Store. If no name is given, contact your IT support person for help. 

The following MTD apps are commonly used on Android devices. Select an app to open its listing in Google Play.  

* [Active Shield Enterprise](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) 
* [Microsoft Defender for Endpoint](https://play.google.com/store/apps/details?id=com.microsoft.scmx)
* [Lookout for Work](https://play.google.com/store/apps/details?id=com.lookout.enterprise&hl)
* [Pradeo Security](https://play.google.com/store/apps/details?id=net.pradeo.service)
* [Harmony Mobile Protect](https://play.google.com/store/apps/details?id=com.lacoon.security.fox)
* [SEP Mobile](https://play.google.com/store/apps/details?id=com.skycure.skycure)
* [Sophos Intercept X for Mobile](https://play.google.com/store/apps/details?id=com.sophos.smsec)
* [Jamf Trust](https://play.google.com/store/apps/details?id=com.wandera.android)
* [Zimperium MTD](https://play.google.com/store/apps/details?id=com.zimperium.zips) 


## Information your organization can see   

Your organization can't see data such as texts, emails, and pictures from your personal apps. MTD apps do report general app information, which is visible to your organization and includes:    

* App name  
* App ID: The unique name that identifies the app in Google Play.  
* App version and short version number: The specific release numbers for an app.  
* App bundle and dynamic size: The amount of space an app uses on your device. 

The level of reporting varies by MTD vendor.  

## Set up MTD app 
This section describes the onscreen setup experience for Apple and Android devices, which includes: 

* Device registration  
* App installation instructions for Apple devices  
* App installation instructions for Android devices  
  
These steps are supplemental and not meant to replace the onscreen instructions. Refer to the onscreen experience or contact your support person for information that's specific to your organization's policies and requirements. 

### Device registration  
Device registration is necessary to confirm your identity and connect your school or work account to your device. If you're on a nonregistered device, the onscreen prompts guide you through registration before you install the MTD app. For more information about device registration, see [Register your personal device on your organization's network](/azure/active-directory/user-help/user-help-register-device-on-network).  

### iOS setup  
These steps begin on the **Get access** screen, which appears after you sign in to a protected work app.  

1. On the **Get access** screen, follow the instructions to install the MTD app that's required by your organization.   
2. Return to the **Get access** screen and select **Open**.  
3. The MTD app asks for permission to open Microsoft Authenticator. Select **Open**. 
4. Select your work account to sign in. 
5. Wait while the MTD app scans your device for security threats. 
6. Return to the school or work app that you were originally trying to access. At this point, your organization might prompt you to configure other app security requirements, such as creating a PIN.   
7. You should now have access to the app. If you're still blocked:  
    * On the **Get access** screen, select **Recheck**.  
    * Go to the MTD app and check for existing threats. Complete the recommended steps to resolve the threat and regain access.    

### Android setup 
These steps begin on the **Get access** screen, which appears after you sign in to a protected work app.  

1. On the **Get access** screen, follow the instructions to install the MTD app that's required by your organization.  
2. Return to the **Get access** screen and select **Open**.  
3. The MTD app asks for your permission to access certain areas of your device, should it need to. In order for this app to work properly, you must **Allow** access to contacts. Requested permissions will vary across MTD vendors.  
4. Select your work account to sign in.  
5. Wait while the MTD app scans your device for security threats.  
6. Return to the school or work app that you were originally trying to access. At this point, your organization might prompt you to configure other app security requirements, such as creating a PIN.  
7. You should now have access to the app. If you're still blocked:  
    * On the **Get access** screen, select **Recheck**.  
    * Go to the MTD app and check for existing threats. Complete the recommended steps to resolve the threat and regain access.  

## Resolving a threat
If a threat is detected and exceeds an acceptable threat level, your organization can either: 
   
* Block access: Block you from using apps while signed in to your work or school account.  
* Wipe data: Delete your work or school data from one or more work apps.  

To resolve a threat and regain access to work apps, complete the following steps.      

1. Open the MTD app on your device.     
2. Open the threat details in the app and read through them. These details explain how the threat could affect your device if left unresolved, and how to resolve it. 
3. Make the required changes on your device. For example, you may need to uninstall an app that's not safe. 
4. Return to the MTD app and start a new scan. 
5. Repeat these steps until all threats are resolved. It can take a few minutes for your changes to sync with the MTD app. Once those changes sync, you can access your work apps again.  

## Get support
Contact your IT support person for help with:

* Identifying which MTD app to use  
* App installation  
* Failed installation  
* Detecting/resolving a threat  
* Uninstalling an MTD app   

Sign into the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) with your work or school account to find your organization's IT helpdesk information.  

## Next steps  

Next, get apps for work or school. For more more information, see:      

* [Use managed apps on your Android device](use-managed-apps-on-your-device-android.md)
* [Use managed apps on your iOS device](use-managed-apps-on-your-device-ios.md)  
