---
title: Protect data and site infrastructure
titleSuffix: Configuration Manager
description: Learn how to protect your organization's resources from exposure or malicious attack with Configuration Manager.
ms.date: 04/05/2021
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

- [Endpoint Protection](../deploy-use/endpoint-protection.md) lets you manage the following Microsoft Defender policies for client computers:

  - Microsoft Defender Antimalware
  - Microsoft Defender Firewall
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender Application Control

  > [!TIP]
  > To manage endpoint protection on co-managed Windows 10 devices using the Microsoft Endpoint Manager cloud service, switch the [**Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) to Intune. For more information, see [Endpoint protection for Microsoft Intune](/intune/endpoint-protection-windows-10).

- Protect data stored on on-premises Windows clients with BitLocker Drive Encryption (BDE). Configuration Manager provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring (MBAM). For more information, see [Plan for BitLocker management](../plan-design/bitlocker-management.md).

Use other components of Microsoft Endpoint Manager to protect your devices. For more information, see [Protect devices with Microsoft Intune](../../../intune/protect/device-protect.md).
