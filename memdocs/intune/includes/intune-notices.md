---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 11/19/2019
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Microsoft Intune support for Windows 10 Mobile ending<!--3544938-->
Microsoft mainstream support for Windows 10 Mobile ended in December, 2019. As mentioned in this support statement, Windows 10 Mobile users will no longer be eligible to receive new security updates, non-security hotfixes, free assisted support options or online technical content updates from Microsoft. Based on the all-up Mobile OS support, Microsoft Intune will now end support for both the Company Portal for the Windows 10 Mobile app and the Windows 10 Mobile Operating System on May 11, 2020.

#### How does this affect me?
If you have Windows 10 Mobile devices deployed in your organization, between now and May 11, 2020 you can enroll new devices, add or remove policies and apps, or update any management settings. After May 11, we will stop new enrollments, and eventually remove Windows 10 Mobile management from the Intune UI. Devices will no longer check into the Intune service and we will delete device and policy data.  

#### What do I need to do to prepare for this change?
You can check your Intune reporting to see what devices or users may be affected. Go to **Devices** > **All devices** and filter by OS. You can add in additional columns to help identify who in your organization has devices running Windows 10 Mobile. Request that your end users upgrade their devices or discontinue using the devices for corporate access.



### Plan for Change: Change in experience when enrolling Android Enterprise dedicated devices in Intune<!--6114580-->
We shared in the November release we were adding support for SCEP certificate deployment to Android Enterprise dedicated devices, to enable certificate-based access to Wi-Fi profiles. This change involved some minor enrollment flow changes for Android Enterprise dedicated devices. With the upcoming March service update or 2003, there are some further changes that we’d like you to be aware of.

#### How does this affect me?
If you manage Android Enterprise dedicated devices in your environment, you will start to see some changes roll out in March.
- For existing Android dedicated devices enrolled prior to the November 22, 2019 or the 1911 service update: These devices have the Microsoft Intune app installed on them. After backend changes roll out in the Intune service in March, SCEP certificates deployed to devices and associated with Wi-Fi profiles will start to apply.
- For devices that were enrolled after November 22, 2019 and before this change rolls out in March: These devices have the Microsoft Intune app installed on them. SCEP certificates deployed to devices and associated with Wi-Fi profiles will continue to apply.
- For new Android Enterprise dedicated device enrollments after the change rolls out in March: End users will see a different set of steps on devices during enrollment. Enrollment will still start the way it does today (with QR, NFC, Zero-touch, or device identifier) but there will be no mandatory app install step. Instead, the Microsoft Intune app will automatically install on devices. Additionally, end users will not need to tap “Enable Intune Agent” during the flow. SCEP Certificates associated with WiFi profiles can be deployed to these devices.

#### What can I do to prepare for this change?
You can update your end user guidance and let your helpdesk know of this change. We’ll update our What’s New page and notify you through the Message center when this change starts to roll out.

#### Additional information
[Support for SCEP certificates in Android Enterprise dedicated devices](https://aka.ms/Dedicated_devices_enrollment)

### Updated support statement for 'Adobe Acrobat Reader for Intune' mobile app<!--5746776-->
We shared in MC188653 at the end of August, that the Adobe Acrobat Reader for Intune mobile app was reaching end-of-life on December 1, 2019 and that Adobe was planning on supporting Intune’s app protection policies within their main Acrobat Reader app. Since then, we received customer feedback that we needed to provide more time to continue allowing IT admins to target, and end users to begin using Adobe Acrobat Reader for Intune. Given the high usage of Adobe Acrobat Reader for Intune on end user devices and its importance in enterprise scenarios, we want to make sure any experience meets your organization's app protection needs. 

While we still recommend targeting the general Acrobat Reader mobile app in your policies since the Acrobat Reader mobile app supports App Protection Policies and has integrated the Intune SDK, the Adobe Acrobat Reader for Intune app will continue to be supported until March 31, 2020. 

#### How does this affect me?
You are receiving this message because our reporting indicates one or more policies in your organization are targeting the Adobe Acrobat Reader for Intune application and/or you may have received our previous EOL communication. 

#### What do I need to do to prepare for this change?
Let your end users and helpdesk know of this change. You can use the [Company Portal's support information functionality](../intune/apps/company-portal-app.md#support-information) to establish a channel for Intune-related questions.

#### Additional Information
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html


### Take Action: Use Microsoft Edge for your Protected Intune Browser Experience<!--5728447-->
As we have been sharing over the past year, Microsoft Edge mobile supports the same set of management features as the Managed Browser, while providing a much-improved end user experience. To make way for the robust experiences provided in Microsoft Edge, we will be retiring the Intune Managed Browser. Starting on January, 27, 2020, Intune will no longer support the Intune Managed Browser.  

#### How does this affect me? 
Starting on February 1, 2020, the Intune Managed Browser will no longer be available in the Google Play Store or the iOS App Store. At this point, you will still be able to target new app protection policies to the Intune Managed Browser, though new users won't be able to download the Intune Managed Browser app. In addition, on iOS, new web clips that are pushed down to MDM-enrolled device will open in Microsoft Edge instead of the Intune Managed Browser.  

On March, 31 2020, the Intune Managed Browser will be removed from the Azure console. This means you will no longer be able to create new policies for the Intune Managed Browser. If you have existing Intune Managed Browser policies in place, they won't be affected. The Intune Managed Browser will show up in the console as an LOB app with no icon, and existing policies will show as targeted to the app still. At this point, we will also remove the option to redirect web content to the Intune Managed Browser within the Data Protection section of App protection policies.  

#### What do I need to do to prepare for this change? 
To ensure a smooth transition from the Intune Managed Browser to Microsoft Edge, we recommend you take the following steps proactively: 

1. Target Microsoft Edge for iOS and Android with app protection policy (also referred to as MAM)  and app config settings. You can reuse your Intune Managed Browser policies for Microsoft Edge by targeting those existing policies to Microsoft Edge as well.  
2. Ensure all MAM-protected apps in your environment have the app protection policy setting "Restrict web content transfer with other apps" set to "Policy managed browsers". 
3. Target all the MAM-protected with the managed app configuration setting "com.microsoft.intune.useEdge" set to true. Starting next month with the release of 1911, you will be able to accomplish steps 2 and 3 simply by configuring the setting "Restrict web content transfer with other apps" to have "Microsoft Edge" selected in the Data Protection section of your app protection policies. 

Support for web clips on iOS and Android is coming. When this support is released, you will need to retarget pre-existing web clips to ensure they open in Microsoft Edge instead of the Managed Browser. 

#### Additional information
Visit our docs on [using Microsoft Edge with app protection policies](../intune/apps/manage-microsoft-edge.md) for more info, or view our [support blog post](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269).


### End of support for legacy PC management

Legacy PC management is going out of support on October 15, 2020. Upgrade devices to Windows 10 and reenroll them as Mobile Device Management (MDM) devices to keep them managed by Intune.

[Learn more](https://go.microsoft.com/fwlink/?linkid=2107122)

### Decreasing support for Android device administrator 
Android device administrator (sometimes referred to "legacy" Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is now available with [Android Enterprise](../intune/enrollment/connect-intune-android-enterprise.md) (released with Android 5.0). In an effort to move to modern, richer, and more secure device management, Google is decreasing device administrator support in new Android releases.

#### How does this affect me?
Because of these changes by Google, Intune users will be impacted in the following ways:  
- Intune will only be able to provide full support for device administrator-managed Android devices running Android 10 and later through Q2 CY2020. Device administrator-managed devices that are running Android 10 or later after this time won't be able to be entirely managed. In particular, impacted devices won’t receive new password requirements.
    - Samsung Knox devices won't be impacted in this timeframe because extended support is provided through Intune’s integration with the Knox platform. This gives you more time to plan the transition off device admin management.    
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

### Plan for change: Intune App SDK and app protection policies for Android moving to support Android 5.0 and higher in an upcoming release <!--4911065 -->
Intune will be moving to support Android 5.x (Lollipop) and higher in an upcoming release. Update any wrapped apps with the latest Intune App SDK and update your devices.

#### How does this affect me?
If you're not using or plan to use either the SDK or APP for Android, this change won't affect you. If you are using the Intune App SDK, be sure to update to the latest version and also update your devices to Android 5.x and higher. If you don't update, apps won't receive updates, and the quality of their experience will diminish over time.

Below find a list of common devices enrolled in Intune that run Android version 4.x. If you have one of these devices, take the appropriate steps to make sure that this device will support Android version 5.0 or higher or that it will be replaced with a device that supports Android version 5.0 or higher. This list isn't exhaustive of all devices that may need to be evaluated:

- Samsung SM-T561  
- Samsung SM-T365
- Samsung GT-I9195
- Samsung SM-G800F
- Samsung SM-G357FZ
- Motorola XT1080
- Samsung GT-I9305
- Samsung SM-T231

#### What do I need to do to prepare for this change?
Wrap your apps with the latest Intune App SDK. You may also set the "Require minimum OS version (Warning only)" conditional launch setting to notify end users on personal devices to upgrade.


