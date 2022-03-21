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

A Cloud PC user's identity defines which access management services manage that user and Cloud PC. This identity defines:

- What types of Cloud PCs the user has access to.
- What types of non-Cloud PC resources the user has access to.

A device can also have an identity which is determined by its join type to Azure Active Directory (Azure AD). For a device, the join type defines:

- If the device requires line of sight to a domain controller.
- How the device is managed.
- How users authenticate to the device.

## Identity types

There are two identity types:

- **[Hybrid identity](/azure/active-directory/hybrid/whatis-hybrid-identity)**: Users or devices that are created in on-premises Windows Server Active Directory, then synchronized to Azure AD.
- **Cloud-only identity**: Users or devices that are created and only exist in Azure AD.

## Device join types

There are two join types that you can select from when [provisioning a Cloud PC](provisioning.md):

- **[Hybrid Azure AD Join](/azure/active-directory/devices/concept-azure-ad-join-hybrid)**: If you choose this join type, Windows 365 will join your Cloud PC to the Windows Server Active Directory domain you provide. Then, if your organization is properly [configured for Hybrid Azure AD Join](/azure/active-directory/devices/howto-hybrid-azure-ad-join), the device will be synchronized to Azure AD.
- **[Azure AD Join](/azure/active-directory/devices/concept-azure-ad-join)**: If you choose this join type, Windows 365 will join your Cloud PC directly to Azure AD.


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
>In order for authentication to work properly, the user's local machine must also be able to access the URLs in the [Remote Desktop clients](/azure/virtual-desktop/safe-url-list#remote-desktop-clients) section of the [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list).

### Windows 365 service authentication

Users must authenticate with the Windows 365 service when:

- They access [windows365.microsoft.com](https://windows365.microsoft.com).
- They navigate to the URL that maps directly to their Cloud PC.
- They use a [Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients to list their Cloud PCs.

This authentication triggers an Azure Active Directory prompt, allowing any credential type that is supported by both Azure Active Directory and your OS.

### Cloud PC authentication

Users must authenticate to their Cloud PC when:

- They navigate to the URL that maps directly to their Cloud PC.
- They use a [Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients) to connect to their Cloud PC.

This authentication request is processed by Azure AD for Azure AD Joined Cloud PCs and on-premises Active Directory for Hybrid Azure AD Joined Cloud PCs.

>[!NOTE]
>If a user launches the web browser URL that maps directly to their Cloud PC, they will encounter the Windows 365 service authentication first, then encounter the Cloud PC authentication.

The following credential types are supported for Cloud PC authentication:
- Windows desktop client
    - Username and password
    - Smartcard
    - [Windows Hello for Business certificate trust](/windows/security/identity-protection/hello-for-business/hello-hybrid-cert-trust)
    - [Windows Hello for Business key trust with certificates](/windows/security/identity-protection/hello-for-business/hello-deployment-rdp-certs)
>[!NOTE]
>Smartcard and Windows Hello authentication require the Windows desktop client to be able to perform Kerberos authentication when used with Hybrid AADJ. This requires the physical client to have line of sight to a domain controller.
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
