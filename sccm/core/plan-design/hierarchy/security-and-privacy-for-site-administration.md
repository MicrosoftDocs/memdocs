---
title: "Site administration security and privacy"
titleSuffix: "Configuration Manager"
description: "Optimize security and privacy for site administration in System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: 8
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Security and privacy for site administration in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic contains security and privacy information for System Center Configuration Manager sites and the hierarchy.

##  <a name="BKMK_Security_Sites"></a> Security best practices for site administration  
 Use the following security best practices to help you secure System Center Configuration Manager sites and the hierarchy.  

 **Run setup only from a trusted source and secure the communication channel between the setup media and the site server.**  

 To help prevent someone from tampering with the source files, run setup from a trusted source. If you store the files on the network, secure the network location.  

 If you do run setup from a network location, to help prevent an attacker from tampering with the files as they are transmitted over the network, use IPsec or Server Message Block (SMB) signing between the source location of the setup files and the site server.  

 In addition, if you use the Setup Downloader to download the files that are required by setup, make sure that you also secure the location where these files are stored and secure the communication channel for this location when you run setup.  

 **Extend the Active Directory schema for System Center Configuration Manager and publish sites to Active Directory Domain Services.**  

 Schema extensions are not required to run System Center Configuration Manager, but they do create a more secure environment because Configuration Manager clients and site servers can retrieve information from a trusted source.  

 If clients are in an untrusted domain, deploy the following site system roles in the clients' domains:  

-   Management point  

-   Distribution point  

-   Application Catalog website point  

> [!NOTE]  
>  A trusted domain for Configuration Manager requires Kerberos authentication. This means that if clients are in another forest that does not have a two-way forest trust with the site server's forest, these clients are considered to be in untrusted domain. An external trust is not sufficient for this purpose.  

 **Use IPsec to secure communications between site system servers and sites.**  

 Although Configuration Manager does secure communication between the site server and the computer that runs SQL Server, Configuration Manager does not secure communications between site system roles and SQL Server. Only some site systems (the enrollment point and the Application Catalog web service point) can be configured for HTTPS for intrasite communication.  

 If you do not use additional controls to secure these server-to-server channels, attackers can use various spoofing and man-in-the-middle attacks against site systems. Use SMB signing when you cannot use IPsec.  

> [!NOTE]  
>  It is particularly important to secure the communication channel between the site server and the package source server. This communication uses SMB. If you cannot use IPsec to secure this communication, use SMB signing to ensure that the files are not tampered with before clients download and run them.  

 **Do not change the security groups that Configuration Manager creates and manages for site system communication.**  

 Security  groups:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager automatically creates and manages these security groups. This includes removing computer accounts when a site system role is removed.  

To ensure service continuity and least privileges, do not manually edit these groups.  

**If clients cannot query the Global Catalog server for Configuration Manager information, manage the trusted root key provisioning process.**  

If clients cannot query the Global Catalog for Configuration Manager information, they must rely on the trusted root key to authenticate valid management points. The trusted root key is stored in the client registry and can be set by using Group Policy or manual configuration.  

If the client does not have a copy of the trusted root key before it contacts a management point for the first time, it trusts the first management point it communicates with. To reduce the risk of an attacker misdirecting clients to an unauthorized management point, you can pre-provision the clients with the trusted root key. For more information, see [Planning for the trusted root key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Use non-default port numbers.**  

Using non-default port numbers can provide additional security because they make it harder for attackers to explore the environment in preparation for an attack. If you decide to use non-default ports, plan for them before you install Configuration Manager, and use them consistently across all sites in the hierarchy. Client request ports and Wake On LAN are examples where you can use non-default port numbers.  

**Use role separation on site systems.**  

Although you can install all the site system roles on a single computer, this practice is rarely used on production networks because it creates a single point of failure.  

**Reduce the attack profile.**  

Isolating each site system role on a different server reduces the chance that an attack against vulnerabilities on one site system can be used against a different site system. Many site system roles require the installation of Internet Information Services (IIS) on the site system, and this increases the attack surface. If you must combine site system roles to reduce hardware expenditure, combine IIS site system roles only with other site system roles that require IIS.  

> [!IMPORTANT]  
>  The fallback status point role is an exception. Because this site system role accepts unauthenticated data from clients, we recommend that you don't ever assign the fallback status point role to any other Configuration Manager site system role.  


**Follow security best practices for Windows Server and run the Security Configuration Wizard on all site systems.**  

The Security Configuration Wizard (SCW) helps you to create a security policy that you can apply to any server on your network. After you install the System Center Configuration Manager template, SCW recognizes Configuration Manager site system roles, services, ports, and applications. It then permits the communication that is required for Configuration Manager and blocks communication that is not required.  

The Security Configuration Wizard is included with the toolkit for System Center 2012 Configuration Manager, which you can download from the Microsoft Download Center: [System Center 2012 — Configuration Manager Component Add-ons and Extensions](http://go.microsoft.com/fwlink/p/?LinkId=251931).  

**Configure static IP addresses for site systems.**  

Static IP addresses are easier to protect from name resolution attacks.  

Static IP addresses also make the configuration of IPsec easier. Using IPsec is a security best practice for securing communication between site systems in Configuration Manager.  

**Do not install other applications on site system servers.**  

When you install other applications on site system servers, you increase the attack surface for Configuration Manager and risk incompatibility issues.  

**Require signing and enable encryption as a site option.**  

Enable the signing and encryption options for the site. Ensure that all clients can support the SHA-256 hash algorithm, and then enable the option **Require SHA-256**.  

**Restrict and monitor Configuration Manager administrative users and use role-based administration to grant these users the minimum permissions that they require.**  

Grant administrative access to Configuration Manager only to users that you trust and then grant them minimum permissions by using the built-in security roles or by customizing the security roles. Administrative users who can create, modify, and deploy applications, task sequence, software updates, configuration items, and configuration baselines, can potentially control devices in the Configuration Manager hierarchy.  

Periodically audit administrative user assignments and their authorization level to verify required changes.  

For more information about configuring role-based administration, see [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

**Secure Configuration Manager backups and secure the communication channel when you back up and restore.**  

When you back up Configuration Manager, this information includes certificates and other sensitive data that could be used by an attacker for impersonation.  

Use SMB signing or IPsec when you transfer this data over the network, and secure the backup location.  

**Whenever you export or import objects from the Configuration Manager console to a network location, secure the location and secure the network channel.**  

Restrict who can access the network folder.  

Use SMB signing or IPsec between the network location and the site server, and between the computer that runs the Configuration Manager console and site server, to prevent an attacker from tampering with the exported data. Use IPsec to encrypt the data on the network to prevent information disclosure.  

**If a site system isn't uninstalled properly or stops functioning and cannot be restored, manually remove the Configuration Manager certificates for this server from other Configuration Manager servers.**  

To remove the PeerTrust that was originally established with the site system and site system roles, manually remove the Configuration Manager certificates for the failed server in the **Trusted People** certificate store on other site system servers. This is particularly important if you repurpose the server without reformatting it.  

For more information about these certificates, see the section **Cryptographic controls for server communication** in [Cryptographic controls technical reference for System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**Do not configure Internet-based site systems to bridge the perimeter network and the intranet.**  

Do not configure site system servers to be multi-homed so that they connect to the perimeter network and the intranet. Although this configuration allows Internet-based site systems to accept client connections from the Internet and the intranet, it eliminates a security boundary between the perimeter network and the intranet.  

**If the site system server is on an untrusted network (such as a perimeter network), configure the site server to initiate connections to the site system.**  

By default, site systems initiate connections to the site server to transfer data, which can be a security risk when the connection initiation is from an untrusted network to the trusted network. When site systems accept connections from the Internet or reside in an untrusted forest, configure the site system option **Require the site server to initiate connections to this site system** so that after the installation of the site system and any site system roles, all connections are initiated from the trusted network.  

**If you use a web proxy server for Internet-based client management, use SSL bridging to SSL, by using termination with authentication.**  

 When you configure SSL termination at the proxy web server, packets from the Internet are subject to inspection before they are forwarded to the internal network. The proxy web server authenticates the connection from the client, terminates it, and then opens a new authenticated connection to the Internet-based site systems.  

 When Configuration Manager client computers use a proxy web server to connect to Internet-based site systems, the client identity (client GUID) is securely contained within the packet payload so that the management point does not consider the proxy web server to be the client. If your proxy web server cannot support the requirements for SSL bridging, SSL tunneling is also supported. This is a less secure option because the SSL packets from the Internet are forwarded to the site systems without termination, so they cannot be inspected for malicious content.  

 If your proxy web server cannot support the requirements for SSL bridging, you can use SSL tunneling. However, this is a less secure option because the SSL packets from the Internet are forwarded to the site systems without termination, so they cannot be inspected for malicious content.  

> [!WARNING]  
>  Mobile devices that are enrolled by Configuration Manager cannot use SSL bridging and must use SSL tunneling only.  

**Configurations to use if you configure the site to wake up computers to install software.**  

-   If you use traditional wake-up packets, use unicast rather than subnet-directed broadcasts.  

-   If you must use subnet-directed broadcasts, configure routers to allow IP-directed broadcasts only from the site server and only on a non-default port number.  

For more information about the different Wake On LAN technologies, see [Planning how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

**If you use email notification, configure authenticated access to the SMTP mail server.**  

Whenever possible, use a mail server that supports authenticated access, and use the computer account of the site server for authentication. If you must specify a user account for authentication, use an account that has the least privileges.  

##  <a name="BKMK_Security_SiteServer"></a> Security best practices for the site server  
 Use the following security best practices to help you secure the Configuration Manager site server.  

 **Install Configuration Manager on a member server instead of a domain controller.**  

 The Configuration Manager site server and site systems do not require installation on a domain controller. Domain controllers do not have a local Security Accounts Management (SAM) database other than the domain database. When you install Configuration Manager on a member server, you can maintain Configuration Manager accounts in the local SAM database rather than in the domain database.  

 This practice also lowers the attack surface on your domain controllers.  

 **Install secondary sites by avoiding copying the files to the secondary site server over the network.**  

 When you run setup and create a secondary site, do not select the option to copy the files from the parent site to the secondary site, and don't use a network source location. When you copy files over the network, a skilled attacker could hijack the secondary site installation package and tamper with the files before they are installed, although timing this attack would be difficult. This attack can be mitigated by using IPsec or SMB when you transfer the files.  

 Instead of copying the files over the network, on the secondary site server, copy the source files from media folder to a local folder. Then, when you run setup to create a secondary site, on the **Installation Source Files** page, select **Use the source files at the following location on the secondary site computer (most secure)**, and specify this folder.  

 For more information, see [Install a secondary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) in the [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) topic.  

##  <a name="BKMK_Security_SQLServer"></a> Security best practices for SQL Server  
 Configuration Manager uses SQL Server as the back-end database. If the database is compromised, attackers could bypass Configuration Manager and access SQL Server directly to launch attacks through Configuration Manager. Consider attacks against SQL Server to be very high risk and mitigate appropriately.  

 Use the following security best practices to help you secure SQL Server for Configuration Manager.  

 **Do not use the Configuration Manager site database server to run other SQL Server applications.**  

 When you increase the access to the Configuration Manager site database server, this increases the risk to your Configuration Manager data. If the Configuration Manager site database is compromised, other applications on the same SQL Server computer are then also put at risk.  

 **Configure SQL Server to use Windows authentication.**  

 Although Configuration Manager accesses the site database by using a Windows account and Windows authentication, it is still possible to configure SQL Server to use SQL Server mixed mode. SQL Server mixed mode allows additional SQL sign-ins to access the database, which is not required and increases the attack surface.  

 **Take additional steps to ensure that secondary sites that use SQL Server Express have the latest software updates.**  

 When you install a primary site, Configuration Manager downloads SQL Server Express from the Microsoft Download Center and copies the files to the primary site server. When you install a secondary site and select the option that installs SQL Server Express, Configuration Manager installs the previously downloaded version and does not check whether new versions are available. To ensure that the secondary site has the latest versions, do one of the following tasks:  

-   After the secondary site has been installed, run Windows Update on the secondary site server.  

-   Before you install the secondary site, manually install SQL Server Express on the computer that will run the secondary site server and ensure that you install the latest version and any software updates. Then install the secondary site, and select the option to use an existing SQL Server instance.  

Periodically run Windows Update for these sites and all installed versions of SQL Server to make sure that they have the latest software updates.  

**Follow best practices for SQL Server.**  

Identify and follow the best practices for your version of SQL Server. However, take into consideration the following requirements for Configuration Manager:  

-   The computer account of the site server must be a member of the Administrators group on the computer that runs SQL Server. If you follow the SQL Server recommendation of "provision administrator principals explicitly", the account that you use to run setup on the site server must be a member of the SQL Users group.  

-   If you install SQL Server by using a domain user account, make sure that the site server computer account is configured for a Service Principal Name (SPN) that is published to Active Directory Domain Services. Without the SPN, Kerberos authentication fails and Configuration Manager setup fails.  

##  <a name="BKMK_Security_IIS"></a> Security best practices for site systems that run IIS  
Several site system roles in Configuration Manager require IIS. The process of securing IIS enables Configuration Manager to operate correctly and reduces the risk of security attacks. When practical, minimize the number of servers that require IIS. For example, run only the number of management points that you require to support your client base, taking into consideration high availability and network isolation for Internet-based client management.  

 Use the following security best practices to help you secure the site systems that run IIS.  

 **Disable IIS functions that you don't require.**  

 Install only the minimum IIS features for the site system role that you install. For more information, see [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Configure the site system roles to require HTTPS.**  

 When clients connect to a site system by using HTTP rather than by using HTTPS, they use Windows authentication, which might fall back to using NTLM authentication rather than Kerberos authentication. When NTLM authentication is used, clients might connect to a rogue server.  

 The exception to this security best practice might be distribution points because package access accounts do not work when the distribution point is configured for HTTPS. Package access accounts provide authorization to the content, so that you can restrict which users can access the content. For more information, see [Security best practices for content management](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Configure a certificate trust list (CTL) in IIS for site system roles.**  

Site system roles:  

-   A distribution point that is configured for HTTPS  

-   A management point that is configured for HTTPS and enabled to support mobile devices

A certificate trust list (CTL) is a defined list of trusted root certification authorities. When you use a CTL with Group Policy and a public key infrastructure (PKI) deployment, a CTL enables you to supplement the existing trusted root certification authorities that are configured on your network, such as those that are automatically installed with Microsoft Windows or added through Windows enterprise root certification authorities. However, when a CTL is configured in IIS, it defines a subset of those trusted root certification authorities.  

This subset provides you with more control over security because the CTL restricts the client certificates that are accepted to only those that are issued from the list of certification authorities in the CTL. For example, Windows comes with a number of well-known, third-party certification authority certificates, such as VeriSign and Thawte.

By default, the computer that runs IIS trusts certificates that chain to these well-known certification authorities. When you do not configure IIS with a CTL for the listed site system roles, any device that has a client certificate issued from these certification authorities is accepted as a valid Configuration Manager client. If you configure IIS with a CTL that did not include these certification authorities, client connections are refused if the certificate chained to these certification authorities. However, for Configuration Manager clients to be accepted for the listed site system roles, you must configure IIS with a CTL that specifies the certification authorities that are used by Configuration Manager clients.  

> [!NOTE]  
>  Only the listed site system roles require you to configure a CTL in IIS. The certificate issuers list that Configuration Manager uses for management points provides the same functionality for client computers when they connect to HTTPS management points.  

For more information about how to configure a list of trusted certification authorities in IIS, refer to your IIS documentation.  

**Do not put the site server on a computer with IIS.**  

Role separation helps to reduce the attack profile and improve recoverability. In addition, the computer account of the site server typically has administrative privileges on all site system roles (and possibly on Configuration Manager clients, if you use client push installation).  

**Use dedicated IIS servers for Configuration Manager.**  

Although you can host multiple web-based applications on the IIS servers that are also used by Configuration Manager, this practice can significantly increase your attack surface. A poorly configured application could allow an attacker to gain control of a Configuration Manager site system, which could allow an attacker to gain control of the hierarchy.  

If you must run other web-based applications on Configuration Manager site systems, create a custom web site for Configuration Manager site systems.  

**Use a custom website.**  

For site systems that run IIS, you can configure Configuration Manager to use a custom website instead of the default website for IIS. If you have to run other web applications on the site system, you must use a custom website. This setting is a site-wide setting rather than a setting for a specific site system.  

In addition to providing additional security, you must use a custom website if you run other web applications on the site system.  

**If you switch from the default website to a custom website after any distribution point roles are installed, remove the default virtual directories.**  

When you change from using the default website to using a custom website, Configuration Manager does not remove the old virtual directories. Remove the virtual directories that Configuration Manager originally created under the default website.  

For example, the virtual directories to remove for a distribution point are the following:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Follow best practices for IIS Server.**  

Identify and follow the best practices for your version of IIS Server. However, take into consideration any requirements that Configuration Manager has for specific site system roles. For more information, see [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

##  <a name="BKMK_Security_ManagementPoint"></a> Security best practices for the management point  
 Management points are the primary interface between devices and Configuration Manager. Consider attacks against the management point and the server that it runs on to be very high risk, and mitigate appropriately. Apply all appropriate security best practices and monitor for unusual activity.  

 Use the following security best practices to help secure a management point in Configuration Manager.  

**When you install a Configuration Manager client on the management point, assign it to that management point's site.**  

 Avoid the scenario where a Configuration Manager client that is on a management point site system is assigned to a site other than the management point's site.  

 If you migrate from an earlier version  to System Center Configuration Manager, migrate the client software on the management point to System Center Configuration Manager as soon as possible.  

##  <a name="BKMK_Security_FSP"></a> Security best practices for the fallback status point  
 Use the following security best practices if you install a fallback status point in Configuration Manager.  

 For more information about the security considerations when you install a fallback status point, see [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#determine-if-you-need-a-fallback-status-point).  


**Do not run other site system roles on the site system, and do not install the status fallback point on a domain controller.**  

 Because the fallback status point is designed to accept unauthenticated communication from any computer, running this site system role with other site system roles or on a domain controller greatly increases the risk to that server.  

**When you use PKI certificates for client communication in Configuration Manager, install the fallback status point before you install the clients.**  

 If Configuration Manager site systems do not accept HTTP client communication, you might not know that clients are unmanaged because of PKI-related certificate issues. However, if clients are assigned to a fallback status point, these certificate issues are reported by the fallback status point.  

 For security reasons, you cannot assign a fallback status point to clients after they are installed. Instead, you can assign this role only during client installation.  

**Avoid using the fallback status point in the perimeter network.**  

 By design, the fallback status point accepts data from any client. Although a fallback status point in the perimeter network could help you to troubleshoot Internet-based clients, you must balance the troubleshooting benefits with the risk of a site system that accepts unauthenticated data in a publicly accessible network.  

 If you do install the fallback status point in the perimeter network or any untrusted network, configure the site server to initiate data transfers rather than using the default setting that allows the fallback status point to initiate a connection to the site server.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Security issues for site administration  
 Review the following security issues for Configuration Manager:  

-   Configuration Manager has no defense against an authorized administrative user who uses Configuration Manager to attack the network. Unauthorized administrative users are a high security risk and could launch numerous attacks, which include the following strategies:  

    -   Use software deployment to automatically install and run malicious software on every Configuration Manager client computer in the enterprise.  

    -   Use remote control to take remote control of a Configuration Manager client without client permission.  

    -   Configure rapid polling intervals and extreme amounts of inventory to create denial of service attacks against the clients and servers.  

    -   Use one site in the hierarchy to write data to another site's Active Directory data.  

    The site hierarchy is the security boundary. Consider sites to be management boundaries only.  

    Audit all administrative user activity and routinely review the audit logs. Require all Configuration Manager administrative users to undergo a background check before they are hired and require periodic rechecks as a condition of employment.  

-   If the enrollment point is compromised, an attacker could obtain certificates for authentication and steal the credentials of users who enroll their mobile devices.  

    The enrollment point communicates with a certification authority and can create, modify, and delete Active Directory objects. Never install the enrollment point in the perimeter network, and always monitor for unusual activity.  

-   If you allow user policies for Internet-based client management or configure the Application Catalog website point for users when they are on the Internet, you increase your attack profile.  

    In addition to using PKI certificates for client-to-server connections, these configurations require Windows authentication, which might fall back to using NTLM authentication rather than Kerberos. NTLM authentication is vulnerable to impersonation and replay attacks. To successfully authenticate a user on the Internet, you must allow a connection from the Internet-based site system server to a domain controller.  

-   The Admin$ share is required on site system servers.  

    The Configuration Manager site server uses the Admin$ share to connect to and perform service operations on site systems. Do not disable or remove the Admin$ share.  

-   Configuration Manager uses name resolution services to connect to other computers, and these services are hard to secure against security attacks such as spoofing, tampering, repudiation, information disclosure, denial of service, and elevation of privilege.  

    Identify and follow any security best practices for the version of DNS and WINS that you use for name resolution.  

##  <a name="BKMK_Privacy_Cliients"></a> Privacy information for Discovery  
 Discovery creates records for network resources and stores them in the System Center Configuration Manager database. Discovery data records contain computer information such as IP addresses, operating systems, and computer names. Active Directory discovery methods can also be configured to discover any information that is stored in Active Directory Domain Services.  

 The only discovery method that is enabled by default is Heartbeat Discovery, but that method only discovers computers that are already have the System Center Configuration Manager client software installed.  

 Discovery information is not sent to Microsoft. Instead, it's stored in the Configuration Manager database. Information is retained in the database until it is deleted every 90 days by the site maintenance task **Delete Aged Discovery Data**.  

 Before you configure additional discovery methods or extend Active Directory discovery, consider your privacy requirements.  
