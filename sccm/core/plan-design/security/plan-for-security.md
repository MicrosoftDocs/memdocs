---
title: Plan for security
titleSuffix: Configuration Manager
description: Get best practices and other information about security in Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Plan for security in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes the concepts for you to consider when planning for security with your Configuration Manager implementation. It includes the following sections:  

- [Plan for certificates (self-signed and PKI)](#BKMK_PlanningForCertificates)  
    - [Cryptography: Next Generation (CNG) certificates](#bkmk_plan-cng)  
    - [Enhanced HTTP](#bkmk_plan-ehttp)  
    - [Certificates for CMG and CDP](#bkmk_plan-cmgcdp)  
    - [The site server signing certificate (self-signed)](#bkmk_plansitesign)  
    - [PKI certificate revocation](#BKMK_PlanningForCRLs)  
    - [The PKI trusted root certificates and the certificate issuers](#BKMK_PlanningForRootCAs)  
    - [PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection)  
    - [A transition strategy for PKI certificates and internet-based client management](#BKMK_PlanningForPKITransition)  

- [Plan for the trusted root key](#BKMK_PlanningForRTK)  

- [Plan for signing and encryption](#BKMK_PlanningForSigningEncryption)  

- [Plan for role-based administration](#BKMK_PlanningForRBA)  

- [Plan for Azure Active Directory](#bkmk_planazuread)  

- [Plan for SMS Provider authentication](#bkmk_auth)



##  <a name="BKMK_PlanningForCertificates"></a> Plan for certificates (self-signed and PKI)  

 Configuration Manager uses a combination of self-signed certificates and public key infrastructure (PKI) certificates.  

 Use PKI certificates whenever possible. For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements). When Configuration Manager requests PKI certificates during enrollment for mobile devices, you must use Active Directory Domain Services and an enterprise certification authority. For all other PKI certificates, deploy and manage them independently from Configuration Manager. 

 PKI certificates are required when client computers connect to internet-based site systems. Some scenarios with the cloud management gateway and cloud distribution point also require PKI certificates. For more information, see [Manage clients on the internet](/sccm/core/clients/manage/manage-clients-internet).

 When you use a PKI, you can also use IPsec to help secure the server-to-server communication between site systems in a site, between sites, and for other data transfer between computers. Implementation of IPsec is independent from Configuration Manager.  

 When PKI certificates aren't available, Configuration Manager automatically generates self-signed certificates. Some certificates in Configuration Manager are always self-signed. In most cases, Configuration Manager automatically manages the self-signed certificates, and you don't have to take additional action. One example is the site server signing certificate. This certificate is always self-signed. It makes sure that the policies that clients download from the management point were sent from the site server and weren't tampered with.  


### <a name="bkmk_plan-cng"></a> Cryptography: Next Generation (CNG) certificates  

 Configuration Manager supports Cryptography: Next Generation (CNG) certificates. Configuration Manager clients can use PKI client authentication certificate with private key in CNG Key Storage Provider (KSP). With KSP support, Configuration Manager clients support hardware-based private key, such as TPM KSP for PKI client authentication certificates. For more information, see [CNG certificates overview](/sccm/core/plan-design/network/cng-certificates-overview).


### <a name="bkmk_plan-ehttp"></a> Enhanced HTTP  

 Using HTTPS communication is recommended for all Configuration Manager communication paths, but is challenging for some customers due to the overhead of managing PKI certificates. The introduction of Azure Active Directory (Azure AD) integration reduces some but not all of the certificate requirements. Starting in version 1806, you can enable the site to use **Enhanced HTTP**. This configuration supports HTTPS on site systems by using a combination of self-signed certificates and Azure AD. It doesn't require PKI. For more information, see [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).  


### <a name="bkmk_plan-cmgcdp"></a> Certificates for CMG and CDP

Managing clients on the internet via the cloud management gateway (CMG) and cloud distribution point (CDP) requires the use of certificates. The number and type of certificates varies depending upon your specific scenarios. For more information, see the following articles:
- [Certificates for the cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)  
- [Certificates for the cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_certs)  


### <a name="bkmk_plansitesign"></a> Plan for the site server signing certificate (self-signed)  

 Clients can securely get a copy of the site server signing certificate from Active Directory Domain Services and from client push installation. If clients can't get a copy of this certificate by one of these mechanisms, install it when you install the client. This process is especially important if the client's first communication with the site is with an internet-based management point. Because this server is connected to an untrusted network, it's more vulnerable to attack. If you don't take this additional step, clients automatically download a copy of the site server signing certificate from the management point.  

 Clients can't securely get a copy of the site server certificate in the following scenarios:  

 - You don't install the client by using client push, and:  

    - You haven't extended the Active Directory schema for Configuration Manager.  

    - You haven't published the client's site to Active Directory Domain Services.  

    - The client is from an untrusted forest or a workgroup.  

 - You're using internet-based client management and you install the client when it's on the internet.  

#### To install clients with a copy of the site server signing certificate  

1.  Locate the site server signing certificate on the primary site server. The certificate is stored in the **SMS** certificate store of Windows. It has the Subject name **Site Server** and the friendly name, **Site Server Signing Certificate**.  

2.  Export the certificate without the private key, store the file securely, and access it only from a secured channel.  

3.  Install the client by using the following client.msi property: `SMSSIGNCERT=<full path and file name>`  


###  <a name="BKMK_PlanningForCRLs"></a> Plan for PKI certificate revocation  

When you use PKI certificates with Configuration Manager, plan for use of a certificate revocation list (CRL). Devices use the CRL to verify the certificate on the connecting computer. The CRL is a file that a certificate authority (CA) creates and signs. It has a list of certificates that the CA has issued but revoked. When a certificate administrator revokes certificates, its thumbprint is added to the CRL. For example, if an issued certificate is known or suspected to be compromised.

> [!IMPORTANT]  
>  Because the location of the CRL is added to a certificate when a CA issues it, ensure that you plan for the CRL before you deploy any PKI certificates that Configuration Manager uses.  

IIS always checks the CRL for client certificates, and you can't change this configuration in Configuration Manager. By default, Configuration Manager clients always check the CRL for site systems. Disable this setting by specifying a site property and by specifying a CCMSetup property.  

Computers that use certificate revocation checking but can't locate the CRL behave as if all certificates in the certification chain are revoked. This behavior is because they can't verify if the certificates are in the list. In this scenario, all connections fail that require certificates and use a CRL.  

Checking the CRL every time that a certificate is used offers more security against using a certificate that's revoked. Although it introduces a connection delay and additional processing on the client. Your organization may require this additional security check for clients on the internet or an untrusted network.  

Consult your PKI administrators before you decide whether Configuration Manager clients must check the CRL. Then consider keeping this option enabled in Configuration Manager when both of the following conditions are true:  

-   Your PKI infrastructure supports a CRL, and it's published where all Configuration Manager clients can locate it. These clients might include devices on the internet, and ones in untrusted forests.  

-   The requirement to check the CRL for each connection to a site system that's configured to use a PKI certificate is greater than the following requirements:  
    - Faster connections  
    - Efficient processing on the client  
    - The risk of clients failing to connect to servers if they can't locate the CRL  


###  <a name="BKMK_PlanningForRootCAs"></a> Plan for the PKI trusted root certificates and the certificate issuers list  

If your IIS site systems use PKI client certificates for client authentication over HTTP, or for client authentication and encryption over HTTPS, you might have to import root CA certificates as a site property. Here are the two scenarios:  

-   You deploy operating systems by using Configuration Manager, and the management points only accept HTTPS client connections.  

-   You use PKI client certificates that don't chain to a root certificate that the management points trust.  

    > [!NOTE]  
    >  When you issue client PKI certificates from the same CA hierarchy that issues the server certificates that you use for management points, you don't have to specify this root CA certificate. However, if you use multiple CA hierarchies and you aren't sure whether they trust each other, import the root CA for the clients' CA hierarchy.  

If you must import root CA certificates for Configuration Manager, export them from the issuing CA or from the client computer. If you export the certificate from the issuing CA that's also the root CA, make sure you don't export the private key. Store the exported certificate file in a secure location to prevent tampering. You need access to the file when you set up the site. If you access the file over the network, make sure the communication is protected from tampering by using IPsec.  

If any root CA certificate that you import is renewed, you must import the renewed certificate.  

These imported root CA certificates and the root CA certificate of each management point create the certificate issuers list that Configuration Manager computers use in the following ways:  

-   When clients connect to management points, the management point verifies that the client certificate is chained to a trusted root certificate in the site's certificate issuers list. If it doesn't, the certificate is rejected, and the PKI connection fails.  

-   When clients select a PKI certificate and have a certificate issuers list, they select a certificate that chains to a trusted root certificate in the certificate issuers list. If there's no match, the client doesn't select a PKI certificate. For more information, see [Plan for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="BKMK_PlanningForClientCertificateSelection"></a> Plan for PKI client certificate selection  

 If your IIS site systems use PKI client certificates for client authentication over HTTP or for client authentication and encryption over HTTPS, plan for how Windows clients select the certificate to use for Configuration Manager.  

> [!NOTE]  
>  Some devices don't support a certificate selection method. Instead, they automatically select the first certificate that fulfills the certificate requirements. For example, clients on Mac computers and mobile devices don't support a certificate selection method.  

In many cases, the default configuration and behavior is sufficient. The Configuration Manager client on Windows computers filters multiple certificates by using these criteria in this order:  

1.  The certificate issuers list: The certificate chains to a root CA that's trusted by the management point.  

2.  The certificate is in the default certificate store of **Personal**.  

3.  The certificate is valid, not revoked, and not expired. The validity check also verifies that the private key is accessible.  

4.  The certificate has client authentication capability, or it's issued to the computer name.  

5.  The certificate has the longest validity period.  

Configure clients to use the certificate issuers list by using the following mechanisms:  

-   Publish it with Configuration Manager site information to Active Directory Domain Services.  

-   Install clients by using client push.  

-   Clients download it from the management point after they're successfully assigned to their site.  

-   Specify it during client installation as a CCMSetup client.msi property of CCMCERTISSUERS.  

Clients that don't have the certificate issuers list when they're first installed and aren't yet assigned to the site skip this check. When clients do have the certificate issuers list and don't have a PKI certificate that chains to a trusted root certificate in the certificate issuers list, certificate selection fails. Clients don't continue with the other certificate selection criteria.  

In most cases, the Configuration Manager client correctly identifies a unique and appropriate PKI certificate. However, when this behavior isn't the case, instead of selecting the certificate based on the client authentication capability, you can set up two alternative selection methods:  

- A partial string match on the client certificate subject name. This method is a case-insensitive match. It's appropriate if you're using the fully qualified domain name (FQDN) of a computer in the subject field and want the certificate selection to be based on the domain suffix, for example **contoso.com**. However, you can use this selection method to identify any string of sequential characters in the certificate subject name that differentiates the certificate from others in the client certificate store.  

  > [!NOTE]
  >  You can't use the partial string match with the subject alternative name (SAN) as a site setting. Although you can specify a partial string match for the SAN by using CCMSetup, it'll be overwritten by the site properties in the following scenarios:  
  > 
  > - Clients retrieve site information that's published to Active Directory Domain Services.  
  >   -   Clients are installed by using client push installation.  
  > 
  >   Use a partial string match in the SAN only when you install clients manually and when they don't retrieve site information from Active Directory Domain Services. For example, these conditions apply to internet-only clients.  

- A match on the client certificate subject name attribute values or the subject alternative name (SAN) attribute values. This method is a case-sensitive match. It's appropriate if you're using an X500 distinguished name or equivalent object ddentifiers (OIDs) in compliance with RFC 3280, and you want the certificate selection to be based on the attribute values. You can specify only the attributes and their values that you require to uniquely identify or validate the certificate and differentiate the certificate from others in the certificate store.  

The following table shows the attribute values that Configuration Manager supports for the client certificate selection criteria.  

|OID Attribute|Distinguished name attribute|Attribute definition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domain component|  
|1.2.840.113549.1.9.1|E or E-mail|Email address|  
|2.5.4.3|CN|Common name|  
|2.5.4.4|SN|Subject name|  
|2.5.4.5|SERIALNUMBER|Serial number|  
|2.5.4.6|C|Country code|  
|2.5.4.7|L|Locality|  
|2.5.4.8|S or ST|State or province name|  
|2.5.4.9|STREET|Street address|  
|2.5.4.10|O|Organization name|  
|2.5.4.11|OU|Organizational unit|  
|2.5.4.12|T or Title|Title|  
|2.5.4.42|G or GN or GivenName|Given name|  
|2.5.4.43|I or Initials|Initials|  
|2.5.29.17|(no value)|Subject Alternative Name|  

If more than one appropriate certificate is located after the selection criteria are applied, you can override the default configuration to select the certificate that has the longest validity period and instead, specify that no certificate is selected. In this scenario, the client won't be able to communicate with IIS site systems with a PKI certificate. The client sends an error message to its assigned fallback status point to alert you to the certificate selection failure so that you can change or refine your certificate selection criteria. The client behavior then depends on whether the failed connection was over HTTPS or HTTP:  

-   If the failed connection was over HTTPS: The client tries to connect over HTTP and uses the client self-signed certificate.  

-   If the failed connection was over HTTP: The client tries to connect again over HTTP by using the self-signed client certificate.  

To help identify a unique PKI client certificate, you can also specify a custom store other than the default of **Personal** in the **Computer** store. However, you must create this store independently from Configuration Manager. You must be able to deploy certificates to this custom store and renew them before the validity period expires.  

For more information, see [Configure settings for client PKI certificates](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  


###  <a name="BKMK_PlanningForPKITransition"></a> Plan a transition strategy for PKI certificates and internet-based client management  

The flexible configuration options in Configuration Manager let you gradually transition clients and the site to use PKI certificates to help secure client endpoints. PKI certificates provide better security and enable you to manage internet clients.  

Because of the number of configuration options and choices in Configuration Manager, there's no single way to transition a site so that all clients use HTTPS connections. However, you can follow these steps as guidance:  

1. Install the Configuration Manager site and configure it so that site systems accept client connections over HTTPS and HTTP.  

2. Configure the **Client Computer Communication** tab in the site properties so that the **Site System Settings** is **HTTP or HTTPS**, and select **Use PKI client certificate (client authentication capability) when available**.  For more information, see [Configure settings for client PKI certificates](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  

3. Pilot a PKI rollout for client certificates. For an example deployment, see [Deploy the client certificate for Windows computers](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

4. Install clients by using the client push installation method. For more information, see the [How to install Configuration Manager clients by using client push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  

5. Monitor client deployment and status by using the reports and information in the Configuration Manager console.  

6. Track how many clients are using a client PKI certificate by viewing the **Client Certificate** column in the **Assets and Compliance** workspace, **Devices** node.  

    You can also deploy the Configuration Manager HTTPS Readiness Assessment Tool (**cmHttpsReadiness.exe**) to computers. Then use the reports to view how many computers can use a client PKI certificate with Configuration Manager.  

   > [!NOTE]
   >  When you install the Configuration Manager client, it installs the **CMHttpsReadiness.exe** tool in the `%windir%\CCM` folder. The following command-line options are available when you run this tool:  
   > 
   > - `/Store:<name>`: This option is the same as the **CCMCERTSTORE** client.msi property  
   > - `/Issuers:<list>`: This option is the same as the **CCMCERTISSUERS** client.msi property    
   > - `/Criteria:<criteria>`: This option is the same as the **CCMCERTSEL** client.msi property    
   > - `/SelectFirstCert`: This option is the same as the **CCMFIRSTCERT** client.msi property    
   > 
   >   For more information, see [About client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).  

7. When you're confident that enough clients are successfully using their client PKI certificate for authentication over HTTP, follow these steps:  

   1.  Deploy a PKI web server certificate to a member server that runs an additional management point for the site, and configure that certificate in IIS. For more information, see [Deploy the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

   2.  Install the management point role on this server and configure the **Client connections** option in the management point properties for **HTTPS**.  

8. Monitor and verify that clients that have a PKI certificate use the new management point by using HTTPS. You can use IIS logging or performance counters to verify.  

9. Reconfigure other site system roles to use HTTPS client connections. If you want to manage clients on the internet, make sure that site systems have an internet FQDN. Configure individual management points and distribution points to accept client connections from the internet.  

    > [!IMPORTANT]  
    >  Before you set up site system roles to accept connections from the internet, review the planning information and prerequisites for internet-based client management. For more information, see [Communications between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

10. Extend the PKI certificate rollout for clients and for site systems that run IIS. Set up the site system roles for HTTPS client connections and internet connections, as required.  

11. For the highest security: When you're confident that all clients are using a client PKI certificate for authentication and encryption, change the site properties to use HTTPS only.  

    This plan first introduces PKI certificates for authentication only over HTTP, and then for authentication and encryption over HTTPS. When you follow this plan to gradually introduce these certificates, you reduce the risk that clients become unmanaged. You'll also benefit from the highest security that Configuration Manager supports.  

##  <a name="BKMK_PlanningForRTK"></a> Plan for the trusted root key  

 The Configuration Manager trusted root key provides a mechanism for Configuration Manager clients to verify site systems belong to their hierarchy. Every site server generates a site exchange key to communicate with other sites. The site exchange key from the top-level site in the hierarchy is called the trusted root key.  

 The function of the trusted root key in Configuration Manager resembles a root certificate in a public key infrastructure. Anything signed by the private key of the trusted root key is trusted further down the hierarchy. Clients store a copy of the site's trusted root key in the **root\ccm\locationservices** WMI namespace. 

 For example, the site issues a certificate to the management point, which it signs with the private key of the trusted root key. The site shares with clients the public key of its trusted root key. Then clients can differentiate between management points that are in their hierarchy and management points that aren't in their hierarchy.   

 Clients automatically retrieve the public copy of the trusted root key by using two mechanisms:  

- You extend the Active Directory schema for Configuration Manager, and publish the site to Active Directory Domain Services. Then clients retrieve this site information from a global catalog server. For more information, see [Prepare Active Directory for site publishing](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

- When you install clients using the client push installation method. For more information, see [Client push installation](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).  

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
    >  When you specify the trusted root key during client installation, also specify the site code. Use the following client.msi property: `SMSSITECODE=<site code>`   


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

 For more information on these installation properties, see [About client installation parameters and properties](/sccm/core/clients/deploy/about-client-installation-properties).



##  <a name="BKMK_PlanningForSigningEncryption"></a> Plan for signing and encryption  
 
 When you use PKI certificates for all client communications, you don't have to plan for signing and encryption to help secure client data communication. If you set up any site systems that run IIS to allow HTTP client connections, decide how to help secure the client communication for the site.  

 To help protect the data that clients send to management points, you can require clients to sign the data. You can also require the SHA-256 algorithm for signing. This configuration is more secure, but don't require SHA-256 unless all clients support it. Many operating systems natively support this algorithm, but older operating systems might require an update or hotfix. 

 While signing helps protect the data from tampering, encryption helps protect the data from information disclosure. You can enable 3DES encryption for the inventory data and state messages that clients send to management points in the site. You don't have to install any updates on clients to support this option. Clients and management points require additional CPU usage for encryption and decryption.  

 For more information about how to configure the settings for signing and encryption, see [Configure signing and encryption](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureSigningEncryption).  



##  <a name="BKMK_PlanningForRBA"></a> Plan for role-based administration  

 For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).  



## <a name="bkmk_planazuread"></a> Plan for Azure Active Directory

 Configuration Manager integrates with Azure Active Directory (Azure AD) to enable the site and clients to use modern authentication. Onboarding your site with Azure AD supports the following Configuration Manager scenarios:

**Client**  

- [Manage clients on the internet via cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

- [Manage cloud domain-joined devices](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

- [Co-management](/sccm/core/clients/manage/co-management-overview)  

- [Deploy user-available apps](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Microsoft Store for Business online apps](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

- Reduce infrastructure requirements. For example, [Software Center using the management point](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex) instead of the application catalog  

- [Manage Office 365 apps](/sccm/sum/deploy-use/manage-office-365-proplus-updates)  


**Server**  

- [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness)  

- [Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics)  

- [Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  

- [Community Hub](/sccm/core/get-started/capabilities-in-technical-preview-1807#bkmk_hub)  

- [Cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- [User discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  


 For more information on connecting your site to Azure AD, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard).


 For more information about Azure AD, see [Azure Active Directory documentation](https://docs.microsoft.com/azure/active-directory/).



## <a name="bkmk_auth"></a> Plan for SMS Provider authentication
<!--1357013--> 

Starting in version 1810, you can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. It applies to all components that access the SMS Provider. For example, the Configuration Manager console, SDK methods, and Windows PowerShell cmdlets. 

This configuration is a hierarchy-wide setting. Before you change this setting, make sure that all Configuration Manager administrators can sign in to Windows with the required authentication level. 

The following levels are available:

- **Windows authentication**: Require authentication with Active Directory domain credentials.   

- **Certificate authentication**: Require authentication with a valid certificate that's issued by a trusted PKI certificate authority.  

- **Windows Hello for Business authentication**: Require authentication with strong two-factor authentication that's tied to a device and uses biometrics or a PIN.  

For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). 



## See also
- [Security and privacy for Configuration Manager clients](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configure security](/sccm/core/plan-design/security/configure-security)  

- [Communication between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Cryptographic controls technical reference](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements)  

