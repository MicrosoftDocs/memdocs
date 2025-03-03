---
title: CMG server authentication certificate
titleSuffix: Configuration Manager
description: The CMG uses HTTPS for secure client communication over the public internet. You can get a certificate from a public provider, or issue one from your public key infrastructure (PKI).
ms.date: 04/08/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# CMG server authentication certificate

*Applies to: Configuration Manager (current branch)*

The first step when you set up a cloud management gateway (CMG) is to get the server authentication certificate. The CMG creates an HTTPS service to which internet-based clients connect. The server requires a server authentication certificate to build the secure channel. You can acquire a certificate for this purpose from a public provider, or issue it from your public key infrastructure (PKI).

When you create the CMG in the Configuration Manager console, you provide this certificate. The common name (CN) of this certificate defines the service name of the CMG.

> [!NOTE]
> You may need additional certificates for clients and management points. These certificates are covered in the third step of the CMG setup process, [Configure client authentication](configure-authentication.md).

A reminder of some CMG terminology that's used in this article:

- **Service name**: The common name (CN) of the CMG server authentication certificate. Clients and the CMG connection point site system role communicate with this service name. For example, `GraniteFalls.contoso.com` or `GraniteFalls.WestUS.CloudApp.Azure.Com`.

- **Deployment name**: The first part of the service name plus the Azure location for the cloud service deployment. The cloud service manager component of the service connection point uses this name when it deploys the CMG in Azure. The deployment name is always in an Azure domain. The Azure location depends upon the deployment method, for example:

  - Virtual machine scale set: `GraniteFalls.WestUS.CloudApp.Azure.Com`
  - Classic deployment: `GraniteFalls.CloudApp.Net`

  > [!IMPORTANT]
  > This article uses examples with a virtual machine scale set as the recommended deployment method in version 2107 and later. If you use a classic deployment, note the difference as you read this article and prepare the server authentication certificate.

## Choose the certificate type

First, decide where you want to get the certificate. There are several factors to consider.

Clients must trust the CMG server authentication certificate to establish the HTTPS channel with the CMG service. There are two methods to accomplish this trust:

1. Use a certificate from a public and globally trusted certificate provider.<!-- memdocs#1668 -->

    - Windows clients include trusted root certificate authorities (CAs) from these providers. By using a certificate issued by one of these providers, your clients automatically trust it.

    - There's a cost associated with this certificate, which is specific to the provider.

1. Use a certificate issued by an enterprise CA from your public key infrastructure (PKI).

    - Most enterprise PKI implementations add the trusted root CAs to Windows clients. For example, if you use Active Directory Certificate Services with group policy. If you issue the CMG server authentication certificate from a CA that your clients don't automatically trust, add the CA trusted root certificate to internet-based clients.

      If you plan to [install the Configuration Manager client from Intune](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client), you can also use Intune certificate profiles to provision certificates on clients. For more information, see [Configure a certificate profile](../../../../../intune-service/protect/certificates-configure.md).

    - Your organization may have an internal cost to issue certificates, but there are generally no external costs associated with this certificate.

> [!IMPORTANT]
> Before you get this certificate, make sure the service name is globally unique for the cloud service and storage account. Also make sure the name uses supported characters. For more information, see [Globally unique name](#globally-unique-name).

### Summary comparison of certificate types

|  | Public provider | Enterprise PKI |
|---------|---------|---------|
| **Client trust** | Trusted in Windows by default | Automatic with some implementations, otherwise need to deploy |
| **Cost** | Yes | Not typical |
| **Service name example** | `GraniteFalls.contoso.com` | `GraniteFalls.contoso.com` or `GraniteFalls.WestUS.CloudApp.Azure.Com`|
| **DNS CNAME required** | Yes | No for Azure domain service name (`GraniteFalls.WestUS.CloudApp.Azure.Com`) |

> [!NOTE]
> The CMG server authentication certificate supports wildcards. Some certificate authorities issue certificates using a wildcard character for the service name prefix. For example, `*.contoso.com`. Some organizations use wildcard certificates to simplify their PKI and reduce maintenance costs.<!--491233-->
>
> For more information on how to use a wildcard certificate with a CMG, see [Set up a CMG](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->

## Globally unique name

This certificate requires a globally unique name to identify the service in Azure. Before you request a certificate, confirm that the Azure _deployment name_ you want is unique. For example, `GraniteFalls.WestUS.CloudApp.Azure.Com`.

### Virtual machine scale set

1. Sign in to the [Azure portal](https://portal.azure.com).

1. From the Azure portal home page, select **Create a resource** under Azure services.

1. Search for **Virtual machine scale set**. Select **Create**.

1. Select the **Subscription** and **Resource group** that you'll use for the CMG.

1. In the **Virtual machine scale set name** field, type the prefix that you want. For example, `GraniteFalls`.

1. Select the **Region** that you'll use for the CMG. For example, **(US) West US**.

The interface reflects whether the domain name is available or already in use by another service.

> [!IMPORTANT]
> Don't create the service in the portal, just use this process to check the name availability.

Repeat this process for the **Key Vault** resource. The virtual machine scale set deployment creates a key vault with the same name, which also needs to be globally unique.<!-- memdocs#1883 -->

### Content-enabled CMG storage account

If you also enable the CMG for content, confirm that it's also a unique Azure storage account name. If the CMG deployment name is unique, but the storage account isn't, Configuration Manager fails to provision the service in Azure. Repeat the above process in the Azure portal with the following changes:

- Search for **Storage account**.

- Test your name in the **Storage account name** field.

> [!IMPORTANT]
> The DNS name prefix should be 3 to 24 characters long, and contain numbers and lowercase letters only. Don't use special characters, like a dash (`-`). For example: `granitefalls`.<!-- SCCMDocs#1080, MEMDocs#1910 -->

## Issue the certificate

The CMG server authentication certificate supports the following configurations:

- 2048-bit or 4096-bit key length

- This certificate supports key storage providers for certificate private keys (v3). For more information, see [CNG v3 certificates overview](../../../plan-design/network/cng-certificates-overview.md).

### Use a public provider certificate

A third-party certificate provider can't create a certificate for an Azure domain like `cloudapp.azure.com`, because Microsoft owns those domains. You can only get a certificate issued for a domain you own. The main reason for acquiring a certificate from a third-party provider is that your clients already trust that provider's root certificate.

The specific process to get this certificate varies by provider. For more information, contact your third-party certificate provider.

For the web server certificate common name (CN):

- You've made sure the _deployment name_ is [globally unique](#globally-unique-name) in Azure for the cloud service and storage account. For example, `GraniteFalls.WestUS.CloudApp.Azure.Com`.

- To determine the _service name_, append the _deployment name_ prefix (`GraniteFalls`) to your organization's domain name (`contoso.com`).

- Use this _service name_ for the certificate common name (CN). For example, `GraniteFalls.contoso.com`.

Next, you need to [create a DNS CNAME alias](#create-a-dns-cname-alias).

### Use an enterprise PKI certificate

Issuing a web server certificate from your organization's PKI varies by product. The instructions for [Deploying the service certificate for cloud-based distribution points](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) are for Active Directory Certificate Services. This process generally applies for the CMG server authentication certificate.

For the web server certificate common name (CN):

- You've made sure the _deployment name_ is [globally unique](#globally-unique-name) in Azure for the cloud service and storage account. For example, `GraniteFalls.WestUS.CloudApp.Azure.Com`.

- To determine the _service name_, you have two options:

  - Use your domain name (recommended). Append the _deployment name_ prefix (`GraniteFalls`) to your organization's domain name (`contoso.com`). For example, `GraniteFalls.contoso.com`. For this option, you also need to [create a DNS CNAME alias](#create-a-dns-cname-alias).

  - Use the Azure deployment name. This option doesn't require a DNS CNAME alias. For example:

    - For the Azure public cloud: `GraniteFalls.WestUS.CloudApp.Azure.Com`.

    - For the Azure US Government cloud: `GraniteFalls.usgovcloudapp.net`.

    > [!NOTE]
    > If the Azure deployment name changes, you'll need to redeploy the service to change this service name. For example, if your service name is in the `cloudapp.net` domain, you can't convert the classic cloud service CMG to a virtual machine scale set. If you use your domain name for the CMG service name, then you can update the DNS CNAME for the new deployment name.<!-- 10362079 -->

- Use this _service name_ for the certificate common name (CN).

## Create a DNS CNAME alias

If the CMG service name uses your organization's domain name (`GraniteFalls.contoso.com`), you need to create a DNS canonical name record (CNAME). This alias maps the _service name_ to the _deployment name_.

Create a CNAME record in your organization's public DNS. The CMG service in Azure and all clients that use it need to resolve the service name. For example:

- Contoso names their CMG **GraniteFalls**.

- The deployment name in Azure is `GraniteFalls.WestUS.CloudApp.Azure.Com`.

- In Contoso's public DNS `contoso.com` namespace, the DNS administrator creates a new CNAME record for the service name `GraniteFalls.contoso.com` to the Azure deployment name, `GraniteFalls.WestUS.CloudApp.Azure.Com`.

When you create the CMG, while the certificate has `GraniteFalls.contoso.com` as the CN, Configuration Manager only extracts the service name prefix, for example: **GraniteFalls**. It appends this prefix to the Azure service domain (`cloudapp.azure.com`) with the region (`westus`) to create the deployment name. For example, `GraniteFalls.WestUS.CloudApp.Azure.Com`. The CNAME alias in the DNS namespace for your domain (`contoso.com`) maps together these two FQDNs.

The Configuration Manager client policy includes the CMG service name, `GraniteFalls.contoso.com`. The client resolves the service name via the CNAME alias to the deployment name, `GraniteFalls.WestUS.CloudApp.Azure.Com`. It then can resolve the IP address of the deployment name to communicate with the service in Azure.<!--SCCMDocs issue #565-->

## Next steps

Continue your CMG setup by configuring Microsoft Entra ID:
  
> [!div class="nextstepaction"]
> [Configure Microsoft Entra ID](configure-azure-ad.md)
