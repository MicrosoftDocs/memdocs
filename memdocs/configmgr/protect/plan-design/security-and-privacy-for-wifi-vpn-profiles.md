---
title: Wi-Fi and VPN profile security and privacy
titleSuffix: Configuration Manager
description: Learn about the security recommendations for managing Wi-Fi and VPN profiles for devices in Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
---

# Security and privacy for Wi-Fi and VPN profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, this company resource access feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 9315387 --> Use Microsoft Intune to [deploy resource access profiles](../../../intune/configuration/device-profiles.md).

## Security recommendations

Use the following security best practices when you manage Wi-Fi and VPN profiles for devices.

### Choose the most secure options that your Wi-Fi and VPN infrastructure and client operating systems can support

Wi-Fi and VPN profiles provide a convenient method to centrally distribute and manage Wi-Fi and VPN settings that your devices already support. Configuration Manager doesn't add Wi-Fi or VPN functionality. Identify, implement, and follow any security recommendations for your devices and infrastructure.

## Privacy information

You can use Wi-Fi and VPN profiles to configure client devices to connect to Wi-Fi and VPN servers. Then use Configuration Manager to evaluate whether those devices become compliant after the profiles are applied. The management point sends compliance information to the site server, and the information is stored in the site database. The information is encrypted when devices send it to the management point, but it isn't stored in encrypted format in the site database. The database retains the information until the site maintenance task **Delete Aged Configuration Management Data** deletes it. The default deletion interval is 90 days, but you can change it. Compliance information isn't sent to Microsoft.

By default, devices don't evaluate Wi-Fi and VPN profiles. In addition, you must configure the profiles, and then deploy them to users.  

Before you configure Wi-Fi or VPN profiles, consider your privacy requirements.  
