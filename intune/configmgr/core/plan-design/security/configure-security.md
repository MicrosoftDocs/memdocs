---
title: Configure security
titleSuffix: Configuration Manager
description: How to configure security-related options for Configuration Manager.
ms.date: 12/21/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configure security in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the information in this article to help you set up security-related options for Configuration Manager. Before you start, make sure you have a [Plan for security](plan-for-security.md).

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

## Client PKI certificates

If you want to use public key infrastructure (PKI) certificates for client connections to site systems that use Internet Information Services (IIS), use the following procedure to configure settings for these certificates.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the primary site to configure.

1. In the ribbon, choose **Properties**. Then switch to the **Communication Security** tab.

1. Select the settings for site systems that use IIS.

    - **HTTPS only**: Clients that are assigned to the site always use a client PKI certificate when they connect to site systems that use IIS. For example, a management point and distribution point.

    - **HTTPS or HTTP**: You don't require clients to use PKI certificates.

    - **Use Configuration Manager-generated certificates for HTTP site systems**: For more information on this setting, see [Enhanced HTTP](../hierarchy/enhanced-http.md).

1. Select the settings for client computers.

    - **Use client PKI certificate (client authentication capability) when available**: If you chose the **HTTPS or HTTP** site server setting, choose this option to use a client PKI certificate for HTTP connections. The client uses this certificate instead of a self-signed certificate to authenticate itself to site systems. If you chose **HTTPS only**, this option is automatically chosen.

        When more than one valid PKI client certificate is available on a client, select **Modify** to configure the client certificate selection methods. For more information about the client certificate selection method, see [Planning for PKI client certificate selection](plan-for-certificates.md#pki-client-certificate-selection).

    - **Clients check the certificate revocation list (CRL) for site systems**: Enable this setting for clients to check your organization's CRL for revoked certificates. For more information about CRL checking for clients, see [Planning for PKI certificate revocation](plan-for-certificates.md#pki-certificate-revocation).

1. To import, view, and delete the certificates for trusted root certification authorities, select **Set**. For more information, see [Planning for the PKI trusted root certificates and the certificate issuers List](plan-for-certificates.md#pki-trusted-root-certificates).

Repeat this procedure for all primary sites in the hierarchy.

## Manage the trusted root key

Use these procedures to pre-provision and verify the trusted root key for a Configuration Manager client.

> [!NOTE]
> If clients can get the trusted root key from Active Directory Domain Services or client push, you don't have to pre-provision it.
>
> When clients use HTTPS communication to management points, you don't have to pre-provision the trusted root key. They establish trust by the PKI certificates.

For more information on the trusted root key, see [Plan for security](plan-for-security.md#the-trusted-root-key).

### Pre-provision a client with the trusted root key by using a file

1. On the site server, browse to the Configuration Manager installation directory. In the `\bin\<platform>` subfolder, open the following file in a text editor: `mobileclient.tcf`

1. Locate the entry, `SMSPublicRootKey`. Copy the value from that line, and close the file without saving any changes.

1. Create a new text file, and paste the key value that you copied from the mobileclient.tcf file.

1. Save the file in a location where all computers can access it, but where the file is safe from tampering.

1. Install the client by using any installation method that accepts client.msi properties. Specify the following property: `SMSROOTKEYPATH=<full path and file name>`

    > [!IMPORTANT]
    > When you specify the trusted root key during client installation, also specify the site code. Use the following client.msi property: `SMSSITECODE=<site code>`

### Pre-provision a client with the trusted root key without using a file

1. On the site server, browse to the Configuration Manager installation directory. In the `\bin\<platform>` subfolder, open the following file in a text editor: `mobileclient.tcf`

1. Locate the entry, `SMSPublicRootKey`. Copy the value from that line, and close the file without saving any changes.

1. Install the client by using any installation method that accepts client.msi properties. Specify the following client.msi property: `SMSPublicRootKey=<key>` where `<key>` is the string that you copied from mobileclient.tcf.

    > [!IMPORTANT]
    >  When you specify the trusted root key during client installation, also specify the site code. Use the following client.msi property: `SMSSITECODE=<site code>`

### Verify the trusted root key on a client

1. Open a Windows PowerShell console as an administrator.

1. Run the following command:

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

The returned string is the trusted root key. Verify that it matches the **SMSPublicRootKey** value in the mobileclient.tcf file on the site server.

### Remove or replace the trusted root key

Remove the trusted root key from a client by using the client.msi property, `RESETKEYINFORMATION = TRUE`.

To replace the trusted root key, reinstall the client together with the new trusted root key. For example, use client push, or specify the client.msi property **SMSPublicRootKey**.

For more information on these installation properties, see [About client installation parameters and properties](../../clients/deploy/about-client-installation-properties.md).

## Signing and encryption

Configure the most secure signing and encryption settings for site systems that all clients in the site can support. These settings are especially important when you let clients communicate with site systems by using self-signed certificates over HTTP.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the primary site to configure.

1. In the ribbon, select **Properties**, and then switch to the **Signing and Encryption** tab.

    This tab is available on a primary site only. If you don't see the **Signing and Encryption** tab, make sure that you're not connected to a central administration site or a secondary site.

1. Configure the signing and encryption options for clients to communicate with the site.

    - **Require signing**: Clients sign data before sending to the management point.

    - **Require SHA-256**: Clients use the SHA-256 algorithm when signing data.

        > [!WARNING]
        > Don't **Require SHA-256** without first confirming that all clients support this hash algorithm. These clients include ones that might be assigned to the site in the future.
        >
        > If you choose this option, and clients with self-signed certificates can't support SHA-256, Configuration Manager rejects them. The SMS_MP_CONTROL_MANAGER component logs the message ID 5443.

    - **Use encryption**: Clients encrypt client inventory data and status messages before sending to the management point.

Repeat this procedure for all primary sites in the hierarchy.

## Role-based administration

Role-based administration combines security roles, security scopes, and assigned collections to define the administrative scope for each administrative user. A scope includes the objects that a user can view in the console, and the tasks related to those objects that they have permission to do. Role-based administration configurations are applied at each site in a hierarchy.

For more information, see [Configure role-based administration](../../servers/deploy/configure/configure-role-based-administration.md). This article details the following actions:

- Create custom security roles

- Configure security roles

- Configure security scopes for an object

- Configure collections to manage security

- Create a new administrative user

- Modify the administrative scope of an administrative user

> [!IMPORTANT]
> Your own administrative scope defines the objects and settings that you can assign when you configure role-based administration for another administrative user. For information about planning for role-based administration, see [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md).

## Manage accounts

Configuration Manager supports Windows accounts for many different tasks and uses. To view accounts that are configured for different tasks, and to manage the password that Configuration Manager uses for each account, use the following procedure:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Security**, and then choose the **Accounts** node.

1. To change the password for an account, select the account in the list. Then choose **Properties** in the ribbon.

1. Choose **Set** to open the **Windows User Account** dialog box. Specify the new password for Configuration Manager to use for this account.

    > [!NOTE]
    > The password that you specify must match this account's password in Active Directory.

For more information, see [Accounts used in Configuration Manager](../hierarchy/accounts.md).

<a name='azure-active-directory'></a>

## Microsoft Entra ID

Integrate Configuration Manager with Microsoft Entra ID to simplify and cloud-enable your environment. Enable the site and clients to authenticate by using Microsoft Entra ID.

For more information, see the **Cloud Management** service in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md).

## SMS Provider authentication

<!--1357013-->
You can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level before they can access Configuration Manager. For more information, see [Plan for SMS Provider authentication](plan-for-security.md#sms-provider-authentication).

> [!IMPORTANT]
> This configuration is a hierarchy-wide setting. Before you change this setting, make sure that all Configuration Manager administrators can sign in to Windows with the required authentication level.

To configure this setting, use the following steps:

1. First sign in to Windows with the intended authentication level.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select **Hierarchy Settings** in the ribbon.

1. Switch to the **Authentication** tab. Select the desired [authentication level](plan-for-security.md#sms-provider-authentication), and then select **OK**.

    - Only when necessary, select **Add** to exclude specific users or groups. For more information, see [Exclusions](#exclusions).

### Exclusions

From the **Authentication** tab of Hierarchy Settings, you can also exclude certain users or groups. Use this option sparingly. For example, when specific users require access to the Configuration Manager console, but can't authenticate to Windows at the required level. It may also be necessary for automation or services that run under the context of a system account.

## Next steps

- [How to enable TLS 1.2](enable-tls-1-2.md)

- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)  

- [Communication between endpoints](../hierarchy/communications-between-endpoints.md)  
