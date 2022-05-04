---
# required metadata

title: Use on-premises services with cloud native endpoints
titleSuffix: Microsoft Endpoint Manager
description: For cloud native endpoints to access on-premises resources, such as file servers, printers, and web servers, use Windows integrated authentication (WIA) and Azure AD Connect.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 05/03/2022
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

# Cloud native endpoints and on-premises resources

**TO DO:**

- ??Answer some outstanding questions.??
- ??In the "Authentication and access to on-premises resources" section, is there an image we can add? It might help??

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](../includes/cloud-native-endpoints-definitions.md)]

Cloud native endpoints can access on-premises resources. This article goes into more detail, and answers some common questions.

This feature applies to:

- Windows cloud native endpoints

For an overview of cloud native endpoints, and their benefits, go to [What are cloud native endpoints?](cloud-native-endpoints-overview.md).

## Prerequisites

For cloud native Windows endpoints to access on-premises resources and services that use on-premises Active Directory (AD) for authentication, the following prerequisites are required:

- Client apps **must use Windows integrated authentication (WIA)**. For more specific information, see [Windows Integrated Authentication (WIA)](/aspnet/web-api/overview/security/integrated-windows-authentication).

- **Configure Azure AD Connect**. Azure AD Connect synchronizes user accounts from the on-premises AD to Azure AD. For more specific information, see [Azure AD Connect sync: Understand and customize synchronization](/azure/active-directory/hybrid/how-to-connect-sync-whatis).

  In Azure AD Connect, you may have to adjust your domain-based filtering to confirm that the required domains data is synchronized to Azure AD.

- The device has line of sight **connectivity (either directly or through VPN) to a domain controller** from the AD domain and to the service or resource being accessed.

## Similar to on-premises Windows devices

For end users, a Windows cloud native endpoint behaves like any other on-premises Windows device. 

The following list is a common set of on-premises resources that users can access from their Windows Azure AD joined devices:

- A file server: Using SMB (Server Message Block), you can map a network drive to a domain-member server that hosts a network share or NAS (Network Attached Storage).

  Users can map drives to shared and personal documents.

- A printer resource on a domain-member server: Users can print to their local or nearest printer.
- A web server on a domain-member server that uses Windows Integrated security: Users can access any Win32 or web-based application.
- Want to manage your on-premises AD domain from an Azure AD joined endpoint: Install the [Remote Server Administration Tools](https://www.microsoft.com/download/details.aspx?id=45520):

  - Use the Active Directory Users and Computers (ADUC) snap-in to administer all AD objects. You must manually enter the domain that you want to connect to.
  - Use the DHCP snap-in to administer an AD-joined DHCP server. You might need to enter the DHCP server name or address.

> [!TIP]
> To understand how Azure AD joined devices use cached credentials in a cloud native approach, watch [OPS108: Windows authentication internals in a hybrid world (syfuhs.net)](https://syfuhs.net/ops108-windows-authentication-internals-in-a-hybrid-world) (opens an external website).

## Authentication and access to on-premises resources

The following steps describe how an Azure AD joined endpoint authenticates and accesses (based on permissions) an on-premises resource.

The following steps are an overview. For more specific information, see [Primary Refresh Token (PRT) and Azure AD](/azure/active-directory/devices/concept-primary-refresh-token).

1. When users sign in, their credentials are sent to the Cloud Authentication Provider (CloudAP) and the Web Account Manager (WAM).

2. The CloudAP plugin sends the user and device credentials to Azure AD. Or, [it authenticates using Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-how-it-works-authentication).

3. During Windows sign in, the Azure AD CloudAP plugin requests a Primary Refresh Token (PRT) from Azure AD using the user credentials. It also caches the PRT, which enables cached sign in when users don't have an internet connection. When users try to access applications, the Azure AD WAM plugin uses the PRT to enable SSO.

4. Azure AD authenticates the user and device, and returns a PRT & an ID token. The ID token includes the following attributes about the user:

    - `sAMAccountName`
    - `netBIOSDomainName`
    - `dnsDomainName`

    These attributes are synced from on-premises AD using Azure AD Connect.

    The Kerberos Authentication Provider receives the credentials and the attributes. On the device, the Windows Local Security Authority (LSA) service enables Kerberos and NTLM authentication.

5. During an access attempt to an on-premises resource requesting Kerberos or NTLM authentication, the device uses the domain name related attributes to find a Domain Controller (DC) using DC Locator.

    - If a DC is found, it sends the credentials and the `sAMAccountName` to the DC for authentication.
    - If using Windows Hello for Business, it does [PKINIT](/openspecs/windows_protocols/ms-pkca/d0cf1763-3541-4008-a75f-a577fa5e8c5b) with the Windows Hello for Business certificate.
    - If no DC is found, then no on-premises authentication happens.

    > [!NOTE]
    > PKINIT is a preauthentication mechanism for Kerberos 5 which uses X.509 certificates to authenticate the Key Distribution Center (KDC) to clients and vice versa.
    > 
    > [MS-PKCA: Public Key Cryptography for Initial Authentication (PKINIT) in Kerberos Protocol](/openspecs/windows_protocols/ms-pkca/d0cf1763-3541-4008-a75f-a577fa5e8c5b)

6. The DC authenticates the user. The DC returns a Kerberos Ticket-Granting Ticket (TGT) or a NTLM token based on the protocol that the on-premises resource or application supports (which Windows caches). ??Caches what specifically??

    If the attempt to get the Kerberos TGT or NTLM token for the domain fails (related DCLocator timeout can cause a delay), then Windows Credential Manager retries. Or, the user may receive an authentication pop-up requesting credentials for the on-premises resource.

7. All apps that use [Windows Integrated Authentication (WIA)](/aspnet/web-api/overview/security/integrated-windows-authentication) automatically get SSO when a user tries to access the apps. **This** includes standard user authentication to an on-premises AD domain using NTLM or Kerberos when accessing on-premises services or resources. ??What's meant by 'this'? Do you mean SSO??

    For more information, see [How SSO to on-premises resources works on Azure AD joined devices](/azure/active-directory/devices/azuread-join-sso).

    It's important to emphasize the value of Windows Integrated Authentication. Native cloud endpoints simply "work" with any application configured for WIA.

    When users access a resource that uses WIA, like a file server, printer, web server, and more, then the TGT is exchanged with a Kerberos service ticket, which is the usual Kerberos workflow.

## Follow the cloud native endpoints guidance

1. [Overview: What are cloud native endpoints?](cloud-native-endpoints-overview.md)
2. [Tutorial: Get started with cloud native Windows endpoints](cloud-native-windows-endpoints.md)
3. [Concept: Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md)
4. 🡺 **Concept: Cloud native endpoints and on-premises resources** (*You are here*)
5. [High level planning guide](cloud-native-endpoints-planning-guide.md)
6. [Known issues and important information](cloud-native-endpoints-known-issues.md)

## Helpful online resources

- [Primary Refresh Token (PRT) and Azure AD](/azure/active-directory/devices/concept-primary-refresh-token)
- [How SSO to on-premises resources works on Azure AD joined devices](/azure/active-directory/devices/azuread-join-sso)
- [How Windows Hello for Business works - Authentication - Windows security](/windows/security/identity-protection/hello-for-business/hello-how-it-works-authentication)
- [Integrated Windows Authentication](/aspnet/web-api/overview/security/integrated-windows-authentication)
- [Azure AD Kerberos authentication (Preview)](/azure/active-directory/authentication/how-to-authentication-kerberos)
- [Azure AD Authentication documentation](/azure/active-directory/authentication/)
