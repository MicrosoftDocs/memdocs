---
title: Plan for security
titleSuffix: Configuration Manager
description: Get best practices and other information about security in Configuration Manager.
ms.date: 05/04/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

## Plan for certificates

Configuration Manager uses a combination of self-signed and public key infrastructure (PKI) digital certificates. Use PKI certificates whenever possible. Some scenarios require PKI certificates. When PKI certificates aren't available, the site automatically generates self-signed certificates. Some scenarios always use self-signed certificates.

For more information, see [Plan for certificates](plan-for-certificates.md).

##  <a name="BKMK_PlanningForRTK"></a> Plan for the trusted root key  

The Configuration Manager trusted root key provides a mechanism for Configuration Manager clients to verify site systems belong to their hierarchy. Every site server generates a site exchange key to communicate with other sites. The site exchange key from the top-level site in the hierarchy is called the trusted root key.  

The function of the trusted root key in Configuration Manager resembles a root certificate in a public key infrastructure. Anything signed by the private key of the trusted root key is trusted further down the hierarchy. Clients store a copy of the site's trusted root key in the **root\ccm\locationservices** WMI namespace. 

For example, the site issues a certificate to the management point, which it signs with the private key of the trusted root key. The site shares with clients the public key of its trusted root key. Then clients can differentiate between management points that are in their hierarchy and management points that aren't in their hierarchy.   

Clients automatically retrieve the public copy of the trusted root key by using two mechanisms:  

- You extend the Active Directory schema for Configuration Manager, and publish the site to Active Directory Domain Services. Then clients retrieve this site information from a global catalog server. For more information, see [Prepare Active Directory for site publishing](../network/extend-the-active-directory-schema.md).  

- When you install clients using the client push installation method. For more information, see [Client push installation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

If clients can't retrieve the trusted root key by using one of these mechanisms, they trust the trusted root key that's provided by the first management point that they communicate with. In this scenario, a client might be misdirected to an attacker's management point where it would receive policy from the rogue management point. This action requires a sophisticated attacker. This attack is limited to the short time before the client retrieves the trusted root key from a valid management point. To reduce this risk of an attacker misdirecting clients to a rogue management point, pre-provision the clients with the trusted root key.  

Use the following procedures to pre-provision and verify the trusted root key for a Configuration Manager client:  

- [Pre-provision a client with the trusted root key by using a file](#bkmk_trk-provision-file)  

- [Pre-provision a client with the trusted root key without using a file](#bkmk_trk-provision-nofile)  

- [Verify the trusted root key on a client](#bkmk_trk-verify)  

- [Remove or replace the trusted root key](#bkmk_trk-reset)  

  > [!NOTE]  
  > If clients can get the trusted root key from Active Directory Domain Services or client push, you don't have to pre-provision it. 
  > 
  > When clients use HTTPS communication to management points, you don't have to pre-provision the trusted root key. They establish trust by the PKI certificates.  


### <a name="bkmk_trk-provision-file"></a> Pre-provision a client with the trusted root key by using a file  

1.  On the site server, open the following file in a text editor: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Locate the entry, **SMSPublicRootKey=**. Copy the key from that line, and close the file without any changes.  

3.  Create a new text file, and paste the key information that you copied from the mobileclient.tcf file.  

4.  Save the file in a location where all computers can access it, but where the file is safe from tampering.  

5.  Install the client by using any installation method that accepts client.msi properties. Specify the following property: `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > When you specify the trusted root key during client installation, also specify the site code. Use the following client.msi property: `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-provision-nofile"></a> Pre-provision a client with the trusted root key without using a file  

1.  On the site server, open the following file in a text editor: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Locate the entry, **SMSPublicRootKey=**. Copy the key from that line, and close the file without any changes.  

3.  Install the client by using any installation method that accepts client.msi properties. Specify the following client.msi property: `SMSPublicRootKey=<key>` where `<key>` is the string that you copied from mobileclient.tcf.  

    > [!IMPORTANT]  
    >  When you specify the trusted root key during client installation, also specify the site code. Use the following client.msi property: `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-verify"></a> Verify the trusted root key on a client  

1. Open a Windows PowerShell console as an administrator.  

2. Run the following command:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

The returned string is the trusted root key. Verify that it matches the **SMSPublicRootKey** value in the mobileclient.tcf file on the site server.  


### <a name="bkmk_trk-reset"></a> Remove or replace the trusted root key  

Remove the trusted root key from a client by using the client.msi property, **RESETKEYINFORMATION = TRUE**. 

To replace the trusted root key, reinstall the client together with the new trusted root key. For example, use client push, or specify the client.msi property **SMSPublicRootKey**.  

For more information on these installation properties, see [About client installation parameters and properties](../../clients/deploy/about-client-installation-properties.md).



##  <a name="BKMK_PlanningForSigningEncryption"></a> Plan for signing and encryption  
 
When you use PKI certificates for all client communications, you don't have to plan for signing and encryption to help secure client data communication. If you set up any site systems that run IIS to allow HTTP client connections, decide how to help secure the client communication for the site.  

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

To help protect the data that clients send to management points, you can require clients to sign the data. You can also require the SHA-256 algorithm for signing. This configuration is more secure, but don't require SHA-256 unless all clients support it. Many operating systems natively support this algorithm, but older operating systems might require an update or hotfix. 

While signing helps protect the data from tampering, encryption helps protect the data from information disclosure. You can enable 3DES encryption for the inventory data and state messages that clients send to management points in the site. You don't have to install any updates on clients to support this option. Clients and management points require additional CPU usage for encryption and decryption.  

For more information about how to configure the settings for signing and encryption, see [Configure signing and encryption](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="BKMK_PlanningForRBA"></a> Plan for role-based administration  

For more information, see [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="bkmk_planazuread"></a> Plan for Azure Active Directory

Configuration Manager integrates with Azure Active Directory (Azure AD) to enable the site and clients to use modern authentication. Onboarding your site with Azure AD supports the following Configuration Manager scenarios:

**Client**  

- [Manage clients on the internet via cloud management gateway](../../clients/manage/cmg/overview.md)  

- [Manage cloud domain-joined devices](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Co-management](../../../comanage/overview.md)  

- [Deploy user-available apps](../../../apps/plan-design/prerequisites-deploy-user-available-apps.md)

- [Microsoft Store for Business online apps](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- [Manage Microsoft 365 Apps for enterprise](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Server**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- [Community Hub](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Cloud distribution point](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [User discovery](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


For more information on connecting your site to Azure AD, see [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md).


For more information about Azure AD, see [Azure Active Directory documentation](/azure/active-directory/).



## <a name="bkmk_auth"></a> Plan for SMS Provider authentication
<!--1357013-->

You can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. It applies to all components that access the SMS Provider. For example, the Configuration Manager console, SDK methods, and Windows PowerShell cmdlets.

This configuration is a hierarchy-wide setting. Before you change this setting, make sure that all Configuration Manager administrators can sign in to Windows with the required authentication level.

The following levels are available:

- **Windows authentication**: Require authentication with Active Directory domain credentials.

- **Certificate authentication**: Require authentication with a valid certificate that's issued by a trusted PKI certificate authority.  

- **Windows Hello for Business authentication**: Require authentication with strong two-factor authentication that's tied to a device and uses biometrics or a PIN.  

For more information, see [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).

## See also

- [Security and privacy for Configuration Manager clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)

- [Configure security](configure-security.md)

- [Communication between endpoints](../hierarchy/communications-between-endpoints.md)

- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)

- [PKI certificate requirements](../network/pki-certificate-requirements.md)
