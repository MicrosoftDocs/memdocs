---
title: Prepare to deploy the client to Macs
titleSuffix: Configuration Manager
description: Configuration tasks prior to deploying the Configuration Manager client to Macs.
ms.date: 01/05/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: install-set-up-deploy
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Prepare to deploy client software to Macs

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in January 2022, this feature of Configuration Manager is deprecated.<!-- 12927803 --> For more information, see [Mac computers](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

Follow these steps to make sure that you're ready to [deploy the Configuration Manager client to Mac computers](deploy-clients-to-macs.md).

For the list of supported versions, see [Supported operating systems for clients and devices](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

## Certificate requirements

Client installation and management for Mac computers requires public key infrastructure (PKI) certificates. PKI certificates secure the communication between the Mac computers and the Configuration Manager site by using mutual authentication and encrypted data transfers. Configuration Manager can request and install a user client certificate. It uses Certificate Services with an enterprise certification authority, and the Configuration Manager enrollment point and enrollment proxy point. You can also request and install a computer certificate independently from Configuration Manager. This certificate must meet the Configuration Manager certificate requirements.  

Configuration Manager Mac clients always check for certificate revocation. You can't disable this function.  

If Mac clients can't locate the certificate revocation list (CRL), they can't connect to Configuration Manager site systems. Especially for Mac clients in a different forest to the issuing certification authority, check your CRL design. Make sure that Mac clients can locate and download a CRL.  

Before you install the Configuration Manager client on a Mac computer, decide how to install the client certificate:  

-   Use Configuration Manager enrollment by using the [CMEnroll tool](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). The enrollment process doesn't support automatic certificate renewal. Re-enroll Mac computers before the certificate expires.  

-   [Use a certificate request and installation method that's independent from Configuration Manager](deploy-clients-to-macs.md#bkmk_external).  

For more information about Mac client certificate requirements, see [PKI certificate requirements for Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

Mac clients are automatically assigned to the Configuration Manager site that manages them. Mac clients install as internet-only clients, even if communication is restricted to the intranet. This configuration means that they communicate with internet-enabled management points and distribution points in their assigned site. Mac computers don't communicate with site systems outside their assigned site.  

> [!IMPORTANT]  
>  The Configuration Manager client for macOS can't be used to connect to a management point that's configured to use a [database replica](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## Deploy a web server certificate to site system servers  

If these site systems don't have it, deploy a web server certificate to the computers that have these site system roles:  

-   Management point  

-   Distribution point  

-   Enrollment point  

-   Enrollment proxy point  

The web server certificate must include the internet FQDN that's specified in the site system properties. The server doesn't have to be accessible from the internet to support Mac computers. If you don't require internet-based client management, you can specify the intranet FQDN value for the internet FQDN.  

Specify the site system's internet FQDN value in the web server certificate for the management point, the distribution point, and the enrollment proxy point.

For more information of an example deployment, see [Deploying the web server certificate for site systems that run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## Deploy a client authentication certificate to site system servers  

If these site systems don't have it, deploy a client authentication certificate to the computers that host these site system roles:  

-   Management point  

-   Distribution point  

For an example deployment that creates and installs the client certificate for management points, see the [Deploying the client certificate for Windows computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

For an example deployment that creates and installs the client certificate for distribution points, see the [Deploying the client certificate for distribution points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  To deploy the client to devices running macOS Sierra, the subject name of the management point certificate must be configured correctly. For example, use the FQDN of the management point server.  



## Prepare the client certificate template for Macs  

The certificate template must have **Read** and **Enroll** permissions for the user account that enrolls the certificate on the Mac computer.  

For more information, see [Deploying the client certificate for Mac computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## Configure the management point and distribution point  

Configure management points for the following options:  

-   HTTPS  

-   Allow client connections from the internet. This configuration value is required to manage Mac computers. However, it doesn't mean that site system servers must be accessible from the internet.  

-   Allow mobile devices and Mac computers to use this management point  

Distribution points aren't required to install the client for Mac. If you want to deploy software to these computers after you install the client, configure distribution points to allow client connections from the internet.  


### To configure management points and distribution points to support Macs  

Before you start this procedure, make sure to configure the management point and distribution point with an internet FQDN. If these servers don't support internet-based client management, specify the intranet FQDN as the internet FQDN value.

The site system roles must be in a primary site.  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node. Then select the server that has the right site system roles.  

2.  In the details pane, select the **Management point** role, and select **Properties** in the ribbon. In the **Management point Properties** window, configure these options:  

    1.  Choose **HTTPS**.  

    2.  Choose **Allow internet-only client connections** or **Allow intranet and internet client connections**. These options require an internet or intranet FQDN.  

    3.  Choose **Allow mobile devices and Mac computers to use this management point**.  

    4. Select **OK** to save this configuration.  

3.  In the details pane of the Server and Site System Roles node, select the **Distribution point** role, and select **Properties** in the ribbon. In the **Distribution point Properties** window, configure these options:  

    -   Choose **HTTPS**.  

    -   Choose **Allow internet-only client connections** or **Allow intranet and internet client connections**. These options require an internet or intranet FQDN.  

    -   Choose **Import certificate**, browse to the exported client distribution point certificate file, and then specify the password.  

4.  Repeat this procedure for all management points and distribution points in primary sites that manage Mac computers.  



## Configure the enrollment proxy point and the enrollment point  

Install both roles in the same site. You don't have to install them on the same site system server, or in the same Active Directory forest.  

For more information about site system role placement and considerations, see [Site system roles](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

To add the site system roles to support Mac computers, see [Install site system roles](../../servers/deploy/configure/install-site-system-roles.md).

On the **System Role Selection** page, select **Enrollment proxy point** and **Enrollment point** from the list of available roles.  



## Install the reporting services point  

For more information, see [Install the reporting services point](../../servers/manage/configuring-reporting.md).  



## Next steps

[Deploy the Configuration Manager client to Mac computers](deploy-clients-to-macs.md)  
