---
title: "Plan for security in System Center Configuration Manager"
description: "Get best practices and other information about security in System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# Plan for security in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

##  <a name="BKMK_PlanningForCertificates"></a> Plan for certificates (self-signed and PKI)  
 Configuration Manager uses a combination of self-signed certificates and public key infrastructure (PKI) certificates.  

 As a security best practice, use PKI certificates whenever possible. For more about PKI certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). When Configuration Manager requests PKI certificates, such as during enrollment for mobile devices and Intel Active Management Technology (AMT) provisioning, you must use Active Directory Domain Services and an enterprise certification authority. For all other PKI certificates, you must deploy and manage them independently from Configuration Manager.  

 PKI certificates are also required when client computers connect to Internet-based site systems, and we recommend that you use PKI certificates when clients connect to site systems that run Internet Information Services (IIS). For more about client communication, see [How to configure client communication ports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 When you use a PKI, you can also use IPsec to help secure the server-to-server communication between site systems in a site, between sites, and for other data transfer between computers. Implementation of IPsec is independent from Configuration Manager.  

 Configuration Manager can automatically generate self-signed certificates when PKI certificates are not available, and some certificates in Configuration Manager are always self-signed. In most cases, Configuration Manager automatically manages the self-signed certificates, and you do not have to take additional action. One possible exception is the site server signing certificate. The site server signing certificate is always self-signed, and it ensures that the client policies that clients download from the management point were sent from the site server and were not tampered with.  

### Plan for the site server signing certificate (self-signed)  
 Clients can securely get a copy of the site server signing certificate from Active Directory Domain Services and from client push installation. If clients cannot get a copy of the site server signing certificate by one of these mechanisms, as a security best practice, install a copy of the site server signing certificate when you install the client. This is especially important if the client's first communication with the site is from the Internet, because the management point is connected to an untrusted network and, therefore, vulnerable to attack. If you do not take this additional step, clients automatically download a copy of the site server signing certificate from the management point.  

 Scenarios when clients cannot securely get a copy of the site server certificate include the following:  

-   You do not install the client by using client push, and any of the following conditions is true:  

    -   The Active Directory schema is not extended for Configuration Manager.  

    -   The client's site is not published to Active Directory Domain Services.  

    -   The client is from an untrusted forest or a workgroup.  

-   You install the client when it is on the Internet.  

##### To install clients with a copy of the site server signing certificate  

1.  Locate the site server signing certificate on the client's primary site server. The certificate is stored in the **SMS** certificate store and has the Subject name **Site Server** and the friendly name, **Site Server Signing Certificate**.  

2.  Export the certificate without the private key, store the file securely, and access it only from a secured channel, for example, by using Server Message Block (SMB) signing or IPsec.  

3.  Install the client by using the Client.msi property, **SMSSIGNCERT=***&lt;Full path and file name\>*, with CCMSetup.exe.  

###  <a name="BKMK_PlanningForCRLs"></a> Plan for PKI certificate revocation  
When you use PKI certificates with Configuration Manager, plan for how and whether clients and servers will use a certificate revocation list (CRL) to verify the certificate on the connecting computer. The CRL is a file that a certification authority (CA) creates and signs and, it has a list of certificates that the CA has issued but revoked. A CA admin can revoke certificates, for example, if an issued certificate is known or suspected to be compromised.  

> [!IMPORTANT]  
>  Because the location of the CRL is added to a certificate when a CA issues it, ensure that you plan for the CRL before you deploy any PKI certificates that Configuration Manager will use.  

By default, IIS always checks the CRL for client certificates, and you cannot change this configuration in Configuration Manager. By default, Configuration Manager clients always check the CRL for site systems. You can disable this setting by specifying a site property and by specifying a CCMSetup property. When you manage Intel AMT-based computers out of band, you can also enable CRL checking for the out-of-band service point and for computers that run the Out of Band Management console.  

Computers that use certificate revocation checking but cannot locate the CRL behave as if all certificates in the certification chain are revoked because their absence from the list cannot be verified. In this scenario, all connections that require certificates and use a CRL fail.  

Checking the CRL every time that a certificate is used offers more security against using a certificate that has been revoked, but it introduces a connection delay and additional processing on the client. You are more likely to require this additional security check when clients are on the Internet or on an untrusted network.  

Consult your PKI admins before you decide whether Configuration Manager clients must check the CRL, and then consider keeping this option enabled in Configuration Manager when both of the following conditions are true:  

-   Your PKI infrastructure supports a CRL, and it is published where all Configuration Manager clients can locate it. Remember that this might include clients on the Internet if you are using Internet-based client management, and clients in untrusted forests.  

-   The requirement to check the CRL for each connection to a site system that's configured to use a PKI certificate is greater than the requirement for faster connections, efficient processing on the client, and the risk of clients failing to connect to servers if they cannot locate the CRL.  

###  <a name="BKMK_PlanningForRootCAs"></a> Plan for the PKI trusted root certificates and the certificate issuers list  
If your IIS site systems use PKI client certificates for client authentication over HTTP or for client authentication and encryption over HTTPS, you might have to import root CA certificates as a site property. Here are the two scenarios:  

-   You deploy operating systems by using Configuration Manager, and the management points only accept HTTPS client connections.  

-   You use PKI client certificates that do not chain to a root certification authority (CA) certificate that is trusted by management points.  

    > [!NOTE]  
    >  When you issue client PKI certificates from the same CA hierarchy that issues the server certificates that you use for management points, you do not have to specify this root CA certificate. However, if you use multiple CA hierarchies and you are not sure whether they trust each other, import the root CA for the clients' CA hierarchy.  

If you must import root CA certificates for Configuration Manager, export them from the issuing CA or from the client computer. If you export the certificate from the issuing CA that is also the root CA, ensure that the private key is not exported. Store the exported certificate file in a secure location to prevent tampering. You must be able to access the file when you set up the site. If you access the file over the network, ensure that the communication is protected from tampering by using SMB signing or IPsec.  

If any root CA certificate that you import is renewed, you must import the renewed certificate.  

These imported root CA certificates and the root CA certificate of each management point create the certificate issuers list that Configuration Manager computers use in the following ways:  

-   When clients connect to management points, the management point verifies that the client certificate chains to a trusted root certificate in the site's certificate issuers list. If it does not, the certificate is rejected, and the PKI connection fails.  

-   When clients select a PKI certificate and have a certificate issuers list, they select a certificate that chains to a trusted root certificate in the certificate issuers list. If there is no match, the client does not select a PKI certificate. For more about the client certificate process, see the [Plan for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) section in this article.  

Independent from the site configuration, you might also have to import a root CA certificate when you enroll mobile devices, enroll Mac computers, and set up Intel AMT-based computers for wireless networks.  

###  <a name="BKMK_PlanningForClientCertificateSelection"></a> Plan for PKI client certificate selection  
 If your IIS site systems will use PKI client certificates for client authentication over HTTP or for client authentication and encryption over HTTPS, plan for how Windows clients will select the certificate to use for Configuration Manager.  

> [!NOTE]  
>  Some devices do not support a certificate selection method. Instead, they automatically select the first certificate that fulfills the certificate requirements. For example, clients on Mac computers and mobile devices do not support a certificate selection method.  

In many cases, the default configuration and behavior will be sufficient. The Configuration Manager client on Windows computers filters multiple certificates by using these criteria in this order:  

1.  The certificate issuers list: The certificate chains to a root CA that is trusted by the management point.  

2.  The certificate is in the default certificate store of **Personal**.  

3.  The certificate is valid, not revoked, and not expired. The validity check verifies that the private key is accessible and that the certificate is not created with a Version 3 certificate template, which is not compatible with Configuration Manager.  

4.  The certificate has client authentication capability, or it is issued to the computer name.  

5.  The certificate has the longest validity period.  

Clients can be configured to use the certificate issuers list by using the following mechanisms:  

-   It is published as Configuration Manager site information to Active Directory Domain Services.  

-   Clients are installed by using client push.  

-   Clients download it from the management point after they are successfully assigned to their site.  

-   It is specified during client installation as a CCMSetup client.msi property of CCMCERTISSUERS.  

Clients that do not have the certificate issuers list when they are first installed and are not yet assigned to the site skip this check. When clients do have the certificate issuers list and do not have a PKI certificate that chains to a trusted root certificate in the certificate issuers list, certificate selection fails, and clients do not continue with the other certificate selection criteria.  

In most cases, the Configuration Manager client correctly identifies a unique and appropriate PKI certificate. However, when this is not the case, instead of selecting the certificate based on the client authentication capability, you can set up two alternative selection methods:  

-   A partial string match on the client certificate Subject name. This is a case-insensitive match that is appropriate if you are using the fully qualified domain name (FQDN) of a computer in the subject field and want the certificate selection to be based on the domain suffix, for example **contoso.com**. However, you can use this selection method to identify any string of sequential characters in the certificate Subject name that differentiate the certificate from others in the client certificate store.  

    > [!NOTE]  
    >  You cannot use the partial string match with the Subject Alternative Name (SAN) as a site setting. Although you can specify a partial string match for the SAN by using CCMSetup, it will be overwritten by the site properties in the following scenarios:  
    >   
    >  -   Clients retrieve site information that is published to Active Directory Domain Services.  
    > -   Clients are installed by using client push installation.  
    >   
    >  Use a partial string match in the SAN only when you install clients manually and when they do not retrieve site information from Active Directory Domain Services. For example, these conditions apply to Internet-only clients.  

-   A match on the client certificate Subject name attribute values or the Subject Alternative Name (SAN) attribute values. This is a case-sensitive match that is appropriate if you are using an X500 distinguished name or equivalent Object Identifiers (OIDs) in compliance with RFC 3280, and you want the certificate selection to be based on the attribute values. You can specify only the attributes and their values that you require to uniquely identify or validate the certificate and differentiate the certificate from others in the certificate store.  

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

If more than one appropriate certificate is located after the selection criteria are applied, you can override the default configuration to select the certificate that has the longest validity period and instead, specify that no certificate is selected. In this scenario, the client will not be able to communicate with IIS site systems with a PKI certificate. The client sends an error message to its assigned fallback status point to alert you to the certificate selection failure so that you can change or refine your certificate selection criteria. The client behavior then depends on whether the failed connection was over HTTPS or HTTP:  

-   If the failed connection was over HTTPS: The client tries to connect over HTTP and uses the client self-signed certificate.  

-   If the failed connection was over HTTP: The client tries to connect again over HTTP by using the self-signed client certificate.  

To help identify a unique PKI client certificate, you can also specify a custom store other than the default of **Personal** in the **Computer** store. However, you must create this store independently from Configuration Manager and must be able to deploy certificates to this custom store and renew them before the validity period expires.  

For information about how to configure the settings for client certificates, see the [Configure Settings for Client PKI Certificates](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) section in the [Configure security in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) article.  

###  <a name="BKMK_PlanningForPKITransition"></a> Plan a transition strategy for PKI certificates and Internet-based client management  
The flexible configuration options in Configuration Manager let you gradually transition clients and the site to use PKI certificates to help secure client endpoints. PKI certificates provide better security and enable you to manage Internet clients.  

Because of the number of configuration options and choices in Configuration Manager, there is no single way to transition a site so that all clients use HTTPS connections. However, you can follow these steps as guidance:  

1.  Install the Configuration Manager site and configure it so that site systems accept client connections over HTTPS and HTTP.  

2.  Configure the **Client Computer Communication** tab in the site properties so that the **Site System Settings** is **HTTP or HTTPS**, and select **Use PKI client certificate (client authentication capability) when available**.  For more information, see the  [Configure settings for client PKI certificates](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) section in the [Configure security in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) article.  

3.  Pilot a PKI rollout for client certificates. For an example deployment, see the *Deploying the Client Certificate for Windows Computers* section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) article.  

4.  Install clients by using the client push installation method. For more information, see the [How to Install Configuration Manager Clients by Using Client Push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) section in the [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) article.  

5.  Monitor client deployment and status by using the reports and information in the Configuration Manager console.  

6.  Track how many clients are using a client PKI certificate by viewing the **Client Certificate** column in the **Assets and Compliance** workspace, **Devices** node.  

     You can also deploy the Configuration Manager HTTPS Readiness Assessment Tool (**cmHttpsReadiness.exe**) to computers and use the reports to view how many computers can use a client PKI certificate with Configuration Manager.  

    > [!NOTE]  
    >  When the Configuration Manager client is installed, the **cmHttpsReadiness.exe** tool is installed in the *%windir%***\CCM** folder. When you run this tool on clients, you can specify the following options:  
    >   
    >  -   /Store:&lt;name\>  
    > -   /Issuers:&lt;list\>  
    > -   /Criteria:&lt;criteria\>  
    > -   /SelectFirstCert  
    >   
    >  These options map to the **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**, and **CCMFIRSTCERT** Client.msi properties, respectively. For more about these options, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  When you are confident that enough clients are successfully using their client PKI certificate for authentication over HTTP, follow these steps:  

    1.  Deploy a PKI web server certificate to a member server that will run an additional management point for the site, and configure that certificate in IIS. For more information, see the *Deploying the Web Server Certificate for Site Systems that Run IIS* section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) article.  

    2.  Install the management point role on this server and configure the **Client connections** option in the management point properties for **HTTPS**.  

8.  Monitor and verify that clients that have a PKI certificate use the new management point by using HTTPS. You can use IIS logging or performance counters to verify this.  

9. Reconfigure other site system roles to use HTTPS client connections. If you want to manage clients on the Internet, ensure that site systems have an Internet FQDN and configure individual management points and distribution points to accept client connections from the Internet.  

    > [!IMPORTANT]  
    >  Before you set up site system roles to accept connections from the Internet, review the planning information and prerequisites for Internet-based client management. For more information, see [Communications between endpoints in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Extend the PKI certificate rollout for clients and for site systems that run IIS, and set up the site system roles for HTTPS client connections and Internet connections, as required.  

11. For the highest security: When you are confident that all clients are using a client PKI certificate for authentication and encryption, change the site properties to use HTTPS only.  

 When you follow this plan to gradually introduce PKI certificates, first for authentication only over HTTP and then for authentication and encryption over HTTPS, you reduce the risk that clients will become unmanaged. In addition, you will benefit from the highest security that Configuration Manager supports.  

##  <a name="BKMK_PlanningForRTK"></a> Plan for the trusted root key  
The Configuration Manager trusted root key provides a mechanism for Configuration Manager clients to verify that site systems belong to their hierarchy. Every site server generates a site exchange key to communicate with other sites. The site exchange key from the top-level site in the hierarchy is called the trusted root key.  

The function of the trusted root key in Configuration Manager resembles a root certificate in a public key infrastructure in that anything signed by the private key of the trusted root key is trusted further down the hierarchy. For example, by signing the management point certificate with the private key of the trusted root key pair, and by making a copy of the public key of the trusted root key pair available to clients, clients can differentiate between management points that are in their hierarchy and management points that are not in their hierarchy. Clients use Windows Management Instrumentation (WMI) to store a copy of the trusted root key in the **root\ccm\locationservices** namespace.  

Clients can automatically retrieve the public copy of the trusted root key by using two mechanisms:  

-   The Active Directory schema is extended for Configuration Manager, the site is published to Active Directory Domain Services, and clients can retrieve this site information from a global catalog server.  

-   Clients are installed by using client push.  

If clients cannot retrieve the trusted root key by using one of these mechanisms, they trust the trusted root key that is provided by the first management point that they communicate with. In this scenario, a client might be misdirected to an attacker's management point where it would receive policy from the rogue management point. This would likely be the action of a sophisticated attacker and might occur only in a limited time before the client retrieves the trusted root key from a valid management point. However, to reduce this risk of an attacker misdirecting clients to a rogue management point, you can pre-provision the clients with the trusted root key.  

Use the following procedures to pre-provision and verify the trusted root key for a Configuration Manager client:  

-   Pre-provision a client with the trusted root key by using a file.  

-   Pre-provision a client with the trusted root key without using a file.  

-   Verify the trusted root key on a client.  

> [!NOTE]  
>  You do not have to pre-provision a client by using the trusted root key if they can get this from Active Directory Domain Services or they are installed by using client push. In addition, you do not have to pre-provision clients when they use HTTPS communication to management points because trust is established by PKI certificates.  

You can remove the trusted root key from a client by using the Client.msi property, **RESETKEYINFORMATION = TRUE**, with CCMSetup.exe. To replace the trusted root key, reinstall the client together with the new trusted root key, for example, by using client push, or by specifying the Client.msi **SMSPublicRootKey** property by using CCMSetup.exe.  

#### To pre-provision a client with the trusted root key by using a file  

1.  In a text editor, open the file, *&lt;Configuration Manager directory\>***\bin\mobileclient.tcf**.  

2.  Locate the entry, **SMSPublicRootKey=**, copy the key from that line, and close the file without any changes.  

3.  Create a new text file, and paste the key information that you copied from the mobileclient.tcf file.  

4.  Save the file, and place it in a location where all computers can access it, but where the file is secured to prevent tampering.  

5.  Install the client by using any installation method that accepts Client.msi properties, and specify the Client.msi property, **SMSROOTKEYPATH=***&lt;Full path and file name\>*.  

    > [!IMPORTANT]  
    >  When you specify the trusted root key for additional security during client installation, you must also specify the site code by using the Client.msi property, **SMSSITECODE=&lt;site code\>**.  

#### To pre-provision a client with the trusted root key without using a file  

1.  In a text editor, open the file, *&lt;Configuration Manager directory\>***\bin\mobileclient.tcf**.  

2.  Locate the entry, SMSPublicRootKey=, note the key from that line or copy it to the Clipboard, and then close the file without any changes.  

3.  Install the client by using any installation method that accepts Client.msi properties, and specify the Client.msi property, **SMSPublicRootKey=***&lt;key\>*, where *&lt;key\>* is the string that you copied from mobileclient.tcf.  

    > [!IMPORTANT]  
    >  When you specify the trusted root key for additional security during client installation, you must also specify the site code by using the Client.msi property, **SMSSITECODE=&lt;site code\>**.  

#### To verify the trusted root key on a client  

1.  On the **Start** menu, choose **Run**, and then enter **Wbemtest**.  

2.  In the **Windows Management Instrumentation Tester** dialog box, choose **Connect**.  

3.  In the **Connect** dialog box, in the **Namespace** box, enter **root\ccm\locationservices**, and then choose **Connect**.  

4.  In the **Windows Management Instrumentation Tester** dialog box, in the **IWbemServices** section, choose **Enum Classes**.  

5.  In the **Superclass Info** dialog box, choose **Recursive**, and then choose **OK**.  

6.  The **Query Result** window, scroll to the end of the list, and then double-click **TrustedRootKey ()**.  

7.  In the **Object editor for TrustedRootKey** dialog box, choose **Instances**.  

8.  In the new **Query Result** window that shows the instances of **TrustedRootKey**, double-click **TrustedRootKey=@**.  

9. In the **Object editor for TrustedRootKey=@** dialog box, in the **Properties** section, scroll down to **TrustedRootKey CIM_STRING**. The string in the right column is the trusted root key. Verify that it matches the **SMSPublicRootKey** value in the file, *&lt;Configuration Manager directory\>***\bin\mobileclient.tcf**.  

##  <a name="BKMK_PlanningForSigningEncryption"></a> Plan for signing and encryption  
 When you use PKI certificates for all client communications, you do not have to plan for signing and encryption to help secure client data communication. But, if you set up any site systems that run IIS to allow HTTP client connections, you must decide how to help secure the client communication for the site.  

 To help protect the data that clients send to management points, you can require data to be signed. In addition, you can require that all signed data from clients that use HTTP is signed by using the SHA-256 algorithm. Although this is a more secure setting, do not enable this option unless all clients support SHA-256. Many operating systems natively support SHA-256, but older operating systems might require an update or hotfix. For example, computers that run Windows Server 2003 SP2 must install a hotfix that is referenced in the [KB article 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 Whereas signing helps protect the data from tampering, encryption helps protect the data from information disclosure. You can enable 3DES encryption for the inventory data and state messages that clients send to management points in the site. You do not have to install any updates on clients to support this option, but consider the additional CPU usage that will be required on clients and the management point to do the encryption and decryption.  

 For more about how to configure the settings for signing and encryption, see the [Configure Signing and Encryption](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) section in the [Configure security in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) article.  

##  <a name="BKMK_PlanningForRBA"></a> Plan for role-based administration  
 For this information, see [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

### See also
[Cryptographic controls technical reference for System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  
