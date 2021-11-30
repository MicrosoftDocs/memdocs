---
# required metadata

title: Set up enrollment for macOS devices
titleSuffix: Microsoft Intune
description: Learn how to set up enrollment for macOS devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/12/2020
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
- [Direct enrollment](device-enrollment-direct-enroll-macos.md): Direct enrollment does not wipe the device.

## Block macOS enrollment
By default, Intune lets macOS devices enroll. To block macOS devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).

## Enroll virtual macOS machines for testing

> [!NOTE]
> macOS virtual machines are only supported for testing. You should not use macOS virtual machines as production devices for your end users. 

You can enroll macOS virtual machines for testing using either Parallels Desktop or VMware Fusion. 

For Parallels Desktop, you need to set the hardware type and the serial number for the virtual machines so that Intune can recognize them. Follow Parallels' instructions for setting hardware type and [serial number](http://kb.parallels.com/123455) to set up the necessary settings for testing. We recommend that you match the hardware type of the device running the virtual machines to the hardware type of the virtual machines that you're creating. You can find this hardware type in **Apple menu** > **About this Mac** > **System Report** > **Model Identifier**. 

For VMware Fusion, you need to [edit the .vmx file](https://kb.vmware.com/s/article/1014782) to set the virtual machine's hardware model and serial number. We recommend that you match the hardware type of the device running the virtual machines to the hardware type of the virtual machines that you're creating. You can find this hardware type in **Apple menu** > **About this Mac** > **System Report** > **Model Identifier**. 

## User Approved enrollment

User Approved MDM enrollment is a type of macOS enrollment that you can use to manage certain security-sensitive settings. For more information, see [Apple's support documentation](https://support.apple.com/HT208019).  
 
As of June 2020, all new macOS MDM enrollments in Intune, including those not done through Automated Device Enrollment (ADE), are considered user approved. The end-user must manually install the management profile in **System Preferences** > **Profiles**, and thus provide approval of the management profile. System Preferences is launched automatically from the Company Portal app for BYOD macOS users. [Instructions to install the management profile](../user-help/enroll-your-device-in-intune-macos-cp.md) are provided in the Company Portal app.     

BYOD macOS MDM enrollments prior to June 2020 may not be user approved if the end-user did not manually provide approval of the management profile in **System Preferences** > **Profiles**. For BYOD enrollments after June 2020, the Company Portal app launches **System Preferences** for the user and the user will need to select Install. If the user did not approve the management profile during enrollment, the user can go to **System Preferences** > **Profiles**, choose the management profile, and select **Approve** to approve the profile at a later point in time.

### Find out if a device is User Approved
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices**> choose the device > **Hardware**.
3. Check the **User approved enrollment** field.


## Next steps

After macOS devices are enrolled, you can [create custom settings for macOS devices](../configuration/custom-settings-macos.md).