---
title: Site administration security and privacy
titleSuffix: Configuration Manager
description: Optimize security and privacy for site administration in Configuration Manager
ms.date: 04/05/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Security and privacy for site administration in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article contains security and privacy information for Configuration Manager sites and the hierarchy.

## <a name="BKMK_Security_Sites"></a> Security guidance for site administration

Use the following guidance to help you secure Configuration Manager sites and the hierarchy.  

### Run setup from a trusted source and secure communication

To help prevent someone from tampering with the source files, run Configuration Manager setup from a trusted source. If you store the files on the network, secure the network location.  

If you do run setup from a network location, to help prevent an attacker from tampering with the files as they're transmitted over the network, use IPsec or SMB signing between the source location of the setup files and the site server.  

If you use the Setup Downloader to download the files that are required by setup, make sure that you secure the location where these files are stored. Also secure the communication channel for this location when you run setup.  

### Extend the Active Directory schema and publish sites to the domain  

Schema extensions aren't required to run Configuration Manager, but they do create a more secure environment. Clients and site servers can retrieve information from a trusted source.  

If clients are in an untrusted domain, deploy the following site system roles in the clients' domains:  

- Management point  

- Distribution point  

> [!NOTE]  
> A trusted domain for Configuration Manager requires Kerberos authentication. If clients are in another forest that doesn't have a two-way forest trust with the site server's forest, these clients are considered to be in an untrusted domain. An external trust isn't sufficient for this purpose.  

### Use IPsec to secure communications

Although Configuration Manager does secure communication between the site server and the computer that runs SQL Server, Configuration Manager doesn't secure communications between site system roles and SQL Server. You can only configure some site systems with HTTPS for intrasite communication.  

If you don't use additional controls to secure these server-to-server channels, attackers can use various spoofing and man-in-the-middle attacks against site systems. Use SMB signing when you can't use IPsec.  

> [!Important]  
> Secure the communication channel between the site server and the package source server. This communication uses SMB. If you can't use IPsec to secure this communication, use SMB signing to make sure that the files aren't tampered with before clients download and run them.  

### Don't change the default security groups

Don't change the following security groups that Configuration Manager creates and manages for site system communication:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager automatically creates and manages these security groups. This behavior includes removing computer accounts when a site system role is removed.  

To make sure service continuity and least privileges, don't manually edit these groups.  

### Manage the trusted root key provisioning process

If clients can't query the global catalog for Configuration Manager information, they must rely on the trusted root key to authenticate valid management points. The trusted root key is stored in the client registry. It can be set by using group policy or manual configuration.  

If the client doesn't have a copy of the trusted root key before it contacts a management point for the first time, it trusts the first management point it communicates with. To reduce the risk of an attacker misdirecting clients to an unauthorized management point, you can pre-provision the clients with the trusted root key. For more information, see [Planning for the trusted root key](../security/plan-for-security.md#the-trusted-root-key).  

### Use non-default port numbers

Using non-default port numbers can provide additional security. They make it harder for attackers to explore the environment in preparation for an attack. If you decide to use non-default ports, plan for them before you install Configuration Manager. Use them consistently across all sites in the hierarchy. Client request ports and Wake On LAN are examples where you can use non-default port numbers.  

### Use role separation on site systems

Although you can install all the site system roles on a single computer, this practice is rarely used on production networks. It creates a single point of failure.  

### Reduce the attack profile

Isolating each site system role on a different server reduces the chance that an attack against vulnerabilities on one site system can be used against a different site system. Many roles require the installation of Internet Information Services (IIS) on the site system, and this need increases the attack surface. If you must combine roles to reduce hardware expenditure, combine IIS roles only with other roles that require IIS.  

> [!IMPORTANT]  
> The fallback status point role is an exception. Because this site system role accepts unauthenticated data from clients, don't assign the fallback status point role to any other Configuration Manager site system role.  

### Configure static IP addresses for site systems

Static IP addresses are easier to protect from name resolution attacks.  

Static IP addresses also make the configuration of IPsec easier. Using IPsec is a security best practice for securing communication between site systems in Configuration Manager.  

### Don't install other applications on site system servers

When you install other applications on site system servers, you increase the attack surface for Configuration Manager. You also risk incompatibility issues.  

### Require signing and enable encryption as a site option

Enable the signing and encryption options for the site. Ensure that all clients can support the SHA-256 hash algorithm, and then enable the option to **Require SHA-256**.  

### Restrict and monitor administrative users

Grant administrative access to Configuration Manager only to users that you trust. Then grant them minimum permissions by using the built-in security roles or by customizing the security roles. Administrative users who can create, modify, and deploy software and configurations can potentially control devices in the Configuration Manager hierarchy.  

Periodically audit administrative user assignments and their authorization level to verify required changes.  

For more information, see [Configure role-based administration](../../servers/deploy/configure/configure-role-based-administration.md).  

### Secure Configuration Manager backups

When you back up Configuration Manager, this information includes certificates and other sensitive data that could be used by an attacker for impersonation.  

Use SMB signing or IPsec when you transfer this data over the network, and secure the backup location.  

### Secure locations for exported objects

Whenever you export or import objects from the Configuration Manager console to a network location, secure the location and secure the network channel.

Restrict who can access the network folder.  

To prevent an attacker from tampering with the exported data, use SMB signing or IPsec between the network location and the site server. Also secure the communication between the computer that runs the Configuration Manager console and site server. Use IPsec to encrypt the data on the network to prevent information disclosure.  

### Manually remove certificates from failed servers

If a site system isn't uninstalled properly, or stops functioning and can't be restored, manually remove the Configuration Manager certificates for this server from other Configuration Manager servers.

To remove the peer trust that was originally established with the site system and site system roles, manually remove the Configuration Manager certificates for the failed server in the **Trusted People** certificate store on other site system servers. This action is important if you reuse the server without reformatting it.  

For more information, see [Cryptographic controls for server communication](../security/cryptographic-controls-technical-reference.md#server-communication).  

### Don't configure internet-based site systems to bridge the perimeter network

Don't configure site system servers to be multi-homed so that they connect to the perimeter network and the intranet. Although this configuration allows internet-based site systems to accept client connections from the internet and the intranet, it eliminates a security boundary between the perimeter network and the intranet.  

### Configure the site server to initiate connections to perimeter networks

If a site system is on an untrusted network, such as a perimeter network, configure the site server to initiate connections to the site system.

By default, site systems initiate connections to the site server to transfer data. This configuration can be a security risk when the connection initiation is from an untrusted network to the trusted network. When site systems accept connections from the internet, or reside in an untrusted forest, configure the site system option to **Require the site server to initiate connections to this site system**. After the installation of the site system and any roles, all connections are initiated by the site server from the trusted network.  

### Use SSL bridging and termination with authentication

If you use a web proxy server for internet-based client management, use SSL bridging to SSL, by using termination with authentication.

When you configure SSL termination at the proxy web server, packets from the internet are subject to inspection before they're forwarded to the internal network. The proxy web server authenticates the connection from the client, terminates it, and then opens a new authenticated connection to the internet-based site systems.  

When Configuration Manager client computers use a proxy web server to connect to internet-based site systems, the client identity (GUID) is securely contained within the packet payload. Then the management point doesn't consider the proxy web server to be the client.

If your proxy web server can't support the requirements for SSL bridging, SSL tunneling is also supported. This option is less secure. The SSL packets from the internet are forwarded to the site systems without termination. Then they can't be inspected for malicious content.  

> [!WARNING]  
> Mobile devices that are enrolled by Configuration Manager can't use SSL bridging. They must use SSL tunneling only.  

### Configurations to use if you configure the site to wake up computers to install software

- If you use traditional wake-up packets, use unicast rather than subnet-directed broadcasts.  

- If you must use subnet-directed broadcasts, configure routers to allow IP-directed broadcasts only from the site server and only on a non-default port number.  

For more information about the different Wake On LAN technologies, see [Planning how to wake up clients](../../clients/deploy/plan/plan-wake-up-clients.md).

### If you use email notification, configure authenticated access to the SMTP mail server

Whenever possible, use a mail server that supports authenticated access. Use the computer account of the site server for authentication. If you must specify a user account for authentication, use an account that has the least privileges. 

### Enforce LDAP channel binding and LDAP signing

The security of Active Directory domain controllers can be improved by configuring the server to reject Simple Authentication and Security Layer (SASL) LDAP binds that do not request signing or to reject LDAP simple binds that are performed on a clear text connection. Starting in version 1910, Configuration Manager supports enforcing LDAP channel binding and LDAP signing. For more information, see [2020 LDAP channel binding and LDAP signing requirements for Windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="BKMK_Security_SiteServer"></a> Security guidance for the site server

Use the following guidance to help you secure the Configuration Manager site server.  

> [!WARNING]  
> Network access account - Don't grant interactive sign-in rights to this account on SQL Servers.
Don't grant this account the right to join computers to the domain. If you must join computers to the domain during a task sequence, use the Task sequence domain join account..

### Install Configuration Manager on a member server instead of a domain controller

The Configuration Manager site server and site systems don't require installation on a domain controller. Domain controllers don't have a local Security Accounts Management (SAM) database other than the domain database. When you install Configuration Manager on a member server, you can maintain Configuration Manager accounts in the local SAM database rather than in the domain database.  

This practice also lowers the attack surface on your domain controllers.  

### Install secondary sites without copying the files over the network

When you run setup and create a secondary site, don't select the option to copy the files from the parent site to the secondary site. Also don't use a network source location. When you copy files over the network, a skilled attacker could hijack the secondary site installation package and tamper with the files before they're installed. Timing this attack would be difficult. This attack can be mitigated by using IPsec or SMB when you transfer the files.  

Instead of copying the files over the network, on the secondary site server, copy the source files from media folder to a local folder. Then, when you run setup to create a secondary site, on the **Installation Source Files** page, select **Use the source files at the following location on the secondary site computer (most secure)**, and specify this folder.  

For more information, see [Install a secondary site](../../servers/deploy/install/setup-wizard-secondary.md).

### Site role installation inherits permissions from drive root

<!-- SCCMDocs#1380 -->
Make sure to properly configure the system drive permissions before you install the first site system role to any server. For example, `C:\SMS_CCM` inherits permissions from `C:\`. If the root of the drive isn't properly secured, then low rights users may be able to access or modify content in the Configuration Manager folder.


## <a name="BKMK_Security_SQLServer"></a> Security guidance for SQL Server

Configuration Manager uses SQL Server as the back-end database. If the database is compromised, attackers could bypass Configuration Manager. If they access SQL Server directly, they can launch attacks through Configuration Manager. Consider attacks against SQL Server to be high risk and mitigate appropriately.  

Use the following security guidance to help you secure SQL Server for Configuration Manager.  

### Don't use the Configuration Manager site database server to run other SQL Server applications

When you increase the access to the Configuration Manager site database server, this action increases the risk to your Configuration Manager data. If the Configuration Manager site database is compromised, other applications on the same SQL Server computer are then also put at risk.  

### Configure SQL Server to use Windows authentication

Although Configuration Manager accesses the site database by using a Windows account and Windows authentication, it's still possible to configure SQL Server to use SQL Server mixed mode. SQL Server mixed mode allows additional SQL Server sign-ins to access the database. This configuration isn't required and increases the attack surface.  

### Update SQL Server Express at secondary sites

When you install a primary site, Configuration Manager downloads SQL Server Express from the Microsoft Download Center. It then copies the files to the primary site server. When you install a secondary site and select the option that installs SQL Server Express, Configuration Manager installs the previously downloaded version. It doesn't check whether new versions are available. To make sure that the secondary site has the latest versions, do one of the following tasks:  

- After you install the secondary site, run Windows Update on the secondary site server.  

- Before you install the secondary site, manually install SQL Server Express on the secondary site server. Make sure that you install the latest version and any software updates. Then install the secondary site, and select the option to use an existing SQL Server instance.  

Periodically run Windows Update for all installed versions of SQL Server. This practice makes sure that they have the latest software updates.  

### Follow general guidance for SQL Server

Identify and follow the general guidance for your version of SQL Server. However, take into consideration the following requirements for Configuration Manager:  

- The computer account of the site server must be a member of the Administrators group on the computer that runs SQL Server. If you follow the SQL Server recommendation of "provision administrator principals explicitly", the account that you use to run setup on the site server must be a member of the SQL Server Users group.  

- If you install SQL Server by using a domain user account, make sure that the site server computer account is configured for a Service Principal Name (SPN) that's published to Active Directory Domain Services. Without the SPN, Kerberos authentication fails and Configuration Manager setup fails.  


## <a name="BKMK_Security_IIS"></a> Security guidance for site systems that run IIS

Several site system roles in Configuration Manager require IIS. The process of securing IIS enables Configuration Manager to operate correctly and reduces the risk of security attacks. When practical, minimize the number of servers that require IIS. For example, run only the number of management points that you require to support your client base, taking into consideration high availability and network isolation for internet-based client management.  

Use the following guidance to help you secure the site systems that run IIS.  

### Disable IIS functions that you don't require

Install only the minimum IIS features for the site system role that you install. For more information, see [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md).  

### Configure the site system roles to require HTTPS

When clients connect to a site system by using HTTP rather than by using HTTPS, they use Windows authentication. This behavior might fall back to using NTLM authentication rather than Kerberos authentication. When NTLM authentication is used, clients might connect to a rogue server.  

The exception to this guidance might be distribution points. Package access accounts don't work when the distribution point is configured for HTTPS. Package access accounts provide authorization to the content, so that you can restrict which users can access the content. For more information, see [Security guidance for content management](security-and-privacy-for-content-management.md#security-guidance).

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

### Configure a certificate trust list (CTL) in IIS for site system roles

Site system roles:  

- A distribution point that you configure for HTTPS  

- A management point that you configure for HTTPS and enable to support mobile devices

A CTL is a defined list of trusted root certification authorities (CAs). When you use a CTL with group policy and a public key infrastructure (PKI) deployment, a CTL enables you to supplement the existing trusted root CAs that are configured on your network. For example, CAs that are automatically installed with Microsoft Windows or added through Windows enterprise root CAs. When a CTL is configured in IIS, it defines a subset of those trusted root CAs.  

This subset provides you with more control over security. The CTL restricts the client certificates that are accepted to only those certificates that are issued from the list of CAs in the CTL. For example, Windows comes with a number of well-known, third-party CA certificates.

By default, the computer that runs IIS trusts certificates that chain to these well-known CAs. When you don't configure IIS with a CTL for the listed site system roles, the site accepts as a valid client any device that has a certificate issued from these CAs. If you configure IIS with a CTL that didn't include these CAs, the site refuses client connections, if the certificate chains to these CAs. For Configuration Manager clients to be accepted for the listed site system roles, you must configure IIS with a CTL that specifies the CAs that are used by Configuration Manager clients.  

> [!NOTE]  
> Only the listed site system roles require you to configure a CTL in IIS. The certificate issuers list that Configuration Manager uses for management points provides the same functionality for client computers when they connect to HTTPS management points.  

For more information about how to configure a list of trusted CAs in IIS, see the IIS documentation.  

### Don't put the site server on a computer with IIS

Role separation helps to reduce the attack profile and improve recoverability. The computer account of the site server typically has administrative privileges on all site system roles. It may also have these privileges on Configuration Manager clients, if you use client push installation.  

### Use dedicated IIS servers for Configuration Manager

Although you can host multiple web-based applications on the IIS servers that are also used by Configuration Manager, this practice can significantly increase your attack surface. A poorly configured application could allow an attacker to gain control of a Configuration Manager site system. This breach could allow an attacker to gain control of the hierarchy.  

If you must run other web-based applications on Configuration Manager site systems, create a custom web site for Configuration Manager site systems.  

### Use a custom website

For site systems that run IIS, configure Configuration Manager to use a custom website instead of the default website. If you have to run other web applications on the site system, you must use a custom website. This setting is a site-wide setting rather than a setting for a specific site system.  

### When you use custom websites, remove the default virtual directories

When you change from using the default website to using a custom website, Configuration Manager doesn't remove the old virtual directories. Remove the virtual directories that Configuration Manager originally created under the default website.  

For example, remove the following virtual directories for a distribution point:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### Follow IIS Server security guidance

Identify and follow the general guidance for your version of IIS Server. Take into consideration any requirements that Configuration Manager has for specific site system roles. For more information, see [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md).  

### Configure IIS custom headers

Configure the following custom headers to disable MIME sniffing:<!-- 8540255 -->

`x-content-type-options: nosniff`

For more information, see [Custom Headers](/iis/configuration/system.webserver/httpprotocol/customheaders).

If other services use the same IIS instance, make sure these custom headers are compatible.

## <a name="BKMK_Security_ManagementPoint"></a> Security guidance for the management point

Management points are the primary interface between devices and Configuration Manager. Consider attacks against the management point and the server that it runs on to be high risk, and mitigate appropriately. Apply all appropriate security guidance and monitor for unusual activity.  

Use the following guidance to help secure a management point in Configuration Manager.  

### Assign the client on a management point to the same site

Avoid the scenario where you assign the Configuration Manager client that's on a management point to a site other than the management point's site.  

If you migrate from an earlier version to Configuration Manager current branch, migrate the client on the management point to the new site as soon as possible.  


## <a name="BKMK_Security_FSP"></a> Security guidance for the fallback status point

If you install a fallback status point in Configuration Manager, use the following security guidance:

For more information about the security considerations when you install a fallback status point, see [Determine whether you require a fallback status point](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### Don't run any other roles on the same site system

The fallback status point is designed to accept unauthenticated communication from any computer. If you run this site system role with other roles or a domain controller, the risk to that server greatly increases.  

### Install the fallback status point before you install clients with PKI certificates

If Configuration Manager site systems don't accept HTTP client communication, you might not know that clients are unmanaged because of PKI-related certificate issues. If you assign clients to a fallback status point, they report these certificate issues through the fallback status point.  

For security reasons, you can't assign a fallback status point to clients after they're installed. You can only assign this role during client installation.  

### Avoid using the fallback status point in the perimeter network

By design, the fallback status point accepts data from any client. Although a fallback status point in the perimeter network could help you to troubleshoot internet-based clients, balance the troubleshooting benefits with the risk of a site system that accepts unauthenticated data in a publicly accessible network.  

If you do install the fallback status point in the perimeter network or any untrusted network, configure the site server to initiate data transfers. Don't use the default setting that allows the fallback status point to initiate a connection to the site server.  


## <a name="BKMK_SecurityIssues_Clients"></a> Security issues for site administration

Review the following security issues for Configuration Manager:  

- Configuration Manager has no defense against an authorized administrative user who uses Configuration Manager to attack the network. Unauthorized administrative users are a high security risk. They could launch many attacks, which include the following strategies:  

    - Use software deployment to automatically install and run malicious software on every Configuration Manager client computer in the organization.  

    - Remotely control a Configuration Manager client without client permission.  

    - Configure rapid polling intervals and extreme amounts of inventory. This action creates denial of service attacks against the clients and servers.  

    - Use one site in the hierarchy to write data to another site's Active Directory data.  

    The site hierarchy is the security boundary. Consider sites to be management boundaries only.  

    Audit all administrative user activity and routinely review the audit logs. Require all Configuration Manager administrative users to undergo a background check before they're hired. Require periodic rechecks as a condition of employment.  

- If the enrollment point is compromised, an attacker could obtain certificates for authentication. They could steal the credentials of users who enroll their mobile devices.  

    The enrollment point communicates with a CA. It can create, modify, and delete Active Directory objects. Never install the enrollment point in the perimeter network. Always monitor for unusual activity.  

- If you allow user policies for internet-based client management, you increase your attack profile.  

    In addition to using PKI certificates for client-to-server connections, these configurations require Windows authentication. They might fall back to using NTLM authentication rather than Kerberos. NTLM authentication is vulnerable to impersonation and replay attacks. To successfully authenticate a user on the internet, you need to allow a connection from the internet-based site system to a domain controller.  

- The **Admin$** share is required on site system servers.  

    The Configuration Manager site server uses the Admin$ share to connect to and do service operations on site systems. Don't disable or remove this share.  

- Configuration Manager uses name resolution services to connect to other computers. These services are hard to secure against the following security attacks:
    - Spoofing
    - Tampering
    - Repudiation
    - Information disclosure
    - Denial of service
    - Elevation of privilege

    Identify and follow any security guidance for the version of DNS that you use for name resolution.  

## <a name="BKMK_Privacy_Cliients"></a> Privacy information for discovery

Discovery creates records for network resources and stores them in the Configuration Manager database. Discovery data records contain computer information such as IP addresses, OS versions, and computer names. You can also configure Active Directory discovery methods to return any information that your organization stores in Active Directory Domain Services.  

The only discovery method that Configuration Manager enables by default is Heartbeat Discovery. This method only discovers computers that already have the Configuration Manager client software installed.  

Discovery information isn't directly sent to Microsoft. It's stored in the Configuration Manager database. Configuration Manager retains information in the database until it deletes the data. This process happens every 90 days by the site maintenance task **Delete Aged Discovery Data**.  
