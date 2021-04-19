---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 04/6/2021
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Plan for Change: Intune ending support for stand-alone client apps on Microsoft Tunnel<!-- 9370486   -->

The Defender for Endpoint app on Android now supports Microsoft Tunnel functionality and will be the official client app for Android Enterprise customers. We will be removing the Microsoft Tunnel client from the Google Play store at the end of June.

#### How this change will affect your organization

If you use the Microsoft Tunnel app for Android, you'll need to move to the Defender for Endpoint app before the June Intune (2106) service release to ensure users can still access the Tunnel Gateway configuration.

#### What you need to do to prepare

For your devices that run Android Enterprise and currently use the Microsoft Tunnel app, plan to [replace the stand-alone tunnel app with the Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md). New devices should use Defender for Endpoint app.

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
