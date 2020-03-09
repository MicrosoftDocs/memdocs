---
title: Troubleshoot Android enterprise devices in Microsoft Intune
description: Suggestions for troubleshooting some of the most common problems when you enroll Android devices in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot Android Enterprise device problems in Microsoft Intune

This article helps Intune administrators understand and troubleshoot problems when Android Enterprise devices in Intune.

## Apps on Android Enterprise devices

### Managed Google Play apps that aren't deployed through Intune are displayed in the work profile
System apps can be enabled in the work profile by the device OEM at the time that the work profile is created. This isn't controlled by the MDM provider.

To troubleshoot, follow these steps:

  1. Collect Company Portal logs.
  2. Note apps that appear in the work profile unexpectedly.
  3. Unenroll device from Intune and uninstall Company Portal.
  4. Install the [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) app, which allows creation of a work profile without an EMM for testing.
  5. Follow the instructions in [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) to create a work profile on the device.
  6. Review apps that appear in the work profile. 
  7. If the same applications show in the Test DPC app, the apps are expected by the OEM for that device.

### Unapproved Managed Google Play for Work store apps aren't being removed from the Client Apps page in Intune
This is expected behavior.

### Managed Google Play apps aren't being reported under the Discovered Apps blade in the Intune portal
This is expected behavior. Only system apps installed in the Work Profile are inventoried in the Discovered Apps blade. To see installed Managed Google Play applications, use the **Managed Apps** blade.

### Are Web Applications supported for work profile enrolled devices?
Yes. For more information, see [Managed Google Play web links](../apps/apps-add-android-for-work.md#managed-google-play-web-links)

## Device management

### File path Internal storage/Android/Data.com.microsoft.windowsintune.companyportal/files missing on work profile enrolled devices

  **Answer**: This is expected behavior. This path is only created for the Device Admin (Legacy Android Enrollment) scenario.

  To collect Company Portal logs, follow these steps:

  1. In the Company Portal app with the badge, tap **Menu** > **Help** > **Email Support**, and then tap **Send Email & Upload logs**. 
  2. When you're prompted **Send help request with**, select one of the Email apps.
  3. An email is generated to your IT admin with an incident ID that can be provided to Microsoft product support.

### Managed Google Play Last Sync time  hasn't been updated in days
This is expected behavior. The sync is only triggered when you manually do so.

### Encryption is required when a device is enrolled. Can it be turned off?
No, Google requires that the device be encrypted to create a work profile. 

### Samsung devices are blocking the use of third-party keyboards like SwiftKey
Samsung began enforcing this restriction on Android 8.0+ devices. Microsoft is currently working with Samsung on this issue and will post new information when it's available.

## Remote actions

### Wipe (Factory Reset) option isn't available for work profile enrolled device
This is expected behavior. In the work profile scenario, the MDM provider doesn't have full control over the device. The only option available is Retire (Remove Company Data) which removes the whole work profile and all its contents.

### Is device passcode reset supported?
For work profile enrolled devices, you can only reset the work profile passcode on Android 8.0 or later devices when:
- the work profile passcode is managed
- the end user has allowed you to reset it.

For Dedicated devices (COSU) and Fully Managed, device passcode reset is supported.


## Next steps

- [Troubleshoot device enrollment in Intune](troubleshoot-device-enrollment-in-intune.md)
- [Ask a question on the Intune forum](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Check the Microsoft Intune Support Team Blog](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Check the Microsoft Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)