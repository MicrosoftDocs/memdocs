---
title: "Enroll user-owned devices for hybrid deployments"
description: "Learn about different methods to enroll user-owned devices for hybrid deployments with Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: 13
author: nathbarn
ms.author: nathbarn
manager: angrobe

---
# Enroll user-owned devices for hybrid deployments with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

User-owned devices can be brought into management by enrolling them, a process often called "bring your own devices" or simply "BYOD." Users do this by installing the Company Portal app and signing in on the device (iOS, macOS, and Android) or by adding a Work or School account to the device and joining a domain (Windows). This process enrolls the device with Intune, giving the user access to resources managed by Intune and letting Intune manage certain device settings, such as requiring a PIN.

To bring devices into management, as an admin you must first [set up mobile device management](setup-hybrid-mdm.md) and [enable enrollment](enable-platform-enrollment.md). Once enrollment is enabled, users can enroll their own devices. See [How to educate your end users about Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate) for considerations and steps to share with your users.

Companies or schools that purchase devices can take advantage of programs that let you [manage company-owned devices](enroll-company-owned-devices.md).
