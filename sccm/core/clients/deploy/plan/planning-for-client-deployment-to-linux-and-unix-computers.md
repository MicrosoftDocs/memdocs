---
title: "Planning client deployment to Linux and UNIX computers | Microsoft Docs"
description: "Plan for client deployment to Linux and UNIX computers in System Center Configuration Manager."
ms.custom: na
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
caps.latest.revision: 9
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# Planning for client deployment to Linux and UNIX computers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can install the System Center Configuration Manager client on computers that run Linux or UNIX. This client is designed for servers that operate as a workgroup computer, and the client does not support interaction with logged-on users. After you install the client software and the client establishes communication with the Configuration Manager site, you manage the client by using the Configuration Manager console and reports.  

> [!NOTE]  
>  The Configuration Manager client for Linux and UNIX computers does not support the following management capabilities:  
>   
>  -   Client push installation  
> -   Operating system deployment  
> -   Application deployment; instead, deploy software by using packages and programs.  
> -   Software inventory  
> -   Software updates  
> -   Compliance settings  
> -   Remote control  
> -   Power management  
> -   Client status client check and remediation  
> -   Internet-based client management  

 For information about the supported Linux and UNIX distributions and the hardware required to support the client for Linux and UNIX, see [Recommended hardware for System Center Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Use the information in this article to help you plan to deploy the Configuration Manager client for Linux and UNIX.  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Prerequisites for Client Deployment to Linux and UNIX Servers  
 Use the following information to determine the prerequisites you must have in place to successfully install the client for Linux and UNIX.  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> Dependencies External to Configuration Manager:  
 The following tables describe the required UNIX and Linux operating systems and package dependencies.  

 **Red Hat Enterprise Linux Server release 5.1 (Tikanga)**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|glibc|C Standard Libraries|2.5-12|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8b-8.3.el5|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server release 6**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|glibc|C Standard Libraries|2.12-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  


 **Solaris 10 SPARC**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|Required operating system patch|PAM memory leak|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|SUNopenssl-librararies (Usr)<br /><br /> Sun provides the OpenSSL libraries for Solaris 10 SPARC. They are bundled with the operating system.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|Required operating system patch|PAM memory leak|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Shared Libs) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris Libraries (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|SUNWopenssl-libraries; OpenSSL Libraries (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Required package|Description|Minimum version|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|C Standard shared library|2.4-31.30|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8a-18.15|  
|PAM|Pluggable Authentication Modules|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|C Standard shared library|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

 **Universal Linux (Debian package) Debian, Ubuntu Server**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|libc6|C Standard shared library|2.3.6|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

 **Universal Linux (RPM package) CentOS, Oracle Linux**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|glibc|C Standard shared library|2.5-12|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|OS version|Version of operating system|AIX 6.1, any Technology Level and Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|OS version|Version of operating system|AIX 7.1, any Technology Level and Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol||  


 **HP-UX 11i v3 IA64**  

|Required package|Description|Minimum version|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Specific IA development libraries|B.11.31|  
|SysMgmtMin|Minimum Software Deployment Tools|B.11.31.0709|  
|SysMgmtMin.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|On HP-UX, PAM is part of the core operating system components. There are no other dependencies.|  

 **Configuration Manager Dependencies:** The following table lists site system roles that support Linux and UNIX clients. For more information about these site system roles, see [Determine the site system roles for System Center Configuration Manager clients](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Configuration Manager site system|More information|  
|---------------------------------------|----------------------|  
|Management point|Although a management point is not required to install a Configuration Manager client for Linux and UNIX, you must have a management point to transfer information between client computers and Configuration Manager servers. Without a management point, you cannot manage client computers.|  
|Distribution point|The distribution point is not required to install a Configuration Manager client for Linux and UNIX. However, the site system role is required if you deploy software to Linux and UNIX servers.<br /><br /> Because the Configuration Manager client for Linux and UNIX does not support communications that use SMB, the distribution points you use with the client must support HTTP or HTTPS communication.|  
|Fallback status point|The fallback status point is not required to install a Configuration Manager client for Linux and UNIX. However, The fallback status point enables computers in the Configuration Manager site to send state messages when they cannot communicate with a management point. Client can also send their installation status to the fallback status point.|  

 **Firewall Requirements**: Ensure that firewalls do not block communications across the ports you specify as client request ports. The client for Linux and UNIX communicates directly with management points, distribution points, and fallback status points.  

 For information about client communication and request ports, see  [Configure the Client for Linux and UNIX to Locate Management Points](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Planning for Communication across Forest Trusts for Linux and UNIX Servers  
 Linux and UNIX servers you manage with Configuration Manager operate as workgroup clients and require similar configurations as Windows-based clients that are in a workgroup. For information about communications from computers that are in workgroups, see the [Communications across Active Directory forests](../../../../core/plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest) section in the [Communications between endpoints in System Center Configuration Manager](../../../../core/plan-design/hierarchy/communications-between-endpoints.md) topic.  

###  <a name="BKMK_ServiceLocationforLnU"></a> Service Location by the client for Linux and UNIX  
 The task of locating a site system server that provides service to clients is referred to as service location. Unlike a Windows-based client, the client for Linux and UNIX does not use Active Directory for service location. Additionally, the Configuration Manager client for Linux and UNIX does not support a client property that specifies the domain suffix of a management point. Instead, the client learns about additional site system servers that provide services to clients from a known management point you assign when you install the client software.  

 For more information about service location, see the [Service Location and how clients determine their assigned management point](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) section in the [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) topic.  

##  <a name="BKMK_SecurityforLnU"></a> Planning for Security and Certificates for Linux and UNIX Servers  
 For secure and authenticated communications with Configuration Manager sites, the Configuration Manager client for Linux and UNIX uses the same model for communication as the Configuration Manager client for Windows.  

 When you install the Linux and UNIX client, you can assign the client a PKI certificate that enables it to use HTTPS to communicate with Configuration Manager sites. If you do not assign a PKI certificate, the client creates a self-signed certificate and communicates only by HTTP.  

 Clients that are provided a PKI certificate when they install use HTTPS to communicate with management points. When a client is unable to locate a management point that supports HTTPS, it will fall back to use HTTP with the provided PKI certificate.  

 When a Linux or UNIX client uses a PKI certificate you do not have to approve them. When a client uses a self-signed certificate, review the hierarchy settings for client approval in the Configuration Manager console. If the client approval method is not **Automatically approve all computers (not recommended)**, you must manually approve the client.  

 For more information about how to manually approve the client, see the [Manage Clients from the Devices Node](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) section in the [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md) topic.  

 For information about how to use certificates in Configuration Manager, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

###  <a name="BKMK_AboutCertsforLnU"></a> About Certificates for use by Linux and UNIX Servers  
 The Configuration Manager client for Linux and UNIX uses a self-signed certificate or an X.509 PKI certificate just like Windows-based clients. There are no changes to the PKI requirements for Configuration Manager site systems when you manage Linux and UNIX clients.  

 The certificates you use for Linux and UNIX clients that communicate to Configuration Manager site systems must be in a Public Key Certificate Standard (PKCS#12) format, and the password must be known so you can specify it to the client when you specify the PKI certificate.  

 The Configuration Manager client for Linux and UNIX supports a single PKI certificate, and does not support multiple certificates. Therefore, the certificate selection criteria you configure for a Configuration Manager site does not apply.  

###  <a name="BKMK_ConfigCertsforLnU"></a> Configuring Certificates for Linux and UNIX Servers  
 To configure a Configuration Manager client for Linux and UNIX servers to use HTTPS communications, you must configure the client to use a PKI certificate at the time you install the client. You cannot provision a certificate prior to installation of the client software.  

 When you install a client that uses a PKI certificate, you use the command-line parameter **-UsePKICert** to specify the location and name of a PKCS#12 file that contains the PKI certificate. Additionally you must use the command line parameter **-certpw** to specify the password for the certificate.  

 If you do not specify **-UsePKICert**, the client generates a self-signed certificate and attempts to communicate to site system servers by using HTTP only.  

##  <a name="BKMK_NoSHA-256"></a> About Linux and UNIX Operating Systems That do not Support SHA-256  
 The following Linux and UNIX operating systems that are supported as clients for Configuration Manager were released with versions of OpenSSL that do not support SHA-256:  

-   Solaris Version 10 (SPARC/x86)  


 To manage these operating systems with Configuration Manager, you must install the Configuration Manager client for Linux and UNIX with a command line switch that directs the client to skip validation of SHA-256. Configuration Manager clients that run on these operating system versions operate in a less secure mode than clients that support SHA-256. This less secure mode of operation has the following behavior:  

-   Clients do not validate the site server signature associated with policy they request from a management point.  

-   Clients do not validate the hash for packages that they download from a distribution point.  

> [!IMPORTANT]  
>  The **ignoreSHA256validation** option allows you to run the client for Linux and UNIX computers in a less secure mode. This is intended for use on older platforms that did not include support for SHA-256. This is a security override and is not recommended by Microsoft, but is supported for use in a secure and trusted datacenter environment.  

 When the Configuration Manager client for Linux and UNIX installs, the install script checks the operating system version. By default, if the operating system version is identified as having released without a version of OpenSSL that supports SHA-256, the installation of the Configuration Manager client fails.  

 To install the Configuration Manager client on Linux and UNIX operating systems that did not release with a version of OpenSSL that supports SHA-256, you must use the install command line switch **ignoreSHA256validation**. When you use this command line option on an applicable Linux or UNIX operating system, the Configuration Manager client will skip SHA-256 validation and after installation, the client will not use SHA-256 to sign data it submits to site systems by using HTTP. For information about configuring Linux and UNIX clients to use certificates, see [Planning for Security and Certificates for Linux and UNIX Servers](#BKMK_SecurityforLnU) in this topic. For information about requiring SHA-256, see the [Configure Signing and Encryption](../../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) section in the [Configure security in System Center Configuration Manager](../../../../core/plan-design/security/configure-security.md) topic.  

> [!NOTE]  
>  The command line option **ignoreSHA256validation** is ignored on computers that run a version of Linux and UNIX that released with versions of OpenSSL that support SHA-256.  
