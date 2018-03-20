---
title: Install the client with Azure AD
titleSuffix: Configuration Manager
description: Install and assign the Configuration Manager client on Windows 10 devices using Azure Active Directory for authentication
ms.custom: na
ms.date: 03/21/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby

---

# Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication

To install the Configuration Manager client on Windows 10 devices using Azure AD authentication, integrate Configuration Manager with Azure Active Directory (Azure AD). Clients can be on the intranet communicating directly with an HTTPS-enabled management point. They can also be internet-based communicating through the CMG or with an internet-based management point. This process uses Azure AD to authenticate clients to the Configuration Manager site. Azure AD replaces the need to configure and use client authentication certificates.



## Before you begin

- An Azure AD tenant is a prerequisite  

- Device requirements:  

    - Windows 10  

    - Joined to Azure AD, either pure cloud domain-joined, or hybrid Azure AD-joined  

- User requirements:  

    - The logged on user must be an Azure AD identity.   

	- If the user is a federated or synchronized identity, you must use Configuration Manager [Active Directory user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) as well as [Azure AD user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). For more information about hybrid identities, see [Define a hybrid identity adoption strategy](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- In addition to the [existing prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) for the management point site system role, also enable **ASP.NET 4.5** on this server. Include any other options that are automatically selected when enabling ASP.NET 4.5.  

- Configure all management points for HTTPS mode. For more information, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements) and [Deploy the web server certificate for site systems that run IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

- Optionally set up a [cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG) to deploy internet-based clients. For on-premises clients that authenticate with Azure AD, you don't need a CMG.  


## Configure Azure Services for Cloud Management

Connect your Configuration Manager site to Azure AD as the first step. For details of this process, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard). Create a connection to the **Cloud Management** service.

Enable [Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) as part of onboarding to **Cloud Management**. 

After you complete these actions, your Configuration Manager site is connected to Azure AD. 



## Configure client settings

These client settings help join Windows 10 devices with Azure AD. They also enable internet-based clients to use the CMG and cloud distribution point.

1.	Configure the following client settings in the **Cloud Services** section using the information in [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).  

	- **Allow access to cloud distribution point**: Enable this setting to help internet-based devices get the required content to install the Configuration Manager client. If the content isn't available on the cloud distribution point, devices can retrieve the content from the CMG. The client installation bootstrap retries the cloud distribution point for four hours before it falls back to the CMG.<!--495533-->  

	- **Automatically register new Windows 10 domain joined devices with Azure Active Directory**: Set to **Yes** or **No**. The default setting is **Yes**. This behavior is also the default in Windows 10, version 1709.

	- **Enable clients to use a cloud management gateway** – Set to **Yes** (default), or **No**.  

2.	Deploy the client settings to the required collection of devices. Do not deploy these settings to user collections.

To confirm the device is joined to Azure AD, run `dsregcmd.exe /status` in a command prompt. The **AzureAdjoined** field in the results shows **YES** if the device is Azure AD-joined.



## Install and register the client using Azure AD identity

To install the client, use the instructions in [How to deploy clients to Windows computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  <!--add anchor to AAD section-->

For more information on the Azure AD client installation properties, see [Client.msi Properties](/sccm/core/clients/deploy/about-client-installation-properties#clientMsiProps).



## Next steps

Once complete, you can continue to [monitor and manage clients](/sccm/core/clients/manage/monitor-clients).
