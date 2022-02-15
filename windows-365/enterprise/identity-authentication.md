---
# required metadata
title: Windows 365 identity and authentication
titleSuffix:
description: Windows 365 identity and authentication
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/11/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Windows 365 identity and authentication

Identity is a key component of your Windows 365 environment as it will determine which users can connect to their Cloud PCs, how they can connect to their Cloud PCs, and how you manage those Cloud PCs.

## Identity types

There are two identity types:

- **[Hybrid identity](/azure/active-directory/hybrid/whatis-hybrid-identity.md)**: User or devices that exist in both on-premises Windows Server Active Directory and Azure Active Directory.
- **Cloud-only identity**: Users or devices that exist only in Azure Active Directory.


## Device join types

The device join type for your Cloud PCs directly correlates to both the type of identity you want the Cloud PCs to have:

- **[Hybrid Azure AD Join](/azure/active-directory/devices/concept-azure-ad-join-hybrid.md)**: If you choose this join type, Windows 365 will join your Cloud PC to the Windows Server Active Directory domain you provide. Then, if your organization is properly [configured for Hybrid Azure AD Join](/azure/active-directory/devices/howto-hybrid-azure-ad-join.md), the device will be synchronized to Azure Active Directory.
- **[Azure AD Join](/azure/active-directory/devices/concept-azure-ad-join.md)**: If you choose this join type, Windows 365 will join your Cloud PC directly to Azure Active Directory.


Below is a table showing key capabilities or requirements based on the selected join type:

|Capability or requirement|Hybrid Azure AD Join|Azure AD Join|
|-|-|-|
|Azure subscription|Required|Optional|
|Azure virtual network with line of sight to the domain controller|Required|Optional|
|User identity type supported for login|Hybrid users only|Hybrid users or cloud-only users|
|Policy management|Group Policy Objects (GPO) or Intune MDM|Intune MDM only|
|Windows Hello for Business login supported|Yes, and the connecting device must have line of sight to the domain controller through the direct network or a VPN|Yes|

## Authentication

To successfully access a Cloud PC, a user must authenticate, in turn, with both:

- The Windows 365 service.
- The Cloud PC.

>[!NOTE]
>Single sign-on (defined as a single authentication prompt that can satisfy both the Windows 365 service authentication and Cloud PC authentication) is not supported at this time.

>[!IMPORTANT]
>In order for authentication to work properly, the user's local machine must also be able to access the URLs in the [Remote Desktop clients](/azure/virtual-desktop/safe-url-list.md#remote-desktop-clients) section of the [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list.md).

### Windows 365 service authentication

Users must authenticate with the Windows 365 service when:

- They access [windows365.microsoft.com](https://windows365.microsoft.com).
- They navigate to the URL that maps directly to their Cloud PC.
- They use a [Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients.md) to list their Cloud PCs.

This authentication triggers an Azure Active Directory prompt, allowing any credential type that is supported by both Azure Active Directory and your OS.

### Cloud PC authentication

Users must authenticate with the Windows 365 service when:

- They navigate to the URL that maps directly to their Cloud PC.
- They use a [Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients.md) to connect to their Cloud PC.

>[!NOTE]
>If a user launches the web browser URL that maps directly to their Cloud PC, they will encounter the Windows 365 service authentication first, then encounter the Cloud PC authentication.

The following credential types are supported for Cloud PC authentication:
- Windows desktop client
    - Username and password
    - Smartcard
    - [Windows Hello for Business certificate trust](/windows/security/identity-protection/hello-for-business/hello-hybrid-cert-trust.md)
    - [Windows Hello for Business key trust with certificates](/windows/security/identity-protection/hello-for-business/hello-deployment-rdp-certs.md)
- Windows store client
    - Username and password
- Web client
    - Username and password
- Android
    - Username and password
- iOS
    - Username and password
- macOS
    - Username and password


<!-- ########################## -->
## Next steps

[Learn about the Cloud PC lifecycle](lifecycle.md).
