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

Understanding the types of identity in your organization is an important factor in how you create your Cloud PCs:

- **[Hybrid identity](/azure/active-directory/hybrid/whatis-hybrid-identity.md)**: User or devices that exist in both on-premises Windows Server Active Directory and Azure Active Directory.
- **Cloud-only identity**: Users or devices that exist only in Azure Active Directory.


## Device join types

The device join type for your Cloud PCs directly correlates to both the type of identity you want the Cloud PCs to have:

- **[Hybrid Azure AD Join](/azure/active-directory/devices/concept-azure-ad-join-hybrid.md)**: If you choose this join type, Windows 365 will join your Cloud PC to the Windows Server Active Directory domain, then rely on the Azure Active Directory Connect tool or your own Windows Server Active Directory Federation Services (AD FS) to synchronize these identites to Azure Active directory.
- **[Azure AD Join](/azure/active-directory/devices/concept-azure-ad-join.md)**: If you choose this join type, Windows 365 will join your Cloud PC directly to Azure Active Directory.


Below is a table showing key capabilities or requirements based on the selected join type:

|Capability or requirement|Hybrid Azure AD Join|Azure AD Join|
|-|-|-|
|Azure subscription required|Yes, and an Azure virtual network with line of sight to the domain controller|No|
|User identity type supported for login|Hybrid users only|Hybrid users or cloud-only users|
|Policy management|Group Policy Objects (GPO) or Intune MDM|Intune MDM only|
|Windows Hello for Business login supported|Yes, and the connecting device must have line of sight to the domain controller through the direct network or a VPN|Yes|

## Authentication

To complete the end to end connection of accessing a Cloud PC, users must first authenticate to the Windows 365 service and then authenticate to the Cloud PC.

>[!NOTE]
>Single sign-on (defined as a single authentication prompt that can satisfy both the Windows 365 service authentication and Cloud PC authentication) is not supported at this time.

## Windows 365 service authentication

The Windows 365 service authentication surfaces in one of two ways:

- When users access [windows365.microsoft.com](https://windows365.microsoft.com) or launch the web browser URL that maps directirecly to their Cloud PC.
- When users access through one of the [Remote Desktop clients](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients.md) and list their Cloud PCs.

This authentication triggers an Azure Active Directory prompt, allowing any credential type that is supported by both Azure Active Directory and your OS.

## Cloud PC authentication

The Cloud PC authentication surfaces in one of the two ways:

- When users launch the web browser URL that maps directly to their Cloud PC.
- When users access through one of the [Remote Desktop clients](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients.md) and select the specific Cloud PC.

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

>[!IMPORTANT]
>In order for authentication to work properly, the user's local machine must also be able to access the URLs in the [Remote Desktop clients](/azure/virtual-desktop/safe-url-list.md#remote-desktop-clients) section of the [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list.md).

<!-- ########################## -->
## Next steps

[Learn about the Cloud PC lifecycle](lifecycle.md).
