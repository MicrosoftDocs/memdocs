---
title:  Configure Microsoft Intune for increased security
description:  Learn how to improve your security posture with Microsoft Intune.

ms.topic: reference
ms.date: 09/30/2025

ms.author: brenduns
author: brenduns
ms.reviewer: ramical
ms.collection:
- tier 1
- M365-identity-device-management
---

# Configure Microsoft Intune for increased security (Preview)

The security recommendations in this document are designed to help you improve your organization's security posture by using Microsoft Intune. These recommendations are influenced by accepted industry standards like those developed by NIST, the configuration baselines we use internally at Microsoft, and our experiences with customers. The recommendations in this article are guided by the following Microsoft [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars) pillars:

- Protect identities and secrets
- Protect tenants and isolate production systems
- Protect networks
- Protect engineering systems
- Monitor and detect cyberthreats
- Accelerate response and remediation

> [!TIP]
> Some organizations might take these recommendations exactly as written, while others might choose to make modifications based on their own business needs.

We recommend that all of the following controls be implemented where licenses are available. These patterns and practices help to provide a secure foundation for other resources built on top of this solution. More controls will be added to this document over time.

## Protect identities and secrets

### Enforce Windows LAPS to protect local administrator credentials<!-- 24560 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24560](./includes/secure-recommendations/24560.md)]

### Enforce BitLocker encryption on Windows devices<!-- 24550 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24550](./includes/secure-recommendations/24550.md)]

### Require Windows Hello for Business for authentication<!-- 24551-->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24551](./includes/secure-recommendations/24551.md)]

### Restrict local account usage on Windows devices<!--  24564 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24564](./includes/secure-recommendations/24564.md)]

### Encrypt macOS devices with FileVault<!-- 24569 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24569](./includes/secure-recommendations/24569.md)]

### Enforce macOS LAPS to protect local administrator credentials during enrollment<!--  24561 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24561](./includes/secure-recommendations/24561.md)]

<!-- ### Enable Platform SSO for macOS devices <or> Enforce Platform SSO on macOS for phishing-resistant authentication<!-- 24568 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24568](./includes/secure-recommendations/24568.md)]-->

### Enforce app protection policies on Android devices to prevent data leakage<!-- 24549 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24549](./includes/secure-recommendations/24549.md)]

### Enforce app protection policies on iOS/iPadOS devices to prevent data leakage<!-- 24548 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24548](./includes/secure-recommendations/24548.md)]

## Protect tenants and isolate production systems

### Configure scope tags for delegated admin access<!-- 24555 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24555](./includes/secure-recommendations/24555.md)]

### Enable enrollment notifications for device onboarding<!-- 24572 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
 [!INCLUDE [24572](./includes/secure-recommendations/24572.md)]

### Enable automatic enrollment for Windows devices<!-- 24546 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24546](./includes/secure-recommendations/24546.md)]

<!-- ### ## Assign least privilege role-based access control roles in Intune<!-- 24521 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24521](./includes/secure-recommendations/24521.md)]-->

<!-- ### Configure platform-specific enrollment restrictions<!-- 24558 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24558](./includes/secure-recommendations/24558.md)]-->

### Enforce compliance policies on Windows devices<!-- 24541 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24541](./includes/secure-recommendations/24541.md)]

### Enforce compliance policies on macOS devices<!-- 24542 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24542](./includes/secure-recommendations/24542.md)]

### Enforce compliance policies on fully managed and corporate owned Android devices<!--  24545 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24545](./includes/secure-recommendations/24545.md)]

### Enforce compliance policies on personally owned Android devices<!--  24547 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24547](./includes/secure-recommendations/24547.md)]

### Enforce compliance policies on iOS/iPadOS devices<!--  24543 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24543](./includes/secure-recommendations/24543.md)]

<!-- ## Enable automatic Defender enrollment for Android devices<!-- 24871 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24871](./includes/secure-recommendations/24871.md)]-->

### Block access from noncompliant devices using Conditional Access<!-- 24824 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24824](./includes/secure-recommendations/24824.md)]

### Block access from unmanaged apps using Conditional Access<!-- 24827 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
 [!INCLUDE [24827](./includes/secure-recommendations/24827.md)]

### Configure device cleanup rules to remove inactive devices<!--  24802 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24802](./includes/secure-recommendations/24802.md)]

### Require user acceptance of terms and conditions<!--  24794 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24794](./includes/secure-recommendations/24794.md)]

### Customize Company Portal branding and support settings<!-- 24823 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
 [!INCLUDE [24823](./includes/secure-recommendations/24823.md)]

### Enable Endpoint Analytics for Windows devices<!-- 24576 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24576](./includes/secure-recommendations/24576.md)]

### Enforce Windows Update policies for patch compliance<!-- 24553 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24553](./includes/secure-recommendations/24553.md)]

### Apply Intune security baselines to Windows devices<!-- 24573 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24573](./includes/secure-recommendations/24573.md)]

### Enforce macOS update policies for patch compliance<!-- 24690 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24690](./includes/secure-recommendations/24690.md)]

### Enforce iOS/iPadOS update policies for patch compliance<!-- 24554 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24554](./includes/secure-recommendations/24554.md)]

## Protect networks

### Enforce Windows Firewall policies<!-- 24540 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24540](./includes/secure-recommendations/24540.md)]

### Apply Attack Surface Reduction rules to Windows devices<!-- 24574 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24574](./includes/secure-recommendations/24574.md)]

### Enforce Defender Antivirus policies on Windows devices<!-- 24575 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24575](./includes/secure-recommendations/24575.md)]

### Enforce macOS Firewall policies<!-- 24552 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24552](./includes/secure-recommendations/24552.md)]

### Enforce Defender Antivirus policies on macOS devices<!-- 24784 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24784](./includes/secure-recommendations/24784.md)]

### Configure secure Wi-Fi profiles for iOS devices<!-- 24839 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24839](./includes/secure-recommendations/24839.md)]

### Configure secure Wi-Fi profiles for Android devices<!-- 24840 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24840](./includes/secure-recommendations/24840.md)]

<!-- ### Configure secure Wi-Fi profiles for macOS devices<!-- 24870 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24870](./includes/secure-recommendations/24870.md)] -->

## Related content

- [Deployment guide for Microsoft Intune](/intune/intune-service/fundamentals/get-started-with-intune)
- [Protect data and devices with Microsoft Intune](/intune/intune-service/protect/device-protect)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)


