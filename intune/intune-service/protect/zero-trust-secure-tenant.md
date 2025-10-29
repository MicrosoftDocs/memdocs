---
title:  Configure Microsoft Intune for increased tenant security
description:  Secure your tenant with Microsoft Intune to support your Zero Trust journey.
ms.topic: reference
ms.date: 10/20/2025
ms.author: brenduns
author: brenduns
ms.reviewer: ramical
ms.collection:
- tier 1
- M365-identity-device-management
---

# Configure Microsoft Intune for Zero Trust: Secure tenants (Preview)

Protecting your Intune tenant is essential to enforcing Zero Trust principles and maintaining a secure, well-managed environment. These recommendations align with Microsoft’s [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars) by limiting blast radius and enforcing least-privilege access through segmented administrative control, secure device onboarding, and policy-driven protections. Together, they help reduce risk, maintain tenant hygiene, and strengthen compliance across platforms.

## Zero Trust security recommendations

### Scope tag configuration is enforced to support delegated administration and least-privilege access<!-- 24555 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24555](./includes/secure-recommendations/24555.md)]

### Device enrollment notifications are enforced to ensure user awareness and secure onboarding<!-- 24572 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
 [!INCLUDE [24572](./includes/secure-recommendations/24572.md)]

### Windows automatic device enrollment is enforced to eliminate risks from unmanaged endpoints<!-- 24546 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24546](./includes/secure-recommendations/24546.md)]

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

### Platform SSO is configured to strengthen authentication on macOS devices<!-- 24568 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24568](./includes/secure-recommendations/24568.md)]

### Automatic enrollment to Microsoft Defender for Endpoint is enabled on Android devices<!-- 24874 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24874](./includes/secure-recommendations/24874.md)]

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

## Related content

- [Deployment guide for Microsoft Intune](/intune/intune-service/fundamentals/get-started-with-intune)
- [Protect data and devices with Microsoft Intune](/intune/intune-service/protect/device-protect)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)