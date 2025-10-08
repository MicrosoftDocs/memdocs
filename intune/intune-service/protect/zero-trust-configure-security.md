---
title:  Configure Microsoft Intune for increased security
description:  Learn how to improve your security posture with Microsoft Intune.
ms.topic: reference
ms.date: 10/06/2025
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
 
### Local administrator credentials on Windows are protected by Windows LAPS<!-- 24560 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24560](./includes/secure-recommendations/24560.md)]

### Data on Windows is protected by BitLocker encryption<!-- 24550 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24550](./includes/secure-recommendations/24550.md)]

### Authentication on Windows uses Windows Hello for Business<!-- 24551-->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24551](./includes/secure-recommendations/24551.md)]

### Local account usage on Windows is restricted to reduce unauthorized access<!--  24564 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24564](./includes/secure-recommendations/24564.md)]

### FileVault encryption protects data on macOS devices<!-- 24569 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24569](./includes/secure-recommendations/24569.md)]

### Local administrator credentials on macOS are protected during enrollment by macOS LAPS<!--  24561 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24561](./includes/secure-recommendations/24561.md)]

<!-- ### Platform SSO is enforced on macOS to enable phishing-resistant authentication<!-- 24568 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24568](./includes/secure-recommendations/24568.md)]-->

### Data on Android is protected by app protection policies<!-- 24549 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24549](./includes/secure-recommendations/24549.md)]

### Data on iOS/iPadOS is protected by app protection policies<!-- 24548 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24548](./includes/secure-recommendations/24548.md)]

## Protect tenants and isolate production systems

### Scope tag configuration is enforced to support delegated administration and least-privilege access<!-- 24555 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24555](./includes/secure-recommendations/24555.md)]

### Device enrollment notifications are enforced to ensure user awareness and secure onboarding<!-- 24572 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
 [!INCLUDE [24572](./includes/secure-recommendations/24572.md)]

### Windows automatic device enrollment is enforced to eliminate risks from unmanaged endpoints<!-- 24546 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24546](./includes/secure-recommendations/24546.md)]

<!-- ### ## Least privilege RBAC roles are assigned in Intune to secure role-based access<!-- 24521 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24521](./includes/secure-recommendations/24521.md)]-->

<!-- ### Platform-specific enrollment restrictions are configured to control device onboarding<!-- 24558 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24558](./includes/secure-recommendations/24558.md)]-->

### Compliance policies protect Windows devices<!-- 24541 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24541](./includes/secure-recommendations/24541.md)]

### Compliance policies protect macOS devices<!-- 24542 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24542](./includes/secure-recommendations/24542.md)]

### Compliance policies protect fully managed and corporate-owned Android devices<!--  24545 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24545](./includes/secure-recommendations/24545.md)]

### Compliance policies protect personally owned Android devices<!--  24547 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24547](./includes/secure-recommendations/24547.md)]

### Compliance policies protect iOS/iPadOS devices<!--  24543 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24543](./includes/secure-recommendations/24543.md)]

<!-- ## Automatic enrollment to Defender is enabled on Android to support threat protection<!-- 24871 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24871](./includes/secure-recommendations/24871.md)]-->

### Conditional Access policies block access from noncompliant devices<!-- 24824 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24824](./includes/secure-recommendations/24824.md)]

### Conditional Access policies block access from unmanaged apps<!-- 24827 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
 [!INCLUDE [24827](./includes/secure-recommendations/24827.md)]

### Device cleanup rules maintain tenant hygiene by hiding inactive devices<!--  24802 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24802](./includes/secure-recommendations/24802.md)]

### Terms and Conditions policies protect access to sensitive data<!--  24794 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24794](./includes/secure-recommendations/24794.md)]

### Company Portal branding and support settings enhance user experience and trust<!-- 24823 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
 [!INCLUDE [24823](./includes/secure-recommendations/24823.md)]

### Endpoint Analytics is enabled to help identify risks on Windows devices<!-- 24576 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24576](./includes/secure-recommendations/24576.md)]

### Windows Update policies are enforced to reduce risk from unpatched vulnerabilities<!-- 24553 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24553](./includes/secure-recommendations/24553.md)]

### Security baselines are applied to Windows devices to strengthen security posture<!-- 24573 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24573](./includes/secure-recommendations/24573.md)]

### Update policies for macOS are enforced to reduce risk from unpatched vulnerabilities<!-- 24690 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24690](./includes/secure-recommendations/24690.md)]

### Update policies for iOS/iPadOS are enforced to reduce risk from unpatched vulnerabilities<!-- 24554 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24554](./includes/secure-recommendations/24554.md)]

## Protect networks

### Windows Firewall policies protect against unauthorized network access<!-- 24540 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24540](./includes/secure-recommendations/24540.md)]

### Attack Surface Reduction rules are applied to Windows devices to prevent exploitation of vulnerable system components<!-- 24574 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24574](./includes/secure-recommendations/24574.md)]

### Defender Antivirus policies protect Windows devices from malware<!-- 24575 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24575](./includes/secure-recommendations/24575.md)]

### macOS Firewall policies protect against unauthorized network access<!-- 24552 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24552](./includes/secure-recommendations/24552.md)]

### Defender Antivirus policies protect macOS devices from malware<!-- 24784 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24784](./includes/secure-recommendations/24784.md)]

### Secure Wi-Fi profiles protect iOS devices from unauthorized network access<!-- 24839 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24839](./includes/secure-recommendations/24839.md)]

### Secure Wi-Fi profiles protect Android devices from unauthorized network access<!-- 24840 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24840](./includes/secure-recommendations/24840.md)]

<!-- ### Secure Wi-Fi profiles are configured to protect macOS connectivity and devices<!-- 24870 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24870](./includes/secure-recommendations/24870.md)] -->

## Related content

- [Deployment guide for Microsoft Intune](/intune/intune-service/fundamentals/get-started-with-intune)
- [Protect data and devices with Microsoft Intune](/intune/intune-service/protect/device-protect)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)


