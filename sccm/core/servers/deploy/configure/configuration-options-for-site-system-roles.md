---
title: "Site system role options"
titleSuffix: "Configuration Manager"
description: "Consult this article for details about Configuration Manager site system roles that are not necessarily self-explanatory."
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration options for site system roles for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Most configuration options for System Center Configuration Manager site system roles are self-explanatory or are explained in the wizard or dialog boxes when you configure them. The following sections explain site system roles whose settings might require additional information.  

##  <a name="BKMK_ApplicationCatalog_Website"></a> Application Catalog website point  
 For information about how to set up the Application Catalog website point for the Application Catalog, see [Plan for and configure application management in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Client connections**  

 Select **HTTPS** to use the more secure connection setting and to check whether clients connect from the Internet. This option requires a PKI certificate on the server for server authentication to clients and for encryption of data over Secure Socket Layer (SSL). For more about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in Internet Information Services (IIS), see the *Deploying the Web Server Certificate for Site Systems that Run IIS* section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Add Application Catalog website to trusted sites zone**  

 This message shows the value in the default client settings whether the **Add Application Catalog website to Internet Explorer trusted sites zone** client setting is currently set to **True** or **False**. If you used custom client settings to configure this setting, you must check this value yourself.  

 If this site system is set up for a fully qualified domain name (FQDN), and the website is not in the trusted sites zone in Internet Explorer, users are prompted for credentials when they connect to the Application Catalog.  

 **Organization name**  

 Enter the name that users see in the Application Catalog. This branding information helps users identify this website as a trusted source.  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> Application Catalog web service point  
 For information about how to set up the Application Catalog web service point for the Application Catalog, see [Plan for and configure application management in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Select **HTTPS** to authenticate the Application Catalog website points to this Application Catalog web service point.  This option requires a PKI certificate on servers that run the Application Catalog website point for server authentication and for encryption of data over SSL. For more about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see the *Deploying the Web Server Certificate for Site Systems that Run IIS* section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_CertificateRegistrationPoint"></a> Certificate registration point  
 For more about how to set up the certificate registration point, see [Introduction to certificate profiles](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="BKMK_Distribution_Point"></a> Distribution point  
 For more about how to set up the distribution point for content deployment, see [Manage content and content infrastructure for System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 For more about how to set up the distribution point for PXE deployments, see [Use PXE to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 For information about how to set up the distribution point for multicast deployments, see [Use multicast to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Install and configure IIS if required by Configuration Manager**  
 Select this option to let Configuration Manager install and set up IIS on the site system if it is not already installed. IIS must be installed on all distribution points, and you must select this setting to continue in the wizard.  

 **Site System Installation Account**  
 For distribution points that are installed on a site server, only the computer account of the site server is supported for use as the Site System Installation Account.  

 **Create a self-signed certificate or import a PKI client certificate**  
 This certificate has two purposes:  

1.  It authenticates the distribution point to a management point before the distribution point sends status messages.  

2.  When **Enable PXE support for clients** is selected, the certificate is sent to computers that do a PXE boot so that they can connect to a management point during the deployment of the operating system.  

When all your management points in the site are set up for HTTP, create a self-signed certificate. When your management points are set up for HTTPS, import a PKI client certificate.  

To import the certificate, browse to a Public-Key Cryptography Standards #12 (PKCS #12) file that has a PKI certificate with the following requirements for Configuration Manager:  

-   Intended use must include client authentication.  

-   The private key must be set up to be exported.  

There are no specific requirements for the certificate Subject name or Subject Alternative Name (SAN), and you can use the same certificate for multiple distribution points.  

For more about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). For an example deployment of this certificate, see the *Deploying the Client Certificate for Distribution Points* section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Enable this distribution point for prestaged content**  
Check this check box to enable the distribution point for prestaged content. When this check box is checked, you can set up distribution behavior when you distribute content. You can choose whether you always prestage content on the distribution point, prestage initial content for the package but use the normal content distribution process for updates to content, or always use the normal content distribution process for content in the package.  

**Boundary groups**  
 You can associate boundary groups to a distribution point. During content deployment, clients must be in a boundary group that is associated with the distribution point to use it as a source location for content.
 - **Prior to version 1610**, you can check the **Allow fallback source location for content** check box to let clients outside these boundary groups fall back and use the distribution point as a source location for content when no other distribution points are available.
 - **Beginning with version 1610**, you no longer can configure **Allow fallback source location for content**.  Instead, you set up relationships between boundary groups that check when a client can begin to search additional boundary groups for valid content source locations.

##  <a name="BKMK_Enrollment_Point"></a> Enrollment point  
Enrollment points are used to install Mac computers and enroll devices that you manage with on-premises mobile device management. For more information, see the following:  

-   [How to deploy clients to Macs in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Allowed connections**  
 The HTTPS setting is automatically selected and requires a PKI certificate on the server for server authentication to the enrollment proxy point, server authentication to the out-of-band service point, and encryption of data over SSL. For more about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see the *Deploying the Web Server Certificate for Site Systems that Run IIS* section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> Enrollment proxy point  
For more about how to set up an enrollment proxy point for mobile devices, see [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Client connections**  
 The HTTPS setting is automatically selected and requires a PKI certificate on the server for server authentication to mobile devices and Mac computers that are enrolled by Configuration Manager, and for encryption of data over Secure Sockets Layer (SSL). For more about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see the *Deploying the Web Server Certificate for Site Systems that Run IIS* section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Fallback_Status_Point"></a> Fallback status point  
**Number of state messages** and **Throttle interval (in seconds)**  
Although the default settings for these options (10,000 state messages and 3,600 seconds for the throttle interval) are sufficient for most circumstances, you might have to change them when both of the following conditions are true:  

-   The fallback status point accepts connections only from the intranet.  

-   You use the fallback status point during a client deployment rollout for many computers.  

In this scenario, a continuous stream of state messages might create a backlog of state messages that causes high central processing unit (CPU) usage on the site server for a sustained period. In addition, you might not see up-to-date information about the client deployment in the Configuration Manager console and in the client deployment reports.  

These fallback status point settings are designed to be set up for state messages that are generated during client deployment. The settings are not designed to be set up for client communication issues, like when clients on the Internet cannot connect to their Internet-based management point. Because the fallback status point cannot apply these settings just to the state messages that are generated during client deployment, do not configure these settings when the fallback status point accepts connections from the Internet.  

Each computer that successfully installs the System Center 2012 Configuration Manager client sends the following four state messages to the fallback status point:  

-   Client deployment started  

-   Client deployment succeeded  

-   Client assignment started  

-   Client assignment succeeded  

Computers that cannot be installed or that assign the Configuration Manager client send additional state messages.  

For example, if you deploy the Configuration Manager client to 20,000 computers, the deployment might send 80,000 state messages to the fallback status point. Because the default throttling configuration lets 10,000 state messages to be sent to the fallback status point each 3,600 seconds (1 hour), state messages might become backlogged on the fallback status point. You must also consider the available network bandwidth between the fallback status point and the site server and the processing power of the site server to process many state messages.  

To help prevent these issues, consider an increase in the number of state messages and a decrease in the throttle interval.  

Reset the throttle values for the fallback status point if either of the following conditions is true:  

-   You calculate that the current throttle values are higher than required to process state messages from the fallback status point.  

-   You find that the current throttle settings create high CPU usage on the site server.  

Do not change the settings for the fallback status point throttle settings unless you understand the consequences. For example, when you increase the throttle settings to high, the CPU usage on the site server can increase to high, which slows down all site operations.  
