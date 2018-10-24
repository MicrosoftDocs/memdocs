---
title: CMG Certificates
description: Learn about the different digital certificates to use with the cloud management gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/24/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
---

# Certificates for the cloud management gateway

*Applies to: System Center Configuration Manager (Current Branch)*

Depending upon the scenario you use to manage clients on the internet with the cloud management gateway (CMG), you need one or more of the following digital certificates:  

- [CMG server authentication certificate](#bkmk_serverauth)  
    - [CMG trusted root certificate to clients](#bkmk_cmgroot)  
    - [Server authentication certificate issued by public provider](#bkmk_serverauthpublic)  
    - [Server authentication certificate issued from enterprise PKI](#bkmk_serverauthpki)  

- [Azure management certificate](#bkmk_azuremgmt)  

- [Client authentication certificate](#bkmk_clientauth)  
    - [Client trusted root certificate to CMG](#bkmk_clientroot)  

- [Enable management point for HTTPS](#bkmk_mphttps)  


For more information about the different scenarios, see [plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


### General information
<!--SCCMDocs issue #779-->
Certificates for the cloud management gateway support the following configurations:  

- **4096-bit key length**  

- Starting in version 1710, support for key storage providers for certificate private keys. For more information, see [CNG certificates overview](/sccm/core/plan-design/network/cng-certificates-overview).  

- Starting in version 1802, when you configure Windows with the following policy: **System cryptography: Use FIPS-compliant algorithms for encryption, hashing, and signing**  

- Starting in version 1802, support for **TLS 1.2**. For more information, see [Cryptographic controls technical reference](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  



## <a name="bkmk_serverauth"></a> CMG server authentication certificate

*This certificate is required in all scenarios.*

You supply this certificate when creating the CMG in the Configuration Manager console.

The CMG creates an HTTPS service to which internet-based clients connect. The server requires a server authentication certificate to build the secure channel. Acquire a certificate for this purpose from a public provider, or issue it from your public key infrastructure (PKI). For more information, see [CMG trusted root certificate to clients](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > This certificate requires a globally unique name to identify the service in Azure. Before requesting a certificate, confirm that the desired Azure domain name is unique. For example, *GraniteFalls.CloudApp.Net*. Log on to the [Microsoft Azure portal](https://portal.azure.com). Select **Create a resource**, choose the **Compute** category, then select **Cloud Service**. In the **DNS name** field, type the desired prefix, for example *GraniteFalls*. The interface reflects whether the domain name is available or already in use by another service. Do not create the service in the portal, just use this process to check the name availability. 
  
 > [!NOTE]
 > Starting in version 1802, the CMG server authentication certificate supports wildcards. Some certificate authorities issue certificates using a wildcard character for the hostname. For example, **\*.contoso.com**. Some organizations use wildcard certificates to simplify their PKI and reduce maintenance costs.<!--491233-->  
 > 
 > For more information on how to use a wildcard certificate with a CMG, see [Set up a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#set-up-a-cmg).<!--SCCMDocs issue #565-->  


### <a name="bkmk_cmgroot"></a> CMG trusted root certificate to clients

Clients must trust the CMG server authentication certificate. There are two methods to accomplish this trust: 

- Use a certificate from a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. Windows clients include trusted root certificate authorities (CAs) from these providers. By using a server authentication certificate issued by one of these providers, your clients automatically trust it.  

- Use a certificate issued by an enterprise CA from your public key infrastructure (PKI). Most enterprise PKI implementations add the trusted root CAs to Windows clients. For example, using Active Directory Certificate Services with group policy. If you issue the CMG server authentication certificate from a CA that your clients don't automatically trust, add the CA trusted root certificate to internet-based clients.  

    - You can also use Configuration Manager certificate profiles to provision certificates on clients. For more information, see [Introduction to certificate profiles](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

> [!Note]  
> Starting in version 1806, when you create a CMG, you're no longer required to provide a trusted root certificate on the Settings page. This certificate isn't required when using Azure Active Directory (Azure AD) for client authentication, but used to be required in the wizard. If you're using PKI client authentication certificates, then you still must add a trusted root certificate to the CMG.<!--SCCMDocs-pr issue #2872-->  


### <a name="bkmk_serverauthpublic"></a> Server authentication certificate issued by public provider

A third-party certificate provider can't create a certificate for CloudApp.net, as that domain is owned by Microsoft. You can only get a certificate issued for a domain you own. The main reason for acquiring a certificate from a third-party provider is that your clients already trust that provider's root certificate.

Use the following process to create a DNS alias:

1. Create a canonical name record (CNAME) in your organization’s public DNS. This record creates an alias for the CMG to a friendly name that you use in the public certificate.

    For example, Contoso names their CMG **GraniteFalls**, which becomes **GraniteFalls.CloudApp.Net** in Azure. In Contoso’s public DNS contoso.com namespace, the DNS administrator creates a new CNAME record for **GraniteFalls.Contoso.com** for the real host name, **GraniteFalls.CloudApp.net**.  

2. Request a server authentication certificate from a public provider using the Common Name (CN) of the CNAME alias.
For example, Contoso uses **GraniteFalls.Contoso.com** for the certificate CN.  

3. Create the CMG in the Configuration Manager console using this certificate. On the **Settings** page of the Create Cloud Management Gateway Wizard:   

    - When you add the server certificate for this cloud service (from **Certificate file**), the wizard extracts the hostname from the certificate CN as the service name.  

    - It then appends that hostname to **cloudapp.net**, or **usgovcloudapp.net** for the Azure US Government cloud, as the Service FQDN to create the service in Azure.  

    - For example, when Contoso creates the CMG, Configuration Manager extracts the hostname **GraniteFalls** from the certificate CN. Azure creates the actual service as **GraniteFalls.CloudApp.net**.  

When you create the CMG instance in Configuration Manager, while the certificate has GraniteFalls.Contoso.com, Configuration Manager only extracts the hostname, for example: GraniteFalls. It appends this hostname to CloudApp.net, which Azure requires when creating a cloud service. The CNAME alias in the DNS namespace for your domain, Contoso.com, maps together these two FQDNs. Configuration Manager gives clients a policy to access this CMG, the DNS mapping ties it together so that they can securely access the service in Azure.<!--SCCMDocs issue #565-->  


### <a name="bkmk_serverauthpki"></a> Server authentication certificate issued from enterprise PKI

Create a custom SSL certificate for the CMG the same as for a cloud distribution point. Follow the instructions for [Deploying the service certificate for cloud-based distribution points](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) but do the following things differently:

- When requesting the custom web server certificate, provide an FQDN for the certificate's common name. This name can be a public domain name you own or you may use the cloudapp.net domain. If using your own public domain, refer to the process above for creating a DNS alias in your organization's public DNS.  

- When using the cloudapp.net public domain for the CMG web server certificate:  

    - On the Azure public cloud, use a name that ends in **cloudapp.net**  

    - Use a name that ends in **usgovcloudapp.net** for the Azure US Government cloud  



## <a name="bkmk_azuremgmt"></a> Azure management certificate

*This certificate is required for classic service deployments. It's not required for Azure Resource Manager deployments.*

You supply this certificate in the Azure portal, and when creating the CMG in the Configuration Manager console.

To create the CMG in Azure, the Configuration Manager service connection point needs to first authenticate to your Azure subscription. When using a classic service deployment, it uses the Azure management certificate for this authentication. An Azure administrator uploads this certificate to your subscription. When you create the CMG in the Configuration Manager console, provide this certificate.

For more information and instructions for how to upload a management certificate, see the following articles in the Azure documentation:

- [Cloud services and management certificates](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Upload an Azure Service Management Certificate](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Make sure to copy the subscription ID associated with the management certificate. You use it for creating the CMG in the Configuration Manager console.



## <a name="bkmk_clientauth"></a> Client authentication certificate

*This certificate is required for internet-based clients running Windows 7, Windows 8.1, and Windows 10 devices not joined to Azure Active Directory (Azure AD). It's also required on the CMG connection point. It isn't required for Windows 10 clients joined to Azure AD.*

The clients use this certificate to authenticate with the CMG. Windows 10 devices that are hybrid or cloud domain-joined don't require this certificate because they use Azure AD to authenticate.

Provision this certificate outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue client authentication certificates. For more information, see [Deploying the client certificate for Windows computers](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="bkmk_clientroot"></a> Client trusted root certificate to CMG

*This certificate is required when using client authentication certificates. When all clients use Azure AD for authentication, this certificate isn't required.* 

You supply this certificate when creating the CMG in the Configuration Manager console.

The CMG must trust the client authentication certificates. To accomplish this trust, provide the trusted root certificate chain. You can specify two trusted root CAs, and four intermediate (subordinate) CAs. 


#### Export the client certificate's trusted root

After issuing a client authentication certificate to a computer, use this process on that computer to export the trusted root.

1.  Open the Start menu. Type "run" to open the Run window. Open `mmc`.  

2.  From the File menu, choose **Add/Remove Snap-in...**.  

3.  In the Add or Remove Snap-ins dialog box, select **Certificates**, then select **Add**.  

    a. In the Certificates snap-in dialog box, select **Computer account**, then select **Next**.  

    b. In the Select Computer dialog box, select **Local computer**, then select **Finish**.  

    c. In the Add or Remove Snap-ins dialog box, select **OK**.  

4.  Expand **Certificates**, expand **Personal**, and select **Certificates**.  

5.  Select a certificate whose Intended Purpose is **Client Authentication**.  

    a. From the Action menu, select **Open**.  

    b. Go to the **Certification Path** tab.  

    c. Select the next certificate up the chain, and select **View Certificate**.  

6.  On this new Certificate dialog box, go to the **Details** tab. Select **Copy to File...**.  

7.  Complete the Certificate Export Wizard using the default certificate format, **DER encoded binary X.509 (.CER)**. Make note of the name and location of the exported certificate.  

8. Export all of the certificates in the certification path of the original client authentication certificate. Make note of which exported certificates are intermediate CAs, and which ones are trusted root CAs.  



## <a name="bkmk_mphttps"></a> Enable management point for HTTPS

Provision this certificate outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue a web server certificate. For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements) and [Deploy the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).


- In versions 1706 or 1710, when managing traditional clients with on-premises identity using a client authentication certificate, this certificate is recommended but not required.  

- In version 1710, when managing Windows 10 clients joined to Azure AD, this certificate is required for management points.  

- Starting in version 1802, this certificate is required in all scenarios. Only management points that you enable for CMG must be HTTPS. This change in behavior provides better support for Azure AD token-based authentication.  

- Starting in version 1806, when using the site option to **Use Configuration Manager-generated certificates for HTTP site systems**, the management point can be HTTP. For more information, see [Enhanced HTTP](#bkmk_ehttp).

### Management point client connection mode summary
These tables summarize whether the management point requires HTTP or HTTPS, depending upon the type of client and site version.

#### For internet-based clients communicating with the cloud management gateway
Configure an on-premises management point to allow connections from the CMG with the following client connection mode:

| Type of client   | 1706        | 1710        | 1802        | 1806        |
|------------------|-------------|-------------|-------------|-------------|
| Workgroup        | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | HTTP, HTTPS |
| AD domain-joined | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | HTTP, HTTPS |
| Azure AD-joined  | HTTPS       | HTTPS       | HTTPS       | E-HTTP, HTTPS |
| Hybrid-joined    | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E-HTTP, HTTP, HTTPS |

#### For on-premises clients communicating with the on-premises management point
Configure an on-premises management point with the following client connection mode:

| Type of client   | 1706        | 1710        | 1802        | 1806        |
|------------------|-------------|-------------|-------------|-------------|
| Workgroup        | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| AD domain-joined | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Azure AD-joined  | HTTPS       | HTTPS       | HTTPS       | HTTPS       |
| Hybrid-joined    | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |

#### Legend of terms
- *Workgroup*: The device isn't joined to a domain or Azure AD, but has a client authentication certificate
- *AD domain-joined*: You join the device to an on-premises Active Directory domain
- *Azure AD-joined*: Also known as cloud domain-joined, you join the device to an Azure Active Directory tenant
- *Hybrid-joined*: You join the device to both an Active Directory domain and an Azure AD tenant
- *HTTP*: On the management point properties, you set the client connections to **HTTP**
- *HTTPS*: On the management point properties, you set the client connections to **HTTPS**
- *E-HTTP*: On the site properties, Client Computer Communication tab, you set the site system settings to **HTTPS or HTTP**, and you enable the option to **Use Configuration Manager-generated certificates for HTTP site systems**. You configure the management point for HTTP or HTTPS. 



## Next steps

- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  

- [Frequently asked questions about the cloud management gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)  

- [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)  
