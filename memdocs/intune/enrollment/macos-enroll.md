---
# required metadata

title: Set up enrollment for macOS devices
titleSuffix: Microsoft Intune
description: Learn how to set up enrollment for macOS devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/26/2022
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up enrollment for macOS devices in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

 Microsoft Intune supports enrollment on personal and company-owned devices. This article describes the methods and features you can use to enroll personal, company-owned, and VM devices in Intune. 
 
## Enable enrollment in Microsoft Intune  

Complete these steps first to enable enrollment in your Microsoft Intune tenant. 

1. [Verify that devices are eligible for Apple device enrollment](https://support.apple.com/en-us/HT204142#eligibility)
2. [Configure domains](../fundamentals/custom-domain-name-configure.md)
3. [Set the MDM Authority](../fundamentals/mdm-authority-set.md)
4. [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)  
5. Assign user licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854)
6. [Create groups](../fundamentals/groups-add.md)
7. [Configure the Company Portal app](../apps/company-portal-app.md)

## Enroll devices
After you enable enrollment, use one of the supported methods described in this section to enroll user-owned and company-owned devices.   

### User-owned macOS devices (BYOD)

Intune supports *bring-your-own-device*, or *BYOD*, which lets people enroll their personal devices themselves. To finish setting up enrollment for BYOD scenarios, tell your licensed users to use one of these options to enroll devices:  

- Sign in to [Company Portal website](https://portal.manage.microsoft.com) and follow on-screen instructions to add device. 
- Install Company Portal app for Mac at [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac) and follow-on screen instructions to add device.    

### Company-owned macOS devices
Intune supports the following enrollment methods for company-owned macOS devices. Select a hyperlinked method to open its setup steps. 

- [Apple Automated Device Enrollment](device-enrollment-program-enroll-macos.md): Use this method to automate the enrollment experience on devices purchased through Apple Business Manager or Apple School Manager. Automated device enrollment deploys the enrollment profile over-the-air, so you don't need to have physical access to devices.   
- [Device enrollment manager (DEM)](device-enrollment-manager-enroll.md): Use this method for large-scale deployments and when there are multiple people in your organization who can help with enrollment setup. Someone with device enrollment manager (DEM) permissions can enroll up to 1,000 devices with a single Azure Active Directory account. This method uses the Company Portal app or Microsoft Intune app to enroll devices. You can't use a DEM account to enroll devices via Automated Device Enrollment.   
- [Direct enrollment](device-enrollment-direct-enroll-macos.md): Direct enrollment enrolls devices with no user affinity, so this method is best for devices that aren't associated with a single user. This method requires you to have physical access to the Macs you're enrolling.  

## Bootstrap tokens   

Intune supports the use of bootstrap tokens on enrolled Macs running macOS 10.15 or later. Bootstrap tokens grant volume ownership status to local user and guest accounts so that non-admin users can approve important operations that an admin would otherwise need to do.  Operations such as: 

* User-initiated software updates  

* Kernel extension installation on Apple silicon  

 You can utilize bootstrap tokens on supervised Macs, and Macs enrolled via macOS automated device enrollment.   

### Get bootstrap token  
 
The bootstrap token is automatically generated when:  

* A newly enrolled Mac checks in with Intune and 
* A secure token-enabled user (typically an Intune administrator) signs in to the Mac with their cleartext password

The token is then automatically escrowed to Microsoft Intune. You can use a command line tool to manually view, generate, and escrow a bootstrap token on supported macOS devices, if needed. For more information about commands, see [Use secure token, bootstrap token, and volume ownership in deployments](https://support.apple.com/guide/deployment/use-secure-and-bootstrap-tokens-dep24dbdcf9e/1/web/1.0) on Apple Support.  

### Monitor bootstrap escrow status  
You can monitor the escrow status for any enrolled Mac in the admin center. The *Bootstrap token escrowed* hardware property reports whether or not the bootstrap token has been escrowed in Intune. Intune reports **Yes** when the token has been successfully escrowed and **No** when the token has not been escrowed. 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
2. Go to **Devices** > **macOS**. All macOS devices are shown in a table. 
3. Select a device. 
4. Select **Hardware**. 
5. In your hardware details, scroll down to **Conditional access** > **Bootstrap token escrowed**.  

### Manage kernel extensions and software updates  
A bootstrap token can be used to approve the installation of both kernel extensions and software updates on a Mac with Apple silicon. 

User-initiated software updates can be carried out with a bootstrap token on Macs that are running macOS, version 11.1, and enrolled via automated device enrollment. To authorize user-initiated software updates on a device that isn't enrolled via automated device enrollment, you must restart the Mac in recovery mode and downgrade its security settings. You can also utilize the bootstrap token for software updates on Macs running macOS 11.2 and later, with the only requirement being that the device needs to be supervised. 

Kernel extension management is automatically available on Macs running macOS 11 or later and enrolled via automated device enrollment. To authorize the remote management of kernel extensions on a device that isn't enrolled via automated device enrollment, you must restart the Mac in recovery mode and downgrade its security settings.

For more information about changing security settings, see [Change security settings on the startup disk of a Mac with Apple silicon](https://support.apple.com/guide/mac-help/change-security-settings-startup-disk-a-mac-mchl768f7291/mac) on Apple Support.      

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
* [How to find and change the serial number](https://kb.parallels.com/123455)  

### VMware Fusion
Add the following lines to your .vmx file to set the VM's hardware model and serial number. The values shown in this sample are examples.  

```md
serialNumber = "ABC123456789"  
hw.model = "MacBookAir10,1"  
```  
Enter any string of alphanumeric characters for the serial number. For hardware model, we recommend using the model of the device that's running the VM. To find your Mac's hardware model, select the Apple menu and go to **About This Mac** > **System Report** > **Model Identifier**.   

VMWare Fusion is only supported on Intel Macs. See the VMware customer connect website for more information about [editing the .vmx file for your VMware Fusion VM](https://kb.vmware.com/s/article/1014782).  

### Apple Silicon 
No changes are required for virtual machines running on Apple Silicon hardware. Parallel Desktop is supported on Macs with Apple Silicon, so if you set up a VM this way, you don't need to modify the hardware model ID or serial number.  

## User-approved enrollment

All Mac enrollments in Intune are considered user-approved. User-approved enrollment lets you manage macOS devices that aren't part of Apple School Manager or Apple Business Manager. It provides the same level of control as supervised macOS devices enrolled using Automated Device Enrollment or Apple Configurator. 

Intune automatically turns on supervision for user-approved devices running macOS 11 and later. It also does this for enrolled devices that later update to macOS 11 or later.  


> [!NOTE]
> Intune announced support for user approved enrollment in June 2020. BYOD enrollments that occured before that time may not be user-approved. For more information about Apple devices becoming user approved, see [User approved MDM enrollment](https://support.apple.com/HT208019) on the Apple Support website. 

### User experience     
The device user signs in to the Company Portal app to initiate enrollment. Company Portal then opens the device's system preferences and prompts the user to install the management profile. Company Portal provides in-app instructions to help users find the profile. Users go to **System Preferences** > **Profiles** to  approve the management profile installation. Device users that don't provide approval during enrollment can return to system preferences later to give approval.  

### Find out if device is user approved  
1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices**.  
3. Choose a macOS device.
4. From the side menu, select **Hardware**.  
5. Check the value next to **User approved enrollment**.  

## Back up and restore with Apple Migration Assistant  
Use Apple Migration Assistant to back up and restore a macOS device. You can use the tool to back up a Mac and restore its app data on a new device. It's important to know:  
- The management profile on the original Mac is not backed up. The device is sent a new management profile as the new Mac re-enrolls. This happens on Macs that go through Apple automated device enrollment and Macs that don't go through automated device enrollment.  
- Company Portal app credentials might be restored on the new Mac after it goes through Migration Assistant and enrolls. If this happens, we recommend that you or the device user completes the following steps to clear app data: 
  1. Sign out of the Company Portal app.  
  2. Sign in to the app or Company Portal website.  

## Next steps

* For user-help documentation, which provides step-by-step enrollment instructions for device users, see [Enroll your macOS device in Intune](../user-help/enroll-your-device-in-intune-macos-cp.md). You can also create your own instructions if you prefer to capture your organization's branded or customized enrollment experience.  

* After macOS devices are enrolled, you can [create custom settings for macOS devices](../configuration/custom-settings-macos.md).  
