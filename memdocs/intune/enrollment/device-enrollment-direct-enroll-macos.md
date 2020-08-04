---
# required metadata

title: Use Direct Enrollment for macOS devices
titleSuffix: 
description: Learn how to enroll macOS devices using Direct Enrollment.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
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
ms.collection: M365-identity-device-management
---

# Use Direct Enrollment for macOS devices

Intune supports the enrollment of macOS devices using direct enrollment for corporate devices. Direct enrollment does not wipe the device. It enrolls the device through macOS settings. This method only supports devices with **no user affinity**.

## Prerequisites

- Physical access to macOS devices
- [Set MDM authority](../fundamentals/mdm-authority-set.md)
- [An Apple MDM push certificate](apple-mdm-push-certificate-get.md)
 - Administrator rights on the macOS devices you are enrolling

## Create an Apple Configurator profile for devices

A device enrollment profile defines the settings applied during enrollment. These settings are applied only once. Follow these steps to create an enrollment profile to enroll macOS devices with direct enrollment.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Apple enrollment** > **Apple Configurator**.

2. Choose **Profiles** > **Create**.

3. Under **Create Enrollment Profile**, type a **Name** and **Description** for the profile for administrative purposes. Users do not see these details. You can use this Name field to create a dynamic group in Azure Active Directory. Use the profile name to define the enrollmentProfileName parameter to assign devices with this enrollment profile. Learn more about Azure Active Directory dynamic groups.

4. For **User Affinity**, choose **Enroll without User Affinity** - Choose this option for devices unaffiliated with a single user. Use this for devices that perform tasks without accessing local user data. Apps requiring user affiliation (including the Company Portal app used for installing line-of-business apps) won't work. Required for direct enrollment.

     > [!NOTE]
     > **Enroll with user affinity** is not supported on macOS when using direct enrollment. For devices that need user affinity, use Automated Device Enrollment.

6. Choose **Create** to save the profile.

## Direct enrollment
Apps requiring user affiliation, including the Company Portal app used for installing line-of-business apps, cannot be installed.

### Export the profile and install on macOS devices

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Apple enrollment** > **Apple Configurator** > **Profiles** >  choose the profile to export > **Export Profile**.
2. Under **Direct enrollment**, choose **Download profile**, and save the file. 

     > [!NOTE]
     > An enrollment profile file is only valid for two weeks at which time you must re-create it.
         
3. Transfer the file to a macOS computer to install it directly.
4. Double-click on the saved **.mobileconfig** to open the file in Profiles.
5. When prompted to install the management profile, select **Install**.
6. Confirm on the next prompt you want to install the management profile by selecting **Install**.
7. Enter the credentials for an admin account on the macOS device and click **OK**.
8. The macOS device is now enrolled in Intune and managed, targeted profiles will begin downloading.

## Next steps

After enrolling macOS devices, you can start [managing them](../remote-actions/device-management.md).