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

In Microsoft Intune, the following security recommendations are presented across several categories. This structure allows organizations to logically break up projects into related consumable chunks.

> [!TIP]
> Some organizations might take these recommendations exactly as written, while others might choose to make modifications based on their own business needs.
>
> These recommendations should be considered distinct from the recommendations as found in the various security baselines that you might deploy with Intune.


<!-- Subsequent articles to use a similar name structure with actual names to TBD.  Initial proposed ToC structure:

Set up Microsoft Intune
 > URLs and IPI address endpoints
 > Set up Intune subscription
 > Manage roles and permissions
 > Configure security recommendations using Zero Trust  
   > Configure security recommendations using Zero Trust [../protect/zero-trust-configure-security.md]
   > Sub 1  [../protect/zero-trust-group1.md]
   > Sub 2  [../protect/zero-trust-group2.md]
   
-->

## Security guidance

### Windows Firewall policies are configured and assigned<!-- 24540 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24540](./includes/secure-recommendations/24540.md)]

### Compliance policies for Windows devices are configured and assigned<!-- 24541 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24541](./includes/secure-recommendations/24541.md)]

### Compliance policies for macOS devices are configured and assigned<!-- 24542 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24542](./includes/secure-recommendations/24542.md)]

### App protection policies for iOS devices are configured and assigned<!-- 24548 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24548](./includes/secure-recommendations/24548.md)]

### App protection policies for Android devices are configured and assigned<!-- 24549 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24549](./includes/secure-recommendations/24549.md)]


### Windows Hello for Business policies are  configured and assigned <!-- 24551 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24551](./includes/secure-recommendations/24551.md)]

### macOS Firewall policy is created and assigned<!-- 24552 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24552](./includes/secure-recommendations/24552.md)]

### Windows Update policy is configured and assigned<!-- 24553 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24553](./includes/secure-recommendations/24553.md)]

### iOS Update policy is configured and assigned<!-- 24554 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24554](./includes/secure-recommendations/24554.md)]

### macOS Update policy is configured and assigned<!-- 24690 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24690](./includes/secure-recommendations/24690.md)]










### PENDING 24550<!-- 24550 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24550](./includes/secure-recommendations/24550.md)]



### PENDING - 24576<!-- 24576 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24576](./includes/secure-recommendations/24576.md)]


### PENDING - <!-- 24521 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24521](./includes/secure-recommendations/24521.md)]


### PENDING - Compliance policies for iOS and iPadOS devices is configured and assigned<!-- 24543 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24543](./includes/secure-recommendations/24543.md)]



### PENDING - Compliance policies for Android Enterprise (Fully managed and corporate-owned work profile) - <!-- 24545 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24545](./includes/secure-recommendations/24545.md)]


### PENDING - Windows automatic enrollment is configured<!-- 24546 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24546](./includes/secure-recommendations/24546.md)]


### PENDING - Compliance policies for Android Enterprise (personally-owned profiles)<!--  24547 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24547](./includes/secure-recommendations/24547.md)]




### PENDING - Scope Tags are configured for delegated administration<!-- 24555 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24555](./includes/secure-recommendations/24555.md)]



### PENDING - Enrollment restrictions are configured for each platform<!-- 24558 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24558](./includes/secure-recommendations/24558.md)]



### PENDING - Cloud LAPS policy is enforced for Windows<!-- 24560 -->
[!INPENDINGCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24560](./includes/secure-recommendations/24560.md)]



### PENDING - Cloud LAPS policy is enforced for macOS<!-- 24561 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24561](./includes/secure-recommendations/24561.md)]



### PENDING - Windows Delivery Optimization is configured<!-- 24564 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24564](./includes/secure-recommendations/24564.md)]



### PENDING - Account Protection and Local Group Membership policies are configured<!-- 24564 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24564](./includes/secure-recommendations/24564.md)]



### PENDING - Single-sign on for macOS is configured<!-- 24568 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24568](./includes/secure-recommendations/24568.md)]



### PENDING - FileVault encryption for macOS is configured<!-- 24569 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24569](./includes/secure-recommendations/24569.md)]



### PENDING - Enrollment Notification<!-- 24572 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24572](./includes/secure-recommendations/24572.md)]



### PENDING - Security Baselines for Windows devices are deployed<!-- 24573 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24573](./includes/secure-recommendations/24573.md)]



### PENDING - Attack Surface Reduction (ASR) policies for Windows devices<!-- 24574 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24574](./includes/secure-recommendations/24574.md)]



### PENDING - Deploy MDM Based policies for endpoint detection and response (EDR) and anti-virus protection<!-- 24575 -->
[!INCLUDE [applies-to-zero-trust-assessment](./includes/secure-recommendations/applies-to-zero-trust-assessment.md)]

[!INCLUDE [24575](./includes/secure-recommendations/24575.md)]
