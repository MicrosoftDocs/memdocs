---
title: PKI certificate requirements
titleSuffix: Configuration Manager
description: Find requirements for PKI certificates that you might need for Configuration Manager.
ms.date: 08/10/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# PKI certificate requirements for Configuration Manager

*Applies to: Configuration Manager (current branch)*

The public key infrastructure (PKI) certificates that you might require for Configuration Manager are listed in the following tables. This information assumes basic knowledge of PKI certificates.

You can use any PKI to create, deploy, and manage most certificates in Configuration Manager. For client certificates that Configuration Manager enrolls on mobile devices and Mac computers, they require use of Active Directory Certificate Services.

When you use Active Directory Certificate Services and certificate templates, this Microsoft PKI solution can ease the management of certificates. Use the **Microsoft certificate template** reference in the sections below to identify the certificate template that most closely matches the certificate requirements. Only an enterprise certification authority (CA) that runs on the Enterprise or Datacenter editions of Windows server can use template-based certificates.

For more information, see the following articles:

- [Step-by-step example deployment of the PKI certificates for Configuration Manager: Windows Server 2008 Certification Authority](example-deployment-of-pki-certificates.md)

- [Active Directory Certificate Services Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11))

- [How to enable Transport Layer Security (TLS) 1.2](../security/enable-tls-1-2.md)

## Supported certificate types

### Secure Hash Algorithm 2 (SHA-2) certificates

Issue new server and client authentication certificates that are signed with SHA-2, which includes SHA-256 and SHA-512. All internet-facing services should use an SHA-2 certificate. For example, if you purchase a public certificate for use with a cloud management gateway, make sure that you purchase an SHA-2 certificate.

Windows doesn't trust certificates signed with SHA-1. For more information, see [Windows Enforcement of SHA1 certificates](https://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-sha1-certificates.aspx).

### CNG v3 certificates

Configuration Manager supports _Cryptography: Next Generation_ (CNG) v3 certificates. Configuration Manager clients can use a PKI client authentication certificate with private key in a CNG Key Storage Provider (KSP). With KSP support, Configuration Manager clients support hardware-based private keys, such as a TPM KSP for PKI client authentication certificates.

For more information, see [CNG v3 certificates overview](cng-certificates-overview.md).

## PKI certificates for servers

### Site systems that run IIS and support HTTPS client connections

This web server certificate is used to:

- Authenticate the servers to the client
- Encrypt all data that's transferred between the client and these servers with TLS.

Applies to:

- Management point
- Distribution point
- Software update point
- State migration point
- Enrollment point
- Enrollment proxy point
- Certificate registration point

Certificate requirements:

- Certificate purpose: **Server authentication**

- Microsoft certificate template: **Web Server**

- The **Enhanced Key Usage** value must contain `Server Authentication (1.3.6.1.5.5.7.3.1)`

- Subject Name:

  - If the site system accepts connections from the internet, the **Subject Name** or **Subject Alternative Name** must contain the internet fully qualified domain name (FQDN).

  - If the site system accepts connections from the intranet, the **Subject Name** or **Subject Alternative Name** must contain either the intranet FQDN (recommended) or the computer's name, depending on how the site system is set up.

  - If the site system accepts connections from both the internet and the intranet, both the internet FQDN and the intranet FQDN (or computer name) must be specified. Use the ampersand (`&`) symbol delimiter between the two names.

  > [!NOTE]
  > When the software update point accepts client connections from the internet only, the certificate must contain both the internet FQDN and the intranet FQDN.

- Key length: Configuration Manager doesn't specify a maximum supported key length for this certificate. Consult your PKI and IIS documentation for any key-size related issues for this certificate.

Most site system roles support key storage providers for certificate private keys (v3). For more information, see [CNG v3 certificates overview](cng-certificates-overview.md).

This certificate must be in the Personal store in the Computer certificate store.

### Cloud management gateway (CMG)

This service certificate is used to:

- Authenticate the CMG service in Azure to Configuration Manager clients

- Encrypt all data transferred between them by using TLS.

Export this certificate in a Public Key Certificate Standard (PKCS #12) format. You need to know the password, so that you can import the certificate when you create the CMG.

Certificate requirements:

- Certificate purpose: **Server authentication**

- Microsoft certificate template: **Web Server**

- The **Enhanced Key Usage** value must contain `Server Authentication (1.3.6.1.5.5.7.3.1)`

- The **Subject Name** must contain a customer-defined _service name_ as the **Common Name** for the specific instance of the cloud management gateway.

- The private key must be exportable.

- Supported key lengths: 2048-bit or 4096-bit

This certificate supports key storage providers for certificate private keys (v3).

For more information, see [CMG server authentication certificate](../../clients/manage/cmg/server-auth-cert.md).

### Site system servers that run Microsoft SQL Server

This certificate is used for server-to-server authentication.

Certificate requirements:

- Certificate purpose: **Server authentication**

- Microsoft certificate template: **Web Server**

- The **Enhanced Key Usage** value must contain `Server Authentication (1.3.6.1.5.5.7.3.1)`

- The **Subject Name** must contain the intranet fully qualified domain name (FQDN)

- Maximum supported key length is 2,048 bits.

This certificate must be in the Personal store in the Computer certificate store. Configuration Manager automatically copies it to the Trusted People Store for servers in the Configuration Manager hierarchy that might have to establish trust with the server.

### SQL Server Always On failover cluster instance

This certificate is used for server-to-server authentication.

Certificate requirements:

- Certificate purpose: **Server authentication**

- Microsoft certificate template: **Web Server**

- The **Enhanced Key Usage** value must contain `Server Authentication (1.3.6.1.5.5.7.3.1)`

- The **Subject Name** must contain the intranet fully qualified domain name (FQDN) of the cluster

- The private key must be exportable

- The certificate must have a validity period of at least two years when you configure Configuration Manager to use the failover cluster instance

- Maximum supported key length is 2,048 bits.

Request and install this certificate on one node in the cluster. Then export the certificate and import it to the other nodes.

This certificate must be in the Personal store in the Computer certificate store. Configuration Manager automatically copies it to the Trusted People Store for servers in the Configuration Manager hierarchy that might have to establish trust with the server.

### Site system monitoring

Applies to:

- Management point
- State migration point

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template: **Workstation Authentication**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- Computers must have a unique value in the **Subject Name** field or in the **Subject Alternative Name** field.

  > [!NOTE]
  > If you use multiple values for the **Subject Alternative Name**, it only uses the first value.

- Maximum supported key length is 2,048 bits.

This certificate is required on the listed site system servers, even if the Configuration Manager client isn't installed. This configuration allows the site to monitor and report on the health of these site system roles.

The certificate for these site systems must be in the Personal store of the Computer certificate store.

### Servers running the Configuration Manager Policy Module with the Network Device Enrollment Service (NDES) role service

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template: **Workstation Authentication**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- There are no specific requirements for the certificate **Subject Name** or **Subject Alternative Name** (SAN). You can use the same certificate for multiple servers running the Network Device Enrollment Service.

- Supported key lengths: 1,024 bits and 2,048 bits.

### Site systems that have a distribution point installed

This certificate has two purposes:

- It authenticates the distribution point to an HTTPS-enabled management point before the distribution point sends status messages.

    > [!NOTE]
    > When you configure all management points for HTTPS, then HTTPS-enabled distribution points must use a PKI-issued certificate. Don't use self-signed certificates on distribution points when management points use certificates. Issues may occur otherwise. For example, distribution points won't sent state messages.<!-- 13860499 -->

- A PXE-enabled distribution point sends this certificate to computers. If the task sequence includes client actions like client policy retrieval or sending inventory information, the computer can connect to an HTTPS-enabled management point during the OS deployment process.

    > [!NOTE]
    > For this PXE scenario, this certificate is only used during the OS deployment process. It isn't installed on the client. Because of this temporary use, you can use the same certificate for every OS deployment if you don't want to use multiple client certificates.
    >
    > The requirements for this certificate are the same as the client certificate for boot images. Because the requirements are the same, you can use the same certificate file.
    >
    > The certificate that you specify to HTTPS-enable a distribution point applies to all content distribution operations, not just OS deployment.

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template: **Workstation Authentication**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- There are no specific requirements for the certificate **Subject Name** or **Subject Alternative Name** (SAN). It's recommended to use a different certificate for each distribution point, but you can use the same certificate.

- The private key must be exportable.

- Maximum supported key length is 2,048 bits.

Export this certificate in a Public Key Certificate Standard (PKCS #12) format. You need to know the password, so that you can import the certificate to the distribution point properties.

### Proxy web servers for internet-based client management

If the site supports internet-based client management, and you use a proxy web server by using SSL termination (bridging) for incoming internet connections, the proxy web server has the following certificate requirements:

> [!NOTE]
> If you use a proxy web server without SSL termination (tunneling), no additional certificates are required on the proxy web server.

Certificate requirements:

- Certificate purpose: **Server authentication** and **Client authentication**

- Microsoft certificate template: **Web Server** and **Workstation Authentication**

- Internet FQDN in the **Subject Name** or **Subject Alternative Name** field. If you use Microsoft certificate templates, the **Subject Alternative Name** is only available with the workstation template.

This certificate is used to authenticate the following servers to internet clients and to encrypt all data transferred between the client and this server with TLS:

- Internet-based management point
- Internet-based distribution point
- Internet-based software update point

The client authentication is used to bridge client connections between the Configuration Manager clients and the internet-based site systems.

## PKI certificates for clients

### Windows client computers

Except for the software update point, this certificate authenticates the client to site systems that run IIS and support HTTPS client connections.

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template: **Workstation Authentication**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- The **Key Usage** value must contain `Digital Signature, Key Encipherment (a0)`

- Client computers must have a unique value in the **Subject Name** or **Subject Alternative Name** field. If used, the **Subject Name** field must contain the local computer name unless an alternative certificate selection criteria is specified. For more information, see [Plan for PKI client certificate selection](../security/plan-for-certificates.md#pki-client-certificate-selection).

  > [!NOTE]
  > If you use multiple values for the **Subject Alternative Name**, it only uses the first value.

- There's no maximum supported key length.<!-- 10568126 -->

By default, Configuration Manager looks for computer certificates in the Personal store in the Computer certificate store.

### Boot images for deploying operating systems

The certificate is used if the task sequence includes client actions like client policy retrieval or sending inventory information. It allows the computer to connect to an HTTPS-enabled management point during the OS deployment process.

This certificate is only used during the OS deployment process. It isn't used to install the client or installed on the device. Because of this temporary use, you can use the same certificate for every OS deployment if you don't want to use multiple client certificates.

When you have an environment that's HTTPS-only, the boot image must have a valid certificate. This certificate allows the device to communicate with the site and for the deployment to continue. The client can automatically generate a certificate when the device is joined to Active Directory, or you can install a client certificate by using another method.

> [!NOTE]
> The requirements for this certificate are the same as the server certificate for site systems with the distribution point role. Because the requirements are the same, you can use the same certificate file.

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template: **Workstation Authentication**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- There are no specific requirements for the certificate **Subject Name** or **Subject Alternative Name** (SAN) fields. You can use the same certificate for all boot images.

- The private key must be exportable.

- Maximum supported key length is 2,048 bits.

Export this certificate in a Public Key Certificate Standard (PKCS #12) format. You need to know the password, so that you can import the certificate to the boot image properties.

### macOS client computers

This certificate authenticates the macOS client computer to the site system servers that it communicates with. For example, management points and distribution points.

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template:

  - For Configuration Manager enrollment: **Authenticated Session**
  - For certificate installation independent from Configuration Manager: **Workstation Authentication**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- Subject Name:

  - For Configuration Manager that creates a User certificate, the certificate **Subject** value is automatically populated with the user name of the person who enrolls the macOS computer.
  - For certificate installation that doesn't use Configuration Manager enrollment, but deploys a Computer certificate independently from Configuration Manager, the certificate **Subject** value must be unique. For example, specify the FQDN of the computer.
  - The **Subject Alternative Name** field isn't supported.

- Maximum supported key length is 2,048 bits.

### Mobile device clients

This certificate authenticates the mobile device client to the site system servers that it communicates with. For example, management points and distribution points.

Certificate requirements:

- Certificate purpose: **Client authentication**

- Microsoft certificate template: **Authenticated Session**

- The **Enhanced Key Usage** value must contain `Client Authentication (1.3.6.1.5.5.7.3.2)`

- Maximum supported key length is 2,048 bits.

These certificates must be in Distinguished Encoding Rules (DER) encoded binary X.509 format. Base64 encoded X.509 format isn't supported.

### Root certification authority (CA) certificates

This certificate is a standard root CA certificate.

Applies to:

- OS deployment
- Client certificate authentication
- Mobile device enrollment

Certificate purpose: Certificate chain to a trusted source

The root CA certificate must be provided when clients have to chain the certificates of the communicating server to a trusted source. The root CA certificate for clients must be provided if the client certificates are issued by a different CA hierarchy than the CA hierarchy that issued the management point certificate.
