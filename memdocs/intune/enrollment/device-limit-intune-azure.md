---
# required metadata

title: Understand Intune and Microsoft Entra device limit restrictions
titleSuffix: Microsoft Intune
description: Learn the differences between Intune device limit restrictions and Microsoft Entra device limit restrictions. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/14/2024
ms.topic: concept-article
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- highpri
---

# Understand Intune and Microsoft Entra device limit restrictions  

**Applies to**

- Android
- iOS
- macOS
- Windows 10
- Windows 11

There are two ways to limit the number of devices an employee or student can use for work or school. You can:  

* Configure device limit restrictions in the Microsoft Intune admin center.  
* Configure a device limit in the Microsoft Entra admin center.  

This article provides an overview of each limitation, and describes the device conditions and provisioning scenarios that support them.   

## Intune device limit restrictions

Configure Intune device limit restrictions to limit the number of devices a user can enroll in Microsoft Intune. You can allow a user to enroll up to 15 devices. To create a device limit restriction, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **Enrollment**. For more information, see [Create a device limit restriction](create-device-limit-restrictions.md). 

Intune device limit restrictions don't apply to devices enrolled via:  

- Android device administrator + device enrollment manager
- Android Enterprise dedicated device  
- Co-management with Configuration Manager   
- Automatic enrollment + group policy  
- Automatic enrollment + device enrollment manager  
- Automatic enrollment + bulk device enrollment
- Automatic enrollment initiated by user through desktop (for example, when they [connect a work or school account in the Windows Settings app](https://support.microsoft.com/windows/manage-user-accounts-in-windows-104dc19f-6430-4b49-6a2b-e4dbd1dcdf32))  
- Windows Autopilot  

Devices enrolled via these methods are enrolled automatically or by an Intune admin, not by an employee or student, and are considered shared devices. Instead, you can apply the Microsoft Entra limit, where supported.   

## Microsoft Entra device limit  

Configure the *maximum number of devices per user* in Microsoft Entra to limit the number of devices that can join or register with Microsoft Entra. To access this setting:  

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).   
2. Go to **Identity** > **Devices** > **Device settings**.

The limit applies to devices that are Microsoft Entra joined or Microsoft Entra registered, with some exceptions. It isn't applicable to Microsoft Entra hybrid joined devices, and devices enrolled via:   

- Android Enterprise dedicated device   
- Windows automatic enrollment + bulk device enrollment  
- Windows automatic enrollment + group policy  

For more information about configuring these setting in Microsoft Entra ID, see [Configure device settings](/azure/active-directory/devices/device-management-azure-portal).  

## Applicable scenarios        
Use the following table to determine the type of limitations you can apply to devices.    

|Platform| Device management solution | User affinity | Does Microsoft Entra limitation apply? | Does Intune limitation apply? |  
| -----| ----- | ----- | ----- | ----- |
|Android| Android Enterprise personally owned work profile | Yes | Yes | Yes|  
|Android| Android Enterprise dedicated device | No | No | No |  
|Android| Android Enterprise fully managed | Yes | Yes | Yes |  
|Android| Android Enterprise corporate-owned work profile | Yes | Yes | Yes |  
|Android| Android device administrator | Yes | Yes | Yes |  
|Android| Android device administrator + device enrollment manager | No | Yes | No | 
|iOS and macOS| BYOD: Apple User Enrollment | Yes | Yes | Yes |  
|iOS and macOS| BYOD: Apple Device Enrollment | Yes | Yes | Yes |  
|iOS and macOS| Apple Automated Device Enrollment | Yes | Yes | Yes |  
|Windows 10/11| BYOD: User enrollment | Yes | Yes | Yes |   
|Windows 10/11| Automatic enrollment + group policy | No | No | No |  
|Windows 10/11| Automatic enrollment + device enrollment manager | No | Yes | No | 
|Windows 10/11| Automatic enrollment + bulk device enrollment | No | No | No |
|Windows 10/11| Windows Autopilot | Yes | Yes | No |  
|Windows 10/11| Co-management with Configuration Manager | No | Yes | No |  

## Android and iOS devices  
 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]  

### iOS or Android devices example 1  

- The Microsoft Entra **Maximum number of devices per user** setting is set to 3.
- The Intune **Device limit** setting is set to 5.
 
**Outcome:** You can enroll up to 3 devices, because the Microsoft Entra ID limits users to a maximum of 3 devices. If you try to enroll more than three devices in Intune, enrollment fails because the fourth device is blocked from registering in Microsoft Entra ID.  

### iOS or Android devices example 2

- The Microsoft Entra **Maximum number of devices per user** setting is set to 20.
- The Intune **Device limit** setting is set to 2.

**Outcome:** You can successfully register and enroll two devices. Intune enrollment will be blocked for any additional devices. The Microsoft Entra limit only applies to Apple automated device enrollment when devices are configured with user affinity. 

## Windows devices  

### Windows 10/11 example 1

- The Microsoft Entra **Maximum number of devices per user** setting is set to 5.  
- The Intune **Device limit** setting is set to 3.  
- The devices are Microsoft Entra hybrid joined and enrolled automatically (GPO configured).  

**Outcome:** Because the enrollment is provisioned by GPO, the Microsoft Entra device limit doesn't apply. The Intune device limit restriction also doesn't apply.  

### Windows 10/11 example 2  

- The Microsoft Entra **Maximum number of devices per user** setting is set to 5.
- The Intune **Device limit** setting is set to 2.
- The devices are local domain joined, and enrolled in the Settings app.  

**Outcome:** You can only enroll two devices before they're blocked. You can register up to five devices.  


## Next steps

- [Create a device limit restriction in Azure.](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Learn more about registration and domain joined.](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)
