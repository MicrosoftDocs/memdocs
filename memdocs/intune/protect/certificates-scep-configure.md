---
title: Configure infrastructure to support SCEP certificate profiles with Microsoft Intune - Azure | Microsoft Docs
description: To use SCEP in Microsoft Intune, configure your on-premises AD domain, create a certification authority, set up the NDES server, and install the Intune Certificate Connector. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/07/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Configure infrastructure to support SCEP with Intune

Intune supports use of the Simple Certificate Enrollment Protocol (SCEP) to [authenticate connections to your apps and corporate resources](certificates-configure.md). SCEP uses the Certification Authority (CA) certificate to secure the message exchange for the Certificate Signing Request (CSR). When your infrastructure supports SCEP, you can use Intune *SCEP certificate* profiles (a type of device profile in Intune) to deploy the certificates to your devices. The Microsoft Intune Certificate Connector is required to use SCEP certificate profiles with Intune when using an Active Directory Certificate Services Certification Authority. The connector isn't required when using [3rd party Certification Authorities](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration). 

The information in this article can help you configure your infrastructure to support SCEP when using Active Directory Certificate Services. After your infrastructure is configured, you can [create and deploy SCEP certificate profiles](certificates-profile-scep.md) with Intune.

> [!TIP]
> Intune also supports use of [Public Key Cryptography Standards #12 certificates](certficates-pfx-configure.md).

## Prerequisites for using SCEP for certificates

Before you proceed, ensure you've [created and deployed a *trusted certificate* profile](certificates-configure.md#export-the-trusted-root-ca-certificate) to devices that will use SCEP certificate profiles. SCEP certificate profiles directly reference the trusted certificate profile that you use to provision devices with a Trusted Root CA certificate.

### Servers and server roles

The following on-premises infrastructure must run on servers that are domain-joined to your Active Directory, with the exception of the Web Application Proxy Server.

- **Certification Authority** – Use a Microsoft Active Directory Certificate Services Enterprise Certification Authority (CA) that runs on an Enterprise edition of Windows Server 2008 R2 with service pack 1, or later. The version of Windows Server you use must remain in support by Microsoft. A Standalone CA is not supported. For more information, see [Install the Certification Authority](https://technet.microsoft.com/library/jj125375.aspx). If your CA runs Windows Server 2008 R2 SP1, you must [install the hotfix from KB2483564](https://support.microsoft.com/kb/2483564/).

- **NDES server role** – You must configure a Network Device Enrollment Service (NDES) server role on Windows Server 2012 R2 or later. In a later section of this article, we guide you through [installing NDES](#set-up-ndes).

  - The server that hosts NDES must be domain-joined and in the same forest as your Enterprise CA.
  - You can't use NDES that’s installed on the server that hosts the Enterprise CA.
  - You’ll install the Microsoft Intune Certificate connector on the same server that hosts NDES.

  To learn more about NDES, see [Network Device Enrollment Service Guidance](https://technet.microsoft.com/library/hh831498.aspx) in the Windows Server documentation, and [Using a Policy Module with the Network Device Enrollment Service](https://technet.microsoft.com/library/dn473016.aspx).

- **Microsoft Intune Certificate Connector** – The Microsoft Intune Certificate Connector is required to use SCEP certificate profiles with Intune. This article will guide you through [installing this connector](#install-the-intune-certificate-connector).

  The connector supports Federal Information Processing Standard (FIPS) mode. FIPS isn’t required, but when it's enabled, you can issue and revoke certificates.
  - The connector must run on the same server as the NDES server role, a server that runs Windows Server 2012 R2 or later.
  - The .NET 4.5 Framework is required by the connector and is automatically included with Windows Server 2012 R2.
  - Internet Explorer Enhanced Security Configuration [must be disabled on the server that hosts NDES](https://technet.microsoft.com/library/cc775800(v=WS.10).aspx) and the Microsoft Intune Certificate Connector.

The following on-premises infrastructure is optional:

To allow devices on the internet to get certificates, you need to publish your NDES URL external to your corporate network. You can use either the Azure AD Application Proxy, the Web Application Proxy Server, or another reverse proxy.

- **Azure AD Application Proxy** (optional) – You can use the Azure AD Application Proxy instead of a dedicated Web Application Proxy (WAP) Server to publish your NDES URL to the internet. This allows both intranet and internet facing devices to get certificates. For more information, see [How to provide secure remote access to on-premises applications](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

- **Web Application Proxy Server** (optional) - Use a server that runs Windows Server 2012 R2 or later as a Web Application Proxy (WAP) server to publish your NDES URL to the internet.  This allows both intranet and internet facing devices to get certificates.

  The server that hosts WAP [must install an update](https://blogs.technet.com/b/ems/archive/2014/12/11/hotfix-large-uri-request-in-web-application-proxy-on-windows-server-2012-r2.aspx) that enables support for the long URLs that are used by the Network Device Enrollment Service. This update is included with the [December 2014 update rollup](https://support.microsoft.com/kb/3013769), or individually from [KB3011135](https://support.microsoft.com/kb/3011135).

  The WAP server must have an SSL certificate that matches the name that’s published to external clients and trust the SSL certificate that’s used on the computer that hosts the NDES service. These certificates enable the WAP server to terminate the SSL connection from clients and create a new SSL connection to the NDES service.

  For more information, see [Plan certificates for WAP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11)#plan-certificates) and [general information about WAP servers](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn584113(v=ws.11)).

### Accounts

- **NDES service account** - Before you set up NDES, identify a domain user account to use as the NDES service account. You’ll specify this account when you configure templates on your issuing CA, before you configure NDES.

  This account must have the following rights on the server that hosts NDES:

  - **Logon Locally**
  - **Logon as a Service**
  - **Logon as a batch job**

  For more information, see [Create a domain user account to act as the NDES service account](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)#to-create-a-domain-user-account-to-act-as-the-ndes-service-account).

- **Access to the computer that hosts the NDES service** - You'll need a domain user account with permissions to install and configure Windows server roles on the server where you install NDES.

- **Access to the certification authority** - You'll need a domain user account that has rights to manage your certification authority.

### Network requirements

We recommend publishing the NDES service through a reverse proxy, such as the [Azure AD application proxy, Web Access Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-publish/), or a third-party proxy. If you don't use a reverse proxy, then allow TCP traffic on port 443 from all hosts and IP addresses on the internet to the NDES service.

Allow all ports and protocols necessary for communication between the NDES service and any supporting infrastructure in your environment. For example, the computer that hosts the NDES service needs to communicate with the CA, DNS servers, domain controllers, and possibly other services or servers within your environment, like Configuration Manager.

### Certificates and templates

The following certificates and templates are used when you use SCEP.

|Object    |Details    |
|----------|-----------|
|**SCEP Certificate Template**         |Template you’ll configure on your issuing CA used to fullfil the devices SCEP requests. |
|**Client authentication certificate** |Requested from your issuing CA or public CA.<br /> You install this certificate on the computer that hosts the NDES service and it's used by the Intune Certificate Connector.<br /> If the certificate has the *client* and *server authentication* key usages set (**Enhanced Key Usages**) on the CA template that you use to issue this certificate. You can then use the same certificate for server and client authentication. |
|**Server authentication certificate** |Web Server certificate requested from your issuing CA or public CA.<br /> You install and bind this SSL certificate in IIS on the computer that hosts NDES.<br />If the certificate has the *client* and *server authentication* key usages set (**Enhanced Key Usages**) on the CA template that you use to issue this certificate. You can then use the same certificate for server and client authentication. |
|**Trusted Root CA certificate**       |To use a SCEP certificate profile, devices must trust your Trusted Root Certification Authority (CA). Use a *trusted certificate profile* in Intune to provision the Trusted Root CA certificate to users and devices. <br/><br/> **-**  Use a single Trusted Root CA certificate per operating system platform and associate that certificate with each trusted certificate profile you create. <br /><br /> **-**  You can use additional Trusted Root CA certificates when needed. For example, you might use additional certificates to provide a trust to a CA that signs the server authentication certificates for your Wi-Fi access points. Create additional Trusted Root CA certificates for issuing CAs.  In the SCEP certificate profile you create in Intune, be sure to specify the Trusted Root CA profile for the issuing CA.<br/><br/> For information about the trusted certificate profile, see [Export the trusted root CA certificate](certificates-configure.md#export-the-trusted-root-ca-certificate) and [Create trusted certificate profiles](certificates-configure.md#create-trusted-certificate-profiles) in *Use certificates for authentication in Intune*. |

## Configure the certification authority

In the following sections, you’ll:

- Configure and publish the required template for NDES
- Set the required permissions for certificate revocation.

The following sections require knowledge of Windows Server 2012 R2 or later, and of Active Directory Certificate Services (AD CS).

### Access your Issuing CA

1. Sign in to your issuing CA with a domain account with rights sufficient to manage the CA.

2. Open the Certification Authority Microsoft Management Console (MMC). Either **Run** 'certsrv.msc' or in **Server Manager**, click **Tools**, and then click **Certification Authority**.

3. Select the **Certificate Templates** node, click **Action** > **Manage**.

### Create the SCEP certificate template

1. Create a v2 Certificate Template (with Windows 2003 compatibility) for use as the SCEP certificate template. You can:

   - Use the *Certificate Templates* snap-in to create a new custom template.
   - Copy an existing template (like the User template) and then update the copy to use as the NDES template.

2. Configure the following settings on the specified tabs of the template:

   - **General**:

     - Uncheck **Publish certificate in Active Directory**.
     - Specify a friendly **Template display name** so you can identify this template later.

   - **Subject Name**:

     - Select **Supply in the request**. Security is enforced by the Intune policy module for NDES.

       ![Template, subject name tab](./media/certificates-scep-configure/scep-ndes-subject-name.jpg)

   - **Extensions**:

     - Ensure that **Description of Application Policies** includes **Client Authentication**.

       > [!IMPORTANT]
       > Only add the application policies that you require. Confirm your choices with your security admins.

     - For iOS/iPadOS and macOS certificate templates, also edit **Key Usage** and make sure **Signature is proof of origin** isn't selected.

     ![Template, extensions tab](./media/certificates-scep-configure/scep-ndes-extensions.jpg)  

   - **Security**:

     - Add the **NDES service account**. This account requires **Read** and **Enroll** permissions to this template.

     - Add additional Accounts for Intune administrators who will create SCEP profiles. These accounts require **Read** permissions to the template to enable these admins to browse to this template while creating SCEP profiles.

     ![Template, security tab](./media/certificates-scep-configure/scep-ndes-security.jpg)

   - **Request Handling**:

     The following image is an example. Your configuration might vary.  

     ![Template, request handling tab](./media/certificates-scep-configure/scep-ndes-request-handling.png)

   - **Issuance Requirements**:

     The following image is an example. Your configuration might vary.

     ![Template, issuance requirements tab](./media/certificates-scep-configure/scep-ndes-issuance-reqs.jpg)

3. Save the certificate template.

### Create the client certificate template

The Intune Certificate Connector requires a certificate with the *Client Authentication* Enhanced Key Usage and Subject name equal to the FQDN of the machine where the connector is installed. A template with the following properties is required:

- **Extensions** > **Application Policies** must contain **Client Authentication**
- **Subject name** > **Supply in the request**.

If you already have a template that includes these properties, you can reuse it, otherwise create a new template by either duplicating an existing one or creating a custom template.

### Create the server certificate template

Communications between managed devices and IIS on the NDES server use HTTPS, which requires use of a certificate. You can use the **Web Server** certificate template to issue this certificate. Or, if you prefer to have a dedicated template, the following properties are required:

- **Extensions** > **Application Policies** must contain **Server Authentication**
- **Subject name** > **Supply in the request**.

> [!NOTE]
> If you have a certificate that satisfies both requirements from the client and server certificate templates, you can use a single certificate for both IIS and the Intune Certificate connector.

### Grant permissions for certificate revocation

For Intune to be able to revoke certificates that are no longer required, you must grant permissions in the Certificate Authority.

On the Intune Certificate Connector, you can either use the NDES server **system account** or a specific account such as the **NDES service account**.

1. On your Certificate Authority console, Right-click the CA name and select **Properties**.

2. In **Security** tab, click **Add**.

3. Grant **Issue and Manage Certificates** permission:

   - If you opt to use the NDES server **system account**, provide the permissions to the NDES server.
   - If you opt to use the **NDES service account**, provide permissions for that account instead.

### Modify the validity period of the certificate template

It's optional to modify the validity period of the certificate template.  

After you [create the SCEP certificate template](#create-the-scep-certificate-template), you can edit the template to review the **Validity period** on the **General** tab.

By default, Intune uses the value configured in the template. However, you can configure the CA to allow the requester to enter a different value, and that value can be set from within the Intune console.

> [!IMPORTANT]
> For iOS/iPadOS and macOS, always use a value set in the template.

#### To configure a value that can be set from within the Intune console

1. On the CA, run the following commands:

   -**certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**
   -**net stop certsvc**
   -**net start certsvc**

2. On the issuing CA, use the Certification Authority snap-in to publish the certificate template. Select the **Certificate Templates** node, select **Action** > **New** > **Certificate Template to Issue**, and then select the certificate template you created in the previous section.

3. Validate that the template has published by viewing it in the **Certificate Templates** folder.

## Set up NDES

The following procedures can help you configure the Network Device Enrollment Service (NDES) for use with Intune. For more information about NDES, see [Network Device Enrollment Service Guidance](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v%3dws.11)).

### Install the NDES service

1. On the server that will host your NDES service, sign in as an **Enterprise Administrator**, and then use the [Add Roles and Features Wizard](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)) to install NDES:

   1. In the Wizard, select **Active Directory Certificate Services** to gain access to the AD CS Role Services. Select **Network Device Enrollment Service**, uncheck **Certification Authority**, and then complete the wizard.

      > [!TIP]
      > In **Installation progress**, don't select **Close**. Instead, select the **Configure Active Directory Certificate Services on the destination server** link. The **AD CS Configuration** wizard opens, which you use for the next procedure in this article, *Configure the NDES service*. After AD CS Configuration opens, you can close the Add Roles and Features wizard.

   2. When NDES is added to the server, the wizard also installs IIS. Confirm that IIS has the following configurations:

      - **Web Server** > **Security** > **Request Filtering**
      - **Web Server** > **Application Development** > **ASP.NET 3.5**

        Installing ASP.NET 3.5 installs .NET Framework 3.5. When installing .NET Framework 3.5, install both the core **.NET Framework 3.5** feature and **HTTP Activation**.

      - **Web Server** > **Application Development** > **ASP.NET 4.5**

        Installing ASP.NET 4.5 installs .NET Framework 4.5. When installing .NET Framework 4.5, install the core **.NET Framework 4.5** feature, **ASP.NET 4.5**, and the **WCF Services** > **HTTP Activation** feature.

      - **Management Tools** > **IIS 6 Management Compatibility** > **IIS 6 Metabase Compatibility**
      - **Management Tools** > **IIS 6 Management Compatibility** > **IIS 6 WMI Compatibility**
      - On the server, add the NDES service account as a member of the local **IIS_IUSR** group.

2. On the computer that hosts the NDES service, run the following command in an elevated command prompt. The following command sets the SPN of the NDES Service account:

   `setspn -s http/<DNS name of the computer that hosts the NDES service> <Domain name>\<NDES Service account name>`

   For example, if the computer that hosts the NDES service is named **Server01**, your domain is **Contoso.com**, and the service account is **NDESService**, use:

   `setspn –s http/Server01.contoso.com contoso\NDESService`  

### Configure the NDES service

1. On the computer that hosts the NDES service, open the **AD CS Configuration** wizard, and then make the following updates:

   > [!TIP]
   > If you're continuing on from the last procedure and clicked the **Configure Active Directory Certificate Services on the destination server** link, this wizard should already be open. Otherwise, open Server Manager to access the post-deployment configuration for Active Directory Certificate Services.

   - In **Role Services**, select the **Network Device Enrollment Service**.
   - In **Service Account for NDES**, specify the NDES Service Account.
   - In **CA for NDES**, click **Select**, and then select the issuing CA where you configured the certificate template.
   - In **Cryptography for NDES**, set the key length to meet your company requirements.
   - In **Confirmation**, select **Configure** to complete the wizard.

2. After the wizard completes, update the following registry key on the computer that hosts the NDES service:

   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP\`

   To update this key, identify the certificate templates' **Purpose** (found on its **Request Handling** tab). Then, update the corresponding registry entry by replacing the existing data with the name of the certificate template (not the display name of the template) that you specified when you [created the certificate template](#create-the-scep-certificate-template).

   The following table maps the certificate template purpose to the values in the registry:

   |Certificate template Purpose (On the Request Handling tab)|Registry value to edit|Value seen in the Intune admin console for the SCEP profile|
   |------------------------|-------------------------|---|
   |Signature               |SignatureTemplate        |Digital Signature |
   |Encryption              |EncryptionTemplate       |Key Encipherment  |
   |Signature and encryption|GeneralPurposeTemplate   |Key Encipherment <br/> Digital Signature |

   For example, if the Purpose of your certificate template is **Encryption**, then edit the **EncryptionTemplate** value to be the name of your certificate template.

3. Configure IIS request filtering to add support in IIS for the long URLs (queries) that the NDES service receives.

   1. In IIS manager, select **Default Web Site** > **Request Filtering** > **Edit Feature Setting** to open the **Edit Request Filtering Settings** page.

   2. Configure the following settings:

      - **Maximum URL length (Bytes)** = 65534
      - **Maximum query string (Bytes)** = 65534

   3. Select **OK** to save this configuration and close IIS manager.

   4. Validate this configuration by viewing the following registry key to confirm it has the indicated values:

      `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters`

      The following values are set as DWORD entries:

      - Name: **MaxFieldLength**, with a decimal value of **65534**
      - Name: **MaxRequestBytes**, with a decimal value of **65534**

4. Restart the server that hosts the NDES service. Don't use **iisreset**; iireset doesn't complete the required changes.

5. Browse to *http://*Server_FQDN*/certsrv/mscep/mscep.dll*. You should see an NDES page similar to the following image:

   ![Test NDES](./media/certificates-scep-configure/scep-ndes-url.png)

   If the web address returns a **503 Service unavailable**, check the computers event viewer. This error commonly occurs when the application pool is stopped due to a missing [permission for the NDES service account](#accounts).
  
### Install and bind certificates on the server that hosts NDES

> [!TIP]
> In the following procedure, you can use a single certificate for both *server authentication* and *client authentication* when that certificate is configured to meet the criteria of both uses. The criteria for each use are described in steps 1 and 3 of the following procedure.

1. Request a **server authentication** certificate from your internal CA or public CA, and then install the certificate on the server.

   If the server uses an external and internal name for a single network address, then the server authentication certificate must have:

   - A **Subject Name** with an external public server name.
   - A **Subject Alternative Name** that includes the internal server name.

2. Bind the server authentication certificate in IIS:

   1. After installing the server authentication certificate, open **IIS Manager**, and select the **Default Web Site**. In the **Actions** pane, select **Bindings**.

   1. Select **Add**, set **Type** to **https**, and then confirm the port is **443**.
   
   1. For **SSL certificate**, specify the server authentication certificate.

3. On your NDES Server, request and install a **client authentication** certificate from your internal CA, or a public certificate authority.

   The client authentication certificate must have the following properties:

   - **Enhanced Key Usage**: This value must include **Client Authentication**.
   - **Subject Name**: The value must be equal to the DNS name of the server where you're installing the certificate (the NDES Server).

4. The server that hosts the NDES service is now ready to support the Intune Certificate Connector.

## Install the Intune Certificate Connector

The Microsoft Intune Certificate Connector installs on the server that runs your NDES service. It isn't supported to use NDES or the Intune Certificate Connector on the same server as your issuing Certification Authority (CA).

### To install the Certificate Connector

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Certificate connectors** > **Add**.

3. Download and save the connector for SCEP file. Save it to a location accessible from the server where you're going to install the connector.

   ![ConnectorDownload](./media/certificates-scep-configure/download-certificates-connector.png)

4. After the download completes, go to the server hosting the Network Device Enrollment Service (NDES) role. Then:

   1. Confirm that .NET 4.5 Framework is installed, as it's required by the Intune Certificate Connector. The .NET 4.5 Framework is automatically included with Windows Server 2012 R2 and newer versions.

   2. Run the installer (**NDESConnectorSetup.exe**). The installer also installs the policy module for NDES and the IIS Certificate Registration Point (CRP) Web Service. The CRP Web Service, *CertificateRegistrationSvc*, runs as an application in IIS.

      When you install NDES for standalone Intune, the CRP service automatically installs with the Certificate Connector.

5. When prompted for the client certificate for the Certificate Connector, choose **Select**, and select the **client authentication** certificate you installed on your NDES Server during step #3 of the procedure [Install and bind certificates on the server that hosts NDES](#install-and-bind-certificates-on-the-server-that-hosts-ndes) from earlier in this article.

   After you select the client authentication certificate, you're returned to the **Client Certificate for Microsoft Intune Certificate Connector** surface. Although the certificate you selected isn't shown, select **Next** to view the properties of that certificate. Select **Next**, and then **Install**.

> [!NOTE]
> The following changes must be made for GCC High tenants prior to launching the Intune Certificate Connector.
> 
> Make edits to the two config files listed below which will update the service endpoints for the GCC High environment. Notice that these updates change the URIs from **.com** to **.us** suffixes. There are a total of three URI updates, two updates within the NDESConnectorUI.exe.config configuration file, and one update in the NDESConnector.exe.config file.
> 
> - File Name: <install_Path>\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe.config
> 
>   Example: (%programfiles%\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe.config)
>   ```
>    <appSettings>
>        <add key="SignInURL" value="https://portal.manage.microsoft.us/Home/ClientLogon"/>
>        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
>        <add key="AccountPortalURL" value="https://manage.microsoft.us"/>
>    </appSettings>
>   ```
> 
> - File Name: <install_Path>\Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config
>
>   Example: (%programfiles%\Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config)
>    ```
>    <appSettings>
>        <add key="BaseServiceAddress" value="https://manage.microsoft.us/" />
>    ```
>
> If these edits are not completed, GCC High tenants will get the error: "Access Denied" "You are not authorized to view this page"

6. After the wizard completes, but before closing the wizard, **Launch the Certificate Connector UI**.

   If you close the wizard before you launch the Certificate Connector UI, you can reopen it by running the following command:

   *<install_Path>\NDESConnectorUI\NDESConnectorUI.exe*

7. In the **Certificate Connector** UI:

   1. Select **Sign In**, and enter your Intune service administrator credentials, or credentials for a tenant administrator with the global administration permission.

   2. The account you use must be assigned a valid Intune license.

   3. After you sign in, the Intune Certificate Connector downloads a certificate from Intune. This certificate is used for authentication between the connector and Intune. If the account you used doesn’t have an Intune license, the connector (NDESConnectorUI.exe) fails to get the certificate from Intune.  

      If your organization uses a proxy server and the proxy is needed for the NDES server to access the Internet, select **Use proxy server**. Then enter the proxy server name, port, and account credentials to connect.

   4. Select the **Advanced** tab, and then enter credentials for an account that has the **Issue and Manage Certificates** permission on your issuing Certificate Authority. **Apply** your changes.  

    5. You can now close the Certificate Connector UI.

8. Open a command prompt, enter **services.msc**, and then **Enter**. Right-click the **Intune Connector Service** > **Restart**.

To validate that the service is running, open a browser, and enter the following URL. It should return a **403** error: `https://<FQDN_of_your_NDES_server>/certsrv/mscep/mscep.dll`

> [!NOTE]
> The Intune Certificate Connector supports TLS 1.2. If the server that hosts the connector supports TLS 1.2, then TLS 1.2 is used. If the server doesn't support TLS 1.2, then TLS 1.1 is used. Currently, TLS 1.1 is used for authentication between the devices and server.

## Next steps

[Create a SCEP certificate profile](certificates-profile-scep.md)  
[Troubleshoot issues for the Intune certificate connector](troubleshoot-certificate-connector-events.md)
