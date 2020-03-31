---
# required metadata

title: How to use the Intune Company Portal app in environments without Google Mobile Services
titleSuffix: Microsoft Intune
description: Learn how you can use the Intune Company Portal app in environments without Google Mobile Services.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use the Intune Company Portal app in environments without Google Mobile Services

The Intune Company Portal app for Android uses Google Mobile Services (GMS) to communicate with the Microsoft Intune service. In some cases, devices may temporarily or permanently not have access to GMS. For example, a device might ship without GMS, or the device may be connecting to a closed network where GMS is not available. This document summarizes the differences and limitations you may observe when installing and using the Intune Company Portal without GMS. 

## Install the Intune Company Portal app without access to the Google Play Store 

### For users outside of mainland China 

If Google Play isn't available, Android devices can download the [Microsoft Intune Company Portal for Android](../user-help/install-the-company-portal-app-android.md) and sideload the app. When installed this way, the app doesn't receive updates or fixes automatically. You must be sure to regularly update and patch the app manually. 

### For users in mainland China 

Because the Google Play Store is currently not available in mainland China, Android devices must obtain apps from Chinese app marketplaces. For more information, see Installing the Intune Company Portal app in mainland China.

## Limitations of Intune device administrator management when GMS is unavailable 

### Unavailable Intune features

Some Intune features rely on components of GMS such as the Google Play store or Google Play services. Because these components are not available in environments without GMS, the following features in the Intune administrator console may be unavailable.  

| Scenario  | Features  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device compliance policies  | When creating or editing compliance policies for Android device administrator, all options listed under **Google Play Protect** are unavailable.  |
| App protection policies (conditional launch)  | **SafetyNet device attestation** and **Require threat scan on apps** device conditions cannot be used for conditional launch.  |
| Client apps  | Apps of type **Android** are not available. Use **Line-of-business app** instead to deploy and manage apps.  |
| Mobile Threat Defense  | Work with your MTD vendor to understand if their solution is integrated with Intune, if it is available in the region of interest, and if it relies on GMS.  |

### Some tasks may be delayed 

In environments where GMS is available, Intune relies on push notifications to speed tasks to finish. For example, if you try to remotely wipe the device, notifications generally get to the device in seconds. In conditions where GMS isn’t available, push notifications may also not be available. Therefore, Intune must wait for the next device check-in time to complete the tasks.  

Enrolled Android devices report to Intune every 8 hours. For example, if a device reports to Intune at 1 PM and the remote tasks are issued at 1:05 PM, Intune will contact the device at 9 PM to complete the tasks. 

The following tasks can require up to 8 hours to finish: 

| Intune Administrator Console  | Intune Company Portal app for Android  | Intune Company Portal Website  |
|---------------------------------|--------------------------------------------------|------------------------------------|
| Full wipe  | Remote device removal  | Device removal (local and remote)  |
| Selective wipe  | Device reset  | Device reset  |
| New or updated app deployments  | Installation of available line-of-business apps  | Device passcode reset  |
| Remote lock  |    |    |
| Passcode reset  |    |    |

If the device recently enrolled, the compliance, non-compliance, and configuration check-in runs more frequently. For more information on device check-ins, see [Common questions, issues, and resolutions with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## Next steps

- [Add apps](apps-add.md)
