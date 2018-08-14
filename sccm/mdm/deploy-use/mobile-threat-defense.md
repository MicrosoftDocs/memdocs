---
title: Restrict access based on risk
titleSuffix: Configuration Manager
description: Restrict access to company resources based on device, network and application risk.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage access to company resource based on device, network, and application risk

*Applies to: System Center Configuration Manager (Current Branch)*

Mobile Threat Defense connectors allow you to leverage your chosen Mobile Threat Defense vendor as a source of information for your compliance policies and conditional access rules. This allows you to add a layer of protection to your organizational resources such as Exchange and Sharepoint, specifically from compromised mobile devices.

> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## What problem does this solve?

Organizations need to protect sensitive data from emerging threats including physical, app-based, and network-based threats, as well as OS vulnerabilities.

Historically, organizations have been proactive when protecting PCs from attack, while mobile devices go un-monitored and unprotected. Mobile platforms have built-in protection such as app isolation and vetted consumer app stores, but these platforms remain vulnerable to sophisticated attacks. Today, more employees use devices for work and need access to sensitive information. Devices need to be protected from increasingly sophisticated attacks.



## How the Intune Mobile Threat Defense connectors work?

The connector protects organizational resources by creating a channel of communication between Intune and your chosen Mobile Threat Defense vendor. Intune Mobile Threat Defense partners offer intuitive, easy to deploy applications for mobile devices which actively scan and analyze threat information to share with Intune. Use this information for either reporting or enforcement purposes. 

For example, a connected Mobile Threat Defense app reports to the Mobile Threat Defense vendor that a device is currently connected to a network which is vulnerable to man-in-the-middle attacks. This information is shared with and categorized to an appropriate risk level: low, medium, or high. Compare this risk with your configured risk level allowances in Intune to determine if access to certain resources of your choice should be revoked while the device is compromised.



## Sample scenarios

When a device is considered infected by the Mobile Threat Defense solution:

![Mobile Threat Defense infected device](../media/mtp/MTD-image-1.png)

Access is granted when the device is remediated:

![Mobile Threat Defense Access granted](../media/mtp/MTD-image-2.png)



## Next steps

Learn how to protect access to company resource based on device, network, and application risk with:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)