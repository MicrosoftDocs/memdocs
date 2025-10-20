---
title:  Configure Microsoft Intune for increased device security
description: Secure devices with Microsoft Intune to support your Zero Trust journey.
ms.topic: reference
ms.date: 10/20/2025
ms.author: brenduns
author: brenduns
ms.reviewer: ramical
ms.collection:
- tier 1
- M365-identity-device-management
---

# Configure Microsoft Intune for Zero Trust: Secure devices (Preview)

Securing endpoints is a critical part of a Zero Trust strategy. These Intune recommendations help protect your network perimeter and devices through policy-driven controls that enforce encryption, restrict unauthorized access, and reduce vulnerability exposure. By applying configuration and security policies across platforms, these checks align with Microsoft’s [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars) and strengthen your organization’s overall security posture.

## Zero Trust security recommendations

### Local administrator credentials on Windows are protected by Windows LAPS<!-- 24560 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24560](./includes/secure-recommendations/24560.md)]

### Local administrator credentials on macOS are protected during enrollment by macOS LAPS<!--  24561 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24561](./includes/secure-recommendations/24561.md)]

<!-- ### Platform SSO is enforced on macOS to enable phishing-resistant authentication<!-- 24568 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24568](./includes/secure-recommendations/24568.md)]-->

### Local account usage on Windows is restricted to reduce unauthorized access<!--  24564 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24564](./includes/secure-recommendations/24564.md)]

### Data on Windows is protected by BitLocker encryption<!-- 24550 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24550](./includes/secure-recommendations/24550.md)]

### FileVault encryption protects data on macOS devices<!-- 24569 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24569](./includes/secure-recommendations/24569.md)]

### Authentication on Windows uses Windows Hello for Business<!-- 24551-->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24551](./includes/secure-recommendations/24551.md)]

### Defender Antivirus policies protect Windows devices from malware<!-- 24575 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24575](./includes/secure-recommendations/24575.md)]

### Defender Antivirus policies protect macOS devices from malware<!-- 24784 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24784](./includes/secure-recommendations/24784.md)]

### Data on Android is protected by app protection policies<!-- 24549 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24549](./includes/secure-recommendations/24549.md)]

### Data on iOS/iPadOS is protected by app protection policies<!-- 24548 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24548](./includes/secure-recommendations/24548.md)]

## Related content

- [Deployment guide for Microsoft Intune](/intune/intune-service/fundamentals/get-started-with-intune)
- [Protect data and devices with Microsoft Intune](/intune/intune-service/protect/device-protect)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)
- [Configure Microsoft Intune for increased security (preview)](/intune/intune-service/protect/zero-trust-configure-security)
