---
# required metadata

title: Resolve threats in Harmony Mobile Protect for Android - Microsoft Intune | Microsoft Docs
description: Learn how to use Harmony Mobile Protect for Android to keep your device secure.    
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2022
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 449c34ec-2d94-4c7f-8691-a5200efee3cb
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: heenamac
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Resolve threats found by Harmony Mobile Protect for Android

Harmony Mobile Protect is a mobile threat defender app that's integrated with Intune to alert you to potential threats and compliance problems. As long as the threat or problem exists on your device, you might not be able to:   

* Connect to corporate e-mail  
* Connect to corporate Wi-Fi  
* Connect to SharePoint Online  
* Sync corporate files with OneDrive  
* Access internal apps   

This article describes how to use the app to view and resolve threats.  

## Set up Harmony Mobile Protect app    
Complete the following steps to set up Harmony Mobile Protect on your device.  

1. Install the app from [Google Play](https://go.microsoft.com/fwlink/?linkid=2139455). Your organization might let you know that you need to get the app via notification, email, or by installing the app on your device.  
    * Company Portal/Intune app notification: Tap the push notification to open Google Play.  
    * Work or school email: Tap the link or scan the QR code provided in that email to open Google Play. 
    * App already installed: Open the app and continue to step 3 to sign in.  
3. When installation is complete, open the app.  
4. Tap your account (the same one you use to sign in at work or school) to sign in.  
5. Tap **ACTIVATE** to make the app a device administrator.  

After your initial sign-in, the app will scan your device for threats.  

## Using Harmony Mobile Protect    
Harmony Mobile Protect detects device threats, app threats, and network security events. This section describes how to use the app to view and resolve each type of threat. 

### Get threat notifications         
By default, Harmony Mobile Protect uses push notifications and its in-app **Threat Center** to alert you to threats and events. As a best practice, do not turn off these notifications.  

 ### View overall device status  
The app's main screen shows the current status and threat count, if applicable. 

* No threat or events detected: The screen shows a green circle with a checkmark. 

* Threats detected: The screen shows a red circle with the number of threats detected.  

* Security event occurred: The screen shows a blue circle with the number of events that occurred.  

## View device threats 
A device threat happens when the settings on your device don't meet your organization's requirements. When a threat is present, a red dot appears next to the **MY DEVICES** icon. To get more details about a threat: 

1. Tap **MY DEVICES** to open the list of settings that were scanned on your device. 
2. Settings that appear in red do not meet your organization's requirements. Tap a red setting to find out more information about it.
3. Open the Settings app on your device to adjust the setting.  
4. If Harmony Mobile Protect doesn't show the threat as resolved right away, return to the app and tap the circle on the main app page to initiate a new scan.  

### View app threats      
An app is considered a threat when it poses a security risk to you or your organization's data. Examples of threats include:

* Apps that contain malware
* Apps that are on your organization's block list
* Apps that are installed from unknown sources 

When a threat is present, a red dot appears next to the **MY APPS** icon. To get more details about a threat: 

1. Tap **MY APPS**. 
2. The **SECURITY HISTORY** section shows the number of apps with threats. Tap the number.
3. The **Threat Center** opens. Tap the **i** info icon next to a threat to get more details about the threat, including the steps to resolve it. The quickest way to resolve a threat is to uninstall the affected app.  

To find out why your organization classifies an app as high, medium, or low risk, contact your IT support person.   

### View security events   
A security event occurs when Harmony Mobile Protect prevents an attack before it happens. This type of event is informational and poses no immediate risk on your device. They could happen if your organization enforces network protection policies, such as requiring you to use a VPN. 

When an event occurs, you'll see a blue dot next to the **MY NETWORK** icon.  To get more details about a security event:

1. Tap **MY NETWORK**. 
2. The **NETWORK PROTECTION** section shows the number of events that occurred. Tap the number.  
3. The **Event Center** opens. Tap the **i** info icon next to any event to get more details about the prevented threat. 

## Next steps  
If you use Company Portal or the Intune app, open the app and sync your device after you resolve a threat. Otherwise, you'll have to wait until Intune checks in with your device to regain access to corporate resources.   

Still need help? 

* For the most up-to-date information about Harmony Mobile Protect, see the Harmony Mobile Protect user and admin guides on the [Check Point support center website](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk120655). 
* For additional help, contact your IT support person. Check out the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information.  
