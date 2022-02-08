---
# required metadata
title: Authentication in Windows 365 Enterprise
titleSuffix:
description: Learn about authentication in Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/22/2021
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

---

# Identity and authentication overview

The ability for users 

## Identities
To understand which identities are supported, see []

### Hybrid identity
Windows 365 Enterprise requires [hybrid identities](/azure/active-directory/hybrid/whatis-hybrid-identity) for users to both receive and access a Cloud PC.

### Cloud-only identity
Windows 365 only supports [cloud-only identities](/microsoft-365/enterprise/about-microsoft-365-identity?view=o365-worldwide#cloud-only-identity) in the [Windows 365 Business](https://www.microsoft.com/windows-365/business) offering.

### External identity
Windows 365 doesn't support [external identities](/azure/active-directory/external-identities/).

## Authenticating to Windows 365 Service
To access Windows 365 and view your Cloud PCs, you must sign-in to Azure Active Directory. This process will trigger automatically when you:
 - Access the [Windows 365 Portal](https://windows365.microsoft.com) in the browser
 - Subscribe or refresh your feed in a supported [Microsoft Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients)



## Authenticating to Windows 365 Cloud PC
To complete the sign-in process to the Windows 365 Cloud PC, you can use any of the following authentication methods, depending on the client you are using:
 - Windows Desktop client
     - Password
     - Smartcard
     - [Windows Hello for Business certificate trust](/windows/security/identity-protection/hello-for-business/hello-hybrid-cert-trust)
     - [Windows Hello for Business key trust with certificates](/windows/security/identity-protection/hello-for-business/hello-deployment-rdp-certs)
 - Web client
     - Password
 - Android client
     - Password
 - iOS client
     - Password
 - macOS client
     - Password

