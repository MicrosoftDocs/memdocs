---
title: CMG client authentication
titleSuffix: Configuration Manager
description: Plan for how clients authenticate to the cloud management gateway (CMG).
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# CMG client authentication

*Applies to: Configuration Manager (current branch)*

Clients that connect to a cloud management gateway (CMG) are potentially on the untrusted public internet. Because of the client's origin, they have a higher authentication requirement. There are three options for identity and authentication with a CMG:

- Azure AD
- PKI certificates
- Configuration Manager site-issued tokens

The following table summarizes the key factors for each method:

|         | Azure AD | PKI certificate | Site token |
|---------|---------|---------|---------|
| **ConfigMgr version** | All supported | All supported | All supported |
| **Windows client version** | Windows 10 or later | All supported | All supported |
| **Scenario support** | User and device | Device-only | Device-only |
| **Management point** | E-HTTP or HTTPS | E-HTTP or HTTPS | E-HTTP or HTTPS |

Microsoft recommends joining devices to Azure AD. Internet-based devices can use Azure AD modern authentication with Configuration Manager. It also enables both device and user scenarios whether the device is on the internet or connected to the internal network.

You can use one or more methods. All clients don't have to use the same method.

Which ever method you choose, you may also need to reconfigure one or more management points. For more information, see [Configure client authentication for CMG](configure-authentication.md#enable-management-point-for-https).

## Azure AD

If your internet-based devices are running Windows 10 or later, consider using Azure AD modern authentication with the CMG. This authentication method is the only one that enables user-centric scenarios. For example, deploying apps to a user collection.

First, the devices need to be either cloud domain-joined or hybrid Azure AD-joined, and the user also needs an Azure AD identity. If your organization is already using Azure AD identities, then you should be set with this prerequisite. If not, talk with your Azure administrator to plan for cloud-based identities. For more information, see [Azure AD device identity](/azure/active-directory/devices/). Until that process is complete, consider [token-based authentication](#site-token) for internet-based clients with your CMG.

There are a few other requirements, depending upon your environment:

- Enable user discovery methods for hybrid identities
- Enable ASP.NET 4.5 on the management point
- Configure client settings

For more information on these prerequisites, see [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md).

> [!NOTE]
> If your devices are in an Azure AD tenant that's separate from the tenant with a subscription for the CMG compute resources, starting in version 2010 you can disable authentication for tenants not associated with users and devices. For more information, see [Configure Azure services](../../../servers/deploy/configure/azure-services-wizard.md#disable-authentication).<!--8537319-->

## PKI certificate

If you have a public key infrastructure (PKI) that can issue client authentication certificates to devices, then consider this authentication method for internet-based devices with your CMG. It doesn't support user-centric scenarios, but supports devices running any supported version of Windows.

> [!TIP]
> Windows devices that are hybrid or cloud domain-joined don't require this certificate because they use [Azure AD](#azure-ad) to authenticate.

This certificate may also be required on the CMG connection point.

## Site token

If you can't join devices to Azure AD or use PKI client authentication certificates, then use Configuration Manager token-based authentication. Site-issued client authentication tokens work on all supported client OS versions, but only support device scenarios.

If clients occasionally connect to your internal network, they're automatically issued a token. They need to communicate directly with an on-premises management point to register with the site and get this client token.

If you can't register clients on the internal network, you can create and deploy a bulk registration token. The bulk registration token enables the client to initially install and communicate with the site. This initial communication is long enough for the site to issue the client its own, unique client authentication token. The client then uses its authentication token for all communication with the site while it's on the internet.

## Next steps

Next, design how to use a CMG in your hierarchy:
  
> [!div class="nextstepaction"]
> [CMG hierarchy design](plan-hierarchy-design.md)
