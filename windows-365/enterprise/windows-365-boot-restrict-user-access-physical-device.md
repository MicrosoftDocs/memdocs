---
# required metadata
title: Restrict user access to Windows 365 Boot physical device.
titleSuffix:
description: Learn what configuration service providers you can use to restrict user access to Windows 365 Boot physical devices.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/28/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elluthra
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-overview
ms.collection:
- M365-identity-device-management
- tier2
---

# Restrict user access to Windows 365 Boot physical device

Windows 365 Boot physical devices are intended to let users interact with their Cloud PCs without the ability to interact with the physical device. To meet this goal, you must set some configuration service provider (CSP) policies.

Windows 365 Boot doesn't automatically set these policies to fully restrict end users from accessing certain resources on the physical device. Admins should review the following CSPs and decide which ones to implement on the physical device to meet your organization's security requirements.

A new CSP policy in [public preview](..\public-preview.md) is available. You can use this policy to further restrict devices automatically. For more information, see [TBS](whats-new.md).

## Prevent access to physical device's Task Manager

In the public preview version of Windows 365 Boot feature, the local device’s Task Manager can still be accessed when users press Ctrl+Alt+Delete. The Task Manager can be disabled by using the [DisableTaskMgr CSP policy](/windows/client-management/mdm/policy-csp-admx-ctrlaltdel#disabletaskmgr).

This policy prevents the use of the Task Manager in the system for all users including admins. It also prevents the launch of Task Manager using shortcut keys on the physical device. While this policy increases the security of the device, this lack of access to the physical device makes it harder to troubleshoot issues on the device.

## Prevent users from changing the physical device's password

Changing user passwords isn't supported for Windows 365 Boot physical devices. If this option is used in your environment, it can be disabled to avoid confusing users by using the [DisableChangePassword CSP policy](/windows/client-management/mdm/policy-csp-admx-ctrlaltdel#disablechangepassword).

## Set default credential provider

The public preview version of Windows 365 Boot is designed for shared PC mode. This mode requires the username and password authentication method. Depending on your environment, other authentication providers might be configured and could confuse your users. To avoid this confusion, consider setting the default credential provider to username and password. To set this default, use the [DefaultCredentialProvider CSP policy](/windows/client-management/mdm/policy-csp-admx-credentialproviders#defaultcredentialprovider).  

## Remove Notifications and Action Center from the task bar

If your devices have touchscreens, it's possible for users to interact with physical device's Notification Center and calendar view. These components also let users launch the Settings app for the Windows 365 Boot physical device. To remove the user's ability to access these components, use the [DisableNotificationCenter CSP policy](/windows/client-management/mdm/policy-csp-admx-taskbar#disablenotificationcenter).

## Prevent physical device notifications

Notifications from the Windows 365 Boot physical device can display over the Cloud PC session. To prevent such notifications, use the [NoToastNotification CSP policy](/windows/client-management/mdm/policy-csp-admx-wpn#notoastnotification).

## Prevent automatic launch of apps during user sign-in

Some applications on the Windows 365 Boot physical device might be configured to automatically launch during user sign-in. To prevent top this behavior, use the [DisableExplorerRunLegacy_1 CSP policy](/windows/client-management/mdm/policy-csp-admx-logon?WT.mc_id=Portal-fx#disableexplorerrunlegacy_1).  

## Improve sign-in on touch screen devices

Touchscreen devices require the touch screen keyboard to show during user sign-in. On Windows 365 boot touch screen devices, you can improve the sign-in experience by using the [EnableTouchKeyboardAutoInvokeInDesktopMode CSP policy](/windows/client-management/mdm/policy-csp-textinput#enabletouchkeyboardautoinvokeindesktopmode).

<!-- ########################## -->
## Next steps

[Troubleshoot Windows 365 Boot](troubleshoot-windows-365-boot.md).
