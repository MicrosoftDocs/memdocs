---
title: Configure security
titleSuffix: Configuration Manager
description: Configure security-related options for Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configure security in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the information in this article to help you set up security-related options for Configuration Manager. It covers the following security options:
- [Client computer communication](#BKMK_ConfigureClientPKI) for client PKI certificates  
- [Signing and encryption](#BKMK_ConfigureSigningEncryption)  
- [Role-based administration](#BKMK_ConfigureRBA)  
- [Manage accounts](#BKMK_ManageAccounts)  
- [Configure Azure Active Directory](#bkmk_azuread)  



##  <a name="BKMK_ConfigureClientPKI"></a> Configure settings for client PKI certificates  

If you want to use public key infrastructure (PKI) certificates for client connections to site systems that use Internet Information Services (IIS), use the following procedure to configure settings for these certificates.  

#### To configure client PKI certificate settings  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the primary site to configure.  

2.  In the ribbon, choose **Properties**. Then switch to the **Client Computer Communication** tab.  

    This tab is available on a primary site only. If you don't see the **Client Computer Communication** tab, make sure that you're not connected to a central administration site or a secondary site.  

3.  Select the settings for site systems that use IIS.  

    - **HTTPS only**: Clients that are assigned to the site always use a client PKI certificate when they connect to site systems that use IIS.  

    - **HTTPS or HTTP**: You don't require clients to use PKI certificates.  

    - **Use Configuration Manager-generated certificates for HTTP site systems**: For more information on this setting, see [Enhanced HTTP](#bkmk_ehttp).  

4.  Select the settings for client computers.  

    - **Use client PKI certificate (client authentication capability) when available**: If you chose the **HTTPS or HTTP** site server setting, choose this option to use a client PKI certificate for HTTP connections. The client uses this certificate instead of a self-signed certificate to authenticate itself to site systems. If you chose **HTTPS only**, this option is automatically chosen.  

    When more than one valid PKI client certificate is available on a client, choose **Modify** to configure the client certificate selection methods.  

    For more information about the client certificate selection method, see [Planning for PKI client certificate selection](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForClientCertificateSelection).  

    - **Clients check the certificate revocation list (CRL) for site systems**: Enable this setting for clients to check your organization's CRL for revoked certificates.  

    For more information about CRL checking for clients, see [Planning for PKI certificate revocation](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).  

5.  To import, view, and delete the certificates for trusted root certification authorities, choose **Set**.  

    For more information, see [Planning for the PKI trusted root certificates and the certificate issuers List](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRootCAs).  


Repeat this procedure for all primary sites in the hierarchy.  



##  <a name="BKMK_ConfigureSigningEncryption"></a> Configure signing and encryption  

Configure the most secure signing and encryption settings for site systems that all clients in the site can support. These settings are especially important when you let clients communicate with site systems by using self-signed certificates over HTTP.  

#### To configure signing and encryption for a site  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the primary site to configure.  

2.  In the ribbon, select **Properties**, and then switch to the **Signing and Encryption** tab.  

    This tab is available on a primary site only. If you don't see the **Signing and Encryption** tab, make sure that you're not connected to a central administration site or a secondary site.  

3.  Configure the signing and encryption options for clients to communicate with the site.  

    - **Require signing**: Clients sign data before sending to the management point.  

    - **Require SHA-256**: Clients use the SHA-256 algorithm when signing data.  

    > [!WARNING]  
    >  Don't **Require SHA-256** without first confirming that all clients support this hash algorithm. These clients include ones that might be assigned to the site in the future.  
    >   
    >  If you choose this option, and clients with self-signed certificates can't support SHA-256, Configuration Manager rejects them. The SMS_MP_CONTROL_MANAGER component logs the message ID 5443.  

    - **Use encryption**: Clients encrypt client inventory data and status messages before sending to the management point. They use the 3DES algorithm.  

Repeat this procedure for all primary sites in the hierarchy.  



##  <a name="BKMK_ConfigureRBA"></a> Configure role-based administration  

Role-based administration combines security roles, security scopes, and assigned collections to define the administrative scope for each administrative user. A scope includes the objects that a user can view in the console, and the tasks related to those objects that they have permission to do. Role-based administration configurations are applied at each site in a hierarchy.  

For more information, see [Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration). This article details the following actions:  

- Create custom security roles  

- Configure security roles  

- Configure security scopes for an object  

- Configure collections to manage security  

- Create a new administrative user  

- Modify the administrative scope of an administrative user  

> [!IMPORTANT]  
>  Your own administrative scope defines the objects and settings that you can assign when you configure role-based administration for another administrative user. For information about planning for role-based administration, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).  



##  <a name="BKMK_ManageAccounts"></a> Manage accounts that Configuration Manager uses  

Configuration Manager supports Windows accounts for many different tasks and uses. To view accounts that are configured for different tasks, and to manage the password that Configuration Manager uses for each account, use the following procedure:  

#### To manage accounts that Configuration Manager uses  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Security**, and then choose the **Accounts** node.  

2.  To change the password for an account, select the account in the list. Then choose **Properties** in the ribbon.  

3.  Choose **Set** to open the **Windows User Account** dialog box. Specify the new password for Configuration Manager to use for this account.  

    > [!NOTE]  
    >  The password that you specify must match this account's password in Active Directory.  

For more information, see [Accounts used in Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).



##  <a name="bkmk_azuread"></a> Configure Azure Active Directory

Integrate Configuration Manager with Azure Active Directory (Azure AD) to simplify and cloud-enable your environment. Enable the site and clients to authenticate by using Azure AD. For more information, see the **Cloud Management** service in [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard).



## See also

- [Plan for security](/sccm/core/plan-design/security/plan-for-security)  

- [Security and privacy for Configuration Manager clients](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Communication between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Cryptographic controls technical reference](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements)  
