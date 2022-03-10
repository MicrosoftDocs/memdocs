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
- [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)  
- Assign user licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Create groups](../fundamentals/groups-add.md)
- [Configure the Company Portal app](../apps/company-portal-app.md)


## User-owned macOS devices (BYOD)

People can BYOD, or *bring-your-own-device*, and enroll personal devices in Intune themselves. To set up enrollment for BYOD scenarios, complete the prerequisites in this article. Then tell your device users to use one of these options to enroll devices:  

- Sign in to [Company Portal website](https://portal.manage.microsoft.com) and follow on-screen instructions to add device. 
- Install Company Portal app for Mac at [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac) and follow-on screen instructions to add device.    


## Company-owned macOS devices
Intune supports the following enrollment methods for company-owned macOS devices:  

- [Apple Automated Device Enrollment](device-enrollment-program-enroll-macos.md): Use this method to automate the enrollment experience on devices purchased through Apple Business Manager or Apple School Manager. Automated device enrollment deploys the enrollment profile over-the-air,so you don't need to have physical access to devices.  
- [Device enrollment manager (DEM)](device-enrollment-manager-enroll.md): Use this method for large-scale deployments and when there are multiple people in your organization who can help with enrollment setup. Someone with device enrollment manager (DEM) permissions can enroll up to 1,000 devices with a single Azure Active Directory account. This method uses the Company Portal app or Microsoft Intune app to enroll devices. You can't use a DEM account to enroll devices via Automated Device Enrollment.   
- [Direct enrollment](device-enrollment-direct-enroll-macos.md): Direct enrollment enrolls devices with no user affinity, so this method is best for devices that aren't associated with a single user. Because there is no user associated, you can't use the Company Portal or Microsoft Intune apps to enroll devices. Instead, you download the profile and transfer it to the macOS device. This method requires you to have physical access to the Macs you're enrolling. 

## Bootstrap tokens    

> [!NOTE]
> This feature is in public preview. It isn't available in GCC High and government cloud tenants.  

Intune supports the use of bootstrap tokens on enrolled Macs running macOS 10.15 or later. Bootstrap tokens grant volume ownership status to local user accounts, so that non-admin users can approve important operations that an admin would otherwise need to do.  Operations such as: 

* User-initiated software updates  
* Silent FileVault encryption  
* Kernel extension installation on Apple silicon  

 You can utilize bootstrap tokens on supervised Macs, and Macs enrolled via automated device enrollment.   

### Get bootstrap token  
 
The bootstrap token is automatically generated when:  

* A newly-enrolled Mac checks in with Intune and 
* A secure token-enabled user (typically an Intune administrator) signs in to the Mac with their clear text password

The token is then automatically escrowed to Microsoft Intune. You can use a command line tool to manually view, generate, and escrow a bootstrap token, if needed. For more information, see [Use secure token, bootstrap token, and volume ownership in deployments](https://support.apple.com/guide/deployment/use-secure-and-bootstrap-tokens-dep24dbdcf9e/1/web/1.0) on Apple Support.  

### Manage kernel extensions  
A bootstrap token can be used to approve the installation of both kernel extensions and software updates on a Mac with Apple silicon. Kernel extension management is automatically available on Macs running macOS 11 or later and enrolled via automated device enrollment. 

To authorize the remote management of kernel extensions on a device that isn't enrolled via automated device enrollment, you must restart the Mac in recovery mode and downgrade its security settings. For more information, see [Change security settings on the startup disk of a Mac with Apple silicon](https://support.apple.com/guide/mac-help/change-security-settings-startup-disk-a-mac-mchl768f7291/mac) on Apple Support.      

## Block macOS enrollment  
By default, Intune lets macOS devices enroll. To block macOS devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).  

## Enroll virtual macOS machines for testing

> [!NOTE]
> macOS virtual machines are only supported for testing. You should not use macOS virtual machines as production devices for your end users. 

You can enroll macOS virtual machines for testing using either Parallels Desktop or VMware Fusion. 

For Parallels Desktop, you need to set the hardware type and the serial number for the virtual machines so that Intune can recognize them. Follow Parallels' instructions for setting hardware type and [serial number](http://kb.parallels.com/123455) to set up the necessary settings for testing. We recommend that you match the hardware type of the device running the virtual machines to the hardware type of the virtual machines that you're creating. You can find this hardware type in **Apple menu** > **About this Mac** > **System Report** > **Model Identifier**. 

For VMware Fusion, you need to [edit the .vmx file](https://kb.vmware.com/s/article/1014782) to set the virtual machine's hardware model and serial number. We recommend that you match the hardware type of the device running the virtual machines to the hardware type of the virtual machines that you're creating. You can find this hardware type in **Apple menu** > **About this Mac** > **System Report** > **Model Identifier**. 

## User approved enrollment

User Approved MDM enrollment is a type of macOS enrollment that you can use to manage certain security-sensitive settings. For more information, see [Apple's support documentation](https://support.apple.com/HT208019).  
 
As of June 2020, all new macOS MDM enrollments in Intune, including those not done through Automated Device Enrollment (ADE), are considered user approved. The end-user must manually install the management profile in **System Preferences** > **Profiles**, and thus provide approval of the management profile. System Preferences is launched automatically from the Company Portal app for BYOD macOS users. [Instructions to install the management profile](../user-help/enroll-your-device-in-intune-macos-cp.md) are provided in the Company Portal app.     

BYOD macOS MDM enrollments prior to June 2020 may not be user approved if the end-user did not manually provide approval of the management profile in **System Preferences** > **Profiles**. For BYOD enrollments after June 2020, the Company Portal app launches **System Preferences** for the user and the user will need to select Install. If the user did not approve the management profile during enrollment, the user can go to **System Preferences** > **Profiles**, choose the management profile, and select **Approve** to approve the profile at a later point in time.

### Find out if a device is User Approved
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices**> choose the device > **Hardware**.
3. Check the **User approved enrollment** field.


## Next steps

* For user-help documentation, which provides step-by-step enrollment instructions for device users, see [Enroll your macOS device in Intune](../user-help/enroll-your-device-in-intune-macos-cp.md). You can also create your own instructions if you prefer to capture your organization's branded or customized enrollment experience.  

* After macOS devices are enrolled, you can [create custom settings for macOS devices](../configuration/custom-settings-macos.md).

* 