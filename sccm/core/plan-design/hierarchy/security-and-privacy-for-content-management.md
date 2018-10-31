---
title: Content management security and privacy
titleSuffix: Configuration Manager
description: Optimize security and privacy for content management in Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Security and privacy for content management in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article contains security and privacy information for content management in Configuration Manager. 



##  <a name="BKMK_Security_ContentManagement"></a> Security best practices for content management  


#### Advantages and disadvantages of HTTPS or HTTP for intranet distribution points
For distribution points on the intranet, consider the advantages and disadvantages of using HTTPS and HTTP. In most scenarios, using HTTP and package access accounts for authorization provides more security than using HTTPS with encryption but without authorization. However, if you have sensitive data in your content that you want to encrypt during transfer, use HTTPS.  

-   **When you use HTTPS for a distribution point**, Configuration Manager doesn't use package access accounts to authorize access to the content, but the content is encrypted when it's transferred over the network.  

-   **When you use HTTP for a distribution point**, you can use package access accounts for authorization, but the content isn't encrypted when it's transferred over the network.  

Starting in version 1806, consider enabling **Enhanced HTTP** for the site. This feature allows clients to use Azure Active Directory authentication to securely communicate with an HTTP distribution point. For more information, see [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).

#### Protect the client authentication certificate file
If you use a PKI client authentication certificate rather than a self-signed certificate for the distribution point, protect the certificate file (.pfx) with a strong password. If you store the file on the network, secure the network channel when you import the file into Configuration Manager.

When you require a password to import the client authentication certificate that the distribution point uses to communicate with management points, this configuration helps to protect the certificate from an attacker. Use Server Message Block (SMB) signing or IPsec between the network location and the site server to prevent an attacker from tampering with the certificate file.  

#### Remove the distribution point role from the site server
By default, Configuration Manager setup installs a distribution point on the site server. Clients don't have to communicate directly with the site server. To reduce the attack surface, assign the distribution point role to other site systems and remove it from the site server.  

#### Secure content at the package access level
The distribution point share allows read access to all users. To restrict which users can access the content, use package access accounts when the distribution point is configured for HTTP. This configuration doesn't apply to cloud distribution points, which don't support package access accounts. For more information, see [Package access accounts](/sccm/core/plan-design/hierarchy/accounts#package-access-account).

#### Configure IIS on the distribution point role
If Configuration Manager installs IIS when you add a distribution point site system role, remove HTTP redirection or IIS Management Scripts and Tools when the distribution point installation is complete. The distribution point doesn't require HTTP redirection or IIS Management Scripts and Tools. To reduce the attack surface, remove these role services for the web server role.  For more information about the role services for the web server role for distribution points, see [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

#### Set package access permissions when you create the package
Because changes to the access accounts on the package files become effective only when you redistribute the package, set the package access permissions carefully when you first create the package. This configuration is important when the package is large or distributed to many distribution points, and when the network bandwidth capacity for content distribution is limited.  

#### Implement access controls to protect media that contains prestaged content
Prestaged content is compressed but not encrypted. An attacker could read and modify the files that are downloaded to devices. Configuration Manager clients reject content that's tampered with, but they still download it.  

#### Import prestaged content with ExtractContent
Only import prestaged content by using the ExtractContent.exe command-line tool. To avoid tampering and elevation of privileges, use only the authorized command-line tool that comes with Configuration Manager.  

#### Secure the communication channel between the site server and the package source location
Use IPsec or SMB signing between the site server and the package source location when you create applications and packages. This configuration helps to prevent an attacker from tampering with the source files.  

#### Remove default virtual directories for custom website with the distribution point role
If you change the site configuration option to use a custom website rather than the default website after installing a distribution point role, remove the default virtual directories. When you switch from the default website to a custom website, Configuration Manager doesn't remove the old virtual directories. Remove the following virtual directories that Configuration Manager originally created under the default website:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### For cloud distribution points, protect your Azure subscription details and certificates
When you use cloud distribution points, protect the following high-value items:
- The user name and password for your Azure subscription
- The Azure management certificate 
- The cloud distribution point service certificate

Store the certificates securely. If you browse to them over the network when you configure the cloud distribution point, use IPsec or SMB signing between the site system server and the source location.  

#### For service continuity, monitor the expiry date of the cloud distribution point certificates
Configuration Manager doesn't warn you when the imported certificates for the cloud distribution point are about to expire. Monitor the expiry dates independently from Configuration Manager. Make sure that you renew and then import the new certificates before the expiry date. This action is important if you acquire a server authentication certificate from an external, public provider, because you might need additional time to acquire a renewed certificate.  

 If either certificate expires, Cloud Services Manager generates the status message ID **9425**. The CloudMgr.log file contains an entry to indicate that the certificate **is in expired state**, with the expiry date also logged in UTC.  



## Security considerations for content management  

Consider the following points when planning for content management:  

-   Clients don't validate content until after it's downloaded.  

     Configuration Manager clients validate the hash on content only after it's downloaded to their client cache. If an attacker tampers with the list of files to download or with the content itself, the download process can take up considerable network bandwidth, only for the client to then discard the content when it encounters the invalid hash.  

-   When you use cloud distribution points, access to the content is automatically restricted to your enterprise. You can't restrict it further to selected users or groups.  

-   When you use cloud distribution points, clients are authenticated by the management point and then use a Configuration Manager token to access cloud distribution points. The token is valid for eight hours. This behavior means that if you block a client because it's no longer trusted, it can continue to download content from a cloud distribution point until the validity period of this token has expired. At this point, the management point won't issue another token for the client because the client is blocked.  

     To avoid a blocked client from downloading content within this eight-hour window, stop the cloud service. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Distribution Points** node.  



##  <a name="BKMK_Privacy_ContentManagement"></a> Privacy information for content management  

 Configuration Manager doesn't include any user data in content files, although an administrative user might choose to do this action.  



## See also

- [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  

- [Security and privacy for application management](/sccm/apps/plan-design/security-and-privacy-for-application-management)  

- [Security and privacy for software updates](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

- [Security and privacy for OS deployment](/sccm/osd/plan-design/security-and-privacy-for-operating-system-deployment)  