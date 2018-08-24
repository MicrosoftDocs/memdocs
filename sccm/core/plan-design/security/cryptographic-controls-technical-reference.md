---
title: "Cryptographic controls technical reference"
titleSuffix: "Configuration Manager"
description: "Learn how signing and encryption can help protect attacks from reading data in System Center Configuration Manager."
ms.date: 12/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Cryptographic controls technical reference

*Applies to: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager uses signing and encryption to help protect the management of the devices in the Configuration Manager hierarchy. With signing, if data has been altered in transit, it's discarded. Encryption helps prevent an attacker from reading the data by using a network protocol analyzer.  

 The primary hashing algorithm that Configuration Manager uses for signing is SHA-256. When two Configuration Manager sites communicate with each other, they sign their communications with SHA-256. The primary encryption algorithm implemented in Configuration Manager is 3DES. This is used for storing data in the Configuration Manager database and for client HTTP communication. When you use client communication over HTTPS, you can configure your public key infrastructure (PKI) to use RSA certificates with the maximum hashing algorithms and key lengths that are documented in [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  

 For most cryptographic operations for Windows-based operating systems, Configuration Manager uses SHA-2, 3DES and AES, and RSA algorithms from the Windows CryptoAPI library rsaenh.dll.  

> [!IMPORTANT]  
>  See information about recommended changes in response to SSL vulnerabilities in [About SSL Vulnerabilities](#about-ssl-vulnerabilities).  

##  Cryptographic controls for Configuration Manager operations  
 Information in Configuration Manager can be signed and encrypted, whether or not you use PKI certificates with Configuration Manager.  

### Policy signing and encryption  
 Client policy assignments are signed by the self-signed site server signing certificate to help prevent the security risk of a compromised management point sending policies that have been tampered with. This is important if you are using Internet-based client management because this environment requires a management point that is exposed to Internet communication.  

 Policy is encrypted with 3DES when it contains sensitive data. Policy that contains sensitive data is sent to authorized clients only. Policy that does not have sensitive data is not encrypted.  

 When policy is stored on the clients, it is encrypted with Data Protection application programming interface (DPAPI).  

### Policy hashing  
 When Configuration Manager clients request policy, they first get a policy assignment so that they know which policies apply to them, and then they request only those policy bodies. Each policy assignment contains the calculated hash for the corresponding policy body. The client retrieves the applicable policy bodies and then calculates the hash on that body. If the hash on the downloaded policy body does not match the hash in the policy assignment, the client discards the policy body.  

 The hashing algorithm for policy is SHA-1 and SHA-256.  

### Content hashing  
 The distribution manager service on the site server hashes the content files for all packages. The policy provider includes the hash in the software distribution policy. When the Configuration Manager client downloads the content, the client regenerates the hash locally and compares it to the one supplied in the policy. If the hashes match, the content has not been altered and the client installs it. If a single byte of the content has been altered, the hashes will not match and the software will not be installed. This check helps to ensure that the correct software is installed because the actual content is crosschecked with the policy.  

 The default hashing algorithm for content is SHA-256. To change this default, see the documentation for the Configuration Manager Software Development Kit (SDK).  

 Not all devices can support content hashing. The exceptions include:  

-   Windows clients when they stream App-V content.  

-   Windows Phone clients, though these clients verify the signature of an application that is signed by a trusted source.  

-   Windows RT client, though these clients verify the signature of an application that is signed by a trusted source and also use package full name (PFN) validation.  

-   iOS, though these devices verify the signature of an application that is signed by any developer certificate from a trusted source.  

-   Nokia client, though, these clients verify the signature of an application that uses a self-signed certificate. Or, the signature of a certificate from a trusted source and the certificate can sign Nokia Symbian Installation Source (SIS) applications.  

-   Android. In addition, these devices do not use signature validation for application installation.  

-   Clients that run on versions of Linux and UNIX that do not support SHA-256. For more information, see [Planning for client deployment to Linux and UNIX computers](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers).  

### Inventory signing and encryption  
 Inventory that clients send to management points is always signed by devices, regardless of whether they communicate with management points over HTTP or HTTPS. If they use HTTP, you can choose to encrypt this data, which is a security best practice.  

### State migration encryption  
 Data stored on state migration points for operating system deployment is always encrypted by the User State Migration Tool (USMT) by using 3DES.  

### Encryption for multicast packages to deploy operating systems  
 For every operating system deployment package, you can enable encryption when the package is transferred to computers by using multicast. The encryption uses Advanced Encryption Standard (AES). If you enable encryption, no additional certificate configuration is required. The multicast-enabled distribution point automatically generates symmetric keys for encrypting the package. Each package has a different encryption key. The key is stored on the multicast-enabled distribution point by using standard Windows APIs. When the client connects to the multicast session, the key exchange occurs over a channel encrypted with either the PKI-issued client authentication certificate (when the client uses HTTPS) or the self-signed certificate (when the client uses HTTP). The client stores the key in memory only for the duration of the multicast session.  

### Encryption for media to deploy operating systems  
 When you use media to deploy operating systems and specify a password to protect the media, the environment variables are encrypted by using Advanced Encryption Standard (AES). Other data on the media, including packages and content for applications, is not encrypted.  

### Encryption for content that is hosted on cloud-based distribution points  
 Beginning with System Center 2012 Configuration Manager SP1, when you use cloud-based distribution points, the content that you upload to these distribution points is encrypted by using Advanced Encryption Standard (AES) with a 256-bit key size. The content is re-encrypted whenever you update it. When clients download the content, it is encrypted and protected by the HTTPS connection.  

### Signing in software updates  
 All software updates must be signed by a trusted publisher to protect against tampering. On client computers, the Windows Update Agent (WUA) scans for the updates from the catalog, but will not install the update if it cannot locate the digital certificate in the Trusted Publishers store on the local computer. If a self-signed certificate was used for publishing the updates catalog, such as WSUS Publishers Self-signed, the certificate must also be in the Trusted Root Certification Authorities certificate store on the local computer to verify the validity of the certificate. WUA also checks whether the **Allow signed content from intranet Microsoft update service location Group Policy** setting is enabled on the local computer. This policy setting must be enabled for WUA to scan for the updates that were created and published with Updates Publisher.  

 When software updates are published in System Center Updates Publisher, a digital certificate signs the software updates when they are published to an update server. You can either specify a PKI certificate or configure Updates Publisher to generate a self-signed certificate to sign the software update.  

### Signed configuration data for compliance settings  
 When you import configuration data, Configuration Manager verifies the file's digital signature. If the files have not been signed, or if the digital signature verification check fails, you will be warned and prompted whether to continue with the import. Continue to import the configuration data only if you explicitly trust the publisher and the integrity of the files.  

### Encryption and hashing for client notification  
 If you use client notification, all communication uses TLS and the highest encryption that the server and client operating systems can negotiate. For example, a client computer running Windows 7 and a management point running Windows Server 2008 R2 can support 128-bit AES encryption, whereas a client computer running Vista to the same management point but will negotiate down to 3DES encryption. The same negotiation occurs for hashing the packets that are transferred during client notification, which uses SHA-1 or SHA-2.  

##  Certificates used by Configuration Manager  
 For a list of the public key infrastructure (PKI) certificates that can be used by Configuration Manager, any special requirements or limitations, and how the certificates are used, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements). This list includes the supported hash algorithms and key lengths. Most certificates support SHA-256 and 2048 bits key length.  

> [!NOTE]  
>  All certificates that Configuration Manager uses must contain only single-byte characters in the subject name or subject alternative name.  

 PKI certificates are required for the following scenarios:  

-   When you manage Configuration Manager clients on the Internet.  

-   When you manage Configuration Manager clients on mobile devices.  

-   When you manage Mac computers.  

-   When you use cloud-based distribution points.  

-   When you manage Intel AMT-based computers out of band.  

 For most other Configuration Manager communications that require certificates for authentication, signing, or encryption, Configuration Manager automatically uses PKI certificates if they are available. If they are not available, Configuration Manager generates self-signed certificates.  

 Configuration Manager does not use PKI certificates when it manages mobile devices by using the Exchange Server connector.  

### Mobile device management and PKI certificates  
 If the mobile device has not been locked by the mobile operator, you can use Configuration Manager or Microsoft Intune to request and install a client certificate. This certificate provides mutual authentication between the client on the mobile device and Configuration Manager site systems or Microsoft Intune services. If your mobile device is locked, you cannot use Configuration Manager or Intune to deploy certificates.  

 If you enable hardware inventory for mobile devices, Configuration Manager or Intune also inventories the certificates that are installed on the mobile device.   

### Operating system deployment and PKI certificates  
 When you use Configuration Manager to deploy operating systems and a management point requires HTTPS client connections, the client computer must also have a certificate to communicate with the management point, even though it is in a transitional phase such as booting from task sequence media or a PXE-enabled distribution point. To support this scenario, you must create a PKI client authentication certificate and export it with the private key and then import it to the site server properties and also add the management pointâ€™s trusted root CA certificate.  

 If you create bootable media, you import the client authentication certificate when you create the bootable media. Configure a password on the bootable media to help protect the private key and other sensitive data configured in the task sequence. Every computer that boots from the bootable media will present the same certificate to the management point as required for client functions such as requesting client policy.  

 If you use PXE boot, you import the client authentication certificate to the PXE-enabled distribution point and it uses the same certificate for every client that boots from that PXE-enabled distribution point. As a security best practice, require users who connect their computers to a PXE service to supply a password to help protect the private key and other sensitive data in the task sequences.  

 If either of these client authentication certificates is compromised, block the certificates in the **Certificates** node in the **Administration** workspace, **Security** node. To manage these certificates, you must have the **Manage operating system deployment certificate** right.  

 After the operating system is deployed and the Configuration Manager is installed, the client will require its own PKI client authentication certificate for HTTPS client communication.  

### ISV proxy solutions and PKI certificates  
 Independent Software Vendors (ISVs) can create applications that extend Configuration Manager. For example, an ISV could create extensions to support non-Windows client platforms such as Macintosh or UNIX computers. However, if the site systems require HTTPS client connections, these clients must also use PKI certificates for communication with the site. Configuration Manager includes the ability to assign a certificate to the ISV proxy that enables communications between the ISV proxy clients and the management point. If you use extensions that require ISV proxy certificates, consult the documentation for that product. For more information about how to create ISV proxy certificates, see the Configuration Manager Software Developer Kit (SDK).  

 If the ISV certificate is compromised, block the certificate in the **Certificates** node in the **Administration** workspace, **Security** node.  

### Asset intelligence and certificates  
 Configuration Manager installs with an X.509 certificate that the Asset Intelligence synchronization point uses to connect to Microsoft. Configuration Manager uses this certificate to request a client authentication certificate from the Microsoft certificate service. The client authentication certificate is installed on the Asset Intelligence synchronization point site system server and it is used to authenticate the server to Microsoft. Configuration Manager uses the client authentication certificate to download the Asset Intelligence catalog and to upload software titles.  

 This certificate has a key length of 1024 bits.  

### Cloud-based distribution points and certificates  
 Beginning with System Center 2012 Configuration Manager SP1, cloud-based distribution points require a management certificate (self-signed or PKI) that you upload to Microsoft Azure. This management certificate requires server authentication capability and a certificate key length of 2048 bits. In addition, you must configure a service certificate for each cloud-based distribution point, which cannot be self-signed but also has server authentication capability and a minimum certificate key length of 2048 bits.  

> [!NOTE]  
>  The self-signed management certificate is for testing purposes only and not for use on production networks.  

 Clients do not require a client PKI certificate to use cloud-based distribution points; they authenticate to the management by using either a self-signed certificate or a client PKI certificate. The management point then issues a Configuration Manager access token to the client, which the client presents to the cloud-based distribution point. The token is valid for 8 hours.  

### The Microsoft Intune Connector and certificates  
 When Microsoft Intune enrolls mobile devices, you can manage these mobile devices in Configuration Manager by creating a Microsoft Intune connector. The connector uses a PKI certificate with client authentication capability to authenticate Configuration Manager to Microsoft Intune and to transfer all information between them by using SSL. The certificate key size is 2048 bits and uses the SHA-1 hash algorithm.  

 When you install the connector, a signing certificate is created and stored on the site server for sideloading keys, and an encryption certificate is created and stored on the certificate registration point to encrypt the Simple Certificate Enrollment Protocol (SCEP) challenge. These certificates also have a key size of 2048 bits and use the SHA-1 hash algorithm.  

 When Intune enrolls mobile devices, it installs a PKI certificate onto the mobile device. This certificate has client authentication capability, uses a key size of 2048 bits, and uses the SHA-1 hash algorithm.  

 These PKI certificates are automatically requested, generated, and installed by Microsoft Intune.  

### CRL checking for PKI certificates  
 A PKI certificate revocation list (CRL) increases administrative and processing overhead but it is more secure. However, if CRL checking is enabled but the CRL is inaccessible, the PKI connection fails. For more information, see [Security and privacy for Configuration Manager](/sccm/core/plan-design/security/security-and-privacy).  

 Certificate revocation list (CRL) checking is enabled by default in IIS, so if you are using a CRL with your PKI deployment, there is nothing additional to configure on most Configuration Manager site systems that run IIS. The exception is for software updates, which requires a manual step to enable CRL checking to verify the signatures on software update files.  

 CRL checking is enabled by default for client computers when they use HTTPS client connections. CRL checking is not enabled by default when you run the Out of Band Management console to connect to AMT-based computer, and you can enable this option. You cannot disable CRL checking for clients on Mac computers in Configuration Manager SP1 or later.  

 CRL checking is not supported for the following connections in Configuration Manager:  

-   Server-to-server connections.  

-   Mobile devices that are enrolled by Configuration Manager.  

-   Mobile devices that are enrolled by Microsoft Intune.  

##  Cryptographic controls for server communication  
 Configuration Manager uses the following cryptographic controls for server communication.  

### Server communication within a site  
 Each site system server uses a certificate to transfer data to other site systems in the same Configuration Manager site. Some site system roles also use certificates for authentication. For example, if you install the enrollment proxy point on one server and the enrollment point on another server, they can authenticate one another by using this identity certificate. When Configuration Manager uses a certificate for this communication, if there is a PKI certificate available that has server authentication capability, Configuration Manager automatically uses it; if not, Configuration Manager generates a self-signed certificate. This self-signed certificate has server authentication capability, uses SHA-256, and has a key length of 2048 bits. Configuration Manager copies the certificate to the Trusted People store on other site system servers that might need to trust the site system. Site systems can then trust one another by using these certificates and PeerTrust.  

 In addition to this certificate for each site system server, Configuration Manager generates a self-signed certificate for most site system roles. When there is more than one instance of the site system role in the same site, they share the same certificate. For example, you might have multiple management points or multiple enrollment points in the same site. This self-signed certificate also uses SHA-256 and has a key length of 2048 bits. It is also copied to the Trusted People Store on site system servers that might need to trust it. The following site system roles generate this certificate:  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Asset Intelligence synchronization point  

-   Certificate registration point  

-   Endpoint Protection point  

-   Enrollment point  

-   Fallback status point  

-   Management point  

-   Multicast-enabled distribution point  

-   Out of band service point  

-   Reporting services point  

-   Software update point  

-   State migration point  

-   System Health Validator point  

-   Microsoft Intune connector  

 These certificates are managed automatically by Configuration Manager, and where necessary, automatically generated.  

 Configuration Manager also uses a client authentication certificate to send status messages from the distribution point to the management point. When the management point is configured for HTTPS client connections only, you must use a PKI certificate. If the management point accepts HTTP connections, you can use a PKI certificate or select the option to use a self-signed certificate that has client authentication capability, uses SHA-256, and has a key length of 2048 bits.  

### Server communication between sites  
 Configuration Manager transfers data between sites by using database replication and file-based replication. For more information, see [Communications between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

 Configuration Manager automatically configures the database replication between sites and uses PKI certificates that have server authentication capability if these are available; if not, Configuration Manager creates self-signed certificates for server authentication. In both cases, authentication between sites is established by using certificates in the Trusted People Store that uses PeerTrust. This certificate store is used to ensure that only the SQL Server computers that are used by the Configuration Manager hierarchy participate in site-to-site replication. Whereas primary sites and the central administration site can replicate configuration changes to all sites in the hierarchy, secondary sites can replicate configuration changes only to their parent site.  

 Site servers establish site-to-site communication by using a secure key exchange that happens automatically. The sending site server generates a hash and signs it with its private key. The receiving site server checks the signature by using the public key and compares the hash with a locally generated value. If they match, the receiving site accepts the replicated data. If the values do not match, Configuration Manager rejects the replication data.  

 Database replication in Configuration Manager uses the SQL Server Service Broker to transfer data between sites by using the following mechanisms:  

-   SQL Server to SQL Server connection: This uses Windows credentials for server authentication and self-signed certificates with 1024 bits to sign and encrypt the data by using Advanced Encryption Standard (AES). If PKI certificates with server authentication capability are available, these will be used. The certificate must be located in the Personal store for the Computer certificate store.  

-   SQL Service Broker: This uses self-signed certificates with 2048 bits for authentication and to sign and encrypt the data by using Advanced Encryption Standard (AES). The certificate must be located in the SQL Server master database.  

 File-based replication uses the Server Message Block (SMB) protocol, and uses SHA-256 to sign this data that is not encrypted but does not contain any sensitive data. If you want to encrypt this data, you can use IPsec and must implement this independently from Configuration Manager.  

##  Cryptographic controls for clients that use HTTPS communication to site systems  
 When site system roles accept client connections, you can configure them to accept HTTPS and HTTP connections, or only HTTPS connections. Site system roles that accept connections from the Internet only accept client connections over HTTPS.  

 Client connections over HTTPS offer a higher level of security by integrating with a public key infrastructure (PKI) to help protect client-to-server communication. However, configuring HTTPS client connections without a thorough understanding of PKI planning, deployment, and operations could still leave you vulnerable. For example, if you do not secure your root CA, attackers could compromise the trust of your entire PKI infrastructure. Failing to deploy and manage the PKI certificates by using controlled and secured processes might result in unmanaged clients that cannot receive critical software updates or packages.  

> [!IMPORTANT]  
>  The PKI certificates that are used for client communication protect the communication only between the client and some site systems. They do not protect the communication channel between the site server and site systems or between site servers.  

### Communication that is unencrypted when clients use HTTPS communication  
 When clients communicate with site systems by using HTTPS, communications are usually encrypted over SSL. However, in the following situations, clients communicate with site systems without using encryption:  

-   Client fails to make an HTTPS connection on the intranet and fall back to using HTTP when site systems allow this configuration  

-   Communication to the following site system roles:  

    -   Client sends state messages to the fallback status point  

    -   Client sends PXE requests to a PXE-enabled distribution point  

    -   Client sends notification data to a management point  

 Reporting services points are configured to use HTTP or HTTPS independently from the client communication mode.  

##  Cryptographic controls for clients chat use HTTP communication to site systems  
 When clients use HTTP communication to site system roles, they can use PKI certificates for client authentication, or self-signed certificates that Configuration Manager generates. When Configuration Manager generates self-signed certificates, they have a custom object identifier for signing and encryption, and these certificates are used to uniquely identify the client. For all supported operating systems except Windows Server 2003, these self-signed certificates use SHA-256, and have a key length of 2048 bits. For Windows Server 2003, SHA1 is used with a key length of 1024 bits.  

### Operating system deployment and self-signed certificates  
 When you use Configuration Manager to deploy operating systems with self-signed certificates, a client computer must also have a certificate to communicate with the management point, even if the computer is in a transitional phase such as booting from task sequence media or a PXE-enabled distribution point. To support this scenario for HTTP client connections, Configuration Manager generates self-signed certificates that have a custom object identifier for signing and encryption, and these certificates are used to uniquely identify the client. For all supported operating systems except Windows Server 2003, these self-signed certificates use SHA-256, and have a key length of 2048 bits. For Windows Server 2003, SHA1 is used with a key length of 1024 bits. If these self-signed certificates are compromised, to prevent attackers from using them to impersonate trusted clients, block the certificates in the **Certificates** node in the **Administration** workspace, **Security** node.  

### Client and server authentication  
 When clients connect over HTTP, they authenticate the management points by using either Active Directory Domain Services or by using the Configuration Manager trusted root key. Clients do not authenticate other site system roles, such as state migration points or software update points.  

 When a management point first authenticates a client by using the self-signed client certificate, this mechanism provides minimal security because any computer can generate a self-signed certificate. In this scenario, the client identity process must be augmented by approval. Only trusted computers must be approved, either automatically by Configuration Manager, or manually, by an administrative user. For more information, see the approval section in [Communications between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

## About SSL vulnerabilities
To improve the security of your Configuration Manager clients and servers, do the following:

-	Enable TLS 1.2

    To enable TLS 1.2 for Configuration Manager, see the following KB article: [How to enable TLS 1.2 for Configuration Manager](https://support.microsoft.com/en-us/help/4040243/how-to-enable-tls-1-2-for-configuration-manager).
-	Disable SSL 3.0, TLS 1.0, and TLS 1.1 
-	Reorder the TLS-related cipher suites 

For more information, see [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/en-us/kb/245030/) and [Prioritizing Schannel Cipher Suites](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx). These procedures do not affect Configuration Manager functionality.

