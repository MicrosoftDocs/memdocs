---
title: Plan for security
titleSuffix: Configuration Manager
description: Get best practices and other information about security in Configuration Manager.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Plan for security in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article describes the following concepts for you to consider when planning for security with your Configuration Manager implementation:

- Certificates (self-signed and PKI)

- The trusted root key

- Signing and encryption

- Role-based administration

- Azure Active Directory

- SMS Provider authentication

Before you start, make sure you're familiar with the [fundamentals of security in Configuration Manager](../../understand/fundamentals-of-security.md).

## Certificates

Configuration Manager uses a combination of self-signed and public key infrastructure (PKI) digital certificates. Use PKI certificates whenever possible. Some scenarios require PKI certificates. When PKI certificates aren't available, the site automatically generates self-signed certificates. Some scenarios always use self-signed certificates.

For more information, see [Plan for certificates](plan-for-certificates.md).

## The trusted root key

The Configuration Manager trusted root key provides a mechanism for Configuration Manager clients to verify that site systems belong to their hierarchy. Every site server generates a site exchange key to communicate with other sites. The site exchange key from the top-level site in the hierarchy is called the trusted root key.

The function of the trusted root key in Configuration Manager resembles a root certificate in a public key infrastructure. Anything signed by the private key of the trusted root key is trusted further down the hierarchy. Clients store a copy of the site's trusted root key in the `root\ccm\locationservices` WMI namespace.

For example, the site issues a certificate to the management point, which it signs with the private key of the trusted root key. The site shares with clients the public key of its trusted root key. Then clients can differentiate between management points that are in their hierarchy and management points that aren't in their hierarchy.

Clients automatically get the public copy of the trusted root key by using two mechanisms:

- You extend the Active Directory schema for Configuration Manager, and publish the site to Active Directory Domain Services. Then clients retrieve this site information from a global catalog server. For more information, see [Prepare Active Directory for site publishing](../network/extend-the-active-directory-schema.md).

- When you install clients using the client push installation method. For more information, see [Client push installation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).

If clients can't get the trusted root key by using one of these mechanisms, they trust the trusted root key that's provided by the first management point that they communicate with. In this scenario, a client might be misdirected to an attacker's management point where it would receive policy from the rogue management point. This action requires a sophisticated attacker. This attack is limited to the short time before the client retrieves the trusted root key from a valid management point. To reduce this risk of an attacker misdirecting clients to a rogue management point, pre-provision the clients with the trusted root key.

For more information and procedures to manage the trusted root key, see [Configure security](configure-security.md#manage-the-trusted-root-key).

## Signing and encryption

When you use PKI certificates for all client communications, you don't have to plan for signing and encryption to help secure client data communication. If you set up any site systems that run IIS to allow HTTP client connections, decide how to help secure the client communication for the site.

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

To help protect the data that clients send to management points, you can require clients to sign the data. You can also require the SHA-256 algorithm for signing. This configuration is more secure, but don't require SHA-256 unless all clients support it. Many operating systems natively support this algorithm, but older operating systems might require an update or hotfix.

While signing helps protect the data from tampering, encryption helps protect the data from information disclosure. You can enable encryption for the inventory data and state messages that clients send to management points in the site. You don't have to install any updates on clients to support this option. Clients and management points require more CPU usage for encryption and decryption.

> [!NOTE]
> To encrypt the data, the client uses the public key of the management point's encryption certificate. Only the management point has the corresponding private key, so only it can decrypt the data.
>
> The client bootstraps this certificate with the management point's signing certificate, which it bootstraps with the site's trusted root key. Make sure to securely provision the trusted root key on clients. For more information, see [The trusted root key](#the-trusted-root-key).

For more information about how to configure the settings for signing and encryption, see [Configure signing and encryption](configure-security.md#signing-and-encryption).

For more information on the cryptographic algorithms used for signing and encryption, see [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md).

## Role-based administration

With Configuration Manager, you use role-based administration to secure the access that administrative users need to use Configuration Manager. You also secure access to the objects that you manage, like collections, deployments, and sites.

With the combination of security roles, security scopes, and collections, you segregate the administrative assignments that meet your organization's requirements. Used together, they define the _administrative scope_ of a user. This administrative scope controls the objects that an administrative user views in the Configuration Manager console, and it controls the permissions that a user has on those objects.

For more information, see [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md).

## Azure Active Directory

Configuration Manager integrates with Azure Active Directory (Azure AD) to enable the site and clients to use modern authentication.

For more information about Azure AD, see [Azure Active Directory documentation](/azure/active-directory/).

Onboarding your site with Azure AD supports the following Configuration Manager scenarios:

### Client scenarios

- [Manage clients on the internet via cloud management gateway](../../clients/manage/cmg/overview.md)

- [Manage cloud domain-joined devices](../../clients/deploy/deploy-clients-cmg-azure.md)

- [Co-management](../../../comanage/overview.md)

- [Deploy user-available apps](../../../apps/plan-design/prerequisites-deploy-user-available-apps.md)

- [Microsoft Store for Business online apps](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- [Manage Microsoft 365 Apps for enterprise](../../../sum/deploy-use/manage-office-365-proplus-updates.md)

### Server scenarios

- [Desktop Analytics](../../../desktop-analytics/overview.md)

- [Tenant attach](../../../tenant-attach/device-sync-actions.md)

- [Endpoint analytics](../../../../analytics/overview.md)

- [Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm)

- [Community Hub](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)

- [User discovery](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)

## SMS Provider authentication

[!INCLUDE [SMS Provider authentication](../hierarchy/includes/sms-provider-authentication.md)]

## Next steps

- [Certificates in Configuration Manager](certificates-overview.md)

- [Plan for PKI certificates](plan-for-certificates.md)

- [Configure security](configure-security.md)

- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)
