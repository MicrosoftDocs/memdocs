---
title: "Troubleshoot Lookout integration"
description: "This topic describes troubleshooting issues that commonly occur with Lookout Integration."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision:
author: mtillman
ms.author: mtillman
manager: angrobe

---
# Troubleshoot Lookout Integration with Intune

*Applies to: System Center Configuration Manager (Current Branch)*

## Troubleshoot login errors
### 403 errors
You may see a 403 error when you log in to the [Lookout MTP console](https://aad.lookout.com):  **you are not authorized to access the service**  This can happen when the username you specified is not a member of the Azure Active Directory (Azure AD) group that is configured to access Lookout MTP.

Lookout MTP is configured to  allow only users from a configured Azure AD group to have access. If you are unsure which group is configured with access to Lookout MTP, contact Lookout Support.

You can contact Lookout Support through on the following methods:

* Email: enterprisesupport@lookout.com
* Login to the  [MTP  Console](http://aad.lookout.com), and navigate to the **Support** module.
* Go to:  https://enterprise.support.lookout.com/hc/requests and make a support request.

### Unable to sign in
You may see the following error when the Azure AD global admin user has not accepted the initial Lookout setup.

![screenshot of the Lookout login screen showing sign in error](media/lookout-consent-not-accepted-error.png)

To resolve this issue, the global admin user must login to  https://aad.lookout.com/les?action=consent
and accept the prompt to initiate the setup. More detailed information can be found in  [Set up your subscription with Lookout MTP](set-up-your-subscription-with-lookout.md) topic

## Troubleshoot device status issues

### Device not showing up in the Lookout MTP console device list

This could happen in either of the following scenarios:
* When the user who owns this device is not in the **Enrollment Group** specified in the **Lookout MTP Console**.  From the **System** module, go to the  **Intune Connector** tab and look at the **Enrollment Management**  settings.  You should see one or more Azure AD groups configured for enrollment.  Verify that the user who owns the missing device is part of one of the specified Azure AD groups.  Once a new user is added to the enrollment group it will take up to the configured polling interval (5 minutes is the default) to see the device show up in the **Devices** module of the Lookout MTP Console.

* If the device is unsupported by Lookout MTP.  Devices that are unsupported will appear in the **Managed Devices** section of the connector settings on the Lookout MTP Console.

### Device continues to be reported as **pending**

A device that is showing  **Pending**  means the end user has not opened the Lookout for work app and tapped the  **Activate** button. For more details on the device activation with Lookout for Work app, read the following topic:

[You are prompted to install Lookout for Work on your Android device ](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### In the Lookout MTP console, a device is showing as active, but does not have a device ID.
This means that the user who owns this device is not in the enrollment group, specified in the Lookout MTP Console.   A device can get into this state is if the user who owns the device has been removed from the enrollment group or the enrollment group that the user belongs to has been removed.

From the **System** module on the Lookout MTP console, go to the  **Intune Connector** tab, and review the **Enrollment** settings.  You should see one or more Azure AD groups configured for enrollment.  Verify that the user who owns the device is part of one of the Azure AD groups specified.

While a device is in this state, Lookout will continue to notify the user of any threats detected, but will not send any threat information to Intune.

### Device shows disconnected state

Disconnected means that Lookout MTP has not heard from the device for over a preconfigured time interval (default is 30 days with a minimum of 7 days). This means that either the Company Portal app or the Lookout for Work app is not installed on the device or has been uninstalled. Reinstalling the apps should resolve this issue. When the user opens Lookout for Work and activates the app, the device resyncs with Lookout MTP and Intune.

### Forcing a resync on the device
From the **Devices** module of the Lookout MTP console, the administrator can select the device and choose to delete it.   The next time the device owner opens the Lookout for Work app and taps **Activate**, the device state will do a full resync.

### The owner of the device is no longer using this device
You must wipe the device and ask the new user to enroll as described in [this topic](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


You can also go to the **Devices** module of the Lookout MTP Console and choose **Delete**.

As long as the new user is in one of the  enrollment groups specified in the Lookout MTP console, the device will appear once Azure AD associates the device to the new user.

## Compliance remediation workflows
[You are prompted to install Lookout for Work on your Android device]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[You need to resolve a threat that Lookout for Work found on your Android device ](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
