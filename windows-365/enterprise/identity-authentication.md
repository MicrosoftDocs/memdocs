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
ms.service: windows-365
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
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 identity and authentication

A Cloud PC user's identity defines which access management services manage that user and Cloud PC. This identity defines:

- The types of Cloud PCs the user has access to.
- The types of non-Cloud PC resources the user has access to.

A device can also have an identity that is determined by its join type to Azure Active Directory (Azure AD). For a device, the join type defines:

- If the device requires line of sight to a domain controller.
- How the device is managed.
- How users authenticate to the device.

## Identity types

There are three identity types:

- **[Hybrid identity](/azure/active-directory/hybrid/whatis-hybrid-identity)**: Users or devices that are created in on-premises Windows Server Active Directory, then synchronized to Azure AD.
- **Cloud-only identity**: Users or devices that are created and only exist in Azure AD.
- **[External identity](/azure/active-directory/external-identities/identity-providers)**: Users who are created and managed outside of your Azure AD tenant but are invited in to your Azure AD tenant to access your organization's resources.

>[!NOTE]
>Windows 365 does not support external identities.

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
|Windows Hello for Business sign-in supported|Yes, and the connecting device must have line of sight to the domain controller through the direct network or a VPN|Yes|

## Authentication

To successfully access a Cloud PC, a user must authenticate, in turn, with both:

- The Windows 365 service.
- The Cloud PC.

Windows 365 offers single sign-on (defined as a single authentication prompt that can satisfy both the Windows 365 service authentication and Cloud PC authentication) as part of the service. See [single sign-on](#single-sign-on-sso) for more information.

>[!IMPORTANT]
>In order for authentication to work properly, the user's local machine must also be able to access the URLs in the [Remote Desktop clients](/azure/virtual-desktop/safe-url-list#remote-desktop-clients) section of the [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list).

## Windows 365 service authentication

Users must authenticate with the Windows 365 service when:

- They access [windows365.microsoft.com](https://windows365.microsoft.com).
- They navigate to the URL that maps directly to their Cloud PC.
- They use a [Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients) to list their Cloud PCs.

This authentication triggers an Azure Active Directory prompt, allowing any credential type that is supported by both Azure Active Directory and your OS.

### Passwordless authentication
You can use any authentication type supported by Azure AD, such as [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) and other [passwordless authentication options](/azure/active-directory/authentication/concept-authentication-passwordless) (for example, FIDO keys), to authenticate to the service.

### Smart card authentication
To use a smart card to authenticate to Azure AD, you must first [configure AD FS for user certificate authentication](/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication) or [configure Azure AD certificate-based authentication](/azure/active-directory/authentication/concept-certificate-based-authentication).

## Cloud PC authentication

Users must authenticate to their Cloud PC when:

- They navigate to the URL that maps directly to their Cloud PC.
- They use a [Remote Desktop client](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients) to connect to their Cloud PC.

This authentication request is processed by Azure AD for Azure AD Joined Cloud PCs and on-premises Active Directory for Hybrid Azure AD Joined Cloud PCs.

>[!NOTE]
>If a user launches the web browser URL that maps directly to their Cloud PC, they will encounter the Windows 365 service authentication first, then encounter the Cloud PC authentication.

The following credential types are supported for Cloud PC authentication:
- Windows desktop client
    - [Single sign-on](#single-sign-on-sso)
    - Username and password
    - Smartcard
    - [Windows Hello for Business certificate trust](/windows/security/identity-protection/hello-for-business/hello-hybrid-cert-trust)
    - [Windows Hello for Business key trust with certificates](/windows/security/identity-protection/hello-for-business/hello-deployment-rdp-certs)
>[!NOTE]
>Smartcard and Windows Hello authentication require the Windows desktop client to be able to perform Kerberos authentication when used with Hybrid AADJ. This requires the physical client to have line of sight to a domain controller.
- Windows store client
    - Username and password
- Web client
    - [Single sign-on](#single-sign-on-sso)
    - Username and password
- Android
    - Username and password
- iOS
    - Username and password
- macOS
    - Username and password

### Single sign-on (SSO)

>[!Important]
>Single sign-on is in [public preview](../public-preview.md) for Azure AD joined Cloud PCs.
>
>Single sign-on is not supported for Hybrid Azure AD joined Cloud PCs.

Single sign-on (SSO) allows the connection to skip the Cloud PC VM credential prompt and automatically sign the user in to Windows through Azure AD authentication. Azure AD authentication provides other benefits including passwordless authentication and support for third-party identity providers. Single sign-on is available on Cloud PCs (either [gallery images](device-images.md#gallery-images) or [custom images](device-images.md#custom-images)) using the following operating systems:

- Windows 11 Enterprise with the [2022-09 Cumulative Updates for Windows 11 Preview (KB5017383)](https://support.microsoft.com/kb/KB5017383) or later installed.
- Windows 10 Enterprise, versions 20H2 or later with the [2022-09 Cumulative Updates for Windows 10 Preview (KB5017380)](https://support.microsoft.com/kb/KB5017380) or later installed.

Without SSO, the client will prompt users for their session host credentials for every connection. The only way to avoid being prompted is to save the credentials in the client. We recommend you only save credentials on secure devices to prevent other users from accessing your resources.

>[!NOTE]
>To maintain single sign-on to Kerberos-based apps and resources in the Cloud PC environment, you must properly [configure your environment to trust the Azure AD Kerberos service](/azure/active-directory/authentication/howto-authentication-passwordless-security-key-on-premises).

## In-session authentication

Once you're connected to your Cloud PC, you may be prompted for authentication inside the session. This section explains how to use credentials other than username and password in this scenario.

### In-session passwordless authentication (preview)

> [!IMPORTANT]
> In-session passwordless authentication is currently in [public preview](../public-preview.md).

Windows 365 supports in-session passwordless authentication (preview](/windows-365/public-preview)) using [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) or security devices like FIDO keys when using the [Windows Desktop client](../end-user-access-cloud-pc.md#remote-desktop). Passwordless authentication is enabled automatically when the Cloud PC and local PC are using the following operating systems:

  - Windows 11 Enterprise with the [2022-09 Cumulative Updates for Windows 11 Preview (KB5017383)](https://support.microsoft.com/kb/KB5017383) or later installed.
  - Windows 10 Enterprise, versions 20H2 or later with the [2022-09 Cumulative Updates for Windows 10 Preview (KB5017380)](https://support.microsoft.com/kb/KB5017380) or later installed.
  
When enabled, all WebAuthn requests in the session are redirected to the local PC. You can use Windows Hello for Business or locally attached security devices to complete the authentication process.

To access Azure AD resources with Windows Hello for Business or security devices, you must enable the FIDO2 Security Key as an authentication method for your users. To enable this method, follow the steps in [Enable FIDO2 security key method](/azure/active-directory/authentication/howto-authentication-passwordless-security-key#enable-fido2-security-key-method).

### In-session smart card authentication

To use a smart card in your session, make sure you've installed the smart card drivers on the Cloud PC and allow smart card redirection as part of [managing RDP device redirections for Cloud PCs](manage-rdp-device-redirections.md). Review the [client comparison chart](/windows-server/remote/remote-desktop-services/clients/remote-desktop-app-compare#other-redirection-devices-etc) to make sure your client supports smart card redirection.

<!-- ########################## -->
## Next steps

[Learn about the Cloud PC lifecycle](lifecycle.md).