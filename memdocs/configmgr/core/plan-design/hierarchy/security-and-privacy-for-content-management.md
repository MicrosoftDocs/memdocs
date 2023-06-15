---
title: Content management security and privacy
titleSuffix: Configuration Manager
description: Optimize security and privacy for content management in Configuration Manager.
ms.date: 07/15/2021
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

# Security and privacy for content management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article contains security and privacy information for content management in Configuration Manager.

## Security guidance

### Advantages and disadvantages of HTTPS or HTTP for intranet distribution points

For distribution points on the intranet, consider the advantages and disadvantages of using HTTPS or HTTP. In most scenarios, using HTTP and [package access accounts](accounts.md#package-access-account) for authorization provides more security than using HTTPS with encryption but without authorization. However, if you have sensitive data in your content that you want to encrypt during transfer, use HTTPS.

- When you use _HTTPS_ for a distribution point: Configuration Manager doesn't use package access accounts to authorize access to the content. The content is encrypted when it's transferred over the network.

- When you use _HTTP_ for a distribution point: You can use package access accounts for authorization. The content isn't encrypted when it's transferred over the network.

Consider enabling **Enhanced HTTP** for the site. This feature allows clients to use Azure Active Directory (Azure AD) authentication to securely communicate with an HTTP distribution point. For more information, see [Enhanced HTTP](enhanced-http.md).

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

### Protect the client authentication certificate file

If you use a PKI client authentication certificate rather than a self-signed certificate for the distribution point, protect the certificate file (.pfx) with a strong password. If you store the file on the network, secure the network channel when you import the file into Configuration Manager.

When you require a password to import the client authentication certificate that the distribution point uses to communicate with management points, this configuration helps to protect the certificate from an attacker. To prevent an attacker from tampering with the certificate file, use server message block (SMB) signing or IPsec between the network location and the site server.

### Remove the distribution point role from the site server

By default, Configuration Manager setup installs a distribution point on the site server. Clients don't have to communicate directly with the site server. To reduce the attack surface, assign the distribution point role to other site systems and remove it from the site server.

### Secure content at the package access level

The distribution point share allows read access to all users. To restrict which users can access the content, use package access accounts when the distribution point is configured for HTTP. This configuration doesn't apply to content-enabled cloud management gateways, which don't support package access accounts.

For more information, see [Package access accounts](accounts.md#package-access-account).

### Configure IIS on the distribution point role

If Configuration Manager installs IIS when you add a distribution point site system role, remove **HTTP redirection** and **IIS Management Scripts and Tools** when the distribution point installation is complete. The distribution point doesn't require these components. To reduce the attack surface, remove these role services for the web server role.

For more information about the role services for the web server role for distribution points, see [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md#distribution-point).

### Set package access permissions when you create the package

Because changes to the access accounts on the package files become effective only when you redistribute the package, set the package access permissions carefully when you first create the package. This configuration is important when the package is large or distributed to many distribution points, and when the network bandwidth capacity for content distribution is limited.

### Implement access controls to protect media that contains prestaged content

[Prestaged content](manage-network-bandwidth.md#BKMK_PrestagingContent) is compressed but not encrypted. An attacker could read and modify the files that are downloaded to devices. Configuration Manager clients reject content that's tampered with, but they still download it.

### Import prestaged content with ExtractContent

Only import prestaged content by using the ExtractContent.exe command-line tool. To avoid tampering and elevation of privileges, use only the authorized command-line tool that comes with Configuration Manager.

For more information, see [Deploy and manage content](../../servers/deploy/configure/deploy-and-manage-content.md#BKMK_ExportContentFromPrestagedContentFile).

### Secure the communication channel between the site server and the package source location

Use IPsec or SMB signing between the site server and the package source location when you create applications, package, and other objects with content. This configuration helps to prevent an attacker from tampering with the source files.

### Remove default virtual directories for custom website with the distribution point role

If you change the site configuration option to use a custom website rather than the default website after installing a distribution point role, remove the default virtual directories. When you switch from the default website to a custom website, Configuration Manager doesn't remove the old virtual directories. Remove the following virtual directories that Configuration Manager originally created under the default website:

- `SMS_DP_SMSPKG$`

- `SMS_DP_SMSSIG$`

- `NOCERT_SMS_DP_SMSPKG$`

- `NOCERT_SMS_DP_SMSSIG$`

For more information about using a custom website, see [Websites for site system servers](../network/websites-for-site-system-servers.md).

### For content-enabled cloud management gateways, protect your Azure subscription details and certificates

When you use content-enabled cloud management gateways (CMGs), protect the following high-value items:

- The user name and password for your Azure subscription
- The secret keys for Azure app registrations
- The server authentication certificate

Store the certificates securely. If you browse to them over the network when you configure the CMG, use IPsec or SMB signing between the site system server and the source location.

### For service continuity, monitor the expiry date of the CMG certificates

Configuration Manager doesn't warn you when the imported certificates for the CMG are about to expire. Monitor the expiry dates independently from Configuration Manager. Make sure that you renew and then import the new certificates before the expiry date. This action is important if you acquire a server authentication certificate from an external, public provider, because you might need more time to acquire a renewed certificate.

If a certificate expires, the Configuration Manager cloud services manager generates a status message with ID **9425**. The CloudMgr.log file contains an entry to indicate that the certificate _is in expired state_, with the expiry date also logged in UTC.

## Security considerations

- Clients don't validate content until after it's downloaded. Configuration Manager clients validate the hash on content only after it's downloaded to their client cache. If an attacker tampers with the list of files to download or with the content itself, the download process can take up considerable network bandwidth. Then the client discards the content when it finds the invalid hash.

- When you use content-enabled cloud management gateways:

  - It automatically restricts access to the content to your organization. You can't restrict it further to selected users or groups.

  - The management point first authenticates the client. Then the client uses a Configuration Manager token to access cloud storage. The token is valid for eight hours. This behavior means that if you block a client because it's no longer trusted, it can continue to download content from cloud storage until this token expires. The management point won't issue another token for the client because it's blocked.

    To avoid a blocked client from downloading content within this eight-hour window, stop the cloud service. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.

## Privacy information

Configuration Manager doesn't include any user data in content files, although an administrative user might choose to do this action.

## Next steps

- [Fundamental concepts for content management](fundamental-concepts-for-content-management.md)

- [Security and privacy for application management](../../../apps/plan-design/security-and-privacy-for-application-management.md)

- [Security and privacy for software updates](../../../sum/plan-design/security-and-privacy-for-software-updates.md)

- [Security and privacy for OS deployment](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)
