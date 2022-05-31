---
# required metadata

title: Enroll devices using a device enrollment manager account
titleSuffix: Microsoft Intune
description: Use the device enrollment manager account to enroll devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/10/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver, shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Add device enrollment managers  

A device enrollment manager (DEM) is a non-administrator user who can enroll devices in Intune. Device enrollment managers are useful to have when you need to enroll and prepare a lot of devices for distribution. People signed in to a DEM account can enroll and manage up to 1,000 devices, while a standard non-admin account can only enroll 15.  

A DEM account requires an Intune user or device license, and an associated Azure AD user. Global Administrators and Intune Service Administrators can add and manage device enrollment managers in the Microsoft Endpoint Manager admin center. 

This article describes the limits and specifications of enrollment manager and how to manage permissions.  

## Supported enrollment methods 

A device enrollment manager can use the following methods to enroll devices in Intune:    

- [Windows Autopilot](../../autopilot/enrollment-autopilot.md)
- [Windows devices bulk enrollment](windows-bulk-enroll.md)
- DEM-initated via Company Portal enrollment   
- DEM-initiated via Azure AD-join  

> [!TIP]
> To compare DEM best practices and capabilities alongside other Windows enrollment methods, see [Intune enrollment method capabilities for Windows devices](./enrollment-method-capab.md).  


## Account permissions 

These Azure AD roles can manage device enrollment managers: 

* Global Administrator 
* Intune Service Administrator role in Azure AD    

They can add and delete device enrollmnet managers, and view all DEM users in the Microsoft Endpoint Manager admin center. You can assign the DEM read-only permission to users who don't meet the role requirements. It lets them see the DEM users they've created.  

## Limitations 

The device enrollment manager account can't be used with all features in Microsoft Intune and has some limitations when used with others. This section describes the limitations you could encounter while sigmed in to a DEM account.  

### Android Enterprise  
You can enroll up to 10 personally owned devices with work profiles. 

The following types of Android Enterprise devices can't be set up via DEM:    

* Corporate-owned with a work profile
* Fully managed  

### Apple Automated Device Enrollment  
DEM is not compatible with Apple Automated Device Enrollment (ADE).   

### Apple volume purchased apps  
* You can't use apps purchased through Apple VPP with Apple VPP user licenses, because of per-user Apple ID requirements for app management.  
* Devices can install VPP apps if they have Apple VPP device licenses.  

### Azure AD  
Applying an Azure AD device restriction to a DEM account will prevent you from reaching the 1,000 device limit that the DEM account can enroll.  

### Conditional access  
Conditional access is only supported with DEM on devices running:  

* Windows 10, version 1803 and later  
* Windows 11     

### Device limit restrictions    
DEM enrolls Windows 10/11 devices in shared device mode, so device limit restrictions won't work on them. Instead, you can configure a hard limit for these devices in the Azure AD admin center. For more information, see [Manage device identities by using the Azure portal](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).       

### Intune Company Portal  

* Device users can't wipe DEM-enrolled devices from Company Portal. You have to sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to wipe these devices.  
* Only the local device appears in the Company Portal app or Company Portal website.   

### Number of accounts  
There's a limit of 150 Device Enrollment Manager (DEM) accounts in Microsoft Intune.  


## Add a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.

2. Select **Add**.

3. On the **Add User** blade, enter a user principal name for the DEM user, and select **Add**. The DEM user is added to the list of DEM users.


## Remove device enrollment manager permissions

Removing a device enrollment manager doesn't affect enrolled devices.

### To remove a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.
2. On the **Device enrollment managers** blade, select the DEM user, and select **Delete**.  
