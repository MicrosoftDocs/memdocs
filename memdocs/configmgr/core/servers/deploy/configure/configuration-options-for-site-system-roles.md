---
title: Site system role options
titleSuffix: Configuration Manager
description: Consult this article for details about Configuration Manager site system roles that are not necessarily self-explanatory.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Configuration options for site system roles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Most configuration options for Configuration Manager site system roles are self-explanatory or are explained in the wizard or dialog boxes when you configure them. The following sections explain site system roles whose settings might require additional information.  

## <a name="BKMK_CertificateRegistrationPoint"></a> Certificate registration point  

For more information about how to set up the certificate registration point, see [Introduction to certificate profiles](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  

## <a name="BKMK_Distribution_Point"></a> Distribution point  

For more information about how to set up the distribution point for content deployment, see [Manage content and content infrastructure](manage-content-and-content-infrastructure.md).  

For more information about how to set up the distribution point for PXE deployments, see [Use PXE to deploy Windows over the network](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

For more information about how to set up the distribution point for multicast deployments, see [Use multicast to deploy Windows over the network](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### Install and configure IIS if required by Configuration Manager

Select this option to let Configuration Manager install and set up IIS on the site system if it's not already installed. IIS must be installed on all distribution points, and you must select this setting to continue in the wizard.  

### Site system installation account

For distribution points that are installed on a site server, only the computer account of the site server is supported for use as the site system installation account. For more information, see [Accounts](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="BKMK_Enrollment_Point"></a> Enrollment point  

Enrollment points are used to install macOS computers and enroll devices that you manage with on-premises mobile device management. For more information, see the following articles:  

- [How to deploy clients to Macs](../../../clients/deploy/deploy-clients-to-macs.md)  

- [How users enroll devices with on-premises MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### Allowed connections

The HTTPS setting is automatically selected and requires a PKI certificate on the server for server authentication to the enrollment proxy point, and encryption of data over SSL. For more information, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).  

For an example deployment of the server certificate and information about how to configure it in IIS, see [Deploying the web server certificate for site systems that run IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="BKMK_Enrollment_Proxy_Point"></a> Enrollment proxy point  

For more information about how to set up an enrollment proxy point for mobile devices, see [How users enroll devices with on-premises MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

### Client connections

The HTTPS setting is automatically selected. It requires the following PKI certificates on the server:

- For server authentication to mobile devices and Mac computers that you enroll with Configuration Manager
- For encryption of data over Secure Sockets Layer (SSL)

For more information about the certificate requirements, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).  

For an example deployment of the server certificate and information about how to configure it in IIS, see [Deploying the web server certificate for site systems that run IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="BKMK_Fallback_Status_Point"></a> Fallback status point  

### Number of state messages and Throttle interval (in seconds)

The default settings for these options are 10,000 state messages and 3,600 seconds for the throttle interval. While these settings are sufficient for most circumstances, you might have to change them when both of the following conditions are true:  

- The fallback status point accepts connections only from the intranet.  

- You use the fallback status point during a client deployment rollout for many computers.  

In this scenario, a continuous stream of state messages might create a backlog of state messages that causes high processor usage on the site server for a sustained period. In addition, you might not see up-to-date information about the client deployment in the Configuration Manager console and in the client deployment reports.  

These fallback status point settings are designed to be set up for state messages that are generated during client deployment. The settings aren't designed to be set up for client communication issues, like when clients on the internet can't connect to their internet-based management point. Because the fallback status point can't apply these settings just to the state messages that are generated during client deployment, don't configure these settings when the fallback status point accepts connections from the internet.  

Each computer that successfully installs the Configuration Manager client sends the following four state messages to the fallback status point:  

- Client deployment started  

- Client deployment succeeded  

- Client assignment started  

- Client assignment succeeded  

Computers that can't be installed or that assign the Configuration Manager client send additional state messages.  

For example, if you deploy the Configuration Manager client to 20,000 computers, the deployment might send 80,000 state messages to the fallback status point. Because the default throttling configuration lets 10,000 state messages to be sent to the fallback status point each 3,600 seconds (1 hour), state messages might become backlogged on the fallback status point. Also consider the available network bandwidth between the fallback status point and the site server and the processing power of the site server to process many state messages.  

To help prevent these issues, consider an increase in the number of state messages and a decrease in the throttle interval.  

Reset the throttle values for the fallback status point if either of the following conditions is true:  

- You calculate that the current throttle values are higher than required to process state messages from the fallback status point.  

- You find that the current throttle settings create high processor usage on the site server.  

Don't change the settings for the fallback status point throttle settings unless you understand the consequences. For example, when you increase the throttle settings to high, the processor usage on the site server can increase to high, which slows down all site operations.  
