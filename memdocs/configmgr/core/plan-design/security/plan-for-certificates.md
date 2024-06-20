---
title: Plan for PKI certificates
titleSuffix: Configuration Manager
description: Plan for the use of PKI digital certificates in Configuration Manager.
ms.date: 03/23/2023
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Plan for PKI certificates in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager uses public key infrastructure (PKI)-based digital certificates when available. Use of these certificates is recommended for greater security, but not required for most scenarios. You need to deploy and manage these certificates independently from Configuration Manager.

This article provides information about PKI certificates in Configuration Manager to help you plan your implementation. For more general information about the use of certificates in Configuration Manager, see [Certificates in Configuration Manager](certificates-overview.md).

## PKI certificate revocation

When you use PKI certificates with Configuration Manager, plan for use of a certificate revocation list (CRL). Devices use the CRL to verify the certificate on the connecting computer. The CRL is a file that a certificate authority (CA) creates and signs. It has a list of certificates that the CA has issued but revoked. When a certificate administrator revokes certificates, its thumbprint is added to the CRL. For example, if an issued certificate is known or suspected to be compromised.

> [!IMPORTANT]
> Because the location of the CRL is added to a certificate when a CA issues it, make sure that you plan for the CRL before you deploy any PKI certificates that Configuration Manager uses.

IIS always checks the CRL for client certificates, and you can't change this configuration in Configuration Manager. By default, Configuration Manager clients always check the CRL for site systems. Disable this setting by specifying a site property and by specifying a CCMSetup property.

Computers that use certificate revocation checking but can't locate the CRL behave as if all certificates in the certification chain are revoked. This behavior is because they can't verify if the certificates are in the certificate revocation list. In this scenario, all connections fail that require certificates and include CRL checking. When validating that your CRL is accessible by browsing to its HTTP location, it's important to note that the Configuration Manager client runs as LOCAL SYSTEM. Testing CRL accessibility with a web browser under a user context may succeed, but the computer account may be blocked when attempting to make an HTTP connection to the same CRL URL. For example, it can be blocked because of an internal web filtering solution like a proxy. Add the CRL URL to the approved list for any web filtering solutions.

Checking the CRL every time that a certificate is used offers more security against using a certificate that's revoked. It does introduce a connection delay and more processing on the client. Your organization may require this security check for clients on the internet or an untrusted network.

Consult your PKI administrators before you decide whether Configuration Manager clients need to check the CRL. When both of the following conditions are true, consider keeping this option enabled in Configuration Manager:

- Your PKI infrastructure supports a CRL, and it's published where all Configuration Manager clients can locate it. These clients might include devices on the internet, and ones in untrusted forests.

- The requirement to check the CRL for each connection to a site system that's configured to use a PKI certificate is greater than the following requirements:
  - Faster connections
  - Efficient processing on the client
  - The risk of clients failing to connect to servers if they can't locate the CRL

## PKI trusted root certificates

If your IIS site systems use PKI client certificates for client authentication over HTTP, or for client authentication and encryption over HTTPS, you might have to import root CA certificates as a site property. Here are the two scenarios:

- You deploy operating systems by using Configuration Manager, and the management points only accept HTTPS client connections.

- You use PKI client certificates that don't chain to a root certificate that the management points trust.

  > [!NOTE]
  > When you issue client PKI certificates from the same CA hierarchy that issues the server certificates that you use for management points, you don't have to specify this root CA certificate. However, if you use multiple CA hierarchies and you aren't sure whether they trust each other, import the root CA for the clients' CA hierarchy.

If you need to import root CA certificates for Configuration Manager, export them from the issuing CA or from the client computer. If you export the certificate from the issuing CA that's also the root CA, don't export the private key. Store the exported certificate file in a secure location to prevent tampering. You need access to the file when you set up the site. If you access the file over the network, make sure the communication is protected from tampering by using IPsec.

If any root CA certificate that you import are renewed, import the renewed certificate.

These imported root CA certificates and the root CA certificate of each management point create the certificate issuers list. Configuration Manager computers use this list in the following ways:

- When clients connect to management points, the management point verifies that the client certificate is chained to a trusted root certificate in the site's certificate issuers list. If it doesn't, the certificate is rejected, and the PKI connection fails.

- When clients select a PKI certificate and have a certificate issuers list, they select a certificate that chains to a trusted root certificate in the certificate issuers list. If there's no match, the client doesn't select a PKI certificate. For more information, see [PKI client certificate selection](#pki-client-certificate-selection).

## PKI client certificate selection

If your IIS site systems use PKI client certificates for client authentication over HTTP or for client authentication and encryption over HTTPS, plan for how Windows clients select the certificate to use for Configuration Manager.

> [!NOTE]
> Some devices don't support a certificate selection method. Instead, they automatically select the first certificate that fulfills the certificate requirements. For example, clients on macOS computers and mobile devices don't support a certificate selection method.

In many cases, the default configuration and behavior are sufficient. The Configuration Manager client on Windows computers filters multiple certificates by using these criteria in this order:

1. The certificate issuers list: The certificate chains to a root CA that's trusted by the management point.

1. The certificate is in the default certificate store of **Personal**.

1. The certificate is valid, not revoked, and not expired. The validity check also verifies that the private key is accessible.

1. The certificate has client authentication capability.

1. The certificate Subject Name contains the local computer name as a substring.

1. The certificate has the longest validity period.

Configure clients to use the certificate issuers list by using the following mechanisms:

- [Publish](../../servers/deploy/configure/publish-site-data.md) it with Configuration Manager site information to Active Directory Domain Services.

- Install clients by using [client push](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).

- Clients download it from the management point after they're successfully [assigned to their site](../../clients/deploy/assign-clients-to-a-site.md).

- Specify it during client installation as a CCMSetup client.msi property of [CCMCERTISSUERS](../../clients/deploy/about-client-installation-properties.md#ccmcertissuers).

If clients don't have the certificate issuers list when they're first installed, and aren't yet assigned to the site, they skip this check. When clients do have the certificate issuers list, and don't have a PKI certificate that chains to a trusted root certificate in the certificate issuers list, certificate selection fails. Clients don't continue with the other certificate selection criteria.

In most cases, the Configuration Manager client correctly identifies a unique and appropriate PKI certificate. When this behavior isn't the case, instead of selecting the certificate based on the client authentication capability, you can set up two alternative selection methods:

- A partial string match on the client certificate subject name. This method is a case-insensitive match. It's appropriate if you're using the fully qualified domain name (FQDN) of a computer in the subject field and want the certificate selection to be based on the domain suffix, for example **contoso.com**. You can use this selection method to identify any string of sequential characters in the certificate subject name that differentiates the certificate from others in the client certificate store.

  > [!NOTE]
  > You can't use the partial string match with the subject alternative name (SAN) as a site setting. Although you can specify a partial string match for the SAN by using CCMSetup, it'll be overwritten by the site properties in the following scenarios:
  >
  > - Clients retrieve site information that's published to Active Directory Domain Services.
  > - Clients are installed by using client push installation.
  >
  > Use a partial string match in the SAN only when you install clients manually and when they don't retrieve site information from Active Directory Domain Services. For example, these conditions apply to internet-only clients.

- A match on the client certificate subject name attribute values or the subject alternative name (SAN) attribute values. This method is a case-sensitive match. It's appropriate if you're using an X500 distinguished name or equivalent object identifiers (OIDs) in compliance with RFC 3280, and you want the certificate selection to be based on the attribute values. You can specify only the attributes and their values that you require to uniquely identify or validate the certificate and differentiate the certificate from others in the certificate store.

The following table shows the attribute values that Configuration Manager supports for the client certificate selection criteria:

|OID Attribute|Distinguished name attribute|Attribute definition|
|-------------|----------------------------|--------------------|
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

> [!NOTE]
> If you configure either of the above alternate certificate selection methods, the certificate Subject Name doesn't need to contain the local computer name.

If more than one appropriate certificate is located after the selection criteria are applied, you can override the default configuration to select the certificate that has the longest validity period. Instead, you can specify that no certificate is selected. In this scenario, the client can't communicate with IIS site systems with a PKI certificate. The client sends an error message to its assigned fallback status point to alert you to the certificate selection failure. Then you can change or refine your certificate selection criteria.

The client behavior then depends on whether the failed connection was over HTTPS or HTTP:

- If the failed connection was over HTTPS: The client tries to connect over HTTP and uses the client self-signed certificate.

- If the failed connection was over HTTP: The client tries to connect again over HTTP by using the self-signed client certificate.

To help identify a unique PKI client certificate, you can also specify a custom store other than the default of **Personal** in the **Computer** store. Create a custom certificate store outside of Configuration Manager. You need to be able to deploy certificates to this custom store and renew them before the validity period expires.

For more information, see [Configure settings for client PKI certificates](configure-security.md#client-pki-certificates).

## Transition strategy for PKI certificates

The flexible configuration options in Configuration Manager let you gradually transition clients and the site to use PKI certificates to help secure client endpoints. PKI certificates provide better security and enable you to manage internet clients.

This plan first introduces PKI certificates for authentication only over HTTP, and then for authentication and encryption over HTTPS. When you follow this plan to gradually introduce these certificates, you reduce the risk that clients become unmanaged. You'll also benefit from the highest security that Configuration Manager supports.

Because of the number of configuration options and choices in Configuration Manager, there's no single way to transition a site so that all clients use HTTPS connections. The following steps provide general guidance:

1. Install the Configuration Manager site and configure it so that site systems accept client connections over HTTPS and HTTP.

1. Configure the **Communication Security** tab in the site properties. Set **Site System Settings** to **HTTP or HTTPS** and select **Use PKI client certificate (client authentication capability) when available**. For more information, see [Configure settings for client PKI certificates](configure-security.md#client-pki-certificates).

1. Pilot a PKI rollout for client certificates. For an example deployment, see [Deploy the client certificate for Windows computers](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

1. Install clients by using the client push installation method. For more information, see the [How to install Configuration Manager clients by using client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

1. Monitor client deployment and status by using the reports and information in the Configuration Manager console.

1. Track how many clients are using a client PKI certificate by viewing the **Client Certificate** column in the **Assets and Compliance** workspace, **Devices** node.

   > [!NOTE]
   > For clients that also have a PKI certificate, the Configuration Manager console displays the **Client certificate** property as **Self-signed**. The client control panel **Client certificate** property shows **PKI**.<!-- 10278780 -->

   You can also deploy the Configuration Manager HTTPS Readiness Assessment Tool (**CMHttpsReadiness.exe**) to computers. Then use the reports to view how many computers can use a client PKI certificate with Configuration Manager.

   > [!NOTE]
   > When you install the Configuration Manager client, it installs the **CMHttpsReadiness.exe** tool in the `%windir%\CCM` folder. The following command-line options are available when you run this tool:
   >
   > - ```/Store:<Certificate store name>```: This option is the same as the [CCMCERTSTORE](../../clients/deploy/about-client-installation-properties.md#ccmcertstore) client.msi property
   > -```/Issuers:<Case-sensitive issuer common name>```: This option is the same as the [CCMCERTISSUERS](../../clients/deploy/about-client-installation-properties.md#ccmcertissuers) client.msi property
   > - ```/Criteria:<Selection criteria>```: This option is the same as the [CCMCERTSEL](../../clients/deploy/about-client-installation-properties.md#ccmcertsel) client.msi property
   > - ```/SelectFirstCert```: This option is the same as the [CCMFIRSTCERT](../../clients/deploy/about-client-installation-properties.md#ccmfirstcert) client.msi property

     The tool outputs information to the CMHttpsReadiness.log in the ```CCM\Logs``` directory.

     For more information, see [About client installation properties](../../clients/deploy/about-client-installation-properties.md).

1. When you're confident that enough clients are successfully using their client PKI certificate for authentication over HTTP, follow these steps:

    1. Deploy a PKI web server certificate to a member server that runs another management point for the site, and configure that certificate in IIS. For more information, see [Deploy the web server certificate for site systems that run IIS](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

    1. Install the management point role on this server. Configure the **Client connections** option in the management point properties for **HTTPS**.

1. Monitor and verify that clients that have a PKI certificate use the new management point by using HTTPS. You can use IIS logging or performance counters to verify.

1. Reconfigure other site system roles to use HTTPS client connections. If you want to manage clients on the internet, make sure that site systems have an internet FQDN. Configure individual management points and distribution points to accept client connections from the internet.

    > [!IMPORTANT]
    > Before you set up site system roles to accept connections from the internet, review the planning information and prerequisites for internet-based client management. For more information, see [Communications between endpoints](../hierarchy/communications-between-endpoints.md).

1. Extend the PKI certificate rollout for clients and for site systems that run IIS. Set up the site system roles for HTTPS client connections and internet connections, as required.

1. For the highest security: When you're confident that all clients are using a client PKI certificate for authentication and encryption, change the site properties to use HTTPS only.

## Next steps

- [Configure security](configure-security.md)

- [Cryptographic controls technical reference](cryptographic-controls-technical-reference.md)

- [PKI certificate requirements](../network/pki-certificate-requirements.md)
