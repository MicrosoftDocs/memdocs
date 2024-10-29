---
title: Protect data and site infrastructure
titleSuffix: Configuration Manager
description: Learn how to protect your organization's resources from exposure or malicious attack with Configuration Manager.
ms.date: 10/05/2021
ms.service: configuration-manager
ms.subservice: protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Protect data and site infrastructure

*Applies to: Configuration Manager (current branch)*

You want your users to securely access your organization's resources. Protect both your infrastructure and your data from exposure or malicious attack. Use Configuration Manager to enable access and help protect your organization's resources.  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) lets you manage the following Microsoft Defender policies for client computers:

  - Microsoft Defender Antimalware
  - Microsoft Defender Firewall
  - Microsoft Defender for Endpoint
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender Application Control

  > [!TIP]
  > To manage endpoint protection on co-managed Windows 10 or later devices using the Microsoft Intune cloud service, switch the [**Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) to Intune. For more information, see [Endpoint protection for Microsoft Intune](/mem/intune/protect/endpoint-protection-windows-10).

- Protect data stored on on-premises Windows clients with BitLocker Drive Encryption (BDE). Configuration Manager provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring (MBAM). For more information, see [Plan for BitLocker management](../plan-design/bitlocker-management.md).

Use other components of Microsoft Intune to protect your devices. For more information, see [Protect devices with Microsoft Intune](../../../intune/protect/device-protect.md).
