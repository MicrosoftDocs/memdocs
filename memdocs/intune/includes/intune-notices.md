---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 04/19/2021
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Plan for Change: Intune ending company portal support for unsupported versions of Windows

Intune follows Windows 10 lifecycle for supported Windows 10 versions. We’re now removing support for the associated Windows 10 Company Portals for those Windows versions that are out of the Modern Support policy.

#### How does this affect me?

Given that Microsoft no longer supports these OSs, this may not affect you; you have likely already upgraded your OS or devices. This will only affect you if you are still managing unsupported Windows 10 versions. Windows and Company portal versions this affects include:

- Windows 10, Version 1507, Company portal version 10.1.721.0
- Windows 10, Version 1511, Company portal version 10.1.1731.0
- Windows 10, Version 1607, Company portal version 10.3.5601.0
- Windows 10, Version 1703, Company portal version 10.3.5601.0
- Windows 10, Version 1709, Company portal version 11.0.11201.0

We will not uninstall these Company portal versions mentioned above, but we will remove them from the Microsoft Store and stop testing our service releases with them.

**User Impact:** If you continue to use an unsupported version of Window 10, your users won't get the latest security updates, new features, bug fixes, latency improvements, accessibility improvements, and performance investments. The user will not be able to be co-managed with System Center Configuration Manager and Intune.

#### What do I need to do?

In the Microsoft Endpoint Manager admin center, use the [Discovered apps](../apps/app-discovered-apps.md) feature to find apps with these versions. On a user’s device, the Company Portal version is shown in the **Settings** page of the company portal. Update to a supported Windows/Company Portal version.

### Plan for Change: Intune moving to support Android 6.0 and higher in April 2021

As mentioned in MC234534, Intune will be moving to support Android 6.0 (Marshmallow) and higher in the April (2104) service release.

#### How this change will affect your organization

Given that the Office mobile apps for Android ended support for Android 5.x (Lollipop) on June 30, 2019 (MC181101) this change may not affect you; you have likely already upgraded your OS or devices. However, if you have any device that is still running Android version 5.x, or decide to enroll any device that is running Android version 5.x, please note that these devices will no longer be supported. Either update them to Android version 6.0 (Marshmallow) or higher or replace them with a device on Android version 6.0 or higher.

> [!NOTE]
> Teams Android devices are not impacted by this announcement and will continue to be supported regardless of their Android OS version.

#### What you need to do to prepare

Notify your helpdesk, if applicable, of this upcoming change in support. You also have two admin options to help inform your end users or block enrollment.

1. Here’s how you can warn end users:
    - Utilize a device compliance policy for Android device administrator or Android Enterprise and set the action for non-compliance to send a message to users before marking them noncompliant.
    - Configure an app protection policy Conditional launch setting with a Min OS version requirement to warn users.
2. Here’s how you can block devices on versions below Android 6.0:
    - Set enrollment restrictions to prevent devices on Android 5.x from enrolling
    - Utilize a device compliance policy for Android device administrator or Android Enterprise to make devices on Android 5.x non-compliant.
    - Configure an app protection policy Conditional launch setting with a Min OS version requirement to block users from app access.
