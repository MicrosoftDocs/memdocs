---
title: "Mobile Threat Defense"
titleSuffix: "Configuration Manager"
description: "Restrict access to company resources based on device, network and application risk using Configuration Manager and Intune Mobile Threat Defense partners"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---
# Intune Mobile Threat Defense connectors in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The [hybrid MDM deployment (SCCM with Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) and the integration between Intune and the Mobile Threat Defense partners give you the ability to control the access to company resources and data based on device risk assessment.

Intune Mobile Threat Defense connectors allow you to leverage your chosen Mobile Threat Defense vendor as a source of information for your compliance policies and conditional access rules. This allows IT Administrators to add a layer of protection to their corporate resources such as Exchange and Sharepoint, specifically from compromised mobile devices.

## What problem does this solve?

Companies need to protect sensitive data from emerging threats including physical, app-based, and network-based threats, as well as operating system vulnerabilities.
Historically, companies have been proactive when protecting PCs from attack, while mobile devices go un-monitored and unprotected. Mobile platforms have built-in protection such as app isolation and vetted consumer app stores, but these platforms remain vulnerable to sophisticated attacks. Today, more employees use devices for work and need access to sensitive information. Devices need to be protected from increasingly sophisticated attacks.

## How the Intune Mobile Threat Defense connectors work?

The connector protects company resources by creating a channel of communication between Intune and your chosen Mobile Threat Defense vendor. Intune Mobile Threat Defense partners offer intuitive, easy to deploy applications for mobile devices which actively scan and analyze threat information to share with Intune, for either reporting or enforcement purposes. For example, if a connected Mobile Threat Defense app reports to the Mobile Threat Defense vendor that a phone on your network is currently connected to a network which is vulnerable to Man in the Middle attacks, this information is shared with and categorized to an appropriate risk level (low/medium/high) – which can then be compared with your configured risk level allowances in Intune to determine if access to certain resources of your choice should be revoked while the device is compromised.

## Sample scenarios

When a device is considered infected by the Mobile Threat Defense solution:

![](http://i.imgur.com/Li1WUOU.png)

Access is granted when the device is remediated:

![](http://i.imgur.com/VCIwpdz.png)

## Mobile Threat Defense partners

Learn how to protect access to company resource based on device, network, and application risk with:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
