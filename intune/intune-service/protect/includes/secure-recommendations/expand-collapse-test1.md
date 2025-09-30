---
title: Windows Firewall policy
ms.author: brenduns
author: brenduns
ms.topic: include
ms.date: 09/02/2025
# sfipillar:
# category: Devices
# risklevel: High
# userimpact: Medium
# implementationcost: Low
---


<details><summary><b>Placeholder entry</b></summary></details>


<details><summary><b>Compliance policy for Windows devices</b></summary><br><b>Applies to: </b><img src ="../../media/applies-to-yes.png" alt="Green circle with a white check mark symbol"> Zero Trust Assessment<br><br>When an Intune policy for compliance for Windows devices hasn't been created and assigned, threat actors can exploit unmanaged or noncompliant Windows devices to gain unauthorized access to corporate resources, bypass security controls, and persist within the environment. Without enforced compliance, Windows devices might lack critical security configurations such as BitLocker encryption, password requirements, firewall settings, or OS version controls. Lack of these configurations increases the risk of data leakage, privilege escalation, and lateral movement. This gap in device compliance management can break the chain of defense, making it difficult to detect and remediate threats or unauthorized access before significant damage occurs.

<b>Remediation action</b>

- [Create and assign Intune compliance policies](/intune/intune-service/protect/create-compliance-policy)
- [Review the Windows compliance settings you can manage with Intune](/intune/intune-service/protect/compliance-policy-create-windows)</details>