---
title:  Configure Microsoft Intune for increased security
description:  Learn how to improve your security posture with Microsoft Intune.
 
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: reference
ms.date:  08/29/2025

ms.author: brenduns
author: brenduns
manager: laurawi
ms.reviewer: ramical

# optional metadata

#ROBOTS:
#audience:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
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

<!-- >
## Protect tenants 
## Apply Compliance policies on devices 
## Protect Apple devices 
## Protect Android devices
## Protect Windows devices 
## Protect Apps on devices
-->

## Protect tenants

<!-- 24521 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24521](./includes/secure-recommendations/24521.md)]-->

### Intune Scope Tags are configured for delegated administration<!-- 24555 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24555](./includes/secure-recommendations/24555.md)]

<!-- 24558 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24558](./includes/secure-recommendations/24558.md)]-->

### Device enrollment notification is configured and assigned<!-- 24572 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
 [!INCLUDE [24572](./includes/secure-recommendations/24572.md)] 


## Apply Compliance policies on devices

<!-- 24545 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24545](./includes/secure-recommendations/24545.md)]-->

<!-- 24547 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24547](./includes/secure-recommendations/24547.md)]-->

<!-- 24543 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24543](./includes/secure-recommendations/24543.md)]-->

### Compliance policies for macOS devices are configured and assigned<!-- 24542 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24542](./includes/secure-recommendations/24542.md)]

### Compliance policies for Windows devices are configured and assigned<!-- 24541 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24541](./includes/secure-recommendations/24541.md)]

## Protect Apple devices

<!-- 24561 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24561](./includes/secure-recommendations/24561.md)]-->

## macOS Defender Antivirus policy is configured and assigned<!-- 24784 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24784](./includes/secure-recommendations/24784.md)]

### macOS FileVault policy is created and Assigned<!-- 24569 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24569](./includes/secure-recommendations/24569.md)]

### macOS Firewall policy is created and assigned<!-- 24552 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24552](./includes/secure-recommendations/24552.md)]

### iOS Update policy is configured and assigned<!-- 24554 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24554](./includes/secure-recommendations/24554.md)]

### macOS Update policy is configured and assigned<!-- 24690 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24690](./includes/secure-recommendations/24690.md)]

<!-- 24568 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
<!-- [!INCLUDE [24568](./includes/secure-recommendations/24568.md)]-->

## Protect Windows devices 

### Windows Cloud LAPS policy is created and assigned<!-- 24560 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24560](./includes/secure-recommendations/24560.md)]

### Windows BitLocker policy is configured and assigned<!-- 24550 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24550](./includes/secure-recommendations/24550.md)]

### Windows Firewall policies are configured and assigned<!-- 24540 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24540](./includes/secure-recommendations/24540.md)]

### Windows Update policy is configured and assigned<!-- 24553 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24553](./includes/secure-recommendations/24553.md)]

### Windows Hello for Business policies are  configured and assigned <!-- 24551-->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24551](./includes/secure-recommendations/24551.md)]

### A Windows security baseline is configured and assigned<!-- 24573 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24573](./includes/secure-recommendations/24573.md)]

<!-- 24564 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24564](./includes/secure-recommendations/24564.md)]-->

<!-- 24574 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24574](./includes/secure-recommendations/24574.md)]-->

<!-- 24575 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24575](./includes/secure-recommendations/24575.md)]-->

### Windows Automatic Enrollment is enabled<!-- 24546 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24546](./includes/secure-recommendations/24546.md)]

<!-- 24562 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
<!-- [!INCLUDE [24562](./includes/secure-recommendations/24562.md)]-->

### Intune Endpoint Analytics policy is created and Assigned<!-- 24576 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)] -->
[!INCLUDE [24576](./includes/secure-recommendations/24576.md)]

## Protect Apps on devices

### App protection policies for Android devices are configured and assigned<!-- 24549 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24549](./includes/secure-recommendations/24549.md)]

### App protection policies for iOS devices are configured and assigned<!-- 24548 -->
<!-- [!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]  -->
[!INCLUDE [24548](./includes/secure-recommendations/24548.md)]


## Related content

- [Deployment guide for Microsoft Intune](/intune/intune-service/fundamentals/get-started-with-intune)
- [Protect data and devices with Microsoft Intune](/intune/intune-service/protect/device-protect)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)





