---
title: "Configuration options for site system roles for System Center Configuration Manager"
ms.custom: na
ms.date: 2016-04-25
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: 5
author: Brenduns
---
# Configuration options for site system roles for System Center Configuration Manager
Most configuration options for System Center Configuration Manager site system roles are self-explanatory or are explained in the wizard or dialog boxes when you configure them.  The following sections contain details for  site system roles that have settings that require additional information.  

##  <a name="BKMK_ApplicationCatalog_Website"></a> Application Catalog website point  
 For information about how to configure the Application Catalog website point for the Application Catalog, see [Plan for and configure application management in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Client connections**  

 Select **HTTPS** to connect by using the more secure setting and to determine whether clients connect from the Internet. This option requires a PKI certificate on the server for server authentication to clients and for encryption of data over Secure Socket Layer (SSL). For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in Internet Information Services (IIS), see the [Deploying the Web Server Certificate for Site Systems that Run IIS](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md#BKMK_webserver2008_cm2012) section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic.  

 **Add Application Catalog website to trusted sites zone**  

 This message displays the value in the default client settings whether the client setting **Add Application Catalog website to Internet Explorer trusted sites zone** is currently set to **True** or **False**. If you have configured this setting by using custom client settings, you must check this value yourself.  

 If this site system is configured for a FQDN, and the website is not in the trusted sites zone in Internet Explorer, users are prompted for credentials when they connect to the Application Catalog.  

 **Organization name**  

 Type the name that users see in the Application Catalog. This branding information helps users to identify this website as a trusted source.  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> Application Catalog web service point  
 For information about how to configure the Application Catalog web service point for the Application Catalog, see [Plan for and configure application management in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Select **HTTPS** to authenticate the Application Catalog website points to this Application Catalog web service point.  This option requires a PKI certificate on the servers running the Application Catalog website point for server authentication and for encryption of data over SSL. For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see the [Deploying the Web Server Certificate for Site Systems that Run IIS](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md#BKMK_webserver2008_cm2012) section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic.  

##  <a name="BKMK_CertificateRegistrationPoint"></a> Certificate registration point  
 For information about how to configure the certificate registration point, see [Configuring certificate profiles in System Center Configuration Manager](../../../../protect/deploy-use/configuring-certificate-profiles.md).  

##  <a name="BKMK_Distribution_Point"></a> Distribution point  
 For information about how to configure the distribution point for content deployment, see [Manage content and content infrastructure for System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 For information about how to configure the distribution point for PXE deployments, see [Use PXE to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 For information about how to configure the distribution point for multicast deployments, see [Use multicast to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Install and configure IIS if required by Configuration Manager**  

 Select this option to let Configuration Manager install and configure IIS on the site system if it is not already installed. IIS must be installed on all distribution points, and you must select this setting to continue in the wizard.  

 **Site System Installation Account**  

 For distribution points that are installed on a site server, only the computer account of the site server is supported for use as the Site System Installation Account.  

 **Create a self-signed certificate or import a PKI client certificate**  

 This certificate has two purposes:  

1.  It authenticates the distribution point to a management point before the distribution point sends status messages.  

2.  When **Enable PXE support for clients** is selected, the certificate is sent to computers that perform a PXE boot so that they can connect to a management point during the deployment of the operating system.  

When all your management points in the site are configured for HTTP, create a self-signed certificate. When your management points are configured for HTTPS, import a PKI client certificate.  

To import the certificate, browse to a Public-Key Cryptography Standards #12 (PKCS #12) file that contains a PKI certificate with the following requirements for Configuration Manager:  

-   Intended use must include client authentication.  

-   The private key must be configured to be exported.  

There are no specific requirements for the certificate Subject name or Subject Alternative Name (SAN), and you can use the same certificate for multiple distribution points.  

For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). For an example deployment of this certificate, see the Deploying the Client Certificate for Distribution Points section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic.  

**Enable this distribution point for prestaged content**  

Select this check box to enable the distribution point for prestaged content. When this check box is selected, you can configure distribution behavior when you distribute content. You can choose whether you always prestage the content on the distribution point, prestage the initial content for the package, but use the normal content distribution process when there are updates to the content, or always use the normal content distribution process for the content in the package.  

**Boundary groups**  

 You can associate boundary groups to a distribution point. During content deployment, clients must be in a boundary group that is associated with the distribution point to use it as a source location for content. You can select the **Allow fallback source location for content** check box to allow clients outside these boundary groups to fall back and use the distribution point as a source location for content when no other distribution points are available.  

##  <a name="BKMK_Enrollment_Point"></a> Enrollment point  
Enrollment points are used to install Mac computers and enroll devices you manage with on-premises mobile device management. For more information, see the following:  

-   [How to deploy clients to Macs in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../../../mdm/deploy-use/how-users-enroll-devices-with-on-premises-mobile-device-management.md)  

**Allowed connections**  

 The HTTPS setting is automatically selected and requires a PKI certificate on the server for server authentication to the enrollment proxy point and the out of band service point, and for encryption of data over SSL. For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see the [Deploying the Web Server Certificate for Site Systems that Run IIS](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md#BKMK_webserver2008_cm2012) section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic.  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> Enrollment proxy point  
For information about how to configure an enrollment proxy point for mobile devices, see [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../../../mdm/deploy-use/how-users-enroll-devices-with-on-premises-mobile-device-management.md).  

**Client connections**  

 The HTTPS setting is automatically selected and requires a PKI certificate on the server for server authentication to mobile devices and Mac computers enrolled by Configuration Manager, and for encryption of data over Secure Sockets Layer (SSL). For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see the [Deploying the Web Server Certificate for Site Systems that Run IIS](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md#BKMK_webserver2008_cm2012) section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic.  

##  <a name="BKMK_Fallback_Status_Point"></a> Fallback status point  
**Number of state messages** and **Throttle interval (in seconds)**  

Although the default settings for these options (10,000 state messages and 3,600 seconds for the throttle interval) are sufficient for most circumstances, you might have to change them when both of the following conditions are true:  

-   The fallback status point accepts connections only from the intranet.  

-   You use the fallback status point during a client deployment rollout for many computers.  

In this scenario, a continuous stream of state messages might create a backlog of state messages that causes high central processing unit (CPU) usage on the site server for a sustained period of time. In addition, you might not see up-to-date information about the client deployment in the Configuration Manager console and in the client deployment reports.  

These fallback status point settings are designed to be configured for state messages that are generated during client deployment. The settings are not designed to be configured for client communication issues, such as when clients on the Internet cannot connect to their Internet-based management point. Because the fallback status point cannot apply these settings just to the state messages that are generated during client deployment, do not configure these settings when the fallback status point accepts connections from the Internet.  

Each computer that successfully installs the System Center 2012 Configuration Manager client sends the following four state messages to the fallback status point:  

-   Client deployment started  

-   Client deployment succeeded  

-   Client assignment started  

-   Client assignment succeeded  

Computers that cannot be installed or assign the Configuration Manager client send additional state messages.  

For example, if you deploy the Configuration Manager client to 20,000 computers, the deployment might create 80,000 state messages sent to the fallback status point. Because the default throttling configuration allows for 10,000 state messages to be sent to the fallback status point each 3600 seconds (1 hour), state messages might become backlogged on the fallback status point because of the throttling configuration. You must also consider the available network bandwidth between the fallback status point and the site server, and the processing power of the site server to process many state messages.  

To help prevent these issues, consider increasing the number of state messages and decreasing the throttle interval.  

Reset the throttle values for the fallback status point if either of the following conditions is true:  

-   You calculate that the current throttle values are higher than required to process state messages from the fallback status point.  

-   You find that the current throttle settings create high CPU usage on the site server.  

Do not change the settings for the fallback status point throttle settings unless you understand the consequences. For example, when you increase the throttle settings to high, the CPU usage on the site server can increase to high, which slows down all site operations.  

## See Also  
 [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md)
