---
# required metadata

title: Use direct enrollment for macOS devices
titleSuffix: Microsoft Intune
description: Deploy and enroll macOS devices in Microsoft Intune using direct enrollment with Apple Configurator.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/03/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
---

# Use direct enrollment for macOS devices  

Manually enroll new or existing corporate-owned Macs via *direct enrollment* with Apple Configurator. Direct enrollment is ideal for bulk enrollments and when you don't have access to Apple School Manager, Apple Business Manager, or when you require a wired network connection. You must have physical access to the Macs to configure and deploy the enrollment profile. 

Direct enrollment lets you enroll the device prior to distribution, and doesn't wipe the device upon enrollment. Devices enrolled this way aren't associated with a user so we recommend this option for shared or kiosk-style devices. These types of devices are purpose driven and commonly used in businesses by frontline workers to scan items, print tickets, get digital signatures, or manage inventory.  

We recommend direct enrollment if you: 

- Are in a region/country that doesn't support Apple Business Manager or Apple School Manager. 
- Don't want to use Apple Business Manager or Apple School Manager because you want to limit admin control over devices, or because you don't want to set up all of the requirements. 
- Need a wired internet connection to enroll devices, or have an unreliable internet connection.   

You can use this method to enroll one or more Macs. If you have many devices, it will take some time to enroll them because you must transfer and open the enrollment profile on each Mac you're enrolling. 

Devices are deployed without user affinity. If you need devices to have user affinity, enroll Macs in Intune via [Apple automated device enrollment](device-enrollment-program-enroll-macos.md).  

See the following visual guide for a summary of all enrollment options and features available for macOS:    

[![A visual representation of Intune enrollment options by platform](../fundamentals/media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)  

## Apps 
Apps requiring user affinity, such as the Intune Company Portal app, aren't supported on Macs enrolled via direct enrollment. The Company Portal app isn't used, needed, or supported for enrollments without user affinity. Be sure device users don't install the Company Portal app from the Apple App Store on enrolled devices.  

## Certificates  
This enrollment type supports the Automated Certificate Management Environment (ACME) protocol. When new devices enroll, the management profile from Intune receives an ACME certificate. The ACME protocol provides better protection than the SCEP protocol against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Devices that are already enrolled in Intune do not get an ACME certificate unless they re-enroll into Microsoft Intune. ACME is supported on devices running macOS 13.1 or later.   

## Prerequisites
   
- Physical access to [supported devices](../fundamentals/supported-devices-browsers.md#apple).  
- Access to Microsoft Intune admin center and Apple Configurator. 
- Set [MDM authority](../fundamentals/mdm-authority-set.md).   
- [An Apple MDM push certificate](apple-mdm-push-certificate-get.md).  
- Administrator rights on the Macs you're enrolling.  

If the Mac you're setting up is enrolled in another MDM provider, you must unenroll it before you can enroll it in Intune. Also, make sure that you don't have a device platform restriction targeted at iOS/iPadOS devices, because it will cause the enrollment profile to fail on enrolling Macs.  

## Step 1: Create enrollment profile 

A device enrollment profile defines the settings applied during direct enrollment. These settings are applied only once. Follow these steps to create an Apple Configurator enrollment profile for the Macs you're enrolling.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
1. Go to **Devices** > **Enrollment**.  
1. Select the **Apple** tab.  
1. Under **Bulk Enrollment Methods**, select **Apple Configurator**.  
1. Go to **Profiles** > **Create**.      
5. The **Create Enrollment Profile** page opens. For **Basics**, type a **Name** and **Description** for the profile. These details can help you quickly find your profile in the admin center. Device users don't see these details.  

  > [!TIP] 
  > You can use the name field to create a dynamic membership rule for Microsoft Entra groups. The *enrollmentProfileName* parameter lets you quickly assign devices with this enrollment profile to the appropriate groups. For more information, see [Dynamic group rule syntax](/azure/active-directory/enterprise-users/groups-dynamic-membership#rules-for-devices).  

5. For **User Affinity**, choose **Enroll without user affinity**. This configuration confirms that you're setting up devices without user association. Direct enrollment *with user affinity*, although available, isn't supported on Macs.   

6. Select **Create** to save the profile.  

## Step 2: Export enrollment profile  
In this step, you export the enrollment profile.    

1. After you create the profile in the admin center, go to **Profiles**.  
1. Choose the profile you want to export. Then select **Export profile**.  
1. A new pane opens. Under **Direct enrollment**, choose **Download profile**.
1. Save the `.mobileconfig` file.  An enrollment profile file is only valid for two weeks. After that time, you must recreate it.  

     > [!NOTE]
     > You can download as many enrollment profiles as you need. Downloading a new profile does not render the previous one invalid, however, it also doesn't extend the expiration date for the previously downloaded file. 

## Step 3: Install enrollment profile    
In this step, you install the enrollment profile on the enrolling Mac. 

1. Transfer the `.mobileconfig` file from your device to the Mac you want to enroll.   
1. Double-click the file to open it.  
1. When you're prompted to install the management profile, select **Install**. 
1. Select **Install** again to confirm you want to install the management profile.  
1. Sign in with an administrator account on the Mac, and then select **OK**.  

The Mac is now enrolled in Microsoft Intune and ready-to-manage. Other profiles assigned to the device begin installing immediately.  

## Next steps  

Start managing enrolled devices in the Microsoft Intune admin center.  

- [Tutorial - Walkthrough the Microsoft Intune admin center](../fundamentals/tutorial-walkthrough-endpoint-manager.md)   
- [Run remote actions on devices with Microsoft Intune](../remote-actions/device-management.md)     
- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)  

