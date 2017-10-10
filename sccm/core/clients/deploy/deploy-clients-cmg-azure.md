---
title: "Install and assign the client from the internet"
description: "Install and assign the System Center Configuration Manager client from the internet."
ms.custom: na
ms.date: 8/07/2017
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
author: arob98
ms.author: angrobe
manager: angrobe

---

# Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication

You can use Configuration Manager cloud services with Azure AD to support the following scenarios:

- Manually install the Configuration Manager client on Windows 10 devices from the internet, and have it assign to a Configuration Manager site (requires the cloud management gateway site system role).
- Use Azure AD to authenticate clients to access your Configuration Manager sites. Azure AD replaces the need to configure and use client authentication certificates.
- Discover Azure AD users into your site to use in collections, and other Configuration Manager operations.

Use the following steps to help you accomplish this:

- **Step 1: Set up the Azure Services app in Configuration Manager Cloud Services and configure Azure AD User Discovery**
- **Step 2: Set up the Cloud Management Gateway** (optional for on-premises clients)
- **Step 3: Configure client settings to join Windows 10 devices with Azure AD and enable clients to use the Cloud Management Gateway**
- **Step 4: Install and register the Configuration Manager client using Azure Active Directory Identity**


## Before you start

- You must have an Azure AD tenant.
- Your devices must run Windows 10, be Azure AD joined, and be logged on using an Azure AD identity. Clients can also be domain joined in addition to Azure AD joined).
- In addition to the [existing prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) for the management point site system role, you must additionally ensure that **ASP.NET 4.5** (and any other options that are automatically selected) are enabled on the computer that hosts this site system role.
- To use Configuration Manager to deploy the client:
	- Configure at least one management point for HTTPS mode if you want to use Azure AD to authenticate instead of client certificates.
		If you are using client certificates instead of the Cloud Management Gateway, an HTTPS management point is optional, but recommended. If you are using Azure AD to authenticate, whether for on premises, or Internet clients, the HTTPS management point is required.
	- Set up a Cloud Management Gateway if you want to deploy Internet clients. For on-premises clients, that you are authenticating with Azure AD, you do not need to configure the Cloud Management Gateway.


## Step 1: Set up the Azure Services app in Configuration Manager Cloud Services

This connects your Configuration Manager site to Azure AD and is a prerequisite for all other operations in this section. 

Azure AD User Discovery is configured as part of *Cloud Management*. The procedure to do so is detailed in step **6** of the procedure [Create the Azure web app for use with Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) in the topic *Configure Azure services for use with Configuration Manager*.
	
After you complete the procedure, you have connected your Configuration Manager site to Azure AD. 

## Step 2: Set up the Cloud Management Gateway

Set up the Cloud Management Gateway to help enable the cloud management scenarios described in this topic. Find help in the following topics: 

- [Plan for cloud management gateway in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Set up cloud management gateway for Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Monitor cloud management gateway in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## Step 3: Configure client settings to join Windows 10 devices with Azure AD and enable clients to use the Cloud Management Gateway

1.	Configure the following client settings (found in the **Cloud Services**) section using the information in [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).
	- **Allow access to cloud distribution point** - Enable this setting to help Internet-based devices to get the required content to install the Configuration Manager client. If the content is not available on the cloud distribution point, devices can retrieve the content from a management point connected to the cloud management gateway.
	- **Automatically register new Windows 10 domain joined devices with Azure Active Directory** – Set to **Yes** (default), or **No**.
	- **Enable clients to use a cloud management gateway** – Set to **Yes** (default), or **No**.
2.	Deploy the client settings to the required collection of devices. Do not deploy these settings to user collections.

To confirm that the device is joined to Azure AD, run the command **dsregcmd.exe /status** in a command prompt window. The **AzureAdjoined** field in the results shows **YES** if the device is Azure AD joined.


## Step 4: Install and register the Configuration Manager client using Azure Active Directory Identity

To install the client, use the instructions in [How to deploy clients to Windows computers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) using the following installation command line: 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP** – Download source. Can set to CMG if bootstrap from internet.
- **CCMHOSTNAME:** The name of your Internet management point. You can find this by running **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** from a command prompt on a managed client.
- **SMSSiteCode:** The site code of your Configuration Manager site.
- **SMSMP:** The name of your lookup management point – the management point can be on your intranet.
- **AADTENANTID:**, **AADTENANTNAME:** The ID and name of the Azure AD tenant you linked to Configuration Manager. You can find this by running dsregcmd.exe /status from a command prompt on an Azure AD joined device.
- **AADCLIENTAPPID:** The Azure AD client app ID. For help finding this, see [Use portal to create an Azure Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri:** The identifier URI of the onboarded Azure AD server app. For more information, see [Configure Azure services for use with Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## Next steps

Once complete, you can continue to [monitor and manage clients](/sccm/core/clients/manage/monitor-clients).
