---
title: "Prepare to deploy client software to Macs"
titleSuffix: "Configuration Manager"
description: Configuration tasks prior to deploying the Configuration Manager client to Macs.
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Prepare to deploy client software to Macs

*Applies to: System Center Configuration Manager (Current Branch)*

Follow these steps to ensure that you're ready to [deploy the Configuration Manager client to Mac computers](/sccm/core/clients/deploy/deploy-clients-to-macs).

## Mac prerequisites

The Mac client installation package is not supplied with the Configuration Manager media. Download the **Clients for Additional Operating Systems** from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Supported versions:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra )  

-   **Mac OS X 10.13** (macOS High Sierra )  

## Certificate requirements
Client installation and management for Mac computers requires public key infrastructure (PKI) certificates. PKI certificates secure the communication between the Mac computers and the Configuration Manager site by using mutual authentication and encrypted data transfers. Configuration Manager can request and install a user client certificate by using Microsoft Certificate Services with an enterprise certification authority (CA) and the Configuration Manager enrollment point and enrollment proxy point site system roles. Or, you can request and install a computer certificate independently from Configuration Manager if the certificate meets the requirements for Configuration Manager.   

Configuration Manager Mac clients always perform certificate revocation checking. You cannot disable this function.  

If Mac clients cannot confirm the certificate revocation status for a server certificate because they cannot locate the CRL, they will not be able to successfully connect to Configuration Manager site systems. Especially for Mac clients in a different forest to the issuing certification authority, check your CRL design to ensure that Mac clients can locate and connect to a CRL distribution point (CDP) for connecting site system servers.  

Before you install the Configuration Manager client on a Mac computer, decide how to install the client certificate:  

-   Use Configuration Manager enrollment by using the [CMEnroll tool](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). The enrollment process does not support automatic certificate renewal so you must re-enroll Mac computers before the installed certificate expires.  

-   [Use a certificate request and installation method that is independent from Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

For more information about the Mac client certificate requirement and other PKI certificates that are required to support Mac computers, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Mac clients are automatically assigned to the Configuration Manager site that manages them. Mac clients install as Internet-only clients, even if communication is restricted to the intranet. This client configuration means that they will communicate with the site system roles (management points and distribution points) in their assigned site when you configure these site system roles to allow client connections from the Internet. Mac computers do not communicate with site system roles outside their assigned site.  

> [!IMPORTANT]  
>  The Configuration Manager Mac client cannot be used to connect to a management point that is configured to use a [database replica](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


## Deploy a web server certificate to site system servers  
If these site systems don't have it, deploy a web server certificate to the computers that have these site system roles:  

-   Management point  

-   Distribution point  

-   Enrollment point  

-   Enrollment proxy point  

The web server certificate must contain the Internet FQDN that is specified in the site system properties. The server doesn't have to be accessible from the Internet to support Mac computers. If you do not require Internet-based client management, you can specify the intranet FQDN value for the Internet FQDN.  

Specify the site system's Internet FQDN value in the web server certificate for the management point, the distribution point, and the enrollment proxy point.

For an example deployment that creates and installs this web server certificate, see the [Deploying the Web Server Certificate for Site Systems that Run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## Deploy a client authentication certificate to site system servers  
 If these site systems don't have it, deploy a client authentication certificate to the computers that host these site system roles:  

-   Management point  

-   Distribution point  

 For an example deployment that creates and installs the client certificate for management points, see the [Deploying the Client Certificate for Windows Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 For an example deployment that creates and installs the client certificate for distribution points, see the [Deploying the Client Certificate for Distribution Points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

>[!IMPORTANT]
>  To deploy the client to devices running macOS Sierra, the Subject name of the management point certificate must be configured correctly, for example, by using the FQDN of the management point server.

## Prepare the client certificate template for Macs  

 The certificate template must have **Read** and **Enroll** permissions for the user account that will enroll the certificate on the Mac computer.  

 See [Deploying the Client Certificate for Mac Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

## Configure the management point and distribution point  
 Configure management points for the following options:  

-   HTTPS  

-   Allow client connections from the Internet. This configuration value is required to manage Mac computers. However, it does not mean that site system servers must be accessible from the Internet.  

-   Allow mobile devices and Mac computers to use this management point  

 Although distribution points are not required to install the client, you must configure distribution points to allow client connections from the Internet if you want to deploy software to these computers after the client is installed.  


### To configure management points and distribution points to support Macs  

Before you start this procedure, make sure that the site system server that runs the management point and distribution point is configured with an Internet FQDN. If these servers won't support Internet-based client management, you can specify the intranet FQDN as the Internet FQDN value.

The site system roles must be in a primary site.  


1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Servers and Site System Roles**, and then choose the server that has the right site system roles.  

3.  In the details pane, right-click **Management point**, choose **Role Properties**, and in the **Management Point Properties** dialog box, configure these options:  

    1.  Choose **HTTPS**.  

    2.  Choose **Allow Internet-only client connections** or **Allow intranet and Internet client connections**. These options require an Internet or intranet FQDN.  

    3.  Choose **Allow mobile devices and Mac computers to use this management point**.  

4.  In the details pane, right-click **Distribution point**, choose **Role Properties**, and in the **Distribution Point Properties** dialog box, configure these options:  

    -   Choose **HTTPS**.  

    -   Choose **Allow Internet-only client connections** or **Allow intranet and Internet client connections**. These options require an Internet or intranet FQDN.  

    -   Choose **Import certificate**, browse to the exported client distribution point certificate file, and then specify the password.  

5.  Repeat steps 2 through 4 for all management points and distribution points in primary sites that you will use with Macs.  

## Configure the enrollment proxy point and the enrollment point  
 You must install both these site system roles in the same site but you do not have to install them on the same site system server, or in the same Active Directory forest.  

 For more information about site system role placement and considerations, see  [Site system roles](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) in [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 These procedures configure the site system roles to support Mac computers.   

-   [New site system server](#new-site-system-server)  

-   [Existing site system server](#existing-site-system-server)  

###  New site system server  

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Servers and Site System Roles**  

3.  On the **Home** tab, in the **Create** group, choose **Create Site System Server**.  

4.  On the **General** page, specify the general settings for the site system.  Make sure that you specify a value for the Internet FQDN. If the server won't be accessible from the Internet, use the intranet FQDN.  

5.  On the **System Role Selection** page, select **Enrollment proxy point** and **Enrollment point** from the list of available roles.  

6.  On the **Enrollment Proxy Point** page, review the settings and make any necessary changes.  

7.  On the **Enrollment Point Settings** page, review the settings and make any necessary changes. Then, complete the wizard.  

### Existing site system server  

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Servers and Site System Roles**, and then choose the server that you want to use to support Macs.  

3.  On the **Home** tab, in the **Create** group, choose **Add Site System Roles**.  

4.  On the **General** page, specify the general settings for the site system, and then click **Next**. Make sure that you specify a value for the Internet FQDN. If the server won't be accessible from the Internet, use the intranet FQDN.   

5.  On the **System Role Selection** page, choose **Enrollment proxy point** and **Enrollment point** from the list of available roles.  

6.  On the **Enrollment Proxy Point** page, review the settings and make any necessary changes.  

7.  On the **Enrollment Point Settings** page, review the settings and make any necessary changes. Then, complete the wizard.  

## Install the reporting services point  
 [Install the reporting services point](../../../core/servers/manage/configuring-reporting.md) if you want to run reports for Macs.  

### Next steps

[Deploy the Configuration Manager client to Mac computers](/sccm/core/clients/deploy/deploy-clients-to-macs).  
