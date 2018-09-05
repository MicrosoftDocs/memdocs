---
title: Site system role options
titleSuffix: Configuration Manager
description: Consult this article for details about Configuration Manager site system roles that are not necessarily self-explanatory.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configuration options for site system roles in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Most configuration options for Configuration Manager site system roles are self-explanatory or are explained in the wizard or dialog boxes when you configure them. The following sections explain site system roles whose settings might require additional information.  



##  <a name="BKMK_ApplicationCatalog_Website"></a> Application Catalog website point  

> [!Note]  
> Starting in version 1806, the application catalog website point is no longer *required*, but still *supported*. For more information, see [Configure Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  
> 
> The **Silverlight user experience** for the application catalog website point is no longer supported. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

 For more information about how to set up the Application Catalog website point, see [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### Client connections
 Select **HTTPS** to use the more secure connection setting and to check whether clients connect from the internet. This option requires a PKI certificate on the server for server authentication to clients, and for encryption of data over Secure Socket Layer (SSL). For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  

 For an example deployment of the server certificate and information about how to configure it in Internet Information Services (IIS), see [Deploying the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

 #### Add Application Catalog website to trusted sites zone  
 This message shows the value in the default client settings whether the **Add Application Catalog website to Internet Explorer trusted sites zone** client setting is currently set to **True** or **False**. If you used custom client settings to configure this setting, enable this setting.  

 If this site system is set up for a fully qualified domain name (FQDN), and the website isn't in the trusted sites zone in Internet Explorer, users are prompted for credentials when they connect to the Application Catalog.  

 #### Organization name  

 Enter the name that users see in the Application Catalog. This branding information helps users identify this website as a trusted source.  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> Application Catalog web service point  

> [!Note]  
> Starting in version 1806, the application catalog web service point is no longer *required*, but still *supported*. For more information, see [Configure Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

 For more information about how to set up the Application Catalog web service point, see [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### HTTPS

 Select **HTTPS** to authenticate the Application Catalog website points to this Application Catalog web service point. This option requires a PKI certificate on servers that run the Application Catalog website point for server authentication, and for encryption of data over SSL. For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  

 For an example deployment of the server certificate and information about how to configure it in Internet Information Services (IIS), see [Deploying the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_CertificateRegistrationPoint"></a> Certificate registration point  

 For more information about how to set up the certificate registration point, see [Introduction to certificate profiles](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  



##  <a name="BKMK_Distribution_Point"></a> Distribution point  

 For more information about how to set up the distribution point for content deployment, see [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

 For more information about how to set up the distribution point for PXE deployments, see [Use PXE to deploy Windows over the network](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

 For more information about how to set up the distribution point for multicast deployments, see [Use multicast to deploy Windows over the network](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

 #### Install and configure IIS if required by Configuration Manager
 Select this option to let Configuration Manager install and set up IIS on the site system if it's not already installed. IIS must be installed on all distribution points, and you must select this setting to continue in the wizard.  

 #### Site System Installation Account
 For distribution points that are installed on a site server, only the computer account of the site server is supported for use as the Site System Installation Account. For more information, see [Accounts](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

 #### Create a self-signed certificate or import a PKI client certificate
 This certificate has two purposes:  

1.  It authenticates the distribution point to a management point before the distribution point sends status messages.  

2.  When **Enable PXE support for clients** is selected, the certificate is sent to computers for PXE boot. They use this certificate to connect to a management point during the deployment of the OS.  

When all your management points in the site are set up for HTTP, create a self-signed certificate. When your management points are set up for HTTPS, import a PKI client certificate.  

To import the certificate, browse to a Public-Key Cryptography Standards #12 (PKCS #12) file that has a PKI certificate with the following requirements for Configuration Manager:  

-   Intended use must include client authentication.  

-   The private key must be set up to be exported.  

There are no specific requirements for the certificate Subject name or Subject Alternative Name (SAN). You can use the same certificate for multiple distribution points.  

For more information about the certificate requirements, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements). 

For an example deployment of this certificate, see [Deploying the client certificate for distribution points](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

#### Enable this distribution point for prestaged content
Select this checkbox to enable the distribution point for prestaged content. When you enable this option, you can set up distribution behavior when you distribute content. You can choose whether you always prestage content on the distribution point, prestage initial content for the package but use the normal content distribution process for updates to content, or always use the normal content distribution process for content in the package. For more information, see [Prestaged content](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

#### Boundary groups
 You can associate boundary groups to a distribution point. During content deployment, clients must be in a boundary group that is associated with the distribution point to use it as a source location for content. Set up relationships between boundary groups that check when a client can begin to search additional boundary groups for valid content source locations. For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/boundary-groups).



##  <a name="BKMK_Enrollment_Point"></a> Enrollment point  

Enrollment points are used to install macOS computers and enroll devices that you manage with on-premises mobile device management. For more information, see the following articles:  

-   [How to deploy clients to Macs](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [How users enroll devices with on-premises MDM](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### Allowed connections
 The HTTPS setting is automatically selected and requires a PKI certificate on the server for server authentication to the enrollment proxy point, server authentication to the out-of-band service point, and encryption of data over SSL. For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see [Deploying the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> Enrollment proxy point  

For more information about how to set up an enrollment proxy point for mobile devices, see [How users enroll devices with on-premises MDM](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

#### Client connections
 The HTTPS setting is automatically selected. It requires the following PKI certificates on the server: 
- For server authentication to mobile devices and Mac computers that you enroll with Configuration Manager 
- For encryption of data over Secure Sockets Layer (SSL)

For more information about the certificate requirements, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  

 For an example deployment of the server certificate and information about how to configure it in IIS, see [Deploying the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Fallback_Status_Point"></a> Fallback status point  

#### Number of state messages and Throttle interval (in seconds)
The default settings for these options are 10,000 state messages and 3,600 seconds for the throttle interval. While these settings are sufficient for most circumstances, you might have to change them when both of the following conditions are true:  

-   The fallback status point accepts connections only from the intranet.  

-   You use the fallback status point during a client deployment rollout for many computers.  

In this scenario, a continuous stream of state messages might create a backlog of state messages that causes high processor usage on the site server for a sustained period. In addition, you might not see up-to-date information about the client deployment in the Configuration Manager console and in the client deployment reports.  

These fallback status point settings are designed to be set up for state messages that are generated during client deployment. The settings aren't designed to be set up for client communication issues, like when clients on the internet can't connect to their internet-based management point. Because the fallback status point can't apply these settings just to the state messages that are generated during client deployment, don't configure these settings when the fallback status point accepts connections from the internet.  

Each computer that successfully installs the Configuration Manager client sends the following four state messages to the fallback status point:  

-   Client deployment started  

-   Client deployment succeeded  

-   Client assignment started  

-   Client assignment succeeded  

Computers that can't be installed or that assign the Configuration Manager client send additional state messages.  

For example, if you deploy the Configuration Manager client to 20,000 computers, the deployment might send 80,000 state messages to the fallback status point. Because the default throttling configuration lets 10,000 state messages to be sent to the fallback status point each 3,600 seconds (1 hour), state messages might become backlogged on the fallback status point. Also consider the available network bandwidth between the fallback status point and the site server and the processing power of the site server to process many state messages.  

To help prevent these issues, consider an increase in the number of state messages and a decrease in the throttle interval.  

Reset the throttle values for the fallback status point if either of the following conditions is true:  

-   You calculate that the current throttle values are higher than required to process state messages from the fallback status point.  

-   You find that the current throttle settings create high processor usage on the site server.  

Don't change the settings for the fallback status point throttle settings unless you understand the consequences. For example, when you increase the throttle settings to high, the processor usage on the site server can increase to high, which slows down all site operations.  
