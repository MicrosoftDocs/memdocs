---
title: Protect data and site infrastructure
titleSuffix: Configuration Manager
description: Learn how to protect your organization's resources from exposure or malicious attack with Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby


---

# Protect data and site infrastructure

*Applies to: Configuration Manager (current branch)*

You want your users to securely access your organization's resources. Protect both your infrastructure and your data from exposure or malicious attack. Use Configuration Manager to enable access and help protect your organization's resources.  

- [Endpoint Protection](/configmgr/protect/deploy-use/endpoint-protection) lets you manage the following Microsoft Defender policies for client computers:

  - Microsoft Defender Antimalware
  - Microsoft Defender Firewall
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender Application Control

  > [!TIP]
  > To manage endpoint protection on co-managed Windows 10 devices using the Microsoft Endpoint Manager cloud service, switch the [**Endpoint Protection** workload](/configmgr/comanage/workloads#endpoint-protection) to Intune. For more information, see [Endpoint protection for Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Protect data stored on on-premises Windows clients with BitLocker Drive Encryption (BDE). Configuration Manager provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring (MBAM). For more information, see [Plan for BitLocker management](/configmgr/protect/plan-design/bitlocker-management).

- Instead of traditional passwords, enable alternative sign-in methods on Windows 10 devices using Windows Hello for Business. For more information, see [Windows Hello for Business settings](/configmgr/protect/deploy-use/windows-hello-for-business-settings).

- Minimize your users' efforts to connect to resources by enabling VPN connectivity using VPN profiles. For more information, see [VPN profiles](/configmgr/protect/deploy-use/vpn-profiles).  

- Wi-fi profiles provide a set of tools and resources to help you manage wireless network settings on devices in your organization. By deploying these settings, you minimize the effort that end users require to connect to wireless networks. For more information, see [Wi-fi profiles](/configmgr/protect/deploy-use/create-wifi-profiles).  

- Provision devices with the certificates that users need to connect to resources. For more information, see [Certificate profiles](/configmgr/protect/deploy-use/introduction-to-certificate-profiles).  
