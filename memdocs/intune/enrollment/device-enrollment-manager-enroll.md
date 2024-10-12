---
# required metadata

title: Enroll devices using a device enrollment manager account
titleSuffix: Microsoft Intune
description: Use the device enrollment manager account to enroll devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/24/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Add device enrollment managers  

A device enrollment manager (DEM) is a nonadministrator user who can enroll devices in Intune. Device enrollment managers are useful to have when you need to enroll and prepare many devices for distribution. People signed in to a DEM account can enroll and manage up to 1,000 devices, while a standard nonadmin account can only enroll 15.  

> [!TIP]
> The following enrollment methods allow standard nonadmin accounts to enroll more than 15 devices:  
>  - Co-management with Configuration Manager
>  - Automatic enrollment + group policy 
>  - Windows Autopilot
>    
> If you're using these methods to enroll devices, you do not need to use a DEM account.  

A DEM account requires an Intune user or device license, and an associated Microsoft Entra user. This article describes the limits and specifications of DEM accounts and how to manage permissions.  

## Supported enrollment methods 

A device enrollment manager can use the following methods to enroll devices in Intune:    

- [Bulk enrollment using a provisioning package](windows-bulk-enroll.md)
- DEM-initiated via Company Portal enrollment   
- DEM-initiated via Microsoft Entra join  

> [!TIP]
> To compare DEM best practices and capabilities alongside other Windows enrollment methods, see [Intune enrollment method capabilities for Windows devices](../fundamentals/deployment-guide-enrollment-windows.md).  


## Role based access control   

To manage device enrollment manager accounts in Microsoft Intune, you must be an [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator). The Intune Administrator role can *update* and *read* device enrollment manager accounts.

|Permission| Description |
|---------------|------------|
|Update | Create new device enrollment manager accounts, or delete device enrollment manager accounts. |  
|Read | View the list of device enrollment manager accounts. | 

## Add a device enrollment manager

> [!TIP]
> Only use dedicated accounts that are not assigned to an individual user as Device enrollment manager accounts. 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **Enrollment**.  
3. Select the **Device enrollment managers** tab.  
4. Choose **Add**.
3. In the **User name** field, enter the user principal name of the user you're adding.
6. Select **Add**. The new device enrollment manager is added to the list of DEM users. 

To remove someone as a device enrollment manager, select their name in the list and then choose **Delete**.

> [!TIP]
> Do not delete accounts assigned as a Device enrollment manager if any devices were enrolled using the account. Doing so will lead to issues with these devices. 

## Limitations 

The device enrollment manager account can't be used with all features in Microsoft Intune and has some limitations when used with others. This section describes the limitations you could encounter while setting up devices from a DEM account.  

### Android Enterprise  
You can enroll up to 10 personally owned devices with work profiles. 

The following types of Android Enterprise devices can't be set up via DEM:    

  * Corporate-owned devices with a work profile
  * Fully managed devices  

### App assignments  
There are no users associated with a DEM-enrolled device, so apps can't be deployed as **Available**. 

### Apple Automated Device Enrollment  
DEM isn't compatible with Apple Automated Device Enrollment (ADE).

### Android open source project (AOSP)
AOSP doesn't support DEM accounts.


### Apple volume purchased apps  
DEM-enrolled devices can install VPP apps if they have Apple VPP device licenses. You can't use apps purchased through Apple VPP with Apple VPP user licenses, because of per-user Apple ID requirements for app management.  

<a name='azure-ad'></a>  

### Microsoft Entra ID  
Applying a Microsoft Entra maximum device limit of less than 1,000 to a DEM account prevents you from reaching the 1,000 device limit that the DEM account can enroll.  

### Certificates  
You must use device-level certificates to manage Wi-Fi and email connections.  

### Conditional access  
Conditional access is only supported with DEM on devices running:  

* Windows 10, version 1803 and later  
* Windows 11     

### Device limit restrictions    
DEM enrolls Windows 10/11 devices in shared device mode, so device limit restrictions won't work on them. Instead, you can configure a hard limit for these devices in the Microsoft Entra admin center. For more information, see [Manage device identities](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).       

### Intune Company Portal  
Only the local device appears in the Company Portal app or Company Portal website. Device users can't wipe DEM-enrolled devices from Company Portal. You have to sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to wipe these devices.  

### Number of accounts  
There's a limit of 150 DEM accounts in Microsoft Intune.  

### VPN profiles  
User-based VPN profiles don't work with DEM-enrolled devices.  
