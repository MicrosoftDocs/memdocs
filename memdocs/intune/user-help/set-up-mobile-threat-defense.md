---
# required metadata

title: Install Mobile Threat Defense on your mobile device
description: Learn how to install Mobile Threat Defense on your mobile device.
keywords:
author: lenewsad
ms.author: lanewsad  
manager: dougeby
ms.date: 04/27/2020
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

#ms.reviewer: aanavath  
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---  

# Install Mobile Threat Defense   

As part of your organization's security requirements, you might be required to install a Mobile Threat Defense (MTD) vendor app. This type of app detects and alerts you to threats on your device, such as suspicious apps, networks, or OS vulnerabilities.  

If you don't have the required MTD app, you'll be blocked from signing in to protected apps with your work or school account. In this article, you'll learn [how to install an MTD app](set-up-mobile-threat-defense.md#install-app) to get unblocked.  

There are a variety of MTD vendor apps available to install, all with different names. Your organization will let you know which one to use. If you're prompted to install the app but aren't given further instructions or a link to get the app, contact your IT support person. 


## Information your organization can see   

Your organization can't see any data, such as texts, emails, and pictures, in your personal apps. The MTD app does report information about your apps, such as name and version, to your organization. The actual information reported depends on the MTD vendor your company uses. Your organization might see:   

* App name  
* App ID: The unique name that identifies the app in Google Play.  
* App version and short version number: The specific release numbers for an app.  
* App bundle and dynamic size: The amount of space an app uses on your device. 


## Install app    
When you sign in to a protected app, you'll automatically be prompted to install an MTD app. Follow the onscreen steps to complete installation. Use the steps in this section for additional help.  
 
You might also be prompted to register your device. Registration is necessary to confirm your identity and connect your school or work account to your device. If you're not registered, you'll automatically be guided through that setup before you install the MTD app. When you get to the **Get access** screen, you can start the installation steps.  

For more information about device registration, see [Register your personal device on your organization's network](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### iOS setup  

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

1. On the **Get access** screen, follow the instructions to install the MTD app that's required by your organization.  
2. Return to the **Get access** screen and select **Open**.  
3. The MTD app asks for your permission to access certain areas of your device, should it need to. In order for this app to work properly, you must **Allow** access to contacts. Requested permissions will vary across MTD vendors.  
4. Select your work account to sign in.  
5. Wait while the MTD app scans your device for security threats.  
6. Return to the school or work app that you were originally trying to access. At this point, your organization might prompt you to configure other app security requirements, such as creating a PIN.  
7. You should now have access to the app. If you're still blocked:  
    * On the **Get access** screen, select **Recheck**.  
    * Go to the MTD app and check for existing threats. Complete the recommended steps to resolve the threat and regain access.  

### Installation failed  

If the installation fails, contact your IT support person. Go to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) to find your organization's contact information.  

You can also send your app logs to your IT support person to provide them with more context about the installation.  
* Android users: [Upload and email your logs](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) from Company Portal.   

* iOS device users: [Retrieve and send your logs](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) from Microsoft Edge for iOS.  

## Resolve a threat  
If a threat exceeds your organization's defined threat level, your organization will either:  
   
* Block access: Blocks you from using your organization's protected apps while signed in to your work or school account.  
* Wipe data: Deletes your work or school data from one or more of your organization's protected apps.  

To resolve a threat and regain access, open the MTD app on your device. Read through the provided information to learn how the threat could affect your device and how to resolve it. After you follow the steps to resolve the threat, go back to the MTD app and initiate a new scan. It might take a few minutes to regain access to your organization.  

## Next steps  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).

