---
# required metadata

title: Automatically enroll devices with Samsung Knox Mobile Enrollment
titleSuffix: Microsoft Intune
description: Learn how to enroll Android devices in Microsoft Intune with the Knox Mobile Enrollment tool.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/01/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 30df0f9e-6e9e-4d75-a722-3819e33d480d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
---

# Enroll devices in Microsoft Intune with Samsung Knox Mobile Enrollment  

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)] 

Use Samsung Knox Mobile Enrollment as a tool to bulk enroll enterprise devices in Microsoft Intune. Knox Mobile Enrollment enables device enrollment to happen straight out-of-the-box after you turn on the device. Enrollment is supported for the following Android Enterprise device types:  

* Dedicated devices  
* Fully managed devices    
* Corporate-owned devices with a work profile  

You must have a Samsung Knox account to access Knox Mobile Enrollment services in the Knox Admin Portal. Samsung Knox accounts require approval from Samsung, which can take one to two business days.  

## Create profile  

To use Microsoft Intune and Knox Mobile Enrollment together, create a profile in the Knox Admin Portal. Add Microsoft Intune to the profile as your enterprise mobility management (EMM) solution. 

**Custom JSON data** appears optional in the Knox Admin Portal, but Microsoft Intune requires it for a successful enrollment. Enter the following JSON data:   

 `{"com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "enter Intune enrollment token string"}`  

 Add your enrollment token to the string where indicated. Additionally, configure these device settings in the profile:  

   * **QR code for enrollment** (optional): Add a QR code to speed up device enrollment. 
   * **System applications**: Leave all system apps enabled to ensure all apps are available in the profile. If you don't select this value, some default system apps are excluded from the apps tray. 
   * **Company name**: Enter your organization's name. The name appears onscreen during device enrollment.  

## Upload devices  
Assign your profile to Android devices uploaded in the Knox Admin Portal. Supported upload methods include:  
 
* Samsung-approved resellers: A Samsung-approved reseller can automatically upload your organization's purchased devices in the Knox Admin Portal, where you can manage them. Use this option if you purchase devices through a Samsung-approved reseller.  

* Knox Deployment App: You don't need to work with a reseller to upload devices in the Knox Deployment App. We recommend using the app for enrolling existing devices that were previously set up in Knox Mobile Enrollment. You can use Bluetooth or NFC to add devices to the Knox Admin Portal.  

## Resources  

For more information about Knox Mobile Enrollment setup and requirements, see:  

* [Get started with Knox Mobile Enrollment](https://docs.samsungknox.com/admin/knox-mobile-enrollment/get-started/get-started-with-knox-mobile-enrollment/)  
* [About Knox Deployment App](https://docs.samsungknox.com/admin/knox-mobile-enrollment/about-kda.htm)  
