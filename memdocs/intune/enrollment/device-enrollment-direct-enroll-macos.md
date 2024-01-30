---
# required metadata

title: Use Direct Enrollment for macOS devices
titleSuffix: Microsoft Intune
description: Enroll macOS devices using Direct Enrollment.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier1
- M365-identity-device-management
---

# Use Direct Enrollment for macOS devices

Intune supports the enrollment of macOS devices using Direct Enrollment (DE) for corporate devices. Direct Enrollment does not wipe the device. It enrolls the device through macOS settings. This method only supports devices with **no user affinity**.

> [!IMPORTANT]
> Make sure that you don't have a [device platform restriction](../enrollment/create-device-platform-restrictions.md) targeted to your iOS/iPadOS devices, because it will cause the enrollment profile to fail when you try exporting it to macOS devices.   

## Prerequisites

- Physical access to macOS devices
- [Set MDM authority](../fundamentals/mdm-authority-set.md)
- [An Apple MDM push certificate](apple-mdm-push-certificate-get.md)
 - Administrator rights on the macOS devices you're enrolling

## Create an Apple Configurator profile for devices

A device enrollment profile defines the settings applied during enrollment. These settings are applied only once. Follow these steps to create an enrollment profile to enroll macOS devices with Direct Enrollment.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
1. Go to **Devices** > **Enrollment**.  
1. Select the **Apple** tab.  
1. Under **Bulk Enrollment Methods**, select **Apple Configurator**.  
1. Go to **Profiles** > **Create**.  
5. Under **Create Enrollment Profile** in the **Basics** tab, type a **Name** and **Description** for the profile for administrative purposes. Device users don't see these details.

  >[!TIP] 
  >You can use the name field to create a dynamic membership rule for Microsoft Entra groups. The *enrollmentProfileName* parameter lets you quickly assign devices with this enrollment profile to the appropriate groups. For more information, see [Dynamic group rule syntax](/azure/active-directory/enterprise-users/groups-dynamic-membership#rules-for-devices).  

5. For **User Affinity**, choose **Enroll without User Affinity** - Choose this option for devices unaffiliated with a single user. Use this for devices that perform tasks without accessing local user data. Apps requiring user affiliation (including the Company Portal app used for installing line-of-business apps) won't work. Required for Direct Enrollment.

     > [!NOTE]
     > **Enroll with user affinity** is not supported on macOS when using Direct Enrollment. For devices that need user affinity, use Automated Device Enrollment.

6. Select **Create** to save the profile.  

## Direct Enrollment
Because Direct Enrollment only supports enrollment without user affinity, the company portal can't be used to install available applications.

### Export the profile and install on macOS devices  

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **Enrollment**.  
1. Select the **Apple** tab.  
1. Under **Bulk Enrollment Methods**, select **Apple Configurator**.  
1. Go to **Profiles** and choose the profile you want to export. Then select **Export Profile**.  
1. Under **Direct enrollment**, choose **Download profile**, and then save the file.  

     > [!NOTE]
     > A downloaded enrollment profile is valid for two weeks after download. You can download as many enrollment profiles using this link as you need. Downloading a new profile does not render the previous one invalid, however, it also doesn't extend the previously downloaded file expiry time. As mentioned before, make sure that you don't have a device platform restriction targeted to your iOS/iPadOS devices, because it will cause the enrollment profile to fail when you try exporting it to macOS devices.  
         
1. Transfer the file to a macOS computer to install it directly.
1. Double-click the saved **mobileconfig** file to open the file in Profiles.  
1. When prompted to install the management profile, select **Install**.
1. Confirm on the next prompt you want to install the management profile by selecting **Install**.
1. Sign in with an admin account on the macOS device, and then select **OK**.

The macOS device is now enrolled in Intune and ready-to-manage. Targeted profiles begin downloading.  

## Next steps

After enrolling macOS devices, you can start [managing them](../remote-actions/device-management.md).  
