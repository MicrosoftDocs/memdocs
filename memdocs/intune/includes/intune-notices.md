---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Microsoft Intune support for Windows 10 Mobile ending<!--3544938-->
Microsoft mainstream support for Windows 10 Mobile ended in December 2019. As mentioned in this support statement, Windows 10 Mobile users will no longer be eligible to receive new security updates, non-security hotfixes, free assisted support options or online technical content updates from Microsoft. Based on the all-up Mobile OS support, Microsoft Intune will now end support for both the Company Portal for the Windows 10 Mobile app and the Windows 10 Mobile Operating System on August 10, 2020.

#### How does this affect me?
If you have Windows 10 Mobile devices deployed in your organization, between now and August 10, 2020 you can enroll new devices, add, or remove policies and apps, or update any management settings. After August 10, we will stop new enrollments, and eventually remove Windows 10 Mobile management from the Intune UI. Devices will no longer check into the Intune service and we will delete device and policy data.  

#### What do I need to do to prepare for this change?
You can check your Intune reporting to see what devices or users may be affected. Go to **Devices** > **All devices** and filter by OS. You can add in additional columns to help identify who in your organization has devices running Windows 10 Mobile. Request that your end users upgrade their devices or discontinue using the devices for corporate access.


### End of support for legacy PC management

Legacy PC management is going out of support on October 15, 2020. Upgrade devices to Windows 10 and reenroll them as Mobile Device Management (MDM) devices to keep them managed by Intune.

[Learn more](https://go.microsoft.com/fwlink/?linkid=2107122)


### Decreasing support for Android device administrator<!--5857738-->
Android device administrator (sometimes referred to "legacy" Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is now available with [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (released with Android 5.0). In an effort to move to modern, richer, and more secure device management, Google is decreasing device administrator support in new Android releases.

#### How does this affect me?
Because of these changes by Google, Intune users will be impacted in the following ways:  
- Intune will only be able to provide full support for device administrator-managed Android devices running Android 10 and later through Q2 CY2020. Device administrator-managed devices that are running Android 10 or later after this time won't be able to be entirely managed. In particular, impacted devices won't receive new password requirements.
    - Samsung Knox devices won't be impacted in this timeframe because extended support is provided through Intune's integration with the Knox platform. This gives you more time to plan the transition off device admin management.    
- Device administrator-managed Android devices that remain on Android versions below Android 10 won't be impacted and can continue to be entirely managed with device administrator.    
- For all devices running Android 10 and later, Google has restricted the ability for device administrator management agents like Company Portal to access device identifier information. This restriction impacts the following Intune features after a device is updated to Android 10 or later:  
    - Network access control for VPN will no longer work.   
    - Identifying devices as corporate-owned with an IMEI or serial number won't automatically mark devices as corporate-owned.  
    - The IMEI and serial number will no longer be visible to IT admins in Intune. 
        > [!NOTE]
        > This only impacts device administrator-managed devices on Android 10 and later and does not affect devices being managed as Android Enterprise. 

#### What do I need to do to prepare for this change?
To avoid the reduction in functionality coming in Q3 CY2020, we recommend the following:
- Don't onboard new devices into device administrator management.
- If a device is expected to receive an update to Android 10, migrate it off of device administrator management to Android Enterprise management and/or app protection policies.

#### Additional information
- [Google's guidance for migration from device administrator to Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google's documentation on the plan to deprecate the device administrator API](https://developers.google.com/android/work/device-admin-deprecation)