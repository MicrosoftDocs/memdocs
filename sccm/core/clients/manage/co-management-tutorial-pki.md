---
# required metadata

title: Tutorial - Configure co-management for devices using PKI
titleSuffix: Configuration Manager 
description: Configure co-management of Windows 10 devices for Configuration Manager and Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2018
ms.topic: tutorial
ms.prod:
ms.service:  
ms.technology:
ms.assetid: 

# optional metadata
---


# Enable co-management for Microsoft Intune and System Center Configuration Manager

In this tutorial, you’ll use your PKI and publicly issued certificates to set up Configuration Manager to support co-management of your Windows 10 devices.  

With co-management, you can use both Microsoft Intune and System Center Configuration Manager to manage a device. You can also use co-management as a bridge to help migrate from managing your devices on-premises to modern cloud-based management.

You can reach co-management from either of the following starting points, though this tutorial follows the path of the second:  
- **Your devices are enrolled in Intune**
- **Your devices are enrolled with Configuration Manager**

When you have Windows 10 devices that are Configuration Manager clients, you can enroll these devices in Intune and enable co-management from the Configuration Manager console. Configuration Manager triggers automatic enrollment into Intune based on the Azure Active Directory (AD) tenant information.

Co-management requires the use of several certificates, configuration of Azure, and public DNS records for key components from Configuration Manager. The bulk of the work is getting your certificates created, configured, and then enrolled on the correct servers.  

**In this tutorial you will:**
> [!div class="checklist"]
> * Review your Azure configurations
> * Configure the PKI environment, including:
>     - Create custom certificate templates and certificates
>     - Identify an Azure Cloud Service Name for your cloud management gateway
>     - Request externally issued SSL certificates for your cloud services
>     - Enroll and export certificates on your primary site server
> * Configure site system roles:
>     - Enable Azure services in Configuration Manager
>     - Deploy the cloud-based site system roles  
>     - Create DNS CNAME records for the cloud-based site system roles
>     - Configure the management point for use with the cloud management gateway
>     - Create a Configuration Manager client settings profile
> * Enable co-management in Configuration Manager, including:   
>     - Enable Auto mobile device management (MDM) enrollment
> * Deploy an Intune app in install the Configuration Manager client


## Prerequisites
Co-management combines your on-premises Configuration Manager and PKI infrastructure with cloud-based resources. Review and configure the following prerequisites before you continue this tutorial.

### Azure services and environment
- Azure Subscription ([free trial](https://azure.microsoft.com/free))
- Azure Active Directory Premium  
- Microsoft Intune 
- Users who [are assigned licenses for Intune](https://docs.microsoft.com/intune/licenses-assign)
- *If you use an on-premises domain:* [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) is configured between your on-premises Active Directory and your Azure Active Directory (AD) tenant

> [! TIP]  
> An EMS Subscription includes both Azure Active Directory Premium and Microsoft Intune. EMS Subscription  ([free trial](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)) 


### On-premises infrastructure
- A [supported version](https://docs.microsoft.com/sccm/core/servers/manage/updates#version-details) of System Center Configuration Manager current branch
  - The [MDM Authority](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) must be set to Intune
  - The primary site must have a management point you can configure for HTTPS  
    > [! TIP]  
    > Simplify your deployment by using Enhanced HTTP. [Enhanced HTTP](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/enhanced-http) was introduced as a pre-release feature in Configuration Manager version 1806.
  
- Microsoft Certificate Authority (CA) that runs on Windows Server 2008 R2 or later, and that is joined to an on-premises AD domain that contains your Configuration Manager deployment
  - The CA's root certificate must be installed on the member server you'll use to manage the cloud distribution point and cloud management gateway

During this tutorial, you'll create, configure, or request the following objects.
- On your Configuration Manager [primary site](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/design-a-hierarchy-of-sites#BKMK_ChoosePriimary) server:
  - [Azure services](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard)  
  - [Cloud management gateway](https://docs.microsoft.com/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)   
  - [Cloud distribution point](https://docs.microsoft.com/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)
- On-premises certificates:
  - *Management Certificate* – An SSL certificate issued by an on-premises Enterprise CA. This certificate establishes a trust between the Azure management API and Configuration Manager.

     This certificate is exported twice, first as a .CER file, and then again as a .PFX (private key) file format. An existing certificate can be reused here if the private key (.PFX file) is available.

  - *Management Point* – An SSL certificate issued by an on-premises Enterprise CA, which is an IIS Web Server SSL certificate. You don't export this certificate. 
    
    You don’t need this certificate if you use [Enhanced HTTP](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/enhanced-http). 

  - *Client Authentication* – This certificate is issued by an on-premises Enterprise CA for the Management Point.  You don't export this certificate.

  - *Trusted root* – A certificate for the trusted root, and additional certificates for any intermediate issuing CAs must be available to set up the cloud management gateway.  These certificates will be exported as .CER files.

- External certificates (Optional – the following certificates can be issued by your own PKI if you won't support clients on the internet):
  
  We recommend getting the following two certificates from a public Certification Authority when possible. However, this tutorial walks you through creating these certificates from your own PKI when you can't get a public SSL.
  - *Cloud management gateway SSL cert* – An SSL certificate that is issued by a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. This certificate will be exported as a .PFX file with Private Key.

  - *Cloud distribution point SSL cert* – An SSL certificate that is issued by a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. This certificate will be exported as a .PFX file with Private Key.


### Permissions
Throughout this tutorial, you'll need the following permissions to complete tasks:
- An account that is a *global administrator* in Azure
- An account that is a *domain admin* on your on-premises infrastructure
- An account that is a *full administrator* for *all* scopes in Configuration Manager.

## Configure your PKI environment
Co-management requires use of several certificates that derive authority from your on-premises Microsoft certificate authority. The following procedures will help you to create and configure these certificates during the tutorial.  You also need two public SSL certificates that you request from a public and globally trusted certificate provider. For some environments, it's possible to use SSL certs from your own PKI.  

### About use of public vs self-issued certificates
The cloud management gateway and cloud distribution point cloud services require SSL certificates.

For a production environment, we recommend you submit a certificate signing requests (CSR) for publicly issued SSL certificates from a public and globally trusted certificate provider.

While the externally provided certificates are recommended, it's possible to issue your own SSL certificates.
- This tutorial will guide you to create the SSL certificates from an on-premises private key infrastructure, so you can complete this tutorial in a lab environment.
- If you have access to public SSL certificates, use the information in the following section to request certificates for use with Co-management. You'll then use those certificates instead of the one that are created as part of this tutorial.  

#### Request public certificates
Use the following information when you submit a certificate signing request to a public certificate
provider.  

For this tutorial, we use the following values:  
- *TestIntuneCMG* and *TestIntuneCDP* to identify the service names of our cloud services
- *Contoso* as the company name
- *Contoso.com* as the public domain

We recommend you use your primary site server to generate the certificate signing requests (CSR), and enroll and export the public SSL certificates. Enroll the certificates on the same server that generated the CSR or you'll not be able to export the private key, which is required.

When you generate the CSR for the cloud management gateway and the cloud distribution point, request a version 2 key provider type. Only version 2 certificates are supported.  

**Cloud management gateway**:  
- **Common Name**: ClousServiceNameCMG.YourCompanyPubilcDomainName.com
Example: TestIntuneCMG.contoso.com
- **Subject Alternative Name**: Same as the Common Name (CN)
- **Organization**:  The name of your organization
- **Department**: Per your organization  
- **City**: Per your organization  
- **State**: Per your organization  
- **Country**: Per your organization  
- **Key Size: 2048**
- **Provider: Microsoft RSA SChannel Cryptographic Provider**

**Cloud distribution point**:
- **Common Name**:  ClousServiceNameCDP.YourCompanyPubilcDomainName.com
Example: TestIntuneCMG.contoso.com
- **Subject Alternative Name**: Same as the Common Name (CN)
- **Organization**:  The name of your organization
- **City**: Per your organization  
- **State**: Per your organization  
- **Country**: Per your organization  
- **Key Size: 2048**
- **Provider: Microsoft RSA SChannel Cryptographic Provider**

#### Enroll and then export public certificates
After you receive the public certificates, import them to the local certificate store of the computer that created the CSR. After you import the two certificates, you'll export them during the following two procedures, later in this tutorial:
- Cloud management gateway: [Export the CMG PKI web certificate (ConfigMgrCloudMGServer)](#export-the-cmg-pki-web-certificate-(configmgrcloudmgserver))
- Cloud distribution point: [Export the CDP PKI web certificate (ConfigMgrCloudDPServer)](#export-the-cdp-pki-web-certificate-(configmgrclouddpserver))

### Cloud management gateway certificate
The Cloud Management Gateway (CMG) certificate is used for encrypting traffic between the Configuration Manager client and the CMG. The certificate traces back to a Trusted Root to verify the server's identity to the client.

**About the cloud management gateway certificate**:
In this tutorial, the cloud management gateway (CMG) certificate uses an FQDN that ends in cloudapp.net for the Azure public cloud. In Azure, the CMG is hosted within the cloudapp.net domain as *\<YourUniqueDnsName>.cloudapp.net*.

Some customer environments use a domain other than *cloudapp.net* that aligns with an organization's public DNS name. When your organization uses a unique DNS name, we recommended using a publicly issued SSL web certificate from a public and globally trusted certificate provider. Windows clients include trusted root certificate authorities (CAs) from public providers. By using a server authentication certificate issued by a public provider, your clients automatically trust the certificate.

Use of a publicly issued certificate replaces the certificate issued by an enterprise CA from your public key infrastructure. When you use your own PKI as the source for this certificate, as is required when using the *\*cloudapp.net* domain name, you must add the organizational PKI root CA as a trusted root on your organization’s clients.

> [! Note]  
> **If you have a publicly issued SSL certificate for your CMG**, import that certificate and then jump to the [Export the CMG web certificate (ConfigMgrCloudMGServer)](#export-the-cmg-web-certificate-(configmgrcloudmgserver)) procedure later in this section.  


In this section of the tutorial, you will:
- Duplicate the Web Server Certificate template
- Customize the template to allow private key export
- Secure the newly created template
- Confirm a custom domain name to use in the Azure *\*cloudapp.net* namespace
- Request and then export the template to make it available


#### Create and issue the PKI web certificate template (ConfigMgrCloudWebServer)
The certificate template you create is used to issue an SSL web certificate. You upload the SSL web certificate to Azure to install on the CMG and then use it for server authentication to clients, and encrypting client to CMG communication. It's also used for the CDP.

1. In Active Directory, create a security group named **ConfigMgr IIS Servers**, and add the member server that will manage cloud-based site system roles to the group.  Use of this group limits access to the certificate templates you'll create.
2. Reboot the Configuration Manager member server you'll use to manage the cloud-based site system roles. Then, on that server, open a cmd prompt and run **gpresult /r** to confirm that the **ConfigMgr IIS Servers** group membership is applied to the server during boot. You should see the server listed under **Domain Computers**.
3. On a member server that runs the Certification Authority console (certsrv.msc), start the console, expand your server name, right-click **Certificate Templates**, and then select **Manage**. The Certificate Templates Console opens.
4. In the results pane, **right-click** the entry that displays **Web Server** in the column Template Display Name, and then select **Duplicate Template**.
5. On the **Compatibility** tab of the new template dialog box, ensure that **Windows 2003 Server**, Enterprise Edition is selected.
   > [! IMPORTANT]  
   > Do not select Windows 2008 Server, Enterprise Edition

6. On the **General tab**, enter the template display name **ConfigMgrCloudWebServer**.
7. On the **Request Handling** tab, select **Allow private key to be exported**.
8. Click the **Security** tab, and then remove the **Enroll** permission from the security groups **Domain Admins and Enterprise Admins**.
9. Click **Add**, specify **ConfigMgr IIS Servers**, and then click **OK**.  Then assign the group the **Enroll** and **Read** permissions.
10. Click **OK**, and then close the Certificate Templates Console.
11. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.
12. In the **Enable Certificate Templates** dialog box, select the new template that you've created, **ConfigMgrCloudWebServer**, and then click **OK**.

With the certificate enabled, you can close the Certification Authority console.


#### Verify a unique FQDN for the CMG cloudapp.net   
Before you request and then export the CMG PKI Web certificate, verify the cloud service DNS name you want to use is available in the cloudapp.net domain. When the name isn't unique, the CMG can't be created in a later procedure. If you can’t create the CMG with the name you use in the certificate you request, you must recreate the certificate with a new and unique name.
1. Sign in to the [Azure portal](https://portal.azure.com/)
2. Select **All services > Cloud services (classic)**. **Cloud services (classic)** is in the **Compute** section.
3. Select **+Add**, and then for **DNS name**, specify the name you want to use.  
   For example, TestIntuneCMG

If the name you specify is available, you'll see a green check instead of a red exclamation point. Close the **Cloud Service (classic)** panes without saving this configuration.

#### Request the CMG PKI web certificate (ConfigMgrCloudMGServer)
When you request a web server certificate for the CMG service, you specify the cloudapp.net FQDN as the common name of the certificate. The FQDN is read from that common name field when you create the CMG in Azure.
1. On the member server you'll use to manage the cloud-based site system roles, run **certlm.msc** to start the Certificate Manager for the Local Computer.

2. In the Certificate Manager console, expand **Certificates - (Local Computer)**, and then select **Personal**.

3. Right-click **Certificates**, and then select **All Tasks > Request New Certificate**.

4. On the **Before You Begin** page, select **Next**.

5. If you see the **Select Certificate Enrollment Policy** page, select **Next**.

6. On the **Request Certificates** page, locate **ConfigMgrCloudWebServer** from the list of certificates, and then select **More information is required to enroll for this certificate. Click here to configure setting to open the Certificate Properties**.

7. On the **Subject** tab, in the **Subject name** area, for **Type** select **Common name**. For **Value**, specify the unique cloud service DNS name that you verified as available. Specify this name as an FQDN that includes *.cloudapp.net*.  
  
   For example, if your DNS name is *TestIntuneCMG*, you would specify *testintuneCMG.cloudapp.net*

8. Select **Add**, and then select **OK** to save this configuration and close the **Certificate Properties**.

9. On the **Request Certificates** page, select **ConfigMgrCloudWebServer**, and then select **Enroll**.

10. On the **Certificates Installation Results** page, wait until the certificate is installed, and then select **Finish**.  
11. To validate the certificate configuration, in the Certificate Manager console:  
    1. Select **Personal > Certificates**, and then open the newly installed certificate.  
    2. On the **General** tab, review the **Issued to** and **Issued by** values.  
    3. On the **Details** tab, select the **Subject** field and confirm that the only subject on the certificate is *CN=\<YourCustomDnsName>.cloudapp.net*.  
    4. Select **OK** to close the certificate.

#### Export the CMG web certificate (ConfigMgrCloudMGServer)
Export the CMG PKI web certificate so it can be used on the CMG in Azure.
> [! NOTE]  
> If you are using a public SSL certificate for the CMG, you will export that certificate in this procedure. To export the certificate for use by the CMG, you must have previously imported it to the server that originally requested it, and then run this procedure on that computer for that certificate.  

1. On the member server you'll use to manage the cloud-based site system roles, run **certlm.msc** to open the Certificate Manager console.

2. In the Certificate Manager console, select **Personal > Certificates**. Then, right-click on the **ConfigMgrCloudMGServer** certificate you enrolled in the previous procedure, and then select **All Tasks > Export**.

3. In the Certificate Export Wizard, select **Next**, select **Yes, export the private key**, and then **Next**.

4. On the Export File Format page, select **Personal Information Exchange - PKCS #12 (.PFX)**, select **Next**, and provide a password. For file name, specify **C:\ConfigMgrCloudMGServer**.

5. Select **Next**, and then confirm the following settings before selecting **Finish** to complete the export:
   - Export Keys = Yes
   - Include all certificates in the certification path = Yes
   - File format = Personal Information Exchange (*.pfx)
6. After you complete the export, locate the .pfx file and place a copy of it on the Configuration Manager primary site server in **C:\Certs**. The Certs folder is a temporary folder to use while moving certificates between servers. You'll need to access the certificate file from the primary site server when you deploy the cloud management gateway to Azure.

   After you copy the certificate to the primary site server, you can delete the Certificate from the Personal Certificate store on this member server.

### Cloud distribution point certificate
The cloud distribution point (CDP) isn't a requirement to use co-management. However, most deployments that manage clients on the internet can expect to need a CDP at some point. The CDP is required if you want to install the Configuration Manager client on a device that is only joined to Azure AD.

The CDP certificate is similar to the CMG certificate and you use the same certificate template to request the CDP certificate as you used for the CMG.  
For more information about this site system role, see [Use a cloud distribution point](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point).

> [! NOTE]  
> **If you have a publicly issued SSL certificate for your CDP**, import that certificate and then jump to the [Export the CMG web certificate (ConfigMgrCloudDPServer)](#export the cmg web certificate (configmgrclouddpserver)) procedure later in this section.  

**In this section of the tutorial, you will**:
- Reuse the Web Server Certificate template that you created for the CMG, for the CDP.
- Request and then export the template to make it available

#### Verify DNS name for the CDP cloudapp.net FQDN is unique
Before you request and then export the CDP PKI Web certificate, verify the cloud service DNS name you want to use is available in the cloudapp.net domain. When the name isn't unique, the CDP can't be created in a later procedure. When you can’t create the CDP with the name you use in the certificate you request, you must recreate the certificate with a new and unique name.  
1. Sign in to the [Azure portal](https://portal.azure.com/)
2. Select **All services > Cloud services (classic)**. **Cloud services (classic)** is in the **Compute** section.
3. Select **+Add**, and then for **DNS name**, specify the name you want to use.  
   For example, TestIntuneCDP

If the name you specify is available, you'll see a green check instead of a red exclamation point. Close the **Cloud Service (classic)** panes without saving this configuration.

#### Request the CDP PKI web certificate (ConfigMgrCloudDPServer)
Like the CMG service, when you request a web server certificate for the CDP service, you specify the cloudapp.net FQDN as the common name of the certificate.  

1. On the member server you use to manage the cloud-based site system roles, run **certlm.msc** to start the Certificate Manager for the Local Computer.

2. In the Certificate Manager console, expand **Certificates - (Local Computer)**, and then select **Personal**.

3. Right-click **Certificates**, and then select **All Tasks > Request New Certificate**.

4. On the **Before You Begin** page, select **Next**.

5. If you see the **Select Certificate Enrollment Policy** page, select **Next**.

6. On the **Request Certificates** page, locate **ConfigMgrCloudWebServer** from the list of certificates, and then select **More information is required to enroll for this certificate. Click here to configure setting to open the Certificate Properties**.  The *ConfigMgrCloudWebServer* is the certificate template that was [created earlier in this tutorial](#create-and-issue-the-pki-web-certificate-template-(configmgrcloudwebserver)).

7. On the **Subject** tab, in the **Subject name** area, for **Type** select **Common name**. For **Value**, specify the unique cloud service DNS name that you verified as available for your cloud distribution point. Specify this name as an FQDN that includes *.cloudapp.net*.   

   For example, if your DNS name is *TestIntuneCDP*, you would specify *testintuneCDP.cloudapp.net*

8. Select **Add**, and then select **OK** to save this configuration and close the **Certificate Properties**.

9. On the **Request Certificates** page, select **ConfigMgrCloudWebServer**, and then select **Enroll**.

10. On the **Certificates Installation Results** page, wait until the certificate is installed, and then select **Finish**.  

11. To validate the certificate configuration, in the Certificate Manager console:  
    1. Select **Personal > Certificates**, and then open the newly installed certificate.  
    2. On the **General** tab, review the **Issued to** and **Issued by** values.  
    3. On the **Details** tab, select the **Subject** field and confirm that the only subject on the certificate is *CN=\<YourCustomDnsName>.cloudapp.net*.  
    4. Select **OK** to close the certificate.  

#### Export the CDP web certificate (ConfigMgrCloudDPServer)
Export the CDP PKI web certificate so it can be used on the CDP in Azure.

> [! NOTE]  
> If you are using a public SSL certificate for the CDP, you will export that certificate in this procedure. To export the certificate for use by the CDP, you must have previously imported it to the server that originally requested it, and then run this procedure on that computer for that certificate.  

1. On the member server where you created the cloud-based site system roles, run **certlm.msc** to open the Certificate Manager console.

2. In the Certificate Manager console, select **Personal > Certificates**. Then, right-click on the **ConfigMgrCloudDPServer** certificate you enrolled in the previous procedure, and then select **All Tasks > Export**.

3. In the Certificate Export Wizard, select **Next**, select **Yes, export the private key**, and then Next.

4. On the Export File Format page, select **Personal Information Exchange - PKCS #12 (.PFX)**, select **Next**, and provide a password. For file name, specify **C:\ConfigMgrCloudDPServer**.

5. Select **Next**, and then confirm the following settings before selecting **Finish** to complete the export:
   - Export Keys = Yes
   - Include all certificates in the certification path = Yes
   - File format = Personal Information Exchange (*.pfx)

6. After you complete the export, locate the .pfx file and place a copy of it on the Configuration Manager primary site server in **C:\Certs**. You'll need to access this file from the primary site server when you deploy the cloud distribution point to Azure.

   After you copy the certificate to the primary site server, you can delete the Certificate from the Personal Certificate store on this member server.

### Azure management certificate
The Azure management certificate is used to access your Azure subscription.  This certificate is used by the Configuration Manager component SMS_CLOUD_SERVICES_MANAGER to create the cloud management gateway (CMG) service in Azure, and for ongoing configurations and administration of the service. This certificate can be self-signed, or issued by an enterprise PKI or a public CA.  

In this section of the tutorial you will:
- Create a self-signed certificate for Azure Management
- Export the certificate in the necessary formats
- Upload the certificate using the Azure portal

#### Create the Azure management certificate template (AzureManagementCert)

1. On the primary site server, open the Internet Information Services (IIS) Manager console (**inetmgr**).  

2. In the navigation pane, select your primary site server, and then double-click on **Server Certificates**.

3. In the Actions pane, select **Create Self-Signed Certificate**.
4. On the **Specify Friendly Name** page, enter **AzureManagementCert** for the friendly name, and then select **OK**.  
5. Close the IIS Manager console to complete this procedure.

#### Export the Azure management certificate (AzureManagementCert)
The Azure management certificate is exported twice:
- First as a .pfx certificate.  This certificate gets added to the Configuration Manager database and is used by SMS_CLOUD_SERVICES_MANAGER.
- Second as a .cer certificate.  This certificate is uploaded to Azure to delegate subscription management.

1. On the primary site server, run **certlm.msc** to open the Certificate Manager console for the local computer.

2. In the Certificate Manager console, select **Personal > Certificates**, right-click on the certificate with the *Friendly Name* **AzureManagementCert**. This certificate is the one you created in the previous procedure.  Next, select **All Tasks > Export**.

3. In the Certificate Export Wizard, select **Next**, select **Yes, export the private key**, and then **Next**.

4. On the Export File Format page, select **Personal Information Exchange - PKCS #12 (.PFX)** > select **Next**, and provide a password. For *File name*, specify C:\Certs\AzureManagementCert

5. Select **Next**, and then confirm the following settings before selecting **Finish** to complete the export:  
   - Export Keys = Yes
   - Include all certificates in the certification path = Yes
   - File format = Personal Information Exchange (*.pfx)

6. Now export the certificate a second time. In the Certificate Manager console, right-click on the **AzureManagementCert > All Tasks > Export**.

7. In the Certificate Export Wizard, select **Next**, select **No, do not export the private key**, and then **Next**.

8. On the Export File Format page, select **DER encoded binary X.509 (.CER) > Next**, and provide a password.  For *File name*, specify **C:\Certs\AzureManagementCert**.

9. Select **Next**, and then **Finish** to complete the export.

10. Because this certificate allows private key export and can be used to manage the entire Azure subscription, you should delete it. To do so:
    1. In the Certificate Manager console, select **Personal > Certificates**, and select the **AzureManagementCert** certificate.  
    2. Confirm the correct certificate is selected by verifying that the friendly name is **AzureManagementCert**, and then delete the certificate.  

    Close the Certificates console to complete the procedure.  

#### Upload the Azure Management certificate to Azure
A global administrator for your Azure subscription must upload the Azure management certificate to your Azure subscription before Configuration Manager can use the certificate to create the cloud management gateway (CMG) service.  
1. On the primary site server, where you have placed certificates in the C:\Cert folder, sign in to the [Azure portal](https://portal.azure.com/)

2. Select **All services > Subscriptions**, and then copy your **Subscription ID** to a notepad file. You'll reference this ID during a later procedure when you create the CMG service.

3. Select **Management certificates > Upload**, and then **Browse** to and select **AzureManagementCert.cer**.

4. Select **Upload**.  After the upload succeeds, the certificate is visible in the Management certificates blade of the portal.

### Client PKI Workstation authentication certificate
Clients use the client authentication certificate from your enterprise PKI (a trusted authority) to authenticate to Configuration Manager when the domain isn't available.  

The following procedures create and then deploy a client authentication certificate to a Configuration Manager client.  

**In this section of the tutorial you will**:
- Create and issue a Workstation Authentication certificate template on your CA
- Configure Autoenrollment of the template by using Group Policy
- Automatically enroll the certificate and verify its installation on computers  


#### Create and issue a Workstation Authentication certificate template (ConfigMgrWorkstationAuth)

1. On a member server that runs the Certification Authority console (certsrv.msc), start the console, expand your server name, right-click **Certificate Templates**, and then select **Manage**. The Certificate Templates Console opens.

2. In the results pane, right-click the entry that displays **Workstation Authentication** in the column Template Display Name, and then select **Duplicate Template**.

3. On the **Compatibility** tab of the new template dialog box, ensure that **Windows 2003** Server, Enterprise Edition is selected.

   > [! IMPORANT]  
   > Do not select Windows 2008 Server, Enterprise Edition

4. On the **General** tab, enter the Template display name **ConfigMgrWorkstationAuth**.  

5. On the **Security** tab, select the **Domain Computers** group and then add the permissions of **Read** and **Autoenroll**. Do not clear **Enroll**.  

   > [! TIP]  
   > In this tutorial, we will not act to autoenroll this certificate. Typically you would do so for a domain-joined PKI deployment. To use autoenroll you must also setup a [Group Policy (GPO) to handle autoenrollment](https://docs.microsoft.com/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client12008).
6. Select **OK**, and then close the Certificate Templates Console.  

7. In the Certification Authority console, right-click **Certificate Templates**, select **New > Certificate Template to Issue**.

8. In the **Enable Certificate Templates** dialog box, select the new template that you've created, **ConfigMgrWorkstationAuth**, and then select **OK**.
Close the Certification Authority console to complete this procedure.

 
 


### Trusted Root Certificate
To set up the cloud management gateway, you must upload to Azure the trusted root certificate for your certification authority (CA), and for any intermediate issuing CAs. You'll also upload the CMG PKI web certificate.  

- If you issue your own CMG and CDP PKI web certificates, clients will need a trusted root certificate in their computer store that matches the root CA of those certificates. Domain joined clients with an enterprise PKI get this certificate automatically.  
- If you use publicly issued certificate with a public DNS name for your CMG service name, the certificate will already be trusted by clients.

**In this section of the tutorial you will**:
- Export the trusted root certificate
- Configure the trusted root in the Site’s Certificate Trust list

#### Export the Trusted Root Certificate of your on-premises Microsoft Certificate Authority

1. On a domain client computer, use administrator credentials to run **certlm.msc** to start the Certificate Manager for the Local Computer.

2. In the **Certificates - Local Computer** console, expand **Trusted Root Certification Authorities > Certificates**, and then locate the on-premises Root CA. An example of the Root CA name might be *Contoso Root CA*.

3. Right-click on the Root CA certificate, and then select **All Tasks > Export > Next**.

4. On the **Export File Format** page, select **DER encoded binary x.509 (.CER)**, and then select **Next**.
5. On the **File to Export** page, specify the name of the file that you want to export, and then select **Next**.
Example: **C:\TrustedRootCert.cer**

6. On the **Completing the Certificate Export Wizard** page, select **Finish** to complete the wizard, and then select **OK** in the confirmation dialog box. The certificates .CER file is saved to the location you indicated, and you can close the console.

7. Transfer the TrustedRootCert.cer file to the C:\Certs folder on the primary site server.


#### Configure the Trusted Root to be accepted for Client Communications
To be accepted for Configuration Manager client communications, a client authentication certificate must match a trusted root certificate that is present on the management point.  

Run the following actions on the primary site server as an administrator.  

1. Open the Configuration Manager console, and then go **Administration > Overview > Site Configuration > Sites**.  

2. Right-click on the primary site, and then select **Properties**.

3. On the Client Computer Communication tab, select **Use PKI client certificate (client auth capability) when available**.

4. For **Trusted Root Certification Authorities**, select **Set** to open the Set Root CA Certificates dialog.

5. Select the **starburst** icon, and then browse to and select **C:\Certs\TrustedRootCERT.cer**. This file is the trusted root certificate you exported in the previous procedure, and then transferred to the primary site server.

6. Select **Open > OK > OK** to save this configuration.    


### Enable Azure cloud services in Configuration Manager
After your certificates are ready, you can then enable Azure cloud services to create an Azure Application Server and Client service.

Run the following procedure from the primary site server that has your exported certificates.

1. From the primary site server, open the Configuration Manager console and go to **Administration > Cloud Services > Azure Services**, and select **Configure Azure Services**.  

   > [! TIP]  
   > For more information about the configurations you make in the wizard, see [Start the Azure Services wizard](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard).  

2. On the Configure Azure Service page, specify a friendly **Name** for the service you're configuring, select **Cloud Management**, and then select **Next**.  
   
    Example:  Name = **Contoso Corp**

3. On the **App Properties** page, for **Web app**, select **Browse** to open the **Server App** dialog, and then select **Create**. Configure the following fields:
   - **Application Name**: Specify a friendly name for the app.
   - **HomePage URL**: This value isn't used by Configuration Manager but is required by Azure AD. By default, this value is https://ConfigMgrService.
   - **App ID URI**: This value needs to be unique in your Azure AD tenant. It is in the access token used by the Configuration Manager client to request access to the service. By default, this value is https://ConfigMgrService.

   Next, select **Sign in**, and specify an Azure Global Admin account. These credentials aren't saved by Configuration Manager. This persona doesn't require permissions in Configuration Manager and doesn't need to be the same account that runs the Azure Services Wizard.

   After sign-in, the results are displayed. Select **OK** to close the Create Server Application dialog and return to the App Properties page.

4. For **Native Client app**, select **Browse** to open the **Client app** dialog.

5. Select **Create** to open the **Create Client Application** dialog, and then configure the following fields:
   - **Application Name**: Specify a friendly name for the app.
   - **Reply URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default, this value is https://ConfigMgrClient.
   Next, select Sign in, and specify an Azure Global Admin account. Like the Web app, these credentials aren't saved and don't require permissions in Configuration Manager.
   
   After sign-in, the results are displayed. Select **OK** to close the Create Client Application dialog and return to the App Properties page. Then, select **Next** to continue.

6. On the **Configure Discovery Settings** page, check the box for **Enable Azure Active Directory User Discovery**, select **Next**, and then complete configuration of the Discovery dialogs for your environment.  

7. Continue through the Summary, Progress, and Completion pages, to complete and then close the wizard.  

   Azure Services for Azure AD User discovery is now enabled in Configuration Manager.  Leave the console open for now.

8. Open a browser and sign in to the [Azure portal](https://portal.azure.com/).

9. Select **All services > Azure Active Directory > App registrations**, and then:

   1. Select your Configuration Manager Server Application.   
   2. Go to **Settings > Required Permissions**, select **Grant Permissions**, and then select **Yes**.
   4. Go to **Settings > Required Permissions, select Grant Permissions**, and then select **Yes**.  

10. In the Configuration Manager console, go to **Administration > Overview > Azure Active Directory Tenants**, and then select your Tenant. Confirm that you can see your Server and Client applications in the **Applications** pane.

11. In the Configuration Manager console, go to **Administration > Overview > Cloud Services > Azure Services**, and select your Azure Service.  Then select **Run Full Discovery Now**. Select **Yes** to confirm the action.

12. On the primary site server, open the Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT.log** and look for the following entry to confirm that discovery is working:  *Successfully published UDX for Azure Active Directory users*

    By default, the log file is in %Program_Files%\Microsoft Configuration Manager\Logs.

    After the log entry is confirmed, you're ready to create your cloud management gateway and cloud distribution point.

## Create the cloud services in Azure
After you create the necessary certificates, you can then create the cloud management gateway (CMG) and cloud distribution point (CDP) in Azure.

**In this section of the tutorial you will**:
- Create the CDP cloud service
- Create the CMG cloud service
- Create DNS CNAME records for both services

### Create the CDP
Use this procedure to install a cloud distribution point as a service in Azure, using the *AzureManagementCert* and *ConfigMgrCloudDPServer* certificates.

1. On the primary site server, open the **Configuration Manager console > Administration > Overview > Cloud Services > Cloud Distribution Points**, and then select **Create Cloud Distribution Point**.

2. On the **General** page:  
   - Select the correct cloud environment **Azure environment**. This tutorial uses **AzurePublicCloud**.   
   - Select **Classic service deployment**  
   - For **Subscription ID**, copy and paste in your **Subscription ID** from the Azure Subscription that you saved during the procedure to [Upload the Azure Management certificate to Azure](#upload-the-azure-management-certificate-to-azure).  You can also sign in to [Azure](http://portal.azure.com/) to identify your Subscription ID.  
   - For **Management certificate**, select the PFX export of the Azure management certificate you created earlier in this tutorial, **C:\Certs\AzureManagementCert.pfx**.  Enter the password, select **OK**, and then select **Next**.  

3. On the **Settings** page, use the dropdown box to set your **Region**.

4. For **Certificate file**, browse to and select **C:\Certs\ConfigMgrCloudDPServer.pfx**. This file is the PFX export you previously created for the cloud distribution point Cloud Service role.  After you specify the password, the **Service name** and **Service FQDN** automatically fill in on the Settings page of the Wizard, based on the details in the .pfx certificate file.    

5. Select **Next**, review the values on the Alert page, and then select **Next**.

6. Review the **Summary**  page and select **Next** to create the cloud distribution point Cloud Service. Select **Close** to complete the Wizard.

7. In the Cloud Distribution Point node of the Configuration Manager console, you can now view the new service.

8. To view the status of the service in the Azure portal, open the **Cloud Services (classic)** blade.  Select the service to view more details.

### Create the CMG
Use this procedure to install a cloud management gateway as a service in Azure, using the *AzureManagementCert*, *ConfigMgrCloudCMServer*, and *TrustedRootCERT* certificates.  The CMG installs at the top-tier site of the hierarchy. In this tutorial, we continue to use the primary site, where certificates have been enrolled and exported.  

> [! TIP]  
> If you use public SSL certificates, you do not need to load the **TrustedRootCERT** certificate as Windows 10 devices already trust the public Certificate Authorities that issue public certificates.

1. On the primary site server, open the Configuration Manager console, and then go **Administration > Overview > Cloud Services > Cloud Management Gateway**, and then select **Create Cloud Management Gateway**.  

2. On the **General** page:
   - Select the correct cloud environment **Azure environment**. This tutorial uses **AzurePublicCloud**.   
   - Select **Classic service deployment**
   - For **Subscription ID**, copy and paste in your **Subscription ID** from the Azure Subscription that yous saved during the procedure to [Upload the Azure Management certificate to Azure](#upload-the-azure-management-certificate-to-azure.  You can also sign in to [Azure](http://portal.azure.com/) to identify your Subscription ID.
   - For **Management certificate**, select the PFX export of the Azure management certificate you created earlier in this tutorial, **C:\Certs\AzureManagementCert.pfx**.  Enter the password, select **OK**, and then select **Next**.  

3. On the **Settings** page, use the dropdown box to set your **Region**.

4. Confirm that the number of **VM Instances** you want to use.
The number of *VM Instances* allows a single Cloud Management Gateway (CMG) Cloud service to scale out to support more client connections. If unsure about the number to use, use the default value of one instance. After this service is created, you can use the Configuration Manager console to edit number of VM instances.  

5. For **Certificate file**, browse to and select **C:\Certs\ConfigMgrCloudCMServer.pfx**. This file is the PFX export you previously created for the cloud management gateway Cloud Service role.  After you specify the password, the **Service name** and **Service FQDN** automatically fill-in on the Settings page of the Wizard, based on the details in the .pfx certificate file.   

6. Select **Certificates**.

7. On the **Certificates uploaded to the cloud service** dialog, select **Add**, and then select **C:\Certs\TrustedRootCERT.cer**, the **Trusted Root Certificate** that you previously exported from a domain client. When the certificate is listed on the dialog box, select **OK** to return the Settings page of the Wizard.

   If you have multiple CAs in the chain, add them as Intermediate CAs using the same process. If multiple root CAs are required, you can add two, with a maximum of four subordinate CAs.

   > [! TIP]  
   > If you use a publicly issued SSL certificate, you do not need to load the trusted root certificate from your on-premises PKI.

8. Unless you publish a public CRL, uncheck the box for **Verify Client Certificate Revocation**.  Select **Next** to continue.

9. Review the values on the Alert page, and then select **Next**.

10. Review the **Summary** page  and click **Next** to create the cloud management gateway Cloud Service. Select **Close** to complete the Wizard.

11. In the Cloud Management Gateway node of the Configuration Manager console, you can now view the new service.

12. To view the status of the service in the Azure portal, open the **Cloud Services (classic)** blade.  Select the service to view more details.

### Create DNS CNAME records
Create DNS CNAME entries for both Azure services, the CMG and the CDP.  These entries enable your Windows 10 devices both inside and outside your corporate network to use name resolution to find the two cloud services in Azure.

The CNAME record example uses the following details:
- The company name is ***Contoso*** with a public DNS namespace of ***Contoso.com***.
- The CMG service name is ***TestIntuneCMG, which becomes ***TestIntuneCMG.CloudApp.Net*** in Azure
- The CDP service name is ***TestIntuneCDP, which becomes ***TestIntuneCDP.CloudApp.Net*** in Azure

CNAME record example for the CMG:  *TestIntuneCMG.contoso.com => TestIntuneCMG.cloudapp.net*  
- **When you use a third-party certificate provider** to issue certificates for the CMG and CDP, create external CNAME records.  For example:
  - *TestIntuneCMG.Contoso.com* that points to the Azure service of TestIntuneCMG.CloudApp.Net
  - *TestIntuneCDP.Contoso.com* that points to the Azure service of TestIntuneCDP.CloudApp.Net
- **When you use your own PKI** to issue the certificates, create CNAME records in your organizations internal DNS.

#### To Create DNS CNAMES for your internal DNS
To complete this procedure, you must use Domain Admin credentials.
Run this procedure two times. For the first run, specify the service name of your cloud management gateway. In this tutorial, we use *TestIntuneCMG*.  The second time through, specify the service name of your cloud distribution point. In this tutorial, we use *TestIntuneCDP*.  
1. On your domain controller open **Server Manager > Tools > DNS > Forward Lookup Zones**.

2. Right-click the forward lookup zone where you want to add the Alias resource record, and then click **New Alias (CNAME)**. The **New Resource Record** dialog box opens.

3. In **Alias name**, specify the name of the service. This is either **TestIntuneCMG** or **TestIntuneCDP**.
When you type a value for **Alias name**, the **Fully qualified domain name (FQDN)** autofills in the dialog box. For example, if your alias name is *TestIntuneCMG* and your domain is contoso.com, the value **TestIntuneCMG.contoso.com** is autofilled for you.

4. In **Fully qualified domain name (FQDN) for target host**, specify the FQDN of the service in Azure.  For example, if your Azure service name is *TestIntuneCMG*, specify *TestIntuneCMG.cloudapp.net*

5. Click **OK** to add the new record to the zone.

6. Run this procedure a second time to create the CNAME record for your second service. When complete, you should have created alias for both your CMG and CDP.  

## Configure the management point and clients to use the CMG
In the following procedures, you'll configure settings that enable management points and clients to use the cloud management gateway.

### Create and install the web server certificate on the management point

1. On the server that hosts the management point, run **certlm.msc** to start the Certificate Manager for the Local Computer.
2. In the Certificate Manager console, expand **Certificates - (Local Computer)**, and then select **Personal**.

3. Right-click **Certificates**, and then select **All Tasks > Request New Certificate**.

4. On the **Before You Begin** page, select **Next**.

5. If you see the **Select Certificate Enrollment Policy** page, select **Next**.

6. On the **Request Certificates** page, select **ConfigMgrCloudWebServer** from the list of certificates, and then select **More information is required to enroll for this certificate. Click here to configure setting to open the Certificate Properties**.

7. On the **Subject** tab, in the **Subject name** area, for **Type** select **Common name**. For **Value**, specify the internal DNS FQDN of your management point.  Then, select **Add**.
 Example:  If the management point server name is *contosoMP* and the domain is *contoso.com*, specify **contosoMP.contoso.com**

8. In the **Alternative name** area, for **Type** select **DNS**.  For **Value**, specify the internal DNS FQDN of your management point. Then, select **Add**.
9. Select **OK** to close the **Certificate Properties** dialog box.
10. On the **Request Certificates** page, select **ConfigMgrCloudWebServer** from the list of available certificates, and then choose Enroll.
11. After the certificate is installs, select Finish.

### Install the Client Authentication certificate to the management point
To support client communications, you must install the Client Authentication Certificate *(ConfigMgrWorkstationAuth)* on the primary site server and on the management point where you added the CMG connection point. Repeat this procedure on each applicable system.

1. On the server that hosts the management point with the CMG connection point, run **certlm.msc** to start the Certificate Manager for the Local Computer.
2. In the Certificate Manager console, expand **Certificates - (Local Computer)**, and then select **Personal**.

3. Right-click **Certificates**, and then select **All Tasks > Request New Certificate**.

4. On the **Before You Begin** page, select **Next**.

5. If you see the **Select Certificate Enrollment Policy** page, select **Next**.

6. On the **Request Certificates** page, select the **ConfigMgrWorkstationAuth** certificate from the list of displayed certificates, and then select **Enroll**.

7.  On the **Certificates Installation Results** page, wait until the certificate is installed, and then select **Finish**.
Close the Certificates console to complete the procedure.

### Create the CMG connection point
In the following procedure, you enable an existing management point for HTTPs, and then add a CMG connection point to the server.
1. In the Configuration Manager console, go to **Administration > Overview > Site Configuration > Servers and Site System Roles**, and select the server with the management point that will host the CMG connection point.

2. In the **Site System Roles** pane, right-click on the **Management point** Role Name, and select **Properties**.  

3. On the **General** tab select **HTTPS**, and then select **Allow Configuration Manager cloud management gateway traffic** and ensure the drop-down displays **Allow intranet and Internet connections**.  

4. Select **OK** to close the Properties of the management point.

5. In the **Servers and Site System Roles** pane, right-click on the server that hosts the management point you configured for HTTPS, and then select **Add Site System Role**.

6. Select **Next**> **Next**, and then select the **Cloud management gateway connection point**.  Select **Next** to continue.  

7. Review the default selections on the **Cloud management gateway connection point** page, ensure the correct CMG is selected. If you have multiple cloud management gateways, you can use the dropdown list to specify a different CMG. You can also change the CMG in use, after installation. Select **Next** to continue.

8. Select **Next** to start installation and then view the results on the Completion page.  Select **Close** to complete the installation.


### Configure Client Settings to direct clients to use the CMG
Use Client Settings to configure Configuration Manager clients to communicate with the CMG.   
1. Open the **Configuration Manager console > Administration > Overview > Client Settings > Create Custom Client Device Settings**.

2. For Name, specify a name to identify these settings enable co-management.
Example: **Co-mgmt device settings**

3. Select **Cloud Services**, and then select **Cloud Services** from the left navigation pane.
4. On the **Custom Device Setting** page, set the following settings to = **Yes**
   - Allow access to cloud distribution  
   - Automatically register new Windows 10 domain joined devices with Azure Active Directory
   - Enable clients to use a cloud management gateway

5. Select **OK** to save this configuration, and then use your organizations process to deploy the **Co-mgmt device settings** to applicable Windows 10 devices.


## Enable co-management in Configuration Manager
With certificates, site system roles, and client certificates and settings in place, you are ready to flip the switch and enable co-management of your Windows 10 devices from within the Configuration Manager console.  

1. In the Configuration Manager console, go to **Administration > Overview > Cloud Services > Co-management**.

2. On the Home tab, in the Manage group, select **Configure co-management** to open the Co-management Configuration Wizard.

3. On the Subscription page, select **Sign In** and sign in to your Intune tenant, and then select **Next**.

4. On the Enablement page, from the *Automatic enrollment in Intune* dropdown list, select one of the following options:
   - **Pilot** - Members of the collection you specify are automatically enrolled into Intune and can then be co-managed. You'll specify the collection on the *Staging* page of this wizard. This option allows you to test co-management on a subset of clients. You can then rollout co-management to additional clients using a phased approach. 

   - **All** - Co-management is enabled for all clients.
Next, select **Copy** to copy the *CCMSETUPCMD* command line for deploying the Configuration Manager client. Save this command line for use when you create an app in Intune that deploys the Configuration Manager client.  Select **Next**.

5. On the Workloads page, switch workloads to move them from Configuration Manager to one of the following, and then select **Next** to continue.  
   - **Pilot Intune** - Switches a workload only for the devices in the Pilot group.
   - **Intune** - Switches the associated workload for all co-managed Windows 10 devices.

   > [! IMPORTANT]  
   > Before you switch any workloads, make sure the corresponding workload in Intune is properly configured and deployed. Doing so ensures that workloads are always managed by one of the management tools for your devices.
6. On the Staging page, specify a collection to use for the **Pilot collection**, and then click **Next**.
The collection you specify is used as part of your phased rollout of co-management. You can change the collections in the pilot group at any time from the co-management properties.
7. On the Summary page, select **Next**, and then **Close** to complete the Wizard.  

With the completion of this procedure, co-management is enabled, and your Azure subscription and on-premises infrastructure is configured to support co-management.

To help ensure that Windows 10 devices that are currently only managed by Intune can be managed by co-management, create and deploy an app in Intune to install the Configuration Manager client.  

## Use Intune to deploy the Configuration Manager client  
After you enable co-management in the Configuration Manager console, use Intune to install Configuration Manager clients on Windows 10 devices that are enrolled with Intune.

### Create an Intune app to install the Configuration Manager client
1. From the primary site server, sign in to the [Azure portal](https://portal.azure.com/) and go to the **Intune > Client apps > Apps > Add**.
2. For **App type**: Select **Line-of-business app**.
3. Select **App package file**, and then browse to the location of the Configuration Manager file  **ccmsetup.msi**, and then select **Open > OK**.
For example, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*   
1. Select **App Information**, and then specify the following details:
- **Description**: Configuration Manager Client
- **Publisher**: Microsoft
- **Command-line arguments**:  *\<Specify the **CCMSETUPCMD** command line you saved from the Enablement page of the Co-management Configuration Wizard.  This command line includes the names of your cloud service and additional values that will enable devices to install the Configuration Manager client software.>*

   The command-line structure should resemble this example:
Example:  CCMSETUPCMD="CCMHOSTNAME=\<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/\<GUID> SMSSiteCode=\<YourSiteCode> AADRESOURCEURI=https://ConfigMgrService AADCLIENTAPPID=\<GUID>"

   > [! TIP]  
   > If you do not have the command line available, you can view the properties of *CoMgmtSettingsProd* in the Configuration Manager console to get a copy of the command line.    

5. Select **OK > Add**.  The app is created and becomes available in the Intune console. After the app is available, you assign it to groups to deploy the Configuration Manager client to Windows 10 devices.

### Assign the Intune app to install the Configuration Manager client
The following procedure deploys the app for installing the Configuration Manager client that you created in the previous procedure. When a user’s Windows 10 device that is managed by Intune installs this app and the Configuration Manager client, it's then managed by co-management.

1. Sign in to the [Azure portal](https://portal.azure.com/).  Select **All services > Intune > Client apps > Apps**, and then select **ConfigMgr Client Setup Bootstrap**, the app you created to deploy the Configuration Manager client.  

2. Select **Assignments > Add group**.  Set **Assignment type** as **Required**, and then use **Included Groups** and **Excluded Groups** to set the Azure Active Directory (AD) groups that have users and devices that you want to participate in co-management.

3. Select **OK** and then **Save** the configuration.
The app is now required by the users and devices you assigned it to. After the app installs the Configuration Manager client on a device, it's managed by co-management.

## Configure auto-enrollment of devices to Intune   
The following procedure configures auto-enrollment for Intune to enable co-management for Configuration Manager clients.

Automatic enrollment lets users enroll their Windows 10 devices. To enroll, users add their work account to their personally owned devices or join a corporate-owned device to Azure Active Directory.

1. Sign in to the [Azure portal](https://portal.azure.com/) and select **Azure Active Directory > Mobility (MDM and MAM) > Microsoft Intune**.  

2. Configure **MDM user scope**. Specify one of the following to configure which users’ devices are managed by Microsoft Intune and accept the defaults for the URL values.
   - **Some** - Select the **Groups** that can automatically enroll their Windows 10 devices
   - **All** - All users can automatically enroll their Windows 10 devices
when set to **None**, MDM automatic enrollment is disabled.

   > [!IMPORTANT]  
   > If both **MAM user scope** and automatic MDM enrollment (**MDM user scope**) are enabled for a group, only MAM is enabled. Only MAM is added for users in that group when they workplace join personal device. Devices are not automatically MDM enrolled.

3. Select **Save** to complete configuration of automatic enrollment.

4. Return to **Mobility (MDM and MAM)** and then select **Microsoft Intune Enrollment**.

5. For MDM user scope, select **All**, and then **Save**.

## Next Steps
After completing the configurations for co-management, you can use co-management to manage devices of users when they enroll their devices with Intune (which installs  the Configuration Manager client), or when they sign in to the company portal on a domain joined computer that runs the Configuration Manager client.

This tutorial for configuring co-management is complete.  

- View the [Co-management dashboard](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard) to review the status of co-managed devices
