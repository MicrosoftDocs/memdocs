---
title: CMG Certificates
description: Learn about the different digital certificates to use with the cloud management gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
---

# Certificates for the cloud management gateway

*Applies to: System Center Configuration Manager (Current Branch)*

Depending upon the scenario you use to manage clients on the internet with the cloud management gateway (CMG), you need one or more digital certificates. For more information about the different scenarios, see [plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## CMG server authentication certificate

*This certificate is required in all scenarios.*

You supply this certificate when creating the CMG in the Configuration Manager console.

The CMG creates an HTTPS service to which internet-based clients connect. The server requires a server authentication certificate to build the secure channel. Purchase a certificate for this purpose from a public provider, or issue it from your public key infrastructure (PKI). For more information, see [CMG trusted root certificate to clients](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > This certificate requires a globally unique name to identify the service in Azure. Before requesting a certificate, confirm that the desired Azure domain name is unique. For example, *GraniteFalls.CloudApp.Net*. Log on to the [Microsoft Azure portal](https://portal.azure.com). Click **Create a resource**, select the **Compute** category, then click **Cloud Service**. In the **DNS name** field, type the desired prefix, for example *GraniteFalls*. The interface reflects whether the domain name is available or already in use by another service. Do not create the service in the portal, just use this process to check the name availability. 
  
 > [!NOTE]
 > Starting in version 1802, the CMG server authentication certificate supports wildcards. Some certificate authorities issue certificates using a wildcard character for the hostname. For example, **\*.contoso.com**. Some organizations use wildcard certificates to simplify their PKI and reduce maintenance costs.
 <!--491233-->


### CMG trusted root certificate to clients

Clients must trust the CMG server authentication certificate. There are two methods to accomplish this trust:
- Use a certificate from a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. Windows clients include trusted root certificate authorities (CAs) from these providers. By using a server authentication certificate issued by one of these providers, your clients automatically trust it. 
- Use a certificate issued by an enterprise CA from your public key infrastructure (PKI). Most enterprise PKI implementations add the trusted root CAs to Windows clients. For example, using Active Directory Certificate Services with group policy. If you issue the CMG server authentication certificate from a CA that your clients do not automatically trust, you need to add the CA trusted root certificate to internet-based clients.
    - You can also use Configuration Manager certificate profiles to provision certificates on clients. For more information, see [Introduction to certificate profiles](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### Server authentication certificate issued by public provider

When you use this method, clients automatically trust the certificate and you don't need to create a custom certificate yourself. Configuration Manager creates the service in Azure with the cloudapp.net domain. A public certificate provider can't issue to you a certificate with this name. Use the following process to create a DNS alias:

1. Create a canonical name record (CNAME) in your organization’s public DNS. This record creates an alias for the CMG to a friendly name that you use in the public certificate.
For example, Contoso names their CMG **GraniteFalls**, which becomes **GraniteFalls.CloudApp.Net** in Azure. In Contoso’s public DNS contoso.com namespace, the DNS administrator creates a new CNAME record for **GraniteFalls.Contoso.com** for the real host name, **GraniteFalls.CloudApp.net**.
2. Request a server authentication certificate from a public provider using the Common Name (CN) of the CNAME alias.
For example, Contoso uses **GraniteFalls.Contoso.com** for the certificate CN.
3. Create the CMG in the Configuration Manager console using this certificate. On the **Settings** page of the Create Cloud Management Gateway Wizard: 
	- When you add the server certificate for this cloud service (from **Certificate file**), the wizard extracts the hostname from the certificate CN as the service name. 
	- It then appends that hostname to **cloudapp.net**, or **usgovcloudapp.net** for the Azure US Government cloud, as the Service FQDN to create the service in Azure.
	- For example, when Contoso creates the CMG, Configuration Manager extracts the hostname **GraniteFalls** from the certificate CN. Azure creates the actual service as **GraniteFalls.CloudApp.net**.

### Server authentication certificate issued from enterprise PKI

Create a custom SSL certificate for the CMG the same as for a cloud distribution point. Follow the instructions for [Deploying the service certificate for cloud-based distribution points](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) but do the following things differently:

- When requesting the custom web server certificate, provide an FQDN for the certificate's common name. For using the CMG on Azure public cloud, use a name that ends in **cloudapp.net**, or **usgovcloudapp.net** for the Azure US Government cloud.



## Azure management certificate

*This certificate is required for classic service deployments. It is not required for Azure Resource Manager deployments.*

You supply this certificate in the Azure portal, and when creating the CMG in the Configuration Manager console.

To create the CMG in Azure, the Configuration Manager service connection point needs to first authenticate to your Azure subscription. When using a classic service deployment, it uses the Azure management certificate for this authentication. An Azure administrator uploads this certificate to your subscription. When you create the CMG in the Configuration Manager console, provide this certificate.

For more information and instructions for how to upload a management certificate, see the following articles in the Azure documentation:

- [Cloud services and management certificates](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Upload an Azure Service Management Certificate](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Make sure to copy the subscription ID associated with the management certificate. You use it for creating the CMG in the Configuration Manager console.



## Client authentication certificate

*This certificate is required for internet-based clients running Windows 7, Windows 8.1, and Windows 10 devices not joined to Azure Active Directory (Azure AD). It's also required on the CMG connection point. It is not required for Windows 10 clients joined to Azure AD.*

The clients use this certificate to authenticate with the CMG. Windows 10 devices that are hybrid or cloud domain-joined don't require this certificate because they use Azure AD to authenticate.

Provision this certificate outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue client authentication certificates. For more information, see [Deploying the client certificate for Windows computers](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### Client trusted root certificate to CMG

*This certificate is required when using client authentication certificates. When all clients use Azure AD for authentication, this certificate is not required.* 

You supply this certificate when creating the CMG in the Configuration Manager console.

The CMG must trust the client authentication certificates. To accomplish this trust, provide the trusted root certificate chain. You can specify two trusted root CAs, and four intermediate (subordinate) CAs. 


#### Export the client certificate's trusted root

After issuing a client authentication certificate to a computer, use this process on that computer to export the trusted root.

1.  Open the Start menu. Type "run" to open the Run window. Open **mmc**. 

2.  From the File menu, choose **Add/Remove Snap-in...**.

3.  In the Add or Remove Snap-ins dialog box, select **Certificates**, then click **Add**. 
    a. In the Certificates snap-in dialog box, select **Computer account**, then click **Next**. 
    b. In the Select Computer dialog box, select **Local computer**, then click **Finish**. 
    c. In the Add or Remove Snap-ins dialog box, click **OK**.

4.  Expand **Certificates**, expand **Personal**, and select **Certificates**.

5.  Select a certificate whose Intended Purpose is **Client Authentication**. 
    a. From the Action menu, select **Open**. 
    b. Switch to the **Certification Path** tab. 
    c. Select the next certificate up the chain, and click **View Certificate**.

6.  On this new Certificate dialog box, switch to the **Details** tab. Click **Copy to File...**.

7.  Complete the Certificate Export Wizard using the default certificate format, **DER encoded binary X.509 (.CER)**. Make note of the name and location of the exported certificate.

8. Export all of the certificates in the certification path of the original client authentication certificate. Make note of which exported certificates are intermediate CAs, and which ones are trusted root CAs.



## Enable management point for HTTPS

*Certificate requirements*
- In versions 1706 or 1710, when managing traditional clients with on-premises identity using a client authentication certificate, this certificate is recommended but not required.
- In version 1710, when managing Windows 10 clients joined to Azure AD, this certificate is required for management points. 
- Starting in version 1802, this certificate is required in all scenarios. Only management points that you enable for CMG must be HTTPS. This change in behavior provides better support for Azure AD token-based authentication. 

Provision this certificate outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue a web server certificate. For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements) and [Deploy the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## Next steps

- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Frequently asked questions about the cloud management gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
