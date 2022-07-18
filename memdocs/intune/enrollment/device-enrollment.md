---
# required metadata

title: What is Microsoft Intune device enrollment
titleSuffix: Microsoft Intune
description: Get an overview of the types of enrollment methods and devices supported in Microsoft Intune. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 5/02/2022
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
  - M365-identity-device-management
  - highpri
---

# What is device enrollment in Intune?  

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To use Microsoft Intune as your mobile device management (MDM) provider, you must enroll devices in Intune using a supported enrollment method. Enrollment sets up and secures the device so that it aligns with your organization's policies and is suitable for use at work or school. Intune deploys and enforces policies through a management profile, which is installed on the device during enrollment. Enrollment is enabled for all platforms by default.  

Microsoft Intune supports Android, macOS, iOS, and Windows devices. Some enrollment methods require you, as the IT administrator, to initiate enrollment while other methods require your employees or students to initiate it. This article provides an overview of the types of devices and enrollment methods that Intune supports.  

## Supported device types  
Microsoft Intune enables mobile device management for:   
* Personal devices, including personally owned phones, tablets, and PCs. 
* Corporate-owned devices, including phones, tablets, and PCs owned by your organization and distributed to employees and students for use at work or school. 

### Personal devices  
Microsoft Intune supports bring-your-own-device, or *BYOD*, enrollment. This type of enrollment enables employees and students to use their personal devices for work or school things. As the admin, you're required to add device users in the Microsoft Endpoint Manager admin center, configure their enrollment experience, and set up Intune policies. Enrollment is initiated and completed by the device user in the Intune Company Portal app.  

> [!NOTE]
> Intune marks devices that are Azure AD-registered as personally-owned devices.  

### Corporate-owned devices  

Microsoft Intune automatically marks certain devices as *corporate-owned*. This classification lets you manage and configure devices with more control and access. For more information about managing and configuring corporate-owned devices, see [Identify devices as corporate-owned](corporate-identifiers-add.md).   

## Compare enrollment options 

Enrollment options vary by operating system (OS). When selecting a method, choose one that works with the devices and features you want to support. 

 In this section, we'll use data tables to compare the available methods. Each table, separated by OS, shows the following data: 

* Method: The enrollment method used to enroll devices in Intune.  
* Enrollment type (Android): The name of the Android enrollment type.    
* Reset required: Tells you if devices are reset to factory default settings during enrollment. Options:  
    * **Yes**: Existing data is wiped from devices during enrollment.  
    * **No**: Existing data is retained on devices during enrollment.  
* User affinity: Tells you whether devices are associated with users during enrollment. Options:  
    * **Yes**: Each device is associated with an Intune-licensed user. 
    * **No**: Devices aren't associated with a user during enrollment, which is a typical configuration for kiosk, point of sale (POS), or shared-utility devices. 
    * **Optional**: Microsoft Intune makes this setting available for you to configure on your own.   
* MDM profile removable: Tells you if users can remove the MDM profile from an enrolled device. Options: 
    * **Yes**: Device users can unenroll devices.  
    * **No**: Device users cannot unenroll devices. 
    * **Configurable via policy** (Android Enterprise): There's a setting in Intune that lets you block factory resets on devices, which prevents users from unenrolling their devices, but it is not configured by default. 

### iOS/iPadOS enrollment methods 
You can use the following methods to enroll iOS/iPadOS devices in Intune:    

* Bring-your-own-device (BYOD)
* Device enrollment manager
* Apple Automated Device Enrollment  
* Setup Assistant enrollment via USB  
* Direct enrollment via USB  

| **Method** | **Reset required** | **User affinity** | **MDM profile removable** | 
|:---:|:---:|:---:|:---:|
|BYOD| No| Yes | Yes | 
|Device enrollment manager| No |No |Yes | 
|Automated Device Enrollment| Yes | Optional | Optional|
|Setup Assistant enrollment via USB| Yes | Optional | Yes| 
|Direct enrollment via USB| No | No | Yes|

For more information about the iOS/iPadOS enrollment methods supported in Intune, see [Enroll iOS/iPadOS devices](ios-enroll.md).  

### macOS enrollment methods  
You can use the following methods to enroll macOS devices in Intune:   

* Bring-your-own-device (BYOD)
* Device enrollment manager
* Apple Automated Device Enrollment  

| **Method** |  **Reset required** |  **User affinity** | **MDM profile removable** |
|:---:|:---:|:---:|:---:|
|BYOD| No| Yes | Yes | 
|Device enrollment manager| No |No |Yes  | 
|Apple Automated Device Enrollment| Yes | Optional | Optional|

For more information about the macOS enrollment methods supported in Intune, see [Set up enrollment for macOS devices](macos-enroll.md).    

### Windows enrollment methods
You can use the following methods to enroll Windows devices in Intune:  

* Bring-your-own-device (BYOD)
* Device enrollment manager
* Automatic enrollment via MDM 
* Automatic enrollment via Group Policy 
* Windows Autopilot
* Bulk enrollment
* Co-management with Microsoft Intune and Configuration Manager 

| **Method** | **Reset required** | **User affinity** | **MDM profile removable** |
|:---:|:---:|:---:|:---:|
|BYOD| No | Yes | Yes | 
|Device enrollment manager| No |No |Yes |
|Automatic enrollment via MDM | No |Yes |Yes | 
|Automatic enrollment via Group Policy|No |Yes |Yes | 
|Windows Autopilot |Yes |Yes |Yes | 
|Bulk enrollment |No |No |Yes | 
|Co-management |No |Yes |Yes | 

For more information about the Windows enrollment methods supported in Intune, see [Enrollment methods for Windows devices ](windows-enrollment-methods.md).  

### Android enrollment methods

To select the appropriate enrollment method for Android devices, consider the enrollment type you'll use and the device's ownership status (personal versus corporate-owned). For more information about the Android enrollment methods supported in Intune, see [Enroll Android devices](android-enroll.md).  

#### Personal Android devices  
You can set up user-initiated enrollment for people who want to use their personal devices at work or school. Employees and students initiate enrollment by signing into the Company Portal app with their work or school account. 

Intune supports the following device management configurations on personal devices: 

* Android Device Administrator (also referred to as *Android Device Admin*)  
* Android Enterprise with work profile

In the table, this data is shown in the Enrollment type column. 

| **Enrollment type** | **Enrollment method** | **Reset required** | **User affinity** | **MDM profile removable** | 
|:---:|:---:|:---:|:---:|:---:|
|Android Device Admin|User-initiated via Company Portal | No | Yes | Yes | 
|Android Enterprise, personal-owned with work profile|User-initiated via Company Portal| No | Yes | Yes |  

#### Corporate-owned Android devices    
Intune supports the following device management configurations on corporate-owned devices: 

* User associated and userless devices created from Android Open Source Project (AOSP) 
* Android Device Administrator (also referred to as *Android Device Admin*)  
* Android Device Admin with Zebra Mobility Extensions 
* Android Enterprise dedicated/kiosk-style  
* Android Enterprise fully managed
* Android Enterprise with work profile

In the table, this data is shown in the Enrollment type column. You can use the following methods to enroll corporate-owned Android devices in Intune:   

* QR code
* Device enrollment manager (DEM) with Company Portal
* User initiated with Company Portal
* Near-field communication (NFC)
* Token entry  
* Google zero-touch enrollment  

| **Enrollment type** | **Enrollment method** | **Reset required** | **User affinity** | **MDM profile removable** |  
|:---:|:---:|:---:|:---:|:---:|
|Android (AOSP) user-associated|QR code|Yes|Yes|Configurable via policy|
|Android (AOSP) userless|QR code|Yes|No|Configurable via policy|  
|Android Device Admin|DEM-initiated via Company Portal| No | No | Yes |
|Android Device Admin|User-initiated via Company Portal with predeclared IMEI or serial number | No | Yes |Yes | 
|Android Device Admin with Zebra Mobility Extensions|User or DEM-initiated via Company Portal| No | Yes if user-initiated; no if DEM-initiated | Yes | 
|Android Enterprise dedicated|NFC, token, QR code, Google zero-touch| Yes | No | Configurable via policy | 
|Android Enterprise fully managed|NFC, token, QR code, Google zero-touch| Yes | Yes | Configurable via policy | 
|Android Enterprise corporate-owned with work profile| NFC, token, QR code, Google zero-touch | Yes | Yes | Configurable via policy | 

## Mobile device record cleanup  

The MDM certificate renews automatically as long as enrolled devices are communicating with the Microsoft Intune service. The MDM certificate doesn't renew for devices that have been wiped, or that fail to sync with Microsoft Intune for an extended period of time. Microsoft Intune deletes idle devices from record 180 days after the MDM certificate expires.  

## Next steps  

You can adjust the settings in Intune to restrict specific platforms from enrolling. For more information, see [Create a device platform restriction](enrollment-restrictions-set.md#create-a-device-platform-restriction).  
