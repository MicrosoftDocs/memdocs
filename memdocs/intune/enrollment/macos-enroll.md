---
# required metadata

title: Set up enrollment for macOS devices
titleSuffix: Microsoft Intune
description: Learn how to set up enrollment for macOS devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/23/2022
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Set up enrollment for macOS devices in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune lets you manage macOS devices to give users access to company email and apps.

As an Intune admin, you can set up enrollment for company-owned macOS devices and personally owned macOS devices ("bring your own device" or BYOD). 

## Prerequisites

Complete the following prerequisites before setting up macOS device enrollment:

- [Make sure your device is eligible for Apple device enrollment](https://support.apple.com/en-us/HT204142#eligibility).
- [Configure domains](../fundamentals/custom-domain-name-configure.md)
- [Set the MDM Authority](../fundamentals/mdm-authority-set.md)
- [Create groups](../fundamentals/groups-add.md)
- [Configure the Company Portal](../apps/company-portal-app.md)
- Assign user licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)

## User-owned macOS devices (BYOD)

You can let users enroll their own personal devices into Intune management. This is known as "bring your own device" or BYOD. After you've completed the prerequisites and assigned user licenses, your users can enroll their devices by:
- Going to the [Company Portal website](https://portal.manage.microsoft.com) or
- Downloading the Mac Company Portal app at [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac).

You can also send your users a link to online enrollment steps: [Enroll your macOS device in Intune](../user-help/enroll-your-device-in-intune-macos-cp.md).

For information about other end-user tasks, see these articles:

- [Resources about the end-user experience with Microsoft Intune](../fundamentals/end-user-educate.md)
- [Using your macOS device with Intune](../user-help/enroll-your-device-in-intune-macos-cp.md)

## Company-owned macOS devices
For organizations that purchase devices for their users, Intune supports the following macOS company-owned device enrollment methods:
- [Apple's Automated Device Enrollment (ADE)](device-enrollment-program-enroll-macos.md): Organizations can purchase macOS devices through ADE. ADE lets you deploy an enrollment profile "over the air" to bring devices into management.
- [Device enrollment manager (DEM)](device-enrollment-manager-enroll.md): You can use a DEM account to enroll up to 1,000 devices.
- [Direct enrollment](device-enrollment-direct-enroll-macos.md): Direct enrollment doesn't wipe the device.

## Block macOS enrollment
By default, Intune lets macOS devices enroll. To block macOS devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).

## Enroll virtual macOS machines for testing

> [!NOTE]
> Intune supports macOS virtual machines for testing purposes only. Don't use macOS virtual machines as official devices for employees or students.  

Intune supports virtual machines running:

* Parallel Desktop
* VMware Fusion  
* Apple Silicon  

Intune needs to know the VM's hardware model and serial number to recognize and enroll it as a device. If you try to enroll a VM without providing those details, enrollment fails. This section provides more information about how to satisfy this requirement before enrollment. 

### Parallels Desktop 
Modify the VM's configuration settings to add or change a VM serial number and hardware model identifier. Enter any string of alphanumeric characters for the serial number. For hardware model, we recommend using the model of the device that's running the VM. To find your Mac's hardware model, select the Apple menu and go to **About This Mac** > **System Report** > **Model Identifier**.   

For more information, see the following topics in the Parallels knowledge base:  

* [How to enroll a macOS VM in Parallels Desktop using Intune](https://kb.parallels.com/en/124564)  
* [How to find and change the serial number](http://kb.parallels.com/123455)  


### VMware Fusion
Add the following lines to your .vmx file to set the VM's hardware model and serial number. The values shown in this sample are examples.  

```
serialNumber = "ABC123456789"  
hw.model = "MacBookAir10,1"  
```

Enter any string of alphanumeric characters for the serial number. For hardware model, we recommend using the model of the device that's running the VM. To find your Mac's hardware model, select the Apple menu and go to **About This Mac** > **System Report** > **Model Identifier**.   

See the VMware customer connect website for more information about [editing the .vmx file for your VMware Fusion VM](https://kb.vmware.com/s/article/1014782).  

### Apple Silicon 
No changes are required for virtual machines running on Apple Silicon hardware. Parallels Desktop and VMware Fusion are supported on Macs with Apple Silicon, so if you set up a VM this way, you don't need to modify the hardware model ID or serial number. 

## User Approved enrollment

User Approved MDM enrollment is a type of macOS enrollment that you can use to manage certain security-sensitive settings. For more information, see [Apple's support documentation](https://support.apple.com/HT208019).  
 
As of June 2020, all new macOS MDM enrollments in Intune, including those not done through Automated Device Enrollment (ADE), are considered user approved. The end-user must manually install the management profile in **System Preferences** > **Profiles**, and thus provide approval of the management profile. System Preferences is launched automatically from the Company Portal app for BYOD macOS users. [Instructions to install the management profile](../user-help/enroll-your-device-in-intune-macos-cp.md) are provided in the Company Portal app.     

BYOD macOS MDM enrollments prior to June 2020 may not be user approved if the end-user did not manually provide approval of the management profile in **System Preferences** > **Profiles**. For BYOD enrollments after June 2020, the Company Portal app launches **System Preferences** for the user and the user will need to select Install. If the user didn't approve the management profile during enrollment, the user can go to **System Preferences** > **Profiles**, choose the management profile, and select **Approve** to approve the profile at a later point in time.

### Find out if a device is User Approved
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices**> choose the device > **Hardware**.
3. Check the **User approved enrollment** field.


## Next steps

After macOS devices are enrolled, you can [create custom settings for macOS devices](../configuration/custom-settings-macos.md).