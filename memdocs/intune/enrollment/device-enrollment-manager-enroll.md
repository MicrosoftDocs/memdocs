---
# required metadata

title: Enroll devices using a device enrollment manager account
titleSuffix: Microsoft Intune
description: Use the device enrollment manager account to enroll devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/02/2021
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

A device enrollment manager is a non-administrator user who can enroll devices in Intune. DEMS are useful to have when you need to enroll and prepare devices before handing them out to . DEM users can enroll up to 1,000 devices, while a standard non-admin account in Intune can only enroll 15.  

A DEM account requires an Intune user or device license. To enable the feature for someone in you organization, you must assign the Intune device enrollment manager permissions to their Azure AD account.  This article provides an overview of device enrollment manager accounts, limitations, and how to manage permissions.  

## Supported enrollment methods 

A device enrollment manager can use the following methods to enroll devices in Intune:    

- [Windows Autopilot](../../autopilot/enrollment-autopilot.md)
- [Windows devices bulk enrollment](windows-bulk-enroll.md)
- DEM initiated via Company Portal
- DEM initiated via Azure AD join  

> [!TIP]
> To compare DEM best practices and capabilities alongside other Windows enrollment methods, see [Intune enrollment method capabilities for Windows devices](./enrollment-method-capab.md).  


## Account permissions 

Users assigned the Global Administrator or Intune Service Administrator role in Azure AD can:   

- Assign DEM permissions      
- See all DEM users in the admin center  

DEMs assigned read-only permissions in Azure AD can only see the DEM users they've created.    

## Limitations 

This section describes the limitations that comes with enrolling devices from your DEM account.      

### Android Enterprise  
You can enroll up to 10 personally-owned devices with work profiles. 

The following types of devices can't be set up with a DEM account: 

* Corporate-owned with a work profile
* Fully managed  

### Automated Device Enrollment  
DEM is not compatible with Apple Automated Device Enrollment (ADE).   

### Azure AD  
Applying an Azure AD device restriction to a DEM account will prevent you from reaching the 1,000 device limit that the DEM account can enroll.  

### Conditional access  
Conditional access is only supported with DEM on devices running:  

* Windows 10, version 1803 and later  
* Windows 11     

### Device limit restrictions    
DEM enrolls Windows 10/11 devices in shared device mode, so device limit restrictions won't work on them. Instead, you can configure a hard limit for these devices in the Azure AD admin center. For more information, see [Manage device identities by using the Azure portal](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).       

### Device wipe    
Enrolled devices can't be wiped from Company Portal. You have to sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to wipe a device you enrolled.  

### Intune Company Portal  
Only the local device appears in the Company Portal app or Company Portal website.   

### Number of accounts  
There's a limit of 150 Device Enrollment Manager (DEM) accounts in Microsoft Intune.  

### Volume purchased apps  
* You can't use apps purchased through Apple VPP with Apple VPP user licenses, because of per-user Apple ID requirements for app management.  
* Devices can install VPP apps if they have Apple VPP device licenses.  

## Add a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.

2. Select **Add**.

3. On the **Add User** blade, enter a user principal name for the DEM user, and select **Add**. The DEM user is added to the list of DEM users.


## Remove device enrollment manager permissions

Removing a device enrollment manager doesn't affect enrolled devices.

### To remove a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.
2. On the **Device enrollment managers** blade, select the DEM user, and select **Delete**.  
