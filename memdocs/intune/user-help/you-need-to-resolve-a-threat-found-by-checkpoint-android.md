---
# required metadata

title: Resolve threats in SandBlast Mobile Protect for Android - Microsoft Intune | Microsoft Docs
description: Learn how to use SandBlast Mobile Protect for Android to keep your device secure.    
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/20/2020
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

#ms.reviewer: heenamac
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Resolve threats found by SandBlast Mobile Protect for Android

SandBlast Mobile Protect is a mobile threat defender app that's integrated with Intune to alert you to potential threats and compliance problems. As long as the threat or problem exists on your device, you might not be able to:   

* Connect to corporate e-mail  
* Connect to corporate Wi-Fi  
* Connect to SharePoint Online  
* Sync corporate files with OneDrive  
* Access internal apps   

This article describes how to use the app to view and resolve threats so that you can maintain your access to these resources.  

## Set up SandBlast Mobile Protect app    
Complete the following steps to set up SandBlast Mobile Protect on your device.  

1. Install the app from [Google Play](https://go.microsoft.com/fwlink/?linkid=2139455). Your organization might let you know that you need to get the app via notification, email, or by installing the app on your device.  
    * Company Portal/Intune app notification: Tap the Company Portal push notification to open Google Play.  
    * Work or school email: Tap the link or scan the QR code provided in that email to open Google Play. 
    * App already installed: Open the app and continue to step 3 to sign in.  
3. When installation is complete, open the app.  
4. Tap your account (the same one you use to sign in to Company Portal) to sign in.  
5. Tap **ACTIVATE** to give the app device administrator permissions.   

After you install the app and sign in, the app will scan your device for threats.  

## Using SandBlast Mobile Protect    
This section describes how to use the app to view and resolve threats and security events.  


### App notifications         
By default, SandBlast Mobile Protect uses two notification methods to alert you to threats:  

* Push notification: Tap the on-screen notification to open the app. 
* Notification in the app's **Threat Center**: After you open the app, tap inside the red circle to go to **Threat Center**.  

As a best practice, do not turn off these notifications. 

If you have Company Portal or the Microsoft Intune app, you'll see warnings in both apps about restricted access. These warnings are related to the threats found in SandBlast Mobile Protect. They will go away after you resolve the threats and check in with Intune.  

 ![Example screenshot of the Company Portal device page, showing the SandBlast Mobile Protect warning.](./media/CP-lookout-virus-banner-1808.png)  

 ### No threat detected   
When no threats are detected, the main app screen shows a glowing, green checkmark. At any time, you can tap **My Devices** to see the complete list of device settings that were scanned. Settings that appear green are compliant with your organization's policies.  

### App threat detected     
An app is considered a threat when it poses a risk to you or your organization's data. Examples of threats include:

* Apps that contain malware
* Apps that are on your organization's block list
* Apps that are installed from unknown sources 

When a threat is present, a red dot appears next to the **MY APPS** icon. To get more details about a threat: 

1. Tap **MY APPS**. 
2. The **SECURITY HISTORY** section shows the number of apps with threats. Tap the number.
3. The **Threat Center** opens. Tap the **i** info icon next to a threat to get more details about the threat, including the steps to resolve it. The quickest way to resolve a threat is to uninstall the affected app.  

To find out why your organization classifies an app as high, medium, or low risk, contact your IT support person.   

### Security event detected  
A security event occurs when SandBlast Mobile Protect prevents an attack before it happens. This type of event is informational and poses no immediate risk on your device. It happens when your organization enforces network protection policies, such as requiring you to use a VPN. 

When an event occurs, you'll see a blue dot next to the **MY NETWORK** icon.  To get more details about a security event:

1. Tap **MY NETWORK**. 
2. The **NETWORK PROTECTION** section shows the number of events that occurred. Tap the number.  
3. The **Event Center** opens. Tap the **i** info icon next to any event to get more details about the prevented threat. 

## Next steps  
Still need help? 

* For the most up-to-date information about SandBlast Mobile Protect, see the SandBlast Mobile Protect user and admin guides on the [Check Point support center website](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk120655). 
* For additional help, contact your IT support person. Check out the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information.  
