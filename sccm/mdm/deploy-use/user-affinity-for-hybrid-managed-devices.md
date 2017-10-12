---
title: "User affinity for hybrid managed devices"
titleSuffix: "Configuration Manager"
description: "Configure user affinity for managed devices in Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: 6
author: dougeby
ms.author: dougeby
manager: angrobe
---
# User affinity for hybrid managed devices in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When configuring profiles for corporate-owned devices, the administrator can specify whether the managed devices can have *user affinity* which identifies a specific user with the device.  

##  <a name="BKMK_iOSCP"></a> Managed devices with user affinity  
 Devices configured with **user affinity** can install and run the Company Portal app to download apps and manage devices. Once users receive their devices they must complete a number of additional steps  to complete the Setup Assistant and install the Company Portal app.  

#### How to enroll iOS devices with user affinity  

1.  When users first power on their new devices, they are prompted to complete the Setup Assistant. The enrollment profile can specify to prompt for credentials during setup. Users must use the credentials (i.e. the unique personal name or UPN) associated with their subscription in Intune.  

2.  During setup, users can also be prompted for an Apple ID. An Apple ID must be provided before the device can install the Company Portal. Users can provide an Apple ID after setup is complete from the iOS **Settings** menu.  

3.  After completing setup, the iOS device must install the Company Portal app from the App Store, for example [Company Portal app](https://itunes.apple.com/us/app/id719171358).  

4.  The user can now login to the Company Portal with the UPN used when setting up the device.  

5.  After logging in, the user is prompted to enroll their device. The first step is to **Identify their device**. The app presents a list of iOS devices that are corporate-enrolled and assigned to the end-user’s Intune account. Choose the matching device.  

     If this device is not already corporate-enrolled, select “new device” to continue with the standard enrolment flow.  

6.  On the next screen, the user must confirm the serial of the new device. The user can tap on the link “confirm the Serial Number” to launch the Settings app to verify the serial number. The user must then enter the last 4 characters of the serial number into the Company Portal app.  

     This step verifies that the device is the corporate device enrolled in Intune. If the serial number on the device does not match, the wrong device was selected. Go back to the previous screen and select a different device.  

7.  After the serial number is verified, the Company Portal app redirects to the Company Portal website to finalize enrolment, and then prompts the user to return to the app.  

8.  Enrollment is now complete. You can now use this device with the full set of capabilities.  

##  <a name="BKMK_noUA"></a> Managed devices without user affinity  
 Devices configured with **no user affinity** do not support the Company Portal and should not install the app. The Company Portal is designed for users who have corporate credentials and require access to personalized corporate resources (e.g. email). Device enrolled with **no user affinity** are not intended to have a dedicated user sign in. Kiosk, point of sale (POS), or shared utility devices are typical use-cases for devices enrolled with no user affinity. If user affinity is required, be sure the device’s enrollment profile has **User Affinity** selected prior to enrolling the device. To change the affinity status on a device, you must retire and re-enroll the device.
