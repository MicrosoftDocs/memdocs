---
# required metadata

title: Install Mobile Threat Defense on your mobile device
description: Find out what mobile threat defense apps are and how to set one up. 
keywords:
author: lenewsad
ms.author: lanewsad  
manager: dougeby
ms.date: 12/18/2020
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

As part of your organization's security requirements, you might be required to install a mobile threat defense (MTD) vendor app. This type of app detects and alerts you to threats on your device, such as suspicious apps, networks, or OS vulnerabilities.  

If you don't have the required MTD app, you'll be blocked from signing in to protected, managed apps (such as Microsoft Excel or OneDrive) with your work or school account. In this article, you'll learn [how to set up an MTD app](set-up-mobile-threat-defense.md#set-up-mtd-app) and regain access.    

## MTD apps for iOS
The following MTD apps are commonly used on iOS devices. Select an app to open its listing in the App Store.   

* [ActiveShield](https://go.microsoft.com/fwlink/?linkid=2143345)
* [Microsoft Defender for Endpoint](https://go.microsoft.com/fwlink/?linkid=2145949)
* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Pradeo Security](https://go.microsoft.com/fwlink/?linkid=2143272)
* [Harmony Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [SEP Mobile (Symantec Endpoint Protection)](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sophos Intercept X for Mobile](https://go.microsoft.com/fwlink/?linkid=2143414)
* [Wandera](https://go.microsoft.com/fwlink/?linkid=2143505)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## MTD apps for Android 
The following MTD apps are commonly used on Android devices. Select an app to open its listing in Google Play.  

* [Active Shield Enterprise](https://go.microsoft.com/fwlink/?linkid=2143507) 
* [Microsoft Defender for Endpoint (Enterprise)](https://go.microsoft.com/fwlink/?linkid=2144546)
* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Pradeo Security](https://go.microsoft.com/fwlink/?linkid=2143413)
* [Harmony Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [SEP Mobile (Symantec Endpoint Protection)](https://go.microsoft.com/fwlink/?linkid=2139454)
* [Sophos Intercept X for Mobile](https://go.microsoft.com/fwlink/?linkid=2143273)
* [Wandera](https://go.microsoft.com/fwlink/?linkid=2143506)
* [Zimperium Mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142) 


## Information your organization can see   

Your organization can't see any data, such as texts, emails, and pictures, in your personal apps. The MTD app does report information about your apps, such as name and version, to your organization. The actual information reported depends on the MTD vendor your company uses. Your organization might see:   

* App name  
* App ID: The unique name that identifies the app in Google Play.  
* App version and short version number: The specific release numbers for an app.  
* App bundle and dynamic size: The amount of space an app uses on your device. 


## Set up MTD app 
When you sign in to a protected app, you'll be prompted to install an MTD app. Follow the onscreen steps to complete installation and gain access to the protected app. 

For additional context, refer to the [iOS](set-up-mobile-threat-defense.md#ios-setup) or [Android](set-up-mobile-threat-defense.md#android-setup) instructions in this section. These steps are supplemental and not meant to replace the instructions shown on screen. 

If you're prompted to install an MTD app but aren't sure which one to install, contact your IT support person for help.  

### Device registration  
Device registration is necessary to confirm your identity and connect your school or work account to your device. If your device isn't registered, you'll automatically be guided through those steps on screen, before you install the MTD app.   

For more information about device registration, see [Register your personal device on your organization's network](/azure/active-directory/user-help/user-help-register-device-on-network).  

### iOS setup  
These steps begin on the **Get access** screen, which appears after you sign in to a protected app.  

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
These steps begin on the **Get access** screen, which appears after you sign in to a protected app.  

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
If a threat is detected and exceeds your organization's defined threat level, your organization will either:  
   
* Block access: Blocks you from using your organization's protected apps while signed in to your work or school account.  
* Wipe data: Deletes your work or school data from one or more of your organization's protected apps.  

To resolve a threat and regain access to protected apps:  

1. Open the MTD app on your device.     
2. Read through the threat details in the app, which explains how the threat could affect your device if left unresolved, and how to resolve it. 
3. After you make the required changes on your device, return to the MTD app and start a new scan. Repeat these steps until all threats are resolved. It can take a few minutes for your changes to sync with your organization. Once those changes sync, you'll regain access to the protected app. 

## Get support
Go to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) to find your organization's contact information. Contact them for help with:

* Identifying which MTD app to use  
* Installation  
* Failed installation  
* Detecting/resolving a threat  
* Uninstalling an MTD app   
 

### Share app logs with IT support  
You can also send your app logs to your IT support person to provide them with more context about a failed installation.  
* Android users: [Upload and email your logs](./send-logs-to-your-it-admin-by-email-android.md) from Company Portal.   

* iOS device users: [Retrieve and send your logs](/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) from Microsoft Edge for iOS.  


## Next steps  

See the following articles to learn more about how managed apps work, how to get them, and how to recognize that you're using one.  

* [Use managed apps on your Android device](use-managed-apps-on-your-device-android.md)
* [Use managed apps on your iOS device](use-managed-apps-on-your-device-ios.md)  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
