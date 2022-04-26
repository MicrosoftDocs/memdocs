---
# required metadata

title: Azure AD Kerberos and cloud native endpoints
titleSuffix: Microsoft Endpoint Manager
description: Learn more about how you can use Azure AD Kerberos with cloud native endpoints. You can move on-premises services that Kerberos authentication to the cloud, such as Win32 apps and file services.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 03/03/2022
ms.topic: conceptual
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer: ahamil, jasandys, wicale
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
---

# Azure AD Kerberos (preview)

Azure AD Kerberos is in preview. It helps organizations migrate on-premises services that use Kerberos authentication, like Win32 apps, file services, web sites, and more to the cloud. It maintains backward compatibility for Kerberos authentication.

Azure AD supports Kerberos authentication to Azure AD. ??What??

For example, [Azure Files](/azure/storage/files/storage-files-introduction) support identity-based authentication over Server Message Block (SMB). It uses [on-premises Active Directory Domain Services (AD DS)](/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview) and [Azure Active Directory Domain Services (Azure AD DS)](/azure/active-directory-domain-services/overview).

With Azure AD Kerberos, end users can use their Azure AD credentials on Azure AD joined cloud native endpoints, including virtual machines (VMs), to authenticate and access Azure Files using Kerberos. They don't rely on their AD DS or Azure AD DS to provide a Kerberos ticket for access to Azure Files.

> [!IMPORTANT]
> Azure AD Kerberos doesn't address the challenges outlined in [Known Issues and Limitations](cloud-native-endpoints-known-issues.md), which require a machine account in your on-premises AD domain.

For a deeper understanding of Azure AD Kerberos (in Preview) and the scenarios it can address, see the following blogs:

- [Why We Built Azure AD Kerberos](https://syfuhs.net/why-we-built-azure-ad-kerberos) (opens an external website)
- [Deep dive: How Azure AD Kerberos works](https://techcommunity.microsoft.com/t5/itops-talk-blog/deep-dive-how-azure-ad-kerberos-works/ba-p/3070889) (opens another Microsoft website)
- [How Azure AD Kerberos Works (syfuhs.net)](https://syfuhs.net/how-azure-ad-kerberos-works) (opens an external website)

## Next steps

- [What are cloud native endpoints?](cloud-native-endpoints-overview.md)
- [Tutorial: Get started with cloud native Windows endpoints with Microsoft Endpoint Manager](cloud-native-windows-endpoints.md)
- [Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md)
- [Cloud native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
- [Planning guide](cloud-native-endpoints-planning-guide.md)
- [Known issues](cloud-native-endpoints-known-issues.md)
