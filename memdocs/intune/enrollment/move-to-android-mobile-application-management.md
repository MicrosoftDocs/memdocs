---
# required metadata

title: Move from Android device administrator to mobile application management
description: Use Microsoft Intune to set up mobile application management, an alternative option to Android device administrator that focuses on app protection and doesn't require device enrollment.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/27/2024
ms.topic: how-to 
ms.service: microsoft-intune 
ms.subservice: enrollment  
ms.localizationpriority: Low
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: esalter
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- intune-scenario

#Customer intent: As an administrator, I want an alternative to Android device administrator that doesn't require enrollment, because my organization doesn't require mobile device management capabilities like deploying Wi-Fi or email configuration profiles.  
---

# Move from device administrator management to mobile application management  

**Applies to Android**  

This article describes how to move from Android device administrator management to mobile application management in Microsoft Intune, and contains recommendations and best practices for a successful transition as [Microsoft Intune ends support for Android device administrator](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-intune-ending-support-for-android-device-administrator/ba-p/3915443).   

There are two ways to utilize mobile application management in Intune: with device enrollment or without device enrollment. In this article, you'll learn how to set up *mobile application management without device enrollment* to manage apps and data on personal devices. We recommend this option for organizations that don't need mobile device management (MDM) capabilities like Wi-Fi deployment or email configuration profiles. If your organization has dependencies that require device management on personal devices, we recommend moving to [Android Enterprise personally owned work profile management](../enrollment/android-move-device-admin-work-profile.md) instead.   

## Prerequisites      

You need the following Intune permissions to set up and enforce mobile application management:   
 * Managed apps/Assign
 * Managed apps/Create  
 * Managed apps/Delete 
 * Managed apps/Read  
 * Managed apps/Update  
 * Managed apps/Wipe    

Additionally, the Intune Company Portal app is required on devices, because it enables device users to receive app protection policies.  

>[!TIP]
> * The built-in [Application Manager](../fundamentals/role-based-access-control-reference.md#application-manager) role has sufficient permissions for mobile application management.  
> * You can add [scope tags](../fundamentals/scope-tags.md) to policies to control object visibility among Intune admin users.  

## Step 1: Configure policies for mobile application management  
Create mobile application management policies in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Within these policies you can, for example, allow or block app features such as *copy and paste*. For more app protection settings and capabilities in Intune, see:  
* [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md): Describes the settings you can configure in an app protection policy.    
* [Intune protected apps](../apps/apps-supported-intune-apps.md#microsoft-apps): Lists apps that support app protection policies.  

The following table lists configurations commonly used with Android device administrator management and similar mobile application management settings to consider using going forward.  

>[!TIP]
> Although similar, the mobile app management policies and settings listed in this table don't neccessarily function the same way as the Android device administrator ones you're used to. Review the linked resources to compare and evaluate policies and settings.  

| Configuration | Android device administrator policy setting |Mobile application management policy setting | More information |
| --- | --- | --- | --- |
|Conditional Access | Use [device-based Conditional Access policies](../protect/app-based-conditional-access-intune-create.md).  | Use [app-based Conditional Access policies](../protect/app-based-conditional-access-intune-create.md). | Before you unenroll devices, consider updating your device-based Conditional Access policies to include an `or` condition for app-based Conditional Access policies.  Otherwise, device users could be in an interim state without MDM or mobile application management enforced. |
| Prevent copy and paste |  **Restrict copy and paste (Knox only)**  <br> <br> Setting available in [Configuration policy > General](../configuration/device-restrictions-android.md#general).   | **Restrict cut, copy, and paste between other apps** <br> <br>  Setting available in [App protection policy > Data protection](../apps/app-protection-policy-settings-android.md#data-protection). | | 
| Enforce password | Password settings vary depending on policy type used.  <br> <br> Settings available in [Configuration policy > Password](../configuration/device-restrictions-android.md#password) and [Compliance policy > Password](../protect/compliance-policy-create-android.md#password).  | **PIN for app access** <br> <br>  Setting available in [App protection policy > Access requirements](../apps/app-protection-policy-settings-android.md#access-requirements). |  |
| Enforce minimum and maximum OS version | OS version settings vary depending on policy type used.  <br> <br> Settings available in [Compliance policy > Operating system version](../protect/compliance-policy-create-android.md#operating-system-version) and [Enrollment > Device platform restriction](../enrollment/create-device-platform-restrictions.md#create-a-device-platform-restriction). | **Min OS version** and **Max OS version** <br> <br> Settings available in [App protection policy > Conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch). | 
| Block rooted devices| **Rooted devices** <br> <br> Setting available in [Compliance policy > Device health](../protect/compliance-policy-create-android.md#device-health).| **Jailbroken/rooted devices** <br> <br> Setting available in [App protection policy > Conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch). |
| Allow specific manufacturers | **Device manufacturers** <br> <br> Setting available in [Enrollment > Device platform restriction](../enrollment/create-device-platform-restrictions.md#create-a-device-platform-restriction). | **Device manufacturers** <br> <br> Setting available in [App protection policy > Conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch). | |
| VPN |Create a [VPN profile](../configuration/vpn-settings-configure.md) in a configuration policy.  |Set up [Microsoft Tunnel for Mobile App Management](../protect/microsoft-tunnel-mam-android.md). |  |
| Assign and deploy apps |  Make apps required for automatic installation or make them available in the Company Portal app. <br> <br> Settings available in [Apps > Android store app](../apps/store-apps-android.md#add-an-app). | Apps you make available to employees and students automatically appear in the Company Portal for Android app or Managed Google Play app.  |  Protect line-of-business (LOB) apps with app protection policies by using the Intune app wrapping tool. If you develop LOB apps in-house, your developers can [leverage the Intune App SDK](../developer/app-sdk.md).  | 
| Wipe corporate data | **Retire** devices to wipe corporate data only, or **Wipe** devices to restore them to factory settings. <br> <br> Settings available in [remote actions](../remote-actions/devices-wipe.md).| **Wipe corporate data from apps** <br> <br> Setting available in [App selective wipe](../apps/apps-selective-wipe.md). |  |  

## Step 2: Restrict Android device administrator 

Create a platform enrollment restriction for Android device administrator to prevent further device administrator enrollments from happening. Devices already enrolled as device administrator remain enrolled and unaffected.  

For more information about how to create a platform enrollment restriction, see [Create device platform restrictions](../enrollment/create-device-platform-restrictions.md).  

## Step 3: Remove devices from device administrator management     
Retire enrolled devices in the Microsoft Intune admin center or instruct device users to unenroll them in the Intune Company Portal app.  

Removing an enrolled device from Intune can have the following effect:  
* The device loses access to work or school apps and websites.  
* The device no longer appears in Intune Company Portal. <!-- This applies to enrolled devices and devices you set up just to access work emails. -->  
* Device users can no longer install work or school apps from Company Portal.  
* Setting requirements and restrictions (such as device PIN, disabling the camera, and prohibiting screenshots) are no longer enforced.  

### Retire device in admin center  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **By platform** > **Android**.   
3. Select **Android devices**.  
3. Select the name of the device that you want to retire. You can add an **OS** filter to make it easier to see all Android device administrator devices in your tenant.  
4. Select **Retire**. Then select **Yes** to confirm that you want to remove the device from device management.   

Removal happens the next time the device checks in and receives the remote *retire* action. The device remains visible in the admin center until the device checks in. If you want to remove stale devices immediately, use the *delete* action instead. For more information about how to remove devices from Microsoft Intune, see [Remove devices](../remote-actions/devices-wipe.md). 

### Let device users unenroll device  
Employees and students can unenroll their devices in the Intune Company Portal app. To support them and ensure that they're successful, you can: 

* Send them a custom notification about device requirements and next steps. For more information, see [Send notifications](../remote-actions/custom-notifications.md).  
* Use your organization's internal communication channels, such as email, to inform them of device requirements and next steps. 

For removal steps that Android device users can do themselves, see [Unenroll Android device](../user-help/unenroll-your-device-from-intune-android.md#remove-device-in-company-portal-app).  

## Best practices  
This section contains best practices for setting up mobile application management.  

### Prevent Company Portal enrollment prompts
When Microsoft Intune detects that the user's device is set up for app protection policies without enrollment, it doesn't prompt the user to enroll via Intune Company Portal. To ensure that other users don't enroll their devices, we recommend configuring the Company Portal app so that there's no enrollment prompt. For more information, see [Device enrollment setting options](../apps/company-portal-app.md#device-enrollment-setting-options). 

To block enrollment of personal devices, create a device enrollment restriction. For more information, see [Best practices for Android platform restrictions](../enrollment/create-device-platform-restrictions.md#best-practice---android-platform-restrictions).  

### Unenrolling devices with Microsoft Entra Conditional Access policies  
If you have Microsoft Entra Conditional Access policies that require devices to be compliant for corporate access, the devices you remove from Android device administrator management will lose their access. To ensure continued access, review your existing Conditional Access policies. For more information, see [Require device to be marked as compliant](/entra/identity/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant). 

You can also:   
* Make app protection a requirement for access.     
* Limit user access to approved client apps with Intune app protection policies.   

For more information, see [Require approved app or app protection policy](/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection).  

## Troubleshooting  
This section describes how to fix issues encountered when switching from Android device administrator to mobile application management. 

### Device user required to install Company Portal app  
**Symptom**: You unenroll a device from device administrator, and when you try to access a protected app you see the message:  

> Company Portal required: To use your work or school account with this app, you must install the Intune Company Portal app. Click **Go to store** to continue.  

**Cause**: The Intune Company Portal app isn't on the device you're using. App protection is built in to the Intune Company Portal, app so the app is required on devices utilizing app protection without enrollment.  

**Solution**: Install the Intune Company Portal app on the device.     

### User account removed from protected apps after user unenrolls device 
**Symptom**: You're prompted to sign in to a work or school app again, even though you already signed in.  

**Cause**: After a device unenrolls from Android device administrator management, Intune performs a mobile application management wipe on protected apps. As a result, the user account is removed from these apps and you're signed out.  

**Solution**: Sign in again to the protected app with your work or school account.  

## More resources    

* [Intune app protection policies overview](../apps/app-protection-policy.md)  
* [App management capabilities by platform](../apps/app-management.md#app-management-capabilities-by-platform)  
* [Troubleshooting app protection policy user issues](/troubleshoot/mem/intune/app-protection-policies/troubleshoot-mam)  
* [Deployment guide: Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-mamwe.md#mam)  