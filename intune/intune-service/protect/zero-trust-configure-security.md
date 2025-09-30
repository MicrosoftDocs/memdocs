---
title:  Configure Microsoft Intune for increased security
description:  Learn how to improve your security posture with Microsoft Intune.

ms.topic: reference
ms.date:  08/29/2025

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

### Windows - Cloud LAPS policy is enforced<!-- 24560 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24560](./includes/secure-recommendations/24560.md)]

### Windows - BitLocker Policy is configured and assigned<!-- 24550 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24550](./includes/secure-recommendations/24550.md)]

### Windows - Hello for Business policy is configured and assigned<!-- 24551-->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24551](./includes/secure-recommendations/24551.md)]

### Windows - Local Account Protection policy is configured and assigned<!--  24564 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24564](./includes/secure-recommendations/24564.md)]

### macOS - Configure macOS FileVault<!-- 24569 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24569](./includes/secure-recommendations/24569.md)]

### macOS - Cloud LAPS is enforced<!--  24561 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24561](./includes/secure-recommendations/24561.md)]

<!-- ### macOS - Platform SSO is configured and assigned 24568 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24568](./includes/secure-recommendations/24568.md)]-->

### App protection policy assigned on Android devices<!-- 24549 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24549](./includes/secure-recommendations/24549.md)]

### App protection policy assigned on iOS/iPad devices<!-- 24548 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24548](./includes/secure-recommendations/24548.md)]

## Protect tenants and isolate production systems

### Tenant - Scope Tags are configured for delegated administration<!-- 24555 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24555](./includes/secure-recommendations/24555.md)]

### Tenant - Enrollment notification<!-- 24572 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
 [!INCLUDE [24572](./includes/secure-recommendations/24572.md)]

### Windows - Automatic enrollment is configured<!-- 24546 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24546](./includes/secure-recommendations/24546.md)]

<!-- ### ## Tenant - Least privilege principal is used for Intune Role and Responsibilities 24521 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24521](./includes/secure-recommendations/24521.md)]-->

<!-- ### Tenant - Enrollment restrictions per platform are configured 24558 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24558](./includes/secure-recommendations/24558.md)]-->

### Compliance policies for Windows devices<!-- 24541 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24541](./includes/secure-recommendations/24541.md)]

### Compliance policies for macOS<!-- 24542 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24542](./includes/secure-recommendations/24542.md)]

### Compliance policies for Android Enterprise (Fully managed and corporate owned work profile)<!--  24545 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24545](./includes/secure-recommendations/24545.md)]

### Compliance policies for Android Enterprise (Personally owned work profile)<!--  24547 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24547](./includes/secure-recommendations/24547.md)]

### Compliance policies for iOS/iPadOS<!--  24543 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24543](./includes/secure-recommendations/24543.md)]

<!-- ## Android - Automatic Enrollment to Defender is enabled for Android Devices <!-- 24871 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24871](./includes/secure-recommendations/24871.md)]-->

### Non-compliant devices are restricted from accessing corporate data<!-- 24824 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24824](./includes/secure-recommendations/24824.md)]

### Unmanaged and unprotected apps are restricted from accessing corporate data<!-- 24827 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
 [!INCLUDE [24827](./includes/secure-recommendations/24827.md)]

### Tenant - A Device Clean-up rule is Configured<!--  24802 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24802](./includes/secure-recommendations/24802.md)]

### Tenant - Terms and conditions is configured and assigned<!--  24794 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24794](./includes/secure-recommendations/24794.md)]

### Tenant - Company Portal branding and end-user support settings are customize<!-- 24823 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
 [!INCLUDE [24823](./includes/secure-recommendations/24823.md)]

### Windows - Endpoint Analytics policy is configured and assigned<!-- 24576 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24576](./includes/secure-recommendations/24576.md)]

### Windows - Windows Update policy is configured and assigned<!-- 24553 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24553](./includes/secure-recommendations/24553.md)]

### Windows - A security baseline is configured and assigned<!-- 24573 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24573](./includes/secure-recommendations/24573.md)]

### macOS - Update policy is configured and assigned<!-- 24690 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24690](./includes/secure-recommendations/24690.md)]

### iOS - Update policy is configured and assigned<!-- 24554 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24554](./includes/secure-recommendations/24554.md)]

## Protect networks

### Windows - Firewall is configured and assigned<!-- 24540 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24540](./includes/secure-recommendations/24540.md)]

### Windows - Deploy Attack Surface Reduction (ASR) policies<!-- 24574 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24574](./includes/secure-recommendations/24574.md)]

### Windows - Defender Antivirus policy is configured and assigned<!-- 24575 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24575](./includes/secure-recommendations/24575.md)]

### macOS - Firewall policy is configured and assigned<!-- 24552 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24552](./includes/secure-recommendations/24552.md)]

### macOS - Defender Antivirus policy is configured and assigned<!-- 24784 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24784](./includes/secure-recommendations/24784.md)]

### Corporate Wi-Fi network on iOS devices is securely managed<!-- 24839 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24839](./includes/secure-recommendations/24839.md)]

### Corporate Wi-Fi network on Android devices is securely managed<!-- 24840 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24840](./includes/secure-recommendations/24840.md)]

<!-- ### Corporate Wi-Fi network on macOS devices is securely managed<!-- 24870 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24870](./includes/secure-recommendations/24870.md)] -->

## Related content

- [Deployment guide for Microsoft Intune](/intune/intune-service/fundamentals/get-started-with-intune)
- [Protect data and devices with Microsoft Intune](/intune/intune-service/protect/device-protect)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)


