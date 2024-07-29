---
title: Include file
description: include file
author: brenduns  
ms.service: microsoft-intune
ms.topic: include
ms.date: 02/12/2024
ms.author: brenduns
ms.custom: include file
---

> [!IMPORTANT]
>
> To support Windows requirements for strong mapping of SCEP certificates that were introduced and announced in [KB5014754 from May 10, 2022](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16) we’ve made changes to Intune SCEP certificate issuance for new and renewed SCEP certificates. With these changes, new or renewed Intune SCEP certificates for iOS/iPadOS, macOS, and Windows now include the following tag in the Subject Alternative Name (SAN) field of the certificate: `URL=tag:microsoft.com,2022-09-14:sid:<value>`  
>
> This tag is used by strong mapping to tie a certificate to a specific device or user SID from Entra ID. With this change and requirement to map a SID from Entra ID:  
>
> - Device certificates are supported for Windows hybrid-joined devices when that device has a SID in Entra ID that has been synchronized from an on-premises Active Directory.
> - User certificates use the User's SID from Entra ID, synced from on-premises Active Directory.
>
> Certification Authorities (CAs) that do not support the URL tag in the SAN might fail to issue certificates. Microsoft Active Directory Certificate Services servers that installed the update from [KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16) support the use of this tag. If you use a third-party CA, check with your CA provider to ensure they support this format, or how and when this support will be added.
>
> For more information, see [Support tip: Implementing strong mapping in Microsoft Intune certificates - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-implementing-strong-mapping-in-microsoft-intune/ba-p/4053376).