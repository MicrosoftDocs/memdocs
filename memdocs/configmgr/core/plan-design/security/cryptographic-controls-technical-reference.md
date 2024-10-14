---
title: Cryptographic controls technical reference
titleSuffix: Configuration Manager
description: Learn how signing and encryption can help protect attacks from reading data in Configuration Manager.
ms.date: 10/15/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: reference
author: Baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Cryptographic controls technical reference

*Applies to: Configuration Manager (current branch)*

Configuration Manager uses signing and encryption to help protect the management of the devices in the Configuration Manager hierarchy. With signing, if data has been altered in transit, it's discarded. Encryption helps prevent an attacker from reading the data by using a network protocol analyzer.

The primary hashing algorithm that Configuration Manager uses for signing is **SHA-256**. When two Configuration Manager sites communicate with each other, they sign their communications with SHA-256.

Starting in version 2107, the primary encryption algorithm that Configuration Manager uses is **AES-256**. Encryption mainly happens in the following two areas:

- If you enable the site to **Use encryption**, the client encrypts its inventory data and state messages that it sends to the management point.

- When the client downloads secret policies, the management point always encrypts these policies. For example, an OS deployment task sequence that includes passwords.


> [!NOTE]
> If you configure HTTPS communication, these messages are encrypted twice. The message is encrypted with AES, then the HTTPS transport is encrypted with AES-256. 

When you use client communication over HTTPS, configure your public key infrastructure (PKI) to use certificates with the maximum hashing algorithms and key lengths. When using CNG v3 certificates, Configuration Manager clients only support certificates that use the RSA cryptographic algorithm. For more information, see [PKI certificate requirements](../network/pki-certificate-requirements.md) and [CNG v3 certificates overview](../network/cng-certificates-overview.md).

For transport security, anything that uses TLS supports AES-256. This support includes when you configure the site for [enhanced HTTP (E-HTTP)](../hierarchy/enhanced-http.md) or HTTPS. For on-premises site systems, you can control the TLS cipher suites. For cloud-based roles like the cloud management gateway (CMG), if you enable TLS 1.2, Configuration Manager configures the cipher suites.

For most cryptographic operations with Windows-based operating systems, Configuration Manager uses these algorithms from the Windows CryptoAPI library rsaenh.dll.

For more information about specific functionality, see [Site operations](#site-operations).

## Site operations

Information in Configuration Manager can be signed and encrypted. It supports these operations with or without PKI certificates.

### Policy signing and encryption

The site signs client policy assignments with its self-signed certificate. This behavior helps prevent the security risk of a compromised management point from sending tampered policies. If you use [internet-based client management](../../clients/manage/plan-internet-based-client-management.md), this behavior is important because it requires an internet-facing management point.

When policy contains sensitive data, starting in version 2107, the management point encrypts it with AES-256. Policy that contains sensitive data is only sent to authorized clients. The site doesn't encrypt policy that doesn't have sensitive data.

When a client stores policy, it encrypts the policy using the Windows data protection application programming interface (DPAPI).

### Policy hashing

When a client requests policy, it first gets a policy assignment. Then it knows which policies apply to it, and it can request only those policy bodies. Each policy assignment contains the calculated hash for the corresponding policy body. The client downloads the applicable policy bodies and then calculates the hash for each policy body. If the hash on the policy body doesn't match the hash in the policy assignment, the client discards the policy body.

The hashing algorithm for policy is **SHA-256**.

### Content hashing  

The distribution manager service on the site server hashes the content files for all packages. The policy provider includes the hash in the software distribution policy. When the Configuration Manager client downloads the content, the client regenerates the hash locally and compares it to the one supplied in the policy. If the hashes match, the content isn't altered, and the client installs it. If a single byte of the content is altered, the hashes won't match, and the client doesn't install the software. This check helps to make sure that the correct software is installed because the actual content is compared with the policy.

The default hashing algorithm for content is **SHA-256**.

Not all devices can support content hashing. The exceptions include:

- Windows clients when they stream App-V content.

### Inventory signing and encryption

When a client sends hardware or software inventory to a management point, it always signs the inventory. It doesn't matter if the client communicates with the management point over E-HTTP or HTTPS. If they use E-HTTP, you can also choose to encrypt this data, which is recommended.

### State migration encryption

When a task sequence captures data from a client for OS deployment, it always encrypts the data. In version 2103 and later, the task sequence runs the User State Migration Tool (USMT) with the **AES-256** encryption algorithm.<!--9171505-->

### Encryption for multicast packages

For every OS deployment package, you can enable encryption when you use multicast. This encryption uses the **AES-256** algorithm. If you enable encryption, no other certificate configuration is required. The multicast-enabled distribution point automatically generates symmetric keys to encrypt the package. Each package has a different encryption key. The key is stored on the multicast-enabled distribution point by using standard Windows APIs.

When the client connects to the multicast session, the key exchange occurs over an encrypted channel. If the client uses HTTPS, it uses the PKI-issued client authentication certificate. If the client uses E-HTTP, it uses the self-signed certificate. The client only stores the encryption key in memory during the multicast session.

### Encryption for OS deployment media

When you use media to deploy operating systems, you should always specify a password to protect the media. With a password, the task sequence environment variables are encrypted with **AES-128**. Other data on the media, including packages and content for applications, isn't encrypted.

### Encryption for cloud-based content

When you enable a cloud management gateway (CMG) to store content, the content is encrypted with **AES-256**. The content is encrypted whenever you update it. When clients download the content, it's encrypted and protected by the HTTPS connection.

### Signing in software updates

All software updates must be signed by a trusted publisher to protect against tampering. On client computers, the Windows Update Agent (WUA) scans for the updates from the catalog. It won't install the update if it can't locate the digital certificate in the Trusted Publishers store on the local computer.

When you publish software updates with System Center Updates Publisher, a digital certificate signs the software updates. You can either specify a PKI certificate or configure Updates Publisher to generate a self-signed certificate to sign the software update. If you use a self-signed certificate to publish the updates catalog, such as WSUS Publishers Self-signed, the certificate must also be in the Trusted Root Certification Authorities certificate store on the local computer. WUA also checks whether the **Allow signed content from intranet Microsoft update service location** group policy setting is enabled on the local computer. This policy setting must be enabled for WUA to scan for the updates that were created and published with System Center Updates Publisher.

### Signed configuration data for compliance settings

When you import configuration data, Configuration Manager verifies the file's digital signature. If the files aren't signed, or if the signature check fails, the console warns you to continue with the import. Only import the configuration data if you explicitly trust the publisher and the integrity of the files.

### Encryption and hashing for client notification

If you use client notification, all communication uses TLS and the highest algorithms that the server and client can negotiate. The same negotiation occurs for hashing the packets that are transferred during client notification, which uses **SHA-2**.

## Certificates

For a list of the public key infrastructure (PKI) certificates that can be used by Configuration Manager, any special requirements or limitations, and how the certificates are used, see [PKI certificate requirements](../network/pki-certificate-requirements.md). This list includes the supported hash algorithms and key lengths. Most certificates support **SHA-256** and **2048**-bits key length.

Most Configuration Manager operations that use certificates also support v3 certificates. For more information, see [CNG v3 certificates overview](../network/cng-certificates-overview.md).

> [!NOTE]
> All certificates that Configuration Manager uses must contain only single-byte characters in the subject name or subject alternative name.

Configuration Manager requires PKI certificates for the following scenarios:

- When you manage Configuration Manager clients on the internet

- When you use a cloud management gateway (CMG)

For most other communication that requires certificates for authentication, signing, or encryption, Configuration Manager automatically uses PKI certificates if available. If they aren't available, Configuration Manager generates self-signed certificates.


### Mobile device management and PKI certificates

> [!NOTE]
> Since Nov 2021 we have deprecated Mobile device management and we recommend customers to uninstall this role.

### OS deployment and PKI certificates

When you use Configuration Manager to deploy operating systems, and a management point requires HTTPS client connections, the client needs a certificate to communicate with the management point. This requirement is even when the client is in a transitional phase such as booting from task sequence media or a PXE-enabled distribution point. To support this scenario, create a PKI client authentication certificate, and export it with the private key. Then import it to the site server properties and also add the management point's trusted root CA certificate.

If you create bootable media, you import the client authentication certificate when you create the bootable media. To help protect the private key and other sensitive data configured in the task sequence, configure a password on the bootable media. Every computer that boots from the bootable media uses the same certificate with the management point as required for client functions such as requesting client policy.

If you use PXE, import the client authentication certificate to the PXE-enabled distribution point. It uses the same certificate for every client that boots from that PXE-enabled distribution point. To help protect the private key and other sensitive data in the task sequences, require a password for PXE.

If either of these client authentication certificates is compromised, block the certificates in the **Certificates** node in the **Administration** workspace, **Security** node. To manage these certificates, you need the permission to **Manage operating system deployment certificate**.

After Configuration Manager deploys the OS installs the client, the client requires its own PKI client authentication certificate for HTTPS client communication.

### ISV proxy solutions and PKI certificates

Independent Software Vendors (ISVs) can create applications that extend Configuration Manager. For example, an ISV could create extensions to support non-Windows client platforms. However, if the site systems require HTTPS client connections, these clients must also use PKI certificates for communication with the site. Configuration Manager includes the ability to assign a certificate to the ISV proxy that enables communications between the ISV proxy clients and the management point. If you use extensions that require ISV proxy certificates, consult the documentation for that product.

If the ISV certificate is compromised, block the certificate in the **Certificates** node in the **Administration** workspace, **Security** node.

#### Copy GUID for ISV proxy certificate

<!--2842082-->

Starting in version 2111, to simplify the management of these ISV proxy certificates, you can now copy its GUID in the Configuration Manager console.

1. In the Configuration Manager console, go to the **Administration** workspace.

1. Expand **Security**, and select the **Certificates** node.

1. Sort the list of the certificates by the **Type** column.

1. Select a certificate of type **ISV Proxy**.

1. In the ribbon, select **Copy Certificate GUID**.

This action copies this certificate's GUID, for example: `aa05bf38-5cd6-43ea-ac61-ab101f943987`

### Asset Intelligence and certificates

> [!NOTE]
> Since Nov 2021 we have deprecated Mobile device management and we recommend customers to uninstall this role.

### Azure services and certificates

The cloud management gateway (CMG) requires server authentication certificates. These certificates allow the service to provide HTTPS communication to clients over the internet. For more information, see [CMG server authentication certificate](../../clients/manage/cmg/server-auth-cert.md).

Clients require another type of authentication to communicate with a CMG and the on-premises management point. They can use Microsoft Entra ID, a PKI certificate, or a site token. For more information, see [Configure client authentication for cloud management gateway](../../clients/manage/cmg/configure-authentication.md).

Clients don't require a client PKI certificate to use cloud-based storage. After they authenticate to the management point, the management point issues a Configuration Manager access token to the client. The client presents this token to the CMG to access the content. The token is valid for eight hours.

### CRL checking for PKI certificates

A PKI certificate revocation list (CRL) increases overall security, but does require some administrative and processing overhead. If you enable CRL checking, but clients can't access the CRL, the PKI connection fails.

IIS enables CRL checking by default. If you use a CRL with your PKI deployment, you don't need to configure most site systems that run IIS. The exception is for software updates, which requires a manual step to enable CRL checking to verify the signatures on software update files.

When a client uses HTTPS, it enables CRL checking by default. 

The following connections don't support CRL checking in Configuration Manager:

- Server-to-server connections

## Server communication

Configuration Manager uses the following cryptographic controls for server communication.

### Server communication within a site

Each site system server uses a certificate to transfer data to other site systems in the same Configuration Manager site. Some site system roles also use certificates for authentication. For example, if you install the enrollment proxy point on one server, and the enrollment point on another server, they can authenticate one another by using this identity certificate.

When Configuration Manager uses a certificate for this communication, if there's a PKI certificate available with server authentication capability, Configuration Manager automatically uses it. If not, Configuration Manager generates a self-signed certificate. This self-signed certificate has server authentication capability, uses SHA-256, and has a key length of 2048 bits. Configuration Manager copies the certificate to the Trusted People store on other site system servers that might need to trust the site system. Site systems can then trust one another by using these certificates and PeerTrust.

In addition to this certificate for each site system server, Configuration Manager generates a self-signed certificate for most site system roles. When there is more than one instance of the site system role in the same site, they share the same certificate. For example, you might have multiple management points in the same site. This self-signed certificate uses SHA-256 and has a key length of 2048 bits. It's copied to the Trusted People Store on site system servers that might need to trust it. The following site system roles generate this certificate:

- Asset Intelligence synchronization point

- Endpoint Protection point

- Fallback status point

- Management point

- Multicast-enabled distribution point

- Reporting services point

- Software update point

- State migration point

Configuration Manager automatically generates and manages these certificates.

To send status messages from the distribution point to the management point, Configuration Manager uses a client authentication certificate. When you configure the management point for HTTPS, it requires a PKI certificate. If the management point accepts E-HTTP connections, you can use a PKI certificate. It can also use a self-signed certificate with client authentication capability, uses SHA-256, and has a key length of 2048 bits.

### Server communication between sites

Configuration Manager transfers data between sites by using database replication and file-based replication. For more information, see [Data transfers between sites](../hierarchy/data-transfers-between-sites.md) and [Communications between endpoints](../hierarchy/communications-between-endpoints.md).

Configuration Manager automatically configures the database replication between sites. If available, it uses PKI certificates with server authentication capability. If not available, Configuration Manager creates self-signed certificates for server authentication. In both cases, it authenticates between sites by using certificates in the Trusted People store that uses PeerTrust. It uses this certificate store to make sure that only the Configuration Manager hierarchy SQL Servers participate in site-to-site replication.

Site servers establish site-to-site communication by using a secure key exchange that happens automatically. The sending site server generates a hash and signs it with its private key. The receiving site server checks the signature by using the public key and compares the hash with a locally generated value. If they match, the receiving site accepts the replicated data. If the values don't match, Configuration Manager rejects the replication data.

Database replication in Configuration Manager uses the SQL Server Service Broker to transfer data between sites. It uses the following mechanisms:

- SQL Server to SQL Server: This connection uses Windows credentials for server authentication and self-signed certificates with 1024 bits to sign and encrypt the data with the AES algorithm. If available, it uses PKI certificates with server authentication capability. It only uses certificates in the computer's Personal certificate store.

- SQL Service Broker: This service uses self-signed certificates with 2048 bits for authentication and to sign and encrypt the data with the AES algorithm. It only uses certificates in the SQL Server master database.

File-based replication uses the server message block (SMB) protocol. It uses **SHA-256** to sign data that isn't encrypted and doesn't contain any sensitive data. To encrypt this data, use IPsec, which you implement independently from Configuration Manager.

## Clients that use HTTPS

When site system roles accept client connections, you can configure them to accept HTTPS and HTTP connections, or only HTTPS connections. Site system roles that accept connections from the internet only accept client connections over HTTPS.

Client connections over HTTPS offer a higher level of security by integrating with a public key infrastructure (PKI) to help protect client-to-server communication. However, configuring HTTPS client connections without a thorough understanding of PKI planning, deployment, and operations could still leave you vulnerable. For example, if you don't secure your root certificate authority (CA), attackers could compromise the trust of your entire PKI infrastructure. Failing to deploy and manage the PKI certificates by using controlled and secured processes might result in unmanaged clients that can't receive critical software updates or packages.

> [!IMPORTANT]
> The PKI certificates that Configuration Manager uses for client communication protect the communication only between the client and some site systems. They don't protect the communication channel between the site server and site systems or between site servers.

### Unencrypted communication when clients use HTTPS

When clients communicate with site systems over HTTPS, most traffic is encrypted. In the following situations, clients communicate with site systems without using encryption:

- Client fails to make an HTTPS connection on the intranet and falls back to using HTTP when site systems allow this configuration.

- Communication to the following site system roles:

  - Client sends state messages to the fallback status point.

  - Client sends PXE requests to a PXE-enabled distribution point.

  - Client sends notification data to a management point.

You configure reporting services points to use HTTP or HTTPS independently from the client communication mode.

## Clients that use E-HTTP

When clients use E-HTTP communication to site system roles, they can use PKI certificates for client authentication, or self-signed certificates that Configuration Manager generates. When Configuration Manager generates self-signed certificates, they have a custom object identifier for signing and encryption. These certificates are used to uniquely identify the client. These self-signed certificates use **SHA-256**, and have a key length of 2048 bits.

### OS deployment and self-signed certificates

When you use Configuration Manager to deploy operating systems with self-signed certificates, the client must also have a certificate to communicate with the management point. This requirement is even if the computer is in a transitional phase such as booting from task sequence media or a PXE-enabled distribution point. To support this scenario for E-HTTP client connections, Configuration Manager generates self-signed certificates that have a custom object identifier for signing and encryption. These certificates are used to uniquely identify the client. These self-signed certificates use **SHA-256**, and have a key length of 2048 bits. If these self-signed certificates are compromised, prevent attackers from using them to impersonate trusted clients. Block the certificates in the **Certificates** node in the **Administration** workspace, **Security** node.

### Client and server authentication

When clients connect over E-HTTP, they authenticate the management points by using either Active Directory Domain Services or by using the Configuration Manager trusted root key. Clients don't authenticate other site system roles, such as state migration points or software update points.

When a management point first authenticates a client by using the self-signed client certificate, this mechanism provides minimal security because any computer can generate a self-signed certificate. Use client approval to enhance this process. Only approve trusted computers, either automatically by Configuration Manager, or manually by an administrative user. For more information, see [Manage clients](../../clients/manage/manage-clients.md#approve).

## About SSL vulnerabilities

To improve the security of your Configuration Manager clients and servers, do the following actions:

- Enable TLS 1.2 across all devices and services. To enable TLS 1.2 for Configuration Manager, see [How to enable TLS 1.2 for Configuration Manager](enable-tls-1-2.md).

- Disable SSL 3.0, TLS 1.0, and TLS 1.1.

- Reorder the TLS-related cipher suites.

For more information, see the following articles:

- [Restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](/troubleshoot/windows-server/windows-security/restrict-cryptographic-algorithms-protocols-schannel)
- [Prioritizing Schannel cipher suites](/windows/win32/secauthn/prioritizing-schannel-cipher-suites)

These procedures don't affect Configuration Manager functionality.

> [!NOTE]
> Updates to Configuration Manager download from the Azure content delivery network (CDN), which has cipher suite requirements. For more information, see [Azure Front Door: TLS configuration FAQ](/azure/frontdoor/front-door-faq#tls-configuration)..<!-- 10424111 -->
