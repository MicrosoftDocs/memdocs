---
# required metadata

title: You need to enable Code Integrity | Microsoft Docs
description:
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2019
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 84892bbc-f888-417b-bbeb-978cc7e10028
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: scottduf
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Enable code integrity

Your organization might require your PC to be enabled with a threat protection feature called *code integrity*. Code integrity checks the drivers and system files on your device for signs of corruption or malicious software. For code integrity to work on your device, another security feature called [*Secure Boot*](https://docs.microsoft.com/windows/security/information-protection/secure-the-windows-10-boot-process#secure-boot) must also be enabled.

If your PC isn't compliant because code integrity is disabled, contact your organization's IT support person. Your support person will help you enable Secure Boot, which will trigger code integrity the next time you start up your device. 

If you identify yourself as an advanced device user and want to try the steps on your own, see [Re-enable Secure Boot](https://docs.microsoft.com/windows-hardware/manufacture/desktop/disabling-secure-boot#re-enable-secure-boot).

## Additional resources for IT administrators

If you're an Intune administrator and want to learn more about Intune's device health compliance settings, see [Add a device compliance policy for Windows 10 devices in Intune](https://docs.microsoft.com/intune/protect/compliance-policy-create-windows). For a detailed look at the compliance actions you can take in Intune, see the [HealthAttestation CSP](https://docs.microsoft.com/windows/client-management/mdm/healthattestation-csp#step-8-take-appropriate-policy-action-based-on-evaluation-results).  

## Next steps

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
